---
title: Utiliser Apache Hive sur la console de requêtes dans HDInsight - Azure
description: Découvrez comment utiliser la console de requêtes Web pour exécuter des requêtes Apache Hive sur un cluster Hadoop HDInsight à partir de votre navigateur.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/12/2017
ms.author: hrasheed
ROBOTS: NOINDEX
ms.openlocfilehash: 1e638bd348b7a5272dd8bfbe25aa841f38a51b9a
ms.sourcegitcommit: c37122644eab1cc739d735077cf971edb6d428fe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53409698"
---
# <a name="run-apache-hive-queries-using-the-query-console"></a>Exécution de requêtes Apache Hive à l’aide de la console de requêtes
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

Dans cet article, vous découvrirez comment utiliser la console de requêtes HDInsight pour exécuter des requêtes Apache Hive sur un cluster Hadoop HDInsight à partir de votre navigateur.

> [!IMPORTANT]  
> La console de requêtes HDInsight n’est disponible que sur les clusters HDInsight Windows. Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou version supérieure, consultez [Exécuter des requêtes Apache Hive dans la vue Hive d’Ambari](apache-hadoop-use-hive-ambari-view.md) pour plus d’informations sur l’exécution de requêtes Hive à partir d’un navigateur web.

## <a id="prereq"></a>Configuration requise
Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :

* Un cluster Hadoop HDInsight Windows
* Un navigateur Web moderne

## <a id="run"></a>Exécuter des requêtes Apache Hive à l’aide de la console de requêtes
1. Ouvrez un navigateur, puis accédez à **https://CLUSTERNAME.azurehdinsight.net**, où **CLUSTERNAME** est le nom de votre cluster HDInsight. Lorsque vous y êtes invité, entrez le nom d'utilisateur et le mot de passe que vous avez entrés lors de la création du cluster.
2. À partir des liens situés en haut de la page, sélectionnez **Éditeur Hive**. Cela affiche un formulaire qui peut être utilisé pour saisir les instructions HiveQL que vous souhaitez exécuter sur le cluster HDInsight.

    ![l’éditeur Hive](./media/apache-hadoop-use-hive-query-console/queryconsole.png)

    Remplacez le texte `Select * from hivesampletable` par les instructions HiveSQL suivantes :

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Ces instructions effectuent les opérations suivantes :

   * **DROP TABLE** : Supprime la table et le fichier de données, si la table existe déjà.
   * **CREATE EXTERNAL TABLE** : Crée une table « externe » dans Hive. Les tables externes stockent uniquement la définition de table dans Hive ; les données restent à leur emplacement d’origine.

     > [!NOTE]  
     > Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe (comme un processus de téléchargement de données automatisé) ou par une autre opération MapReduce, mais souhaitez toujours que les requêtes Hive utilisent les données les plus récentes.
     >
     > La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.
     >
     >
   * **ROW FORMAT** : Indique à Hive la façon dont les données sont mises en forme. Dans ce cas, les champs de chaque journal sont séparés par un espace.
   * **STORED AS TEXTFILE LOCATION** : Indique à Hive où sont stockées les données (répertoire example/data) et qu’elles sont stockées sous forme de texte
   * **SELECT** : Sélectionne toutes les lignes dont la colonne **t4** contient la valeur **[ERROR]**. Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.
   * **INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log. Cela limite la recherche au fichier sample.log qui contient les données et l'empêche de renvoyer des données provenant d'autres fichiers d'exemple qui ne correspondent pas au schéma que nous avons défini.
3. Cliquez sur **Envoyer**. La **session de la tâche** située au bas de la page devrait afficher les détails de la tâche.
4. Une fois le champ **État** défini sur **Terminé**, sélectionnez **Afficher les détails** de la tâche. Dans la page relative aux détails, la **sortie de la tâche** contient `[ERROR]    3`. Vous pouvez utiliser le bouton **Télécharger** , situé en dessous de ce champ, pour télécharger un fichier contenant la sortie de la tâche.

## <a id="summary"></a>Résumé
Comme vous pouvez le constater, la console de requêtes permet d'exécuter facilement des requêtes Hive sur un cluster HDInsight, de surveiller l'état de la tâche et de récupérer le résultat.

Pour en savoir plus sur l’utilisation de la console de requêtes Hive pour l’exécution de tâches Hive, sélectionnez **Prise en main** en haut de la console de requêtes, puis utilisez les exemples fournis. Chaque exemple aborde le processus d'analyse de données à l'aide de Hive, y compris les explications des instructions HiveQL utilisées dans l'exemple.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur Hive dans HDInsight :

* [Utiliser Apache Hive avec Apache Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utiliser Apache Pig avec Apache Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utiliser MapReduce avec Apache Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Si vous utilisez Tez avec Hive, consultez les documents suivants pour les informations de débogage :

* [Utiliser l’interface utilisateur Apache Tez sur HDInsight Windows](../hdinsight-debug-tez-ui.md)
* [Utiliser la vue Tez Apache Ambari sur HDInsight Linux](../hdinsight-debug-ambari-tez-view.md)

[1]:apache-hadoop-visual-studio-tools-get-started.md

[azure-purchase-options]: https://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: https://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: https://azure.microsoft.com/pricing/free-trial/

[apache-tez]: https://tez.apache.org
[apache-hive]: https://hive.apache.org/
[apache-log4j]: https://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: https://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]:apache-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: https://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
