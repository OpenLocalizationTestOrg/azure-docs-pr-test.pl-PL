---
title: "przy użyciu programu PowerShell - Azure HDInsight klastrów Hadoop aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Hadoop, HBase, Storm i Spark klastrów w systemie Linux dla usługi HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Tworzenie klastrów z systemem Linux w usłudze HDInsight przy użyciu programu Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Program Azure PowerShell jest zaawansowane środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń w systemie Microsoft Azure. Ten dokument zawiera informacje dotyczące sposobu toocreate usługi HDInsight opartej na systemie Linux klaster przy użyciu programu Azure PowerShell. Zawiera również przykład skryptu.

> [!NOTE]
> Program Azure PowerShell jest dostępny tylko na komputerach klienckich z systemem Windows. Jeśli używasz klienta systemu Linux, Unix lub Mac OS X, zobacz [tworzenia klastra usługi HDInsight opartej na systemie Linux przy użyciu interfejsu wiersza polecenia Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) informacji o używaniu hello Azure CLI toocreate klastra.

## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć następujące hello przed rozpoczęciem tej procedury:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.

## <a name="create-cluster"></a>Tworzenie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate klastra usługi HDInsight przy użyciu programu Azure PowerShell, należy wykonać hello następujące procedury:

* Tworzenie grupy zasobów platformy Azure
* Tworzenie konta usługi Azure Storage
* Tworzenie kontenera obiektów Blob platformy Azure
* Tworzenie klastra usługi HDInsight

Witaj poniższy skrypt pokazuje, jak toocreate nowego klastra:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

podane dla logowania do klastra hello wartości Hello są hello toocreate używane konto użytkownika usługi Hadoop dla klastra hello. Użyj tego tooservices tooconnect konta hostowanych w klastrze hello, takich jak web UI lub interfejsów API REST.

Hello wartości określonej dla użytkownika SSH hello są użytkownika SSH hello toocreate używane dla klastra hello. Użyj tego konta toostart zdalnej sesji SSH w klastrze hello i uruchom zadania. Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

> [!IMPORTANT]
> Jeśli planujesz toouse więcej niż 32 węzłami procesów roboczych (na utworzenie klastra lub przez hello skalowania klastra po utworzeniu), należy również określić rozmiaru węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.
>
> Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Może potrwać toocreate minut too20 klastra.

## <a name="create-cluster-configuration-object"></a>Tworzenie klastra: obiekt konfiguracji

Można również utworzyć HDInsight konfiguracji obiektów przy użyciu `New-AzureRmHDInsightClusterConfig` polecenia cmdlet. Następnie można zmodyfikować tej konfiguracji obiektu tooenable dodatkowe opcje konfiguracji dla klastra. Na koniec użyj hello `-Config` parametru hello `New-AzureRmHDInsightCluster` konfiguracji hello toouse polecenia cmdlet.

Witaj poniższy skrypt tworzy tooconfigure obiekt konfiguracji R Server na typ klastra usługi HDInsight. Konfiguracja Hello pozwala węzeł krawędzi, programu RStudio i konto magazynu dodatkowe.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane. Podczas korzystania z tego przykładu należy utworzyć konto magazynu dodatkowe hello w hello tej samej lokalizacji co powitania serwera.

## <a name="customize-clusters"></a>Dostosowywanie klastrów

* Zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Usuń klaster hello

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki

Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą hello następujące zasoby toolearn jak toowork z klastrem.

### <a name="hadoop-clusters"></a>Klastry Hadoop

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Klastrów HBase

* [Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Klastry STORM

* [Tworzenie topologii Java dla Storm w usłudze HDInsight](hdinsight-storm-develop-java-topology.md)
* [Użyj składników języka Python w Storm w usłudze HDInsight](hdinsight-storm-develop-python-topology.md)
* [Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Klastry Spark

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)

