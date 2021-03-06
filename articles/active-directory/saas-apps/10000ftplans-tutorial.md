---
title: 'Tutoriel : Intégration d’Azure Active Directory à 10,000ft Plans | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et 10,000ft Plans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: a9cb621598c198780916929681ab76b199e6ebb3
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55170740"
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a>Didacticiel : Intégration d’Azure Active Directory à 10,000ft Plans

Dans ce didacticiel, vous allez apprendre à intégrer 10,000ft Plans à Azure Active Directory (Azure AD).

L’intégration de 10,000ft Plans avec Azure AD vous offre les avantages suivants :

- Vous pouvez contrôler qui a accès à 10,000ft Plans dans Azure AD
- Vous pouvez permettre à vos utilisateurs de se connecter automatiquement à 10,000ft Plans (en connexion unique) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD avec 10,000ft Plans, vous devez disposer des éléments suivants :

- Un abonnement Azure AD
- Un abonnement à 10,000ft Plans pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’un mois.

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de 10,000ft Plans à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-10000ft-plans-from-the-gallery"></a>Ajout de 10,000ft Plans à partir de la galerie
Pour configurer l’intégration de 10,000ft Plans à Azure AD, vous devez ajouter 10,000ft Plans à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter 10,000ft Plans à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![APPLICATIONS][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![APPLICATIONS][3]

4. Dans la zone de recherche, tapez **10,000ft Plans**.

    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. Dans le panneau de résultats, sélectionnez **10,000ft Plans**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 10,000ft Plans avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur 10,000ft Plans équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur 10,000ft Plans associé doit être établie.

Dans 10,000ft Plans, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec 10,000ft Plans, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test 10,000ft Plans](#creating-a-10000ft-plans-test-user)** pour avoir un équivalent de Britta Simon dans 10,000ft Plans lié à sa représentation dans Azure AD.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** : permet à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application 10,000ft Plans.

**Pour configurer l’authentification unique Azure AD avec 10,000ft Plans, effectuez les étapes suivantes :**

1. Dans le portail Azure, dans la page d’intégration de l’application **10,000ft Plans**, cliquez sur **Authentification unique**.

    ![Configurer l'authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. Dans la section **Domaine et URL 10,000ft Plans**, effectuez les étapes suivantes :

    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez l’URL : `https://app.10000ft.com`

    b. Dans la zone de texte **Identificateur**, tapez l’URL : `https://app.10000ft.com/saml/metadata`

    > [!NOTE] 
    > La valeur de **l’identificateur** est différente si vous avez un domaine personnalisé. Pour obtenir cette valeur, contactez [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support). 
 
4. Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de 10,000ft Plans**, cliquez sur **Configurer 10,000ft** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. Pour configurer l’authentification unique côté **10,000ft Plans**, vous devez envoyer le **Certificat (brut) téléchargé, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Pour en savoir plus sur la fonctionnalité de documentation incorporée, accédez à : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/10000ftplans-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-a-10000ft-plans-test-user"></a>Création d’un utilisateur de test 10,000ft Plans

L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans 10,000ft Plans. 10,000ft Plans prend en charge l’approvisionnement juste-à-temps, option activée par défaut. Vous n’avez aucune opération à effectuer dans cette section. Un utilisateur est créé lors d’une tentative d’accès à 10,000ft Plans s’il n’existe pas déjà. 

> [!NOTE]
> Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support 10,000ft Plans](https://www.10000ft.com/plans/support).

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à 10,000ft Plans.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à 10,000ft Plans, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **10,000ft Plans**.

    ![Configurer l'authentification unique](./media/10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.  
Lorsque vous cliquez sur la vignette 10,000ft Plans dans le volet d’accès, vous devez être connecté automatiquement à votre application 10,000ft Plans.
 
## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/10000ftplans-tutorial/tutorial_general_203.png

