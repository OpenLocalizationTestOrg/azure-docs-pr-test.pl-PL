---
title: "aaaUse interakcyjne Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse interakcyjne (gałąź na LLAP) Hive w usłudze HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Użyj interaktywnego Hive w usłudze HDInsight (wersja zapoznawcza)
Interakcyjne gałęzi rejestru () [Na żywo długich i procesu](https://cwiki.apache.org/confluence/display/Hive/LLAP)) jest nowy HDInsight [typ klastra](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).  Interakcyjne Hive umożliwia buforowanie pamięci sprawia, że zapytań programu Hive bardziej interakcyjne i szybsze. Ta nowa funkcja sprawia, że HDInsight jedną hello na świecie większości wydajność, elastyczne i otwórz rozwiązania typu Big Data w chmurze hello z pamięci podręcznej w pamięci (przy użyciu Hive i Spark) i zaawansowane analizy za pośrednictwem głęboką integrację z usługami R. 

klastra interakcyjne Hive Hello różni się od hello klastra usługi Hadoop. Zawiera on tylko hello Hive usługi. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie i innych usług, są usuwani ze tego typu klastra wkrótce.
> Hello usługi Hive w klastrze interakcyjne Hive hello jest dostępny tylko za pośrednictwem hello widoku Hive narzędzia Ambari, Beeline i ODBC programu Hive. Nie są dostępne za pośrednictwem konsoli Hive, Templeton, wiersza polecenia platformy Azure i programu Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Tworzenie klastra interakcyjne Hive
Interakcyjne gałęzi klastra jest obsługiwana tylko w klastrach opartych na systemie Linux. Aby uzyskać informacje dotyczące tworzenia klastrów usługi HDInsight, zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Wykonanie gałąź z gałęzi interakcyjne
Istnieją różne opcje, w jaki sposób można wykonywać zapytań programu Hive:

* Uruchom Hive za pomocą hello widoku Hive narzędzia Ambari
  
    Witaj informacji o korzystaniu z Hive View hello, zobacz [hello użyj widoku Hive z usługą Hadoop w usłudze HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Uruchom przy użyciu Beeline gałęzi
  
    Hello informacji na temat używania Beeline w usłudze HDInsight, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight z Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Możesz użyć Beeline hello headnode lub węzłem krawędzi puste.  Zaleca się użycie Beeline z węzłem krawędzi puste.  Informacje dotyczące tworzenia klastra usługi HDInsight z pustym edgenode, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).
* Uruchom gałęzi przy użyciu Hive ODBC
  
    Hello informacji na temat używania ODBC programu Hive, zobacz [tooHadoop łączenie programu Excel z sterownik Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md).

**Witaj toofind JDBC ciąg połączenia:**

1. Logowanie przy użyciu następującego adresu URL hello tooAmbari: https://<ClusterName>. AzureHDInsight.net.
2. Kliknij przycisk **Hive** z menu po lewej stronie powitania.
3. Kliknij przycisk hello wyróżnione ikona toocopy hello URL:
   
   ![JDBC LLAP interakcyjne Hive HDInsight Hadoop](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Zobacz też
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Dowiedz się, jak klastrów toocreate interakcyjne Hive w usłudze HDInsight.
* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight z Beeline](hdinsight-hadoop-use-hive-beeline.md): Dowiedz się, jak zapytań Hive toosubmit Beeline toouse.
* [Połącz Excel tooHadoop sterownik Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md): Dowiedz się, jak tooconnect tooHive programu Excel.

