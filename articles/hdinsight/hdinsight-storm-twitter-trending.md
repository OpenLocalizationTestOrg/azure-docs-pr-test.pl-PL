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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Określenia trendów tematy Twitter z systemu Apache Storm w usłudze HDInsight

Dowiedz się, jak używać Trident do tworzenia topologii Storm, która określa trendów tematy (skrót znaczniki) w serwisie Twitter.

Trident to Abstrakcja wysokiego poziomu, która udostępnia narzędzia, takie jak sprzężenia, agregacje, grupowanie, funkcje i filtry. Ponadto Trident dodaje elementów podstawowych do wykonywania stanowe, przyrostowe przetwarzanie. Przykład używane w tym dokumencie jest topologii Trident spout niestandardowych i funkcji. Używa również kilka wbudowanych funkcji dostarczonych przez Trident.

## <a name="requirements"></a>Wymagania

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java i JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Konto dewelopera w serwisie Twitter

## <a name="download-the-project"></a>Pobieranie projektu

Klonowanie projektu lokalnie, należy użyć poniższego kodu.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a>Opis topologii

Na poniższym diagramie przedstawiono z sposób przepływu danych za pośrednictwem tej topologii:

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Ten diagram jest uproszczona prezentacja topologii. Wiele wystąpień składników są dystrybuowane między węzłami w klastrze.


Kod języka Trident, który implementuje topologii wygląda następująco:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Ten kod wykonuje następujące czynności:

1. Tworzy strumień z spout. Spout pobiera tweetów z serwisem Twitter i filtruje je dla określonych słów kluczowych (love, muzyka i kawy, w tym przykładzie).

2. HashtagExtractor, funkcją niestandardową służy do wyodrębniania tagi wyznaczania wartości skrótu z każdego tweet. Tagi wyznaczania wartości skrótu są emitowane w strumieniu.

3. Strumień jest pogrupowane według znaczników wyznaczania wartości skrótu i przekazane do agregatora. Ten agregator tworzy liczbę ile razy podczas każdego znacznika wyznaczania wartości skrótu. Te dane są utrwalane w pamięci. Na koniec nowy strumień jest emitowany zawierający tag wyznaczania wartości skrótu i count.

4. **FirstN** zestawu jest stosowany do zwracanych tylko pierwszych 10 wartości, na podstawie pola Liczba.

> [!NOTE]
> Aby uzyskać więcej informacji na temat pracy z Trident, zobacz [omówienie Trident API](http://storm.apache.org/releases/current/Trident-API-Overview.html) dokumentu.

### <a name="the-spout"></a>Spout

Spout, **TwitterSpout**, używa [Twitter4j](http://twitter4j.org/en/) można pobrać z serwisem Twitter tweetów. Zostanie utworzony filtr słowa __chętnie__, **utworów muzycznych**, i **kawy**. Przychodzące tweetów (stan) zgodne z filtrem są przechowywane w połączonych kolejki blokowania. Ponadto elementy są pobierane poza kolejki i wysyłanego do topologii.

### <a name="the-hashtagextractor"></a>HashtagExtractor

Można wyodrębnić skrótu tagów, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) służy do pobierania wszystkie tagi wyznaczania wartości skrótu, które są zawarte w tweet. Są one następnie wysyłanego do strumienia.

## <a name="configure-twitter"></a>Konfigurowanie usługi Twitter

Wykonaj następujące kroki, aby zarejestrować nową aplikację usługi Twitter i uzyskiwania informacji token dostępu i konsumentów potrzebne do odczytywania z serwisem Twitter:

1. Przejdź do [aplikacji w usłudze Twitter](https://apps.twitter.com) i kliknij przycisk **Utwórz nową aplikację** przycisku. Po wypełnieniu formularza, pozostaw **wywołania zwrotnego adresu URL** pole puste.

2. Po utworzeniu aplikacji, kliknij przycisk **kluczy i tokenów dostępu** kartę.

3. Kopiuj **konsumenta** i **klucz tajny klienta** informacji.

4. W dolnej części strony, wybierz **Utwórz moje tokenu dostępu** Jeśli nie istnieją żadne tokenów. Podczas tworzenia tokenów Skopiuj **Token dostępu** i **klucz tajny tokenu dostępu** informacji.

5. W **TwitterSpoutTopology** wcześniej sklonowany, otwórz projekt **resources/twitter4j.properties** pliku, Dodaj informacje zebrane w poprzednich krokach, a następnie zapisz plik.

## <a name="build-the-topology"></a>Tworzenie topologii

Aby skompilować projekt, należy użyć poniższego kodu:

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a>Topologia testów

Aby przetestować topologii lokalnie, użyj następującego polecenia:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Po uruchomieniu topologii powinny być widoczne informacje o debugowaniu, który zawiera skrót liczby emitowany przez topologii i tagów. Dane wyjściowe powinny wyglądać podobnie do następującego tekstu:

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

Teraz, gdy zostały przetestowane topologii lokalnie, odnajdywanie wdrażanie topologii: [wdrażanie topologii Apache Storm w usłudze HDInsight oraz zarządzania nimi](hdinsight-storm-deploy-monitor-topology.md).

Można również zainteresować następujące tematy Storm:

* [Tworzenie topologii Java dla Storm w usłudze HDInsight za pomocą programu Maven](hdinsight-storm-develop-java-topology.md)
* [Tworzenie topologii C# dla Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Aby uzyskać więcej przykładów Storm dla usługi HDInsight:

* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

