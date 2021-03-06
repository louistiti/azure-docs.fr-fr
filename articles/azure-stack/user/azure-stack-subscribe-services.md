---
title: Dans ce didacticiel, vous allez apprendre à vous abonner à une offre Azure Stack | Microsoft Docs
description: Ce didacticiel explique comment créer un nouvel abonnement dans les services Azure Stack et comment tester l’offre en créant une machine virtuelle de test.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 11/13/2018
ms.author: sethm
ms.reviewer: unknown
ms.lastreviewed: 11/13/2018
ms.openlocfilehash: 4cc2adc334ede3f2377722137d4a6c84544bf425
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55251472"
---
# <a name="tutorial-create-and-test-a-subscription"></a>Didacticiel : créer et tester un abonnement

Ce didacticiel vous montre comment créer un abonnement qui contient une offre et comment la tester. Pour le test, connectez-vous au portail utilisateur Azure Stack en tant qu’administrateur cloud, abonnez-vous à l’offre, puis créez une machine virtuelle.

> [!TIP]
> Pour une expérience d’évaluation plus avancée, vous pouvez [créer un abonnement pour un utilisateur particulier](../azure-stack-subscribe-plan-provision-vm.md#create-a-subscription-as-a-cloud-operator), puis vous connecter en tant que cet utilisateur dans le portail utilisateur. 

Dans ce didacticiel, vous allez apprendre à vous abonner à une offre Azure Stack.

Contenu :

> [!div class="checklist"]
> * S’abonner à une offre 
> * Tester l’offre

## <a name="subscribe-to-an-offer"></a>S’abonner à une offre

Pour vous abonner à une offre en tant qu’utilisateur, connectez-vous au portail utilisateur Azure Stack afin de découvrir les services offerts par l’opérateur Azure Stack.

1. Connectez-vous au portail utilisateur et sélectionnez **Obtenir un abonnement**.

   ![Prendre un abonnement](media/azure-stack-subscribe-services/get-subscription.png)

2. Dans le champ **Nom d’affichage** , tapez un nom pour votre abonnement. Ensuite, sélectionnez **Offre** pour choisir l’une des offres disponibles dans la section **Choisir une offre**. Sélectionnez ensuite **Créer**.

   ![Créer une offre](media/azure-stack-subscribe-services/create-subscription.png)

   > [!TIP]
   > Vous devez maintenant actualiser le portail utilisateur pour commencer à utiliser votre abonnement.

3. Pour afficher l’abonnement que vous avez créé, sélectionnez **Tous les services**. Ensuite, dans la catégorie **GÉNÉRAL**, sélectionnez **Abonnements**, puis sélectionnez votre nouvel abonnement. Une fois que vous êtes abonné à une offre, actualisez le portail pour voir si les nouveaux services ont été ajoutés à votre nouvel abonnement. Dan cet exemple, **Machines virtuelles** a été ajouté.

   ![Afficher l’abonnement](media/azure-stack-subscribe-services/view-subscription.png)

## <a name="test-the-offer"></a>Tester l’offre

En étant connecté au portail utilisateur, vous pouvez tester l’offre en provisionnant une machine virtuelle à l’aide des fonctionnalités du nouvel abonnement. 

> [!NOTE]
> Ce test nécessite d’avoir ajouté une machine virtuelle Windows Server 2016 Datacenter à la place de marché Azure Stack. 

1. Connectez-vous au portail utilisateur.

2. Dans le portail utilisateur, sélectionnez **Machines virtuelles**, **Ajouter**, **Windows Server 2016 Datacenter**, puis cliquez sur **Créer**.

3. Dans la section **Bases**, tapez un **Nom**, un **Nom d’utilisateur** et un **Mot de passe**, choisissez un **Abonnement**, créez un **Groupe de ressources** (ou sélectionnez un groupe existant), puis sélectionnez **OK**.

4. Dans la section **Choisir une taille**, sélectionnez **A1 Standard**, puis cliquez sur **Sélectionner**.  

5. Dans le panneau **Paramètres**, acceptez les valeurs par défaut et sélectionnez **OK**.

6. Dans la section **Résumé**, cliquez sur **OK** pour créer la machine virtuelle.  

7. Pour voir votre nouvelle machine virtuelle, sélectionnez **Machines virtuelles**, puis recherchez la nouvelle machine virtuelle et cliquez sur son nom.

    ![Toutes les ressources](media/azure-stack-subscribe-services/view-vm.png)

> [!NOTE]
> Le déploiement de la machine virtuelle prend quelques minutes.


## <a name="next-steps"></a>Étapes suivantes

Ce que vous avez appris dans ce didacticiel :

> [!div class="checklist"]
> * S’abonner à une offre 
> * Tester l’offre


> [!div class="nextstepaction"]
> [Créer une machine virtuelle à partir d’un modèle de communauté](azure-stack-create-vm-template.md)