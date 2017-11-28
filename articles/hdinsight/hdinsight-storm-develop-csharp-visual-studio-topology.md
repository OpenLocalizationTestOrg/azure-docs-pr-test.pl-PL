---
title: aaaApache topologii Storm z programu Visual Studio i C# - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate topologii Storm w języku C#. Utworzyć topologię, liczba proste programu word w Visual Studio za pomocą narzędzi Hadoop hello for Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="37d10-104">Tworzenie topologii C# dla Apache Storm przy użyciu narzędzi Data Lake hello for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37d10-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="37d10-105">Dowiedz się, jak toocreate topologii Storm C# za pomocą usługi Azure Data Lake (Hadoop) z hello narzędzia dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37d10-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="37d10-106">Ten dokument przeprowadzi Cię przez proces hello Tworzenie projektu Storm w Visual Studio, testowanie go lokalnie i wdrażania go tooan Apache Storm w klastrze usługi HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="37d10-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="37d10-107">Możesz także dowiedzieć się, jak toocreate hybrydowe topologie, wykorzystujące składniki C# i Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="37d10-108">Gdy hello kroków w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, hello skompilowany projekt może mieć tooeither przesyłanego klastra z systemem Linux lub HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="37d10-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="37d10-109">Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.</span><span class="sxs-lookup"><span data-stu-id="37d10-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="37d10-110">Topologia toouse C# z opartą na systemie Linux klaster, należy zaktualizować hello pakietu Microsoft.SCP.Net.SDK NuGet używany przez tooversion Twojego projektu 0.10.0.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="37d10-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="37d10-111">Hello wersję pakietu hello musi być również zgodna wersja główna hello Storm zainstalowany w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="37d10-112">Wersja usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-112">HDInsight version</span></span> | <span data-ttu-id="37d10-113">Wersja platformy STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-113">Storm version</span></span> | <span data-ttu-id="37d10-114">Wersja SCP.NET</span><span class="sxs-lookup"><span data-stu-id="37d10-114">SCP.NET version</span></span> | <span data-ttu-id="37d10-115">Domyślna wersja Mono</span><span class="sxs-lookup"><span data-stu-id="37d10-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="37d10-116">3.3</span><span class="sxs-lookup"><span data-stu-id="37d10-116">3.3</span></span> |<span data-ttu-id="37d10-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="37d10-117">0.10.x</span></span> |<span data-ttu-id="37d10-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="37d10-118">0.10.x.x</span></span></br><span data-ttu-id="37d10-119">(tylko w usłudze HDInsight opartych na systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="37d10-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="37d10-120">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="37d10-120">NA</span></span> |
| <span data-ttu-id="37d10-121">3.4</span><span class="sxs-lookup"><span data-stu-id="37d10-121">3.4</span></span> | <span data-ttu-id="37d10-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="37d10-122">0.10.0.x</span></span> | <span data-ttu-id="37d10-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="37d10-123">0.10.0.x</span></span> | <span data-ttu-id="37d10-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="37d10-124">3.2.8</span></span> |
| <span data-ttu-id="37d10-125">3,5</span><span class="sxs-lookup"><span data-stu-id="37d10-125">3.5</span></span> | <span data-ttu-id="37d10-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="37d10-126">1.0.2.x</span></span> | <span data-ttu-id="37d10-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="37d10-127">1.0.0.x</span></span> | <span data-ttu-id="37d10-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="37d10-128">4.2.1</span></span> |
| <span data-ttu-id="37d10-129">3.6</span><span class="sxs-lookup"><span data-stu-id="37d10-129">3.6</span></span> | <span data-ttu-id="37d10-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="37d10-130">1.1.0.x</span></span> | <span data-ttu-id="37d10-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="37d10-131">1.0.0.x</span></span> | <span data-ttu-id="37d10-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="37d10-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="37d10-133">Topologie języka C# w klastrach opartych na systemie Linux należy użyć .NET 4.5 i użyj Mono toorun na powitania klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="37d10-134">Sprawdź [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="37d10-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="37d10-135">Instalacja programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37d10-135">Install Visual Studio</span></span>

<span data-ttu-id="37d10-136">Topologie języka C# z SCP.NET można tworzyć przy użyciu jednej z hello następujące wersje programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="37d10-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="37d10-137">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="37d10-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="37d10-138">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="37d10-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="37d10-139">Program Visual Studio 2015 lub [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="37d10-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="37d10-140">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="37d10-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="37d10-141">Zainstaluj Data Lake tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37d10-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="37d10-142">tooinstall Data Lake tools dla programu Visual Studio, wykonaj kroki hello w [rozpocząć korzystanie z usługi Data Lake tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="37d10-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="37d10-143">Instalowanie języka Java</span><span class="sxs-lookup"><span data-stu-id="37d10-143">Install Java</span></span>

<span data-ttu-id="37d10-144">Podczas przesyłania topologii Storm z programu Visual Studio SCP.NET generuje plik zip, który zawiera hello topologii i zależności.</span><span class="sxs-lookup"><span data-stu-id="37d10-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="37d10-145">Java jest używane toocreate te Kompresuj pliki, ponieważ używa ona formatu, który jest bardziej zgodne z opartą na systemie Linux klastrów.</span><span class="sxs-lookup"><span data-stu-id="37d10-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="37d10-146">Zainstaluj hello Java Developer Kit (JDK) 7 lub nowszego środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="37d10-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="37d10-147">Możesz uzyskać hello JDK Oracle z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="37d10-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="37d10-148">Można również użyć [innych dystrybucje Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="37d10-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="37d10-149">Witaj `JAVA_HOME` środowiska zmiennej musi toohello punktu katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="37d10-150">Witaj `PATH` zmiennej środowiskowej musi zawierać hello `%JAVA_HOME%\bin` katalogu.</span><span class="sxs-lookup"><span data-stu-id="37d10-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="37d10-151">Program hello C# console application tooverify że Java i hello JDK są prawidłowo zainstalowane następujące:</span><span class="sxs-lookup"><span data-stu-id="37d10-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="37d10-152">Szablony STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-152">Storm templates</span></span>

<span data-ttu-id="37d10-153">Witaj usługi Data Lake tools dla Visual Studio zawierają hello następujące szablony:</span><span class="sxs-lookup"><span data-stu-id="37d10-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="37d10-154">Typ projektu</span><span class="sxs-lookup"><span data-stu-id="37d10-154">Project type</span></span> | <span data-ttu-id="37d10-155">Pokazuje</span><span class="sxs-lookup"><span data-stu-id="37d10-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="37d10-156">Aplikacja STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-156">Storm Application</span></span> |<span data-ttu-id="37d10-157">Pusty projekt topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="37d10-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="37d10-158">Przykładowy składnik zapisywania usługi Azure SQL STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="37d10-159">Jak tooAzure toowrite bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="37d10-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="37d10-160">Przykładowe czytnika rozwiązania Cosmos Azure DB STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="37d10-161">Jak tooread z bazy danych usługi Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="37d10-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="37d10-162">Przykładowy składnik zapisywania rozwiązania Cosmos Azure DB STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="37d10-163">Jak tooAzure toowrite DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="37d10-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="37d10-164">Przykładowe czytnika EventHub STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="37d10-165">Jak tooread z usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="37d10-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="37d10-166">Przykładowy składnik zapisywania EventHub STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="37d10-167">Jak tooAzure toowrite usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="37d10-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="37d10-168">Przykładowe bazy danych HBase czytnika STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="37d10-169">Jak tooread z bazy danych HBase w usłudze HDInsight klastrów.</span><span class="sxs-lookup"><span data-stu-id="37d10-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="37d10-170">Przykładowe bazy danych HBase zapisywania STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="37d10-171">Jak klastrów tooHBase toowrite w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="37d10-172">Przykład hybrydowego STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="37d10-173">Jak toouse składnika Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="37d10-174">Przykładowe STORM</span><span class="sxs-lookup"><span data-stu-id="37d10-174">Storm Sample</span></span> |<span data-ttu-id="37d10-175">Topologii liczby podstawowych programu word.</span><span class="sxs-lookup"><span data-stu-id="37d10-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="37d10-176">Nie wszystkie szablony będzie działać z opartą na systemie Linux usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="37d10-177">Pakiety Nuget służące przez hello szablony mogą być niezgodne z Mono.</span><span class="sxs-lookup"><span data-stu-id="37d10-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="37d10-178">Sprawdź hello [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentów i użyj hello [analizator przenośność .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="37d10-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="37d10-179">W hello kroków w tym dokumencie należy użyć hello Podstawowa aplikacja Storm projektu typu toocreate topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="37d10-180">Informacje o szablonach HBase</span><span class="sxs-lookup"><span data-stu-id="37d10-180">HBase templates notes</span></span>

<span data-ttu-id="37d10-181">Hello czytnika HBase i szablony zapisywania użyć hello interfejsu API REST HBase, nie hello HBase interfejsu API języka Java, toocommunicate z bazy danych HBase w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="37d10-182">Informacje o szablonach EventHub</span><span class="sxs-lookup"><span data-stu-id="37d10-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37d10-183">Witaj opartych na języku Java EventHub spout składnika dołączonego hello czytnika EventHub szablonu nie może działać z systemu Storm w usłudze HDInsight w wersji 3.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="37d10-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="37d10-184">Zaktualizowana wersja tego składnika jest dostępna w [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="37d10-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="37d10-185">Aby przykładową topologię, która używa tej składnika i współpracuje z systemu Storm w usłudze HDInsight 3.5, zobacz [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="37d10-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="37d10-186">Tworzenie topologii C#</span><span class="sxs-lookup"><span data-stu-id="37d10-186">Create a C# topology</span></span>

1. <span data-ttu-id="37d10-187">Otwórz program Visual Studio, wybierz **pliku** > **nowy**, a następnie wybierz **projektu**.</span><span class="sxs-lookup"><span data-stu-id="37d10-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="37d10-188">Z hello **nowy projekt** okna, rozwiń węzeł **zainstalowana** > **szablony**i wybierz **usługi Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="37d10-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="37d10-189">Wybierz z listy hello szablonów **aplikacji Storm**.</span><span class="sxs-lookup"><span data-stu-id="37d10-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="37d10-190">U dołu hello hello ekranu, wprowadź **WordCount** jako nazwa hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Zrzut ekranu nowego projektu okna](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="37d10-192">Po utworzeniu projektu hello powinny mieć hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="37d10-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="37d10-193">**Plik program.cs**: plik definiuje hello topologii dla projektu.</span><span class="sxs-lookup"><span data-stu-id="37d10-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="37d10-194">Domyślnie zostanie utworzona domyślną topologię, która składa się z jednego spout i jeden bolt.</span><span class="sxs-lookup"><span data-stu-id="37d10-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="37d10-195">**Spout.cs**: spout przykład, który emituje liczb losowych.</span><span class="sxs-lookup"><span data-stu-id="37d10-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="37d10-196">**Bolt.cs**: przykład bolt, który śledzi liczbę elementów emitowane przez hello spout.</span><span class="sxs-lookup"><span data-stu-id="37d10-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="37d10-197">Podczas tworzenia projektu hello NuGet pobieranie najnowszych hello [pakietu SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="37d10-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="37d10-198">Spout hello wdrożenie</span><span class="sxs-lookup"><span data-stu-id="37d10-198">Implement hello spout</span></span>

1. <span data-ttu-id="37d10-199">Otwórz **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="37d10-199">Open **Spout.cs**.</span></span> <span data-ttu-id="37d10-200">Elementach spout są używane tooread danych w topologii z zewnętrznego źródła.</span><span class="sxs-lookup"><span data-stu-id="37d10-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="37d10-201">główne składniki powitania dla spout są:</span><span class="sxs-lookup"><span data-stu-id="37d10-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="37d10-202">**NextTuple**: wywoływane przez Storm, gdy elementy spout hello jest dozwolone tooemit krotek nowe.</span><span class="sxs-lookup"><span data-stu-id="37d10-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="37d10-203">**Potwierdzenia** (tylko w przypadku topologii transakcyjnych): obsługuje inicjowane przez inne składniki w topologii hello krotek wysyłane z hello spout potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="37d10-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="37d10-204">Potwierdzeniem krotka umożliwia spout hello wiedzieć, że jej został pomyślnie przetworzony przez składniki podrzędne.</span><span class="sxs-lookup"><span data-stu-id="37d10-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="37d10-205">**Niepowodzenie** (tylko w przypadku topologii transakcyjnych): obsługuje krotek, które są niepowodzenie przetwarzania innych składników w topologii hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="37d10-206">Implementacja metody niepowodzenie umożliwia toore-Emituj hello spójnej kolekcji, dzięki czemu mogą być przetwarzane ponownie.</span><span class="sxs-lookup"><span data-stu-id="37d10-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="37d10-207">Zamień zawartość hello hello **Spout** klasy z hello następującego tekstu.</span><span class="sxs-lookup"><span data-stu-id="37d10-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="37d10-208">Ta spout losowo emituje zdania na powitania topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="37d10-209">Bolts hello wdrożenie</span><span class="sxs-lookup"><span data-stu-id="37d10-209">Implement hello bolts</span></span>

1. <span data-ttu-id="37d10-210">Usunięcie istniejących hello **Bolt.cs** plik z projektu hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="37d10-211">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Dodaj** > **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="37d10-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="37d10-212">Wybierz z listy hello **Storm Bolt**, a następnie wprowadź **Splitter.cs** jako nazwa hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="37d10-213">Powtórz ten proces toocreate, drugi bolt o nazwie **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="37d10-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="37d10-214">**Splitter.cs**: implementuje elementu bolt, który dzieli zdania na poszczególnych wyrazów i emituje nowego strumienia słów.</span><span class="sxs-lookup"><span data-stu-id="37d10-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="37d10-215">**Counter.cs**: implementuje elementu bolt, który zlicza każdego wyrazu i emituje nowego strumienia słów i liczby powitania dla każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="37d10-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="37d10-216">Tych elementów bolt odczytu i zapisu toostreams, ale można również użyć bolt toocommunicate ze źródeł, takich jak bazy danych lub usługi.</span><span class="sxs-lookup"><span data-stu-id="37d10-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="37d10-217">Otwórz **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="37d10-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="37d10-218">Domyślnie ma tylko jedną metodę: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="37d10-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="37d10-219">Witaj metody Execute jest wywoływane, gdy hello bolt odbiera tuple do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="37d10-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="37d10-220">W tym miejscu możesz przeczytać i przetwarzania przychodzących krotek i Emituj krotek wychodzących.</span><span class="sxs-lookup"><span data-stu-id="37d10-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="37d10-221">Zamień zawartość hello hello **podziału** klasy z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="37d10-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="37d10-222">Otwórz **Counter.cs**i Zastąp zawartość klasy hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37d10-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="37d10-223">Zdefiniuj topologię hello</span><span class="sxs-lookup"><span data-stu-id="37d10-223">Define hello topology</span></span>

<span data-ttu-id="37d10-224">Elementach spout i elementów bolt są rozmieszczone na wykresie, który definiuje sposób hello dane przepływają między składnikami.</span><span class="sxs-lookup"><span data-stu-id="37d10-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="37d10-225">Ta topologia wykres hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="37d10-225">For this topology, hello graph is as follows:</span></span>

![Diagram przedstawiający sposób rozmieszczenia elementów](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="37d10-227">Zdania są emitowane z hello spout i są rozproszone tooinstances z hello podziału bolt.</span><span class="sxs-lookup"><span data-stu-id="37d10-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="37d10-228">bolt podziału Hello dzieli hello zdań w wyrazy, które są rozproszone toohello licznika bolt.</span><span class="sxs-lookup"><span data-stu-id="37d10-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="37d10-229">Ponieważ wyrazów jest przechowywanych lokalnie w wystąpienia licznika hello, chcemy się upewnić, że określone wyrazy przepływ toohello toomake tego samego wystąpienia bolt licznika.</span><span class="sxs-lookup"><span data-stu-id="37d10-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="37d10-230">Każde wystąpienie przechowuje informacje o słów.</span><span class="sxs-lookup"><span data-stu-id="37d10-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="37d10-231">Ponieważ bolt podziału hello przechowuje bez stanu, rzeczywiście nie ma znaczenia, którego wystąpienia podziału hello otrzymuje zdanie, które.</span><span class="sxs-lookup"><span data-stu-id="37d10-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="37d10-232">Otwórz **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="37d10-232">Open **Program.cs**.</span></span> <span data-ttu-id="37d10-233">Metoda ważne Hello jest **GetTopologyBuilder**, które jest używane toodefine hello topologię, która jest przesyłany tooStorm.</span><span class="sxs-lookup"><span data-stu-id="37d10-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="37d10-234">Zamień zawartość hello **GetTopologyBuilder** z powitania po topologii hello tooimplement kodu opisanych powyżej:</span><span class="sxs-lookup"><span data-stu-id="37d10-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="37d10-235">Przedstawia topologię hello</span><span class="sxs-lookup"><span data-stu-id="37d10-235">Submit hello topology</span></span>

1. <span data-ttu-id="37d10-236">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="37d10-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37d10-237">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37d10-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="37d10-238">Jeśli masz więcej niż jedną subskrypcję, zaloguj się toohello, który zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="37d10-239">Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="37d10-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="37d10-240">Można monitorować, jeśli przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="37d10-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="37d10-241">Gdy topologia hello został pomyślnie przesłany, hello **topologii Storm** dla klastra hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="37d10-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="37d10-242">Wybierz hello **WordCount** topologii z hello listy tooview informacji na temat hello systemem topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37d10-243">Można również wyświetlić **topologii Storm** z **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="37d10-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="37d10-244">Rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy klaster Storm w usłudze HDInsight, a następnie wybierz **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="37d10-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="37d10-245">tooview informacji o składnikach hello topologii hello, kliknij dwukrotnie składnik hello hello diagramie.</span><span class="sxs-lookup"><span data-stu-id="37d10-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="37d10-246">Z hello **podsumowanie topologii** wyświetlić, kliknij przycisk **Kill** toostop hello topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37d10-247">Topologii STORM nadal toorun, dopóki nie zostaną one wyłączone lub klaster hello jest usunięty.</span><span class="sxs-lookup"><span data-stu-id="37d10-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="37d10-248">Topologia transakcyjne</span><span class="sxs-lookup"><span data-stu-id="37d10-248">Transactional topology</span></span>

<span data-ttu-id="37d10-249">Topologia poprzedniej Hello jest nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="37d10-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="37d10-250">składniki Hello w topologii hello implementuje funkcje tooreplaying wiadomości.</span><span class="sxs-lookup"><span data-stu-id="37d10-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="37d10-251">Na przykład transakcyjne topologii Utwórz projekt i wybierz **próbki Storm** jako hello typu projektu.</span><span class="sxs-lookup"><span data-stu-id="37d10-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="37d10-252">Topologie transakcyjne zaimplementować powitania po toosupport powtarzania danych:</span><span class="sxs-lookup"><span data-stu-id="37d10-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="37d10-253">**Buforowanie metadanych**: hello spout muszą być przechowywane metadane dotyczące danych hello wysyłanego, dzięki czemu hello danych można je pobrać i wysyłanego ponownie, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="37d10-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="37d10-254">Ponieważ hello danych emitowanych przez próbki hello jest mały, hello danych pierwotnych dla każdej krotki są przechowywane w słowniku powtarzania.</span><span class="sxs-lookup"><span data-stu-id="37d10-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="37d10-255">**Potwierdzenia**: każdego bolt w topologii hello można wywołać `this.ctx.Ack(tuple)` tooacknowledge, że pomyślnie przetworzył spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="37d10-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="37d10-256">Witaj w przypadku wszystkich elementów bolt prześledzone hello krotki, `Ack` wywoływana jest metoda hello spout.</span><span class="sxs-lookup"><span data-stu-id="37d10-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="37d10-257">Witaj `Ack` metody umożliwia hello spout tooremove danych, który był buforowany powtarzania.</span><span class="sxs-lookup"><span data-stu-id="37d10-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="37d10-258">**Niepowodzenie**: każdego bolt można wywołać `this.ctx.Fail(tuple)` tooindicate przetwarzanie nie powiodło się dla spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="37d10-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="37d10-259">Błąd Hello propaguje toohello `Fail` metody spout hello, w którym krotki hello można odtworzyć za pomocą buforowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="37d10-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="37d10-260">**Identyfikator sekwencji**: podczas emitowania krotka, można określić identyfikator unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="37d10-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="37d10-261">Ta wartość określa krotki hello przetwarzania powtórzeń (Ack i błędów).</span><span class="sxs-lookup"><span data-stu-id="37d10-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="37d10-262">Na przykład Witaj spout w hello **próbki Storm** projekt używa następujących hello podczas emitowania danych:</span><span class="sxs-lookup"><span data-stu-id="37d10-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="37d10-263">Ten kod emituje krotka zawiera zdanie toohello domyślny strumień, z identyfikatorem sekwencji hello zawarte w **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="37d10-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="37d10-264">Na przykład **lastSeqId** jest zwiększany dla każdego krotki wysyłanego.</span><span class="sxs-lookup"><span data-stu-id="37d10-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="37d10-265">Jak pokazano w hello **próbki Storm** projektu, czy składnik jest transakcyjna można ustawić w czasie wykonywania na podstawie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="37d10-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="37d10-266">Hybrydowych topologii C# i Java</span><span class="sxs-lookup"><span data-stu-id="37d10-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="37d10-267">Umożliwia także Data Lake tools dla Visual Studio toocreate hybrydowe topologie, gdzie są niektóre składniki C#, a niektóre Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="37d10-268">Na przykład topologii hybrydowego Utwórz projekt i wybierz **przykład hybrydowego Storm**.</span><span class="sxs-lookup"><span data-stu-id="37d10-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="37d10-269">Ten typ przykładowych pokazano hello następujące pojęcia:</span><span class="sxs-lookup"><span data-stu-id="37d10-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="37d10-270">**Java spout** i **C# bolt**: zdefiniowanych w **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="37d10-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="37d10-271">Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="37d10-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="37d10-272">**C# spout** i **Java bolt**: zdefiniowanych w **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="37d10-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="37d10-273">Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="37d10-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="37d10-274">Ta wersja również pokazuje, jak toouse Clojure kodu z pliku tekstowego jako składnik Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="37d10-275">tooswitch hello topologię, która jest używana po przesłaniu hello projektu, po prostu przenieść hello `[Active(true)]` topologii toohello instrukcji ma toouse, przed przesłaniem go toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="37d10-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="37d10-276">Wszystkie pliki hello Java, które są wymagane są dostarczane jako część tego projektu w hello **JavaDependency** folderu.</span><span class="sxs-lookup"><span data-stu-id="37d10-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="37d10-277">Podczas tworzenia i przesyłania topologii hybrydowe, należy wziąć pod uwagę następujące hello:</span><span class="sxs-lookup"><span data-stu-id="37d10-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="37d10-278">Należy użyć **JavaComponentConstructor** toocreate wystąpienia hello Klasa Java spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="37d10-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="37d10-279">Należy używać **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON obiektów danych tooserialize do lub wychodzący składniki Java za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="37d10-280">Podczas przesyłania hello topologii toohello serwera, należy użyć hello **dodatkowe konfiguracje** hello toospecify opcji **ścieżki plików Java**.</span><span class="sxs-lookup"><span data-stu-id="37d10-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="37d10-281">Określona ścieżka Hello powinna być hello katalog, który zawiera pliki JAR hello, które zawierają klas Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="37d10-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="37d10-282">Azure Event Hubs</span></span>

<span data-ttu-id="37d10-283">Wersja SCP.NET 0.9.4.203 wprowadza nowe klasy i metody specjalnie z myślą o pracy z hello spout Centrum zdarzeń (Java spout, służącą do odczytywania z usługi Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="37d10-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="37d10-284">Po utworzeniu topologię, która używa spout Centrum zdarzeń Użyj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="37d10-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="37d10-285">**EventHubSpoutConfig** klasy: tworzy obiekt zawierający konfigurację hello hello spout składnika.</span><span class="sxs-lookup"><span data-stu-id="37d10-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="37d10-286">**TopologyBuilder.SetEventHubSpout** metody: dodaje hello Centrum zdarzeń spout składnika toohello topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="37d10-287">Możesz nadal korzystać hello **CustomizedInteropJSONSerializer** tooserialize dane generowane przez hello spout.</span><span class="sxs-lookup"><span data-stu-id="37d10-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="37d10-288"><a id="configurationmanager"></a>Użyj program Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="37d10-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="37d10-289">Nie używaj **ConfigurationManager** wartości konfiguracji tooretrieve z elementów bolt i spout składników.</span><span class="sxs-lookup"><span data-stu-id="37d10-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="37d10-290">W ten sposób może spowodować wyjątek pustego wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="37d10-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="37d10-291">Zamiast tego hello konfiguracji projektu jest przekazywany do topologii Storm hello jako pary kluczy i wartości w kontekście topologii hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="37d10-292">Każdego składnika, który korzysta z wartości konfiguracji musi pobrać je z kontekstu hello podczas inicjowania.</span><span class="sxs-lookup"><span data-stu-id="37d10-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="37d10-293">Witaj poniższy kod przedstawia sposób tooretrieve te wartości:</span><span class="sxs-lookup"><span data-stu-id="37d10-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="37d10-294">Jeśli używasz `Get` tooreturn metody instancję składnika, należy upewnić się, czy przekazaniem zarówno hello `Context` i `Dictionary<string, Object>` Konstruktor toohello parametrów.</span><span class="sxs-lookup"><span data-stu-id="37d10-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="37d10-295">Witaj przykładem jest podstawowy `Get` metodę, która poprawnie przekazuje te wartości:</span><span class="sxs-lookup"><span data-stu-id="37d10-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="37d10-296">Jak tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="37d10-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="37d10-297">Najnowsze wersje SCP.NET obsługuje uaktualnienie pakietu przez pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="37d10-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="37d10-298">Dostępna jest nowa aktualizacja, pojawi się powiadomienie uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="37d10-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="37d10-299">Sprawdź toomanually do uaktualnienia, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="37d10-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="37d10-300">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="37d10-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="37d10-301">Wybierz z Menedżera pakietów hello, **aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="37d10-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="37d10-302">Czy jest dostępna aktualizacja, są one dostępne.</span><span class="sxs-lookup"><span data-stu-id="37d10-302">If an update is available, it is listed.</span></span> <span data-ttu-id="37d10-303">Kliknij przycisk **aktualizacji** dla tooinstall pakietu hello go.</span><span class="sxs-lookup"><span data-stu-id="37d10-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37d10-304">Jeśli projekt został utworzony przy użyciu starszej wersji SCP.NET, który nie używa NuGet, należy wykonać hello następujące kroki tooupdate tooa nowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="37d10-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="37d10-305">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="37d10-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="37d10-306">Przy użyciu hello **wyszukiwania** pola, Wyszukaj, a następnie dodaj **Microsoft.SCP.Net.SDK** toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="37d10-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="37d10-307">Rozwiązywanie typowych problemów z topologii</span><span class="sxs-lookup"><span data-stu-id="37d10-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="37d10-308">Wyjątki wskaźnika o wartości null</span><span class="sxs-lookup"><span data-stu-id="37d10-308">Null pointer exceptions</span></span>

<span data-ttu-id="37d10-309">Gdy używasz topologii C# z klastrem usługi HDInsight opartej na systemie Linux, blokowania i spout składników, które używają **ConfigurationManager** tooread ustawienia konfiguracji w czasie wykonywania mogą zwracać wyjątki wskaźnika o wartości null.</span><span class="sxs-lookup"><span data-stu-id="37d10-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="37d10-310">Hello konfiguracji projektu jest przekazywany do topologii Storm hello jako pary kluczy i wartości w kontekście topologii hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="37d10-311">Można go pobrać z hello słownika obiektu, który jest przekazywany tooyour składniki, gdy są one inicjowane.</span><span class="sxs-lookup"><span data-stu-id="37d10-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="37d10-312">Aby uzyskać więcej informacji, zobacz hello [ConfigurationManager](#configurationmanager) sekcji tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="37d10-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="37d10-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="37d10-313">System.TypeLoadException</span></span>

<span data-ttu-id="37d10-314">Jeśli używasz topologii C# z klastrem usługi HDInsight opartej na systemie Linux, możesz napotkać hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="37d10-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="37d10-315">Ten błąd występuje podczas używania pliku binarnego, który nie jest zgodny z wersją .NET, który obsługuje Mono hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="37d10-316">W przypadku klastrów usługi HDInsight opartej na systemie Linux upewnij się, że projekt korzysta z plików binarnych skompilowanego dla platformy .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="37d10-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="37d10-317">Testowanie topologii lokalnie</span><span class="sxs-lookup"><span data-stu-id="37d10-317">Test a topology locally</span></span>

<span data-ttu-id="37d10-318">Chociaż jest łatwe toodeploy klastra tooa topologii, w niektórych przypadkach może być konieczne tootest topologii lokalnie.</span><span class="sxs-lookup"><span data-stu-id="37d10-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="37d10-319">Następujące kroki toorun hello i testów hello przykładową topologię w tym samouczku lokalnie w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="37d10-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="37d10-320">Testowanie lokalnym działa tylko dla basic, C# — tylko topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="37d10-321">Nie można użyć lokalnego testowanie pod kątem hybrydowe topologie lub topologie, wykorzystujące wiele strumieni.</span><span class="sxs-lookup"><span data-stu-id="37d10-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="37d10-322">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="37d10-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="37d10-323">We właściwościach projektu hello, zmień hello **Output typu** za**aplikacji konsoli**.</span><span class="sxs-lookup"><span data-stu-id="37d10-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Zrzut ekranu przedstawiający właściwości projektu z wyróżnionym typem danych wyjściowych](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="37d10-325">Pamiętaj toochange hello **Output typu** za tworzenie kopii**biblioteki klas** przed wdrożeniem hello topologii tooa klastra.</span><span class="sxs-lookup"><span data-stu-id="37d10-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="37d10-326">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Dodaj** > **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="37d10-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="37d10-327">Wybierz **klasy**, a następnie wprowadź **LocalTest.cs** jako nazwa klasy hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="37d10-328">Na koniec kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="37d10-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="37d10-329">Otwórz **LocalTest.cs**i dodaj następujące hello **przy użyciu** instrukcji u góry hello:</span><span class="sxs-lookup"><span data-stu-id="37d10-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="37d10-330">Użyj hello poniższy kod jako zawartość hello hello **LocalTest** klasy:</span><span class="sxs-lookup"><span data-stu-id="37d10-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="37d10-331">Zająć tooread moment, za pośrednictwem hello komentarze w kodzie.</span><span class="sxs-lookup"><span data-stu-id="37d10-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="37d10-332">Ten kod zawiera **LocalContext** toorun hello składników w hello Środowisko deweloperskie, a będzie się powtarzał hello strumienia danych między plikami tootext składników na lokalnym dysku hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="37d10-333">Otwórz **Program.cs**i dodaj następujące toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="37d10-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="37d10-334">Zapisz zmiany hello, a następnie kliknij przycisk **F5** lub wybierz **debugowania** > **Rozpocznij debugowanie** toostart hello projektu.</span><span class="sxs-lookup"><span data-stu-id="37d10-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="37d10-335">Okno konsoli powinna wyświetlane i rejestrowania stanu hello testów postępu.</span><span class="sxs-lookup"><span data-stu-id="37d10-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="37d10-336">Gdy **testy zakończone** pojawia się, naciśnij klawisz w dowolnym oknie hello tooclose klucza.</span><span class="sxs-lookup"><span data-stu-id="37d10-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="37d10-337">Użyj **Eksploratora Windows** toolocate hello katalog, który zawiera projekt.</span><span class="sxs-lookup"><span data-stu-id="37d10-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="37d10-338">Na przykład: **C:\Users\<your_user_name > \Documents\Visual 2013\Projects\WordCount\WordCount w Studio**.</span><span class="sxs-lookup"><span data-stu-id="37d10-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="37d10-339">W tym katalogu, otwórz **Bin**, a następnie kliknij przycisk **debugowania**.</span><span class="sxs-lookup"><span data-stu-id="37d10-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="37d10-340">Powinny pojawić się hello plików tekstowych, które zostały utworzone podczas testów hello: sentences.txt, counter.txt i splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="37d10-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="37d10-341">Otwórz każdy plik tekstowy i sprawdzić hello danych.</span><span class="sxs-lookup"><span data-stu-id="37d10-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37d10-342">Ciąg danych będzie nadal występował jako tablica wartości dziesiętnych w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="37d10-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="37d10-343">Na przykład \[[97,103,111]] w hello **splitter.txt** pliku jest słowem hello *i*.</span><span class="sxs-lookup"><span data-stu-id="37d10-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="37d10-344">Należy się hello tooset **typ projektu** kopii za**biblioteki klas** przed wdrożeniem tooa Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="37d10-345">Informacje w Dzienniku</span><span class="sxs-lookup"><span data-stu-id="37d10-345">Log information</span></span>

<span data-ttu-id="37d10-346">Można łatwo rejestrowanie informacji z składniki topologii sieci, za pomocą `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="37d10-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="37d10-347">Na przykład następujące hello tworzy wpis informacyjny w dzienniku:</span><span class="sxs-lookup"><span data-stu-id="37d10-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="37d10-348">Zarejestrowane informacje mogą być wyświetlane z hello **dziennik usługi Hadoop**, który znajduje się w **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="37d10-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="37d10-349">Rozwiń pozycję powitania dla Storm w klastrze usługi HDInsight, a następnie rozwiń **dziennik usługi Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="37d10-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="37d10-350">Na koniec wybierz tooview pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="37d10-351">Witaj dzienniki są przechowywane w hello kontem magazynu platformy Azure, który jest używany przez klaster.</span><span class="sxs-lookup"><span data-stu-id="37d10-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="37d10-352">Dzienniki hello tooview w programie Visual Studio, musisz zalogować się toohello subskrypcji platformy Azure, który jest właścicielem konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="37d10-353">Wyświetl informacje o błędzie</span><span class="sxs-lookup"><span data-stu-id="37d10-353">View error information</span></span>

<span data-ttu-id="37d10-354">błędy tooview, które wystąpiły w uruchomionej topologii, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="37d10-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="37d10-355">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello Storm w klastrze usługi HDInsight i wybierz **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="37d10-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="37d10-356">Dla hello **Spout** i **Bolts**, hello **ostatniego błędu** kolumna zawiera informacje na temat hello ostatniego błędu.</span><span class="sxs-lookup"><span data-stu-id="37d10-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="37d10-357">Wybierz hello **Spout identyfikator** lub **identyfikator Bolt** hello składnika, który zawiera błąd na liście.</span><span class="sxs-lookup"><span data-stu-id="37d10-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="37d10-358">Na stronie szczegółów hello jest błąd wyświetlania, dodatkowe informacje są wymienione w hello **błędy** sekcji u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="37d10-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="37d10-359">tooobtain więcej informacji, wybierz opcję **portu** z hello **modułów** sekcji hello strony, toosee hello Storm procesu roboczego w dzienniku hello ostatnich kilka minut.</span><span class="sxs-lookup"><span data-stu-id="37d10-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="37d10-360">Błędy przesyłania topologii</span><span class="sxs-lookup"><span data-stu-id="37d10-360">Errors submitting topologies</span></span>

<span data-ttu-id="37d10-361">Jeśli wystąpią błędy przesyłania tooHDInsight topologii hello składników po stronie serwera, które obsługi przesyłania topologii w klastrze usługi HDInsight można znaleźć dzienników.</span><span class="sxs-lookup"><span data-stu-id="37d10-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="37d10-362">tooretrieve te dzienniki, użyj hello następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="37d10-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="37d10-363">Zastąp __sshuser__ z hello konta użytkownika SSH hello klastra.</span><span class="sxs-lookup"><span data-stu-id="37d10-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="37d10-364">Zastąp __clustername__ o nazwie hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37d10-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="37d10-365">Aby uzyskać więcej informacji na temat używania `scp` i `ssh` z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="37d10-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="37d10-366">Przesyłanie może zakończyć się niepowodzeniem kilka przyczyn:</span><span class="sxs-lookup"><span data-stu-id="37d10-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="37d10-367">JDK nie jest zainstalowany lub nie znajduje się w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="37d10-368">Wymagane zależności Java nie znajdują się w hello przesyłania.</span><span class="sxs-lookup"><span data-stu-id="37d10-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="37d10-369">Niezgodne zależności.</span><span class="sxs-lookup"><span data-stu-id="37d10-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="37d10-370">Zduplikowane nazwy topologii.</span><span class="sxs-lookup"><span data-stu-id="37d10-370">Duplicate topology names.</span></span>

<span data-ttu-id="37d10-371">Jeśli hello `hdinsight-scpwebapi.out` dziennik zawiera `FileNotFoundException`, może to być spowodowane hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="37d10-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="37d10-372">Witaj JDK nie jest w ścieżce hello na powitania Środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="37d10-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="37d10-373">Sprawdź, że hello JDK jest zainstalowany w hello Środowisko deweloperskie, który `%JAVA_HOME%/bin` znajduje się w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="37d10-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="37d10-374">Brak zależności Java.</span><span class="sxs-lookup"><span data-stu-id="37d10-374">You are missing a Java dependency.</span></span> <span data-ttu-id="37d10-375">Upewnij się, że łącznie z plikami wymagane JAR jako część hello przesyłania.</span><span class="sxs-lookup"><span data-stu-id="37d10-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37d10-376">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37d10-376">Next steps</span></span>

<span data-ttu-id="37d10-377">Na przykład przetwarzania danych z usługi Event Hubs, zobacz [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="37d10-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="37d10-378">Na przykład topologii C#, która dzieli strumienia danych na wiele strumieni zobacz [przykład C# Storm](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="37d10-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="37d10-379">Zobacz więcej informacji o tworzeniu topologie języka C#, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="37d10-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="37d10-380">Więcej sposobów toowork z usługą HDInsight i więcej Storm na próbkach HDInsight Zobacz hello następujące dokumenty:</span><span class="sxs-lookup"><span data-stu-id="37d10-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="37d10-381">**SCP.NET firmy Microsoft**</span><span class="sxs-lookup"><span data-stu-id="37d10-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="37d10-382">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="37d10-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="37d10-383">**Apache Storm w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="37d10-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="37d10-384">Wdrażanie i monitorowanie topologii z systemu Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="37d10-385">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="37d10-386">**Apache Hadoop w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="37d10-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="37d10-387">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="37d10-388">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="37d10-389">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="37d10-390">**Bazy danych Apache HBase w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="37d10-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="37d10-391">Wprowadzenie do korzystania z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="37d10-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
