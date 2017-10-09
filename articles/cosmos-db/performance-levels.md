---
title: "poziomy wydajności aaaDocumentDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu poziomy wydajności usługi DocumentDB interfejsu API umożliwiają tooreserve przepływności na podstawie kontenera na."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Wycofanie hello poziomy wydajności S1, S2 i S3

> [!IMPORTANT] 
> Witaj S1, S2 i S3 poziomy wydajności omówione w tym artykule jest wycofana i nie będą już dostępne dla nowych kont usługi DocumentDB interfejsu API.
>

Ten artykuł zawiera omówienie poziomów wydajności S1, S2 i S3 i omówiono, jak kolekcje hello, korzystających z tych poziomów wydajności będzie toosingle zmigrowane kolekcje partycji na 1 sierpnia 2017 r. Po przeczytaniu tego artykułu, będziesz w stanie tooanswer hello następujące pytania:

- [Dlaczego są wydajności S1, S2 i S3 hello poziomy wycofana?](#why-retired)
- [Kolekcje z jedną partycją i kolekcji partycjonowanych porównanie toohello S1, S2, poziomy wydajności S3?](#compare)
- [Co mogę zrobić muszą tooensure toodo nieprzerwany dostęp do danych toomy?](#uninterrupted-access)
- [Jak mojej kolekcji ulegnie zmianie po migracji hello?](#collection-change)
- [Jak Moje rozliczeń ulegnie zmianie po jestem toosingle zmigrowane kolekcje partycji?](#billing-change)
- [Co zrobić, jeśli potrzebna jest więcej niż 10 GB przestrzeni dyskowej?](#more-storage-needed)
- [Można zmienić między hello poziomy wydajności S1, S2 i S3 przed 1 sierpnia 2017 r?](#change-before)
- [Jak wiedzą, gdy został zmigrowany mojej kolekcji?](#when-migrated)
- [Jak przeprowadzić migrację z hello S1, S2, S3 kolekcjami partycji toosingle poziomów wydajności na własną?](#migrate-diy)
- [Jak m wpływ mam EA klienta?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Dlaczego są wydajności S1, S2 i S3 hello poziomy wycofana?

poziomy wydajności S1, S2 i S3 Hello nie nie elastyczność hello oferty, która oferuje kolekcje interfejsu API usługi DocumentDB. Hello S1, S2, poziomy wydajności S3, zarówno hello przepływności i pojemność pamięci masowej zostały wstępnie ustawiony i nie zaproponował elastyczność. Azure DB rozwiązania Cosmos oferuje teraz hello możliwości toocustomize Twojego przepływność i Magazyn, oferty, można znacznie większą elastyczność tooscale Twojego możliwości stosownie do potrzeb.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Kolekcje z jedną partycją i kolekcji partycjonowanych porównanie toohello S1, S2, poziomy wydajności S3?

Witaj w poniższej tabeli porównano hello przepływność i Magazyn opcje dostępne w kolekcji partycjonowanych i S1, S2, S3 poziomy wydajności w kolekcje z jedną partycją. Oto przykład dla regionu nam wschodnie 2:

|   |Kolekcja podzielonym na partycje|Kolekcja jednej partycji|S1|S2|S3|
|---|---|---|---|---|---|
|Maksymalna przepustowość|Nieograniczona liczba|10 K RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Przepustowość minimalna|2.5 K RU/s|400 RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Maksymalna przestrzeń magazynowa|Nieograniczona liczba|10 GB|10 GB|10 GB|10 GB|
|Cena (co miesiąc)|Przepływność: $6 / 100 RU/s<br><br>Magazyn: 0,25 USD/GB|Przepływność: $6 / 100 RU/s<br><br>Magazyn: 0,25 USD/GB|$25 USD|$50 USD|$100 USD|

Czy klient EA? Jeśli tak, zobacz [am I wpływ mam EA klienta?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>Co mogę zrobić muszą tooensure toodo nieprzerwany dostęp do danych toomy?

Nothing, DB rozwiązania Cosmos obsługuje migrację hello za Ciebie. Jeśli masz kolekcję S1, S2 lub S3 bieżącej kolekcji będą tooa migrowanych kolekcji jednej partycji na 31 lipca 2017 r. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Jak mojej kolekcji ulegnie zmianie po migracji hello?

Jeśli masz kolekcji S1 będzie tooa migrowanych kolekcji jednej partycji o 400 RU/s przepustowości. 400 RU/s jest hello najniższy przepływności dostępne kolekcje z jedną partycją. Jednak koszt hello 400 RU/s w hello jest Kolekcja jednej partycji w przybliżeniu hello takie same, jak zostały płatność za pomocą kolekcji S1 i 250 RU/s — dzięki nie płatność za hello bardzo 150 tooyou dostępne RU/s.

Jeśli masz kolekcji S2 będzie tooa migrowanych kolekcji jednej partycji o 1 K RU/s. Zostanie wyświetlone nie Zmień poziom przepływności tooyour.

Jeśli masz kolekcji S3 będzie tooa migrowanych kolekcji jednej partycji z 2,5 K RU/s. Zostanie wyświetlone nie Zmień poziom przepływności tooyour.

W każdym z tych przypadków po migracji kolekcji użytkownik będzie być może toocustomize poziom przepływności lub skalować go w górę i w dół jako wymagane tooprovide małych opóźnieniach dostępu tooyour użytkowników. toochange poziomu przepływności powitania po migracji ma kolekcji po prostu otwórz konto DB rozwiązania Cosmos w hello portalu Azure kliknij skali, wybierz kolekcję, a następnie Dostosuj poziom przepływności hello, jak pokazano w powitania po zrzut ekranu:

![Jak tooscale przepływność w hello portalu Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Jak Moje rozliczeń ulegnie zmianie po jestem toohello zmigrowane kolekcje z jedną partycją?

Wykonując zawiera 10 kolekcji S1, 1 GB pamięci masowej dla każdego regionu nam wschodnie hello, i migracji tych 10 S1 kolekcje too10 kolekcje z jedną partycją na 400 RU/s (minimalny poziom hello). Jeśli zachowasz hello kolekcje 10 jednej partycji dla całego miesiąca, rachunku będzie wyglądać następująco:

![Jak S1 ceny 10 kolekcje porównuje too10 kolekcji przy użyciu ceny Kolekcja jednej partycji](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Co zrobić, jeśli potrzebna jest więcej niż 10 GB przestrzeni dyskowej?

Czy masz kolekcję o poziomie wydajności S1, S2 lub S3 lub mieć Kolekcja jednej partycji, które mają 10 GB dostępnego miejsca, można użyć toomigrate narzędzia migracji danych DB rozwiązania Cosmos hello tooa Twojego danych praktycznie na partycje kolekcji nieograniczony magazyn. Aby uzyskać informacje dotyczące korzyści hello kolekcję partycjonowaną, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](documentdb-partition-data.md). Aby uzyskać informacje dotyczące toomigrate można znaleźć S1, S2, S3 lub kolekcji tooa podzielona na partycje Kolekcja jednej partycji, [migracji z jednej partycji toopartitioned kolekcji](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>Można zmienić między hello poziomy wydajności S1, S2 i S3 przed 1 sierpnia 2017 r?

Istniejące konta tylko z wydajnością S1, S2 i S3 zostanie stanie toochange i zmieniać warstwy poziomu wydajności za pośrednictwem portalu hello lub programowo. 1 sierpnia 2017 hello S1, S2, i poziomy wydajności S3 nie będą już dostępne. W przypadku zmiany z kolekcji jednej partycji tooa S1 S3 i S3 nie może zwracać toohello poziomy wydajności S1, S2 lub S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Jak wiedzą, gdy został zmigrowany mojej kolekcji?

Witaj migracji nastąpi na 31 lipca 2017 r. Jeśli masz kolekcję używającą hello S1, S2 lub poziomy wydajności S3, zespołu DB rozwiązania Cosmos hello skontaktuje się z Tobą za pośrednictwem poczty e-mail przed dokonaniem migracji hello. Po zakończeniu migracji hello, na 1 sierpnia 2017 hello portalu Azure zostaną wyświetlone kolekcji używany cen warstwy standardowa.

![Jak tooconfirm kolekcji ma warstwy cenowej standardowa toohello migracji](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Jak przeprowadzić migrację z hello S1, S2, S3 kolekcjami partycji toosingle poziomów wydajności na własną?

Można migrować z hello S1, S2, a kolekcje partycji toosingle przy użyciu portalu Azure hello poziomy wydajności S3 lub programowo. Można to zrobić na własnych przed 1 sierpnia toobenefit z hello przepływności elastyczne opcje kolekcje z jedną partycją lub będziemy kolekcji można migrować na 31 lipca 2017 r.

**kolekcje z partycją toosingle toomigrate przy użyciu hello portalu Azure**

1. W hello [ **portalu Azure**](https://portal.azure.com), kliknij przycisk **bazy danych Azure rozwiązania Cosmos**, następnie wybierz hello DB rozwiązania Cosmos konta toomodify. 
 
    Jeśli **bazy danych Azure rozwiązania Cosmos** nie jest na hello przechodzenia kliknij pozycję >, przewiń zbyt**baz danych**, wybierz pozycję **bazy danych Azure rozwiązania Cosmos**, a następnie wybierz konto usługi DocumentDB hello.  

2. W menu zasobów hello w obszarze **kontenery**, kliknij przycisk **skali**, wybierz z listy rozwijanej hello hello toomodify kolekcji, a następnie kliknij przycisk **warstwy cenowej**. Konta przy użyciu wstępnie zdefiniowanych przepływności mają warstwy cenowej S1, S2 lub S3.  W hello **wybierz warstwę cenową** bloku, kliknij przycisk **standardowe** toochange zdefiniowane toouser przepływności, a następnie kliknij przycisk **wybierz** toosave zmiany.

    ![Zrzut ekranu przedstawiający blok ustawień hello pokazujący, gdzie toochange hello wartość przepływności](./media/performance-levels/change-performance-set-thoughput.png)

3. Po powrocie do hello **skali** bloku, hello **warstwy cenowej** zostanie zmieniona zbyt**standardowe** i hello **przepływności (RU/s)** zostanie wyświetlone okno z Wartość domyślna 400. Zestaw hello przepływności od 400 do 10 000 [jednostek żądania](request-units.md)/second (RU/s). Witaj **Szacowana kwota rachunku miesięczne** u dołu hello hello strony automatycznie aktualizuje tooprovide szacunkową hello koszt co miesiąc. 

    >[!IMPORTANT] 
    > Po zapisaniu zmian i przenieść toohello warstwy cenowej standardowa, nie można wycofać toohello poziomy wydajności S1, S2 lub S3.

4. Kliknij przycisk **zapisać** toosave zmiany.

    Jeśli okaże się, że potrzebujesz więcej przepływności (większe niż 10 000 RU/s) lub więcej pamięci masowej (większe niż 10GB) można utworzyć kolekcję partycjonowaną. toomigrate kolekcji tooa podzielona na partycje Kolekcja jednej partycji, zobacz [migracji z jednej partycji toopartitioned kolekcji](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > Zmiana z tooStandard S1, S2 lub S3 może trwać too2 minut.
    > 
    > 

**kolekcje z partycją toosingle toomigrate przy użyciu zestawu .NET SDK hello**

Inną opcją w przypadku zmiany poziomów wydajności z kolekcji jest przez nasze zestawy SDK. W tej sekcji opisano tylko zmiana wydajności kolekcji poziomu przy użyciu naszych [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), ale hello proces jest podobny do naszych innych zestawów SDK.

Oto fragment kodu dla zmiana too5 przepływność kolekcji hello, 000 jednostek żądań na sekundę:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Odwiedź stronę [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview dodatkowe przykłady i Dowiedz się więcej o naszym metody oferta:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Jak m wpływ mam EA klienta?

Umowa EA klienci będą cen chronione do końca hello Umowa.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji o cenach i zarządzanie danymi za pomocą usługi Azure rozwiązania Cosmos bazy danych, zapoznaj się z tymi zasobami:

1.  [Partycjonowanie danych w bazie danych rozwiązania Cosmos](documentdb-partition-data.md). Zrozumieć różnicę hello kontenera jednej partycji i kontenery podzielonym na partycje, a także wskazówki dotyczące implementowania bezproblemowo partycjonowania tooscale strategii.
2.  [Cennik rozwiązania cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Więcej informacji na temat hello koszt obsługi przepływności i korzystanie z magazynu.
3.  [Jednostek żądania](request-units.md). Zrozumienie hello zużycie przepustowości dla różnych operacji typów, na przykład Odczyt, zapis zapytania.
