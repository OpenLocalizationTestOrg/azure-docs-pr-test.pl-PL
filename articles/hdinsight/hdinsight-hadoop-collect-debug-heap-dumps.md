---
title: "aaaDebug i analizowanie usługi Hadoop z zrzuty stosu - Azure | Dokumentacja firmy Microsoft"
description: "Automatycznie zbieranie zrzutów sterty dla usług Hadoop i umieścić wewnątrz hello konta magazynu obiektów Blob platformy Azure do debugowania i analizy."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Zbieranie zrzutów sterty w toodebug magazynu obiektów Blob i analizowanie usługi Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Zrzuty stosu zawierającego migawkę pamięci aplikacji hello, w tym hello wartości zmiennych w czasie hello zrzutu hello został utworzony. Tak, aby były przydatne do diagnozowania problemów występujących w czasie wykonywania. Zrzuty stosu mogą być automatycznie zbierane na potrzeby usług Hadoop i umieszczony wewnątrz hello konta magazynu obiektów Blob platformy Azure przez użytkownika w obszarze HDInsightHeapDumps /.

Kolekcja Hello zrzuty stosu dla różnych usług musi być włączony dla usług w poszczególnych klastrach. Witaj domyślny dla tej funkcji jest toobe wyłączone dla klastra. Te zrzuty stosu może być duży, dlatego jest konta magazynu obiektów Blob hello wskazane toomonitor których one są zapisywane po włączeniu hello kolekcji.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). informacje Hello w tym artykule dotyczą tylko usługi HDInsight opartej na tooWindows. Aby informacji na temat usługi HDInsight opartej na systemie Linux, zobacz [zrzuty stosu Włącz usługi Hadoop w HDInsight opartych na systemie Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Kwalifikujących się usług dla zrzuty stosu
Można włączyć zrzuty stosu dla hello następujące usługi:

* **hcatalog** -tempelton
* **gałąź** -serwera hiveserver2, potrzeby magazynu metadanych, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager nodemanager, timelineserver
* **System plików hdfs** -datanode secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Elementy konfiguracji, które umożliwiają zrzuty stosu
tooturn na zrzuty stosu dla usługi, należy tooset hello odpowiednia konfiguracja elementy w sekcji powitania dla tej usługi, które jest określone przez **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Witaj wartość **service_name** może być dowolną hello usług wymienione w tym miejscu: tempelton, serwera hiveserver2, potrzeby magazynu metadanych, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, lub namenode.

## <a name="enable-using-azure-powershell"></a>Włącz przy użyciu programu Azure PowerShell
Na przykład tooturn na zrzuty stosu przy użyciu programu Azure PowerShell dla jobhistoryserver, program hello następującego skryptu:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Włącz przy użyciu zestawu .NET SDK
Na przykład tooturn na zrzuty stosu przy użyciu jobhistoryserver hello Azure HDInsight .NET SDK, program hello następującego kodu:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
