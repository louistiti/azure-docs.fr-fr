---
title: Aide sur la limitation de requêtes Azure Key Vault
description: La limitation Key Vault permet de réduire le nombre d’appels simultanés afin d’empêcher toute surexploitation des ressources.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: ''
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.topic: conceptual
ms.date: 05/10/2018
ms.author: bryanla
ms.openlocfilehash: 261a735a94aca23fe10bdab461a9619250f67f41
ms.sourcegitcommit: b4755b3262c5b7d546e598c0a034a7c0d1e261ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54884978"
---
# <a name="azure-key-vault-throttling-guidance"></a>Aide sur la limitation de requêtes Azure Key Vault

La limitation de requêtes est le processus permettant de réduire le nombre d’appels simultanés au service Azure afin d’empêcher toute surexploitation des ressources. Azure Key Vault (AKV) est conçu pour gérer un volume élevé de requêtes. En cas d’affluence, la limitation des requêtes du client permet de maintenir des performances et une fiabilité optimales pour le service AKV.

Les limites varient selon les scénarios. Par exemple, si vous réalisez un volume important d’écritures, la possibilité de limitation est plus élevée que si vous effectuez uniquement des lectures.

## <a name="how-does-key-vault-handle-its-limits"></a>Comment Key Vault gère-t-il ses limites ?

Les limites de service de Key Vault sont là pour empêcher tout usage abusif des ressources et garantir la qualité du service pour tous les clients de Key Vault. En cas de dépassement d’un seuil de service, Key Vault limite toutes les autres requêtes de ce client sur une période donnée. Dans ce cas, Key Vault retourne le code d’état HTTP 429 (Trop de requêtes), et les requêtes échouent. Par ailleurs, les requêtes qui ont échoué et retournent une erreur 429 sont comptabilisées dans les limites suivies par Key Vault. 

Si vous avez un scénario valide justifiant une limitation supérieure, contactez-nous.


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a>Guide pratique pour limiter une application en réponse à des limites de service

Voici les **meilleures pratiques** pour limiter une application :
- Réduisez le nombre d’opérations par requête.
- Réduisez la fréquence des requêtes.
- Évitez les nouvelles tentatives immédiates. 
    - Toutes les requêtes sont comptabilisées dans le cadre de vos limites d’utilisation.

Lorsque vous implémentez la gestion des erreurs de votre application, utilisez le code d’erreur HTTP 429 pour détecter si une limitation côté client est nécessaire. Si la requête échoue à nouveau avec un code d’erreur HTTP 429, cela signifie que vous rencontrez toujours une limite de service Azure. Continuez à utiliser la méthode de limitation côté client recommandée, en réessayant la requête jusqu’à ce qu’elle aboutisse.

Le code qui implémente un backoff exponentiel est montré ci-dessous. 
```
     public async Task OnGetAsync()
     {
         Message = "Your application description page.";
         int retries = 0;
         bool retry = false;
         do 
         {
             try
             {
                 AzureServiceTokenProvider azureServiceTokenProvider = new AzureServiceTokenProvider();
                 KeyVaultClient keyVaultClient = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(azureServiceTokenProvider.KeyVaultTokenCallback));
                 var secret = await keyVaultClient.GetSecretAsync("https://<YourKeyVaultName>.vault.azure.net/secrets/AppSecret")
                         .ConfigureAwait(false);
                 Message = secret.Value;
             }
             /// <exception cref="KeyVaultErrorException">
             /// Thrown when the operation returned an invalid status code
             /// </exception>
             catch (KeyVaultErrorException keyVaultException)
             {
                 Message = keyVaultException.Message;
                 if ((int)keyVaultException.Response.StatusCode == 429)
                 {
                    retry = true;

                    long waitTime = Math.Min(getWaitTime(retries), 2000000);
                    Thread.Sleep(new TimeSpan(waitTime));
                }
             }
         } while(retry && (retries++ < 10));         
         
     }

     // This method implements exponential backoff in case of 429 errors from Azure Key Vault
     private static long getWaitTime(int retryCount)
     {
        return (long)Math.Pow(2, retryCount) * 100L;
     }
```

### <a name="recommended-client-side-throttling-method"></a>Méthode de limitation côté client recommandée

En cas de code d’erreur HTTP 429, commencez à limiter votre client suivant une approche d’interruption exponentielle :

1. Patientez une seconde, relancez la requête ;
2. Si la limitation persiste, patientez deux secondes, relancez la requête ;
3. Si la limitation persiste, patientez quatre secondes, relancez la requête ;
4. Si la limitation persiste, patientez huit secondes, relancez la requête ;
5. Si la limitation persiste, patientez seize secondes, relancez la requête.

À ce stade, vous ne devriez pas recevoir de code de réponse HTTP 429.

## <a name="see-also"></a>Voir aussi

Pour orienter la limitation de façon plus approfondie sur Microsoft Cloud, consultez la page [Modèle de limitation](https://docs.microsoft.com/azure/architecture/patterns/throttling).

