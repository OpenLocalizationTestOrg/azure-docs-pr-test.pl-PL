---
title: "Przetwarzać zdarzeń z usługi Event Hubs dzięki platformie Storm - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie przetwarzania danych z usługi Azure Event Hubs w topologii Storm C#, utworzony w programie Visual Studio za pomocą narzędzi HDInsight tools for Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="1ede4-103">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="1ede4-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="1ede4-104">Dowiedz się, jak pracować z usługą Azure Event Hubs z systemu Apache Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ede4-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="1ede4-105">Ten dokument używa topologii Storm C# do odczytywania i zapisywania danych z centrów Evbent</span><span class="sxs-lookup"><span data-stu-id="1ede4-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="1ede4-106">Wersja języka Java tego projektu, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="1ede4-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="1ede4-107">SCP.NET</span></span>

<span data-ttu-id="1ede4-108">Kroki opisane w tym dokumencie Użyj SCP.NET, pakietu NuGet, który ułatwia tworzenie topologii C# i składniki do użycia z systemu Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ede4-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ede4-109">Podczas czynności opisane w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, skompilowany projekt może zostać przesłane do systemu Storm w klastrze usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="1ede4-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1ede4-110">Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.</span><span class="sxs-lookup"><span data-stu-id="1ede4-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="1ede4-111">HDInsight 3.4 i większe wykorzystanie Mono uruchamiania topologie języka C#.</span><span class="sxs-lookup"><span data-stu-id="1ede4-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="1ede4-112">Przykład używane w tym dokumencie współpracuje z 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ede4-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="1ede4-113">Jeśli planujesz tworzenie własnych rozwiązań .NET dla usługi HDInsight, sprawdź [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="1ede4-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="1ede4-114">Przechowywanie wersji klastra</span><span class="sxs-lookup"><span data-stu-id="1ede4-114">Cluster versioning</span></span>

<span data-ttu-id="1ede4-115">Pakiet Microsoft.SCP.Net.SDK NuGet używanych w przypadku projektu musi być zgodna wersja główna systemu STORM zainstalowany w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ede4-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="1ede4-116">HDInsight w wersji 3.5 i 3,6 używać systemu Storm 1.x, dlatego należy użyć 1.0.x.x wersji SCP.NET z tych klastrach.</span><span class="sxs-lookup"><span data-stu-id="1ede4-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ede4-117">Przykład, w tym dokumencie oczekuje HDInsight w wersji 3.5 lub 3,6 klastra.</span><span class="sxs-lookup"><span data-stu-id="1ede4-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="1ede4-118">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="1ede4-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1ede4-119">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="1ede4-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="1ede4-120">Topologie języka C# muszą również wskazywać .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="1ede4-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="1ede4-121">Jak pracować z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1ede4-121">How to work with Event Hubs</span></span>

<span data-ttu-id="1ede4-122">Firma Microsoft udostępnia zestaw składników Java, które mogą służyć do komunikacji z usługą Event Hubs od topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="1ede4-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="1ede4-123">Można znaleźć pliku archiwum (JAR) Java, który zawiera 3,6 HDInsight zgodna wersja tych składników na [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="1ede4-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ede4-124">Gdy składniki są napisane w języku Java, łatwo można je od topologii C#.</span><span class="sxs-lookup"><span data-stu-id="1ede4-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="1ede4-125">Następujące składniki są używane w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1ede4-125">The following components are used in this example:</span></span>

* <span data-ttu-id="1ede4-126">__EventHubSpout__: odczytuje dane z usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1ede4-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="1ede4-127">__EventHubBolt__: zapisuje dane do usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1ede4-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="1ede4-128">__EventHubSpoutConfig__: umożliwia skonfigurowanie EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="1ede4-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="1ede4-129">__EventHubBoltConfig__: umożliwia skonfigurowanie EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="1ede4-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="1ede4-130">Przykład użycia spout</span><span class="sxs-lookup"><span data-stu-id="1ede4-130">Example spout usage</span></span>

<span data-ttu-id="1ede4-131">SCP.NET udostępnia metody do dodawania EventHubSpout do topologii.</span><span class="sxs-lookup"><span data-stu-id="1ede4-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="1ede4-132">Tych metod można ułatwić dodawanie spout niż przy użyciu metody ogólne do dodawania składnika Java.</span><span class="sxs-lookup"><span data-stu-id="1ede4-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="1ede4-133">W poniższym przykładzie pokazano, jak utworzyć elementy spout przy użyciu __SetEventHubSpout__ i **EventHubSpoutConfig** metody udostępniane przez SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="1ede4-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="1ede4-134">Poprzedni przykład tworzy nowy składnik spout o nazwie __EventHubSpout__i skonfiguruje je do komunikowania się z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="1ede4-135">Wskazówka równoległości dla składnika ma ustawioną wartość liczby partycji w zdarzeniu koncentratora.</span><span class="sxs-lookup"><span data-stu-id="1ede4-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="1ede4-136">To ustawienie umożliwia Storm do utworzenia wystąpienia składnika dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="1ede4-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="1ede4-137">Przykład użycia bolt</span><span class="sxs-lookup"><span data-stu-id="1ede4-137">Example bolt usage</span></span>

<span data-ttu-id="1ede4-138">Użyj **JavaComponmentConstructor** metodę w celu utworzenia wystąpienia elementy bolt.</span><span class="sxs-lookup"><span data-stu-id="1ede4-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="1ede4-139">W poniższym przykładzie pokazano, jak utworzyć i skonfigurować nowe wystąpienie klasy **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="1ede4-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="1ede4-140">W tym przykładzie użyto wyrażenia Clojure przekazany jako ciąg, zamiast **JavaComponentConstructor** utworzyć **EventHubBoltConfig**, tak jak w przykładzie elementy spout.</span><span class="sxs-lookup"><span data-stu-id="1ede4-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="1ede4-141">Każda metoda działa.</span><span class="sxs-lookup"><span data-stu-id="1ede4-141">Either method works.</span></span> <span data-ttu-id="1ede4-142">Użyj metody tak najważniejsze dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="1ede4-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="1ede4-143">Pobieranie ukończone projektu</span><span class="sxs-lookup"><span data-stu-id="1ede4-143">Download the completed project</span></span>

<span data-ttu-id="1ede4-144">Możesz pobrać pełną wersję utworzonego w ramach tego samouczka z projektu [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="1ede4-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="1ede4-145">Jednakże nadal musisz podać ustawienia konfiguracji, wykonując kroki opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1ede4-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1ede4-146">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ede4-146">Prerequisites</span></span>

* <span data-ttu-id="1ede4-147">[Systemu Apache Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="1ede4-148">Przykład używane w tym dokumencie wymaga Storm w usłudze HDInsight w wersji 3.5 lub 3,6.</span><span class="sxs-lookup"><span data-stu-id="1ede4-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="1ede4-149">To nie zadziała ze starszymi wersjami usługi hdinsight, ze względu na istotne zmiany nazwy klasy.</span><span class="sxs-lookup"><span data-stu-id="1ede4-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="1ede4-150">Wersja tego przykładu, która współdziała z klastrami starsze, dla [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="1ede4-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="1ede4-151">[Centrum zdarzeń Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="1ede4-152">[Zestawu Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1ede4-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="1ede4-153">[Narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="1ede4-154">Java JDK 1.8 lub nowszego środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="1ede4-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="1ede4-155">Pobieranie JDK są dostępne z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="1ede4-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="1ede4-156">**JAVA_HOME** zmiennej środowiskowej musi wskazywać katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="1ede4-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="1ede4-157">**%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="1ede4-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="1ede4-158">Pobierz składniki usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1ede4-158">Download the Event Hubs components</span></span>

<span data-ttu-id="1ede4-159">Pobierz elementy spout centra zdarzeń i elementów bolt składnika z [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="1ede4-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="1ede4-160">Utwórz katalog o nazwie `eventhubspout`i Zapisz plik do katalogu.</span><span class="sxs-lookup"><span data-stu-id="1ede4-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="1ede4-161">Konfigurowanie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1ede4-161">Configure Event Hubs</span></span>

<span data-ttu-id="1ede4-162">Centra zdarzeń to źródło danych, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1ede4-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="1ede4-163">Skorzystaj z informacji w sekcji "Tworzenie Centrum zdarzeń" [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="1ede4-164">Po utworzeniu Centrum zdarzeń wyświetlić **EventHub** bloku na platformie Azure, portalu i wybierz pozycję **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="1ede4-165">Wybierz **+ Dodaj** można dodać następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="1ede4-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="1ede4-166">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1ede4-166">Name</span></span> | <span data-ttu-id="1ede4-167">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="1ede4-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="1ede4-168">Składnik zapisywania</span><span class="sxs-lookup"><span data-stu-id="1ede4-168">writer</span></span> |<span data-ttu-id="1ede4-169">Send</span><span class="sxs-lookup"><span data-stu-id="1ede4-169">Send</span></span> |
   | <span data-ttu-id="1ede4-170">Czytnik</span><span class="sxs-lookup"><span data-stu-id="1ede4-170">reader</span></span> |<span data-ttu-id="1ede4-171">Nasłuchiwanie</span><span class="sxs-lookup"><span data-stu-id="1ede4-171">Listen</span></span> |

    ![Zrzut ekranu udziału dostępu zasady okna](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="1ede4-173">Wybierz **czytnika** i **zapisywania** zasad.</span><span class="sxs-lookup"><span data-stu-id="1ede4-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="1ede4-174">Skopiuj i Zapisz wartość klucza podstawowego dla obu zasad, jak te wartości są używane później.</span><span class="sxs-lookup"><span data-stu-id="1ede4-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="1ede4-175">Skonfiguruj EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="1ede4-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="1ede4-176">Jeśli nie został jeszcze zainstalowany najnowszej wersji narzędzia HDInsight tools for Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ede4-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="1ede4-177">Pobierz rozwiązania z [eventhub storm hybrydowy](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="1ede4-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="1ede4-178">W **EventHubWriter** otwarciu projektu **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="1ede4-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="1ede4-179">Użyj informacji z Centrum zdarzeń, który został wcześniej skonfigurowany, aby wypełnić wartości następujących kluczy:</span><span class="sxs-lookup"><span data-stu-id="1ede4-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="1ede4-180">Klucz</span><span class="sxs-lookup"><span data-stu-id="1ede4-180">Key</span></span> | <span data-ttu-id="1ede4-181">Wartość</span><span class="sxs-lookup"><span data-stu-id="1ede4-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="1ede4-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="1ede4-182">EventHubPolicyName</span></span> |<span data-ttu-id="1ede4-183">Moduł zapisujący (jeśli użyto inną nazwę dla zasad o *wysyłania* uprawnień, zamiast tego użyj.)</span><span class="sxs-lookup"><span data-stu-id="1ede4-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="1ede4-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="1ede4-184">EventHubPolicyKey</span></span> |<span data-ttu-id="1ede4-185">Klucz dla modułu zapisującego zasad.</span><span class="sxs-lookup"><span data-stu-id="1ede4-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="1ede4-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="1ede4-186">EventHubNamespace</span></span> |<span data-ttu-id="1ede4-187">Przestrzeń nazw zawiera Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="1ede4-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="1ede4-188">EventHubName</span></span> |<span data-ttu-id="1ede4-189">Nazwę Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-189">Your event hub name.</span></span> |
   | <span data-ttu-id="1ede4-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="1ede4-190">EventHubPartitionCount</span></span> |<span data-ttu-id="1ede4-191">Liczba partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="1ede4-192">Zapisz i Zamknij **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="1ede4-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="1ede4-193">Skonfiguruj EventHubReader</span><span class="sxs-lookup"><span data-stu-id="1ede4-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="1ede4-194">Otwórz **EventHubReader** projektu.</span><span class="sxs-lookup"><span data-stu-id="1ede4-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="1ede4-195">Otwórz **App.config** plik **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="1ede4-196">Użyj informacji z Centrum zdarzeń, który został wcześniej skonfigurowany, aby wypełnić wartości następujących kluczy:</span><span class="sxs-lookup"><span data-stu-id="1ede4-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="1ede4-197">Klucz</span><span class="sxs-lookup"><span data-stu-id="1ede4-197">Key</span></span> | <span data-ttu-id="1ede4-198">Wartość</span><span class="sxs-lookup"><span data-stu-id="1ede4-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="1ede4-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="1ede4-199">EventHubPolicyName</span></span> |<span data-ttu-id="1ede4-200">Czytnik (Jeśli używasz inną nazwę dla zasad o *nasłuchiwania* uprawnień, zamiast tego użyj.)</span><span class="sxs-lookup"><span data-stu-id="1ede4-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="1ede4-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="1ede4-201">EventHubPolicyKey</span></span> |<span data-ttu-id="1ede4-202">Klucz dla zasad czytnika.</span><span class="sxs-lookup"><span data-stu-id="1ede4-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="1ede4-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="1ede4-203">EventHubNamespace</span></span> |<span data-ttu-id="1ede4-204">Przestrzeń nazw zawiera Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="1ede4-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="1ede4-205">EventHubName</span></span> |<span data-ttu-id="1ede4-206">Nazwę Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-206">Your event hub name.</span></span> |
   | <span data-ttu-id="1ede4-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="1ede4-207">EventHubPartitionCount</span></span> |<span data-ttu-id="1ede4-208">Liczba partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1ede4-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="1ede4-209">Zapisz i Zamknij **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="1ede4-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="1ede4-210">Topologie wdrażania</span><span class="sxs-lookup"><span data-stu-id="1ede4-210">Deploy the topologies</span></span>

1. <span data-ttu-id="1ede4-211">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **EventHubReader** projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Zrzut ekranu z Eksplorator rozwiązań z przesyłania do systemu Storm w usłudze HDInsight wyróżnione](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="1ede4-213">Na **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="1ede4-214">Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** i wybierz katalog, który zawiera plik JAR pobranego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1ede4-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="1ede4-215">Na koniec kliknij **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-215">Finally, click **Submit**.</span></span>

    ![Zrzut ekranu przedstawia topologię — okno dialogowe](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="1ede4-217">Po przesłaniu topologii **podglądu topologii Storm** pojawi się.</span><span class="sxs-lookup"><span data-stu-id="1ede4-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="1ede4-218">Zaznacz, aby wyświetlić informacje o topologii **EventHubReader** topologię. w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1ede4-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Zrzut ekranu przedstawiający podgląd topologie Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="1ede4-220">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **EventHubWriter** projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="1ede4-221">Na **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="1ede4-222">Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** i wybierz katalog, który zawiera plik JAR pobranego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1ede4-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="1ede4-223">Na koniec kliknij **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="1ede4-224">Po przesłaniu topologii, Odśwież listę topologii w **podglądu topologii Storm** Aby sprawdzić, czy obu topologiach są uruchomione w klastrze.</span><span class="sxs-lookup"><span data-stu-id="1ede4-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="1ede4-225">W **podglądu topologii Storm**, wybierz pozycję **EventHubReader** topologii.</span><span class="sxs-lookup"><span data-stu-id="1ede4-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="1ede4-226">Aby otworzyć składnik podsumowania dla elementy bolt, kliknij dwukrotnie **LogBolt** składnika na diagramie.</span><span class="sxs-lookup"><span data-stu-id="1ede4-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="1ede4-227">W **modułów** wybierz jeden z linków w **portu** kolumny.</span><span class="sxs-lookup"><span data-stu-id="1ede4-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="1ede4-228">Spowoduje to wyświetlenie informacji zarejestrowanych przez składnik.</span><span class="sxs-lookup"><span data-stu-id="1ede4-228">This displays information logged by the component.</span></span> <span data-ttu-id="1ede4-229">Zarejestrowane informacje jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="1ede4-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="1ede4-230">Zatrzymywanie topologii</span><span class="sxs-lookup"><span data-stu-id="1ede4-230">Stop the topologies</span></span>

<span data-ttu-id="1ede4-231">Aby zatrzymać topologie, wybierz każdej topologii w **podglądu topologii Storm**, następnie kliknij przycisk **Kill**.</span><span class="sxs-lookup"><span data-stu-id="1ede4-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Zrzut ekranu z Storm topologii podglądu, z wyróżnionym przyciskiem Kill](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="1ede4-233">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="1ede4-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="1ede4-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ede4-234">Next steps</span></span>

<span data-ttu-id="1ede4-235">W tym dokumencie zapoznaniu spout centra zdarzeń w języku Java i zablokowanie od topologii C# do pracy z danymi w usłudze Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1ede4-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="1ede4-236">Aby dowiedzieć się więcej o tworzeniu topologie języka C#, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="1ede4-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="1ede4-237">Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ede4-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="1ede4-238">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="1ede4-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="1ede4-239">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1ede4-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
