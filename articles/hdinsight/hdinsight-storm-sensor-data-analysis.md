---
title: "dane czujników aaaAnalyze z systemu Apache Storm i bazy danych HBase | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooApache Storm z siecią wirtualną. Używać systemu Storm danych czujnika tooprocess HBase z Centrum zdarzeń i wizualizację go z D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="7c571-104">Analizowanie danych czujnika z systemu Apache Storm, Centrum zdarzeń i bazy danych HBase w usłudze HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="7c571-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="7c571-105">Dowiedz się, jak toouse Apache Storm w dane czujników tooprocess HDInsight z Centrum zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c571-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="7c571-106">Witaj danych będzie przechowywany do bazy danych Apache HBase w usłudze HDInsight i wizualizowane za pomocą D3.js.</span><span class="sxs-lookup"><span data-stu-id="7c571-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="7c571-107">Szablon usługi Azure Resource Manager Hello używany w tym dokumencie przedstawiono sposób toocreate wielu zasobów platformy Azure w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c571-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="7c571-108">Szablon Hello tworzy sieci wirtualnej platformy Azure, dwa klastry usługi HDInsight (Storm oraz bazy danych HBase) i aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c571-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="7c571-109">Implementacja node.js pulpit nawigacyjny sieci web w czasie rzeczywistym jest toohello automatycznie wdrożonej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c571-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="7c571-110">Witaj informacje w tym dokumencie i przykład, w tym dokumencie wymagają HDInsight wersji 3,6.</span><span class="sxs-lookup"><span data-stu-id="7c571-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="7c571-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7c571-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7c571-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="7c571-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c571-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c571-113">Prerequisites</span></span>

* <span data-ttu-id="7c571-114">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c571-114">An Azure subscription.</span></span>
* <span data-ttu-id="7c571-115">[Node.js](http://nodejs.org/): pulpitu nawigacyjnego sieci web hello toopreview używane lokalnie na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="7c571-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="7c571-116">[Java i hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): używane topologii Storm hello toodevelop.</span><span class="sxs-lookup"><span data-stu-id="7c571-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="7c571-117">[Maven](http://maven.apache.org/what-is-maven.html): używanych projektów hello toobuild i kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7c571-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="7c571-118">[Git](http://git-scm.com/): toodownload używane hello projektu z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c571-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="7c571-119">**SSH** klienta: używane tooconnect toohello opartych na systemie Linux klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="7c571-120">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7c571-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="7c571-121">Nie trzeba istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="7c571-122">kroki Hello w tym dokumencie Utwórz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="7c571-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="7c571-123">Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c571-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="7c571-124">Storm w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="7c571-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="7c571-125">Baza danych HBase w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="7c571-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="7c571-126">Aplikacji sieci Web platformy Azure obsługuje hello pulpit nawigacyjny z sieci web</span><span class="sxs-lookup"><span data-stu-id="7c571-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="7c571-127">Architektura</span><span class="sxs-lookup"><span data-stu-id="7c571-127">Architecture</span></span>

![diagram architektury](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="7c571-129">W tym przykładzie składa się z hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="7c571-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="7c571-130">**Usługa Azure Event Hubs**: zawiera dane, które mają być zbierane z czujników.</span><span class="sxs-lookup"><span data-stu-id="7c571-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="7c571-131">**STORM w usłudze HDInsight**: udostępnia w czasie rzeczywistym przetwarzania danych z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="7c571-132">**Baza danych HBase w usłudze HDInsight**: udostępnia trwałym magazynem danych NoSQL dla danych po przetworzeniu przez Storm.</span><span class="sxs-lookup"><span data-stu-id="7c571-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="7c571-133">**Usługi sieci wirtualnej Azure**: umożliwia bezpieczną komunikację między hello Storm w usłudze HDInsight i bazy danych HBase w klastrach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7c571-134">Sieć wirtualna jest wymagany, korzystając z interfejsu API klienta Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="7c571-135">Nie jest widoczne za pośrednictwem bramy publicznego hello w przypadku klastrów HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="7c571-136">Instalowanie bazy danych HBase i Storm klastrów w tej samej sieci wirtualnej umożliwia hello hello klastra Storm (lub inne systemy w sieci wirtualnej hello) toodirectly dostęp do bazy danych HBase przy użyciu interfejsu API klienta.</span><span class="sxs-lookup"><span data-stu-id="7c571-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="7c571-137">**Witryny sieci Web pulpitu nawigacyjnego**: przykładowy pulpit nawigacyjny, który wykresy danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="7c571-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="7c571-138">witryny sieci Web Hello jest zaimplementowany w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="7c571-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="7c571-139">[Użyciu biblioteki Socket.IO](http://socket.io/) jest używany w czasie rzeczywistym komunikacji między hello topologii Storm i hello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7c571-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7c571-140">Przy użyciu biblioteki Socket.io komunikacji jest szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="7c571-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="7c571-141">Możesz użyć dowolnej architektury komunikacji, takie jak Websocket raw lub SignalR.</span><span class="sxs-lookup"><span data-stu-id="7c571-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="7c571-142">[D3.js](http://d3js.org/) jest używane toograph hello dane są przesyłane toohello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7c571-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c571-143">Dwa klastry są wymagane, ponieważ nie ma żadnych obsługiwana metoda toocreate jednego klastra usługi HDInsight Storm i bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="7c571-144">Witaj topologii odczytuje dane z Centrum zdarzeń za pomocą hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) klasy i zapisuje dane do bazy danych HBase przy użyciu hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) Klasa.</span><span class="sxs-lookup"><span data-stu-id="7c571-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="7c571-145">Komunikacja z witryny sieci Web hello odbywa się przy użyciu [client.java użyciu biblioteki socket.io](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="7c571-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="7c571-146">powitania po diagram wyjaśniono hello układ topologii hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagram topologii](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="7c571-148">Ten diagram jest uproszczona prezentacja hello topologii.</span><span class="sxs-lookup"><span data-stu-id="7c571-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="7c571-149">Dla każdej partycji w Centrum zdarzeń jest tworzone wystąpienie każdego składnika.</span><span class="sxs-lookup"><span data-stu-id="7c571-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="7c571-150">Te wystąpienia są rozproszone na powitania węzłów w klastrze hello, a dane są przesyłane między nimi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7c571-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="7c571-151">Dane z analizatora toohello spout hello jest równoważone.</span><span class="sxs-lookup"><span data-stu-id="7c571-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="7c571-152">Dane z toohello analizator hello pulpitu nawigacyjnego i HBase są grupowane według Identyfikatora urządzenia, tak, aby zawsze hello wiadomości z tym samym urządzeniu przepływ toohello tego składnika.</span><span class="sxs-lookup"><span data-stu-id="7c571-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="7c571-153">Składniki topologii</span><span class="sxs-lookup"><span data-stu-id="7c571-153">Topology components</span></span>

* <span data-ttu-id="7c571-154">**Elementów Spout Centrum zdarzeń**: hello spout jest podana jako część systemu Apache Storm w wersji 0.10.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7c571-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7c571-155">w tym przykładzie spout Centrum zdarzeń Hello wymaga platformy Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6.</span><span class="sxs-lookup"><span data-stu-id="7c571-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="7c571-156">**ParserBolt.java**: hello dane, które są emitowane przez hello spout jest nieprzetworzone dane JSON, a czasami więcej niż jedno zdarzenie jest emitowany naraz.</span><span class="sxs-lookup"><span data-stu-id="7c571-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="7c571-157">Dany element bolt odczytuje hello danych emitowanych przez hello spout i analizuje wiadomości powitania JSON.</span><span class="sxs-lookup"><span data-stu-id="7c571-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="7c571-158">Hello bolt następnie emituje hello danych jako spójnej kolekcji, która zawiera wiele pól.</span><span class="sxs-lookup"><span data-stu-id="7c571-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="7c571-159">**DashboardBolt.java**: ten składnik pokazano, jak toouse hello użyciu biblioteki Socket.io biblioteki klienta dla programu Java toosend danych w czasie rzeczywistym toohello sieci web z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7c571-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="7c571-160">**nie hbase.yaml**: hello definicji topologii używany podczas pracy w trybie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7c571-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="7c571-161">Nie używa składników bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-161">It does not use HBase components.</span></span>
* <span data-ttu-id="7c571-162">**z hbase.yaml**: hello definicji topologii używany, gdy działa w klastrze hello hello topologii.</span><span class="sxs-lookup"><span data-stu-id="7c571-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="7c571-163">Wykorzystuje ona składników bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-163">It does use HBase components.</span></span>
* <span data-ttu-id="7c571-164">**dev.Properties**: hello informacji o konfiguracji dla hello spout Centrum zdarzeń, HBase bolt i składniki pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7c571-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="7c571-165">Przygotowywanie środowiska</span><span class="sxs-lookup"><span data-stu-id="7c571-165">Prepare your environment</span></span>

<span data-ttu-id="7c571-166">Przed skorzystaniem z tego przykładu, należy utworzyć usługi Azure Event Hub, które topologii Storm hello odczytuje z.</span><span class="sxs-lookup"><span data-stu-id="7c571-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="7c571-167">Konfigurowanie Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7c571-167">Configure Event Hub</span></span>

<span data-ttu-id="7c571-168">Centrum zdarzeń jest hello źródła danych w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7c571-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="7c571-169">Użyj hello następujące kroki toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="7c571-170">Z hello [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy** -> **Internetu rzeczy** -> **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="7c571-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="7c571-171">W hello **utworzyć Namespace** sekcji, wykonaj następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="7c571-172">Wprowadź **nazwa** hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7c571-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="7c571-173">Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="7c571-173">Select a pricing tier.</span></span> <span data-ttu-id="7c571-174">**Podstawowe** jest wystarczająca dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="7c571-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="7c571-175">Wybierz hello Azure **subskrypcji** toouse.</span><span class="sxs-lookup"><span data-stu-id="7c571-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="7c571-176">Wybierz istniejącą grupę zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="7c571-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="7c571-177">Wybierz hello **lokalizacji** dla hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="7c571-178">Wybierz **toodashboard numeru Pin**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7c571-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="7c571-179">Po ukończeniu procesu tworzenia hello hello informacji centra zdarzeń w przestrzeni nazw jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="7c571-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="7c571-180">W tym miejscu, wybierz **+ Dodaj Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="7c571-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="7c571-181">W hello **tworzenia Centrum zdarzeń** sekcji, wprowadź nazwę **sensordata**, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7c571-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="7c571-182">Pozostaw hello innych pól na powitania wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="7c571-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="7c571-183">Z centrów zdarzeń hello wyświetlić obszar nazw, wybierz opcję **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="7c571-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="7c571-184">Wybierz hello **sensordata** wpisu.</span><span class="sxs-lookup"><span data-stu-id="7c571-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="7c571-185">Witaj sensordata Centrum zdarzeń, zaznacz **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="7c571-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="7c571-186">Użyj hello **+ Dodaj** hello tooadd łącze następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="7c571-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="7c571-187">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="7c571-187">Policy name</span></span> | <span data-ttu-id="7c571-188">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="7c571-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="7c571-189">urządzenia</span><span class="sxs-lookup"><span data-stu-id="7c571-189">devices</span></span> | <span data-ttu-id="7c571-190">Send</span><span class="sxs-lookup"><span data-stu-id="7c571-190">Send</span></span> |
    | <span data-ttu-id="7c571-191">STORM</span><span class="sxs-lookup"><span data-stu-id="7c571-191">storm</span></span> | <span data-ttu-id="7c571-192">Nasłuchiwanie</span><span class="sxs-lookup"><span data-stu-id="7c571-192">Listen</span></span> |

1. <span data-ttu-id="7c571-193">Zaznacz obie zasady i zanotuj hello **klucz podstawowy** wartość.</span><span class="sxs-lookup"><span data-stu-id="7c571-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="7c571-194">Należy hello wartość dla obu zasad w przyszłości czynności.</span><span class="sxs-lookup"><span data-stu-id="7c571-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="7c571-195">Pobierz i skonfiguruj hello projektu</span><span class="sxs-lookup"><span data-stu-id="7c571-195">Download and configure hello project</span></span>

<span data-ttu-id="7c571-196">Użyj powitania po toodownload hello projektu z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c571-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="7c571-197">Po zakończeniu wykonywania polecenia hello masz powitania po strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="7c571-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="7c571-198">Ten dokument nie przechodzi w szczegółach toofull hello kodu zawarte w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7c571-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="7c571-199">Jednak kod hello jest całkowicie oznaczone jako.</span><span class="sxs-lookup"><span data-stu-id="7c571-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="7c571-200">tooconfigure hello projektu tooread z Centrum zdarzeń, otwórz hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` plik i dodać Twojego toohello informacje o Centrum zdarzeń następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="7c571-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="7c571-201">Kompilowanie i testowanie lokalnie</span><span class="sxs-lookup"><span data-stu-id="7c571-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c571-202">Lokalnie przy użyciu topologii hello wymaga działającego środowiska deweloperskiego Storm.</span><span class="sxs-lookup"><span data-stu-id="7c571-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="7c571-203">Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) w serwisie Apache.org.</span><span class="sxs-lookup"><span data-stu-id="7c571-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="7c571-204">Jeśli używasz środowiska projektowego systemu Windows może zostać wyświetlony `java.io.IOException` podczas uruchamiania topologii hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7c571-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="7c571-205">Jeśli tak, przesuń w topologii hello toorunning w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="7c571-206">Przed przeprowadzeniem jej testów, należy uruchomić hello pulpitu nawigacyjnego tooview hello dane wyjściowe hello topologii i generowanie toostore danych w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c571-207">składnik HBase Hello Ta topologia nie jest aktywne podczas testowania lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7c571-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="7c571-208">Witaj interfejsu API języka Java dla klastra HBase hello nie są dostępne z hello zewnętrznej sieci wirtualnej platformy Azure, zawierającą hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="7c571-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="7c571-209">Uruchom aplikację sieci web hello</span><span class="sxs-lookup"><span data-stu-id="7c571-209">Start hello web application</span></span>

1. <span data-ttu-id="7c571-210">Otwórz wiersz polecenia i zmień katalogi zbyt`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="7c571-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="7c571-211">Użyj następującej zależności hello tooinstall polecenia wymagane przez aplikację sieci web hello hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="7c571-212">Użyj następującej aplikacji sieci web hello toostart polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="7c571-213">Zostanie wyświetlony komunikat toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7c571-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="7c571-214">Otwórz przeglądarkę sieci web, a następnie wprowadź `http://localhost:3000/` jako adres hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="7c571-215">Jest wyświetlana strona toohello podobne, po obrazu:</span><span class="sxs-lookup"><span data-stu-id="7c571-215">A page similar toohello following image is displayed:</span></span>
   
    ![pulpit nawigacyjny sieci Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="7c571-217">Ten wiersz polecenia pozostaw otwarte.</span><span class="sxs-lookup"><span data-stu-id="7c571-217">Leave this command prompt open.</span></span> <span data-ttu-id="7c571-218">Po zakończeniu testowania, Użyj serwera sieci web hello toostop Ctrl-C.</span><span class="sxs-lookup"><span data-stu-id="7c571-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="7c571-219">Generowanie danych</span><span class="sxs-lookup"><span data-stu-id="7c571-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="7c571-220">Witaj w tej sekcji użycia środowiska Node.js, dzięki czemu mogą być używane na dowolnej platformie.</span><span class="sxs-lookup"><span data-stu-id="7c571-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="7c571-221">Inne przykłady języka można znaleźć w temacie hello `SendEvents` katalogu.</span><span class="sxs-lookup"><span data-stu-id="7c571-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="7c571-222">Otwórz nowy wiersz, powłokę lub terminal i zmień katalogi zbyt`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="7c571-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="7c571-223">zależności hello tooinstall wymagane przez aplikację hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7c571-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="7c571-224">Otwórz hello `app.js` plik w edytorze tekstów i Dodaj hello uzyskanymi wcześniej informacji Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="7c571-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7c571-225">W tym przykładzie przyjęto założenie, że użyto `sensordata` jako hello nazwę Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="7c571-226">Oraz że `devices` jako nazwa hello zasady hello `Send` oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7c571-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="7c571-227">Użyj następującego polecenia tooinsert nowe wpisy w Centrum zdarzeń hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="7c571-228">Pojawić kilka wierszy danych wyjściowych, które zawierają hello danych wysłanych tooEvent Centrum:</span><span class="sxs-lookup"><span data-stu-id="7c571-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="7c571-229">Skompilować i uruchomić hello topologii</span><span class="sxs-lookup"><span data-stu-id="7c571-229">Build and start hello topology</span></span>

1. <span data-ttu-id="7c571-230">Otwórz nowy wiersz polecenia i zmień katalogi zbyt`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="7c571-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="7c571-231">toobuild i pakietu hello topologii, należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="7c571-232">Topologia hello toostart w trybie lokalnym hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7c571-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="7c571-233">`--local`Topologia hello jest uruchamiany w trybie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7c571-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="7c571-234">`--filter`używa hello `dev.properties` parametry toopopulate plików w definicji topologii hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="7c571-235">`resources/no-hbase.yaml`używa hello `no-hbase.yaml` definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="7c571-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="7c571-236">Po rozpoczęciu topologii hello odczytuje wpisów z Centrum zdarzeń, a następnie wysyła je pulpitu nawigacyjnego toohello uruchomiony na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7c571-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="7c571-237">Powinny pojawić się wiersze są wyświetlane na pulpicie nawigacyjnym z sieci web hello, podobne toohello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="7c571-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![pulpit nawigacyjny z danymi](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="7c571-239">Pulpit nawigacyjny hello jest uruchomiona, użyj hello `node app.js` polecenie z poprzedniego hello kroki toosend nowych danych tooEvent koncentratorów.</span><span class="sxs-lookup"><span data-stu-id="7c571-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="7c571-240">Ponieważ wartości temperatury hello są losowo generowany, wykres hello należy zaktualizować tooshow dużych zmian w temperatury.</span><span class="sxs-lookup"><span data-stu-id="7c571-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c571-241">Musi być w hello **hdinsight-eventhub — przykład/SendEvents/Nodejs** katalogu przy użyciu hello `node app.js` polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c571-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="7c571-242">Po zweryfikowaniu tego pulpitu nawigacyjnego hello aktualizacji topologii hello Zatrzymaj przy użyciu klawiszy Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="7c571-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="7c571-243">Możesz również używać serwera web lokalne powitania toostop klawisze Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="7c571-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="7c571-244">Tworzenie klastra Storm oraz bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="7c571-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="7c571-245">Witaj kroki opisane w tej sekcji używają [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate klastra sieci wirtualnej platformy Azure i Storm oraz bazy danych HBase na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c571-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="7c571-246">Szablon Hello również utworzenie aplikacji sieci Web platformy Azure i wdraża kopię hello pulpitu nawigacyjnego do niego.</span><span class="sxs-lookup"><span data-stu-id="7c571-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="7c571-247">Sieć wirtualna jest używana, co topologii hello uruchomiona w klastrze Storm hello mogą bezpośrednio komunikować się z hello klastra HBase przy użyciu interfejsu API języka Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="7c571-248">Szablon usługi Resource Manager Hello używane w tym dokumencie znajduje się w publicznym kontenerze obiektów blob w **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="7c571-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="7c571-249">Kliknij przycisk hello toosign przycisk w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7c571-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="7c571-250">Z hello **wdrożenie niestandardowe** wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="7c571-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Parametry HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="7c571-252">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa hello w przypadku klastrów Storm oraz bazy danych HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="7c571-253">Na przykład wprowadzenie **abc** jest tworzony klaster Storm o nazwie **storm abc** i klaster HBase o nazwie **hbase abc**.</span><span class="sxs-lookup"><span data-stu-id="7c571-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="7c571-254">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora hello hello klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="7c571-255">**Hasło logowania klastra**: hello hasła użytkownika administratora w przypadku klastrów Storm oraz bazy danych HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="7c571-256">**Nazwa użytkownika SSH**: hello toocreate użytkownika SSH hello klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="7c571-257">**Hasło SSH**: hello hasło użytkownika SSH hello hello klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="7c571-258">**Lokalizacja**: hello region klastrów hello są tworzone w.</span><span class="sxs-lookup"><span data-stu-id="7c571-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="7c571-259">Kliknij przycisk **OK** toosave hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="7c571-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="7c571-260">Użyj hello **podstawy** sekcji toocreate grupę zasobów lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="7c571-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="7c571-261">W hello **lokalizacja grupy zasobów** menu rozwijanego wybierz hello tej samej lokalizacji, ponieważ wybrane dla hello **lokalizacji** parametru w hello **ustawienia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="7c571-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="7c571-262">Przeczytaj hello warunków i postanowień, a następnie wybierz **zgadzam się toohello warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="7c571-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="7c571-263">Ponadto sprawdź **toodashboard numeru Pin** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="7c571-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="7c571-264">Trwa około 20 minut toocreate hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="7c571-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="7c571-265">Po utworzeniu hello zasobów wyświetlane są informacje o grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Grupa zasobów dla sieci wirtualnej hello i klastrów](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="7c571-267">Zwróć uwagę, że w nazwach hello klastrów HDInsight hello jest **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ hbase**, gdzie nazwę BAZOWĄ jest nazwą hello podane toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c571-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="7c571-268">Użyjesz tych nazw w kolejnym kroku podczas łączenia klastrów toohello.</span><span class="sxs-lookup"><span data-stu-id="7c571-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="7c571-269">Należy pamiętać, że hello nazwę hello pulpitu nawigacyjnego witryny jest również **pulpitu nawigacyjnego nazwę bazową**.</span><span class="sxs-lookup"><span data-stu-id="7c571-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="7c571-270">Ta wartość jest używana w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7c571-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="7c571-271">Skonfiguruj hello bolt pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="7c571-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="7c571-272">toosend danych toohello pulpitu nawigacyjnego wdrożony jako aplikacja sieci web, należy zmodyfikować powitania po wierszu hello `dev.properties`pliku:</span><span class="sxs-lookup"><span data-stu-id="7c571-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="7c571-273">Zmień `http://localhost:3000` zbyt`http://BASENAME-dashboard.azurewebsites.net` i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="7c571-274">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej hello podany w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="7c571-275">Można również użyć grupy zasobów hello utworzone wcześniej tooselect hello pulpitu nawigacyjnego i widoku hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7c571-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="7c571-276">Tworzenie tabeli HBase hello</span><span class="sxs-lookup"><span data-stu-id="7c571-276">Create hello HBase table</span></span>

<span data-ttu-id="7c571-277">toostore danych w bazie danych HBase, należy najpierw utworzymy tabelę.</span><span class="sxs-lookup"><span data-stu-id="7c571-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="7c571-278">Wstępne tworzenie zasobów, które Storm musi toowrite do, jak w trakcie zasobów toocreate z wewnątrz topologii Storm może doprowadzić do wielu wystąpień w trakcie toocreate hello tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7c571-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="7c571-279">Utwórz zasoby hello poza hello topologii i używać systemu Storm do odczytu/zapisu i analiza.</span><span class="sxs-lookup"><span data-stu-id="7c571-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="7c571-280">Użyj SSH tooconnect toohello klastra HBase przy użyciu hello SSH użytkownika i hasło podane toohello szablonu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="7c571-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="7c571-281">Na przykład, jeśli połączenie przy użyciu hello `ssh` polecenia, należy użyć następującej składni hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="7c571-282">Zastąp `sshuser` z nazwą użytkownika SSH hello podane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="7c571-283">Zastąp `clustername` o nazwie klastra HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="7c571-284">W sesji SSH hello Uruchom hello powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="7c571-285">Po załadowaniu hello powłoki, zobacz `hbase(main):001:0>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="7c571-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="7c571-286">Z powłoki HBase hello wprowadź hello następujące polecenia toocreate danych czujnika hello toostore tabeli:</span><span class="sxs-lookup"><span data-stu-id="7c571-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="7c571-287">Sprawdź, czy tabela hello został utworzony za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="7c571-288">To polecenie zwróci informacje toohello podobnie poniższy przykład, wskazując, że istnieją 0 wierszy w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="7c571-289">Wprowadź `exit` tooexit hello powłoki HBase:</span><span class="sxs-lookup"><span data-stu-id="7c571-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="7c571-290">Skonfiguruj hello HBase bolt</span><span class="sxs-lookup"><span data-stu-id="7c571-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="7c571-291">tooHBase toowrite z klastra Storm hello, musisz podać hello HBase bolt hello szczegóły konfiguracji klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="7c571-292">Użyj jednej z hello następujące przykłady tooretrieve hello dozorcy kworum dla klastra HBase:</span><span class="sxs-lookup"><span data-stu-id="7c571-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="7c571-293">Zastąp `your_HDInsight_cluster_name` o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="7c571-294">Aby uzyskać więcej informacji na temat instalowania hello `jq` narzędzie, zobacz [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="7c571-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="7c571-295">Po wyświetleniu monitu wprowadź hasło hello logowania administratora HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="7c571-296">Zastąp "your_HDInsight_cluster_name o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c571-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="7c571-297">Po wyświetleniu monitu wprowadź hasło hello logowania administratora HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="7c571-298">W tym przykładzie wymaga programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c571-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="7c571-299">Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="7c571-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="7c571-300">informacje Hello zwrócone przez te przykłady są podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7c571-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="7c571-301">Te informacje jest używany przez toocommunicate Storm hello klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="7c571-302">Modyfikowanie hello `dev.properties` plik i dodać hello dozorcy kworum informacji toohello po wierszu:</span><span class="sxs-lookup"><span data-stu-id="7c571-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="7c571-303">Tworzenie pakietu i wdrażanie hello tooHDInsight rozwiązania</span><span class="sxs-lookup"><span data-stu-id="7c571-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="7c571-304">W środowisku projektowania Użyj powitania po klaster storm toohello topologii Storm kroki toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="7c571-305">Z hello `TemperatureMonitor` katalogu, użyj następujących hello polecenia tooperform nowej kompilacji i utworzyć pakiet JAR z projektu:</span><span class="sxs-lookup"><span data-stu-id="7c571-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="7c571-306">To polecenie tworzy plik o nazwie `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `docelowego "katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="7c571-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="7c571-307">Użyj scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` i `dev.properties` klaster Storm tooyour plików.</span><span class="sxs-lookup"><span data-stu-id="7c571-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="7c571-308">Poniższy przykład, Zastąp w hello `sshuser` hello użytkownika SSH podana podczas tworzenia klastra hello i `clustername` o nazwie hello klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="7c571-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="7c571-309">Po wyświetleniu monitu wprowadź hasło hello hello użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="7c571-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="7c571-310">Może upłynąć kilka minut tooupload hello plików.</span><span class="sxs-lookup"><span data-stu-id="7c571-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="7c571-311">Aby uzyskać więcej informacji na temat używania hello `scp` i `ssh` poleceń z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="7c571-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="7c571-312">Po przekazaniu pliku hello, Połącz klaster Storm toohello przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="7c571-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7c571-313">Zastąp `sshuser` z nazwą użytkownika SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="7c571-314">Zastąp `clustername` o nazwie klastra Storm hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="7c571-315">toostart hello topologii, użyj następującego polecenia w sesji SSH hello hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="7c571-316">`--remote`przesyła hello topologii toohello Nimbus usługi, która dystrybuuje ją toohello przełożonego węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="7c571-317">`--filter`używa hello `dev.properties` parametry toopopulate plików w definicji topologii hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="7c571-318">`-R /with-hbase.yaml`używa hello `with-hbase.yaml` zawarte w pakiecie hello topologii.</span><span class="sxs-lookup"><span data-stu-id="7c571-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="7c571-319">Po uruchomieniu hello topologii, otwórz toohello przeglądarki witrynę sieci Web została opublikowana na platformie Azure, a następnie użyj hello `node app.js` polecenia toosend danych tooEvent koncentratora.</span><span class="sxs-lookup"><span data-stu-id="7c571-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="7c571-320">Informacje o hello sieci web pulpitu nawigacyjnego aktualizacji toodisplay hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="7c571-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![pulpit nawigacyjny](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="7c571-322">Wyświetlanie danych HBase</span><span class="sxs-lookup"><span data-stu-id="7c571-322">View HBase data</span></span>

<span data-ttu-id="7c571-323">Użyj hello następujące kroki tooconnect tooHBase i sprawdź, czy hello danych zostało zapisanych toohello tabeli:</span><span class="sxs-lookup"><span data-stu-id="7c571-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="7c571-324">Użyj klastra HBase toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="7c571-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7c571-325">Zastąp `sshuser` z nazwą użytkownika SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="7c571-326">Zastąp `clustername` o nazwie klastra HBase hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="7c571-327">W sesji SSH hello Uruchom hello powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="7c571-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="7c571-328">Po załadowaniu hello powłoki, zobacz `hbase(main):001:0>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="7c571-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="7c571-329">Widok wierszy z tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="7c571-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="7c571-330">To polecenie zwraca informacje o podobnych toohello następującego tekstu, wskazujące, że w tabeli hello jest danych.</span><span class="sxs-lookup"><span data-stu-id="7c571-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="7c571-331">Ta operacja skanowania zwraca maksymalnie 10 wierszy z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="7c571-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="7c571-332">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="7c571-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="7c571-333">toodelete hello klastrów, magazynu i aplikacji sieci web w tym samym czasie, Usuń grupę zasobów hello, który je zawiera.</span><span class="sxs-lookup"><span data-stu-id="7c571-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c571-334">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c571-334">Next steps</span></span>

<span data-ttu-id="7c571-335">Aby uzyskać więcej przykładów dotyczących topologii Storm z usługą HDInsight, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="7c571-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="7c571-336">Aby uzyskać więcej informacji na temat systemu Apache Storm, zobacz hello [Apache Storm](https://storm.incubator.apache.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="7c571-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="7c571-337">Aby uzyskać więcej informacji dotyczących bazy danych HBase w usłudze HDInsight, zobacz hello [HBase HDInsight Przegląd](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c571-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="7c571-338">Aby uzyskać więcej informacji o użyciu biblioteki Socket.io, zobacz hello [użyciu biblioteki socket.io](http://socket.io/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="7c571-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="7c571-339">Aby uzyskać więcej informacji o D3.js, zobacz [D3.js — danych na dokumentach](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="7c571-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="7c571-340">Aby uzyskać informacje o tworzeniu topologii w języku Java, zobacz [Java opracowywania topologii Apache STORM w usłudze HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7c571-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="7c571-341">Aby uzyskać informacji o tworzeniu topologii w środowisku .NET, zobacz [topologii opracowywania C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7c571-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
