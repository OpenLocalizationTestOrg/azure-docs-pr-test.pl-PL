---
title: "zdarzenia aaaCorrelate w zależności od platformy Storm oraz bazy danych HBase w usłudze HDInsight"
description: "Dowiedz się, jak zdarzenia toocorrelate, pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase w usłudze HDInsight."
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
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="8f39f-103">Korelowanie zdarzeń pojawiające się w różnych momentach za pomocą Storm i bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="8f39f-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="8f39f-104">Przy użyciu magazynu danych z systemu Apache Storm, może skorelować danych wpisów, pojawiające się w różnych godzinach.</span><span class="sxs-lookup"><span data-stu-id="8f39f-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="8f39f-105">Na przykład łączenie zdarzenia logowania i wylogowania dla toocalculate sesji użytkownika jak długo hello sesji trwała.</span><span class="sxs-lookup"><span data-stu-id="8f39f-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="8f39f-106">W tym dokumencie omówiono sposób toocreate podstawowe topologii Storm C#, który śledzi zdarzenia logowania i wylogowywania sesji użytkownika, a następnie oblicza hello czas trwania sesji hello.</span><span class="sxs-lookup"><span data-stu-id="8f39f-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="8f39f-107">Topologia Hello używa bazy danych HBase jako magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8f39f-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="8f39f-108">Baza danych HBase można też tooperform partii zapytań na powitania danych historycznych tooproduce dodatkowe informacje szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="8f39f-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="8f39f-109">Na przykład jak wiele sesji użytkownika zostały rozpoczął się lub zakończył się w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="8f39f-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f39f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f39f-110">Prerequisites</span></span>

* <span data-ttu-id="8f39f-111">Visual Studio i hello HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f39f-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="8f39f-112">Aby uzyskać więcej informacji, zobacz [rozpocząć korzystanie z hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f39f-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="8f39f-113">Apache Storm w usłudze HDInsight klastra (z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="8f39f-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="8f39f-114">Topologie SCP.NET są obsługiwane w klastrach opartych na systemie Linux Storm utworzone po 10/28/2016, hello HBase zestawu SDK pakietu .NET jest dostępny od 10/28/2016 nie działa poprawnie na HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="8f39f-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="8f39f-115">Bazy danych Apache HBase w klastrze usługi HDInsight (Linux lub z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="8f39f-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8f39f-116">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8f39f-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8f39f-117">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="8f39f-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8f39f-118">[Java](https://java.com) 1.7 lub nowszej na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="8f39f-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="8f39f-119">Java jest topologii hello toopackage używane, gdy jest toohello przesyłanego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8f39f-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="8f39f-120">Witaj **JAVA_HOME** środowiska zmiennej musi toohello punktu katalog, który zawiera Java.</span><span class="sxs-lookup"><span data-stu-id="8f39f-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="8f39f-121">Witaj **%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="8f39f-122">Architektura</span><span class="sxs-lookup"><span data-stu-id="8f39f-122">Architecture</span></span>

![Diagram przepływu danych hello za pośrednictwem hello topologii](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="8f39f-124">Korelowanie zdarzeń wymaga identyfikator wspólnej dla hello źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="8f39f-125">For example identyfikator użytkownika, identyfikator sesji lub inny element danych to) unikatowy i (b) objęte wszystkie dane przesyłane tooStorm.</span><span class="sxs-lookup"><span data-stu-id="8f39f-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="8f39f-126">W tym przykładzie użyto toorepresent wartość identyfikatora GUID identyfikator sesji.</span><span class="sxs-lookup"><span data-stu-id="8f39f-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="8f39f-127">W tym przykładzie składa się z dwóch klastrów usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8f39f-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="8f39f-128">HBase: dane historyczne w magazynie danych trwałych</span><span class="sxs-lookup"><span data-stu-id="8f39f-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="8f39f-129">STORM: dane przychodzące tooingest używane</span><span class="sxs-lookup"><span data-stu-id="8f39f-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="8f39f-130">dane Hello jest generowany losowo hello topologii Storm i składa się z hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8f39f-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="8f39f-131">Identyfikator sesji: identyfikator GUID, który unikatowo identyfikuje każdej sesji</span><span class="sxs-lookup"><span data-stu-id="8f39f-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="8f39f-132">Zdarzenie: POCZĄTKOWY lub końcowy zdarzeniem.</span><span class="sxs-lookup"><span data-stu-id="8f39f-132">Event: a START or END event.</span></span> <span data-ttu-id="8f39f-133">Na przykład, START zawsze występuje przed zakończeniem</span><span class="sxs-lookup"><span data-stu-id="8f39f-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="8f39f-134">Czas: czas hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="8f39f-135">Te dane są przetwarzane i przechowywane w bazie danych HBase.</span><span class="sxs-lookup"><span data-stu-id="8f39f-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="8f39f-136">Topologii STORM</span><span class="sxs-lookup"><span data-stu-id="8f39f-136">Storm topology</span></span>

<span data-ttu-id="8f39f-137">Po uruchomieniu sesji **START** zdarzeń jest odbierany przez hello topologii i rejestrowane tooHBase.</span><span class="sxs-lookup"><span data-stu-id="8f39f-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="8f39f-138">Gdy **zakończenia** odebraniu zdarzenia, topologii hello pobiera hello **START** zdarzeń i oblicza hello czasu między zdarzeniami hello dwa.</span><span class="sxs-lookup"><span data-stu-id="8f39f-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="8f39f-139">To **czas trwania** wartość następnie jest przechowywana w bazie danych HBase oraz hello **zakończenia** informacji o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="8f39f-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f39f-140">Gdy ta topologia przedstawia podstawowy wzorzec hello, rozwiązanie produkcji wymagałoby tootake projektu dla hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="8f39f-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="8f39f-141">Zdarzeń przybywających poza kolejnością</span><span class="sxs-lookup"><span data-stu-id="8f39f-141">Events arriving out of order</span></span>
> * <span data-ttu-id="8f39f-142">Zduplikowane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="8f39f-142">Duplicate events</span></span>
> * <span data-ttu-id="8f39f-143">Porzuconych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8f39f-143">Dropped events</span></span>

<span data-ttu-id="8f39f-144">Witaj przykładowa topologia składa się z hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="8f39f-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="8f39f-145">Session.CS: symuluje sesji użytkownika, tworząc Identyfikatora sesji losowe okresu sesji hello czas i czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="8f39f-146">Spout.CS: tworzy 100 sesji, emituje zdarzenia URUCHAMIANIA czeka hello losowe limitu czasu dla każdej sesji i następnie emituje zdarzenia zakończenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="8f39f-147">Następnie odtwarza zakończenia sesji toogenerate nowe.</span><span class="sxs-lookup"><span data-stu-id="8f39f-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="8f39f-148">HBaseLookupBolt.cs: używa toolook identyfikator sesji hello sesji informacji z bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="8f39f-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="8f39f-149">Podczas przetwarzania zdarzenia zakończenia znajduje hello odpowiednie zdarzenie START i oblicza hello czas trwania sesji hello.</span><span class="sxs-lookup"><span data-stu-id="8f39f-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="8f39f-150">HBaseBolt.cs: Przechowuje informacje do bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="8f39f-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="8f39f-151">TypeHelper.cs: Konwersja typów odczytu / zapisu tooHBase ułatwia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="8f39f-152">Schemat bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="8f39f-152">HBase schema</span></span>

<span data-ttu-id="8f39f-153">W bazie danych HBase hello dane są przechowywane w tabeli z powitania po schemat i ustawień:</span><span class="sxs-lookup"><span data-stu-id="8f39f-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="8f39f-154">Klucz wiersza: hello sesji identyfikator jest używany jako klucz hello wiersze w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8f39f-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="8f39f-155">Rodziny kolumn: Nazwa rodziny hello jest "cf".</span><span class="sxs-lookup"><span data-stu-id="8f39f-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="8f39f-156">Są przechowywane w tej rodzinie kolumn:</span><span class="sxs-lookup"><span data-stu-id="8f39f-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="8f39f-157">Zdarzenie: POCZĄTKOWY lub końcowy.</span><span class="sxs-lookup"><span data-stu-id="8f39f-157">event: START or END.</span></span>

  * <span data-ttu-id="8f39f-158">czas: Wystąpił hello czasu w milisekundach hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8f39f-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="8f39f-159">czas trwania: hello długość od rozpoczęcia i zakończenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="8f39f-160">WERSJE: rodziny "cf" hello ustawiono tooretain 5 wersje każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8f39f-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8f39f-161">Wersje są dziennik z poprzedniej wartości przechowywanych dla klucza określonego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8f39f-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="8f39f-162">Domyślnie HBase tylko zwraca wartość hello hello najnowszej wersji wiersza.</span><span class="sxs-lookup"><span data-stu-id="8f39f-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="8f39f-163">W takim przypadku hello tego samego wiersza jest używany dla każdej wersji wiersza jest identyfikowany przez wartość sygnatury czasowej hello wszystkie zdarzenia (START, koniec.).</span><span class="sxs-lookup"><span data-stu-id="8f39f-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="8f39f-164">Wersje zapewniają widok historycznych danych dotyczących zdarzenia zarejestrowane dla określonego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="8f39f-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="8f39f-165">Pobierz hello projektu</span><span class="sxs-lookup"><span data-stu-id="8f39f-165">Download hello project</span></span>

<span data-ttu-id="8f39f-166">Witaj przykładowy projekt można pobrać z [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="8f39f-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="8f39f-167">Ten plik do pobrania zawiera hello następujących projektów C#:</span><span class="sxs-lookup"><span data-stu-id="8f39f-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="8f39f-168">CorrelationTopology: Topologii Storm C# losowo emituje zdarzenia rozpoczęcia i zakończenia sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f39f-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="8f39f-169">Każdej sesji ważny od 1 do 5 minut.</span><span class="sxs-lookup"><span data-stu-id="8f39f-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="8f39f-170">SessionInfo: C# aplikacja konsolowa, która tworzy hello tabeli HBase i zawiera przykładowe zapytania tooreturn informacji o sesji przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="8f39f-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="8f39f-171">Utwórz tabelę hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-171">Create hello table</span></span>

1. <span data-ttu-id="8f39f-172">Otwórz hello **SessionInfo** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f39f-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="8f39f-173">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **SessionInfo** projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="8f39f-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Zrzut ekranu przedstawiający menu z wybrane właściwości](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="8f39f-175">Wybierz **ustawienia**, a następnie hello ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="8f39f-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="8f39f-176">HBaseClusterURL: tooyour klaster HBase hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="8f39f-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="8f39f-177">Na przykład https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="8f39f-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="8f39f-178">HBaseClusterUserName: konto użytkownika hello admin/HTTP dla klastra</span><span class="sxs-lookup"><span data-stu-id="8f39f-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="8f39f-179">HBaseClusterPassword: hello hasła dla konta użytkownika administracyjnego/HTTP hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="8f39f-180">HBaseTableName: Nazwa hello hello toouse tabeli z tego przykładu</span><span class="sxs-lookup"><span data-stu-id="8f39f-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="8f39f-181">HBaseTableColumnFamily: Nazwa rodziny kolumny hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Obraz okna dialogowego Ustawienia](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="8f39f-183">Uruchamianie hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8f39f-183">Run hello solution.</span></span> <span data-ttu-id="8f39f-184">Po wyświetleniu monitu wybierz hello "c" klucza toocreate hello tabeli na klaster HBase.</span><span class="sxs-lookup"><span data-stu-id="8f39f-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="8f39f-185">Tworzenie i wdrażanie topologii Storm hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="8f39f-186">Otwórz hello **CorrelationTopology** rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f39f-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="8f39f-187">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **CorrelationTopology** projektu i wybierz polecenie Właściwości.</span><span class="sxs-lookup"><span data-stu-id="8f39f-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="8f39f-188">W oknie właściwości hello wybierz **ustawienia** , a następnie wprowadź wartości konfiguracji powitania dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="8f39f-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="8f39f-189">Witaj 5 pierwszych są hello używać tej samej wartości hello **SessionInfo** projektu:</span><span class="sxs-lookup"><span data-stu-id="8f39f-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="8f39f-190">HBaseClusterURL: tooyour klaster HBase hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="8f39f-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="8f39f-191">Na przykład https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="8f39f-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="8f39f-192">HBaseClusterUserName: hello admin/HTTP konta użytkownika dla klastra.</span><span class="sxs-lookup"><span data-stu-id="8f39f-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="8f39f-193">HBaseClusterPassword: hello hasło dla konta użytkownika administracyjnego/HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="8f39f-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="8f39f-194">HBaseTableName: Nazwa hello hello toouse tabeli z tym przykładem.</span><span class="sxs-lookup"><span data-stu-id="8f39f-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="8f39f-195">Ta wartość jest hello takie same nazwy tabeli, ponieważ używany w projekcie SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="8f39f-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="8f39f-196">HBaseTableColumnFamily: Nazwa rodziny hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="8f39f-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="8f39f-197">Ta wartość jest hello takie same nazwy rodziny kolumny w hello SessionInfo projektu.</span><span class="sxs-lookup"><span data-stu-id="8f39f-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8f39f-198">Nie zmieniaj hello HBaseTableColumnNames, jako ustawienia domyślne hello są nazwy hello są używane przez **SessionInfo** tooretrieve danych.</span><span class="sxs-lookup"><span data-stu-id="8f39f-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="8f39f-199">Zapisz właściwości hello, a następnie kompilacji hello projektu.</span><span class="sxs-lookup"><span data-stu-id="8f39f-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="8f39f-200">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8f39f-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="8f39f-201">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f39f-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Obraz powitania Prześlij toostorm element menu](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="8f39f-203">W hello **przesyłania topologii** okno dialogowe, ma toodeploy tej topologii do klastra Storm hello wybierz.</span><span class="sxs-lookup"><span data-stu-id="8f39f-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f39f-204">Witaj przesyłania topologii, po raz pierwszy może potrwać kilka sekund tooretrieve nazwę hello klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8f39f-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="8f39f-205">Po topologii hello toohello przekazywać i przesyłanego klastra, hello **widoku topologii Storm** otwiera i wyświetla hello systemem topologii.</span><span class="sxs-lookup"><span data-stu-id="8f39f-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="8f39f-206">toorefresh hello danych, wybierz opcję hello **CorrelationTopology** i użyj przycisku Odśwież hello na powitania z góry po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8f39f-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Obraz powitania topologii widoku](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="8f39f-208">Po rozpoczęciu topologii hello generowania danych hello wartość hello **Emitted** zwiększa kolumny.</span><span class="sxs-lookup"><span data-stu-id="8f39f-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f39f-209">Jeśli hello **widoku topologii Storm** nie jest otwierany automatycznie, użyj hello następujących tooopen kroki:</span><span class="sxs-lookup"><span data-stu-id="8f39f-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="8f39f-210">W **Eksploratora rozwiązań**, rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8f39f-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="8f39f-211">Klaster Storm powitania kliknij prawym przyciskiem myszy hello topologii uruchomionych na, a następnie wybierz **topologii Storm widoku**</span><span class="sxs-lookup"><span data-stu-id="8f39f-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="8f39f-212">Dane hello zapytania</span><span class="sxs-lookup"><span data-stu-id="8f39f-212">Query hello data</span></span>

<span data-ttu-id="8f39f-213">Po wysyłanego danych użyj hello następujące kroki tooquery hello danych.</span><span class="sxs-lookup"><span data-stu-id="8f39f-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="8f39f-214">Zwraca toohello **SessionInfo** projektu.</span><span class="sxs-lookup"><span data-stu-id="8f39f-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="8f39f-215">Jeśli nie jest uruchomiona, Uruchom nowe wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="8f39f-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="8f39f-216">Po wyświetleniu monitu wybierz **s** toosearch rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="8f39f-217">Są tooenter zostanie wyświetlony monit o rozpoczęcia i zakończenia czasu toodefine zakres czasu - zwracane są tylko zdarzenia między tymi dwiema wartościami godziny.</span><span class="sxs-lookup"><span data-stu-id="8f39f-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="8f39f-218">Użyj następujących hello formatowania podczas wprowadzania hello rozpoczęcia i zakończenia razy: GG: mm i "Używam" lub "pm".</span><span class="sxs-lookup"><span data-stu-id="8f39f-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="8f39f-219">Na przykład 23:20:00.</span><span class="sxs-lookup"><span data-stu-id="8f39f-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="8f39f-220">tooreturn rejestrowane zdarzenia, użyj czas rozpoczęcia z przed hello wdrożonej topologii Storm i czas zakończenia teraz.</span><span class="sxs-lookup"><span data-stu-id="8f39f-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="8f39f-221">Witaj zwracanych danych zawiera wpisy toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="8f39f-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="8f39f-222">Wyszukiwanie zakończenia zdarzenia działa hello sam jako rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="8f39f-223">Jednak zakończenia zdarzenia są generowane losowo od 1 do 5 minut po hello rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="8f39f-224">Tootry może mieć kilka zakresów toofind hello zakończenia zdarzenia w czasie.</span><span class="sxs-lookup"><span data-stu-id="8f39f-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="8f39f-225">Zdarzenia zakończenia zawierają również hello czas trwania sesji hello - hello różnica między hello rozpoczęcia zdarzenia czas i czas zakończenia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8f39f-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="8f39f-226">Oto przykładowe dane dla zdarzenia zakończenia:</span><span class="sxs-lookup"><span data-stu-id="8f39f-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="8f39f-227">Wartości czasu hello są według czasu lokalnego, czas hello zwracane z kwerendy hello jest w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="8f39f-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="8f39f-228">Zatrzymywanie topologii hello</span><span class="sxs-lookup"><span data-stu-id="8f39f-228">Stop hello topology</span></span>

<span data-ttu-id="8f39f-229">Gdy wszystko jest gotowe toostop hello topologii, zwróć toohello **CorrelationTopology** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f39f-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="8f39f-230">W hello **widoku topologii Storm**, wybierz hello topologii, a następnie użyj hello **Kill** u góry hello hello topologii widoku.</span><span class="sxs-lookup"><span data-stu-id="8f39f-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="8f39f-231">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="8f39f-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="8f39f-232">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f39f-232">Next steps</span></span>

<span data-ttu-id="8f39f-233">Aby uzyskać więcej przykładów Storm, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8f39f-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
