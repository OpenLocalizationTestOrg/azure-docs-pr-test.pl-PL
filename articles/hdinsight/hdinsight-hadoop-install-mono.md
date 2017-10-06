---
title: "aaaInstall lub zaktualizuj Mono w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse określonej wersji Mono z klastrem usługi HDInsight. Mono jest toorun używanych aplikacji .NET w klastrach HDInsight opartych na systemie Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Zainstaluj lub zaktualizuj Mono w usłudze HDInsight

Dowiedz się, jak tooinstall określonej wersji programu [Mono](https://www.mono-project.com) HDInsight 3.4 lub nowszego.

Mono jest zainstalowany w wersji 3.4 HDInsight lub nowszym i jest używany toorun aplikacji .NET. Uzyskać informacji o wersji hello Mono dołączone do każdej wersji usługi HDInsight, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md). tooinstall inną wersję w klastrze, użyj akcji skryptu hello w tym dokumencie. 

## <a name="how-it-works"></a>Jak to działa

Ten skrypt akceptuje hello następującego parametru:

* __Numer wersji mono__: wersja hello Mono tooinstall. Wersja Hello musi być dostępny z [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

skrypt Hello instaluje powitania po Mono pakiety:

* __Zakończenie mono__

* __Urząd certyfikacji — certyfikaty — mono__

## <a name="hello-script"></a>Witaj skryptu

__Lokalizacja skryptu__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Wymagania dotyczące__:

* Witaj skryptu muszą być stosowane na powitania __węzły główne__ i __węzłów procesu roboczego__.

## <a name="toouse-hello-script"></a>toouse hello skryptu

Aby uzyskać informacje dotyczące toouse ten skrypt z usługą HDInsight, zobacz temat hello [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) dokumentu. Można użyć skryptu hello za pomocą hello portalu Azure, programu Azure PowerShell lub hello wiersza polecenia platformy Azure.

Gdy następujące hello dokument akcji skryptu, użyj hello następującego identyfikatora URI:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Podczas konfigurowania usługi HDInsight za pomocą tego skryptu, należy oznaczyć skrypt hello jako __Persisted__. To ustawienie umożliwia HDInsight tooapply węzłów tooworker skryptu hello dodanych do skalowania operacji.


## <a name="next-steps"></a>Następne kroki

Wiesz już, jak tooupgrade lub zainstaluj określonej wersji Mono w usłudze HDInsight. Aby uzyskać więcej informacji na temat używania aplikacji .NET z Mono w usłudze HDInsight Zobacz hello w następujących dokumentach:

* [Użyj .NET do przesyłania strumieniowego MapReduce w usłudze HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [.NET za pomocą technologii Hive i Pig w usłudze HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Tworzenie rozwiązań C# z systemu Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Migracja rozwiązań platformy .NET usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Aby uzyskać więcej informacji dotyczących za pomocą akcji skryptu, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)