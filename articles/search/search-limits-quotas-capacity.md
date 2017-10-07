---
title: "limity aaaService w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Ograniczenia usługi używane do planowania pojemności i maksymalna limity żądań i odpowiedzi dla usługi Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Ograniczenia usługi w usłudze Azure Search
Maksymalne zawartości w pamięci masowej, obciążenia i ilości indeksów, dokumentów, a inne obiekty są zależne od tego, czy możesz [udostępnić usługi Azure Search](search-create-service-portal.md) w **wolne**, **podstawowe**, lub **standardowe** warstwy cenowej.

* **Bezpłatne** jest wielodostępne usług udostępnionych, która pochodzi z subskrypcją platformy Azure. Jest opcja dodatkowe — bezpłatnie dla istniejących subskrybentów, umożliwiający tooexperiment z usługą hello przed utworzeniem dla zasobów dedykowanych.
* **Podstawowe** zawiera dedykowany zasobów obliczeniowych dla obciążeń produkcyjnych na mniejszą skalę.
* **Standardowe** działa na dedykowanych maszyn o większej pojemności magazynu i przetwarzania na każdym poziomie. Standard składa się z czterech poziomów: S1, S2 S3 i o wysokiej gęstości S3 (S3 HD).

> [!NOTE]
> Usługa jest zainicjowana dla określonej warstwy. Tooget warstw toojump potrzebujesz większej pojemności, należy zapewnić nowej usługi (uaktualnienie w miejscu, nie istnieje). Aby uzyskać więcej informacji, zobacz [wybierz jednostki SKU lub warstwy](search-sku-tier.md). więcej informacji na temat dostosowywania wydajności w ramach usługi toolearn zostały już aprowizowanej, zobacz [skalowania zasobu poziomy kwerendy i indeksowania obciążeń](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Na limity subskrypcji
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Limity dla usług
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Na granicach indeksu
Brak odpowiednika między ograniczenia dotyczące indeksów i limity indeksatorów. Biorąc pod uwagę limit 200 indeksów, maksymalny limit indeksatory hello jest również 200 hello tę samą usługę.

| Zasób | Bezpłatna | Podstawowa | S1 | S2 | S3 | S3 (wysoka gęstość) |
| --- | --- | --- | --- | --- | --- | --- |
| Indeks: maksymalna pól w indeksie |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Indeks: maksymalny oceniania profil dla każdej z indeksu |100 |100 |100 |100 |100 |100 |
| Indeks: maksymalna funkcje dla profilu |8 |8 |8 |8 |8 |8 |
| Indeksatory: maksymalne obciążenie indeksowania dla wywołania |10 000 dokumentów |Ograniczone tylko dokumenty maksymalna |Ograniczone tylko dokumenty maksymalna |Ograniczone tylko dokumenty maksymalna |Ograniczone tylko dokumenty maksymalna |N/D <sup>2</sup> |
| Indeksatory: maksymalny czas działania | 1 – 3 minuty <sup>3</sup> |24 godziny |24 godziny |24 godziny |24 godziny |N/D <sup>2</sup> |
| Indeksator obiektów blob: rozmiar maksymalny obiektu blob, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indeksator obiektów blob: Maksymalna liczba znaków zawartości wyodrębniony z obiektu blob |32,000 |64,000 |4 miliony |4 miliony |4 miliony |N/D <sup>2</sup> |

<sup>1</sup> warstwy podstawowa jest hello tylko jednostki SKU z dolny limit 100 pól w indeksie.

<sup>2</sup> S3 HD nie obsługuje obecnie indeksatorów. Jeśli masz pilną potrzebę dla tej funkcji, skontaktuj się z pomocą techniczną platformy Azure.

<sup>3</sup> indeksatora maksymalny czas wykonywania warstwę bezpłatna hello jest 3 minuty źródła obiektów blob i 1 minuty dla wszystkich źródeł danych.

## <a name="document-size-limits"></a>Limity rozmiaru dokumentu
| Zasób | Bezpłatna | Podstawowa | S1 | S2 | S3 | S3 (wysoka gęstość) |
| --- | --- | --- | --- | --- | --- | --- |
| Rozmiar poszczególnych dokumentu na indeks interfejsu API |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |

Odwołuje się rozmiar maksymalny dokumentu toohello podczas wywoływania indeksu interfejsu API. Rozmiar dokumentu jest rzeczywiście limit rozmiaru hello hello treści żądania interfejsu API indeksu. Ponieważ jednocześnie można przekazać partii wielu dokumentów toohello indeksu interfejsu API, limit rozmiaru hello faktycznie zależy liczby dokumentów w partii hello. Dla partii z pojedynczego dokumentu rozmiar maksymalny dokumentu hello jest 16 MB JSON.

rozmiar dokumentu tookeep, pamiętaj tooexclude-kolejność danych z hello żądania. Obrazy i inne dane binarne nie są bezpośrednio zapytań i nie powinny być przechowywane w hello indeksu. toointegrate-kolejność danych w wynikach wyszukiwania, zdefiniuj niemożliwych pole, które przechowuje zasobu toohello odwołanie do adresu URL.

## <a name="workload-limits-queries-per-second"></a>Limity obciążenia (zapytania na sekundę)
| Zasób | Bezpłatna | Podstawowa | S1 | S2 | S3 | S3 (wysoka gęstość) |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |Nie dotyczy |Około 3 na replikę |Około 15 na replikę |Około 60 na replikę |Ponad 60 na replikę |Ponad 60 na replikę |

Zapytania na sekundę (QPS) jest przybliżenie oparte na algorytmy heurystyczne, przy użyciu klienta symulowanych i rzeczywistych obciążeń tooderive szacowane wartości. Dokładne przepływności QPS różni się w zależności od Twoje dane i hello rodzaj hello zapytania.

Mimo że szacunkowe podano powyżej, rzeczywista szybkość jest trudne toodetermine, szczególnie w hello wolne udostępnionej usługi, której przepływności na podstawie dostępnej przepustowości i konkurowanie o zasoby systemowe. Warstwa bezpłatna hello, zasobów obliczeniowych i magazynu są współużytkowane przez wielu subskrybentów, zawsze będą się różnić w zależności od tego, jak wiele innych obciążeń uruchomionych na powitania QPS dla rozwiązania tym samym czasie.

Na poziomie standardowa hello można oszacować QPS więcej ściśle ponieważ mają kontrolę nad jednego z parametrów hello. W sekcji hello najlepszych praktyk w [Zarządzanie rozwiązania wyszukiwania](search-manage.md) wskazówki na temat toocalculate QPS dla obciążeń.

## <a name="api-request-limits"></a>Limity żądań interfejsu API
* Maksymalnie 16 MB na żądanie <sup>1</sup>
* Maksymalna długość adresu URL 8 KB
* Maksymalna 1000 dokumentów na partię indeksu przekazuje, scala lub usuwanie
* Maksymalny 32 pola w klauzuli $orderby
* Rozmiar termin wyszukiwania maksymalna to 32 766 bajtów (32 KB minus 2 bajty) tekstu kodowany w formacie UTF-8

<sup>1</sup> w usłudze Azure Search hello treść żądania jest podmiotu tooan górny limit 16 MB, nakładające praktyczne limit na powitania zawartość poszczególnych pól lub kolekcje, które w przeciwnym razie nie są ograniczone przez teoretycznego limity (zobacz [obsługiwane typy danych](https://msdn.microsoft.com/library/azure/dn798938.aspx) uzyskać więcej informacji dotyczących ograniczenia i pola kompozycji).

## <a name="api-response-limits"></a>Limity odpowiedzi interfejsu API
* Maksymalna 1000 zwrócone na stronę wyników wyszukiwania
* Maksymalną 100 sugestie zwracane zgodnie z żądaniem Sugeruj interfejsu API

## <a name="api-key-limits"></a>Limity klucz interfejsu API
Klucze interfejsu API są używane do uwierzytelniania usługi. Istnieją dwa typy. Administrator klucze są określone w nagłówku żądania hello i przyznać dostęp do odczytu zapisu toohello usługi. Klucze zapytania są tylko do odczytu, określony adres URL hello i aplikacji rozproszonych zwykle tooclient.

* Maksymalnie 2 kluczy administratora usługi
* Maksymalnie 50 kluczy zapytania dla usługi
