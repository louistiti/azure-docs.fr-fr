---
title: Organisation logique des ressources Azure à l’aide de balises | Microsoft Docs
description: Indique comment appliquer des balises afin d’organiser des ressources Azure dédiées à la facturation et à la gestion.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: conceptual
ms.date: 11/20/2018
ms.author: tomfitz
ms.openlocfilehash: aa3cd0305c1ac2db269dcc46243ec3da1232e6f6
ms.sourcegitcommit: 58dc0d48ab4403eb64201ff231af3ddfa8412331
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55079526"
---
# <a name="use-tags-to-organize-your-azure-resources"></a>Organisation des ressources Azure à l’aide de balises

[!INCLUDE [resource-manager-governance-tags](../../includes/resource-manager-governance-tags.md)]

Pour appliquer des balises aux ressources, l’utilisateur doit disposer de l’accès en écriture pour ce type de ressource. Pour appliquer des balises à tous les types de ressources, utilisez le rôle [Contributeur](../role-based-access-control/built-in-roles.md#contributor). Pour appliquer des balises à un seul type de ressource, utilisez le rôle Contributeur pour cette ressource. Par exemple, pour appliquer des balises aux machines virtuelles, utilisez le [collaborateur de machine virtuelle](../role-based-access-control/built-in-roles.md#virtual-machine-contributor).

[!INCLUDE [Handle personal data](../../includes/gdpr-intro-sentence.md)]

## <a name="powershell"></a>PowerShell

Les exemples de cet article nécessitent la version 6.0 ou ultérieure d’Azure PowerShell. Si vous ne disposez pas de la version 6.0 ou ultérieure, [mettez à jour votre version](/powershell/azure/install-az-ps).

Pour afficher les balises existantes pour un *groupe de ressources*, utilisez :

```azurepowershell-interactive
(Get-AzResourceGroup -Name examplegroup).Tags
```

Le script retourne les informations au format suivant :

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

Pour afficher les balises existantes pour une *ressource dont l’ID de ressource est spécifié*, utilisez :

```azurepowershell-interactive
(Get-AzResource -ResourceId /subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Storage/storageAccounts/<storage-name>).Tags
```

Alternativement, pour afficher les balises existantes pour une *ressource dont le nom et le groupe de ressources sont spécifiés*, utilisez :

```azurepowershell-interactive
(Get-AzResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

Pour obtenir *les groupes de ressources contenant une balise spécifique*, utilisez :

```azurepowershell-interactive
(Get-AzResourceGroup -Tag @{ Dept="Finance" }).ResourceGroupName
```

Pour obtenir *les ressources contenant une balise spécifique*, utilisez :

```azurepowershell-interactive
(Get-AzResource -Tag @{ Dept="Finance"}).Name
```

Pour obtenir *les ressources contenant un nom de balise spécifique*, utilisez :

```azurepowershell-interactive
(Get-AzResource -TagName Dept).Name
```

Chaque fois que vous appliquez des balises à une ressource ou un groupe de ressources, vous remplacez les balises existantes de cette ressource ou de ce groupe de ressources. Par conséquent, vous devez utiliser une approche différente selon que la ressource ou le groupe de ressources a des balises existantes.

Pour ajouter des balises à un *groupe de ressources ne contenant pas de balises existantes*, utilisez :

```azurepowershell-interactive
Set-AzResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

Pour ajouter des balises à un *groupe de ressources avec des balises existantes*, récupérez les balises existantes, ajoutez la nouvelle balise et réappliquez les balises :

```azurepowershell-interactive
$tags = (Get-AzResourceGroup -Name examplegroup).Tags
$tags.Add("Status", "Approved")
Set-AzResourceGroup -Tag $tags -Name examplegroup
```

Pour ajouter des balises à une *ressource ne contenant pas de balises existantes*, utilisez :

```azurepowershell-interactive
$r = Get-AzResource -ResourceName examplevnet -ResourceGroupName examplegroup
Set-AzResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceId $r.ResourceId -Force
```

Pour ajouter des balises à une *ressource avec des balises existantes*, utilisez :

```azurepowershell-interactive
$r = Get-AzResource -ResourceName examplevnet -ResourceGroupName examplegroup
$r.Tags.Add("Status", "Approved")
Set-AzResource -Tag $r.Tags -ResourceId $r.ResourceId -Force
```

Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *sans conserver les balises existantes*, utilisez le script suivant :

```azurepowershell-interactive
$groups = Get-AzResourceGroup
foreach ($g in $groups)
{
    Get-AzResource -ResourceGroupName $g.ResourceGroupName | ForEach-Object {Set-AzResource -ResourceId $_.ResourceId -Tag $g.Tags -Force }
}
```

Pour appliquer toutes les balises d’un groupe de ressources à ses ressources et *conserver les balises existantes sur les ressources qui ne sont pas des doublons*, utilisez le script suivant :

```azurepowershell-interactive
$group = Get-AzResourceGroup "examplegroup"
if ($null -ne $group.Tags) {
    $resources = Get-AzResource -ResourceGroupName $group.ResourceGroupName
    foreach ($r in $resources)
    {
        $resourcetags = (Get-AzResource -ResourceId $r.ResourceId).Tags
        if ($resourcetags)
        {
            foreach ($key in $group.Tags.Keys)
            {
                if (-not($resourcetags.ContainsKey($key)))
                {
                    $resourcetags.Add($key, $group.Tags[$key])
                }
            }
            Set-AzResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
        else
        {
            Set-AzResource -Tag $group.Tags -ResourceId $r.ResourceId -Force
        }
    }
}
```

Pour supprimer toutes les balises, utilisez une table de hachage vide :

```azurepowershell-interactive
Set-AzResourceGroup -Tag @{} -Name examplegroup
```

## <a name="azure-cli"></a>Azure CLI

Pour afficher les balises existantes pour un *groupe de ressources*, utilisez :

```azurecli
az group show -n examplegroup --query tags
```

Le script retourne les informations au format suivant :

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

Alternativement, pour afficher les balises existantes pour une *ressource dont le nom, le type et le groupe sont spécifiés*, utilisez :

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

Durant un bouclage sur une collection de ressources, vous préférez peut-être afficher la ressource par ID de ressource. Un exemple complet est présenté plus loin dans cet article. Pour afficher les balises existantes pour une *ressource dont l’ID de ressource est spécifié*, utilisez :

```azurecli
az resource show --id <resource-id> --query tags
```

Pour obtenir des groupes de ressources contenant une balise spécifique, utilisez `az group list` :

```azurecli
az group list --tag Dept=IT
```

Pour obtenir toutes les ressources contenant une balise et une valeur spécifiques, utilisez `az resource list` :

```azurecli
az resource list --tag Dept=Finance
```

Chaque fois que vous appliquez des balises à une ressource ou un groupe de ressources, vous remplacez les balises existantes de cette ressource ou de ce groupe de ressources. Par conséquent, vous devez utiliser une approche différente selon que la ressource ou le groupe de ressources a des balises existantes.

Pour ajouter des balises à un *groupe de ressources ne contenant pas de balises existantes*, utilisez :

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

Pour ajouter des balises à une *ressource ne contenant pas de balises existantes*, utilisez :

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

Pour ajouter des balises à une ressource qui comporte déjà les balises, récupérez les balises existantes et reformatez cette valeur, puis réappliquez les balises nouvelles et existantes :

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *sans conserver les balises existantes*, utilisez le script suivant :

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups
do
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv)
  for resid in $r
  do
    az resource tag --tags $t --id $resid
  done
done
```

Pour appliquer toutes les balises d’un groupe de ressources à ses ressources *en conservant les balises existantes*, utilisez le script suivant :

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups
do
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv)
  for resid in $r
  do
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done
done
```

## <a name="templates"></a>Modèles

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portail

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="rest-api"></a>API REST

Le portail Azure et PowerShell utilisent tous deux [l’API REST du Gestionnaire de ressources](https://docs.microsoft.com/rest/api/resources/) en arrière-plan. Si vous avez besoin d’intégrer le balisage dans un autre environnement, vous pouvez récupérer des balises en utilisant **GET** sur l’ID de ressource et mettre à jour le jeu de balises en utilisant un appel **PATCH**.

## <a name="tags-and-billing"></a>Balises et facturation

Vous pouvez utiliser des balises pour regrouper vos données de facturation. Par exemple, si vous exécutez plusieurs machines virtuelles pour différentes organisations, vous pouvez recourir aux balises pour regrouper l’utilisation par centre de coûts. Vous pouvez également utiliser des balises pour catégoriser les coûts par environnement d’exécution ; par exemple, l’utilisation de la facturation pour les machines virtuelles en cours d’exécution dans l’environnement de production.

Vous pouvez récupérer des informations sur les balises par le biais des [API Resource Usage et RateCard](../billing/billing-usage-rate-card-overview.md) ou du fichier de valeurs séparées par des virgules (CSV). Téléchargez le fichier d’utilisation depuis le [Centre des comptes Azure](https://account.azure.com/Subscriptions) ou depuis le portail Azure. Pour plus d’informations, consultez [Télécharger et consulter votre facture Azure et vos données d’utilisation quotidienne](../billing/billing-download-azure-invoice-daily-usage-date.md). Lorsque vous téléchargez le fichier d’utilisation depuis le Centre des comptes Azure, sélectionnez **Version 2**. Pour les services qui prennent en charge les balises avec la facturation, les balises s’affichent dans la colonne **Balises**.

Pour plus d’informations sur les opérations de l’API REST, consultez [Informations de référence sur l’API REST Azure Billing](/rest/api/billing/).

## <a name="next-steps"></a>Étapes suivantes

* Les types de ressources ne prennent pas tous en charge les étiquettes. Pour déterminer si vous pouvez appliquer une étiquette à un type de ressource, consultez [Prise en charge des étiquettes pour les ressources Azure](tag-support.md).
* Vous pouvez appliquer des restrictions et des conventions sur votre abonnement avec des stratégies personnalisées. La stratégie que vous définissez peut exiger que toutes les ressources aient une valeur pour une balise en particulier. Pour plus d’informations, consultez [Qu’est-ce qu’Azure Policy ?](../azure-policy/azure-policy-introduction.md)
* Pour plus d’informations sur l’utilisation du portail, consultez [Utilisation du portail Azure pour gérer vos ressources Azure](resource-group-portal.md).  
