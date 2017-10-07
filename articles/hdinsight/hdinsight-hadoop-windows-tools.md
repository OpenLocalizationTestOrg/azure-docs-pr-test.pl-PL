---
title: "aaaUse komputera z systemem Windows z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Praca z Komputerami z systemem Windows w Hadoop w usłudze HDInsight. Zarządzanie i klastrów zapytania przy użyciu narzędzi programu PowerShell, Visual Studio i Linux. Tworzenie rozwiązania typu big data z platformą .NET."
services: hdinsight
keywords: "hadoop w systemie windows, usługi hadoop dla systemu windows"
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Praca w hello ekosystemu Hadoop w usłudze HDInsight z komputera z systemem Windows

Dowiedz się więcej o programowanie i opcje zarządzania na komputerze z systemem Windows hello dla pracy w hello ekosystemu Hadoop w usłudze HDInsight. 

HDInsight jest oparta na Apache Hadoop i składniki platformy Hadoop, technologii open source opracowany w systemie Linux. HDInsight w wersji 3.4 i wyższych używa hello dystrybucji Ubuntu Linux jako hello podstawowego systemu operacyjnego dla hello klastra. Można jednak pracować z usługą HDInsight, z poziomu klienta systemu Windows lub środowiska projektowego systemu Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Przy użyciu programu PowerShell dla zadania wdrażania i zarządzania
Program Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i automatyzowania zadań wdrażania i zarządzania w usłudze HDInsight z systemu Windows.

Przykłady zadania, które można wykonać przy użyciu programu PowerShell:

* [Tworzenie klastrów za pomocą programu PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Uruchamianie zapytań Hive przy użyciu programu PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Zarządzanie klastrami przy użyciu programu PowerShell](hdinsight-administer-use-powershell.md)

Wykonaj kroki zbyt[Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello najnowszej wersji. Jeśli masz skrypty wymagające toobe zmodyfikować toouse hello nowe polecenia cmdlet dla usługi Azure Resource Manager, zobacz [migracji tooAzure narzędzi programistycznych opartych na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Narzędzia można uruchomić w przeglądarce
Witaj następujących narzędzi ma interfejsu użytkownika, który jest uruchamiany w przeglądarce sieci web:
* **[Powłoka chmury Azure (wersja zapoznawcza)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  jest interaktywny, wiersza polecenia powłoki, uruchomioną w przeglądarce i z poziomu hello portalu Azure.
* **[Interfejs sieci Web Ambari](hdinsight-hadoop-manage-ambari.md)**  zarządzania i narzędzia dostępne w portalu Azure, które mogą być używane toomanage różnych rodzajów zadań, takich jak hello do monitorowania:
    * [Użyj narzędzia Ambari z hello interfejsu API REST](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Widok hive narzędzia Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Widok tez w Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Narzędzia Data Lake (Hadoop) dla programu Visual Studio
Użyj narzędzi Data Lake Tools dla Visual Studio toodeploy i zarządzanie topologiami Storm. Narzędzia Data Lake Tools instaluje hello SCP.NET zestaw SDK, który pozwala topologii Storm C# toodevelop z programem Visual Studio.

Przed przejściem do toohello następujące przykłady, [zainstalować i spróbować narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Przykłady zadań, które można zrobić za pomocą programu Visual Studio i narzędzi Data Lake Tools dla programu Visual Studio:
* [Wdrażanie i zarządzanie topologiami Storm w programie Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Tworzenie topologii C# dla Storm przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). bity Hello obejmują szablony przykład topologii Storm mogą łączyć toodatabases, takie jak bazy danych Azure rozwiązania Cosmos i bazy danych SQL.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio i hello zestawu .NET SDK 

Można użyć programu Visual Studio z klastrami toomanage zestawu .NET SDK hello i tworzyć aplikacje danych big data. Można użyć innych IDEs dla hello następujące zadania, ale przykłady są wyświetlane w programie Visual Studio.

Przykłady zadań, które można wykonać za pomocą hello zestawu .NET SDK w programie Visual Studio:
* [Tworzenie klastrów i pracy w usłudze HDInsight z poziomu aplikacji .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Uruchamianie zapytań Hive przy użyciu zestawu .NET SDK hello](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [C# zdefiniowane przez użytkownika funkcji za pomocą technologii Hive i Pig przesyłania strumieniowego na platformie Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Porada Jeśli korzystasz z rozwiązań .NET z klastrami HDInsight opartych na systemie Windows, jest odpowiedni moment tooplan migracji tooLinux klastrów. Aby uzyskać więcej informacji, zobacz [rozwiązanie migracji .NET dla usługi HDInsight opartej na systemie Windows usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA i Eclipse IDE for klastry Spark
Zarówno [Intellij IDEA](https://www.jetbrains.com/idea/download) i hello [Eclipse IDE](https://www.eclipse.org/downloads/) można używać do:
* Tworzenie i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight.
* Dostęp do zasobów klastra Spark.
* Tworzenie i uruchamianie aplikacji Scala Spark lokalnie.

Te artykuły Pokaż jak: 
* Intellij IDEA: [aplikacji Spark Utwórz za pomocą hello Azure narzędzi dla wtyczkę Intellij i hello Scala zestawu SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Zaćmienie-IDE lub Scala IDE dla programu Eclipse: [Spark tworzenia aplikacji i hello zestawu narzędzi platformy Azure dla programu Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notesów na Spark dla analityków danych 
Klastry platformy Apache Spark w usłudze HDInsight obejmują notesów Zeppelin i jądra, które mogą być używane z notesów Jupyter. 

* [Dowiedz się, jak toouse jądra na Spark klastry aplikacji Spark tootest notesów Jupyter](hdinsight-apache-spark-zeppelin-notebook.md)
* [Dowiedz się, jak notesów Zeppelin toouse na Spark klastrów toorun Spark zadania](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Uruchamianie narzędzi opartych na systemie Linux i technologii w systemie Windows

W razie wystąpienia sytuacji, w których należy użyć narzędzia lub technologii, która jest dostępna tylko w systemie Linux, należy wziąć pod uwagę hello następujące opcje:

* **Bash (beta) w systemie Windows 10** zapewnia podsystemu systemu Linux w systemie Windows. Bash umożliwia toodirectly uruchomić narzędzia Linux bez konieczności toomaintain dedykowanych instalacja systemu Linux. [Zainstaluj i uruchom hello Bash w wersji beta w systemie Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker dla systemu Windows** udostępnia narzędzia oparte na systemie Linux toomany i można je uruchomić bezpośrednio z systemu Windows. Na przykład można użyć Docker toorun hello Beeline klienta gałęzi bezpośrednio z systemu Windows. Można również użyć toorun Docker lokalnego notesu Jupyter i połączenie zdalne tooSpark w usłudze HDInsight. [Rozpoczynanie pracy z rozwiązaniem Docker dla systemu Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  umożliwia system plików toographically przeglądania hello klastra za pośrednictwem połączenia SSH.

## <a name="next-steps"></a>Następne kroki
Jeśli nowy tooworking w klastrach opartych na systemie Linux, zobacz hello wykonaj artykuły:
* [Konfigurowanie usługi Hadoop, Kafka, Spark lub innych klastrów](hdinsight-hadoop-provision-linux-clusters.md)
* [Porady dotyczące klastrów usługi HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md)