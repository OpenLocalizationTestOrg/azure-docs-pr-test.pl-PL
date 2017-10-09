---
title: "aaaUse .NET z MapReduce z Hadoop w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse aplikacji .NET do przesyłania strumieniowego MapReduce na HDInsight opartych na systemie Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Migracja rozwiązań .NET dla usługi HDInsight opartej na systemie Windows usługi HDInsight opartej na tooLinux

Opartych na systemie Linux klastrów usługi HDInsight użyj [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET. Mono umożliwia toouse .NET składników, takich jak aplikacje MapReduce z opartą na systemie Linux usługą HDInsight. Dowiedz się, w tym dokumencie, sposobu tworzenia rozwiązań .NET toomigrate dla toowork klastrów usługi HDInsight opartej na systemie Windows z Mono na HDInsight opartych na systemie Linux.

## <a name="mono-compatibility-with-net"></a>Mono zgodności z platformą .NET

Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5. Aby uzyskać więcej informacji na powitania wersji Mono dołączone do usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md). tooinstall określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.

Aby uzyskać szczegółowe informacje o zgodności Mono i .NET, zobacz hello [Mono zgodności (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentu.

> [!IMPORTANT]
> Hello SCP.NET framework jest zgodny z Mono. Aby uzyskać więcej informacji o używaniu SCP.NET z Mono, zobacz [program Visual Studio topologii toodevelop C# dla Apache Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Przenośność zautomatyzowanych analiz

Witaj [analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) mogą być używane toogenerate raport o niezgodności między aplikacji i Mono. Za pomocą aplikacji hello następujące kroki tooconfigure hello analizator toocheck przenośności Mono:

1. Zainstaluj hello [analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Podczas instalacji wybierz wersję hello toouse programu Visual Studio.

2. Z programu Visual Studio 2015, wybierz __Analizuj__ > __ustawień analizatora przenośność__i upewnij się, że __4.5__ zaewidencjonowania hello __Mono__  sekcji.

    ![zaewidencjonowano Mono sekcji ustawień analizatora hello 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Wybierz __OK__ toosave hello konfiguracji.

3. Wybierz __analizowanie__ > __analizowanie przenośności zestawu__. Wybierz zestaw hello, który zawiera rozwiązania, a następnie wybierz __Otwórz__ toobegin analizy.

4. Po zakończeniu analizy wybierz __Analizuj__ > __przeglądać raporty analityczne__. W __wyniki analizy przenośność__, wybierz pozycję __Otwórz raport__ tooopen raportu.

    ![Przenośność analizatora wyniki w oknie dialogowym](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Analizator Hello nie może przechwycić każdy problem z rozwiązania. Na przykład ścieżka pliku `c:\temp\file.txt` jest uznawany za poprawny, ponieważ Mono działa w systemie Windows i hello ścieżka jest prawidłowa w tym kontekście. Jednak hello ścieżka jest nieprawidłowa na platformie systemu Linux.

## <a name="manual-portability-analysis"></a>Ręczne przenośność analizy

Wykonaj inspekcji ręcznej w kodzie, korzystając z informacji hello hello [przenośność aplikacji (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) dokumentu.

## <a name="modify-and-build"></a>Zmodyfikuj i kompilacji

Możesz kontynuować toouse toobuild programu Visual Studio .NET rozwiązań dla usługi HDInsight. Należy jednak Sprawdź, czy hello projektu jest skonfigurowany toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Wdrażanie i testowanie

Po zmodyfikowaniu rozwiązania przy użyciu hello zalecenia z hello analizatora przenośność .NET lub ręcznej analizy, należy przetestować z usługą HDInsight. Testowanie rozwiązania hello w klastrze usługi HDInsight opartej na systemie Linux może ujawnić niewielkie problemy, które wymagają toobe rozwiązany. Firma Microsoft zaleca włączyć dodatkowe rejestrowanie w Twojej aplikacji podczas testowania go.

Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do dzienników Zobacz hello w następujących dokumentach:

* [Uzyskiwanie dostępu do dzienników aplikacji usługi YARN w usłudze HDInsight opartej na systemie Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Następne kroki

* [Używanie języka C# z MapReduce w usłudze HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Funkcje zdefiniowane przez użytkownika w języku C# za pomocą technologii Hive i Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Tworzenie topologii C# dla Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)