---
title: "aaaAzure DB rozwiązania Cosmos jako wartość klucza magazynu — omówienie koszt | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat niski koszt hello przy użyciu bazy danych Azure rozwiązania Cosmos jako magazyn wartości klucza."
keywords: "magazyn kluczy i wartości"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure DB rozwiązania Cosmos jako magazyn wartości klucza — koszt — omówienie

Azure DB rozwiązania Cosmos jest usługą bazy danych globalnie rozproszone i wiele modeli łatwe tworzenie aplikacji wysokiej dostępności, dużej skali. Domyślnie program Azure DB rozwiązania Cosmos automatycznie indeksuje wszystkie dane hello go wysyła strumień, wydajnie. Umożliwia to szybkie i spójne [SQL](documentdb-sql-query.md) (i [JavaScript](programming.md)) kwerendy dla każdego typu danych. 

Tym artykule opisano koszt hello Azure DB rozwiązania Cosmos do zapisu proste i operacje odczytu, gdy jest używany jako magazyn kluczy i wartości. Zapisu operacji zalicza się wstawienia, zastępuje, usuwa i upserts dokumentów. Oprócz zapewnienia wysokiej dostępności 99,99%, gwarantowane oferty Azure DB rozwiązania Cosmos < opóźnieniem 10 ms dla odczytów i < 15 ms opóźnienie hello (indeksowane), zapisuje na powitania 99-ty percentyl. 

## <a name="why-we-use-request-units-rus"></a>Dlaczego używamy jednostek żądania (RUs)

Azure wydajności bazy danych rozwiązania Cosmos jest oparta na powitania ilość elastycznie [jednostek żądania](request-units.md) (RU) dla hello partycji. Hello inicjowania obsługi administracyjnej jest drugiego stopnia szczegółowości i została zakupiona RUs na sekundę i RUs na minutę ([mylić z hello rozliczenia godzinowe toobe](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs należy traktować jako walutę upraszczającym hello przepływności wymagane dla aplikacji hello inicjowania obsługi administracyjnej. Klientów nie mają toothink z rozróżnianie między odczytu i zapisu jednostki pojemności. model jednej waluty Hello RUs tworzy efektywność tooshare pojemności hello udostępniane między odczyty i zapisy. Ten model elastycznie pojemności umożliwia tooprovide usługi hello przepływności przewidywalną i spójny gwarancji, małych opóźnień i wysokiej dostępności. Na koniec używamy RU toomodel przepływności, ale każdy elastycznie RU również ma zdefiniowanych ilość zasobów (pamięć, Core). RU/s nie jest tylko IOPS.

Jako system globalnie rozproszoną bazę danych bazy danych rozwiązania Cosmos jest hello tylko Azure usługa, która zapewnia SLA na opóźnienia, przepływności i spójności w dodanie toohigh dostępności. Przepływność Hello, które należy udostępnić jest stosowane tooeach regionów hello skojarzonych z Twoim kontem bazy danych DB rozwiązania Cosmos. Dla odczytów, DB rozwiązania Cosmos oferuje wiele dobrze zdefiniowany [poziomy spójności](consistency-levels.md) dla toochoose z. 

Hello poniższej tabeli hello liczba RUs wymagane tooperform odczytu i zapisu na podstawie rozmiaru dokumentu o rozmiarze 1KB i 100KBs transakcji.

|Rozmiar elementu|Odczyt 1|1 zapisu|
|-------------|------|-------|
|1 KB|1 RU|5 RUs|
|100 KB|10 RUs|50 RUs|

## <a name="cost-of-reads-and-writes"></a>Koszt odczyty i zapisy

Jeśli dostarczasz RU/s 1000 to kwoty too3.6m RU na godzinę i koszt $0.08 hello godziny (w Europie i hello US). Rozmiar dokumentu o rozmiarze 1KB, to oznacza, że będzie można korzystać z odczyty 3,6 m lub zapisuje 0,72 m (3.6mRU / 5) przy użyciu sieci udostępnionej przepływności. Znormalizowany toomillion odczytuje i zapisuje, hello koszt wyniesie odczyty /m 0,022 $ (0.08 $ / 3,6) i zapisuje 0.111 $/ m (0.08 $ / 0,72). Koszt Hello milionów staje się minimalny, jak pokazano w poniższej tabeli hello.

|Rozmiar elementu|1 mln odczytu|1 mln zapisu|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|


Większość hello podstawowych obiektów blob lub obiektu Magazyny usług opłatą $0,40 na milionów transakcji odczytu i 5 USD na transakcję milionów zapisu. Jeśli używane optymalnie, rozwiązania Cosmos bazy danych może być too98% tańszy niż te rozwiązania, (dla transakcji o rozmiarze 1KB).

## <a name="next-steps"></a>Następne kroki

Wkrótce nowe artykuły dotyczące optymalizacji Inicjowanie obsługi zasobów bazy danych Azure rozwiązania Cosmos. W międzyczasie hello uznać wolnego toouse naszych [Kalkulator RU](https://www.documentdb.com/capacityplanner).

