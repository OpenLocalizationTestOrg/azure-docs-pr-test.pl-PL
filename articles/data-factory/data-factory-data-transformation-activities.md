---
title: "Przekształcenie danych: Proces & przekształcenia danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootransform danych lub przetwarzania danych w fabryce danych Azure przy użyciu platformy Hadoop, uczenie maszynowe lub usługi Azure Data Lake Analytics."
keywords: "przekształcenia danych, przetwarzania danych przekształcania danych, transformacji działania"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Przekształć dane w fabryce danych Azure
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Przesyłanie strumieniowe usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Procedura składowana](data-factory-stored-proc-activity.md)
> * [Język U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Niestandardowe .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Omówienie
W tym artykule opisano działania przekształcania danych w fabryce danych Azure, można użyć tootransform, przetwarzania danych pierwotnych do przewidywania i szczegółowych informacji. Wykonuje działanie transformacji w środowisku komputerowym, takich jak klaster Azure HDInsight lub partii zadań Azure. Łącza tooarticles Usługa udostępnia szczegółowe informacje o każdym działaniu transformacji.

Fabryka danych obsługuje hello następujące działania przekształcania danych, które mogą zostać dodane za[potoki](data-factory-create-pipelines.md) albo indywidualnie lub powiązane z innym działaniem.

> [!NOTE]
> Aby uzyskać wskazówki krok po kroku instrukcje, zobacz [utworzyć potok transformację Hive](data-factory-build-your-first-pipeline.md) artykułu.  
> 
> 

## <a name="hdinsight-hive-activity"></a>Działanie HDInsight Hive
Witaj HDInsight Hive działania w potoku fabryki danych wykonuje zapytań programu Hive samodzielnie lub w klastrze systemu Windows/Linux-based HDInsight na żądanie. Zobacz [Hive działania](data-factory-hive-activity.md) artykułu, aby uzyskać szczegółowe informacje dotyczące tego działania. 

## <a name="hdinsight-pig-activity"></a>Działanie HDInsight Pig
Witaj HDInsight Pig działania w potoku fabryki danych wykonuje zapytania Pig samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie. Zobacz [działania Pig](data-factory-pig-activity.md) artykułu, aby uzyskać szczegółowe informacje dotyczące tego działania. 

## <a name="hdinsight-mapreduce-activity"></a>Działania HDInsight MapReduce
Witaj działania HDInsight MapReduce w potoku fabryki danych wykonuje programy MapReduce samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie. Zobacz [działania MapReduce](data-factory-map-reduce.md) artykułu, aby uzyskać szczegółowe informacje dotyczące tego działania.

## <a name="hdinsight-streaming-activity"></a>Działanie usługi HDInsight przesyłania strumieniowego
Witaj HDInsight działaniu przesyłania strumieniowego w potoku fabryki danych wykonuje przesyłania strumieniowego usługi Hadoop programy samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie. Zobacz [działaniu przesyłania strumieniowego HDInsight](data-factory-hadoop-streaming-activity.md) szczegółowe informacje dotyczące tego działania.

## <a name="hdinsight-spark-activity"></a>Działania platformy Spark w usłudze HDInsight
Witaj HDInsight Spark działania w potoku fabryki danych wykonuje programy Spark w klastrze usługi HDInsight. Aby uzyskać więcej informacji, zobacz [programy Spark wywołania z fabryki danych Azure](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Machine Learning działań
Azure umożliwia fabryki danych tooeasily możesz utworzyć potoki korzystających z opublikowanych uczenie maszynowe Azure w sieci web usługi analizy predykcyjnej. Przy użyciu hello [działanie wykonywania wsadowego](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) w potoku fabryki danych Azure, można wywołać usługi Machine Learning web toomake operacje przewidywania dla usługi na powitania danych w partii.

Wraz z upływem czasu hello modeli predykcyjnych w hello uczenia maszynowego oceniania eksperymenty muszą toobe retrained przy użyciu nowych danych wejściowych zestawów danych. Po wykonaniu ponownego trenowania chcesz hello tooupdate oceniania usługi sieci web z hello retrained modelu uczenia maszynowego. Można użyć hello [działanie aktualizacji zasobu](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) usługi sieci web hello tooupdate z hello nowo trenowanego modelu.  

Zobacz [uczenia maszynowego Użyj działania](data-factory-azure-ml-batch-execution-activity.md) szczegółowe informacje o tych działań uczenia maszynowego. 

## <a name="stored-procedure-activity"></a>Działania procedury składowanej
Witaj działania procedury składowanej SQL Server można używać w tooinvoke potoku fabryki danych procedury składowanej w jednym z powitania po magazynów danych: baza danych SQL Azure, Magazyn danych SQL Azure, bazy danych serwera SQL w przedsiębiorstwie lub maszynie Wirtualnej platformy Azure. Zobacz [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) artykułu, aby uzyskać szczegółowe informacje.  

## <a name="data-lake-analytics-u-sql-activity"></a>Działanie U-SQL usługi Data Lake Analytics
Data Lake Analytics U-SQL działanie uruchamia skrypt U-SQL w klastrze usługi Azure Data Lake Analytics. Zobacz [działanie U-SQL analizy danych](data-factory-usql-activity.md) artykułu, aby uzyskać szczegółowe informacje. 

## <a name="net-custom-activity"></a>Niestandardowe działanie platformy .NET
Dane tootransform w taki sposób, który nie jest obsługiwany przez fabrykę danych należy można tworzyć niestandardowe działania na własną logikę przetwarzania danych i użyj hello działania w potoku hello. Można skonfigurować hello niestandardowych .NET działania toorun przy użyciu usługi partia zadań Azure lub klaster Azure HDInsight. Zobacz [skorzystać z działań niestandardowych](data-factory-use-custom-activities.md) artykułu, aby uzyskać szczegółowe informacje. 

Można tworzyć niestandardowe działania toorun R skrypty w klastrze usługi HDInsight z języka R zainstalowanego. Zobacz [Uruchamianie skryptów języka R przy użyciu usługi Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>Środowiska obliczeniowe
Można utworzyć połączonej usługi dla środowiska obliczeniowego hello, a następnie użyć hello połączone usługi, podczas definiowania działania transformacji. Istnieją dwa typy środowisk obliczeniowe obsługiwane przez fabryki danych. 

1. **Na żądanie**: W tym przypadku środowiska komputerowego hello pełni zarządza fabryki danych. Jest automatycznie tworzony przez hello usługi fabryka danych przed zadanie jest tooprocess przesłanych danych i usunięta po zakończeniu zadania hello. Można skonfigurować i sterowanie ustawieniami szczegółowego hello obliczeń na żądanie środowiska do wykonywania zadań zarządzania klastrem i uruchamianie akcji. 
2. **Bring Your Own**: W tym przypadku własne środowisko przetwarzania danych (na przykład klaster usługi HDInsight) może być rejestrowany jako połączonej usługi z fabryki danych. środowiska komputerowego Hello jest zarządzany przez użytkownika i hello usługi fabryka danych używa tooexecute hello działań. 

Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) toolearn artykuł o obliczeniowe usług obsługiwanych przez fabryki danych. 

## <a name="summary"></a>Podsumowanie
Obsługuje fabryki danych Azure hello następujące działania przekształcania danych i hello środowisk obliczeniowych hello działań. Witaj transformacji działania może być dodany toopipelines indywidualnie lub powiązane z innym działaniem.

| Działanie przekształcania danych | Środowisko obliczeniowe |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Przesyłanie strumieniowe usługi Hadoop](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Działania usługi Machine Learning: wykonywanie wsadowe i aktualizacja zasobów](data-factory-azure-ml-batch-execution-activity.md) |Maszyna wirtualna platformy Azure |
| [Procedura składowana](data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Data Warehouse lub SQL Server |
| [Język U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](data-factory-use-custom-activities.md) |Usługa HDInsight [Hadoop] lub usługa Azure Batch |

