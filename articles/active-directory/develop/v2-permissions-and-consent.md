---
title: Étendues, autorisations et consentement Azure Active Directory v2.0 | Microsoft Docs
description: Une description de l’autorisation dans le point de terminaison v2.0 Azure AD, relative notamment aux étendues, aux autorisations et aux consentements.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.subservice: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/24/2018
ms.author: celested
ms.reviewer: hirsin, jesakowi, justhu
ms.custom: aaddev
ms.openlocfilehash: 94a8cb5f0764ac1ed7330fb75131d3084d804f1e
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55091932"
---
# <a name="permissions-and-consent-in-the-azure-active-directory-v20-endpoint"></a>Autorisations et consentement dans le point de terminaison Azure Active Directory v2.0

[!INCLUDE [active-directory-develop-applies-v2](../../../includes/active-directory-develop-applies-v2.md)]

Les applications qui s’intègrent à la plateforme d’identité Microsoft suivent un modèle d’autorisation permettant aux utilisateurs et aux administrateurs de contrôler l’accès aux données. L’implémentation de ce modèle d’autorisation a été mise à jour sur le point de terminaison v2.0, et elle modifie la façon dont une application doit interagir avec la plateforme d’identité Microsoft. Cet article aborde les concepts de base de ce modèle d’autorisation, notamment les étendues, les autorisations et le consentement.

> [!NOTE]
> Le point de terminaison v2.0 ne prend pas en charge l’intégralité des scénarios et fonctionnalités. Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limitations de v2.0](active-directory-v2-limitations.md).

## <a name="scopes-and-permissions"></a>Étendues et autorisations

La plateforme d’identité Microsoft implémente le protocole d’autorisation [OAuth 2.0](active-directory-v2-protocols.md). OAuth 2.0 est une méthode par le biais de laquelle une application tierce peut accéder aux ressources hébergées sur le web au nom d’un utilisateur. Les ressources hébergées sur le web qui s’intègrent à la plateforme d’identité Microsoft présentent un identificateur de ressource, également appelé *URI d’ID d’application*. Voici, par exemple, quelques-unes des ressources hébergées sur le Web de Microsoft :

* Microsoft Graph : `https://graph.microsoft.com`
* API de messagerie Office 365 : `https://outlook.office.com`
* Azure AD Graph : `https://graph.windows.net`

> [!NOTE]
> Nous vous recommandons fortement d’utiliser Microsoft Graph au lieu d’Azure AD Graph, l’API de messagerie Office 365, etc.

Cela s’applique également aux ressources tierces intégrées à la plateforme d’identité Microsoft. Ces ressources peuvent également définir un ensemble d’autorisations à utiliser pour diviser la fonctionnalité de cette ressource en fragments plus réduits. Par exemple, [Microsoft Graph](https://graph.microsoft.com) a défini des autorisations pour effectuer les tâches suivantes, entre autres :

* Lire le calendrier d’un utilisateur
* Écrire dans le calendrier d’un utilisateur
* Envoi de messages en tant qu’utilisateur

En définissant ces types d’autorisations, la ressource dispose d’un contrôle précis sur ses données et sur l’exposition de la fonctionnalité d’API. Une application tierce peut demander ces autorisations à des utilisateurs et des administrateurs. Ces derniers doivent approuver la requête avant que l’application puisse accéder aux données ou agir pour le compte d’un utilisateur. En fragmentant les fonctionnalités de la ressource en ensembles plus réduits d’autorisations, il est possible de créer des applications tierces pour qu’elles demandent uniquement les autorisations nécessaires à leur fonctionnement. Les utilisateurs et les administrateurs peuvent connaître avec précision les données auxquelles l’application a accès, et être ainsi moins inquiets quant à une éventuelle intention malveillante. Les développeurs doivent toujours respecter le concept de moindre privilège et demander uniquement les autorisations dont ils ont besoin pour faire fonctionner leurs applications.

Dans OAuth, ces types d’autorisations sont appelés des *étendues*. On y fait également référence simplement sous le nom d’*autorisations*. Une autorisation est représentée dans la plateforme d’identité Microsoft sous forme de valeur de chaîne. Toujours dans l’exemple Microsoft Graph, la valeur de chaîne pour chaque autorisation est la suivante :

* Lire le calendrier d’un utilisateur en utilisant `Calendars.Read`
* Écrire dans le calendrier d’un utilisateur en utilisant `Calendars.ReadWrite`
* Envoi de messages en tant qu’utilisateur en utilisant `Mail.Send`

Généralement, une application peut demander ces autorisations en spécifiant les étendues dans les requêtes dirigées vers le point de terminaison d’autorisation v2.0. Toutefois, certaines autorisations à privilèges élevés peuvent uniquement être accordées par le biais du consentement de l’administrateur. Elles sont généralement demandées/accordées à l’aide du [point de terminaison de consentement de l’administrateur](v2-permissions-and-consent.md#admin-restricted-scopes). Lisez la suite pour en savoir plus.

## <a name="permission-types"></a>Types d'autorisations

La plateforme d’identité Microsoft prend en charge deux types d’autorisations : les **autorisations déléguées** et les **autorisations d’application**.

* Les **autorisations déléguées** sont utilisées par les applications pour lesquelles un utilisateur est connecté et présent. Pour ces applications, l’utilisateur ou un administrateur accorde les autorisations que l’application demande. Ensuite, l’application se voit déléguer une autorisation d’agir pour le compte de l’utilisateur connecté lors des appels à une ressource cible. Certaines autorisations déléguées peuvent être accordées par des utilisateurs non administrateurs, mais certaines autorisations à privilèges élevés requièrent le [consentement de l’administrateur](v2-permissions-and-consent.md#admin-restricted-scopes). Pour connaître les rôles administrateur habilités à donner leur consentement pour les autorisations déléguées, consultez [Autorisations du rôle administrateur dans Azure AD](../users-groups-roles/directory-assign-admin-roles.md).

* Les **autorisations d’application** sont utilisées par les applications qui s’exécutent sans qu’un utilisateur soit connecté et présent (les applications qui s’exécutent en tant que services ou démons en arrière-plan, par exemple).  Les autorisations de l’application peuvent uniquement être [accordées par un administrateur](v2-permissions-and-consent.md#requesting-consent-for-an-entire-tenant).

Les _autorisations effectives_ correspondent aux autorisations accordées à votre application lorsqu’elle envoie des requêtes à une ressource cible. Vous devez comprendre la différence entre les autorisations déléguées, les autorisations d’application et les autorisations effectives que votre application reçoit lorsqu’elle interroge la ressource cible.

- Pour les autorisations déléguées, les _autorisations effectives_ de votre application correspondent au niveau de privilège le moins élevé entre les autorisations déléguées que l’application a reçues (par le biais d’un consentement) et les privilèges de l’utilisateur actuellement connecté. Votre application ne peut jamais avoir plus de privilèges que l’utilisateur connecté. Au sein des organisations, les privilèges de l’utilisateur connecté peuvent être déterminés par la stratégie ou l’appartenance à un ou plusieurs rôles d’administrateur. Pour connaître les rôles administrateur habilités à donner leur consentement pour les autorisations déléguées, consultez [Autorisations du rôle administrateur dans Azure AD](../users-groups-roles/directory-assign-admin-roles.md).
  Supposons que votre application ait reçu l’autorisation déléguée _User.ReadWrite.All_. Cette autorisation permet nominalement à votre application de lire et mettre à jour le profil de chaque utilisateur dans une organisation. Si l’utilisateur connecté est un administrateur général, votre application est en mesure de mettre à jour le profil de chaque utilisateur de l’organisation. Toutefois, si l’utilisateur connecté n’a pas de rôle d’administrateur, votre application peut uniquement mettre à jour le profil de l’utilisateur connecté. Elle ne peut pas mettre à jour les profils des autres utilisateurs de l’organisation, car l’utilisateur pour lequel elle est autorisée à agir n’a pas ces privilèges.
  
- Pour les autorisations d’application, les _autorisations effectives_ de votre application correspondent au niveau complet des privilèges impliqués par l’autorisation. Par exemple, une application disposant de l’autorisation d’application _User.ReadWrite.All_ peut mettre à jour le profil de chaque utilisateur de l’organisation. 

## <a name="openid-connect-scopes"></a>Étendues OpenId Connect

L’implémentation v2.0 d’OpenID Connect comprend quelques étendues bien définies qui ne s’appliquent pas à une ressource particulière : `openid`, `email`, `profile` et `offline_access`.

### <a name="openid"></a>openid

Si une application exécute la connexion à l’aide [d’OpenID Connect](active-directory-v2-protocols.md), elle doit solliciter l’étendue `openid`. L’étendue `openid` s’affiche sur la page de consentement du compte professionnel, en tant qu’autorisation de connexion, et sur la page de consentement du compte Microsoft personnel en tant qu’autorisation « Afficher votre profil et se connecter aux applications et aux services à l’aide de votre compte Microsoft ». Avec cette autorisation, une application peut recevoir un identifiant utilisateur unique sous la forme de la revendication `sub`. Elle permet également à l’application d’accéder au point de terminaison des informations utilisateur. L’étendue `openid` peut être utilisée sur le point de terminaison de jeton v2.0 afin d’acquérir des jetons d’ID, qui peuvent être sollicités pour sécuriser les appels HTTP entre différents composants d’une application.

### <a name="email"></a>email

L’étendue `email` peut être utilisée avec l’étendue `openid` ainsi que d’autres. Elle permet à l’application d’accéder à l’adresse de messagerie principale de l’utilisateur sous la forme de la revendication `email`. La revendication `email` est incluse dans un jeton uniquement si une adresse de messagerie est associée au compte d’utilisateur, ce qui n’est pas toujours le cas. Si elle utilise l’étendue `email`, votre application doit être préparée à faire face à l’éventualité où la revendication `email` n’existerait pas dans le jeton.

### <a name="profile"></a>Profil

L’étendue `profile` peut être utilisée avec l’étendue `openid` ainsi que d’autres. Elle permet à l’application d’accéder à une quantité d’informations importante sur l’utilisateur, notamment le prénom de l’utilisateur, son nom de famille, son nom d’utilisateur privilégié et l’ID d’objet. Pour obtenir la liste complète des revendications de profil disponibles dans le paramètre id_token pour un utilisateur donné, consultez la page [de référence `id_tokens`](id-tokens.md).

### <a name="offlineaccess"></a>offline_access

[L’étendue `offline_access`](https://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) permet à votre application d’accéder aux ressources pour le compte de l’utilisateur pendant une période prolongée. Dans la page de consentement du compte professionnel, cette étendue apparaît en tant qu’autorisation « Accéder à vos données à tout moment ». Dans la page de consentement du compte Microsoft personnel, elle apparaît en tant qu’autorisation « Accéder à vos informations à tout moment ». Lorsqu’un utilisateur approuve l’étendue `offline_access`, votre application peut recevoir les jetons d’actualisation du point de terminaison des jetons v2.0. Les jetons d’actualisation sont de longue durée. Votre application peut obtenir de nouveaux jetons d’accès lorsque les plus anciens arrivent à expiration.

Si votre application ne sollicite pas l’étendue `offline_access`, elle ne reçoit pas de jetons d’actualisation. Ainsi, lorsque vous échangez un code d’autorisation dans le [flux de code d’autorisation OAuth 2.0](active-directory-v2-protocols.md), vous recevez uniquement un jeton d’accès du point de terminaison `/token`. Le jeton d’accès est valide pendant une courte durée : il arrive généralement à expiration en une heure. À ce stade, votre application doit rediriger l’utilisateur vers le point de terminaison `/authorize` afin de récupérer un nouveau code d’autorisation. Pendant ce réacheminement, en fonction du type d’application, l’utilisateur peut devoir entrer à nouveau ses informations d’identification ou accepter une nouvelle fois les autorisations.

Pour en savoir plus sur la récupération et l’utilisation des jetons d’actualisation, consultez la page de [référence sur les protocoles v2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Demande de consentement d’utilisateur individuel

Dans une demande d’autorisation [OpenID Connect ou OAuth 2.0](active-directory-v2-protocols.md), une application peut demander les autorisations nécessaires à l’aide du paramètre de requête `scope`. Par exemple, lorsqu’un utilisateur se connecte à une application, cette dernière envoie une requête semblable à l’exemple ci-dessous (avec des sauts de ligne ajoutés pour une meilleure lisibilité) :

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendars.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Le paramètre `scope` correspond à une liste d’autorisations déléguées séparées par des espaces, demandées par l’application. Chaque autorisation est indiquée par l’ajout de la valeur correspondante à l’identificateur de la ressource (URI d’ID d’application). Dans l’exemple de requête, l’application nécessite l’autorisation de lecture du calendrier de l’utilisateur et d’envoi de messages au nom de l’utilisateur.

Une fois que l’utilisateur a entré ses informations d’identification, le point de terminaison v2.0 recherche un enregistrement correspondant de *consentement d’utilisateur*. Si, par le passé, l’utilisateur n’a jamais accepté les autorisations demandées et qu’un administrateur n’a jamais accepté ces autorisations pour le compte de toute l’organisation, le point de terminaison v2.0 demande à l’utilisateur d’accorder les autorisations demandées.

![Consentement dans le compte professionnel](./media/v2-permissions-and-consent/work_account_consent.png)

Lorsque l’utilisateur approuve la demande d’autorisation, le consentement est enregistré de manière à ce que l’utilisateur n’ait pas à le fournir à nouveau lors des connexions suivantes à l’application.

## <a name="requesting-consent-for-an-entire-tenant"></a>Demande de consentement d’un client entier

Souvent, lorsqu’une organisation achète une licence ou un abonnement à une application, elle souhaite configurer proactivement l’application afin que tous les membres de l’organisation puissent l’utiliser. Dans le cadre de cette procédure, un administrateur peut autoriser l’application à agir au nom de n’importe quel utilisateur au sein du locataire. Si l’administrateur donne son consentement pour l’intégralité du locataire, les utilisateurs de l’organisation ne voient pas de page de consentement pour l’application.

Pour demander le consentement pour les autorisations déléguées pour tous les utilisateurs d’un locataire, votre application peut utiliser le point de terminaison de consentement de l’administrateur.

En outre, les applications doivent utiliser le point de terminaison de consentement de l’administrateur pour demander les autorisations d’application.

## <a name="admin-restricted-permissions"></a>Autorisations restreintes aux administrateurs

Certaines autorisations à privilège élevé de l’écosystème Microsoft peuvent être définies sur *restreintes aux administrateurs*. Ces types d’autorisations peuvent être illustrés par ces exemples :

* Lire les profils complets de tous les utilisateurs à l’aide de `User.Read.All`
* Écrire des données dans le répertoire d’une organisation à l’aide de `Directory.ReadWrite.All`
* Lire tous les groupes dans le répertoire d’une organisation à l’aide de `Groups.Read.All`

Si un utilisateur consommateur peut accorder à une application l’accès à ce type de données, les utilisateurs d’organisation sont limités lorsqu’il s’agit d’octroyer l’accès au même jeu de données d’entreprise sensibles. Si votre application requiert l’accès à l’une de ces autorisations d’un utilisateur de l’organisation, ce dernier recevra un message erreur indiquant qu’il n’est pas autorisé à donner son consentement pour les autorisations de votre application.

Si votre application requiert l’accès aux étendues restreintes aux administrateurs pour les organisations, vous devez demander l’autorisation directement à un administrateur d’entreprise également à l’aide du point de terminaison de consentement de l’administrateur, décrit ci-dessous.

Si l’application demande des autorisations déléguées à privilèges élevés et qu’un administrateur accorde ces autorisations via le point de terminaison de consentement de l’administrateur, le consentement est accordé à tous les utilisateurs du locataire.

Si l’application demande des autorisations d’application et qu’un administrateur accorde ces autorisations via le point de terminaison de consentement de l’administrateur, cette attribution n’est pas effectuée pour le compte d’un utilisateur spécifique. L’application cliente reçoit les autorisations *directement*. Ces types d’autorisations sont généralement uniquement utilisés par les services démon et d’autres applications non interactives qui s’exécutent en arrière-plan.

## <a name="using-the-admin-consent-endpoint"></a>Utilisation du point de terminaison de consentement administrateur

Lorsqu’un administrateur d’entreprise utilise votre application et qu’il est dirigé vers le point de terminaison d’autorisation, la plateforme d’identité Microsoft détecte le rôle de l’utilisateur et lui demande s’il souhaite donner son consentement pour le compte de l’intégralité du locataire pour les autorisations que vous avez demandées. Toutefois, il existe également un point de terminaison de consentement de l’administrateur dédié que vous pouvez utiliser si vous souhaitez demander proactivement qu’un administrateur accorde son autorisation pour le compte de l’intégralité du locataire. Vous devez également utiliser ce point de terminaison pour demander des autorisations d’application (qui ne peuvent pas être demandées à l’aide du point de terminaison d’autorisation).

Si vous suivez ces étapes, votre application peut demander des autorisations pour tous les utilisateurs d’un locataire, notamment les étendues restreintes aux administrateurs. Il s’agit d’une opération à privilèges élevés qui doit être effectuée uniquement si elle est nécessaire dans votre scénario.

Pour voir un exemple de code qui implémente les étapes, consultez [l’exemple d’étendues restreintes aux administrateurs](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-the-permissions-in-the-app-registration-portal"></a>Demander les autorisations dans le portail d’inscription de l’application

Le consentement de l’administrateur n’accepte de paramètre d’étendue. Ainsi, toute autorisation demandée doit être définie de manière statique dans l’inscription de l’application. En général, il est recommandé de veiller à ce que les autorisations définies de manière statique pour une application donnée constituent un sur-ensemble des autorisations qui seront demandées de façon dynamique/incrémentielle.

Pour configurer la liste des autorisations demandées de manière statique pour une application : 
1. Accédez à votre application dans le [portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou [créez une application](quickstart-v2-register-an-app.md) si ce n’est déjà fait.
2. Recherchez la section **Autorisations pour Microsoft Graph**, puis ajoutez les autorisations nécessaires à votre application.
3. **Enregistrez** l’inscription de l’application.

### <a name="recommended-sign-the-user-in-to-your-app"></a>Recommandé : connectez l’utilisateur à votre application

En général, lorsque vous créez une application qui utilise le point de terminaison de consentement de l’administrateur, l’application doit disposer d’une page ou vue dans laquelle l’administrateur peut approuver ses autorisations. Cette page peut faire partie du flux d’inscription de l’application, des paramètres de l’application, ou ce peut être un flux de connexion dédié. Dans de nombreux cas, il est judicieux pour l’application d’afficher la vue de « connexion » uniquement après qu’un utilisateur se soit connecté avec un compte Microsoft professionnel ou scolaire.

Lorsque vous connectez l’utilisateur à votre application, vous pouvez identifier l’organisation à laquelle l’administrateur appartient, avant de lui demander d’approuver les autorisations nécessaires. Même si cela n’est pas strictement nécessaire, cela peut vous aider à créer une expérience plus intuitive pour les utilisateurs de l’organisation. Pour connecter l’utilisateur, suivez nos [didacticiels sur le protocole v2.0](active-directory-v2-protocols.md).

### <a name="request-the-permissions-from-a-directory-admin"></a>Demander les autorisations à un administrateur d’annuaire

Lorsque vous êtes prêt à demander les autorisations à l’administrateur de votre organisation, vous pouvez rediriger l’utilisateur vers le *point de terminaison de consentement de l’administrateur* v2.0.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting the below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Paramètre | Condition | Description |
| --- | --- | --- |
| `tenant` | Obligatoire | Le client d’annuaire auquel vous souhaitez demander l’autorisation. Peut être fourni au format GUID ou sous forme de nom convivial OU référencé de manière générique avec « common » comme indiqué dans l’exemple. |
| `client_id` | Obligatoire | ID d’application que le [portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) a affecté à votre application. |
| `redirect_uri` | Obligatoire |URI de redirection où vous souhaitez que la réponse soit envoyée pour être gérée par votre application. Il doit correspondre exactement à l’un des URI de redirection que vous avez inscrits dans le portail d’inscription des applications. |
| `state` | Recommandé | Une valeur incluse dans la requête, qui sera également renvoyée dans la réponse de jeton. Il peut s’agir d’une chaîne du contenu de votre choix. Utilisez l’état pour encoder les informations sur l’état de l’utilisateur dans l’application avant la requête d’authentification, comme la page ou la vue sur laquelle ou laquelle il était positionné. |

À ce stade, Azure AD nécessite qu’un administrateur client se connecte pour terminer la demande. L’administrateur est invité à approuver toutes les autorisations que vous avez demandées pour votre application dans le portail d’inscription.

#### <a name="successful-response"></a>Réponse correcte

Si l’administrateur approuve les autorisations pour votre application, la réponse correcte ressemble à ce qui suit :

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Paramètre | Description |
| --- | --- | --- |
| `tenant` | Client d’annuaire ayant accordé à votre application les autorisations demandées au format GUID. |
| `state` | Une valeur incluse dans la requête qui sera également renvoyée dans la réponse de jeton. Il peut s’agir d’une chaîne du contenu de votre choix. La valeur d’état est utilisée pour coder les informations sur l’état de l’utilisateur dans l’application avant la requête d’authentification, comme la page ou l’écran sur lequel ou laquelle il était positionné. |
| `admin_consent` | Est défini sur **true**. |

#### <a name="error-response"></a>Réponse d’erreur

Si l’administrateur n’approuve pas les autorisations pour votre application, la réponse d’échec ressemble à ce qui suit :

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Paramètre | Description |
| --- | --- | --- |
| `error` |Une chaîne de code d’erreur pouvant être utilisée pour classer les types d’erreur se produisant, et pouvant être utilisée pour intervenir face aux erreurs. |
| `error_description` |Un message d’erreur spécifique qui peut aider un développeur à identifier la cause principale d’une erreur. |

Une fois que vous avez reçu une réponse correcte du point de terminaison de consentement de l’administrateur, votre application a acquis les autorisations qu’elle avait demandées. Vous pouvez alors demander un jeton pour la ressource souhaitée.

## <a name="using-permissions"></a>Utilisation des autorisations

Une fois que l’utilisateur accepte les autorisations pour votre application, cette dernière peut acquérir des jetons d’accès représentant l’autorisation de votre application à accéder, dans une certaine capacité, à une ressource. Un jeton d’accès peut être utilisé pour une ressource uniquement, mais l’encodage de ce jeton comporte les informations relatives à toutes les autorisations octroyées pour cette ressource à votre application. Pour acquérir un jeton d’accès, votre application peut transmettre une requête au point de terminaison de jeton v2.0 :

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

Vous pouvez utiliser le jeton d’accès obtenu dans les requêtes HTTP transmises à la ressource. Il indique de façon fiable à la ressource que votre application dispose de l’autorisation appropriée pour effectuer une tâche spécifique. 

Pour en savoir plus sur le protocole OAuth 2.0 et sur le mode d’obtention des jetons d’accès, consultez la page de [référence sur les protocoles du point de terminaison v2.0](active-directory-v2-protocols.md).

## <a name="troubleshooting"></a>Résolution de problèmes

Si vous, ou les utilisateurs de votre application, constatez des erreurs inattendues au cours du processus de consentement, consultez cet article pour connaître les étapes de dépannage : [Erreur inattendue lors du consentement à une application](../manage-apps/application-sign-in-unexpected-user-consent-error.md).
