---
title: "Korelowanie zdarzeń w czasie z Storm oraz bazy danych HBase w usłudze HDInsight"
description: "Dowiedz się, jak skorelować zdarzenia pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="df752-103">Korelowanie zdarzeń pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="df752-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="df752-104">Przy użyciu magazynu danych z systemu Apache Storm, może skorelować danych wpisów, pojawiające się w różnych godzinach.</span><span class="sxs-lookup"><span data-stu-id="df752-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="df752-105">Na przykład łączenie zdarzeń logowania i wylogowywania sesji użytkownika do obliczenia, jak długo trwającej sesji.</span><span class="sxs-lookup"><span data-stu-id="df752-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="df752-106">W tym dokumencie Dowiedz się jak utworzyć podstawowy topologii Storm C#, który śledzi zdarzenia logowania i wylogowywania sesji użytkownika, a czas trwania sesji.</span><span class="sxs-lookup"><span data-stu-id="df752-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="df752-107">Topologia używa bazy danych HBase jako magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="df752-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="df752-108">HBase można też wykonać partii zapytania na danych historycznych, aby wygenerować dodatkowe informacje szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="df752-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="df752-109">Na przykład jak wiele sesji użytkownika zostały rozpoczął się lub zakończył się w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="df752-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df752-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="df752-110">Prerequisites</span></span>

* <span data-ttu-id="df752-111">Visual Studio i narzędzi HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df752-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="df752-112">Aby uzyskać więcej informacji, zobacz [rozpocząć korzystanie z narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="df752-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="df752-113">Apache Storm w usłudze HDInsight klastra (z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="df752-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="df752-114">Topologie SCP.NET są obsługiwane w klastrach opartych na systemie Linux Storm utworzone po 10/28/2016, HBase zestawu SDK pakietu .NET jest dostępny od 10/28/2016 nie działa poprawnie na HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="df752-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="df752-115">Bazy danych Apache HBase w klastrze usługi HDInsight (Linux lub z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="df752-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="df752-116">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="df752-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="df752-117">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="df752-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="df752-118">[Java](https://java.com) 1.7 lub nowszej na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="df752-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="df752-119">Java służy do pakietu topologii po przesłaniu do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df752-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="df752-120">**JAVA_HOME** zmiennej środowiskowej musi wskazywać katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="df752-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="df752-121">**%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce</span><span class="sxs-lookup"><span data-stu-id="df752-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="df752-122">Architektura</span><span class="sxs-lookup"><span data-stu-id="df752-122">Architecture</span></span>

![Diagram przepływu danych za pośrednictwem topologii](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="df752-124">Korelowanie zdarzeń wymaga identyfikator wspólnej dla źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df752-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="df752-125">For example identyfikator użytkownika, identyfikator sesji lub inny element danych) unikatowy i (b) uwzględnionych w wszystkich danych przesyłanych do systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="df752-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="df752-126">W tym przykładzie używane wartości identyfikatora GUID do reprezentowania identyfikator sesji.</span><span class="sxs-lookup"><span data-stu-id="df752-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="df752-127">W tym przykładzie składa się z dwóch klastrów usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="df752-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="df752-128">HBase: dane historyczne w magazynie danych trwałych</span><span class="sxs-lookup"><span data-stu-id="df752-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="df752-129">STORM: używany do pozyskiwania przychodzących danych.</span><span class="sxs-lookup"><span data-stu-id="df752-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="df752-130">Dane losowo generowany przez topologii Storm i składa się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="df752-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="df752-131">Identyfikator sesji: identyfikator GUID, który unikatowo identyfikuje każdej sesji</span><span class="sxs-lookup"><span data-stu-id="df752-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="df752-132">Zdarzenie: POCZĄTKOWY lub końcowy zdarzeniem.</span><span class="sxs-lookup"><span data-stu-id="df752-132">Event: a START or END event.</span></span> <span data-ttu-id="df752-133">Na przykład, START zawsze występuje przed zakończeniem</span><span class="sxs-lookup"><span data-stu-id="df752-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="df752-134">Czas: czas zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df752-134">Time: the time of the event.</span></span>

<span data-ttu-id="df752-135">Te dane są przetwarzane i przechowywane w bazie danych HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="df752-136">Topologii STORM</span><span class="sxs-lookup"><span data-stu-id="df752-136">Storm topology</span></span>

<span data-ttu-id="df752-137">Po uruchomieniu sesji **START** zdarzeń jest odbierany przez topologii i logowania do bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="df752-138">Gdy **zakończenia** odebraniu zdarzenia, pobiera topologię **START** zdarzeń i oblicza czasu między dwoma zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="df752-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="df752-139">To **czas trwania** wartość następnie jest przechowywana w bazie danych HBase, wraz z **zakończenia** informacji o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="df752-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df752-140">Gdy ta topologia przedstawia podstawowy wzorzec, rozwiązanie produkcji musi podjąć projektu w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="df752-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="df752-141">Zdarzeń przybywających poza kolejnością</span><span class="sxs-lookup"><span data-stu-id="df752-141">Events arriving out of order</span></span>
> * <span data-ttu-id="df752-142">Zduplikowane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="df752-142">Duplicate events</span></span>
> * <span data-ttu-id="df752-143">Porzuconych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="df752-143">Dropped events</span></span>

<span data-ttu-id="df752-144">Przykładowa topologia składa się z następujących składników:</span><span class="sxs-lookup"><span data-stu-id="df752-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="df752-145">Session.CS: symuluje sesji użytkownika, tworząc Identyfikatora sesji losowe początkowy czas i czas trwania sesji.</span><span class="sxs-lookup"><span data-stu-id="df752-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="df752-146">Spout.CS: tworzy 100 sesji, emituje zdarzenia URUCHAMIANIA czeka losowe limitu czasu dla każdej sesji i następnie emituje zdarzenia zakończenia.</span><span class="sxs-lookup"><span data-stu-id="df752-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="df752-147">Następnie odtwarza zakończenia sesji, aby wygenerować nowe.</span><span class="sxs-lookup"><span data-stu-id="df752-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="df752-148">HBaseLookupBolt.cs: używa Identyfikatora sesji do wyszukiwania informacji o sesji z bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="df752-149">Podczas przetwarzania zdarzenia zakończenia odnajduje odpowiednie zdarzenie rozpoczęcia i czas trwania sesji.</span><span class="sxs-lookup"><span data-stu-id="df752-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="df752-150">HBaseBolt.cs: Przechowuje informacje do bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="df752-151">TypeHelper.cs: Ułatwia konwersja typu podczas odczytu / zapisu do bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="df752-152">Schemat bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="df752-152">HBase schema</span></span>

<span data-ttu-id="df752-153">W bazie danych HBase dane są przechowywane w tabeli zawierającej następujące schematu/ustawienia:</span><span class="sxs-lookup"><span data-stu-id="df752-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="df752-154">Klucz wiersza: sesji identyfikator jest używany jako klucz wiersze w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="df752-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="df752-155">Rodziny kolumn: Nazwa rodziny jest "cf".</span><span class="sxs-lookup"><span data-stu-id="df752-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="df752-156">Są przechowywane w tej rodzinie kolumn:</span><span class="sxs-lookup"><span data-stu-id="df752-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="df752-157">Zdarzenie: POCZĄTKOWY lub końcowy.</span><span class="sxs-lookup"><span data-stu-id="df752-157">event: START or END.</span></span>

  * <span data-ttu-id="df752-158">czasu: czas w milisekundach, które wystąpiło zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="df752-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="df752-159">czas trwania: odległość między POCZĄTKOWĄ i KOŃCOWĄ zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="df752-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="df752-160">WERSJE: ustawiono rodziny "cf" do zachowania 5 wersje każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="df752-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="df752-161">Wersje są dziennik z poprzedniej wartości przechowywanych dla klucza określonego wiersza.</span><span class="sxs-lookup"><span data-stu-id="df752-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="df752-162">Domyślnie HBase tylko zwraca wartość dla najnowszej wersji wiersza.</span><span class="sxs-lookup"><span data-stu-id="df752-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="df752-163">W takim przypadku tego samego wiersza jest używany dla każdej wersji wiersza jest identyfikowany przez wartość sygnatury czasowej wszystkie zdarzenia (START, koniec.).</span><span class="sxs-lookup"><span data-stu-id="df752-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="df752-164">Wersje zapewniają widok historycznych danych dotyczących zdarzenia zarejestrowane dla określonego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="df752-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="df752-165">Pobieranie projektu</span><span class="sxs-lookup"><span data-stu-id="df752-165">Download the project</span></span>

<span data-ttu-id="df752-166">Przykładowy projekt można pobrać z [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="df752-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="df752-167">Ten plik do pobrania zawiera następujących projektów C#:</span><span class="sxs-lookup"><span data-stu-id="df752-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="df752-168">CorrelationTopology: Topologii Storm C# losowo emituje zdarzenia rozpoczęcia i zakończenia sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="df752-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="df752-169">Każdej sesji ważny od 1 do 5 minut.</span><span class="sxs-lookup"><span data-stu-id="df752-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="df752-170">SessionInfo: C# aplikacja konsolowa, która tworzy tabeli HBase i zawiera przykładowe zapytania do zwracania informacji dotyczących sesji przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="df752-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="df752-171">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="df752-171">Create the table</span></span>

1. <span data-ttu-id="df752-172">Otwórz **SessionInfo** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df752-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="df752-173">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **SessionInfo** projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="df752-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Zrzut ekranu przedstawiający menu z wybrane właściwości](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="df752-175">Wybierz **ustawienia**, następnie ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="df752-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="df752-176">HBaseClusterURL: adres URL klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="df752-177">Na przykład https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="df752-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="df752-178">HBaseClusterUserName: admin/HTTP konta użytkownika dla klastra</span><span class="sxs-lookup"><span data-stu-id="df752-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="df752-179">HBaseClusterPassword: hasło dla konta użytkownika administracyjnego/HTTP</span><span class="sxs-lookup"><span data-stu-id="df752-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="df752-180">HBaseTableName: Nazwa tabeli, aby użyć tego przykładu</span><span class="sxs-lookup"><span data-stu-id="df752-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="df752-181">HBaseTableColumnFamily: Kolumna nazwę rodziny</span><span class="sxs-lookup"><span data-stu-id="df752-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Obraz okna dialogowego Ustawienia](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="df752-183">Uruchom rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="df752-183">Run the solution.</span></span> <span data-ttu-id="df752-184">Po wyświetleniu monitu wybierz klawisz "c", aby utworzyć tabelę na klaster HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="df752-185">Tworzenie i wdrażanie topologii Storm</span><span class="sxs-lookup"><span data-stu-id="df752-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="df752-186">Otwórz **CorrelationTopology** rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df752-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="df752-187">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **CorrelationTopology** projektu i wybierz polecenie Właściwości.</span><span class="sxs-lookup"><span data-stu-id="df752-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="df752-188">W oknie właściwości wybierz **ustawienia** , a następnie wprowadź wartości konfiguracji dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="df752-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="df752-189">5 pierwszych są takie same wartości używane przez **SessionInfo** projektu:</span><span class="sxs-lookup"><span data-stu-id="df752-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="df752-190">HBaseClusterURL: adres URL klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="df752-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="df752-191">Na przykład https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="df752-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="df752-192">HBaseClusterUserName: admin/HTTP konta użytkownika dla klastra.</span><span class="sxs-lookup"><span data-stu-id="df752-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="df752-193">HBaseClusterPassword: hasło dla konta użytkownika administracyjnego/HTTP.</span><span class="sxs-lookup"><span data-stu-id="df752-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="df752-194">HBaseTableName: Nazwa tabeli do użycia z tym przykładem.</span><span class="sxs-lookup"><span data-stu-id="df752-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="df752-195">Ta wartość jest taka sama nazwa tabeli używana w projekcie SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="df752-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="df752-196">HBaseTableColumnFamily: Kolumna nazwę rodziny.</span><span class="sxs-lookup"><span data-stu-id="df752-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="df752-197">Ta wartość jest tę samą nazwę rodziny kolumny, które jest używane w projekcie SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="df752-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="df752-198">Nie należy zmieniać HBaseTableColumnNames, wartości domyślne są nazwy używane przez **SessionInfo** do pobierania danych.</span><span class="sxs-lookup"><span data-stu-id="df752-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="df752-199">Zapisz właściwości, a następnie skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="df752-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="df752-200">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **przesyłania do systemu Storm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df752-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="df752-201">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="df752-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Obraz przesyłania do elementu menu storm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="df752-203">W **przesyłania topologii** okno dialogowe, wybierz klaster Storm chcesz wdrożyć tej topologii do.</span><span class="sxs-lookup"><span data-stu-id="df752-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="df752-204">Przy pierwszym przesłaniu topologii, może potrwać kilka sekund pobrać nazwy klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df752-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="df752-205">Gdy topologia zostało przekazane i przesłane do klastra, **widoku topologii Storm** otwiera i wyświetla uruchomionej topologii.</span><span class="sxs-lookup"><span data-stu-id="df752-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="df752-206">Aby odświeżyć dane, wybierz **CorrelationTopology** i użyj przycisku Odśwież u góry po prawej części strony.</span><span class="sxs-lookup"><span data-stu-id="df752-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Obraz topologii widoku](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="df752-208">Kiedy rozpoczyna generowania danych, wartość w topologii **Emitted** zwiększa kolumny.</span><span class="sxs-lookup"><span data-stu-id="df752-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="df752-209">Jeśli **widoku topologii Storm** nie Otwórz automatycznie, aby go otworzyć, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df752-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="df752-210">W **Eksploratora rozwiązań**, rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df752-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="df752-211">Kliknij prawym przyciskiem myszy klaster Storm topologia działa na, a następnie wybierz **topologii Storm widoku**</span><span class="sxs-lookup"><span data-stu-id="df752-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="df752-212">Dane zapytania</span><span class="sxs-lookup"><span data-stu-id="df752-212">Query the data</span></span>

<span data-ttu-id="df752-213">Po wysyłanego danych wykonaj następujące kroki, aby wysyłać zapytania o dane.</span><span class="sxs-lookup"><span data-stu-id="df752-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="df752-214">Wróć do **SessionInfo** projektu.</span><span class="sxs-lookup"><span data-stu-id="df752-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="df752-215">Jeśli nie jest uruchomiona, Uruchom nowe wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="df752-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="df752-216">Po wyświetleniu monitu wybierz **s** do wyszukania rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df752-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="df752-217">Zostanie wyświetlony monit o wprowadź czas rozpoczęcia i zakończenia, aby zdefiniować zakres czasu - zwracane są tylko zdarzenia między tymi dwiema wartościami godziny.</span><span class="sxs-lookup"><span data-stu-id="df752-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="df752-218">Podczas wprowadzania godziny rozpoczęcia i zakończenia, użyj następującego formatu: GG: mm i "Używam" lub "pm".</span><span class="sxs-lookup"><span data-stu-id="df752-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="df752-219">Na przykład 23:20:00.</span><span class="sxs-lookup"><span data-stu-id="df752-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="df752-220">Aby przywrócić zarejestrowane zdarzenia, użyj czas rozpoczęcia z przed wdrożonej topologii Storm i czas zakończenia teraz.</span><span class="sxs-lookup"><span data-stu-id="df752-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="df752-221">Danych zwrotnych zawiera wpisy podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="df752-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="df752-222">Wyszukiwanie zdarzeń zakończenia działa tak samo, jak rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df752-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="df752-223">Jednak zakończenia zdarzenia są generowane losowo od 1 do 5 minut po zdarzeniu rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="df752-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="df752-224">Może być konieczne spróbuj kilka przedziałów czasu, aby znaleźć zdarzenia zakończenia.</span><span class="sxs-lookup"><span data-stu-id="df752-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="df752-225">Zdarzenia zakończenia zawierają również czas trwania sesji - różnicę czasu zdarzenia rozpoczęcia i godzina zakończenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df752-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="df752-226">Oto przykładowe dane dla zdarzenia zakończenia:</span><span class="sxs-lookup"><span data-stu-id="df752-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="df752-227">Wprowadzone wartości czasu są według czasu lokalnego, czas zwróconych przez kwerendę jest w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="df752-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="df752-228">Zatrzymywanie topologii</span><span class="sxs-lookup"><span data-stu-id="df752-228">Stop the topology</span></span>

<span data-ttu-id="df752-229">Gdy wszystko będzie gotowe zatrzymać topologii, wróć do **CorrelationTopology** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df752-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="df752-230">W **widoku topologii Storm**, wybierz topologii, a następnie użyj **Kill** u góry widoku topologii.</span><span class="sxs-lookup"><span data-stu-id="df752-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="df752-231">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="df752-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="df752-232">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df752-232">Next steps</span></span>

<span data-ttu-id="df752-233">Aby uzyskać więcej przykładów Storm, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="df752-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
