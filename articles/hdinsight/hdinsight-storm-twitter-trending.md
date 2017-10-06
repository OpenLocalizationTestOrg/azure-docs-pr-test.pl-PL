---
title: "Tematy trendów aaaTwitter z systemu Apache Storm w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Trident toocreate topologii Apache Storm, która określa tematy trendów w serwisie Twitter na podstawie hashtagów."
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="ec171-103">Określenia trendów tematy Twitter z systemu Apache Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec171-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="ec171-104">Dowiedz się, jak toouse Trident toocreate topologii Storm określający umożliwia analizę trendów tematy (skrót znaczniki) w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="ec171-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="ec171-105">Trident to Abstrakcja wysokiego poziomu, która udostępnia narzędzia, takie jak sprzężenia, agregacje, grupowanie, funkcje i filtry.</span><span class="sxs-lookup"><span data-stu-id="ec171-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="ec171-106">Ponadto Trident dodaje elementów podstawowych do wykonywania stanowe, przyrostowe przetwarzanie.</span><span class="sxs-lookup"><span data-stu-id="ec171-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="ec171-107">przykład Witaj używane w tym dokumencie jest topologii Trident spout niestandardowych i funkcji.</span><span class="sxs-lookup"><span data-stu-id="ec171-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="ec171-108">Używa również kilka wbudowanych funkcji dostarczonych przez Trident.</span><span class="sxs-lookup"><span data-stu-id="ec171-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="ec171-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ec171-109">Requirements</span></span>

* <span data-ttu-id="ec171-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java i hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="ec171-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="ec171-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="ec171-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="ec171-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="ec171-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="ec171-113">Konto dewelopera w serwisie Twitter</span><span class="sxs-lookup"><span data-stu-id="ec171-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="ec171-114">Pobierz hello projektu</span><span class="sxs-lookup"><span data-stu-id="ec171-114">Download hello project</span></span>

<span data-ttu-id="ec171-115">Użyj hello poniższy kod projektu hello tooclone lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ec171-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="ec171-116">Opis hello topologii</span><span class="sxs-lookup"><span data-stu-id="ec171-116">Understanding hello topology</span></span>

<span data-ttu-id="ec171-117">Witaj poniższym diagramie przedstawiono z sposób przepływu danych za pośrednictwem tej topologii:</span><span class="sxs-lookup"><span data-stu-id="ec171-117">hello following diagram shows of how data flows through this topology:</span></span>

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="ec171-119">Ten diagram jest uproszczona prezentacja hello topologii.</span><span class="sxs-lookup"><span data-stu-id="ec171-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="ec171-120">Wiele wystąpień składników hello są rozproszone na powitania węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="ec171-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="ec171-121">Hello Trident kod, który implementuje topologii hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="ec171-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="ec171-122">Ten kod wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="ec171-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="ec171-123">Tworzy strumień z hello spout.</span><span class="sxs-lookup"><span data-stu-id="ec171-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="ec171-124">Hello spout pobiera tweetów z serwisem Twitter i filtruje je dla określonych słów kluczowych (love, muzyka i kawy, w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="ec171-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="ec171-125">HashtagExtractor, funkcją niestandardową jest używane tooextract tagi wyznaczania wartości skrótu z każdym tweet.</span><span class="sxs-lookup"><span data-stu-id="ec171-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="ec171-126">tagi skrótu Hello są emitowany toohello strumienia.</span><span class="sxs-lookup"><span data-stu-id="ec171-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="ec171-127">strumień Hello jest pogrupowane według znaczników wyznaczania wartości skrótu i przekazany tooan agregatora.</span><span class="sxs-lookup"><span data-stu-id="ec171-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="ec171-128">Ten agregator tworzy liczbę ile razy podczas każdego znacznika wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="ec171-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="ec171-129">Te dane są utrwalane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="ec171-129">This data is persisted in memory.</span></span> <span data-ttu-id="ec171-130">Na koniec nowy strumień jest emitowany zawierający tag skrótu hello i liczba hello.</span><span class="sxs-lookup"><span data-stu-id="ec171-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="ec171-131">Witaj **FirstN** tooreturn zastosowane tylko hello pierwszych 10 wartości, na podstawie pola Liczba hello jest zestawu.</span><span class="sxs-lookup"><span data-stu-id="ec171-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="ec171-132">Aby uzyskać więcej informacji na temat pracy z Trident, zobacz hello [omówienie Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ec171-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="ec171-133">Hello spout</span><span class="sxs-lookup"><span data-stu-id="ec171-133">hello spout</span></span>

<span data-ttu-id="ec171-134">Hello spout **TwitterSpout**, używa [Twitter4j](http://twitter4j.org/en/) tweetów tooretrieve z serwisem Twitter.</span><span class="sxs-lookup"><span data-stu-id="ec171-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="ec171-135">Filtr jest tworzona dla słowa hello __chętnie__, **utworów muzycznych**, i **kawy**.</span><span class="sxs-lookup"><span data-stu-id="ec171-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="ec171-136">Przychodzące tweetów (stan) zgodne filtrem hello są przechowywane w połączonych kolejki blokowania.</span><span class="sxs-lookup"><span data-stu-id="ec171-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="ec171-137">Na koniec elementy są pobierane poza hello kolejki i wysyłanego toohello topologii.</span><span class="sxs-lookup"><span data-stu-id="ec171-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="ec171-138">Witaj HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="ec171-138">hello HashtagExtractor</span></span>

<span data-ttu-id="ec171-139">tagi skrótu tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) jest używane tooretrieve wszystkie tagi wyznaczania wartości skrótu, które są zawarte w hello tweet.</span><span class="sxs-lookup"><span data-stu-id="ec171-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="ec171-140">Te są następnie emitowany toohello strumienia.</span><span class="sxs-lookup"><span data-stu-id="ec171-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="ec171-141">Konfigurowanie usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="ec171-141">Configure Twitter</span></span>

<span data-ttu-id="ec171-142">Użyj hello następujące kroki tooregister nową aplikację usługi Twitter i uzyskiwanie powitania klienta i dostęp tokenu informacje potrzebne tooread z serwisem Twitter:</span><span class="sxs-lookup"><span data-stu-id="ec171-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="ec171-143">Przejdź za[aplikacji w usłudze Twitter](https://apps.twitter.com) i kliknij przycisk hello **Utwórz nową aplikację** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ec171-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="ec171-144">Po wypełnieniu formularza hello, pozostaw hello **wywołania zwrotnego adresu URL** pole puste.</span><span class="sxs-lookup"><span data-stu-id="ec171-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="ec171-145">Po utworzeniu aplikacji hello kliknij hello **kluczy i tokenów dostępu** kartę.</span><span class="sxs-lookup"><span data-stu-id="ec171-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="ec171-146">Kopiuj hello **konsumenta** i **klucz tajny klienta** informacji.</span><span class="sxs-lookup"><span data-stu-id="ec171-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="ec171-147">U dołu hello strony hello, zaznacz pole wyboru **Utwórz moje tokenu dostępu** Jeśli nie istnieją żadne tokenów.</span><span class="sxs-lookup"><span data-stu-id="ec171-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="ec171-148">Po utworzeniu hello tokenów, hello kopiowania **Token dostępu** i **klucz tajny tokenu dostępu** informacji.</span><span class="sxs-lookup"><span data-stu-id="ec171-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="ec171-149">W hello **TwitterSpoutTopology** projektu, należy wcześniej sklonowany, otwórz hello **resources/twitter4j.properties** plików, dodawanie hello informacji zebranych w poprzednich krokach hello, a następnie zapisz plik hello .</span><span class="sxs-lookup"><span data-stu-id="ec171-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="ec171-150">Tworzenie topologii hello</span><span class="sxs-lookup"><span data-stu-id="ec171-150">Build hello topology</span></span>

<span data-ttu-id="ec171-151">Użyj hello poniższy kod toobuild hello projektu:</span><span class="sxs-lookup"><span data-stu-id="ec171-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="ec171-152">Topologia hello testu</span><span class="sxs-lookup"><span data-stu-id="ec171-152">Test hello topology</span></span>

<span data-ttu-id="ec171-153">Użyj hello następujące polecenie lokalnie tootest hello topologii:</span><span class="sxs-lookup"><span data-stu-id="ec171-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="ec171-154">Po uruchomieniu topologii hello powinny być widoczne informacje o debugowaniu, zawierający skrótu hello liczby emitowany przez hello topologii i tagów.</span><span class="sxs-lookup"><span data-stu-id="ec171-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="ec171-155">dane wyjściowe Hello powinna zostać wyświetlona podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ec171-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="ec171-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec171-156">Next steps</span></span>

<span data-ttu-id="ec171-157">Teraz, gdy zostały przetestowane topologii hello lokalnie, odnajdywania, jak toodeploy hello topologii: [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ec171-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="ec171-158">Można również zainteresować następujące tematy Storm hello:</span><span class="sxs-lookup"><span data-stu-id="ec171-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="ec171-159">Tworzenie topologii Java dla Storm w usłudze HDInsight za pomocą programu Maven</span><span class="sxs-lookup"><span data-stu-id="ec171-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ec171-160">Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec171-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="ec171-161">Aby uzyskać więcej przykładów Storm dla usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ec171-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="ec171-162">Przykładowe topologie dla systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec171-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

