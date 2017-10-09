---
title: "Jednostka SKU aaaChoose lub warstwy cenowej dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Usługa wyszukiwanie Azure można udostępnić w tych jednostki SKU: bezpłatne, Basic i Standard, gdzie Standard jest dostępna w różne konfiguracje zasobów i pojemności, poziomów."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Wybieranie jednostki SKU lub warstwy cenowej usługi Azure Search
W usłudze Azure Search [usługi zostanie zainicjowana](search-create-service-portal.md) w określonych warstwę cenową lub jednostki SKU. Dostępne są następujące opcje **wolne**, **podstawowe**, lub **standardowe**, gdzie **standardowe** są dostępne w wielu konfiguracjach i pojemności.

Celem tego artykułu Hello jest toohelp wybierz warstwę. Jeśli pojemność warstwy okaże się toobe zbyt niska, będzie konieczne tooprovision nową usługę na powitania wyższego poziomu, a następnie ponownie załaduj z indeksów. Nie jest uaktualnienie w miejscu nie hello usługi takie same z jednym tooanother jednostki SKU.

> [!NOTE]
> Po wybraniu warstwy i [alokowanie usługi wyszukiwania](search-create-service-portal.md), można zwiększyć repliki i liczby partycji w ramach usługi hello. Aby uzyskać instrukcje, zobacz [skalowania zasobu poziomy kwerendy i indeksowania obciążeń](search-capacity-planning.md).
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Jak tooapproach cen warstwy decyzji
W usłudze Azure Search warstwy hello określa pojemności, nie dostępności funkcji. Ogólnie rzecz biorąc funkcje są dostępne w każdej warstwy, włączając funkcje w wersji zapoznawczej. Jedynym wyjątkiem Hello nie jest obsługiwane dla indeksatorów w S3 HD.

> [!TIP]
> Firma Microsoft zaleca, aby zawsze udostępnieniem **wolne** usługi (po jednym dla każdego subskrypcji bez terminu wygaśnięcia), aby jego łatwo dostępne dla projektów lekki. Użyj hello **wolne** usługi do testowania i oceny; Utwórz drugi usługą płatną na powitania **podstawowe** lub **standardowe** warstwy do produkcji lub większych obciążeń testu.
>
>

Pojemność i kosztów działających usługi hello go ręcznie dostępnych. Informacje w tym artykule mogą pomóc zdecydować, który SKU dostarcza odpowiednią równowagę między hello, ale dla każdego z nich toobe przydatne, potrzebujesz co najmniej szacunkowe powitania po:

* Liczba i rozmiar indeksów planujesz toocreate
* Liczba i rozmiar tooupload dokumentów
* Niektóre informacje o tym wielkości zapytania pod względem zapytania na drugie (QPS)

Liczba i rozmiar są ważne, ponieważ osiągnięto maksymalny limit za pośrednictwem nienaruszalne ograniczenie liczby hello indeksy lub dokumentów w usłudze lub zasobów (repliki lub magazynu) używany przez usługę hello. Witaj rzeczywiste limitu dla Twojej usługi jest pobiera zależności używany na pierwszym: zasobów lub obiektów.

Szacunkowe w ręcznie hello następujące kroki, należy uprościć proces hello:

* **Krok 1** Przejrzyj opisy SKU hello poniżej toolearn o dostępnych opcjach.
* **Krok 2** odpowiedzi na pytania hello poniżej tooarrive na wstępne decyzji.
* **Krok 3** Finalize zdecydować, czy przeglądanie limity stałe w magazynie i cenach.

## <a name="sku-descriptions"></a>Opisy jednostki SKU
Witaj w poniższej tabeli przedstawiono opis każdej warstwy.

| Warstwa | Podstawowe scenariusze |
| --- | --- |
| **W warstwie bezpłatna** |Usługa udostępnionego, bez żadnych opłat, używany do oceny, dochodzenia lub małych obciążeń. Ponieważ są one udostępniane innym użytkownikom, przepływności zapytania i indeksowania w zależności od kogo jeszcze jest za pomocą usługi hello. Pojemność jest mała (50 MB lub 3 indeksów z się 10 000 dokumentów każdego). |
| **Podstawowa** |Obciążeń produkcyjnych małych na dedykowanym sprzęcie. Wysokiej dostępności. Pojemność jest too3 repliki i 1 partycji (2 GB). |
| **S1** |Standardowa 1 obsługuje elastyczne kombinacje partycji (12) i repliki (12), używany w przypadku obciążeń produkcyjnych średnia na dedykowanym sprzęcie. Możesz przydzielić partycji i replik w kombinacji obsługiwane przez maksymalną liczbę jednostek wyszukiwania rozliczeniowy 36. Na tym poziomie partycje są 25 GB i QPS jest około 15 zapytania na sekundę. |
| **S2** |Standardowy 2 jest uruchamiane przy użyciu jednostek wyszukiwania hello 36 tej samej, jak S1, ale większy rozmiar partycji i replik większych obciążeń produkcyjnych. Na tym poziomie partycje są 100 GB i QPS jest około 60 zapytania na sekundę. |
| **S3** |Standardowa 3 działa proporcjonalnie większych obciążeń produkcyjnych w systemach wyższej zakończenia w konfiguracjach too12 partycji i replik 12 jednostek wyszukiwania w obszarze 36. Na tym poziomie partycje są 200 GB i QPS jest więcej niż 60 zapytania na sekundę. |
| **S3 HD** |Standardowa 3 o wysokiej gęstości jest przeznaczona dla dużej liczby mniejsze indeksów. Użytkownik może zawierać maksymalnie too3 partycji, co 200 GB. QPS jest więcej niż 60 zapytania na sekundę. |

> [!NOTE]
> Maksymalne wartości repliki i partycji są rozliczane się jako jednostek wyszukiwania (36 jednostka maksymalną dla danej usługi), które nakłada skuteczne niższej niż maksymalna jakie hello oznacza na wartość przedniej. Na przykład toouse hello maksymalnie 12 replik, może mieć co najwyżej 3 partycji (12 * 3 = 36 jednostek). Podobnie toouse maksymalną partycji, Zmniejsz too3 repliki. Zobacz [skalować poziomy zasobów dla zapytania i obciążeń w usłudze Azure Search indeksowanie](search-capacity-planning.md) wykresu w dozwolonym kombinacji.
>
>

## <a name="review-limits-per-tier"></a>Przejrzyj limity dla warstwy
Witaj następujący plan jest podzbiorem limitów hello z [ograniczenia usługi w usłudze Azure Search](search-limits-quotas-capacity.md). Wyświetla listę hello czynniki najprawdopodobniej tooimpact decyzji jednostki SKU. Podczas przeglądania hello poniższe pytania mogą odwoływać się toothis wykresu.

| Zasób | Bezpłatna | Podstawowa | S1 | S2 | S3 | S3 (wysoka gęstość) |
| --- | --- | --- | --- | --- | --- | --- |
| Umowa dotycząca poziomu usług (SLA) |Nie<sup>1</sup> |Tak |Tak |Tak |Tak |Tak |
| Limity indeksu |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Limity dokumentów |10 000 łącznie |1 mln dla usługi |15 milionów dla każdej partycji |60 milionów dla każdej partycji |120 milionów dla każdej partycji |1 mln w indeksie |
| Maksymalna partycji |Nie dotyczy |1 |12 |12 |12 |3<sup>2</sup> |
| Rozmiar partycji |Całkowita liczba 50 MB |2 GB na usługi |25 GB dla jednej partycji |100 GB dla jednej partycji (w górę tooa maksymalnie 1,2 TB na usługę) |200 GB dla jednej partycji (w górę tooa maksymalnie 2.4 TB na usługę) |200 GB (w górę tooa maksymalnie 600 GB dla usługi) |
| Maksymalna repliki |Nie dotyczy |3 |12 |12 |12 |12 |
| Zapytania na sekundę |Nie dotyczy |Około 3 na replikę |Około 15 na replikę |Około 60 na replikę |Ponad 60 na replikę |Ponad 60 na replikę |

<sup>1</sup> bezpłatnej warstwy i Podgląd funkcji nie pochodzą z umów dotyczących poziomu usług (SLA). Dla wszystkich warstw rozliczeniowy umowy SLA zaczną obowiązywać podczas obsługi administracyjnej nadmiarowość wystarczające dla Twojej usługi. Co najmniej dwa repliki są wymagane do umowy SLA kwerendy (odczyt). Co najmniej trzech repliki są wymagane dla zapytań i indeksowania SLA (odczytu i zapisu). Hello liczby partycji nie jest brany pod uwagę umowy dotyczącej poziomu usług. 

<sup>2</sup> S3 i S3 HD obsługiwanych przez infrastrukturę identyczne dużej pojemności, ale każda z nich osiągnie limit maksymalny na różne sposoby. S3 dotyczy mniejszą liczbę bardzo dużych indeksów. W efekcie jej maksymalny limit jest powiązany z zasobów (2.4 TB dla każdej usługi). S3 HD dotyczy duża liczba indeksów bardzo mała. W indeksach 1000 S3 HD osiągnięty limit w postaci hello ograniczeń indeksu. Jeśli klient S3 HD, który wymaga więcej niż 1000 indeksów, skontaktuj się z Microsoft Support informacji na temat tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Eliminowanie jednostki magazynowe, które nie spełniają wymagań
Witaj następujące pytania mogą pomóc przyjeździe hello właściwa decyzja jednostki SKU dla obciążenia.

1. Czy masz **Umowa dotycząca poziomu usług (SLA)** wymagania? Można użyć dowolnego rozliczeniowy warstwy (podstawowe w górę), ale konieczne jest skonfigurowanie usługi w celu zapewnienia nadmiarowości. Co najmniej dwa repliki są wymagane do umowy SLA kwerendy (odczyt). Co najmniej trzech repliki są wymagane dla zapytań i indeksowania SLA (odczytu i zapisu). Hello liczby partycji nie jest brany pod uwagę umowy dotyczącej poziomu usług.
2. **Jak wiele indeksów** czy potrzebne? Jednym z hello zmienne największych factoring do decyzji jednostka SKU jest hello liczba indeksów obsługiwanych przez każdy jednostki SKU. Obsługa indeksu jest znacząco różną w dolnym hello warstw cenowych. Wymagania dotyczące liczba indeksów można decydujące podstawowy SKU decyzji.
3. **Jak wiele dokumentów** zostaną załadowane do każdego indeksu? hello liczby i rozmiaru dokumentów określi rozmiar hello hello indeksu. Przy założeniu, że można oszacować hello planowanego rozmiar hello indeksu, możesz porównać numer przed rozmiar partycji hello na SKU przedłużony hello liczba partycji wymagane toostore indeks tego rozmiaru.
4. **Co to jest hello zapytania oczekiwanego obciążenia**? Gdy wymagania dotyczące magazynu są zrozumiałe, należy wziąć pod uwagę obciążeń zapytania. S2 i obu SKU S3 oferują niemal równoważne przepływności, ale wymaganiami SLA będzie wykluczyć wszystkie jednostki SKU w wersji zapoznawczej.
5. Planując hello S2 lub warstwy S3, określić, czy jest wymagany [indeksatory](search-indexer-overview.md). Indeksatory nie są jeszcze dostępne dla warstwy S3 HD hello. Informacje o innym podejściu jest toouse modelu wypychania aktualizacji indeksu, w którym można zapisywać toopush kodu aplikacji indeksu tooan zestawu danych.

Większość klientów może reguł określonych SKU przychodzący lub wychodzący oparte na ich toohello odpowiedzi powyżej pytania. Jeśli nadal nie masz pewności które toogo jednostki SKU z, możesz tooMSDN pytania lub fora StackOverflow lub się z pomocą techniczną platformy Azure, aby uzyskać dalsze informacje.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>Decyzja sprawdzania poprawności: hello SKU oferuje wystarczającej ilości miejsca i QPS?
Jako ostatni etap ponownie hello [cennikiem](https://azure.microsoft.com/pricing/details/search/) i hello [sekcje-service i na indeks ograniczenia usługi](search-limits-quotas-capacity.md) toodouble wyboru oszacowania przed limity subskrypcji i usług.

Jeśli wymagania cen lub magazynem albo hello są poza zakresem, może zaistnieć toorefactor hello obciążenia między wieloma usługami mniejsze (na przykład). Na bardziej szczegółowym poziomie można zmodyfikowanie toobe indeksów jest mniejsza, lub Użyj filtrów kwerendy toomake bardziej wydajne.

> [!NOTE]
> Wymagania dotyczące magazynu może być nadmiernie nadmuchany, jeśli dokumenty zawierają nadmiarowe dane. W idealnym przypadku dokumenty zawierają tylko dane z możliwością wyszukiwania lub metadanych. Dane binarne jest niemożliwych i powinny być przechowywane oddzielnie (np. w tabeli lub obiektu blob magazynu Azure) z polem w toohold indeksu hello adresu URL danych zewnętrznych toohello odwołania. Hello maksymalny rozmiar poszczególnych dokumentu jest 16 MB lub mniej Jeśli jesteś zbiorczego przekazywania wielu dokumentów w jedno żądanie. Zobacz [usługi limity w usłudze Azure Search](search-limits-quotas-capacity.md) Aby uzyskać więcej informacji.
>
>

## <a name="next-step"></a>Następny krok
Po sprawdzeniu, którego jednostka SKU jest hello mieści się po prawej, nadal dalszych kroków:

* [Utwórz usługę wyszukiwania, w portalu hello](search-create-service-portal.md)
* [Zmień hello Alokacja tooscale partycji i replik usługi](search-capacity-planning.md)
