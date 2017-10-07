---
title: "aaaCapacity planowania dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Dostosuj partycji i replik zasobów komputera w usłudze Azure Search, gdzie w jednostkach rozliczeniowy wyszukiwania kosztuje każdego zasobu."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Poziomy zasobów skali kwerendy i indeksowania obciążeń w usłudze Azure Search
Po [wybierz warstwę cenową](search-sku-tier.md) i [alokowanie usługi wyszukiwania](search-create-service-portal.md), hello następnym krokiem jest toooptionally wzrost hello liczby replik lub partycje używane przez usługę. Każda warstwa oferuje ustalona liczba jednostek rozliczeń. W tym artykule opisano sposób tooallocate tooachieve tych jednostek optymalną konfigurację, który równoważy wymagania dotyczące wykonywania zapytania, indeksowanie i magazynu.

Konfiguracja zasobu jest dostępna podczas konfigurowania usługi na powitania [warstwy Basic](http://aka.ms/azuresearchbasic) lub jednego z hello [warstwy standardowa](search-limits-quotas-capacity.md). W przypadku rozliczeniowy usług w tych warstwach pojemności jest zakupić według przyrostów *jednostek wyszukiwania* (SUs) gdzie każdej partycji i replik liczone jako jeden SU. 

Użycie mniejszej liczby powoduje SUs rachunek proporcjonalnie niższa. Karta jest włączona dla tak długo, jak usługa hello jest skonfigurowana. Jeśli tymczasowo nie jest używana usługa hello tylko sposób rozliczeń tooavoid przez usunięcie usługi hello i następnie ponownie go utworzyć w razie konieczności.

> [!Note]
> Usunięcie usługi spowoduje usunięcie wszystkich na nim. Nie istnieje żadne funkcje w ramach usługi Azure Search do wykonywania kopii zapasowych i przywracanie utrwalone wyszukiwania danych. tooredeploy istniejący indeks na nowej usługi, uruchom toocreate program używany hello i pierwotnie go załadować. 

## <a name="terminology-partitions-and-replicas"></a>Terminologią: partycji i replik
Partycji i replik są zasoby głównej hello, które wykonują kopie usługi wyszukiwania.

| Zasób | Definicja |
|----------|------------|
|*Partycje* | Udostępnia magazynu indeksu i we/wy dla operacji odczytu/zapisu (na przykład podczas odbudowywania lub odświeżanie indeks).|
|*Repliki* | Wystąpienia usługi wyszukiwania hello, używany głównie tooload operacje kwerend równowagi. Każda replika zawsze obsługuje jedną kopię indeksu. Jeśli masz 12 replik, masz 12 kopie każdy indeks załadowany na powitania usługi.|

> [!NOTE]
> Nie istnieje sposób toodirectly obsługi i zarządzania, które indeksy Uruchom na replice. Jedna kopia każdy indeks dla każdej repliki jest częścią architektury usługi hello.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Jak tooallocate partycji i replik
Usługi w usłudze Azure Search początkowo jest przydzielany minimalny poziom zasobów składające się z jednej partycji i replik jednej. Dla warstwy, które obsługują tę przyrostowo można dostosować zasoby obliczeniowe, zwiększając partycji, jeśli wymagają więcej pamięci masowej i we/wy, lub Dodaj więcej replik większych woluminów zapytania lub lepszą wydajność. Usługa rejestracji musi mieć wystarczające zasoby toohandle wszystkich obciążeń (indeksowanie i kwerend). Nie można podzielić obciążenia między wieloma usługami.

tooincrease lub zmień przydział hello replik i partycji, firma Microsoft zaleca używanie hello portalu Azure. Hello portal wymusza limity dopuszczalny kombinacje, które pozostają poniżej maksymalny limit:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz usługę wyszukiwania hello.
2. W **ustawienia**, otwórz hello **skali** bloku i użyj hello tooincrease suwaki lub zmniejszyć liczbę hello partycji i replik.

Jeśli potrzebujesz opartych na skryptach lub oparte na kodzie metody inicjowania obsługi administracyjnej hello [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn832687.aspx) portalu toohello alternatywnych.

Ogólnie rzecz biorąc wyszukiwanie aplikacji muszą replik więcej niż partycje, szczególnie w przypadku, gdy operacje usług hello są ukierunkowane kierunku obciążeń zapytania. Witaj w sekcji [wysokiej dostępności](#HA) zawiera informacje o przyczynie.

> [!NOTE]
> Po zainicjowaniu obsługi usługi, nie może być uaktualniony tooa nowszej wersji produktu. Będzie konieczne toocreate usługi wyszukiwania na nową warstwę hello i załaduj ponownie z indeksów. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) Aby uzyskać pomoc dotyczącą usługi udostępniania.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Wysoka dostępność
Ponieważ jest bardzo proste i względnie szybkie tooscale w górę, ogólnie zalecamy czy uruchomić jedną partycję oraz jedną lub dwie repliki, a następnie skalowania w górę jako woluminy zapytania kompilacji. Dla wielu usług w warstwach Basic lub S1 hello jedną partycję miejsce wystarczające magazynu i operacji We/Wy (co 15 milionów dokumentów na partycję).

Uruchom zapytanie obciążeń głównie w replikach. Jeśli potrzebujesz więcej przepustowości lub wysoką dostępność, prawdopodobnie będzie wymagać dodatkowych replik.

Ogólne zalecenia dotyczące wysokiej dostępności są:

* Dwie repliki wysokiej dostępności obciążeń tylko do odczytu (queries)
* Co najmniej trzech replik wysokiej dostępności obciążeń odczytu/zapisu (kwerend oraz indeksowania podczas dodawania, aktualizacji lub usuwania pojedyncze dokumenty)

Umowy dotyczące poziomu usług (SLA) dla usługi wyszukiwanie Azure są przeznaczone dla operacji zapytań i indeksu aktualizacje, które składają się z Dodawanie, aktualizowanie lub usuwanie dokumentów.

### <a name="index-availability-during-a-rebuild"></a>Indeks dostępności podczas kompilowania

Wysoka dostępność dla usługi Azure Search dotyczy tooqueries i pod indeksem aktualizacje, które nie obejmują odbudowanie indeksu. Usuwanie pola, Zmień typ danych lub zmień nazwę pola, należy najpierw toorebuild hello indeksu. Indeks hello toorebuild, należy usunąć hello indeks, Utwórz ponownie indeks hello i załaduj ponownie dane hello.

> [!NOTE]
> Można dodać nowego indeksu usługi Azure Search tooan pól bez odbudowanie indeksu hello. wartość Hello hello nowe pole będzie równy null dla wszystkich dokumentów już w indeksie hello.

toomaintain indeksu dostępności podczas kompilowania, musi mieć kopię hello indeksu o innej nazwie na powitania sama usługa, lub kopię hello indeksu z hello sama nazwa na inną usługę, a następnie podaj przekierowania lub pracy awaryjnej logikę w kodzie.

## <a name="disaster-recovery"></a>Odzyskiwanie po awarii
Obecnie nie istnieje wbudowany mechanizm odzyskiwania po awarii. Dodawanie repliki lub partycje będą hello strategii niewłaściwy realizacji celów odzyskiwania po awarii. najbardziej typowym podejściem Hello jest tooadd nadmiarowości na poziomie usługi hello poprzez ustawienie drugi Usługa wyszukiwania w innym regionie. Podobnie jak w przypadku dostępności podczas odbudowywania indeksu, przekierowywanie hello lub logiki trybu failover muszą pochodzić z kodu.

## <a name="increase-query-performance-with-replicas"></a>Zwiększ wydajność zapytań z replikami
Opóźnienie kwerendy jest wskaźnik potrzebne są dodatkowe repliki. Ogólnie rzecz biorąc pierwszym krokiem procesu poprawę wydajności zapytań jest tooadd więcej zasobów. Podczas dodawania replik dodatkowych kopii indeksu hello są przełączony w tryb online toosupport większych obciążeń zapytania i hello saldo tooload żądania hello wiele replik.

Nie możemy przekazać twardych szacuje na zapytania na sekundę (QPS): zapytania wydajność zależy od złożoności hello hello zapytań i konkurencyjnych obciążeń. Średnio repliki na podstawowym lub jednostki SKU S1 może obsłużyć QPS około 15, ale przepustowość sieci jest wyższe lub niższe w zależności od złożoności kwerendy (aspektowej zapytania są bardziej złożonych) i opóźnienie sieci. Jest także toorecognize, że chociaż Dodawanie repliki doda ostatecznie skalowalność i wydajność, hello wynik nie jest liniowa ściśle ważne: dodanie trzy repliki nie gwarantuje Potrójna przepływności.

toolearn o QPS podejścia do oszacowania QPS dla obciążeń, w tym temacie [Zarządzanie usługą wyszukiwania](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Zwiększ wydajność indeksowania partycji
Aplikacji wyszukiwania, które wymagają niemal odświeżanie danych w czasie rzeczywistym, należy proporcjonalnie więcej partycji niż replik. Dodawanie partycji rozprzestrzenia operacji odczytu/zapisu w większej liczby zasobów obliczeniowych. Również daje więcej miejsca na dysku do przechowywania dodatkowych indeksów oraz dokumentów.

Indeksy większe trwać dłużej tooquery. Tak może się okazać, że każdy dodatkowe zwiększenie partycji wymaga mniejsze, ale proporcjonalny wzrost replik. złożoność Hello woluminu zapytania i zapytań będzie uwzględnić szybkość wykonywania zapytania jest włączona.

## <a name="basic-tier-partition-and-replica-combinations"></a>Warstwa podstawowa: kombinacji partycji i replik
Podstawowa usługa można mieć dokładnie jedną partycję i replik toothree maksymalnie trzy SUs. zasób tylko regulowany Hello jest replik. Należy co najmniej dwóch replik wysokiej dostępności na kwerendach.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Standardowa warstw: kombinacji partycji i replik
W poniższej tabeli przedstawiono hello SUs wymagane toosupport kombinacji repliki i partycji, podmiotu toohello 36 SU limit, wszystkie warstwy standardowa.

|   | **1 partycji** | **partycje 2** | **3 partycji** | **partycje 4** | **partycje 6** | **partycje 12** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 repliki** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 replik** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **repliki 3** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 replik** |4 SU |8 SU |12 SU |16 SU |24 SU |Nie dotyczy |
| **5 repliki** |5 SU |10 SU |15 SU |20 SU |30 SU |Nie dotyczy |
| **6 repliki** |6 SU |12 SU |18 SU |24 SU |36 SU |Nie dotyczy |
| **12 repliki** |12 SU |24 SU |36 SU |Nie dotyczy |Nie dotyczy |Nie dotyczy |

SUs, ceny i pojemność są szczegółowo opisane w na powitania witrynie systemu Azure. Aby uzyskać więcej informacji, zobacz [szczegóły cennika](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> Liczba Hello repliki i partycji dzieli bez reszty do 12 (w szczególności 1, 2, 3, 4, 6, 12). Jest to spowodowane usługi Azure Search wstępnie dzieli każdy indeks na odłamków 12, dzięki czemu mogą być rozkładu w równe części wszystkich partycji. Na przykład jeśli usługa ma trzy partycje, Utwórz indeks każda partycja zawiera cztery odłamków hello indeksu. Jak odłamków usługi Azure Search jako indeks jest szczegółów implementacji, toochange podmiotu w przyszłych wersjach. Mimo że numer hello 12 dzisiaj, prawdopodobnie nie powinien który number tooalways należeć 12 hello przyszłych.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Formuła rozliczeń dla repliki i partycji zasobów
Formuła Hello obliczania SUs liczby są używane dla określonej kombinacji jest iloczyn hello repliki i partycji, lub (R X P = SU). Na przykład trzech replik pomnożona przez trzy partycje jest on rozliczany jako dziewięć SUs.

Koszt SU jest określany przez warstwę hello, o mniejszej szybkości rozliczeń jednostkę Basic niż dla standardowej. Ocenia dla każdej warstwy można znaleźć na [szczegóły cennika](https://azure.microsoft.com/pricing/details/search/).
