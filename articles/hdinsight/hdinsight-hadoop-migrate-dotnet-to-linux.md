---
title: ".NET za pomocą MapReduce z Hadoop w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z aplikacji .NET do przesyłania strumieniowego MapReduce na HDInsight opartych na systemie Linux."
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
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="f904b-103">Migracja rozwiązań .NET dla komputerów z systemem Windows usługi HDInsight w usłudze HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f904b-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="f904b-104">Opartych na systemie Linux klastrów usługi HDInsight użyj [Mono (https://mono-project.com)](https://mono-project.com) na uruchamianie aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="f904b-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="f904b-105">Mono umożliwia .NET składników, takich jak MapReduce aplikacje za pomocą usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f904b-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="f904b-106">W tym dokumencie Dowiedz się, jak przeprowadzić migrację rozwiązania .NET utworzone dla komputerów z systemem Windows w usłudze hdinsight do pracy z Mono na HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f904b-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="f904b-107">Mono zgodności z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="f904b-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="f904b-108">Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5.</span><span class="sxs-lookup"><span data-stu-id="f904b-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="f904b-109">Aby uzyskać więcej informacji w wersji Mono dołączone do usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f904b-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f904b-110">Aby zainstalować określoną wersję Mono, zobacz [Zainstaluj lub zaktualizuj Mono](hdinsight-hadoop-install-mono.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f904b-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="f904b-111">Aby uzyskać szczegółowe informacje o zgodności Mono i .NET, zobacz [Mono zgodności (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f904b-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f904b-112">W ramach SCP.NET jest zgodny z Mono.</span><span class="sxs-lookup"><span data-stu-id="f904b-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="f904b-113">Aby uzyskać więcej informacji o używaniu SCP.NET z Mono, zobacz [program Visual Studio umożliwia tworzenie topologii C# dla Apache Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f904b-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="f904b-114">Przenośność zautomatyzowanych analiz</span><span class="sxs-lookup"><span data-stu-id="f904b-114">Automated portability analysis</span></span>

<span data-ttu-id="f904b-115">[Analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) może służyć do generowania raportu dotyczącego niezgodności między aplikacji i Mono.</span><span class="sxs-lookup"><span data-stu-id="f904b-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="f904b-116">Do skonfigurowania analizatora do sprawdzenia aplikacji przenośności Mono, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f904b-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="f904b-117">Zainstaluj [analizator przenośność .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="f904b-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="f904b-118">Podczas instalacji wybierz wersję programu Visual Studio do użycia.</span><span class="sxs-lookup"><span data-stu-id="f904b-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="f904b-119">Z programu Visual Studio 2015, wybierz __Analizuj__ > __ustawień analizatora przenośność__i upewnij się, że __4.5__ zaewidencjonowania __Mono__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="f904b-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 zaewidencjonowany Mono sekcji ustawień analizatora](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="f904b-121">Wybierz __OK__ Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="f904b-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="f904b-122">Wybierz __analizowanie__ > __analizowanie przenośności zestawu__.</span><span class="sxs-lookup"><span data-stu-id="f904b-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="f904b-123">Wybierz zestaw, który zawiera rozwiązania, a następnie wybierz __Otwórz__ rozpocząć analizy.</span><span class="sxs-lookup"><span data-stu-id="f904b-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="f904b-124">Po zakończeniu analizy wybierz __Analizuj__ > __przeglądać raporty analityczne__.</span><span class="sxs-lookup"><span data-stu-id="f904b-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="f904b-125">W __wyniki analizy przenośność__, wybierz pozycję __Otwórz raport__ aby otworzyć raport.</span><span class="sxs-lookup"><span data-stu-id="f904b-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Przenośność analizatora wyniki w oknie dialogowym](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="f904b-127">Analizatora nie może przechwycić każdy problem z rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f904b-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="f904b-128">Na przykład ścieżka pliku `c:\temp\file.txt` jest uznawany za poprawny, ponieważ Mono działa w systemie Windows, a ścieżka jest prawidłowa w tym kontekście.</span><span class="sxs-lookup"><span data-stu-id="f904b-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="f904b-129">Jednak ścieżka jest nieprawidłowa na platformie systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f904b-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="f904b-130">Ręczne przenośność analizy</span><span class="sxs-lookup"><span data-stu-id="f904b-130">Manual portability analysis</span></span>

<span data-ttu-id="f904b-131">Wykonaj inspekcji ręcznej w kodzie, korzystając z informacji w [przenośność aplikacji (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f904b-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="f904b-132">Zmodyfikuj i kompilacji</span><span class="sxs-lookup"><span data-stu-id="f904b-132">Modify and build</span></span>

<span data-ttu-id="f904b-133">Można nadal używać programu Visual Studio do tworzenia rozwiązań .NET dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f904b-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="f904b-134">Należy jednak upewnij się, że projekt jest skonfigurowany do używania programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f904b-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="f904b-135">Wdrażanie i testowanie</span><span class="sxs-lookup"><span data-stu-id="f904b-135">Deploy and test</span></span>

<span data-ttu-id="f904b-136">Po zmodyfikowaniu rozwiązania przy użyciu zalecenia z analizatora przenośność .NET lub ręcznej analizy, należy przetestować z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f904b-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="f904b-137">Testowanie rozwiązania w klastrze usługi HDInsight opartej na systemie Linux może ujawnić niewielkie problemy, które muszą zostać poprawione.</span><span class="sxs-lookup"><span data-stu-id="f904b-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="f904b-138">Firma Microsoft zaleca włączyć dodatkowe rejestrowanie w Twojej aplikacji podczas testowania go.</span><span class="sxs-lookup"><span data-stu-id="f904b-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="f904b-139">Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do dzienników można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="f904b-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="f904b-140">Uzyskiwanie dostępu do dzienników aplikacji usługi YARN w usłudze HDInsight opartej na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f904b-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="f904b-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f904b-141">Next steps</span></span>

* [<span data-ttu-id="f904b-142">Używanie języka C# z MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f904b-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="f904b-143">Funkcje zdefiniowane przez użytkownika w języku C# za pomocą technologii Hive i Pig</span><span class="sxs-lookup"><span data-stu-id="f904b-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="f904b-144">Tworzenie topologii C# dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f904b-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)