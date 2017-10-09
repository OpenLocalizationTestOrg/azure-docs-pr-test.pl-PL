---
title: "aaaUse Apache Spark przesyłania strumieniowego z usługą Event Hubs w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Tworzenie przykładowej przesyłania strumieniowego Apache Spark w sposób toosend danych strumienia tooAzure Centrum zdarzeń, a następnie odbierają te zdarzenia w klastrze Spark w usłudze HDInsight przy użyciu języka scala aplikacji."
keywords: "Apache spark przesyłania strumieniowego przesyłania strumieniowego spark, przykładowe spark, apache spark przesyłania strumieniowego, np. przykładowych azure Centrum zdarzeń, spark próbki"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="9b094-104">Platforma Apache Spark przesyłania strumieniowego: klastra przetwarzania danych z usługi Azure Event Hubs z platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="9b094-105">W tym artykule możesz tworzyć Apache Spark przesyłania strumieniowego próbki, która obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9b094-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="9b094-106">Korzystając z komunikatów tooingest autonomicznej aplikacji do usługi Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="9b094-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="9b094-107">Z dwa różne podejścia możesz pobrać wiadomości powitania z Centrum zdarzeń w czasie rzeczywistym za pomocą aplikacji uruchomionej w klastrze Spark w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b094-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="9b094-108">Tworzenie potoków analitycznych przesyłania strumieniowego systemów magazynowania toodifferent danych toopersist lub uzyskiwanie szczegółowych informacji z danych na bieżąco hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b094-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b094-109">Prerequisites</span></span>

* <span data-ttu-id="9b094-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b094-110">An Azure subscription.</span></span> <span data-ttu-id="9b094-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9b094-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="9b094-112">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b094-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9b094-113">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="9b094-114">Przesyłanie strumieniowe Spark pojęcia</span><span class="sxs-lookup"><span data-stu-id="9b094-114">Spark Streaming concepts</span></span>

<span data-ttu-id="9b094-115">Aby uzyskać szczegółowy opis przesyłania strumieniowego Spark, zobacz [Apache Spark przesyłania strumieniowego omówienie](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="9b094-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="9b094-116">HDInsight oferuje hello tooa tej samej funkcji przesyłania strumieniowego Spark klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9b094-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="9b094-117">Do czego służy to rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="9b094-117">What does this solution do?</span></span>

<span data-ttu-id="9b094-118">W tym artykule przedstawiono przykład przesyłania strumieniowego Spark toocreate wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9b094-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="9b094-119">Tworzenie usługi Azure Event Hub, który będzie otrzymywał strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9b094-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="9b094-120">Uruchom aplikacja autonomiczna lokalnego, który generuje zdarzenia i wypchnięcia jej toohello Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="9b094-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="9b094-121">Witaj przykładowej aplikacji, w tym jest opublikowana w [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="9b094-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="9b094-122">Zdalne uruchamianie przesyłania strumieniowego aplikacji w klastrze Spark, które odczytuje wydarzeń transmisji strumieniowej z Azure Centrum zdarzeń i przeprowadzania różnych przetwarzania danych/analizy.</span><span class="sxs-lookup"><span data-stu-id="9b094-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="9b094-123">Tworzenie Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9b094-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="9b094-124">Zaloguj się na toohello [Azure Portal](https://ms.portal.azure.com)i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="9b094-125">Kliknij pozycję **Internet rzeczy**, a następnie kliknij pozycję **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="9b094-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="9b094-126">![Tworzenie Centrum zdarzeń do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "tworzenia Centrum zdarzeń do przesyłania strumieniowego przykład Spark")</span><span class="sxs-lookup"><span data-stu-id="9b094-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="9b094-127">W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="9b094-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="9b094-128">Wybierz hello cenowym (Basic lub Standard).</span><span class="sxs-lookup"><span data-stu-id="9b094-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="9b094-129">Ponadto Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w zasobów hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9b094-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="9b094-130">Kliknij przycisk **Utwórz** toocreate hello w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="9b094-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="9b094-131">![Podaj nazwę Centrum zdarzeń przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Podaj nazwę Centrum zdarzeń przesyłania strumieniowego przykład Spark")</span><span class="sxs-lookup"><span data-stu-id="9b094-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b094-132">Użytkownik powinien wybierz hello takie same **lokalizacji** jako klastra Apache Spark w HDInsight tooreduce opóźnienia i koszty.</span><span class="sxs-lookup"><span data-stu-id="9b094-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="9b094-133">Hello centra zdarzeń w przestrzeni nazw kliknij na liście hello nowo utworzonego w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="9b094-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="9b094-134">W bloku przestrzeni nazw hello, kliknij **usługi Event Hubs**, a następnie kliknij przycisk **+ Centrum zdarzeń** toocreate z nowym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9b094-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="9b094-135">![Tworzenie Centrum zdarzeń do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "tworzenia Centrum zdarzeń do przesyłania strumieniowego przykład Spark")</span><span class="sxs-lookup"><span data-stu-id="9b094-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="9b094-136">Wpisz nazwę Centrum zdarzeń, too10 liczba partycji hello zestawu i too1 przechowywania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="9b094-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="9b094-137">Firma Microsoft nie są archiwizacji z wiadomości powitania w tym rozwiązaniu, pozostaw rest hello jako domyślne, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b094-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="9b094-138">![Podaj szczegóły zdarzenia koncentratora do przesyłania strumieniowego przykład Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "podanie szczegółów Centrum zdarzeń przesyłania strumieniowego przykład Spark")</span><span class="sxs-lookup"><span data-stu-id="9b094-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="9b094-139">nowo utworzone Centrum zdarzeń Hello znajduje się w bloku Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="9b094-140">![Wyświetlanie Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Widok Centrum zdarzeń dla hello Spark przykład przesyłania strumieniowego")</span><span class="sxs-lookup"><span data-stu-id="9b094-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="9b094-141">W bloku przestrzeni nazw hello (nie hello określonym Centrum zdarzeń blok), kliknij **zasady dostępu współużytkowanego**, a następnie kliknij przycisk **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="9b094-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="9b094-142">![Ustawianie zasad Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Centrum zdarzeń ustawić zasady dla hello Spark przykład przesyłania strumieniowego")</span><span class="sxs-lookup"><span data-stu-id="9b094-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="9b094-143">Kliknij przycisk hello toocopy przycisku Kopiuj hello **RootManageSharedAccessKey** głównej Schowka o toohello ciąg połączenia i klucza.</span><span class="sxs-lookup"><span data-stu-id="9b094-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="9b094-144">Zapisz te toouse później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="9b094-145">![Wyświetlanie kluczy zasad Centrum zdarzeń, na przykład przesyłania strumieniowego Spark hello](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "klucze zasad Centrum zdarzeń widoku hello Spark przykład przesyłania strumieniowego")</span><span class="sxs-lookup"><span data-stu-id="9b094-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="9b094-146">Wysyłanie wiadomości tooAzure Centrum zdarzeń przy użyciu języka Scala przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b094-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="9b094-147">W tej sekcji użyjesz lokalnego Scala aplikacja autonomiczna, który generuje strumienia zdarzeń i wysyła je z tooAzure Centrum zdarzeń, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9b094-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="9b094-148">Ta aplikacja jest dostępna w witrynie GitHub pod [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="9b094-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="9b094-149">w tym miejscu w krokach Hello założono, ma to repozytorium GitHub już rozwidlone.</span><span class="sxs-lookup"><span data-stu-id="9b094-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="9b094-150">Upewnij się, że masz następujące hello zainstalowany na komputerze hello gdzie uruchomić tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="9b094-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="9b094-151">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="9b094-151">Oracle Java Development kit.</span></span> <span data-ttu-id="9b094-152">Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="9b094-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="9b094-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="9b094-153">Apache Maven.</span></span> <span data-ttu-id="9b094-154">Możesz pobrać go z [tutaj](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="9b094-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="9b094-155">Dostępne są instrukcje tooinstall Maven [tutaj](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="9b094-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="9b094-156">Otwórz wiersz polecenia i przejdź do lokalizacji toohello sklonować repozytorium GitHub hello hello przykładowej Scala aplikacji i uruchom następujące polecenie toobuild hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="9b094-157">Hello jar dane wyjściowe aplikacji hello **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, utworzony na podstawie **/target** katalogu.</span><span class="sxs-lookup"><span data-stu-id="9b094-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="9b094-158">Możesz użyć tego JAR w dalszej części tego artykułu tootest hello kompletnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9b094-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="9b094-159">Utwórz komunikatów tooreceive aplikacji z Centrum zdarzeń do klastra Spark</span><span class="sxs-lookup"><span data-stu-id="9b094-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="9b094-160">Mamy dwa tooconnect metod przesyłania strumieniowego Spark i usługi Azure Event Hubs, połączenie oparte na odbiorcy i oparte na DStream bezpośrednie połączenie.</span><span class="sxs-lookup"><span data-stu-id="9b094-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="9b094-161">Na podstawie DStream bezpośrednio wprowadzono na stycznia 2017 w wersji hello 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="9b094-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="9b094-162">Ma tooreplace hello oryginalnego odbiornika połączenia jako jest więcej wydajności i wydajne zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b094-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="9b094-163">Znaleziono więcej szczegółów w [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="9b094-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="9b094-164">Bezpośrednie DStream obsługuje tylko Spark 2.0 +.</span><span class="sxs-lookup"><span data-stu-id="9b094-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="9b094-165">Tworzenie aplikacji hello zależności toospark eventhubs łącznik</span><span class="sxs-lookup"><span data-stu-id="9b094-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="9b094-166">Firma Microsoft opublikuje również hello przemieszczania wersji Spark-EventHubs w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b094-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="9b094-167">toouse hello przemieszczania Spark EventHubs, pierwszym krokiem hello jest wersja tooindicate GitHub zgodnie z hello źródło repozytorium, dodając powitania po toopom.xml wpis:</span><span class="sxs-lookup"><span data-stu-id="9b094-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="9b094-168">Następnie można dodać następujące zależności tooyour projektu tootake hello wersji wstępnej, hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="9b094-169">Zależność narzędzia maven</span><span class="sxs-lookup"><span data-stu-id="9b094-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="9b094-170">Zależności SBT</span><span class="sxs-lookup"><span data-stu-id="9b094-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="9b094-171">Bezpośrednie połączenie DStream</span><span class="sxs-lookup"><span data-stu-id="9b094-171">Direct DStream Connection</span></span>

<span data-ttu-id="9b094-172">Można pobrać plik jar wbudowanych zawierający przykłady użycia bezpośredniego DStream w [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="9b094-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="9b094-173">Plik jar Hello zawiera trzy przykłady, których kodu źródłowego są dostępne pod adresem [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="9b094-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="9b094-174">Biorąc [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) na przykład:</span><span class="sxs-lookup"><span data-stu-id="9b094-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="9b094-175">W hello powyżej przykład `eventhubParameters` są hello parametrów określonych tooa EventHubs SIS i że masz toopass on toohello `createDirectStreams` interfejs API, który konstruuje przestrzeni nazw usługi Event Hubs tooa mapowania obiektu DStream bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="9b094-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="9b094-176">Za pośrednictwem obiektu DStream bezpośredniego hello należy wywołać wszystkich API DStream dostarczonych przez strukturę interfejsu API platformy Spark przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9b094-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="9b094-177">W tym przykładzie mamy obliczania częstotliwość hello każdego wyrazu w odstępach czasu hello ostatniej partii micro 3.</span><span class="sxs-lookup"><span data-stu-id="9b094-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="9b094-178">Odbiornik połączenia</span><span class="sxs-lookup"><span data-stu-id="9b094-178">Receiver-based Connection</span></span>

<span data-ttu-id="9b094-179">Spark, przesyłanie strumieniowe przykładowej aplikacji napisanych w języku Scala, który odbiera zdarzenia i miejsc docelowych toodifferent hello trasy, znajduje się w temacie [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="9b094-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="9b094-180">Wykonaj kroki hello poniżej aplikacji hello tooupdate dla danej konfiguracji Centrum zdarzeń i Utwórz hello jar danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9b094-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="9b094-181">Uruchom IntelliJ IDEA i z hello uruchomić ekranu wybierz **wyewidencjonowania z kontroli wersji** , a następnie kliknij przycisk **Git**.</span><span class="sxs-lookup"><span data-stu-id="9b094-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="9b094-182">![Apache Spark przesyłania strumieniowego przykład — Pobierz źródła z repozytorium Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark przesyłania strumieniowego przykład — Pobierz źródła z repozytorium Git")</span><span class="sxs-lookup"><span data-stu-id="9b094-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="9b094-183">W hello **klonowania repozytorium** okno dialogowe, podaj hello tooclone repozytorium Git toohello adres URL z, określ hello tooclone katalogu do, a następnie kliknij **klonowania**.</span><span class="sxs-lookup"><span data-stu-id="9b094-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="9b094-184">![Apache Spark przesyłania strumieniowego przykład — klonować z Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark przesyłania strumieniowego przykład — klonować z Git")</span><span class="sxs-lookup"><span data-stu-id="9b094-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="9b094-185">Wykonaj monity hello dopóki projektu hello jest całkowicie sklonować.</span><span class="sxs-lookup"><span data-stu-id="9b094-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="9b094-186">Naciśnij klawisz **Alt + 1** tooopen hello **widoku projektu**.</span><span class="sxs-lookup"><span data-stu-id="9b094-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="9b094-187">Powinien on przypominać następujące hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="9b094-188">![Apache Spark przesyłania strumieniowego przykład — widok projektu](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark przesyłania strumieniowego przykład — widok projektu")</span><span class="sxs-lookup"><span data-stu-id="9b094-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="9b094-189">Upewnij się, że kod aplikacji hello jest skompilowana przy użyciu Java8.</span><span class="sxs-lookup"><span data-stu-id="9b094-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="9b094-190">tooensure tego, kliknij **pliku**, kliknij przycisk **struktury projektu**, a na powitania **projektu** karcie, upewnij się, że ustawiono zbyt poziomie język projektu**8 - wyrażeń lambda, typ adnotacje, itp.**.</span><span class="sxs-lookup"><span data-stu-id="9b094-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="9b094-191">![Apache Spark przesyłania strumieniowego przykład — zestaw kompilatora](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark przesyłania strumieniowego przykład — zestaw kompilatora")</span><span class="sxs-lookup"><span data-stu-id="9b094-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="9b094-192">Otwórz hello **pom.xml** i upewnij się, że wersja Spark hello jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="9b094-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="9b094-193">W obszarze `<properties>` węzła, Znajdź powitania po fragment i zweryfikować hello Spark wersji.</span><span class="sxs-lookup"><span data-stu-id="9b094-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="9b094-194">Aplikacja Hello wymaga jar zależności, nazywany **jar sterownik JDBC**.</span><span class="sxs-lookup"><span data-stu-id="9b094-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="9b094-195">Jest to wymagane toowrite wiadomości powitania odebranych z Centrum zdarzeń do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b094-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="9b094-196">Możesz pobrać ten jar (4.1 lub nowszym) z [tutaj](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b094-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="9b094-197">Dodaj odwołanie toothis jar hello biblioteki projektu.</span><span class="sxs-lookup"><span data-stu-id="9b094-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="9b094-198">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="9b094-199">Z którym masz aplikacji hello, Otwórz okno IntelliJ IDEA, kliknij przycisk **pliku**, kliknij przycisk **struktury projektu**, a następnie kliknij przycisk **biblioteki**.</span><span class="sxs-lookup"><span data-stu-id="9b094-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="9b094-200">Kliknij hello dodać ikonę (![dodać ikonę](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), kliknij przycisk **Java**, a następnie przejdź toohello której pobrano jar sterownik JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="9b094-201">Wykonaj hello monity tooadd hello jar pliku toohello projektu biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9b094-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="9b094-202">![Dodaj brakujące zależności](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Dodaj brakujące słoików zależności")</span><span class="sxs-lookup"><span data-stu-id="9b094-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="9b094-203">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="9b094-203">Click **Apply**.</span></span>

7. <span data-ttu-id="9b094-204">Utwórz plik jar hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9b094-204">Create hello output jar file.</span></span> <span data-ttu-id="9b094-205">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="9b094-206">W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** a następnie kliknij przycisk hello oraz symboli.</span><span class="sxs-lookup"><span data-stu-id="9b094-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="9b094-207">Na powitania wyskakującym oknie dialogowym kliknij pozycję **JAR**, a następnie kliknij przycisk **z modułów z zależnościami**.</span><span class="sxs-lookup"><span data-stu-id="9b094-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="9b094-208">![Przykład strumieniowych Apache Spark — tworzenie JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "przykład strumieniowych Apache Spark — tworzenie JAR")</span><span class="sxs-lookup"><span data-stu-id="9b094-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="9b094-209">W hello **utworzyć JAR z modułów** okna dialogowego, kliknij przycisk wielokropka hello (![wielokropka](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) przed hello **klasy głównym**.</span><span class="sxs-lookup"><span data-stu-id="9b094-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="9b094-210">W hello **Wybierz klasy głównym** okno dialogowe, wybierz jedno z dostępnych klas hello a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b094-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="9b094-211">![Apache Spark przesyłania strumieniowego przykład — wybierz klasę dla jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark przesyłania strumieniowego przykład — wybierz klasę dla jar")</span><span class="sxs-lookup"><span data-stu-id="9b094-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="9b094-212">W hello **utworzyć JAR z modułów** okna dialogowego polu należy upewnić się, ta opcja hello zbyt**wyodrębnić docelowy toohello JAR** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b094-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="9b094-213">Spowoduje to utworzenie jednego JAR z wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="9b094-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="9b094-214">![Przykład strumieniowych Apache Spark — tworzenie jar z modułów](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "przykład strumieniowych Apache Spark — tworzenie jar z modułów")</span><span class="sxs-lookup"><span data-stu-id="9b094-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="9b094-215">Witaj **układu dane wyjściowe** karta zawiera listę wszystkich słoików hello, które są dołączane jako część hello projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="9b094-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="9b094-216">Można wybrać i hello Usuń te, na którym hello Scala aplikacji nie ma żadnych zależności bezpośrednich.</span><span class="sxs-lookup"><span data-stu-id="9b094-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="9b094-217">Dla aplikacji hello jest tworzone w tym miejscu, należy usunąć wszystkie elementy oprócz hello ostatnią (**danych wyjściowych kompilacji spark-przesyłania strumieniowego danych trwałości — przykłady**).</span><span class="sxs-lookup"><span data-stu-id="9b094-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="9b094-218">Wybierz toodelete słoików hello, a następnie kliknij przycisk hello **usunąć** ikona (![ikona usuwania](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="9b094-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="9b094-219">![Apache Spark przesyłania strumieniowego przykład — usuń wyodrębnione słoików](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark przesyłania strumieniowego przykład — usuń wyodrębnione słoików")</span><span class="sxs-lookup"><span data-stu-id="9b094-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="9b094-220">Upewnij się, że **kompilacji w upewnij** pole jest zaznaczone, co zapewnia, że jar hello jest tworzony za każdym razem, gdy projekt hello jest utworzony lub zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="9b094-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="9b094-221">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="9b094-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="9b094-222">W hello **układu dane wyjściowe** karty u dołu hello hello **dostępne elementy** okno, masz hello SQL JDBC jar, że dodane starszych toohello projektu biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9b094-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="9b094-223">Należy dodać ten toohello **układu dane wyjściowe** kartę. Kliknij prawym przyciskiem myszy plik jar hello, a następnie kliknij przycisk **Wyodrębnij do głównego dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="9b094-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="9b094-224">![Apache Spark przesyłania strumieniowego przykład — jar zależności wyodrębniania](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark przesyłania strumieniowego przykład — jar zależności wyodrębniania")</span><span class="sxs-lookup"><span data-stu-id="9b094-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="9b094-225">Witaj **układu dane wyjściowe** kartę powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="9b094-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="9b094-226">![Apache Spark przesyłania strumieniowego przykład — karta ostateczne dane wyjściowe](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark przesyłania strumieniowego przykład — karta ostateczne dane wyjściowe")</span><span class="sxs-lookup"><span data-stu-id="9b094-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="9b094-227">W hello **struktury projektu** okno dialogowe, kliknij przycisk **Zastosuj** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b094-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="9b094-228">Na pasku menu hello, kliknij przycisk **kompilacji**, a następnie kliknij przycisk **projektu należy**.</span><span class="sxs-lookup"><span data-stu-id="9b094-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="9b094-229">Możesz również kliknąć **artefaktów kompilacji** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="9b094-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="9b094-230">Hello jar dane wyjściowe utworzony na podstawie **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="9b094-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="9b094-231">![Przykład strumieniowych Apache Spark - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "przykład strumieniowych Apache Spark - output JAR")</span><span class="sxs-lookup"><span data-stu-id="9b094-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="9b094-232">Zdalne uruchamianie aplikacji hello w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="9b094-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="9b094-233">W tym artykule jest używane Livy toorun hello Apache Spark przesyłania strumieniowego aplikacji zdalnie w klastrze Spark.</span><span class="sxs-lookup"><span data-stu-id="9b094-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="9b094-234">Aby uzyskać szczegółowe omówienie na jak klastra toouse Livy z Spark w usłudze HDInsight, zobacz [przesyłania zadania zdalnie tooan Apache Spark klastra w usłudze Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="9b094-235">Przed rozpoczęciem działania aplikacji do przesyłania strumieniowego Spark hello istnieje kilka rzeczy, które należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="9b094-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="9b094-236">Uruchom zdarzenia toogenerate aplikacji autonomicznej lokalne powitania i wysyłane tooEvent koncentratora.</span><span class="sxs-lookup"><span data-stu-id="9b094-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="9b094-237">Witaj Użyj następującego polecenia toodo tak:</span><span class="sxs-lookup"><span data-stu-id="9b094-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="9b094-238">Przesyłanie strumieniowe jar hello kopiowania (**spark-przesyłania strumieniowego data trwałości examples.jar**) toohello magazynu obiektów Blob Azure skojarzonego z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="9b094-239">Dzięki temu tooLivy dostępny jar hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="9b094-240">Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), więc toodo, narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="9b094-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="9b094-241">Istnieje wiele innych klientów za pomocą tooupload danych.</span><span class="sxs-lookup"><span data-stu-id="9b094-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="9b094-242">Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="9b094-243">Zainstaluj narzędzie CURL na komputerze hello, w którym działają te aplikacje z.</span><span class="sxs-lookup"><span data-stu-id="9b094-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="9b094-244">Używamy hello tooinvoke CURL Livy punkty końcowe toorun hello zadania zdalnie.</span><span class="sxs-lookup"><span data-stu-id="9b094-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="9b094-245">Uruchom hello Spark przesyłania strumieniowego aplikacji tooreceive hello zdarzeń do obiektu Blob magazynu Azure jako tekst</span><span class="sxs-lookup"><span data-stu-id="9b094-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="9b094-246">Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):</span><span class="sxs-lookup"><span data-stu-id="9b094-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="9b094-247">Witaj parametrów w pliku hello **inputBlob.txt** są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b094-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="9b094-248">Daj nam zrozumieć, jakie są parametry hello w pliku wejściowym hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="9b094-249">**plik** jest plik jar hello ścieżki toohello aplikacji hello konta magazynu platformy Azure skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="9b094-250">**className** jest hello nazwy klasy hello w hello jar.</span><span class="sxs-lookup"><span data-stu-id="9b094-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="9b094-251">**argumenty** hello lista argumentów wymaganych przez klasę hello</span><span class="sxs-lookup"><span data-stu-id="9b094-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="9b094-252">**numExecutors** hello liczba rdzeni używane przez przesyłania strumieniowego aplikacji hello toorun Spark.</span><span class="sxs-lookup"><span data-stu-id="9b094-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="9b094-253">Zawsze należy co najmniej dwa razy hello liczby partycji Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9b094-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="9b094-254">**executorMemory**, **executorCores**, **driverMemory** są zasoby tooassign wymagane parametry używane toohello przesyłania strumieniowego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b094-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="9b094-255">Nie trzeba toocreate hello dane wyjściowe foldery (EventCheckpoint, EventCount/EventCount10) używane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="9b094-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="9b094-256">przesyłanie strumieniowe aplikacji Hello utworzy je.</span><span class="sxs-lookup"><span data-stu-id="9b094-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="9b094-257">Po uruchomieniu polecenia hello, powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="9b094-258">Zanotuj identyfikator partii hello hello ostatni wiersz danych wyjściowych hello (w tym przykładzie jest '1').</span><span class="sxs-lookup"><span data-stu-id="9b094-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="9b094-259">tooverify, który hello aplikacji zostanie wykonane pomyślnie, można sprawdzić konta magazynu Azure skojarzony z klastrem hello i powinna zostać wyświetlona hello **/EventCount/EventCount10** folder utworzony istnieje.</span><span class="sxs-lookup"><span data-stu-id="9b094-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="9b094-260">Ten folder powinien zawierać obiektów blob, które przechwytuje hello liczbą zdarzeń przetwarzane w ramach hello okres określony dla parametru hello **partii interwał w sekundach**.</span><span class="sxs-lookup"><span data-stu-id="9b094-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="9b094-261">Aplikacja przesyłania strumieniowego Spark Hello będzie nadal toorun, do momentu jego zakończenia.</span><span class="sxs-lookup"><span data-stu-id="9b094-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="9b094-262">toodo tak, użycie hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9b094-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="9b094-263">Uruchamianie aplikacji hello tooreceive hello zdarzeń do obiektu Blob magazynu Azure jako JSON</span><span class="sxs-lookup"><span data-stu-id="9b094-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="9b094-264">Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):</span><span class="sxs-lookup"><span data-stu-id="9b094-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="9b094-265">Witaj parametrów w pliku hello **inputJSON.txt** są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b094-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="9b094-266">Parametry Hello są podobne toowhat, określone dla hello tekst wyjściowy hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="9b094-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="9b094-267">Ponownie nie trzeba toocreate hello dane wyjściowe foldery (EventCheckpoint, EventCount/EventCount10) używane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="9b094-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="9b094-268">przesyłanie strumieniowe aplikacji Hello utworzy je.</span><span class="sxs-lookup"><span data-stu-id="9b094-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="9b094-269">Po uruchomieniu polecenia hello, można sprawdzić konta magazynu Azure skojarzony z klastrem hello i powinna zostać wyświetlona hello **/EventStore10** folder utworzony istnieje.</span><span class="sxs-lookup"><span data-stu-id="9b094-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="9b094-270">Otwórz każdy plik i jest poprzedzony prefiksem **części -** i powinna zostać wyświetlona hello zdarzenia przetwarzane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9b094-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="9b094-271">Uruchamianie aplikacji hello tooreceive hello zdarzeń w tabeli programu Hive</span><span class="sxs-lookup"><span data-stu-id="9b094-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="9b094-272">Witaj toorun aplikacji przesyłania strumieniowego Spark strumieni zdarzeń do gałęzi tabeli, możesz muszą niektóre dodatkowe składniki.</span><span class="sxs-lookup"><span data-stu-id="9b094-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="9b094-273">Są to:</span><span class="sxs-lookup"><span data-stu-id="9b094-273">These are:</span></span>

* <span data-ttu-id="9b094-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="9b094-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="9b094-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="9b094-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="9b094-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="9b094-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="9b094-277">gałąź site.xml</span><span class="sxs-lookup"><span data-stu-id="9b094-277">hive-site.xml</span></span>

<span data-ttu-id="9b094-278">Witaj **JAR** pliki są dostępne w klastrze Spark w usłudze HDInsight w `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="9b094-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="9b094-279">Witaj **hive-site.xml** znajduje się w temacie `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="9b094-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="9b094-280">Można użyć [WinScp](http://winscp.net/eng/download.php) toocopy za pośrednictwem tych plików z komputera lokalnego tooyour hello klastra.</span><span class="sxs-lookup"><span data-stu-id="9b094-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="9b094-281">Następnie można użyć tych plików przez tooyour konta magazynu skojarzone z klastrem hello toocopy narzędzia.</span><span class="sxs-lookup"><span data-stu-id="9b094-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="9b094-282">Aby uzyskać więcej informacji dotyczących sposobu tooupload pliki toohello konta magazynu, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="9b094-283">Po skopiowaniu przez tooyour plików hello kontem magazynu platformy Azure, otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL, a następnie uruchom hello następujące polecenie (zastąp nazwę użytkownika/hasło i klaster nazwa):</span><span class="sxs-lookup"><span data-stu-id="9b094-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="9b094-284">Witaj parametrów w pliku hello **inputHive.txt** są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b094-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="9b094-285">Parametry Hello są podobne toowhat, określone dla hello tekst wyjściowy w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="9b094-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="9b094-286">Ponownie, nie trzeba dane wyjściowe hello toocreate folderów (EventCheckpoint, EventCount/EventCount10) lub hello tabeli Hive (EventHiveTable10), które są używane jako parametry wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9b094-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="9b094-287">przesyłanie strumieniowe aplikacji Hello utworzy je.</span><span class="sxs-lookup"><span data-stu-id="9b094-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="9b094-288">Należy pamiętać, że hello **słoików** i **pliki** opcja zawiera pliki JAR toohello ścieżek i hello hive-site.xml skopiowanego toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9b094-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="9b094-289">Pomyślnie utworzono tooverify, który hello tabelę programu hive, możesz SSH na powitania klastra i wykonywania zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="9b094-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="9b094-290">Aby uzyskać instrukcje, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="9b094-291">Po nawiązaniu połączenia przy użyciu protokołu SSH, można uruchomić następujące polecenie tooverify hello tej tabeli Hive hello **EventHiveTable10**, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="9b094-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="9b094-292">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="9b094-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="9b094-293">Można również uruchomić zapytania SELECT tooview zawartość hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b094-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="9b094-294">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="9b094-295">Uruchamianie aplikacji hello tooreceive hello zdarzeń w tabeli bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="9b094-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="9b094-296">Przed uruchomieniem tego kroku, upewnij się, że masz utworzony bazę danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9b094-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="9b094-297">Aby uzyskać instrukcje, zobacz [Utwórz bazę danych SQL w minutach](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="9b094-298">toocomplete to sekcja, potrzebne są wartości dla nazwy bazy danych, nazwę serwera bazy danych i hello poświadczenia administratora bazy danych jako parametry.</span><span class="sxs-lookup"><span data-stu-id="9b094-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="9b094-299">Mimo że nie trzeba toocreate hello bazy danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b094-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="9b094-300">Witaj przesyłania strumieniowego aplikacji Spark utworzy który.</span><span class="sxs-lookup"><span data-stu-id="9b094-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="9b094-301">Otwórz wiersz polecenia, przejdź do katalogu toohello, w którym zainstalowano narzędzie CURL i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="9b094-302">Witaj parametrów w pliku hello **inputSQL.txt** są zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b094-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="9b094-303">tooverify, który hello aplikacji zostanie wykonane pomyślnie, możesz połączyć toohello bazy danych Azure SQL przy użyciu programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9b094-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="9b094-304">Aby uzyskać instrukcje dotyczące toodo, który zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="9b094-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="9b094-305">Po przejściu toohello połączenia bazy danych, można przejść toohello **EventContent** tabeli, która została utworzona przez hello przesyłania strumieniowego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b094-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="9b094-306">Danych hello tooget szybkie zapytania jest uruchamiane z hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b094-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="9b094-307">Uruchom następujące zapytanie hello:</span><span class="sxs-lookup"><span data-stu-id="9b094-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="9b094-308">Powinny pojawić się dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="9b094-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="9b094-309"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9b094-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9b094-310">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="9b094-311">Projekt połączenie oparte na odbiorcy i bezpośredniego DStream</span><span class="sxs-lookup"><span data-stu-id="9b094-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="9b094-312">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="9b094-312">Scenarios</span></span>
* [<span data-ttu-id="9b094-313">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="9b094-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9b094-314">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="9b094-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9b094-315">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9b094-316">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9b094-317">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b094-317">Create and run applications</span></span>
* [<span data-ttu-id="9b094-318">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="9b094-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9b094-319">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="9b094-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9b094-320">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="9b094-320">Tools and extensions</span></span>
* [<span data-ttu-id="9b094-321">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="9b094-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9b094-322">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="9b094-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9b094-323">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9b094-324">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9b094-325">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="9b094-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9b094-326">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9b094-327">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="9b094-327">Manage resources</span></span>
* [<span data-ttu-id="9b094-328">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9b094-329">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b094-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
