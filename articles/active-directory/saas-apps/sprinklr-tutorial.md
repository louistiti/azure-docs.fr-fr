---
title: 'Tutoriel : Intégration d’Azure Active Directory à Sprinklr | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 884cee735f6bf9f383b525890acf295040cc0c63
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55194625"
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Tutoriel : Intégration d’Azure Active Directory à Sprinklr

Dans ce didacticiel, vous allez apprendre à intégrer Sprinklr à Azure Active Directory (Azure AD).

L’intégration de Sprinklr dans Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à Sprinklr
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Sprinklr (par le biais de l’authentification unique) avec leur compte Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD à Sprinklr, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Sprinklr pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de Sprinklr à partir de la galerie
1. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sprinklr-from-the-gallery"></a>Ajout de Sprinklr à partir de la galerie
Pour configurer l’intégration de Sprinklr avec Azure AD, vous devez ajouter Sprinklr, disponible dans la galerie, à votre liste d’applications SaaS gérées.

**Pour ajouter Sprinklr à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

1. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![APPLICATIONS][2]
    
1. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![APPLICATIONS][3]

1. Dans la zone de recherche, entrez **Sprinklr**.

    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/tutorial_sprinklr_search.png)

1. Dans le volet de résultats, sélectionnez **Sprinklr**, puis cliquez sur **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sprinklr, avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Sprinklr correspondant dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Sprinklr associé doit être établie.

Dans Sprinklr, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec Sprinklr, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
1. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
1. **[Création d’un utilisateur de test Sprinklr](#creating-a-sprinklr-test-user)** pour avoir un équivalent de Britta Simon dans Sprinklr lié à la représentation Azure AD de l’utilisateur.
1. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** : permet à Britta Simon d’utiliser l’authentification unique Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Sprinklr.

**Pour configurer l’authentification unique Azure AD avec Sprinklr, procédez comme suit :**

1. Dans le portail Azure, sur la page d’intégration de l’application **Sprinklr**, cliquez sur **Authentification unique**.

    ![Configurer l'authentification unique][4]

1. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l'authentification unique](./media/sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

1. Dans la section **Domaine et URL Sprinklr**, procédez comme suit :

    ![Configurer l'authentification unique](./media/sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.sprinklr.com`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour les valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez l’[équipe de support technique Sprinklr](https://www.sprinklr.com/contact-us/). 
 
1. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configure Single Sign-On](./media/sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

1. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l'authentification unique](./media/sprinklr-tutorial/tutorial_general_400.png)

1. Dans la section **Configuration de Sprinklr**, cliquez sur **Configurer Sprinklr** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

1. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Sprinklr en tant qu’administrateur.

1. Accédez à **Administration \> Settings**.
   
    ![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")

1. Accédez à **Manager Partner \> Single Sign** dans le volet gauche.
   
    ![Gérer les partenaires](./media/sprinklr-tutorial/ic782908.png "Gérer les partenaires")

1. Cliquez sur **+Add Single Sign Ons**.
   
    ![Authentification unique](./media/sprinklr-tutorial/ic782909.png "Authentification unique")

1. Dans la page **Single Sign on** , procédez comme suit :
   
    ![Authentification unique](./media/sprinklr-tutorial/ic782910.png "Authentification unique")

    a. Dans la zone de texte **Name** (Nom), indiquez le nom de votre configuration (par exemple, *WAADSSOTest*).

    b. Sélectionnez **Enabled**.

    c. Sélectionnez **Use new SSO Certificate**.
             
    e. Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Identity provider certificate (Certificat du fournisseur d’identité)**.

    f. Dans la zone de texte **ID d’entité**, collez la valeur **ID d’entité SAML** que vous avez copié à partir du portail Azure.

    g. Collez la valeur **URL du service d’authentification unique SAML** copiée à partir du portail Azure dans la zone de texte **URL d’identification du fournisseur d’identité**.

    h. Collez la valeur **URL de déconnexion** copiée à partir du portail Azure dans la zone de texte **URL de déconnexion du fournisseur d’identité**.
     
    i. Dans **SAML User ID Type**, sélectionnez **Assertion contains User’s sprinklr.com username**.

    j. Dans **SAML User ID Location**, sélectionnez **User ID is in the Name Identifier element of the Subject statement**.

    k. Cliquez sur **Enregistrer**.
       
    ![SAML](./media/sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Pour en savoir plus sur la fonctionnalité de documentation incorporée, accédez à : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/create_aaduser_01.png) 

1. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/create_aaduser_02.png) 

1. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/create_aaduser_03.png) 

1. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/sprinklr-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-a-sprinklr-test-user"></a>Création d’un utilisateur de test Sprinklr

1. Connectez-vous à votre site d’entreprise Sprinklr en tant qu’administrateur.

1. Accédez à **Administration \> Settings**.
   
    ![Administration](./media/sprinklr-tutorial/ic782907.png "Administration")

1. Accédez à **Manage Client \> Users** dans le volet gauche.
   
    ![Paramètres](./media/sprinklr-tutorial/ic782914.png "Paramètres")

1. Cliquez sur **Add User**.
   
    ![Paramètres](./media/sprinklr-tutorial/ic782915.png "Paramètres")

1. Dans la page **Edit User** , procédez comme suit :
   
    ![Modifier l’utilisateur](./media/sprinklr-tutorial/ic782916.png "Modifier l’utilisateur") 

    a. Dans les zones de texte **Email**, **First Name** et **Last Name**, saisissez les informations du compte utilisateur Azure AD que vous souhaitez approvisionner.

    b. Sélectionnez **Password Disabled**.

    c. Sélectionner une **Langue**.

    d. Sélectionnez un **Type d’utilisateur**.

    e. Cliquez sur **Update**.
   
     >[!IMPORTANT]
     >**Password Disabled** pour permettre à un utilisateur de se connecter par le biais d’un fournisseur d’identité. 
     
1. Accédez à **Role**, puis procédez comme suit :
   
    ![Rôles de partenaires](./media/sprinklr-tutorial/ic782917.png "Rôles de partenaires")

    a. Dans la liste **Global**, sélectionnez **ALL\_Permissions**.  

    b. Cliquez sur **Update**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par Sprinklr, pour approvisionner des comptes utilisateur AAD. 

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Sprinklr.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à Sprinklr, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

1. Dans la liste des applications, sélectionnez **Sprinklr**.

    ![Configurer l'authentification unique](./media/sprinklr-tutorial/tutorial_sprinklr_app.png) 

1. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

1. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

1. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

1. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Sprinklr dans le volet d'accès, vous serez connecté automatiquement à votre application Sprinklr. Pour en savoir plus sur le volet d’accès, consultez l’article [Présentation du volet d’accès](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/sprinklr-tutorial/tutorial_general_203.png

