---
title: aaaUse R w klastrach toocustomize HDInsight - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall R przy użyciu skryptu akcji i użyj R w klastrach usługi HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>Instalowanie i używanie języka R w klastrach usługi Hadoop w usłudze HDInsight

Dowiedz się, jak toocustomize systemu Windows na podstawie klastra usługi HDInsight przy użyciu akcji skryptu języka R, oraz jak klastrów toouse R w usłudze HDInsight. Witaj [oferty HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) obejmuje R Server w ramach klastra usługi HDInsight. Dzięki temu skrypty R toouse MapReduce i Spark toorun rozproszone obliczenia. Aby uzyskać więcej informacji, zobacz temat [Rozpoczęcie pracy z platformą R Server w usłudze HDInsight](hdinsight-hadoop-r-server-get-started.md). Uzyskać informacji na temat używania R z systemem Linux klastrem, zobacz [instalacji i używania R w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md).

Można zainstalować język R w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*. Przykładowy skrypt tooinstall R w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

**Pokrewne artykuły**

* [Zainstaluj i użyj języka R w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>Co to jest R?
Witaj <a href="http://www.r-project.org/" target="_blank">R projektu do statystycznego przetwarzania danych</a> jest otwarty języka źródłowego i środowiska do statystycznego przetwarzania danych. R zawiera setki kompilacji funkcji statystycznych i własnej język programowania, łączącą aspekty funkcjonalne i zorientowanym obiektowo programowania. Umożliwia także rozbudowane funkcje graficzne. R jest hello preferowanych środowisko programowania najbardziej professional chi i służące w wielu różnych pól.

R jest zgodny z magazynu obiektów Blob Azure (WASB), aby dane przechowywane mogą być przetwarzane przy użyciu języka R w usłudze HDInsight.  

## <a name="install-r"></a>Zainstalować język R
A [przykładowy skrypt](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R w klastrze usługi HDInsight jest dostępny w trybie tylko do odczytu obiektów blob w usłudze Azure Storage. Ta sekcja zawiera instrukcje dotyczące sposobu toouse hello przykładowy skrypt podczas tworzenia klastra hello przy użyciu hello portalu Azure.

> [!NOTE]
> Witaj przykładowy skrypt został wprowadzony z klastra usługi HDInsight w wersji 3.1. Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).
>
>

1. Po utworzeniu klastra usługi HDInsight z hello portalu kliknij **konfiguracji opcjonalnej**, a następnie kliknij przycisk **akcji skryptu**.
2. Na powitania **akcji skryptu** wprowadź hello następujące wartości:

    ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize akcji skryptu Użyj klastra")

    <table border='1'>
        <tr><th>Właściwość</th><th>Wartość</th></tr>
        <tr><td>Nazwa</td>
            <td>Określ nazwę hello akcji skryptu, na przykład <b>zainstalować R</b>.</td></tr>
        <tr><td>Identyfikator URI skryptu</td>
            <td>Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra, na przykład <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>Typ węzła</td>
            <td>Określ hello węzłów, na których uruchomiono hello dostosowywania skryptu. Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>węzłów procesu roboczego</b> tylko.
        <tr><td>Parametry</td>
            <td>Określ parametry hello, jeśli są wymagane przez skrypt hello. Jednak hello tooinstall skryptu języka R nie wymaga żadnych parametrów, dzięki czemu można to pole pozostanie puste.</td></tr>
    </table>

    Więcej niż jeden tooinstall akcji skryptu można dodać wiele składników w klastrze hello. Po dodaniu hello skryptów, kliknij przycisk toostart znacznik wyboru hello crating hello klastra.

Umożliwia także hello tooinstall skryptu języka R w usłudze HDInsight przy użyciu programu Azure PowerShell lub hello zestawu .NET SDK usługi HDInsight. Instrukcje dotyczące tych procedur znajdują się w dalszej części tego artykułu.

## <a name="run-r-scripts"></a>Uruchom skrypty języka R
W tej sekcji opisano, jak skrypt toorun R na powitania Hadoop klastra z usługą HDInsight.

1. **Ustanowić klastra toohello połączenia pulpitu zdalnego**: Z hello portalu, Włącz pulpit zdalny dla klastra hello zostały utworzone z języka R zainstalowanego, a następnie połącz toohello klastra. Aby uzyskać instrukcje, zobacz [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Otwórz hello R konsoli**: hello R instalacji umieszcza konsoli toohello R łącza na pulpicie hello hello węzła głównego. Kliknij go tooopen hello R konsoli.
3. **Uruchom skrypt hello R**: hello R skrypt można uruchomić bezpośrednio z konsoli hello R wklejenie go, wybierając ją i naciskając klawisz ENTER. Poniżej przedstawiono prosty przykład skrypt generuje hello too100 liczb od 1 i mnoży je przez 2.

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

Witaj pierwsze dwa wiersze wywołania hello RHadoop bibliotek, które są instalowane z R. hello wiersza końcowego odbitek hello wyniki toohello konsoli. dane wyjściowe Hello powinien wyglądać następująco:

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>Zainstalować język R przy użyciu programu Azure PowerShell
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu programu Azure PowerShell. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).

## <a name="install-r-using-net-sdk"></a>Zainstalować język R przy użyciu zestawu .NET SDK
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu hello zestawu .NET SDK. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).

## <a name="see-also"></a>Zobacz też
* [Zainstaluj i użyj języka R w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md)
* [Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark
* [Zainstaluj w klastrach HDInsight Giraph](hdinsight-hadoop-giraph-install.md): Akcja skryptu próbki o instalowaniu Giraph
* [Zainstaluj w klastrach HDInsight Solr](hdinsight-hadoop-solr-install-linux.md): Akcja skryptu próbki o instalowaniu Solr.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
