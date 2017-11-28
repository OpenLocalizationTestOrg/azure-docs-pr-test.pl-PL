---
title: Analizowanie danych czujnika z systemu Apache Storm i bazy danych HBase | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak nawiązać połączenie z siecią wirtualną systemu Apache Storm. Za pomocą Storm HBase do przetwarzania danych czujnika z Centrum zdarzeń i wizualizację go z D3.js."
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
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="d6328-104">Analizowanie danych czujnika z systemu Apache Storm, Centrum zdarzeń i bazy danych HBase w usłudze HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="d6328-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="d6328-105">Dowiedz się, jak używać systemu Apache Storm w usłudze HDInsight do przetwarzania danych czujnika z Centrum zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6328-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="d6328-106">Dane są następnie przechowywane do bazy danych Apache HBase w usłudze HDInsight i wizualizowane za pomocą D3.js.</span><span class="sxs-lookup"><span data-stu-id="d6328-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="d6328-107">Szablon usługi Azure Resource Manager używany w tym dokumencie przedstawia sposób tworzenia wielu zasobów platformy Azure w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6328-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="d6328-108">Szablon tworzy sieci wirtualnej platformy Azure, dwa klastry usługi HDInsight (Storm oraz bazy danych HBase) i aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6328-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="d6328-109">Node.js stosowania pulpit nawigacyjny sieci web w czasie rzeczywistym jest wdrażana automatycznie do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6328-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="d6328-110">Informacje przedstawione w tym dokumencie i przykład, w tym dokumencie wymagają 3,6 wersji usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="d6328-111">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="d6328-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6328-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="d6328-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6328-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6328-113">Prerequisites</span></span>

* <span data-ttu-id="d6328-114">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6328-114">An Azure subscription.</span></span>
* <span data-ttu-id="d6328-115">[Node.js](http://nodejs.org/): używany do podglądu pulpitu nawigacyjnego sieci web lokalnie na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="d6328-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="d6328-116">[Java i JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): stworzono topologii Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="d6328-117">[Maven](http://maven.apache.org/what-is-maven.html): używane do tworzenia i skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="d6328-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="d6328-118">[Git](http://git-scm.com/): używany do pobierania projektu z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6328-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="d6328-119">**SSH** klienta: umożliwia łączenie się z klastrami HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="d6328-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="d6328-120">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d6328-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="d6328-121">Nie trzeba istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="d6328-122">Kroki opisane w tym dokumencie utworzenie następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="d6328-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="d6328-123">Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6328-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="d6328-124">Storm w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="d6328-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="d6328-125">Baza danych HBase w klastrze usługi HDInsight (opartych na systemie Linux dwóch węzłów procesu roboczego)</span><span class="sxs-lookup"><span data-stu-id="d6328-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="d6328-126">Aplikacji sieci Web Azure, który jest hostem sieci web pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="d6328-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="d6328-127">Architektura</span><span class="sxs-lookup"><span data-stu-id="d6328-127">Architecture</span></span>

![diagram architektury](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="d6328-129">W tym przykładzie składa się z następujących składników:</span><span class="sxs-lookup"><span data-stu-id="d6328-129">This example consists of the following components:</span></span>

* <span data-ttu-id="d6328-130">**Usługa Azure Event Hubs**: zawiera dane, które mają być zbierane z czujników.</span><span class="sxs-lookup"><span data-stu-id="d6328-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="d6328-131">**STORM w usłudze HDInsight**: udostępnia w czasie rzeczywistym przetwarzania danych z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="d6328-132">**Baza danych HBase w usłudze HDInsight**: udostępnia trwałym magazynem danych NoSQL dla danych po przetworzeniu przez Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="d6328-133">**Usługi sieci wirtualnej Azure**: umożliwia bezpieczną komunikację między Storm w usłudze HDInsight i bazy danych HBase w usłudze hdinsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d6328-134">Sieć wirtualna jest wymagana podczas korzystania z bazy danych HBase w języku Java klienta interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d6328-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="d6328-135">Nie jest widoczne za pośrednictwem publicznego bramy w przypadku klastrów HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="d6328-136">Instalowanie klastrów HBase i Storm do tej samej sieci wirtualnej umożliwia klastra Storm (lub inne systemy w sieci wirtualnej) bezpośredni dostęp do bazy danych HBase przy użyciu interfejsu API klienta.</span><span class="sxs-lookup"><span data-stu-id="d6328-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="d6328-137">**Witryny sieci Web pulpitu nawigacyjnego**: przykładowy pulpit nawigacyjny, który wykresy danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="d6328-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="d6328-138">Witryna sieci Web jest zaimplementowany w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="d6328-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="d6328-139">[Użyciu biblioteki Socket.IO](http://socket.io/) jest używany w czasie rzeczywistym komunikacji między topologii Storm i witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d6328-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d6328-140">Przy użyciu biblioteki Socket.io komunikacji jest szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="d6328-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="d6328-141">Możesz użyć dowolnej architektury komunikacji, takie jak Websocket raw lub SignalR.</span><span class="sxs-lookup"><span data-stu-id="d6328-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="d6328-142">[D3.js](http://d3js.org/) służy do danych, które są wysyłane do witryny sieci Web programu graph.</span><span class="sxs-lookup"><span data-stu-id="d6328-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6328-143">Dwa klastry są wymagane, ponieważ nie ma żadnych obsługiwana metoda tworzenia jednego klastra usługi HDInsight Storm i bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="d6328-144">Topologia odczytuje dane z Centrum zdarzeń za pomocą [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) klasy i zapisuje dane do bazy danych HBase przy użyciu [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) klasy.</span><span class="sxs-lookup"><span data-stu-id="d6328-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="d6328-145">Komunikacja z witryny sieci Web odbywa się przy użyciu [client.java użyciu biblioteki socket.io](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="d6328-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="d6328-146">Poniższy diagram wyjaśniono układ topologii:</span><span class="sxs-lookup"><span data-stu-id="d6328-146">The following diagram explains the layout of the topology:</span></span>

![diagram topologii](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="d6328-148">Ten diagram jest uproszczona prezentacja topologii.</span><span class="sxs-lookup"><span data-stu-id="d6328-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="d6328-149">Dla każdej partycji w Centrum zdarzeń jest tworzone wystąpienie każdego składnika.</span><span class="sxs-lookup"><span data-stu-id="d6328-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="d6328-150">Te wystąpienia są dystrybuowane między węzłami w klastrze, a dane są przesyłane między nimi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d6328-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="d6328-151">Dane z spout Analizator jest równoważone.</span><span class="sxs-lookup"><span data-stu-id="d6328-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="d6328-152">Dane z analizatora do pulpitu nawigacyjnego i HBase są grupowane według Identyfikatora urządzenia tak, aby komunikaty z tego samego urządzenia zawsze przepływać do tego składnika.</span><span class="sxs-lookup"><span data-stu-id="d6328-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="d6328-153">Składniki topologii</span><span class="sxs-lookup"><span data-stu-id="d6328-153">Topology components</span></span>

* <span data-ttu-id="d6328-154">**Elementów Spout Centrum zdarzeń**: spout jest podana jako część systemu Apache Storm w wersji 0.10.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d6328-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d6328-155">Spout Centrum zdarzeń, w tym przykładzie wymaga platformy Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6.</span><span class="sxs-lookup"><span data-stu-id="d6328-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="d6328-156">**ParserBolt.java**: dane, które są emitowane przez elementy spout są nieprzetworzone dane JSON, a czasami więcej niż jedno zdarzenie jest emitowany naraz.</span><span class="sxs-lookup"><span data-stu-id="d6328-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="d6328-157">Dany element bolt odczytuje dane emitowane przez elementy spout i analizuje komunikat JSON.</span><span class="sxs-lookup"><span data-stu-id="d6328-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="d6328-158">Elementy bolt następnie emituje dane jako spójnej kolekcji, która zawiera wiele pól.</span><span class="sxs-lookup"><span data-stu-id="d6328-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="d6328-159">**DashboardBolt.java**: ten składnik pokazano, jak wysyłać dane w czasie rzeczywistym do pulpitu nawigacyjnego sieci web przy użyciu biblioteki klienta użyciu biblioteki Socket.io dla języka Java.</span><span class="sxs-lookup"><span data-stu-id="d6328-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="d6328-160">**nie hbase.yaml**: definicja topologii używany podczas pracy w trybie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d6328-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="d6328-161">Nie używa składników bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-161">It does not use HBase components.</span></span>
* <span data-ttu-id="d6328-162">**z hbase.yaml**: definicja topologii używana podczas uruchamiania topologii w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d6328-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="d6328-163">Wykorzystuje ona składników bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-163">It does use HBase components.</span></span>
* <span data-ttu-id="d6328-164">**dev.Properties**: informacje o konfiguracji do spout Centrum zdarzeń, HBase bolt i elementów pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6328-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="d6328-165">Przygotowywanie środowiska</span><span class="sxs-lookup"><span data-stu-id="d6328-165">Prepare your environment</span></span>

<span data-ttu-id="d6328-166">Przed skorzystaniem z tego przykładu, należy utworzyć usługi Azure Event Hub, które odczytuje topologii Storm z.</span><span class="sxs-lookup"><span data-stu-id="d6328-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="d6328-167">Konfigurowanie Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d6328-167">Configure Event Hub</span></span>

<span data-ttu-id="d6328-168">Centrum zdarzeń jest źródłem danych, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d6328-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="d6328-169">Wykonaj następujące kroki, aby utworzyć Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="d6328-170">Z [portalu Azure](https://portal.azure.com), wybierz pozycję **+ nowy** -> **Internetu rzeczy** -> **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="d6328-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="d6328-171">W **utworzyć Namespace** sekcji, wykonaj następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d6328-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="d6328-172">Wprowadź **nazwa** dla przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d6328-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="d6328-173">Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="d6328-173">Select a pricing tier.</span></span> <span data-ttu-id="d6328-174">**Podstawowe** jest wystarczająca dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="d6328-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="d6328-175">Wybierz platformy Azure **subskrypcji** do użycia.</span><span class="sxs-lookup"><span data-stu-id="d6328-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="d6328-176">Wybierz istniejącą grupę zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="d6328-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="d6328-177">Wybierz **lokalizacji** do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="d6328-178">Wybierz **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d6328-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="d6328-179">Po zakończeniu procesu tworzenia, zostaną wyświetlone informacje centra zdarzeń, dla przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d6328-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="d6328-180">W tym miejscu, wybierz **+ Dodaj Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="d6328-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="d6328-181">W **tworzenia Centrum zdarzeń** sekcji, wprowadź nazwę **sensordata**, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d6328-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="d6328-182">Pozostaw innych pól na wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="d6328-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="d6328-183">Z widoku centra zdarzeń w przestrzeni nazw, wybierz **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="d6328-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="d6328-184">Wybierz **sensordata** wpisu.</span><span class="sxs-lookup"><span data-stu-id="d6328-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="d6328-185">Wybierz z sensordata Centrum zdarzeń **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="d6328-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="d6328-186">Użyj **+ Dodaj** łącze, aby dodać następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="d6328-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="d6328-187">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="d6328-187">Policy name</span></span> | <span data-ttu-id="d6328-188">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="d6328-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="d6328-189">urządzenia</span><span class="sxs-lookup"><span data-stu-id="d6328-189">devices</span></span> | <span data-ttu-id="d6328-190">Send</span><span class="sxs-lookup"><span data-stu-id="d6328-190">Send</span></span> |
    | <span data-ttu-id="d6328-191">STORM</span><span class="sxs-lookup"><span data-stu-id="d6328-191">storm</span></span> | <span data-ttu-id="d6328-192">Nasłuchiwanie</span><span class="sxs-lookup"><span data-stu-id="d6328-192">Listen</span></span> |

1. <span data-ttu-id="d6328-193">Zaznacz obie zasady i zanotuj **klucz podstawowy** wartość.</span><span class="sxs-lookup"><span data-stu-id="d6328-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="d6328-194">Należy wartość dla obu zasad w przyszłości czynności.</span><span class="sxs-lookup"><span data-stu-id="d6328-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="d6328-195">Pobierz i konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="d6328-195">Download and configure the project</span></span>

<span data-ttu-id="d6328-196">Użyj następującego polecenia można pobrać projektu z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6328-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="d6328-197">Po zakończeniu wykonywania polecenia, należy mieć następującą strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="d6328-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="d6328-198">Ten dokument nie może pełne szczegóły zawarte w tym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="d6328-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="d6328-199">Jednak kod jest całkowicie oznaczone jako.</span><span class="sxs-lookup"><span data-stu-id="d6328-199">However, the code is fully commented.</span></span>

<span data-ttu-id="d6328-200">Aby skonfigurować projekt, aby odczytać z Centrum zdarzeń, otwórz `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` pliku i Dodaj informacje Centrum zdarzeń do następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="d6328-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="d6328-201">Kompilowanie i testowanie lokalnie</span><span class="sxs-lookup"><span data-stu-id="d6328-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6328-202">Lokalnie przy użyciu topologii wymaga działającego środowiska deweloperskiego Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="d6328-203">Aby uzyskać więcej informacji, zobacz [Konfigurowanie środowiska projektowego Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) w serwisie Apache.org.</span><span class="sxs-lookup"><span data-stu-id="d6328-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="d6328-204">Jeśli używasz środowiska projektowego systemu Windows może zostać wyświetlony `java.io.IOException` podczas uruchamiania topologii lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d6328-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="d6328-205">Jeśli tak, przejść do uruchamiania topologii w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="d6328-206">Przed przeprowadzeniem jej testów, należy uruchomić Pulpit nawigacyjny, aby wyświetlić dane wyjściowe topologii i generować dane mają być przechowywane w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6328-207">Składnik HBase Ta topologia nie jest aktywne, podczas testowania lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d6328-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="d6328-208">Interfejsu API języka Java klastra HBase nie jako dostępne spoza sieci wirtualnej Azure, która zawiera klastrów.</span><span class="sxs-lookup"><span data-stu-id="d6328-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="d6328-209">Uruchom aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="d6328-209">Start the web application</span></span>

1. <span data-ttu-id="d6328-210">Otwórz wiersz polecenia i przejdź do `hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="d6328-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="d6328-211">Aby zainstalować zależności wymagane przez aplikację sieci web, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="d6328-212">Aby uruchomić aplikację sieci web, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="d6328-213">Zobaczysz komunikat podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="d6328-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="d6328-214">Otwórz przeglądarkę sieci web, a następnie wprowadź `http://localhost:3000/` jako adres.</span><span class="sxs-lookup"><span data-stu-id="d6328-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="d6328-215">Wyświetlane są stronę podobną do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="d6328-215">A page similar to the following image is displayed:</span></span>
   
    ![pulpit nawigacyjny sieci Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="d6328-217">Ten wiersz polecenia pozostaw otwarte.</span><span class="sxs-lookup"><span data-stu-id="d6328-217">Leave this command prompt open.</span></span> <span data-ttu-id="d6328-218">Po zakończeniu testowania, użyj klawiszy Ctrl-C, aby zatrzymać serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6328-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="d6328-219">Generowanie danych</span><span class="sxs-lookup"><span data-stu-id="d6328-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="d6328-220">Kroki opisane w tej sekcji użycia środowiska Node.js, dzięki czemu mogą być używane na dowolnej platformie.</span><span class="sxs-lookup"><span data-stu-id="d6328-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="d6328-221">Inne przykłady języka można znaleźć `SendEvents` katalogu.</span><span class="sxs-lookup"><span data-stu-id="d6328-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="d6328-222">Otwórz nowy wiersz, powłokę lub terminalu i przejdź do `hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="d6328-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="d6328-223">Aby zainstalować zależności wymagane przez aplikację, należy użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="d6328-224">Otwórz `app.js` plik w edytorze tekstów i Dodaj informacje o Centrum zdarzeń uzyskanymi wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d6328-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="d6328-225">W tym przykładzie przyjęto założenie, że użyto `sensordata` jako nazwy Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="d6328-226">Oraz że `devices` jako nazwę zasady, która ma `Send` oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="d6328-227">Użyj następującego polecenia, aby wstawić nowe wpisy w Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="d6328-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="d6328-228">Pojawić kilka wierszy danych wyjściowych, które zawierają dane wysyłane do Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="d6328-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
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

### <a name="build-and-start-the-topology"></a><span data-ttu-id="d6328-229">Skompilować i uruchomić topologii</span><span class="sxs-lookup"><span data-stu-id="d6328-229">Build and start the topology</span></span>

1. <span data-ttu-id="d6328-230">Otwórz nowy wiersz polecenia i przejdź do `hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="d6328-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="d6328-231">Aby skompilować i pakiet topologii, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="d6328-232">Aby uruchomić topologii w trybie lokalnym, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="d6328-233">`--local`Topologia jest uruchamiany w trybie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d6328-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="d6328-234">`--filter`używa `dev.properties` plik, aby wypełnić parametrów w definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="d6328-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="d6328-235">`resources/no-hbase.yaml`używa `no-hbase.yaml` definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="d6328-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="d6328-236">Po rozpoczęciu topologii odczytuje wpisów z Centrum zdarzeń, a następnie wysyła je do pulpitu nawigacyjnego na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d6328-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="d6328-237">Powinny pojawić się wiersze są wyświetlane na pulpicie nawigacyjnym w sieci web, podobnie do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="d6328-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![pulpit nawigacyjny z danymi](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="d6328-239">Pulpit nawigacyjny jest uruchomiona, użyj `node app.js` polecenie poprzednie kroki, aby wysłać nowe dane do usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6328-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="d6328-240">Ponieważ wartości temperatury są losowo generowany, wykres należy zaktualizować pokazanie dużych zmian w temperatury.</span><span class="sxs-lookup"><span data-stu-id="d6328-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6328-241">Musi być w **hdinsight-eventhub — przykład/SendEvents/Nodejs** katalogu, korzystając z `node app.js` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d6328-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="d6328-242">Po zweryfikowaniu, że aktualizacje pulpitu nawigacyjnego, Zatrzymaj topologię za pomocą klawiszy Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="d6328-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="d6328-243">Ctrl + C umożliwia także zatrzymać serwer lokalnej sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6328-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="d6328-244">Tworzenie klastra Storm oraz bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="d6328-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="d6328-245">Kroki opisane w tej sekcji Użyj [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) do utworzenia klastra sieci wirtualnej platformy Azure i Storm oraz bazy danych HBase w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d6328-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="d6328-246">Szablon także tworzy aplikacji sieci Web platformy Azure i wdraża kopię pulpitu nawigacyjnego do niego.</span><span class="sxs-lookup"><span data-stu-id="d6328-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="d6328-247">Sieć wirtualna jest używana, co topologii uruchomionych na klaster Storm może komunikować się bezpośrednio z klastra HBase przy użyciu interfejsu API języka Java HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="d6328-248">Szablon usługi Resource Manager używany w tym dokumencie znajduje się w publicznym kontenerze obiektów blob w **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="d6328-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="d6328-249">Kliknij poniższy przycisk, aby zalogować się do platformy Azure i otwórz szablon usługi Resource Manager w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6328-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="d6328-250">Z **wdrożenie niestandardowe** sekcji, wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="d6328-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![Parametry HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="d6328-252">**Podstawowa nazwa klastra**: Ta wartość jest używana jako nazwa podstawowa dla Storm oraz klastrów HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="d6328-253">Na przykład wprowadzenie **abc** jest tworzony klaster Storm o nazwie **storm abc** i klaster HBase o nazwie **hbase abc**.</span><span class="sxs-lookup"><span data-stu-id="d6328-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="d6328-254">**Nazwa użytkownika logowania klastra**: nazwa użytkownika administratora w przypadku klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="d6328-255">**Hasło logowania klastra**: hasła użytkownika administratora w przypadku klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="d6328-256">**Nazwa użytkownika SSH**: użytkownika SSH do tworzenia klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="d6328-257">**Hasło SSH**: hasło dla użytkownika SSH w przypadku klastrów Storm oraz bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="d6328-258">**Lokalizacja**: utworzony klastrów w regionie.</span><span class="sxs-lookup"><span data-stu-id="d6328-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="d6328-259">Kliknij przycisk **OK**, aby zapisać parametry.</span><span class="sxs-lookup"><span data-stu-id="d6328-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="d6328-260">Użyj **podstawy** sekcji, aby utworzyć grupę zasobów lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="d6328-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="d6328-261">W **lokalizacja grupy zasobów** listy rozwijanej wybierz polecenie tej samej lokalizacji co zostanie wybrany do **lokalizacji** parametru w **ustawienia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6328-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="d6328-262">Przeczytaj warunki i postanowienia, a następnie wybierz **akceptuję warunki i postanowienia, o których wspomniano**.</span><span class="sxs-lookup"><span data-stu-id="d6328-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="d6328-263">Ponadto sprawdź **Przypnij do pulpitu nawigacyjnego** , a następnie wybierz **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="d6328-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="d6328-264">Tworzenie klastrów trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="d6328-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="d6328-265">Po utworzeniu zasobów wyświetlane są informacje o grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6328-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![Grupa zasobów dla sieci wirtualnej i klastrów](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="d6328-267">Należy zauważyć, że nazwy klastrów usługi HDInsight są **nazwę BAZOWĄ storm** i **nazwę BAZOWĄ hbase**, gdzie nazwę BAZOWĄ jest podana nazwa do szablonu.</span><span class="sxs-lookup"><span data-stu-id="d6328-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="d6328-268">Te nazwy można użyć w kolejnym kroku, podczas nawiązywania połączenia z klastrów.</span><span class="sxs-lookup"><span data-stu-id="d6328-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="d6328-269">Należy również zauważyć, że nazwa witryny pulpitu nawigacyjnego **pulpitu nawigacyjnego nazwę bazową**.</span><span class="sxs-lookup"><span data-stu-id="d6328-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="d6328-270">Ta wartość jest używana w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6328-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="d6328-271">Skonfiguruj bolt pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="d6328-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="d6328-272">Aby wysyłać dane do pulpitu nawigacyjnego wdrożony jako aplikacja sieci web, należy zmodyfikować następujący wiersz w `dev.properties`pliku:</span><span class="sxs-lookup"><span data-stu-id="d6328-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="d6328-273">Zmień `http://localhost:3000` do `http://BASENAME-dashboard.azurewebsites.net` i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="d6328-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="d6328-274">Zastąp **nazwę BAZOWĄ** o nazwie podstawowej podany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="d6328-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="d6328-275">Umożliwia także grupy zasobów utworzone wcześniej, aby wybrać pulpitu nawigacyjnego i wyświetlić adres URL.</span><span class="sxs-lookup"><span data-stu-id="d6328-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="d6328-276">Tworzenie tabeli HBase</span><span class="sxs-lookup"><span data-stu-id="d6328-276">Create the HBase table</span></span>

<span data-ttu-id="d6328-277">Aby przechowywać dane w bazie danych HBase, możemy utworzyć tabelę.</span><span class="sxs-lookup"><span data-stu-id="d6328-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="d6328-278">Wstępne tworzenie zasobów, które wymaga Storm do zapisu, jako próby utworzenia zasobów z wewnątrz platformy Storm topologii może spowodować wiele wystąpień w trakcie tworzenia tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d6328-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="d6328-279">Tworzenie zasobów spoza topologii i używać systemu Storm do odczytu/zapisu i analiz.</span><span class="sxs-lookup"><span data-stu-id="d6328-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="d6328-280">Używanie protokołu SSH do nawiązania połączenia klastra HBase przy użyciu protokołu SSH użytkownika i hasło do szablonu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d6328-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="d6328-281">Na przykład, jeśli połączenie przy użyciu `ssh` polecenia, należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="d6328-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="d6328-282">Zastąp `sshuser` przy użyciu nazwy użytkownika SSH podana podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d6328-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="d6328-283">Zastąp `clustername` z nazwą klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="d6328-284">W sesji SSH należy uruchomić powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="d6328-285">Po załadowaniu powłoki, zobacz `hbase(main):001:0>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="d6328-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="d6328-286">Z poziomu powłoki HBase wprowadź następujące polecenie, aby utworzyć tabelę do przechowywania danych czujników:</span><span class="sxs-lookup"><span data-stu-id="d6328-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="d6328-287">Sprawdź, czy tabela została utworzona za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6328-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="d6328-288">To polecenie zwróci informacje podobne do poniższego przykładu, wskazującą, czy 0 wierszy w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6328-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="d6328-289">Wprowadź `exit` do Wyjdź z powłoki HBase:</span><span class="sxs-lookup"><span data-stu-id="d6328-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="d6328-290">Skonfiguruj HBase bolt</span><span class="sxs-lookup"><span data-stu-id="d6328-290">Configure the HBase bolt</span></span>

<span data-ttu-id="d6328-291">Można zapisać do bazy danych HBase z klastra Storm, należy podać szczegóły konfiguracji klastra HBase HBase bolt.</span><span class="sxs-lookup"><span data-stu-id="d6328-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="d6328-292">Aby pobrać dozorcy kworum dla klastra HBase, użyj jednej z poniższych przykładach:</span><span class="sxs-lookup"><span data-stu-id="d6328-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="d6328-293">Element `your_HDInsight_cluster_name` należy zastąpić nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="d6328-294">Aby uzyskać więcej informacji na temat instalowania `jq` narzędzie, zobacz [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="d6328-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="d6328-295">Po wyświetleniu monitu wprowadź hasło dla nazwy logowania administratora usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="d6328-296">Zastąp "your_HDInsight_cluster_name o nazwie z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="d6328-297">Po wyświetleniu monitu wprowadź hasło dla nazwy logowania administratora usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6328-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="d6328-298">W tym przykładzie wymaga programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6328-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="d6328-299">Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [wprowadzenie do programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="d6328-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="d6328-300">Informacje zwracane przez te przykłady jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="d6328-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="d6328-301">Te informacje są używane przez Storm do komunikowania się z klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="d6328-302">Modyfikowanie `dev.properties` plik i dodać informacje kworum dozorcy do następującego:</span><span class="sxs-lookup"><span data-stu-id="d6328-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="d6328-303">Tworzenie pakietu i wdrożenia rozwiązania w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6328-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="d6328-304">W środowisku projektowania wykonaj następujące kroki do wdrożenia topologii Storm do klastra storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="d6328-305">Z `TemperatureMonitor` katalogu, użyj następujące polecenie, aby wykonać nową kompilację i utworzyć JAR pakietu z projektu:</span><span class="sxs-lookup"><span data-stu-id="d6328-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="d6328-306">To polecenie tworzy plik o nazwie `TemperatureMonitor-1.0-SNAPSHOT.jar in the `docelowego "katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="d6328-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="d6328-307">Użyj połączenia usługi, aby przekazać `TemperatureMonitor-1.0-SNAPSHOT.jar` i `dev.properties` pliki do klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="d6328-308">W poniższym przykładzie Zastąp `sshuser` użytkownika SSH podana podczas tworzenia klastra, i `clustername` o nazwie klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="d6328-309">Po wyświetleniu monitu wprowadź hasło dla użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="d6328-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="d6328-310">Może upłynąć kilka minut, aby przekazać pliki.</span><span class="sxs-lookup"><span data-stu-id="d6328-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="d6328-311">Aby uzyskać więcej informacji na temat używania `scp` i `ssh` poleceń z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d6328-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="d6328-312">Po przekazaniu pliku nawiązać połączenia z klastrem Storm przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="d6328-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d6328-313">Zastąp `sshuser` przy użyciu nazwy użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="d6328-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="d6328-314">Zastąp `clustername` z nazwą klastra Storm.</span><span class="sxs-lookup"><span data-stu-id="d6328-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="d6328-315">Aby uruchomić topologii, użyj następującego polecenia w sesji SSH:</span><span class="sxs-lookup"><span data-stu-id="d6328-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="d6328-316">`--remote`przesyła topologii z usługą Nimbus, której przesłanie go do przełożonego węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d6328-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="d6328-317">`--filter`używa `dev.properties` plik, aby wypełnić parametrów w definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="d6328-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="d6328-318">`-R /with-hbase.yaml`używa `with-hbase.yaml` topologii uwzględniony w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d6328-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="d6328-319">Po uruchomieniu topologii, otwórz przeglądarkę Aby witryna sieci Web została opublikowana na platformie Azure, a następnie użyj `node app.js` polecenie, aby wysyłać dane do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d6328-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="d6328-320">Powinien zostać wyświetlony pulpit nawigacyjny sieci web, zaktualizować, aby wyświetlić informacje.</span><span class="sxs-lookup"><span data-stu-id="d6328-320">You should see the web dashboard update to display the information.</span></span>
   
    ![pulpit nawigacyjny](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="d6328-322">Wyświetlanie danych HBase</span><span class="sxs-lookup"><span data-stu-id="d6328-322">View HBase data</span></span>

<span data-ttu-id="d6328-323">Aby podłączyć się do bazy danych HBase i sprawdź, czy dane zostały zapisane w tabeli, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d6328-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="d6328-324">Używanie protokołu SSH do nawiązania połączenia klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d6328-325">Zastąp `sshuser` przy użyciu nazwy użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="d6328-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="d6328-326">Zastąp `clustername` z nazwą klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="d6328-327">W sesji SSH należy uruchomić powłoki HBase.</span><span class="sxs-lookup"><span data-stu-id="d6328-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="d6328-328">Po załadowaniu powłoki, zobacz `hbase(main):001:0>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="d6328-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="d6328-329">Widok wierszy z tabeli:</span><span class="sxs-lookup"><span data-stu-id="d6328-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="d6328-330">To polecenie zwraca informacje podobne do następującego, co oznacza, że istnieje danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6328-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
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
   > <span data-ttu-id="d6328-331">Ta operacja skanowania zwraca maksymalnie 10 wierszy z tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6328-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="d6328-332">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="d6328-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d6328-333">Aby usunąć klastrów, magazynu i aplikacji sieci web w tym samym czasie, Usuń grupę zasobów, który je zawiera.</span><span class="sxs-lookup"><span data-stu-id="d6328-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6328-334">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6328-334">Next steps</span></span>

<span data-ttu-id="d6328-335">Aby uzyskać więcej przykładów dotyczących topologii Storm z usługą HDInsight, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="d6328-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="d6328-336">Aby uzyskać więcej informacji na temat systemu Apache Storm, zobacz [Apache Storm](https://storm.incubator.apache.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="d6328-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="d6328-337">Aby uzyskać więcej informacji dotyczących bazy danych HBase w usłudze HDInsight, zobacz [HBase HDInsight Przegląd](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6328-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="d6328-338">Aby uzyskać więcej informacji o użyciu biblioteki Socket.io, zobacz [użyciu biblioteki socket.io](http://socket.io/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="d6328-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="d6328-339">Aby uzyskać więcej informacji o D3.js, zobacz [D3.js — danych na dokumentach](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="d6328-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="d6328-340">Aby uzyskać informacje o tworzeniu topologii w języku Java, zobacz [Java opracowywania topologii Apache STORM w usłudze HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d6328-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="d6328-341">Aby uzyskać informacji o tworzeniu topologii w środowisku .NET, zobacz [topologii opracowywania C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d6328-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
