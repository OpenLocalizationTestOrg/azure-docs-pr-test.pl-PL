---
title: "aaaInstall i użyj Giraph na platformie Hadoop clusters w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toocustomize HDInsight z Giraph i jak toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Zainstalować i używać Giraph w klastrach HDInsight opartych na systemie Windows

Dowiedz się, jak toocustomize systemu Windows na podstawie klastra usługi HDInsight przy użyciu akcji skryptu Giraph i jak toouse Giraph tooprocess dużych wykresów. Uzyskać informacji o używaniu Giraph z klastra opartych na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Aby uzyskać informacje na temat tooinstall Giraph w klastrze usługi HDInsight opartej na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).


Giraph można zainstalować w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*. Przykładowy skrypt tooinstall Giraph w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). Witaj przykładowy skrypt działa tylko w przypadku klastra HDInsight w wersji 3.1. Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).

**Pokrewne artykuły**

* [Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-giraph"></a>Co to jest Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight. Wykresy modelu relacje między obiektami, takimi jak hello połączeń między routerami w dużych sieci, takich jak Internet, hello lub relacje między osoby w sieciach społecznościowych (czasami określonego tooas społecznościowych wykres). Wykres przetwarzania pozwala tooreason o hello relacje między obiektami na wykresie, takich jak:

* Identyfikuje potencjalne znajomych oparte na bieżącej relacji.
* Identyfikowanie hello najkrótszy trasy między dwoma komputerami w sieci.
* Obliczanie rangę strony hello stron sieci Web.

## <a name="install-giraph-using-portal"></a>Zainstaluj Giraph przy użyciu portalu
1. Rozpocznij tworzenie klastra przy użyciu hello **Utwórz niestandardowy** opcji, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-provision-clusters.md).
2. Na powitania **akcji skryptu** strony kreatora powitania kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:

    ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize akcji skryptu Użyj klastra")

    <table border='1'>
        <tr><th>Właściwość</th><th>Wartość</th></tr>
        <tr><td>Nazwa</td>
            <td>Określ nazwę hello akcji skryptu. Na przykład <b>zainstalować Giraph</b>.</td></tr>
        <tr><td>Identyfikator URI skryptu</td>
            <td>Określ hello identyfikator URI (Uniform Resource) toohello skrypt, który jest wywołana toocustomize hello klastra. Na przykład <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Typ węzła</td>
            <td>Określ hello węzłów, na których uruchomiono hello dostosowywania skryptu. Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>tylko węzłów procesu roboczego</b>.
        <tr><td>Parametry</td>
            <td>Określ parametry hello, jeśli są wymagane przez skrypt hello. Hello skryptu tooinstall Giraph nie wymaga żadnych parametrów, więc można to pole pozostanie puste.</td></tr>
    </table>

    Więcej niż jeden tooinstall akcji skryptu można dodać wiele składników w klastrze hello. Po dodaniu hello skryptów, kliknij przycisk toostart znacznikiem wyboru hello tworzenia klastra hello.

## <a name="use-giraph"></a>Korzystanie z systemu Giraph
Używamy hello SimpleShortestPathsComputation przykład toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementacji do znajdowania hello najkrótszy ścieżki między obiektami na wykresie. Użyj hello następujące kroki tooupload hello przykładowych danych i hello próbki jar, uruchomienie zadania przy użyciu przykład SimpleShortestPathsComputation Witaj, a następnie Wyświetl hello wyniki.

1. Przekaż przykładowe tooAzure plik danych magazynu obiektów Blob. Na lokalnej stacji roboczej, Utwórz nowy plik o nazwie **tiny_graph.txt**. Powinien on zawierać hello następujące wiersze:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Przekaż hello tiny_graph.txt toohello podstawowego magazynu plików dla klastra usługi HDInsight. Aby uzyskać instrukcje na temat danych tooupload, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).

    Te dane w tym artykule opisano relacje między obiektami w ukierunkowanego wykresu, używając formatu hello [źródła\_identyfikator, źródło\_wartość [[dest\_identyfikator], [krawędzi\_wartość],...]]. Każdy wiersz zawiera relację między **źródła\_identyfikator** obiektu i co najmniej jeden **dest\_identyfikator** obiektów. Witaj **krawędzi\_wartość** (lub wagi) można traktować jako siły hello lub odległość hello połączenie między **source_id** i **dest\_identyfikator**.

    Rysowane, i przy użyciu wartości hello (lub wagi) jako hello odległość między obiektami, hello powyżej danych może wyglądać następująco:

    ![tiny_graph.txt rysowane jako okręgi wiersze z różnymi odległość między](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Uruchom przykład Witaj SimpleShortestPathsComputation. Użyj powitania po przykład Witaj toorun poleceń cmdlet programu Azure PowerShell przy użyciu pliku tiny_graph.txt hello jako dane wejściowe.

    > [!IMPORTANT]
    > Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    W hello powyżej przykładzie, Zastąp **clustername** o nazwie hello klastra usługi HDInsight, zawierający Giraph zainstalowane.
3. Wyświetl wyniki hello. Po zakończeniu zadania hello hello wyniki będą przechowywane w dwóch plikach danych wyjściowych w hello **wasb: / / / przykład/out/shotestpaths** folderu. Witaj plików są nazywane **części m-00001** i **części m-00002**. Wykonaj następujące kroki toodownload i widoku wyjściowego hello hello:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Spowoduje to utworzenie hello **shortestpaths przykład/wyjście** struktura katalogów w bieżącym katalogu hello na stacji roboczej i Witaj dwie dane wyjściowe pliki toothat lokalizacji.

    Użyj hello **Cat** polecenia cmdlet toodisplay hello zawartość plików hello:

        Cat example/output/shortestpaths/part*

    dane wyjściowe Hello powinna zostać wyświetlona podobne toohello poniżej:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    przykład Witaj SimpleShortestPathComputation jest zakodowany toostart z obiektem ID 1 i Znajdź hello najkrótszy ścieżki tooother obiektów. Dlatego hello dane wyjściowe powinny zostać odczytany jako `destination_id distance`, gdzie odległości jest wartość hello (lub wagi) krawędzi hello pokonać między obiektu ID 1 i identyfikatora hello docelowej.

    Wizualizacja to, możesz sprawdzić wyniki hello przez podróży hello najkrótszy ścieżek między 1 Identyfikatora i wszystkie inne obiekty. Należy pamiętać, że hello najkrótszy ścieżki między ID 1 i 4 identyfikator wynosi 5. Jest to hello całkowita odległość między <span style="color:orange">ID 1 i 3</span>, a następnie <span style="color:red">identyfikator 3 i 4</span>.

    ![Rysowanie obiektów jako kółka za pomocą najmniejszej ścieżek między](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Zainstaluj Giraph przy użyciu programu Azure PowerShell
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu programu Azure PowerShell. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Zainstaluj Giraph przy użyciu zestawu .NET SDK
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu hello zestawu .NET SDK. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Zobacz też
* [Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).
* [Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark.
* [Zainstalować język R w klastrach HDInsight][hdinsight-install-r]: Akcja skryptu próbki o instalowaniu R.
* [Zainstaluj w klastrach HDInsight Solr](hdinsight-hadoop-solr-install.md): Akcja skryptu próbki o instalowaniu Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
