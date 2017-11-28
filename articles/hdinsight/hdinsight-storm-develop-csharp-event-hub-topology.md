---
title: "zdarzenia aaaProcess z centrów zdarzeń z systemu Storm - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess dane z usługi Azure Event Hubs w topologii Storm C# utworzone w programie Visual Studio przy użyciu hello narzędzi HDInsight tools dla programu Visual Studio."
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
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="802a3-103">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="802a3-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="802a3-104">Dowiedz się, jak toowork z usługą Azure Event Hubs z systemu Apache Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802a3-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="802a3-105">Ten dokument używa C# Storm topologii tooread i zapisu danych z centrów Evbent</span><span class="sxs-lookup"><span data-stu-id="802a3-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="802a3-106">Wersja języka Java tego projektu, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="802a3-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="802a3-107">SCP.NET</span></span>

<span data-ttu-id="802a3-108">kroki Hello w tym dokumencie Użyj SCP.NET, pakietu NuGet, który ułatwia topologie łatwe toocreate C# i składniki do użycia z systemu Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802a3-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="802a3-109">Gdy hello kroków w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, hello skompilowany projekt może być przesłane tooa Storm w klastrze usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="802a3-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="802a3-110">Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.</span><span class="sxs-lookup"><span data-stu-id="802a3-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="802a3-111">HDInsight 3.4 i większa topologie Mono toorun C# Użyj.</span><span class="sxs-lookup"><span data-stu-id="802a3-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="802a3-112">przykład Witaj używane w tym dokumencie współpracuje z 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802a3-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="802a3-113">Jeśli planujesz tworzenie własnych rozwiązań .NET dla usługi HDInsight, sprawdź hello [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.</span><span class="sxs-lookup"><span data-stu-id="802a3-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="802a3-114">Przechowywanie wersji klastra</span><span class="sxs-lookup"><span data-stu-id="802a3-114">Cluster versioning</span></span>

<span data-ttu-id="802a3-115">Witaj używanego dla projektu pakietu Microsoft.SCP.Net.SDK NuGet musi odpowiadać wersji głównych hello Storm zainstalowany w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="802a3-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="802a3-116">HDInsight w wersji 3.5 i 3,6 używać systemu Storm 1.x, dlatego należy użyć 1.0.x.x wersji SCP.NET z tych klastrach.</span><span class="sxs-lookup"><span data-stu-id="802a3-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="802a3-117">przykład Witaj w tym dokumencie oczekuje HDInsight w wersji 3.5 lub 3,6 klastra.</span><span class="sxs-lookup"><span data-stu-id="802a3-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="802a3-118">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="802a3-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="802a3-119">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="802a3-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="802a3-120">Topologie języka C# muszą również wskazywać .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="802a3-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="802a3-121">Jak toowork z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="802a3-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="802a3-122">Firma Microsoft udostępnia zestaw składników Java, które mogą być używane toocommunicate z usługą Event Hubs od topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="802a3-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="802a3-123">Można znaleźć pliku archiwum (JAR) Java hello, który zawiera 3,6 HDInsight zgodna wersja tych składników na [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="802a3-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="802a3-124">Gdy składniki hello są napisane w języku Java, łatwo można je od topologii C#.</span><span class="sxs-lookup"><span data-stu-id="802a3-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="802a3-125">następujące składniki Hello są używane w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="802a3-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="802a3-126">__EventHubSpout__: odczytuje dane z usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="802a3-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="802a3-127">__EventHubBolt__: zapisuje dane tooEvent koncentratorów.</span><span class="sxs-lookup"><span data-stu-id="802a3-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="802a3-128">__EventHubSpoutConfig__: tooconfigure EventHubSpout używane.</span><span class="sxs-lookup"><span data-stu-id="802a3-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="802a3-129">__EventHubBoltConfig__: tooconfigure EventHubBolt używane.</span><span class="sxs-lookup"><span data-stu-id="802a3-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="802a3-130">Przykład użycia spout</span><span class="sxs-lookup"><span data-stu-id="802a3-130">Example spout usage</span></span>

<span data-ttu-id="802a3-131">SCP.NET udostępnia metody do dodawania EventHubSpout tooyour topologii.</span><span class="sxs-lookup"><span data-stu-id="802a3-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="802a3-132">Te metody umożliwiają łatwiejsze tooadd spout niż przy użyciu metody rodzajowe hello do dodawania składnika Java.</span><span class="sxs-lookup"><span data-stu-id="802a3-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="802a3-133">Witaj poniższym przykładzie pokazano, jak hello toocreate spout za pomocą __SetEventHubSpout__ i **EventHubSpoutConfig** metody udostępniane przez SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="802a3-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="802a3-134">Witaj w poprzednim przykładzie tworzy nowy składnik spout o nazwie __EventHubSpout__i skonfiguruje je toocommunicate z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="802a3-135">Wskazówka równoległości Hello składnika hello jest ustawiana toohello liczby partycji w Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="802a3-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="802a3-136">To ustawienie umożliwia Storm toocreate wystąpienia składnika powitania dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="802a3-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="802a3-137">Przykład użycia bolt</span><span class="sxs-lookup"><span data-stu-id="802a3-137">Example bolt usage</span></span>

<span data-ttu-id="802a3-138">Użyj hello **JavaComponmentConstructor** toocreate metody wystąpienia hello bolt.</span><span class="sxs-lookup"><span data-stu-id="802a3-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="802a3-139">Witaj poniższym przykładzie pokazano, jak toocreate i skonfiguruj nowe wystąpienie klasy hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="802a3-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="802a3-140">W tym przykładzie użyto wyrażenia Clojure przekazany jako ciąg, zamiast **JavaComponentConstructor** toocreate **EventHubBoltConfig**, tak jak na przykład Witaj spout.</span><span class="sxs-lookup"><span data-stu-id="802a3-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="802a3-141">Każda metoda działa.</span><span class="sxs-lookup"><span data-stu-id="802a3-141">Either method works.</span></span> <span data-ttu-id="802a3-142">Użyj metody hello tak najlepsze tooyou.</span><span class="sxs-lookup"><span data-stu-id="802a3-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="802a3-143">Pobierz ukończyć powitalnych projektu</span><span class="sxs-lookup"><span data-stu-id="802a3-143">Download hello completed project</span></span>

<span data-ttu-id="802a3-144">Możesz pobrać pełną wersję utworzonego w ramach tego samouczka z projektu hello [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="802a3-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="802a3-145">Jednak nadal potrzebujesz tooprovide ustawienia konfiguracji, wykonując kroki hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="802a3-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="802a3-146">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="802a3-146">Prerequisites</span></span>

* <span data-ttu-id="802a3-147">[Systemu Apache Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="802a3-148">przykład Witaj używane w tym dokumencie wymaga Storm w usłudze HDInsight w wersji 3.5 lub 3,6.</span><span class="sxs-lookup"><span data-stu-id="802a3-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="802a3-149">Nie działa ze starszymi wersjami usługi hdinsight, zmiany nazwy klasy toobreaking ukończenia.</span><span class="sxs-lookup"><span data-stu-id="802a3-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="802a3-150">Wersja tego przykładu, która współdziała z klastrami starsze, dla [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="802a3-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="802a3-151">[Centrum zdarzeń Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="802a3-152">Witaj [zestawu Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="802a3-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="802a3-153">Witaj [narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="802a3-154">Java JDK 1.8 lub nowszego środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="802a3-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="802a3-155">Pobieranie JDK są dostępne z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="802a3-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="802a3-156">Witaj **JAVA_HOME** środowiska zmiennej musi toohello punktu katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="802a3-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="802a3-157">Witaj **%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="802a3-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="802a3-158">Pobierz hello składniki usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="802a3-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="802a3-159">Hello pobierania centrów zdarzeń spout i zablokowanie składnika z [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="802a3-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="802a3-160">Utwórz katalog o nazwie `eventhubspout`i Zapisz plik hello do katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="802a3-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="802a3-161">Konfigurowanie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="802a3-161">Configure Event Hubs</span></span>

<span data-ttu-id="802a3-162">Centra zdarzeń to hello źródła danych w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="802a3-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="802a3-163">Użyj informacji hello w sekcji "Tworzenie Centrum zdarzeń" hello z [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="802a3-164">Po utworzeniu Centrum zdarzeń hello wyświetlić hello **EventHub** bloku w hello Azure portalu i wybierz pozycję **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="802a3-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="802a3-165">Wybierz **+ Dodaj** hello tooadd następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="802a3-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="802a3-166">Nazwa</span><span class="sxs-lookup"><span data-stu-id="802a3-166">Name</span></span> | <span data-ttu-id="802a3-167">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="802a3-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="802a3-168">Składnik zapisywania</span><span class="sxs-lookup"><span data-stu-id="802a3-168">writer</span></span> |<span data-ttu-id="802a3-169">Send</span><span class="sxs-lookup"><span data-stu-id="802a3-169">Send</span></span> |
   | <span data-ttu-id="802a3-170">Czytnik</span><span class="sxs-lookup"><span data-stu-id="802a3-170">reader</span></span> |<span data-ttu-id="802a3-171">Nasłuchiwanie</span><span class="sxs-lookup"><span data-stu-id="802a3-171">Listen</span></span> |

    ![Zrzut ekranu udziału dostępu zasady okna](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="802a3-173">Wybierz hello **czytnika** i **zapisywania** zasad.</span><span class="sxs-lookup"><span data-stu-id="802a3-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="802a3-174">Skopiuj i Zapisz hello wartość klucza podstawowego dla obu zasad, jak te wartości są używane później.</span><span class="sxs-lookup"><span data-stu-id="802a3-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="802a3-175">Skonfiguruj hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="802a3-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="802a3-176">Jeśli hello najnowszą wersję narzędzi HDInsight hello nie jest już zainstalowany dla programu Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="802a3-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="802a3-177">Pobierz hello rozwiązania z [eventhub storm hybrydowy](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="802a3-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="802a3-178">W hello **EventHubWriter** projektu, otwórz hello **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="802a3-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="802a3-179">Użyj informacji hello z Centrum zdarzeń hello skonfigurowane wcześniej toofill hello wartości hello następujące klucze:</span><span class="sxs-lookup"><span data-stu-id="802a3-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="802a3-180">Klucz</span><span class="sxs-lookup"><span data-stu-id="802a3-180">Key</span></span> | <span data-ttu-id="802a3-181">Wartość</span><span class="sxs-lookup"><span data-stu-id="802a3-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="802a3-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="802a3-182">EventHubPolicyName</span></span> |<span data-ttu-id="802a3-183">Moduł zapisujący (jeśli użyto inną nazwę dla zasad hello o *wysyłania* uprawnień, zamiast tego użyj.)</span><span class="sxs-lookup"><span data-stu-id="802a3-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="802a3-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="802a3-184">EventHubPolicyKey</span></span> |<span data-ttu-id="802a3-185">klucz Hello hello zapisywania zasad.</span><span class="sxs-lookup"><span data-stu-id="802a3-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="802a3-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="802a3-186">EventHubNamespace</span></span> |<span data-ttu-id="802a3-187">Witaj przestrzeni nazw, która zawiera Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="802a3-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="802a3-188">EventHubName</span></span> |<span data-ttu-id="802a3-189">Nazwę Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-189">Your event hub name.</span></span> |
   | <span data-ttu-id="802a3-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="802a3-190">EventHubPartitionCount</span></span> |<span data-ttu-id="802a3-191">Witaj liczbę partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="802a3-192">Zapisz i zamknij hello **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="802a3-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="802a3-193">Skonfiguruj hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="802a3-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="802a3-194">Otwórz hello **EventHubReader** projektu.</span><span class="sxs-lookup"><span data-stu-id="802a3-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="802a3-195">Otwórz hello **App.config** pliku hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="802a3-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="802a3-196">Użyj informacji hello z Centrum zdarzeń hello skonfigurowane wcześniej toofill hello wartości hello następujące klucze:</span><span class="sxs-lookup"><span data-stu-id="802a3-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="802a3-197">Klucz</span><span class="sxs-lookup"><span data-stu-id="802a3-197">Key</span></span> | <span data-ttu-id="802a3-198">Wartość</span><span class="sxs-lookup"><span data-stu-id="802a3-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="802a3-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="802a3-199">EventHubPolicyName</span></span> |<span data-ttu-id="802a3-200">Czytnik (Jeśli używasz inną nazwę dla zasad hello o *nasłuchiwania* uprawnień, zamiast tego użyj.)</span><span class="sxs-lookup"><span data-stu-id="802a3-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="802a3-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="802a3-201">EventHubPolicyKey</span></span> |<span data-ttu-id="802a3-202">klucz Hello hello czytnika zasad.</span><span class="sxs-lookup"><span data-stu-id="802a3-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="802a3-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="802a3-203">EventHubNamespace</span></span> |<span data-ttu-id="802a3-204">Witaj przestrzeni nazw, która zawiera Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="802a3-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="802a3-205">EventHubName</span></span> |<span data-ttu-id="802a3-206">Nazwę Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-206">Your event hub name.</span></span> |
   | <span data-ttu-id="802a3-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="802a3-207">EventHubPartitionCount</span></span> |<span data-ttu-id="802a3-208">Witaj liczbę partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="802a3-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="802a3-209">Zapisz i zamknij hello **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="802a3-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="802a3-210">Wdrażanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="802a3-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="802a3-211">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **EventHubReader** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="802a3-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Zrzut ekranu z Eksplorator rozwiązań z tooStorm przesyłania w usłudze HDInsight wyróżnione](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="802a3-213">Na powitania **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**.</span><span class="sxs-lookup"><span data-stu-id="802a3-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="802a3-214">Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** i hello wybierz katalog, który zawiera plik JAR hello pobranego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="802a3-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="802a3-215">Na koniec kliknij **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="802a3-215">Finally, click **Submit**.</span></span>

    ![Zrzut ekranu przedstawia topologię — okno dialogowe](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="802a3-217">Po przesłaniu topologii hello hello **podglądu topologii Storm** pojawi się.</span><span class="sxs-lookup"><span data-stu-id="802a3-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="802a3-218">tooview informacji o topologii hello, wybierz hello **EventHubReader** topologię. w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="802a3-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Zrzut ekranu przedstawiający podgląd topologie Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="802a3-220">Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **EventHubWriter** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="802a3-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="802a3-221">Na powitania **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**.</span><span class="sxs-lookup"><span data-stu-id="802a3-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="802a3-222">Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** , i hello wybierz katalog, który zawiera plik JAR hello pobranego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="802a3-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="802a3-223">Na koniec kliknij **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="802a3-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="802a3-224">Po przesłaniu hello topologii, Odśwież listę topologii hello w hello **podglądu topologii Storm** tooverify obu topologiach uruchomionych w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="802a3-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="802a3-225">W **podglądu topologii Storm**, wybierz pozycję hello **EventHubReader** topologii.</span><span class="sxs-lookup"><span data-stu-id="802a3-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="802a3-226">Podsumowanie hello bolt składnika hello tooopen kliknij dwukrotnie hello **LogBolt** składnika hello diagramie.</span><span class="sxs-lookup"><span data-stu-id="802a3-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="802a3-227">W hello **modułów** sekcji, wybierz jeden z linków hello hello **portu** kolumny.</span><span class="sxs-lookup"><span data-stu-id="802a3-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="802a3-228">Spowoduje to wyświetlenie informacji zarejestrowanych przez składnik hello.</span><span class="sxs-lookup"><span data-stu-id="802a3-228">This displays information logged by hello component.</span></span> <span data-ttu-id="802a3-229">informacje o Hello rejestrowane są podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="802a3-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="802a3-230">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="802a3-230">Stop hello topologies</span></span>

<span data-ttu-id="802a3-231">topologie hello toostop, wybierz każdej topologii w hello **podglądu topologii Storm**, następnie kliknij przycisk **Kill**.</span><span class="sxs-lookup"><span data-stu-id="802a3-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Zrzut ekranu z Storm topologii podglądu, z wyróżnionym przyciskiem Kill](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="802a3-233">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="802a3-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="802a3-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="802a3-234">Next steps</span></span>

<span data-ttu-id="802a3-235">W tym dokumencie uzyskanych jak toouse hello Java centra zdarzeń spout i zablokowanie z toowork topologii C#, w danych w usłudze Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="802a3-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="802a3-236">toolearn więcej informacji na temat tworzenia topologie języka C#, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="802a3-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="802a3-237">Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="802a3-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="802a3-238">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="802a3-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="802a3-239">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="802a3-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
