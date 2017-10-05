---
title: Topologii Apache Storm i Visual Studio C# - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Informacje o sposobie tworzenia topologii Storm w języku C#. Utworzyć topologię, liczba proste programu word w Visual Studio za pomocą narzędzia usługi Hadoop dla programu Visual Studio."
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="f0d98-104">Tworzenie topologii C# dla Apache Storm przy użyciu narzędzi Data Lake tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0d98-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="f0d98-105">Informacje o sposobie tworzenia topologii Storm C# za pomocą narzędzi usługi Azure Data Lake (Hadoop) dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0d98-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="f0d98-106">Ten dokument przeprowadzi Cię przez proces tworzenia projektu Storm w programie Visual Studio, testowanie go lokalnie i wdrażania go do systemu Apache Storm w klastrze usługi HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d98-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="f0d98-107">Możesz również Dowiedz się, jak tworzyć hybrydowe topologie, korzystających z języka C# i składniki Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d98-108">Podczas czynności opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, skompilowany projekt może zostać przesłane do klastra z systemem Linux lub HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="f0d98-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="f0d98-109">Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.</span><span class="sxs-lookup"><span data-stu-id="f0d98-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="f0d98-110">Aby użyć topologii C# z klastrem opartych na systemie Linux, musisz zaktualizować pakiet Microsoft.SCP.Net.SDK NuGet używany w projekcie do wersji 0.10.0.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f0d98-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="f0d98-111">Wersja pakietu musi być również zgodna z wersją główną systemu Storm zainstalowanego w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="f0d98-112">Wersja usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-112">HDInsight version</span></span> | <span data-ttu-id="f0d98-113">Wersja platformy STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-113">Storm version</span></span> | <span data-ttu-id="f0d98-114">Wersja SCP.NET</span><span class="sxs-lookup"><span data-stu-id="f0d98-114">SCP.NET version</span></span> | <span data-ttu-id="f0d98-115">Domyślna wersja Mono</span><span class="sxs-lookup"><span data-stu-id="f0d98-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="f0d98-116">3.3</span><span class="sxs-lookup"><span data-stu-id="f0d98-116">3.3</span></span> |<span data-ttu-id="f0d98-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-117">0.10.x</span></span> |<span data-ttu-id="f0d98-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-118">0.10.x.x</span></span></br><span data-ttu-id="f0d98-119">(tylko w usłudze HDInsight opartych na systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="f0d98-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="f0d98-120">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f0d98-120">NA</span></span> |
| <span data-ttu-id="f0d98-121">3.4</span><span class="sxs-lookup"><span data-stu-id="f0d98-121">3.4</span></span> | <span data-ttu-id="f0d98-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-122">0.10.0.x</span></span> | <span data-ttu-id="f0d98-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-123">0.10.0.x</span></span> | <span data-ttu-id="f0d98-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="f0d98-124">3.2.8</span></span> |
| <span data-ttu-id="f0d98-125">3,5</span><span class="sxs-lookup"><span data-stu-id="f0d98-125">3.5</span></span> | <span data-ttu-id="f0d98-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-126">1.0.2.x</span></span> | <span data-ttu-id="f0d98-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-127">1.0.0.x</span></span> | <span data-ttu-id="f0d98-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="f0d98-128">4.2.1</span></span> |
| <span data-ttu-id="f0d98-129">3.6</span><span class="sxs-lookup"><span data-stu-id="f0d98-129">3.6</span></span> | <span data-ttu-id="f0d98-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-130">1.1.0.x</span></span> | <span data-ttu-id="f0d98-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="f0d98-131">1.0.0.x</span></span> | <span data-ttu-id="f0d98-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="f0d98-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f0d98-133">Topologie C# w klastrach opartych na systemie Linux muszą korzystać z platformy .NET 4.5 i używać platformy Mono, aby mogły działać w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="f0d98-134">Sprawdź [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="f0d98-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="f0d98-135">Instalacja programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0d98-135">Install Visual Studio</span></span>

<span data-ttu-id="f0d98-136">Topologie języka C# z SCP.NET można tworzyć przy użyciu jednej z następujących wersji programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f0d98-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="f0d98-137">Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="f0d98-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="f0d98-138">Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="f0d98-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="f0d98-139">Program Visual Studio 2015 lub [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="f0d98-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="f0d98-140">Visual Studio 2017 (dowolna wersja)</span><span class="sxs-lookup"><span data-stu-id="f0d98-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="f0d98-141">Zainstaluj Data Lake tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0d98-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="f0d98-142">Aby zainstalować usługi Data Lake tools dla programu Visual Studio, postępuj zgodnie z instrukcjami [rozpocząć korzystanie z usługi Data Lake tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f0d98-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="f0d98-143">Instalowanie języka Java</span><span class="sxs-lookup"><span data-stu-id="f0d98-143">Install Java</span></span>

<span data-ttu-id="f0d98-144">Podczas przesyłania topologii Storm z programu Visual Studio SCP.NET generuje plik zip, który zawiera topologii i zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d98-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="f0d98-145">Java służy do tworzenia tych plików zip, ponieważ używa ona formatu, który jest bardziej zgodne z opartą na systemie Linux klastrów.</span><span class="sxs-lookup"><span data-stu-id="f0d98-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="f0d98-146">Zainstaluj Java Developer Kit (JDK) 7 lub nowszego środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="f0d98-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="f0d98-147">Możesz uzyskać JDK Oracle z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="f0d98-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="f0d98-148">Można również użyć [innych dystrybucje Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="f0d98-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="f0d98-149">`JAVA_HOME` Zmiennej środowiskowej musi wskazywać katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="f0d98-150">`PATH` Zmiennej środowiskowej musi zawierać `%JAVA_HOME%\bin` katalogu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="f0d98-151">Aby zweryfikować, że Java i zestaw JDK są prawidłowo zainstalowane, można użyć następujących aplikacji konsolowej C#:</span><span class="sxs-lookup"><span data-stu-id="f0d98-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="f0d98-152">Szablony STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-152">Storm templates</span></span>

<span data-ttu-id="f0d98-153">Narzędzia Data Lake dla programu Visual Studio zapewniają następujące szablony:</span><span class="sxs-lookup"><span data-stu-id="f0d98-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="f0d98-154">Typ projektu</span><span class="sxs-lookup"><span data-stu-id="f0d98-154">Project type</span></span> | <span data-ttu-id="f0d98-155">Pokazuje</span><span class="sxs-lookup"><span data-stu-id="f0d98-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="f0d98-156">Aplikacja STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-156">Storm Application</span></span> |<span data-ttu-id="f0d98-157">Pusty projekt topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="f0d98-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="f0d98-158">Przykładowy składnik zapisywania usługi Azure SQL STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="f0d98-159">Jak można zapisać do bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d98-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="f0d98-160">Przykładowe czytnika rozwiązania Cosmos Azure DB STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="f0d98-161">Jak można odczytać z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0d98-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="f0d98-162">Przykładowy składnik zapisywania rozwiązania Cosmos Azure DB STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="f0d98-163">Jak napisać do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0d98-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="f0d98-164">Przykładowe czytnika EventHub STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="f0d98-165">Jak można odczytać z usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f0d98-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="f0d98-166">Przykładowy składnik zapisywania EventHub STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="f0d98-167">Jak napisać usługi Azure Event hubs.</span><span class="sxs-lookup"><span data-stu-id="f0d98-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="f0d98-168">Przykładowe bazy danych HBase czytnika STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="f0d98-169">Jak można odczytać z bazy danych HBase w usłudze hdinsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="f0d98-170">Przykładowe bazy danych HBase zapisywania STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="f0d98-171">Sposób zapisywania do bazy danych HBase na klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="f0d98-172">Przykład hybrydowego STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="f0d98-173">Jak używać składnika Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-173">How to use a Java component.</span></span> |
| <span data-ttu-id="f0d98-174">Przykładowe STORM</span><span class="sxs-lookup"><span data-stu-id="f0d98-174">Storm Sample</span></span> |<span data-ttu-id="f0d98-175">Topologii liczby podstawowych programu word.</span><span class="sxs-lookup"><span data-stu-id="f0d98-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="f0d98-176">Nie wszystkie szablony będzie działać z opartą na systemie Linux usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="f0d98-177">Pakiety Nuget służące za pomocą szablonów nie może być zgodna z Mono.</span><span class="sxs-lookup"><span data-stu-id="f0d98-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="f0d98-178">Sprawdź [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentów i użyj [.NET przenośność analizator](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) do identyfikowania potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="f0d98-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="f0d98-179">Instrukcje w tym dokumencie umożliwia Podstawowa aplikacja Storm projektu typu Tworzenie topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="f0d98-180">Informacje o szablonach HBase</span><span class="sxs-lookup"><span data-stu-id="f0d98-180">HBase templates notes</span></span>

<span data-ttu-id="f0d98-181">Szablony HBase i zapisu Użyj interfejsu API REST HBase, nie HBase API języka Java, do komunikowania się z bazą danych HBase w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="f0d98-182">Informacje o szablonach EventHub</span><span class="sxs-lookup"><span data-stu-id="f0d98-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0d98-183">Składnik spout opartych na języku Java EventHub zawartych w szablonie czytnika EventHub nie mogą działać z Storm w usłudze HDInsight w wersji 3.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f0d98-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="f0d98-184">Zaktualizowana wersja tego składnika jest dostępna w [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="f0d98-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="f0d98-185">Aby przykładową topologię, która używa tej składnika i współpracuje z systemu Storm w usłudze HDInsight 3.5, zobacz [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="f0d98-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="f0d98-186">Tworzenie topologii C#</span><span class="sxs-lookup"><span data-stu-id="f0d98-186">Create a C# topology</span></span>

1. <span data-ttu-id="f0d98-187">Otwórz program Visual Studio, wybierz **pliku** > **nowy**, a następnie wybierz **projektu**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="f0d98-188">Z **nowy projekt** okna, rozwiń węzeł **zainstalowana** > **szablony**i wybierz **usługi Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="f0d98-189">Wybierz z listy szablonów **aplikacji Storm**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="f0d98-190">W dolnej części ekranu, wprowadź **WordCount** jako nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0d98-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Zrzut ekranu nowego projektu okna](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="f0d98-192">Po utworzeniu projektu, musisz mieć następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="f0d98-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="f0d98-193">**Plik program.cs**: plik definiuje topologii dla projektu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="f0d98-194">Domyślnie zostanie utworzona domyślną topologię, która składa się z jednego spout i jeden bolt.</span><span class="sxs-lookup"><span data-stu-id="f0d98-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="f0d98-195">**Spout.cs**: spout przykład, który emituje liczb losowych.</span><span class="sxs-lookup"><span data-stu-id="f0d98-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="f0d98-196">**Bolt.cs**: przykład bolt, który śledzi liczbę elementów emitowane przez elementy spout.</span><span class="sxs-lookup"><span data-stu-id="f0d98-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="f0d98-197">Podczas tworzenia projektu NuGet pobierze najnowszą [pakietu SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="f0d98-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="f0d98-198">Implementowanie spout</span><span class="sxs-lookup"><span data-stu-id="f0d98-198">Implement the spout</span></span>

1. <span data-ttu-id="f0d98-199">Otwórz **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-199">Open **Spout.cs**.</span></span> <span data-ttu-id="f0d98-200">Elementach spout są używane do odczytywania danych w topologii z zewnętrznego źródła.</span><span class="sxs-lookup"><span data-stu-id="f0d98-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="f0d98-201">Główne składniki spout są:</span><span class="sxs-lookup"><span data-stu-id="f0d98-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="f0d98-202">**NextTuple**: wywoływane przez Storm, gdy elementy spout może wyemitować krotek nowe.</span><span class="sxs-lookup"><span data-stu-id="f0d98-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="f0d98-203">**Potwierdzenia** (tylko w przypadku topologii transakcyjnych): obsługuje inicjowane przez inne składniki w topologii krotek wysyłane z spout potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="f0d98-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="f0d98-204">Potwierdzeniem krotka umożliwia spout wiedzieć, że jej został pomyślnie przetworzony przez składniki podrzędne.</span><span class="sxs-lookup"><span data-stu-id="f0d98-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="f0d98-205">**Niepowodzenie** (tylko w przypadku topologii transakcyjnych): obsługuje krotek, które są niepowodzenie przetwarzania innych składników w topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="f0d98-206">Implementacja metody błędów pozwala na ponowne Emituj spójnej kolekcji, dzięki czemu mogą być przetwarzane ponownie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="f0d98-207">Zastąp zawartość **Spout** klasy z następującym tekstem.</span><span class="sxs-lookup"><span data-stu-id="f0d98-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="f0d98-208">Spout ten emituje losowo zdanie w topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="f0d98-209">Implementowanie elementów bolt</span><span class="sxs-lookup"><span data-stu-id="f0d98-209">Implement the bolts</span></span>

1. <span data-ttu-id="f0d98-210">Usuń istniejącą **Bolt.cs** plik z projektu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="f0d98-211">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **Dodaj** > **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="f0d98-212">Wybierz z listy, **Storm Bolt**, a następnie wprowadź **Splitter.cs** jako nazwy.</span><span class="sxs-lookup"><span data-stu-id="f0d98-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="f0d98-213">Powtórz ten proces, aby utworzyć drugi bolt o nazwie **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="f0d98-214">**Splitter.cs**: implementuje elementu bolt, który dzieli zdania na poszczególnych wyrazów i emituje nowego strumienia słów.</span><span class="sxs-lookup"><span data-stu-id="f0d98-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="f0d98-215">**Counter.cs**: implementuje elementu bolt, który zlicza każdego wyrazu i emituje nowego strumienia słów i liczby dla każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f0d98-216">Tych elementów bolt odczytu i zapisu do strumieni, ale umożliwia także bolt do komunikowania się ze źródeł, takich jak bazy danych lub usługi.</span><span class="sxs-lookup"><span data-stu-id="f0d98-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="f0d98-217">Otwórz **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="f0d98-218">Domyślnie ma tylko jedną metodę: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="f0d98-219">Metody Execute jest wywoływane, gdy elementy bolt odbiera tuple do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="f0d98-220">W tym miejscu możesz przeczytać i przetwarzania przychodzących krotek i Emituj krotek wychodzących.</span><span class="sxs-lookup"><span data-stu-id="f0d98-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="f0d98-221">Zastąp zawartość **podziału** klasy następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="f0d98-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="f0d98-222">Otwórz **Counter.cs**i Zastąp zawartość klasy następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="f0d98-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="f0d98-223">Zdefiniuj topologię</span><span class="sxs-lookup"><span data-stu-id="f0d98-223">Define the topology</span></span>

<span data-ttu-id="f0d98-224">Elementach spout i elementów bolt są rozmieszczone na wykresie, która określa, jak dane przepływają między składnikami.</span><span class="sxs-lookup"><span data-stu-id="f0d98-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="f0d98-225">Ta topologia wykres jest w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f0d98-225">For this topology, the graph is as follows:</span></span>

![Diagram przedstawiający sposób rozmieszczenia elementów](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="f0d98-227">Zdania są emitowane z spout i są dystrybuowane do wystąpień bolt podziału.</span><span class="sxs-lookup"><span data-stu-id="f0d98-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="f0d98-228">Bolt podziału dzieli zdań w wyrazy, które są dystrybuowane do bolt licznika.</span><span class="sxs-lookup"><span data-stu-id="f0d98-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="f0d98-229">Ponieważ wyrazów jest przechowywanych lokalnie w wystąpieniu licznika, chcemy się upewnić się, że określone wyrazy przepływać do tego samego wystąpienia licznika bolt.</span><span class="sxs-lookup"><span data-stu-id="f0d98-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="f0d98-230">Każde wystąpienie przechowuje informacje o słów.</span><span class="sxs-lookup"><span data-stu-id="f0d98-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="f0d98-231">Ponieważ bolt podziału przechowuje bez stanu, naprawdę nie ma znaczenia, którego wystąpienia rozdzielacza otrzymuje zdanie, które.</span><span class="sxs-lookup"><span data-stu-id="f0d98-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="f0d98-232">Otwórz **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-232">Open **Program.cs**.</span></span> <span data-ttu-id="f0d98-233">Metoda ważne jest **GetTopologyBuilder**, które jest używane do definiowania topologia, z której zostało przesłane do systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="f0d98-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="f0d98-234">Zastąp zawartość **GetTopologyBuilder** z następujący kod do wdrożenia topologii opisanych powyżej:</span><span class="sxs-lookup"><span data-stu-id="f0d98-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="f0d98-235">Przedstawia topologię</span><span class="sxs-lookup"><span data-stu-id="f0d98-235">Submit the topology</span></span>

1. <span data-ttu-id="f0d98-236">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0d98-237">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d98-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="f0d98-238">Jeśli masz więcej niż jedną subskrypcję, zaloguj się do tego, który zawiera Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="f0d98-239">Wybierz Storm w klastrze usługi HDInsight z **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="f0d98-240">Można monitorować, jeśli przesyłanie zakończy się pomyślnie, za pomocą **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="f0d98-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="f0d98-241">Gdy topologia zostało pomyślnie przesłane, **topologii Storm** dla klastra powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="f0d98-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="f0d98-242">Wybierz **WordCount** topologii z listy, aby wyświetlić informacje o uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0d98-243">Można również wyświetlić **topologii Storm** z **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="f0d98-244">Rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy klaster Storm w usłudze HDInsight, a następnie wybierz **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="f0d98-245">Aby wyświetlić informacje o składnikach topologii, kliknij dwukrotnie składnik na diagramie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="f0d98-246">Z **podsumowanie topologii** wyświetlić, kliknij przycisk **Kill** przestanie topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0d98-247">Topologii STORM nadal uruchamiać, dopóki nie zostaną one wyłączone lub usunąć klastra.</span><span class="sxs-lookup"><span data-stu-id="f0d98-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="f0d98-248">Topologia transakcyjne</span><span class="sxs-lookup"><span data-stu-id="f0d98-248">Transactional topology</span></span>

<span data-ttu-id="f0d98-249">Poprzednie topologia jest nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="f0d98-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="f0d98-250">Składniki w topologii nie implementuje funkcje odtwarzanie wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f0d98-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="f0d98-251">Na przykład transakcyjne topologii Utwórz projekt i wybierz **próbki Storm** jako typ projektu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="f0d98-252">Topologie transakcyjne zaimplementować następujące polecenie, aby obsługiwać powtarzania danych:</span><span class="sxs-lookup"><span data-stu-id="f0d98-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="f0d98-253">**Buforowanie metadanych**: spout muszą być przechowywane metadane na temat danych emitowanych, dzięki czemu dane można je pobrać i wysyłanego ponownie, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="f0d98-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="f0d98-254">Ponieważ danych emitowanych przez próbki jest mały, danych pierwotnych dla każdej krotki znajduje się w słowniku powtarzania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="f0d98-255">**Potwierdzenia**: każdego bolt topologii można wywołać `this.ctx.Ack(tuple)` potwierdzić, że pomyślnie przetworzył spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0d98-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="f0d98-256">Gdy wszystkie elementów bolt prześledzone spójnej kolekcji, `Ack` wywoływana jest metoda spout.</span><span class="sxs-lookup"><span data-stu-id="f0d98-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="f0d98-257">`Ack` Metoda pozwala spout do usunięcia danych, który był buforowany powtarzania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="f0d98-258">**Niepowodzenie**: każdego bolt można wywołać `this.ctx.Fail(tuple)` wskazująca, że przetwarzanie nie powiodło się dla spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0d98-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="f0d98-259">Błąd propaguje do `Fail` metody spout, gdzie można odtworzyć spójna kolekcja znajdująca się przy użyciu buforowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="f0d98-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="f0d98-260">**Identyfikator sekwencji**: podczas emitowania krotka, można określić identyfikator unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="f0d98-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="f0d98-261">Ta wartość określa spójnej kolekcji dla przetwarzania powtórzeń (Ack i błędów).</span><span class="sxs-lookup"><span data-stu-id="f0d98-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="f0d98-262">Na przykład spout w **próbki Storm** projektu są używane następujące podczas emitowania danych:</span><span class="sxs-lookup"><span data-stu-id="f0d98-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="f0d98-263">Ten kod emituje spójnych kolekcji zawierający zdania do domyślny strumień, z identyfikatorem sekwencji zawartych w **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="f0d98-264">Na przykład **lastSeqId** jest zwiększany dla każdego krotki wysyłanego.</span><span class="sxs-lookup"><span data-stu-id="f0d98-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="f0d98-265">Jak pokazano w **próbki Storm** projektu, czy składnik jest transakcyjna można ustawić w czasie wykonywania na podstawie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f0d98-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="f0d98-266">Hybrydowych topologii C# i Java</span><span class="sxs-lookup"><span data-stu-id="f0d98-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="f0d98-267">Data Lake tools dla Visual Studio umożliwia również tworzyć hybrydowe topologie, gdzie są niektóre składniki C#, a niektóre Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="f0d98-268">Na przykład topologii hybrydowego Utwórz projekt i wybierz **przykład hybrydowego Storm**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="f0d98-269">Ten typ przykładowych pokazano następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="f0d98-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="f0d98-270">**Java spout** i **C# bolt**: zdefiniowanych w **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="f0d98-271">Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="f0d98-272">**C# spout** i **Java bolt**: zdefiniowanych w **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="f0d98-273">Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f0d98-274">Ta wersja także przedstawiono sposób użycia Clojure kodu z pliku tekstowego jako składnik Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="f0d98-275">Aby przełączyć topologię, która jest używana po przesłaniu projektu, po prostu przenieść `[Active(true)]` instrukcji topologii, którego chcesz użyć, przed przesłaniem go do klastra.</span><span class="sxs-lookup"><span data-stu-id="f0d98-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d98-276">Wszystkie pliki języka Java, które są wymagane są dostarczane jako część tego projektu w **JavaDependency** folderu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="f0d98-277">Podczas tworzenia i przesyłania topologii hybrydowe, należy wziąć pod uwagę następujące:</span><span class="sxs-lookup"><span data-stu-id="f0d98-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="f0d98-278">Należy użyć **JavaComponentConstructor** można utworzyć wystąpienia klasy Java dla spout lub elementów bolt.</span><span class="sxs-lookup"><span data-stu-id="f0d98-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="f0d98-279">Należy używać **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** do serializowania danych do lub wychodzący składniki Java z obiektów języka Java na format JSON.</span><span class="sxs-lookup"><span data-stu-id="f0d98-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="f0d98-280">Podczas przesyłania topologii do serwera, należy użyć **dodatkowe konfiguracje** opcję, aby określić **ścieżki plików Java**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="f0d98-281">Określona ścieżka powinna być katalog zawierający pliki JAR, które zawierają klas Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="f0d98-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f0d98-282">Azure Event Hubs</span></span>

<span data-ttu-id="f0d98-283">Wersja SCP.NET 0.9.4.203 wprowadza nowe klasy i metody specjalnie z myślą o pracy z spout Centrum zdarzeń (Java spout, służącą do odczytywania z usługi Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="f0d98-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="f0d98-284">Podczas tworzenia topologię, która używa spout Centrum zdarzeń, należy użyć następujących metod:</span><span class="sxs-lookup"><span data-stu-id="f0d98-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="f0d98-285">**EventHubSpoutConfig** klasy: tworzy obiekt zawierający konfigurację dla składnika spout.</span><span class="sxs-lookup"><span data-stu-id="f0d98-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="f0d98-286">**TopologyBuilder.SetEventHubSpout** metody: dodaje składnik spout Centrum zdarzeń do topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d98-287">Możesz nadal korzystać **CustomizedInteropJSONSerializer** do serializowania danych produkowane przez elementy spout.</span><span class="sxs-lookup"><span data-stu-id="f0d98-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="f0d98-288"><a id="configurationmanager"></a>Użyj program Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="f0d98-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="f0d98-289">Nie używaj **ConfigurationManager** można pobrać wartości konfiguracji z bolt i spout składników.</span><span class="sxs-lookup"><span data-stu-id="f0d98-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="f0d98-290">W ten sposób może spowodować wyjątek pustego wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="f0d98-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="f0d98-291">Zamiast tego konfiguracji projektu jest przekazywany do topologii Storm jako pary kluczy i wartości w kontekście topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="f0d98-292">Każdego składnika, który korzysta z wartości konfiguracji należy pobrać je z kontekstu podczas inicjowania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="f0d98-293">Poniższy kod przedstawia sposób pobierania tych wartości:</span><span class="sxs-lookup"><span data-stu-id="f0d98-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="f0d98-294">Jeśli używasz `Get` metodę, aby zwrócić wystąpienia składnika, należy upewnić się, że przekazuje zarówno `Context` i `Dictionary<string, Object>` parametrów konstruktora.</span><span class="sxs-lookup"><span data-stu-id="f0d98-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="f0d98-295">Poniższy przykład jest podstawowy `Get` metodę, która poprawnie przekazuje te wartości:</span><span class="sxs-lookup"><span data-stu-id="f0d98-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="f0d98-296">Jak zaktualizować SCP.NET</span><span class="sxs-lookup"><span data-stu-id="f0d98-296">How to update SCP.NET</span></span>

<span data-ttu-id="f0d98-297">Najnowsze wersje SCP.NET obsługuje uaktualnienie pakietu przez pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0d98-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="f0d98-298">Dostępna jest nowa aktualizacja, pojawi się powiadomienie uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="f0d98-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="f0d98-299">Aby ręcznie sprawdzić uaktualnienia, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f0d98-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="f0d98-300">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="f0d98-301">Wybierz z Menedżera pakietów, **aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="f0d98-302">Czy jest dostępna aktualizacja, są one dostępne.</span><span class="sxs-lookup"><span data-stu-id="f0d98-302">If an update is available, it is listed.</span></span> <span data-ttu-id="f0d98-303">Kliknij przycisk **aktualizacji** dla pakietu go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="f0d98-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0d98-304">Jeśli projekt został utworzony przy użyciu starszej wersji SCP.NET, który nie używa NuGet, należy wykonać następujące kroki, aby zaktualizować do nowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="f0d98-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="f0d98-305">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="f0d98-306">Przy użyciu **wyszukiwania** pola, Wyszukaj, a następnie dodaj **Microsoft.SCP.Net.SDK** do projektu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="f0d98-307">Rozwiązywanie typowych problemów z topologii</span><span class="sxs-lookup"><span data-stu-id="f0d98-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="f0d98-308">Wyjątki wskaźnika o wartości null</span><span class="sxs-lookup"><span data-stu-id="f0d98-308">Null pointer exceptions</span></span>

<span data-ttu-id="f0d98-309">Gdy używasz topologii C# z klastrem usługi HDInsight opartej na systemie Linux, blokowania i spout składników, które używają **ConfigurationManager** można odczytać ustawień konfiguracji w czasie wykonywania mogą zwracać wyjątki wskaźnika o wartości null.</span><span class="sxs-lookup"><span data-stu-id="f0d98-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="f0d98-310">Konfiguracja dla projektu jest przekazywany do topologii Storm jako pary kluczy i wartości w kontekście topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="f0d98-311">Można go pobrać z obiekt słownika, który jest przekazywany do składników programu, gdy są one inicjowane.</span><span class="sxs-lookup"><span data-stu-id="f0d98-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="f0d98-312">Aby uzyskać więcej informacji, zobacz [ConfigurationManager](#configurationmanager) sekcji tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="f0d98-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="f0d98-313">System.TypeLoadException</span></span>

<span data-ttu-id="f0d98-314">Używając topologii C# z klastrem usługi HDInsight opartej na systemie Linux, może wystąpić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="f0d98-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="f0d98-315">Ten błąd występuje podczas używania pliku binarnego, który jest niezgodny z wersją programu .NET, który obsługuje Mono.</span><span class="sxs-lookup"><span data-stu-id="f0d98-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="f0d98-316">W przypadku klastrów usługi HDInsight opartej na systemie Linux upewnij się, że projekt korzysta z plików binarnych skompilowanego dla platformy .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="f0d98-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="f0d98-317">Testowanie topologii lokalnie</span><span class="sxs-lookup"><span data-stu-id="f0d98-317">Test a topology locally</span></span>

<span data-ttu-id="f0d98-318">Chociaż jest to łatwa do wdrożenia topologii do klastra, w niektórych przypadkach może być konieczne test topologii lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="f0d98-319">Wykonaj następujące kroki, aby uruchomić i przetestować przykładową topologię w tym samouczku lokalnie w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="f0d98-320">Testowanie lokalnym działa tylko dla basic, C# — tylko topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="f0d98-321">Nie można użyć lokalnego testowanie pod kątem hybrydowe topologie lub topologie, wykorzystujące wiele strumieni.</span><span class="sxs-lookup"><span data-stu-id="f0d98-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="f0d98-322">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="f0d98-323">We właściwościach projektu, należy zmienić **Output typu** do **aplikacji konsoli**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Zrzut ekranu przedstawiający właściwości projektu z wyróżnionym typem danych wyjściowych](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="f0d98-325">Pamiętaj, aby zmienić **Output typu** do **biblioteki klas** przed wdrożeniem topologii do klastra.</span><span class="sxs-lookup"><span data-stu-id="f0d98-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="f0d98-326">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Dodaj** > **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="f0d98-327">Wybierz **klasy**, a następnie wprowadź **LocalTest.cs** jak nazwa klasy.</span><span class="sxs-lookup"><span data-stu-id="f0d98-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="f0d98-328">Na koniec kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="f0d98-329">Otwórz **LocalTest.cs**i dodaj następującą **przy użyciu** instrukcji u góry:</span><span class="sxs-lookup"><span data-stu-id="f0d98-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="f0d98-330">Użyj następującego kodu jako zawartość **LocalTest** klasy:</span><span class="sxs-lookup"><span data-stu-id="f0d98-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="f0d98-331">Poświęć chwilę, aby zapoznaj się z artykułem komentarze w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="f0d98-332">Ten kod zawiera **LocalContext** do uruchamiania w środowisku programistycznym, a składniki będzie się powtarzał strumienia danych między składnikami w plikach tekstowych na dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f0d98-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="f0d98-333">Otwórz **Program.cs**i Dodaj następujący kod do **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="f0d98-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="f0d98-334">Zapisz zmiany, a następnie kliknij przycisk **F5** lub wybierz **debugowania** > **Rozpocznij debugowanie** do uruchamiania projektu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="f0d98-335">Okno konsoli powinna wyświetlane i rejestrowania stanu postęp testów.</span><span class="sxs-lookup"><span data-stu-id="f0d98-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="f0d98-336">Gdy **testy Zakończono** pojawia się, naciśnij dowolny klawisz, aby zamknąć okno.</span><span class="sxs-lookup"><span data-stu-id="f0d98-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="f0d98-337">Użyj **Eksploratora Windows** można zlokalizować katalogu, który zawiera projekt.</span><span class="sxs-lookup"><span data-stu-id="f0d98-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="f0d98-338">Na przykład: **C:\Users\<your_user_name > \Documents\Visual 2013\Projects\WordCount\WordCount w Studio**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="f0d98-339">W tym katalogu, otwórz **Bin**, a następnie kliknij przycisk **debugowania**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="f0d98-340">Powinny pojawić się plikami tekstowymi, które zostały utworzone podczas testów: sentences.txt, counter.txt i splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="f0d98-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="f0d98-341">Otwórz każdy plik tekstowy i sprawdzać dane.</span><span class="sxs-lookup"><span data-stu-id="f0d98-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0d98-342">Ciąg danych będzie nadal występował jako tablica wartości dziesiętnych w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="f0d98-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="f0d98-343">Na przykład \[[97,103,111]] w **splitter.txt** plik jest słowo *i*.</span><span class="sxs-lookup"><span data-stu-id="f0d98-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d98-344">Należy ustawić **typ projektu** do **biblioteki klas** przed wdrożeniem w Storm w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="f0d98-345">Informacje w Dzienniku</span><span class="sxs-lookup"><span data-stu-id="f0d98-345">Log information</span></span>

<span data-ttu-id="f0d98-346">Można łatwo rejestrowanie informacji z składniki topologii sieci, za pomocą `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="f0d98-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="f0d98-347">Na przykład następujący tworzy wpis informacyjny w dzienniku:</span><span class="sxs-lookup"><span data-stu-id="f0d98-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="f0d98-348">Zarejestrowane informacje mogą być wyświetlane z **dziennik usługi Hadoop**, który znajduje się w **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="f0d98-349">Rozwiń pozycję dla Storm w klastrze usługi HDInsight, a następnie rozwiń **dziennik usługi Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="f0d98-350">Na koniec wybierz plik dziennika, aby wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="f0d98-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d98-351">Dzienniki są przechowywane na koncie magazynu Azure, który jest używany przez klaster.</span><span class="sxs-lookup"><span data-stu-id="f0d98-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="f0d98-352">Aby wyświetlić dzienniki w programie Visual Studio, możesz zalogować się do subskrypcji platformy Azure, który jest właścicielem konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f0d98-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="f0d98-353">Wyświetl informacje o błędzie</span><span class="sxs-lookup"><span data-stu-id="f0d98-353">View error information</span></span>

<span data-ttu-id="f0d98-354">Aby wyświetlić błędy, które wystąpiły w uruchomionej topologii, użyj następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="f0d98-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="f0d98-355">Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierz **topologii Storm widoku**.</span><span class="sxs-lookup"><span data-stu-id="f0d98-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="f0d98-356">Aby uzyskać **Spout** i **Bolts**, **ostatniego błędu** kolumna zawiera informacje o ostatnim błędzie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="f0d98-357">Wybierz **Spout identyfikator** lub **identyfikator Bolt** składnika, który zawiera błąd na liście.</span><span class="sxs-lookup"><span data-stu-id="f0d98-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="f0d98-358">Na stronie Szczegóły błędu wyświetlanych, dodatkowe informacje są wymienione w **błędy** sekcji u dołu strony.</span><span class="sxs-lookup"><span data-stu-id="f0d98-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="f0d98-359">Aby uzyskać więcej informacji, wybierz **portu** z **modułów** części strony, aby wyświetlić dziennik procesu roboczego Storm ostatnich kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f0d98-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="f0d98-360">Błędy przesyłania topologii</span><span class="sxs-lookup"><span data-stu-id="f0d98-360">Errors submitting topologies</span></span>

<span data-ttu-id="f0d98-361">Jeśli wystąpią błędy przesyłania topologii do usługi HDInsight można znaleźć dzienniki dla składników po stronie serwera, które obsługi przesyłania topologii w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="f0d98-362">Aby pobrać te dzienniki, użyj następującego polecenia w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="f0d98-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="f0d98-363">Zastąp __sshuser__ przy użyciu konta użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="f0d98-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="f0d98-364">Zastąp __clustername__ z nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f0d98-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="f0d98-365">Aby uzyskać więcej informacji na temat używania `scp` i `ssh` z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0d98-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f0d98-366">Przesyłanie może zakończyć się niepowodzeniem kilka przyczyn:</span><span class="sxs-lookup"><span data-stu-id="f0d98-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="f0d98-367">JDK nie jest zainstalowany lub nie znajduje się w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="f0d98-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="f0d98-368">Wymagane zależności Java nie znajdują się w przesyłania.</span><span class="sxs-lookup"><span data-stu-id="f0d98-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="f0d98-369">Niezgodne zależności.</span><span class="sxs-lookup"><span data-stu-id="f0d98-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="f0d98-370">Zduplikowane nazwy topologii.</span><span class="sxs-lookup"><span data-stu-id="f0d98-370">Duplicate topology names.</span></span>

<span data-ttu-id="f0d98-371">Jeśli `hdinsight-scpwebapi.out` dziennik zawiera `FileNotFoundException`, może to być spowodowane przez następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="f0d98-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="f0d98-372">Zestaw JDK, który nie jest w ścieżce na środowisko deweloperskie.</span><span class="sxs-lookup"><span data-stu-id="f0d98-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="f0d98-373">Sprawdź, czy w środowisku programistycznym, który jest zainstalowany zestaw JDK `%JAVA_HOME%/bin` znajduje się w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="f0d98-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="f0d98-374">Brak zależności Java.</span><span class="sxs-lookup"><span data-stu-id="f0d98-374">You are missing a Java dependency.</span></span> <span data-ttu-id="f0d98-375">Upewnij się, że łącznie z plikami JAR wymaganych w ramach złożenia.</span><span class="sxs-lookup"><span data-stu-id="f0d98-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0d98-376">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0d98-376">Next steps</span></span>

<span data-ttu-id="f0d98-377">Na przykład przetwarzania danych z usługi Event Hubs, zobacz [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f0d98-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="f0d98-378">Na przykład topologii C#, która dzieli strumienia danych na wiele strumieni zobacz [przykład C# Storm](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="f0d98-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="f0d98-379">Aby dowiedzieć się więcej informacji o tworzeniu topologie języka C#, zobacz [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="f0d98-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="f0d98-380">Inne sposoby pracy z usługą HDInsight i więcej Storm na próbkach HDInsight można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="f0d98-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="f0d98-381">**SCP.NET firmy Microsoft**</span><span class="sxs-lookup"><span data-stu-id="f0d98-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="f0d98-382">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="f0d98-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="f0d98-383">**Apache Storm w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f0d98-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="f0d98-384">Wdrażanie i monitorowanie topologii z systemu Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="f0d98-385">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="f0d98-386">**Apache Hadoop w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f0d98-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="f0d98-387">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f0d98-388">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f0d98-389">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f0d98-390">**Bazy danych Apache HBase w usłudze HDInsight**</span><span class="sxs-lookup"><span data-stu-id="f0d98-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="f0d98-391">Wprowadzenie do korzystania z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0d98-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
