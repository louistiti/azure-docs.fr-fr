---
title: 'Tutoriel : Intégration d’Azure Active Directory à ASC Contracts | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et ASC Contracts.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 5737bd76e7809035f21103f45a20fa8306061f30
ms.sourcegitcommit: 98645e63f657ffa2cc42f52fea911b1cdcd56453
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54823298"
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a>Tutoriel : Intégration d’Azure Active Directory à ASC Contracts

Dans ce tutoriel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) à ASC Contracts.

L’intégration de ASC Contracts à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à ASC Contracts.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à ASC Contracts (par authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD à ASC Contracts, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement ASC Contracts pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de ASC Contracts à partir de la galerie
1. Configuration et test de l’authentification unique Azure AD

## <a name="adding-asc-contracts-from-the-gallery"></a>Ajout de ASC Contracts à partir de la galerie
Pour configurer l’intégration d’ASC Contracts à Azure AD, vous devez ajouter ASC Contracts, disponible dans la galerie, à votre liste d’applications SaaS gérées.

**Pour ajouter ASC Contracts à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

1. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![APPLICATIONS][2]
    
1. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![APPLICATIONS][3]

1. Dans la zone de recherche, tapez **ASC Contracts**.

    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/tutorial_asccontracts_search.png)

1. Dans le panneau de résultats, sélectionnez **ASC Contracts**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ASC Contracts, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ASC Contracts équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur ASC Contracts associé doit être établie.

Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans ASC Contracts.

Pour configurer et tester l’authentification unique Azure AD avec ASC Contracts, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
1. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
1. **[Création d’un utilisateur de test ASC Contracts](#creating-an-asc-contracts-test-user)** pour avoir un équivalent de Britta Simon dans ASC Contracts lié à la représentation Azure AD de l’utilisateur.
1. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** : permet à Britta Simon d’utiliser l’authentification unique Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ASC Contracts.

**Pour configurer l’authentification unique Azure AD avec ASC Contracts, procédez comme suit :**

1. Dans le portail Azure, sur la page d’intégration de l’application **ASC Contracts**, cliquez sur **Authentification unique**.

    ![Configurer l'authentification unique][4]

1. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l'authentification unique](./media/asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

1. Dans la section **Domaine et URL ASC Contracts**, procédez comme suit :

    ![Configurer l'authentification unique](./media/asccontracts-tutorial/tutorial_asccontracts_url.png)

    a. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.asccontracts.com/shibboleth`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.asccontracts.com/shibboleth.sso/login`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels. Contactez l’équipe ASC Networks Inc. (ASC) au **613.599.6178** pour obtenir ces valeurs.

1. Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Configure Single Sign-On](./media/asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

1. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l'authentification unique](./media/asccontracts-tutorial/tutorial_general_400.png)

1. Pour configurer l’authentification unique côté **ASC Contracts**, appelez le support ASC Networks Inc. (ASC) au **613.599.6178** et fournissez le fichier **XML des métadonnées** téléchargé. Ils effectuent les réglages nécessaires sur l’application pour que la connexion SSO SAML soit définie correctement des deux côtés.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Pour en savoir plus sur la fonctionnalité de documentation incorporée, accédez à : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/create_aaduser_01.png) 

1. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/create_aaduser_02.png) 

1. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/create_aaduser_03.png) 

1. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/asccontracts-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-an-asc-contracts-test-user"></a>Création d’un utilisateur de test ASC Contracts

Collaborez avec l’équipe de support ASC Networks Inc. (ASC) au **613.599.6178** pour lui demander d’ajouter les utilisateurs dans la plateforme ASC Contracts.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ASC Contracts.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à ASC Contracts, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

1. Dans la liste des applications, sélectionnez **ASC Contracts**.

    ![Configurer l'authentification unique](./media/asccontracts-tutorial/tutorial_asccontracts_app.png) 

1. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

1. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

1. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

1. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette ASC Contracts dans le volet d’accès, vous devez être connecté automatiquement à votre application ASC Contracts. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/asccontracts-tutorial/tutorial_general_203.png
