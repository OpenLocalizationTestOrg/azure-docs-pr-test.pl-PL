---
title: "Twitter trendów tematy z systemu Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Trident do tworzenia topologii Apache Storm, która określa tematy trendów w serwisie Twitter, w oparciu o hashtagów."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="044cc-103">Określenia trendów tematy Twitter z systemu Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="044cc-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="044cc-104">Dowiedz się, jak używać Trident do tworzenia topologii Storm, która określa trendów tematy (skrót znaczniki) w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="044cc-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="044cc-105">Trident to Abstrakcja wysokiego poziomu, która udostępnia narzędzia, takie jak sprzężenia, agregacje, grupowanie, funkcje i filtry.</span><span class="sxs-lookup"><span data-stu-id="044cc-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="044cc-106">Ponadto Trident dodaje elementów podstawowych do wykonywania stanowe, przyrostowe przetwarzanie.</span><span class="sxs-lookup"><span data-stu-id="044cc-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="044cc-107">Przykład używane w tym dokumencie jest topologii Trident spout niestandardowych i funkcji.</span><span class="sxs-lookup"><span data-stu-id="044cc-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="044cc-108">Używa również kilka wbudowanych funkcji dostarczonych przez Trident.</span><span class="sxs-lookup"><span data-stu-id="044cc-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="044cc-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="044cc-109">Requirements</span></span>

* <span data-ttu-id="044cc-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java i JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="044cc-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="044cc-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="044cc-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="044cc-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="044cc-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="044cc-113">Konto dewelopera w serwisie Twitter</span><span class="sxs-lookup"><span data-stu-id="044cc-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="044cc-114">Pobieranie projektu</span><span class="sxs-lookup"><span data-stu-id="044cc-114">Download the project</span></span>

<span data-ttu-id="044cc-115">Klonowanie projektu lokalnie, należy użyć poniższego kodu.</span><span class="sxs-lookup"><span data-stu-id="044cc-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="044cc-116">Opis topologii</span><span class="sxs-lookup"><span data-stu-id="044cc-116">Understanding the topology</span></span>

<span data-ttu-id="044cc-117">Na poniższym diagramie przedstawiono z sposób przepływu danych za pośrednictwem tej topologii:</span><span class="sxs-lookup"><span data-stu-id="044cc-117">The following diagram shows of how data flows through this topology:</span></span>

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="044cc-119">Ten diagram jest uproszczona prezentacja topologii.</span><span class="sxs-lookup"><span data-stu-id="044cc-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="044cc-120">Wiele wystąpień składników są dystrybuowane między węzłami w klastrze.</span><span class="sxs-lookup"><span data-stu-id="044cc-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="044cc-121">Kod języka Trident, który implementuje topologii wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="044cc-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="044cc-122">Ten kod wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="044cc-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="044cc-123">Tworzy strumień z spout.</span><span class="sxs-lookup"><span data-stu-id="044cc-123">Creates a stream from the spout.</span></span> <span data-ttu-id="044cc-124">Spout pobiera tweetów z serwisem Twitter i filtruje je dla określonych słów kluczowych (love, muzyka i kawy, w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="044cc-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="044cc-125">HashtagExtractor, funkcją niestandardową służy do wyodrębniania tagi wyznaczania wartości skrótu z każdego tweet.</span><span class="sxs-lookup"><span data-stu-id="044cc-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="044cc-126">Tagi wyznaczania wartości skrótu są emitowane w strumieniu.</span><span class="sxs-lookup"><span data-stu-id="044cc-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="044cc-127">Strumień jest pogrupowane według znaczników wyznaczania wartości skrótu i przekazane do agregatora.</span><span class="sxs-lookup"><span data-stu-id="044cc-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="044cc-128">Ten agregator tworzy liczbę ile razy podczas każdego znacznika wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="044cc-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="044cc-129">Te dane są utrwalane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="044cc-129">This data is persisted in memory.</span></span> <span data-ttu-id="044cc-130">Na koniec nowy strumień jest emitowany zawierający tag wyznaczania wartości skrótu i count.</span><span class="sxs-lookup"><span data-stu-id="044cc-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="044cc-131">**FirstN** zestawu jest stosowany do zwracanych tylko pierwszych 10 wartości, na podstawie pola Liczba.</span><span class="sxs-lookup"><span data-stu-id="044cc-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="044cc-132">Aby uzyskać więcej informacji na temat pracy z Trident, zobacz [omówienie Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="044cc-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="044cc-133">Spout</span><span class="sxs-lookup"><span data-stu-id="044cc-133">The spout</span></span>

<span data-ttu-id="044cc-134">Spout, **TwitterSpout**, używa [Twitter4j](http://twitter4j.org/en/) można pobrać z serwisem Twitter tweetów.</span><span class="sxs-lookup"><span data-stu-id="044cc-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="044cc-135">Zostanie utworzony filtr słowa __chętnie__, **utworów muzycznych**, i **kawy**.</span><span class="sxs-lookup"><span data-stu-id="044cc-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="044cc-136">Przychodzące tweetów (stan) zgodne z filtrem są przechowywane w połączonych kolejki blokowania.</span><span class="sxs-lookup"><span data-stu-id="044cc-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="044cc-137">Ponadto elementy są pobierane poza kolejki i wysyłanego do topologii.</span><span class="sxs-lookup"><span data-stu-id="044cc-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="044cc-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="044cc-138">The HashtagExtractor</span></span>

<span data-ttu-id="044cc-139">Można wyodrębnić skrótu tagów, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) służy do pobierania wszystkie tagi wyznaczania wartości skrótu, które są zawarte w tweet.</span><span class="sxs-lookup"><span data-stu-id="044cc-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="044cc-140">Są one następnie wysyłanego do strumienia.</span><span class="sxs-lookup"><span data-stu-id="044cc-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="044cc-141">Konfigurowanie usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="044cc-141">Configure Twitter</span></span>

<span data-ttu-id="044cc-142">Wykonaj następujące kroki, aby zarejestrować nową aplikację usługi Twitter i uzyskiwania informacji token dostępu i konsumentów potrzebne do odczytywania z serwisem Twitter:</span><span class="sxs-lookup"><span data-stu-id="044cc-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="044cc-143">Przejdź do [aplikacji w usłudze Twitter](https://apps.twitter.com) i kliknij przycisk **Utwórz nową aplikację** przycisku.</span><span class="sxs-lookup"><span data-stu-id="044cc-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="044cc-144">Po wypełnieniu formularza, pozostaw **wywołania zwrotnego adresu URL** pole puste.</span><span class="sxs-lookup"><span data-stu-id="044cc-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="044cc-145">Po utworzeniu aplikacji, kliknij przycisk **kluczy i tokenów dostępu** kartę.</span><span class="sxs-lookup"><span data-stu-id="044cc-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="044cc-146">Kopiuj **konsumenta** i **klucz tajny klienta** informacji.</span><span class="sxs-lookup"><span data-stu-id="044cc-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="044cc-147">W dolnej części strony, wybierz **Utwórz moje tokenu dostępu** Jeśli nie istnieją żadne tokenów.</span><span class="sxs-lookup"><span data-stu-id="044cc-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="044cc-148">Podczas tworzenia tokenów Skopiuj **Token dostępu** i **klucz tajny tokenu dostępu** informacji.</span><span class="sxs-lookup"><span data-stu-id="044cc-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="044cc-149">W **TwitterSpoutTopology** wcześniej sklonowany, otwórz projekt **resources/twitter4j.properties** pliku, Dodaj informacje zebrane w poprzednich krokach, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="044cc-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="044cc-150">Tworzenie topologii</span><span class="sxs-lookup"><span data-stu-id="044cc-150">Build the topology</span></span>

<span data-ttu-id="044cc-151">Aby skompilować projekt, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="044cc-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="044cc-152">Topologia testów</span><span class="sxs-lookup"><span data-stu-id="044cc-152">Test the topology</span></span>

<span data-ttu-id="044cc-153">Aby przetestować topologii lokalnie, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="044cc-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="044cc-154">Po uruchomieniu topologii powinny być widoczne informacje o debugowaniu, który zawiera skrót liczby emitowany przez topologii i tagów.</span><span class="sxs-lookup"><span data-stu-id="044cc-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="044cc-155">Dane wyjściowe powinny wyglądać podobnie do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="044cc-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="044cc-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="044cc-156">Next steps</span></span>

<span data-ttu-id="044cc-157">Teraz, gdy zostały przetestowane topologii lokalnie, odnajdywanie wdrażanie topologii: [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="044cc-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="044cc-158">Można również zainteresować następujące tematy Storm:</span><span class="sxs-lookup"><span data-stu-id="044cc-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="044cc-159">Tworzenie topologii Java dla Storm w usłudze HDInsight za pomocą programu Maven</span><span class="sxs-lookup"><span data-stu-id="044cc-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="044cc-160">Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="044cc-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="044cc-161">Aby uzyskać więcej przykładów Storm dla usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="044cc-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="044cc-162">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="044cc-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

