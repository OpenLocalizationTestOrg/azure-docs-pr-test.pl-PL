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
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="f7e48-103">Migracja rozwiązań .NET dla usługi HDInsight opartej na systemie Windows usługi HDInsight opartej na tooLinux</span><span class="sxs-lookup"><span data-stu-id="f7e48-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="f7e48-104">Opartych na systemie Linux klastrów usługi HDInsight użyj [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="f7e48-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="f7e48-105">Mono umożliwia toouse .NET składników, takich jak aplikacje MapReduce z opartą na systemie Linux usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7e48-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="f7e48-106">Dowiedz się, w tym dokumencie, sposobu tworzenia rozwiązań .NET toomigrate dla toowork klastrów usługi HDInsight opartej na systemie Windows z Mono na HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f7e48-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="f7e48-107">Mono zgodności z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="f7e48-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="f7e48-108">Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="f7e48-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="f7e48-109">Aby uzyskać więcej informacji na powitania wersji Mono dołączone do usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f7e48-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f7e48-110">tooinstall określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f7e48-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="f7e48-111">Aby uzyskać szczegółowe informacje o zgodności Mono i .NET, zobacz hello [Mono zgodności (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f7e48-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7e48-112">Hello SCP.NET framework jest zgodny z Mono.</span><span class="sxs-lookup"><span data-stu-id="f7e48-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="f7e48-113">Aby uzyskać więcej informacji o używaniu SCP.NET z Mono, zobacz [program Visual Studio topologii toodevelop C# dla Apache Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f7e48-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="f7e48-114">Przenośność zautomatyzowanych analiz</span><span class="sxs-lookup"><span data-stu-id="f7e48-114">Automated portability analysis</span></span>

<span data-ttu-id="f7e48-115">Witaj [analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) mogą być używane toogenerate raport o niezgodności między aplikacji i Mono.</span><span class="sxs-lookup"><span data-stu-id="f7e48-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="f7e48-116">Za pomocą aplikacji hello następujące kroki tooconfigure hello analizator toocheck przenośności Mono:</span><span class="sxs-lookup"><span data-stu-id="f7e48-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="f7e48-117">Zainstaluj hello [analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="f7e48-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="f7e48-118">Podczas instalacji wybierz wersję hello toouse programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7e48-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="f7e48-119">Z programu Visual Studio 2015, wybierz __Analizuj__ > __ustawień analizatora przenośność__i upewnij się, że __4.5__ zaewidencjonowania hello __Mono__  sekcji.</span><span class="sxs-lookup"><span data-stu-id="f7e48-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![zaewidencjonowano Mono sekcji ustawień analizatora hello 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="f7e48-121">Wybierz __OK__ toosave hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f7e48-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="f7e48-122">Wybierz __analizowanie__ > __analizowanie przenośności zestawu__.</span><span class="sxs-lookup"><span data-stu-id="f7e48-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="f7e48-123">Wybierz zestaw hello, który zawiera rozwiązania, a następnie wybierz __Otwórz__ toobegin analizy.</span><span class="sxs-lookup"><span data-stu-id="f7e48-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="f7e48-124">Po zakończeniu analizy wybierz __Analizuj__ > __przeglądać raporty analityczne__.</span><span class="sxs-lookup"><span data-stu-id="f7e48-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="f7e48-125">W __wyniki analizy przenośność__, wybierz pozycję __Otwórz raport__ tooopen raportu.</span><span class="sxs-lookup"><span data-stu-id="f7e48-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Przenośność analizatora wyniki w oknie dialogowym](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="f7e48-127">Analizator Hello nie może przechwycić każdy problem z rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7e48-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="f7e48-128">Na przykład ścieżka pliku `c:\temp\file.txt` jest uznawany za poprawny, ponieważ Mono działa w systemie Windows i hello ścieżka jest prawidłowa w tym kontekście.</span><span class="sxs-lookup"><span data-stu-id="f7e48-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="f7e48-129">Jednak hello ścieżka jest nieprawidłowa na platformie systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f7e48-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="f7e48-130">Ręczne przenośność analizy</span><span class="sxs-lookup"><span data-stu-id="f7e48-130">Manual portability analysis</span></span>

<span data-ttu-id="f7e48-131">Wykonaj inspekcji ręcznej w kodzie, korzystając z informacji hello hello [przenośność aplikacji (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f7e48-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="f7e48-132">Zmodyfikuj i kompilacji</span><span class="sxs-lookup"><span data-stu-id="f7e48-132">Modify and build</span></span>

<span data-ttu-id="f7e48-133">Możesz kontynuować toouse toobuild programu Visual Studio .NET rozwiązań dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7e48-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="f7e48-134">Należy jednak Sprawdź, czy hello projektu jest skonfigurowany toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f7e48-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="f7e48-135">Wdrażanie i testowanie</span><span class="sxs-lookup"><span data-stu-id="f7e48-135">Deploy and test</span></span>

<span data-ttu-id="f7e48-136">Po zmodyfikowaniu rozwiązania przy użyciu hello zalecenia z hello analizatora przenośność .NET lub ręcznej analizy, należy przetestować z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f7e48-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="f7e48-137">Testowanie rozwiązania hello w klastrze usługi HDInsight opartej na systemie Linux może ujawnić niewielkie problemy, które wymagają toobe rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="f7e48-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="f7e48-138">Firma Microsoft zaleca włączyć dodatkowe rejestrowanie w Twojej aplikacji podczas testowania go.</span><span class="sxs-lookup"><span data-stu-id="f7e48-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="f7e48-139">Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do dzienników Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="f7e48-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="f7e48-140">Uzyskiwanie dostępu do dzienników aplikacji usługi YARN w usłudze HDInsight opartej na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f7e48-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="f7e48-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7e48-141">Next steps</span></span>

* [<span data-ttu-id="f7e48-142">Używanie języka C# z MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f7e48-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="f7e48-143">Funkcje zdefiniowane przez użytkownika w języku C# za pomocą technologii Hive i Pig</span><span class="sxs-lookup"><span data-stu-id="f7e48-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="f7e48-144">Tworzenie topologii C# dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f7e48-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)