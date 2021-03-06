---
title: 'Démarrage rapide : Reconnaissance vocale, Node.js - Services de reconnaissance vocale'
titleSuffix: Azure Cognitive Services
description: Utilisez ce guide pour créer une application console de reconnaissance vocale à l’aide du SDK Speech pour Node.js. Lorsque vous avez terminé, vous pouvez utiliser le microphone de l’ordinateur pour une retranscription vocale en temps réel.
services: cognitive-services
author: fmegen
manager: cgronlun
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: quickstart
ms.date: 1/16/2019
ms.author: fmegen
ms.openlocfilehash: c9f83368a540003e8bcc35282c664ec23e4ff068
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55226500"
---
# <a name="quickstart-recognize-speech-with-the-speech-sdk-for-nodejs"></a>Démarrage rapide : Reconnaissance vocale à l’aide du SDK Speech pour Node.js

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

Dans cet article, vous allez apprendre à créer un projet Node.js en utilisant la liaison JavaScript du SDK Speech de Cognitive Services pour transcrire la parole en texte.
L’application est basée sur le [SDK Speech de Microsoft Cognitive Services](https://aka.ms/csspeech/npmpackage).

## <a name="prerequisites"></a>Prérequis

* Clé d’abonnement Azure pour le service Speech. [Vous pouvez en obtenir une gratuitement](get-started.md).
* Version actuelle de [Node.js](https://nodejs.org).

## <a name="create-a-new-project"></a>Création d'un projet

Créez un dossier et initialisez le projet.

```sh
npm init -f
```

Le fichier package.json est alors initialisé avec les valeurs par défaut. Vous serez probablement amené à modifier ce fichier par la suite.

## <a name="install-the-speech-sdk"></a>Installer le Kit de développement logiciel (SDK) Speech

Ajoutez le SDK Speech à votre projet Node.js.

```
npm install microsoft-cognitiveservices-speech-sdk
```

La dernière version du SDK Speech et tous les prérequis seront téléchargés à partir de npmjs, puis installés. Le SDK est installé dans le répertoire `node_modules` à l’intérieur de votre dossier de projet.

## <a name="use-the-speech-sdk"></a>Utiliser le SDK Speech

Créez un fichier nommé `index.js` dans le dossier, puis ouvrez-le dans un éditeur de texte.

> [!NOTE]
> Dans Node.js, notez que le SDK Speech ne prend en charge ni le microphone ni le type de données Fichier. Ceux-ci ne sont pris en charge que sur les navigateurs. Utilisez plutôt l’interface Stream pour accéder au SDK Speech, au moyen de `AudioInputStream.createPushStream()` ou de `AudioInputStream.createPullStream()`.

Dans cet exemple, nous allons utiliser l’interface `PushAudioInputStream`.

Ajoutez le code JavaScript suivant :

[!code-javascript[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/js-node/index.js#code)]

## <a name="run-the-sample"></a>Exécution de l'exemple

Pour lancer l’application, adaptez `YourSubscriptionKey`, `YourServiceRegion`, et `YourAudioFile.wav` à votre configuration. Vous pouvez ensuite l’exécuter en appelant la commande suivante :

```sh
node index.js
```

Cette commande déclenche une reconnaissance à l’aide du nom de fichier fourni et présente la sortie dans la console.

Voici un exemple de sortie résultant de l’exécution d’`index.js` après la mise à jour de la clé d’abonnement et l’utilisation du fichier `whatstheweatherlike.wav`.

```json
SpeechRecognitionResult {
  "privResultId": "9E30EEBD41AC4571BB77CF9164441F46",
  "privReason": 3,
  "privText": "What's the weather like?",
  "privDuration": 15900000,
  "privOffset": 300000,
  "privErrorDetails": null,
  "privJson": {
    "RecognitionStatus": "Success",
    "DisplayText": "What's the weather like?",
    "Offset": 300000,
    "Duration": 15900000
  },
  "privProperties": null
}
```

## <a name="install-and-use-the-speech-sdk-with-visual-studio-code"></a>Installer et utiliser le SDK Speech avec Visual Studio Code

Vous pouvez également exécuter l’exemple à partir de Visual Studio Code. Suivez ces étapes pour installer, ouvrir et exécuter le guide de démarrage rapide :

1. Démarrez Visual Studio Code et cliquez sur « Ouvrir le dossier », puis accédez au dossier de démarrage rapide.

   ![Capture d’écran de l’ouverture du dossier](media/sdk/qs-js-node-01-open_project.png)

1. Ouvrez un terminal dans Visual Studio Code.

   ![Capture d’écran de la fenêtre de terminal](media/sdk/qs-js-node-02_open_terminal.png)

1. Exécutez npm pour installer les dépendances.

   ![Capture d’écran de l’installation de npm](media/sdk/qs-js-node-03-npm_install.png)

1. Vous êtes maintenant prêt à ouvrir `index.js` et à définir un point d’arrêt.

   ![Capture d’écran d’index.js avec un point d’arrêt à la ligne 16](media/sdk/qs-js-node-04-setup_breakpoint.png)

1. Pour démarrer le débogage, appuyez sur F5 ou sélectionnez Déboguer/Démarrer le débogage à partir du menu.

   ![Capture d’écran du menu Déboguer](media/sdk/qs-js-node-05-start_debugging.png)

1. Quand un point d’arrêt est atteint, vous pouvez inspecter la pile des appels et les variables.

   ![Capture d’écran du débogueur](media/sdk/qs-js-node-06-hit_breakpoint.png)

1. Toute sortie s’affiche dans la fenêtre de console de débogage.

   ![Capture d’écran de la console de débogage](media/sdk/qs-js-node-07-debug_output.png)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Explorer des exemples Node.js sur GitHub](https://aka.ms/csspeech/samples)
