---
title: "aaaLearn o operacjach usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Elastyczność usługi SQL Data Warehouse pozwala powiększać, zmniejszać lub wstrzymywać moc obliczeniową przy użyciu ruchomej skali jednostek magazynu danych (jednostki DWU). W tym artykule opisano metryki magazynu danych hello i ich relacji tooDWUs. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Obciążenie magazynu danych
Obciążenie magazynu danych odwołuje się tooall hello działań, wykonywanych w magazynie danych. Obciążenie magazynu danych Hello uwzględnia cały proces ładowania danych do magazynu hello, wykonywanie analiz i raportowania w magazynie danych hello zarządzanie danymi w magazynie danych hello i eksportowanie danych z magazynu danych hello hello. Witaj zaawansowania i zasięgu tych składników często są proporcjonalnie do poziomu dojrzałości hello hello hurtowni danych.

## <a name="new-toodata-warehousing"></a>Nowe magazynów toodata?
Magazyn danych to kolekcja danych, które są ładowane z jedną lub więcej danych źródła, a także jest używane tooperform zadań analizy biznesowej, takich jak raportowanie i analiza danych.

Cechą magazynów danych są zapytania, które skanują dużą liczbę wierszy, uwzględniają szerokie zakresy danych i mogą zwracać stosunkowo duże wyniki hello w celach analizy i raportowania. Charakterystyczne dla magazynów danych jest również ładowanie stosunkowo dużej ilości danych w porównaniu z operacjami wstawiania/aktualizowania/usuwania na niskim poziomie transakcji.

* Magazyn danych sprawdza się najlepiej, gdy hello dane są przechowywane w taki sposób, który optymalizuje zapytania tooscan dużej liczby wierszy lub duże zakresy danych. Ten typ skanowania działa najlepiej, gdy hello dane są przechowywane i przeszukiwane według kolumn, a nie według wierszy.

> [!NOTE]
> Indeks magazynu kolumn w pamięci Hello, który używa magazynu kolumn, zapewnia większe wzmocnienie kompresji too10x i 100 x większe wzmocnienie wydajności zapytań za pośrednictwem tradycyjnych drzew binarnych raportowania i zapytań analiz. Firma Microsoft indeksy magazynu kolumn jako hello standard przechowywania i skanowania dużej ilości danych w magazynie danych.
> 
> 

* Magazyn danych ma inne wymagania niż system, który jest zoptymalizowany do przetwarzania transakcji online (OLTP). Witaj OLTP system ma wiele Wstawianie, aktualizowanie i usuwanie operacji. Te operacje dążą toospecific wierszy w tabeli hello. Działania wyszukiwania tabeli są wykonywane najlepiej, jeśli dane hello są przechowywane w sposób wiersz po wierszu. dane Hello można sortować i szybko za rozdzielaniu i zajmowaniu o nazwie wyszukiwanie binarne drzewa lub btree.

## <a name="data-loading"></a>Ładowanie danych
Ładowanie danych jest dużą część obciążenia magazynu danych hello. Firmy zwykle mają zajęty system OLTP, który śledzi zmiany w ciągu dnia hello, gdy klienci generują transakcje biznesowe. Okresowo często w nocy, podczas okna obsługi, hello transakcje są przenoszone lub kopiowane toohello hurtowni danych. Po hello danych w magazynie danych hello analityków można wykonywać analizy i podejmować decyzje biznesowe dotyczące danych hello.

* Tradycyjnie proces ładowania hello jest wywoływana ETL dla wyodrębniania, przekształcania i ładowania. Zwykle dane muszą toobe przekształcone, aby były zgodne z innymi danymi w magazynie danych hello. Wcześniej w firmach używano dedykowanych przekształcenia hello tooperform serwerów ETL. Teraz takie szybkiemu, równoległemu przetwarzaniu można najpierw załadować dane do usługi SQL Data Warehouse i następnie wykonać transformacje hello. Ten proces jest nazywany wyodrębniania, obciążenia i przekształcenie (ELT) i staje się nowy standard hello obciążenia pracą z magazynu danych.

> [!NOTE]
> Za pomocą serwera SQL Server 2016 można teraz wykonywać analizy w czasie rzeczywistym w tabeli OLTP. To nie Zastąp hello potrzebę toostore magazynu danych i analizować dane, ale zapewnia analizy tooperform sposób, w czasie rzeczywistym.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Zapytania raportowe i analityczne
Zapytania raportowe i analityczne są często dzielone na kategorie (małe, średnie i duże) na podstawie różnych kryteriów, ale najczęściej na podstawie kryterium czasu. W większości magazynów danych obciążenie ma charakter mieszany i zawiera zarówno zapytania krótkie, jak i długotrwałe. W każdym przypadku jest ważne toodetermine tej mieszanki oraz toodetermine jej częstotliwość (co godzinę, codziennie, koniec miesiąca, koniec kwartału i tak dalej). Jest ważne toounderstand, który hello obciążenie mieszanymi zapytaniami w połączeniu z współbieżnością realizacji tooproper Planowanie wydajności dla magazynu danych.

* Planowanie pojemności może być złożonym zadaniem w przypadku obciążenia mieszanymi zapytaniami, szczególnie w przypadku, gdy będziesz potrzebować magazyn danych toohello pojemności tooadd realizacji długi czas. SQL Data Warehouse eliminuje pilną potrzebę planowania pojemności hello, ponieważ można zwiększyć lub zmniejszyć pojemność obliczeń, w dowolnym momencie, a pojemność magazynu i wydajności obliczeniowej są dopasowywane niezależnie.

### <a name="data-management"></a>Zarządzanie danymi
Zarządzanie danymi jest istotne, szczególnie gdy wiadomo, że może zabraknąć miejsca na dysku w hello Najbliższa przyszłość. Magazyny danych zazwyczaj dzielą dane hello na istotne zakresy, które są przechowywane jako partycje w tabeli. Wszystkie produkty oparte na programie SQL Server pozwalają przenosić partycje do tabeli i hello tabeli. Przełączanie partycji umożliwia przenoszenie starszych danych tooless tańsze magazynowanie i Zachowaj hello najnowszych danych w magazynie online.

* Indeksy magazynu kolumn obsługują tabele partycjonowane. W indeksach magazynu kolumn partycjonowane tabele są używane na potrzeby zarządzania danymi oraz archiwizacji. W tabelach przechowywanych wiersz po wierszu partycje pełnią ważniejszą rolę w zakresie wydajności zapytania.  
* Technologia PolyBase odgrywa ważną rolę w zarządzaniu danymi. Przy użyciu programu PolyBase, masz hello opcja tooarchive starszych danych tooHadoop lub magazynu obiektów blob platformy Azure.  Udostępnia wiele opcji, ponieważ dane hello jest nadal w trybie online.  Może potrwać dłużej tooretrieve danych z usługi Hadoop, ale zależnościami hello czasu pobierania może być większe niż hello przestrzeni magazynowej.

### <a name="exporting-data"></a>Eksportowanie danych
Jednym ze sposobów toomake dostępnych danych dla raportów i analiz jest toosend danych z tooservers magazynu danych hello przeznaczony do uruchamiania raportów i analiz. Serwery te są nazywane składnicami danych. Można na przykład wstępnie przetworzyć dane raportu i wyeksportować je z serwerów toomany magazynu danych Witaj świecie hello toomake go szeroko dostępne dla klientów oraz analityków.

* Aby generować raporty, każdej nocy można przesyłać Serwery raportowania tylko do odczytu z migawki codziennych danych hello. Daje to większą przepustowość dla klientów podczas zmniejszyć zapotrzebowanie na zasoby obliczeniowe hello na powitania hurtowni danych. W aspekcie bezpieczeństwa składnice danych umożliwiają tooreduce hello liczbę użytkowników, którzy mają dostęp toohello danych magazynu.
* Analiz można skonstruować moduł analizy w magazynie danych hello i przeprowadzać analizy w magazynie danych hello, lub wstępnie przetworzyć dane i wyeksportować go toohello serwer analiz do dalszej analizy.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz nieco SQL Data Warehouse, Dowiedz się jak tooquickly [Tworzenie usługi SQL Data Warehouse] [ create a SQL Data Warehouse] i [załadować przykładowe dane][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
