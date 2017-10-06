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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Określenia trendów tematy Twitter z systemu Apache Storm w usłudze HDInsight

Dowiedz się, jak toouse Trident toocreate topologii Storm określający umożliwia analizę trendów tematy (skrót znaczniki) w serwisie Twitter.

Trident to Abstrakcja wysokiego poziomu, która udostępnia narzędzia, takie jak sprzężenia, agregacje, grupowanie, funkcje i filtry. Ponadto Trident dodaje elementów podstawowych do wykonywania stanowe, przyrostowe przetwarzanie. przykład Witaj używane w tym dokumencie jest topologii Trident spout niestandardowych i funkcji. Używa również kilka wbudowanych funkcji dostarczonych przez Trident.

## <a name="requirements"></a>Wymagania

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java i hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Konto dewelopera w serwisie Twitter

## <a name="download-hello-project"></a>Pobierz hello projektu

Użyj hello poniższy kod projektu hello tooclone lokalnie.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Opis hello topologii

Witaj poniższym diagramie przedstawiono z sposób przepływu danych za pośrednictwem tej topologii:

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Ten diagram jest uproszczona prezentacja hello topologii. Wiele wystąpień składników hello są rozproszone na powitania węzłów w klastrze hello.


Hello Trident kod, który implementuje topologii hello jest następujący:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Ten kod wykonuje hello następujące akcje:

1. Tworzy strumień z hello spout. Hello spout pobiera tweetów z serwisem Twitter i filtruje je dla określonych słów kluczowych (love, muzyka i kawy, w tym przykładzie).

2. HashtagExtractor, funkcją niestandardową jest używane tooextract tagi wyznaczania wartości skrótu z każdym tweet. tagi skrótu Hello są emitowany toohello strumienia.

3. strumień Hello jest pogrupowane według znaczników wyznaczania wartości skrótu i przekazany tooan agregatora. Ten agregator tworzy liczbę ile razy podczas każdego znacznika wyznaczania wartości skrótu. Te dane są utrwalane w pamięci. Na koniec nowy strumień jest emitowany zawierający tag skrótu hello i liczba hello.

4. Witaj **FirstN** tooreturn zastosowane tylko hello pierwszych 10 wartości, na podstawie pola Liczba hello jest zestawu.

> [!NOTE]
> Aby uzyskać więcej informacji na temat pracy z Trident, zobacz hello [omówienie Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) dokumentu.

### <a name="hello-spout"></a>Hello spout

Hello spout **TwitterSpout**, używa [Twitter4j](http://twitter4j.org/en/) tweetów tooretrieve z serwisem Twitter. Filtr jest tworzona dla słowa hello __chętnie__, **utworów muzycznych**, i **kawy**. Przychodzące tweetów (stan) zgodne filtrem hello są przechowywane w połączonych kolejki blokowania. Na koniec elementy są pobierane poza hello kolejki i wysyłanego toohello topologii.

### <a name="hello-hashtagextractor"></a>Witaj HashtagExtractor

tagi skrótu tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) jest używane tooretrieve wszystkie tagi wyznaczania wartości skrótu, które są zawarte w hello tweet. Te są następnie emitowany toohello strumienia.

## <a name="configure-twitter"></a>Konfigurowanie usługi Twitter

Użyj hello następujące kroki tooregister nową aplikację usługi Twitter i uzyskiwanie powitania klienta i dostęp tokenu informacje potrzebne tooread z serwisem Twitter:

1. Przejdź za[aplikacji w usłudze Twitter](https://apps.twitter.com) i kliknij przycisk hello **Utwórz nową aplikację** przycisku. Po wypełnieniu formularza hello, pozostaw hello **wywołania zwrotnego adresu URL** pole puste.

2. Po utworzeniu aplikacji hello kliknij hello **kluczy i tokenów dostępu** kartę.

3. Kopiuj hello **konsumenta** i **klucz tajny klienta** informacji.

4. U dołu hello strony hello, zaznacz pole wyboru **Utwórz moje tokenu dostępu** Jeśli nie istnieją żadne tokenów. Po utworzeniu hello tokenów, hello kopiowania **Token dostępu** i **klucz tajny tokenu dostępu** informacji.

5. W hello **TwitterSpoutTopology** projektu, należy wcześniej sklonowany, otwórz hello **resources/twitter4j.properties** plików, dodawanie hello informacji zebranych w poprzednich krokach hello, a następnie zapisz plik hello .

## <a name="build-hello-topology"></a>Tworzenie topologii hello

Użyj hello poniższy kod toobuild hello projektu:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Topologia hello testu

Użyj hello następujące polecenie lokalnie tootest hello topologii:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Po uruchomieniu topologii hello powinny być widoczne informacje o debugowaniu, zawierający skrótu hello liczby emitowany przez hello topologii i tagów. dane wyjściowe Hello powinna zostać wyświetlona podobne toohello następującego tekstu:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Następne kroki

Teraz, gdy zostały przetestowane topologii hello lokalnie, odnajdywania, jak toodeploy hello topologii: [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology.md).

Można również zainteresować następujące tematy Storm hello:

* [Tworzenie topologii Java dla Storm w usłudze HDInsight za pomocą programu Maven](hdinsight-storm-develop-java-topology.md)
* [Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Aby uzyskać więcej przykładów Storm dla usługi HDInsight:

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

