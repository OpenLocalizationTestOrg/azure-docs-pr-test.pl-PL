---
title: "Omówienie testów porównawczych aaaAzure bazy danych SQL"
description: "W tym temacie opisano hello Azure SQL bazy danych testu porównawczego używany pomiaru wydajności hello bazy danych SQL Azure."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Omówienie testów porównawczych bazy danych SQL Azure
## <a name="overview"></a>Omówienie
Microsoft Azure SQL Database oferuje trzy [warstw usług](sql-database-service-tiers.md) wiele poziomów wydajności. Każdy poziom wydajności udostępnia zwiększa zestaw zasobów lub zasilania, zaprojektowany toodeliver coraz wyższej przepustowości.

Jest ważne toobe tooquantify stanie jak hello zwiększa możliwości każdym poziomie wydajności przekłada się na wydajności zwiększona bazy danych. toodo, który to firma Microsoft opracowała hello Azure SQL bazy danych testu porównawczego (ASDB). Witaj testu porównawczego wykonuje podstawowe operacje, w przypadku wszystkich obciążeń OLTP. Firma Microsoft mierzenia przepływności hello uzyskuje baz danych uruchomionych w każdym poziomie wydajności.

Witaj zasobów i power każda warstwa i poziom wydajności usługi są wyrażane w postaci liczby [jednostki transakcji bazy danych (Dtu)](sql-database-what-is-a-dtu.md). Liczba jednostek Dtu umożliwiają toodescribe hello relatywną pojemność poziomu wydajności oparte na mieszanych pomiarach Procesora, pamięci, Odczyt i zapis stawki oferowanych na każdym poziomie wydajności. Podwojenie hello klasyfikacji jednostek dtu w warstwie bazy danych oznacza toodoubling hello bazy danych zasilania. Hello testu porównawczego pozwala nam tooassess hello wpływ na wydajność bazy danych hello zwiększenie zasilania oferowanych na każdym poziomie wydajności przez wykonywania operacji rzeczywistej bazy danych podczas skalowania proporcjonalnie do rozmiaru bazy danych, liczby użytkowników i stawki za transakcje toohello zasobów udostępnianych toohello bazy danych.

Przeprowadzili przepływności hello hello warstwy podstawowej usługi przy użyciu transakcji za godzinę warstwie usług standardowa hello przy użyciu transakcji na minutę i hello warstwę Premium za pomocą transakcji na sekundę, ułatwia łatwiejsze tooquickly dotyczą hello potencjalne wydajności każdej warstwy toohello wymagań aplikacji.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Korelowanie wydajność bazy danych world tooreal wyników testu wydajności
Jest ważne toounderstand tego ASDB, takich jak wszystkich testów porównawczych, jest tylko reprezentatywnej i świadczy. Witaj transakcji wskaźników z aplikacją testu porównawczego hello zostanie nie być hello takie same jak porty, które mogą być osiągnięte z innymi aplikacjami. testu porównawczego Hello składa się z kolekcją innej transakcji, uruchomienia typów ze schematem zawierający zakres tabel i typy danych. Podczas ćwiczeń testu porównawczego hello hello podstawowych operacji, które są typowe obciążenia OLTP tooall, nie reprezentuje dowolnej klasy określonej bazy danych lub aplikacji. Celem Hello testu porównawczego hello jest tooprovide uzasadnione przewodnik toohello względną wydajność bazy danych, które można oczekiwać podczas skalowania w górę lub w dół od poziomów wydajności. W rzeczywistości bazy danych o różnych rozmiarach i złożoność, występują różne kombinacje obciążeń i będzie odpowiadać na różne sposoby. Na przykład aplikacji intensywnie wykonujących operacje We/Wy wcześniej napotkać progi we/wy lub aplikacji użycie Procesora CPU napotkać limitów CPU wcześniej. Nie ma żadnej gwarancji, że wszelkie określonej bazy danych są skalowane w powitalne sam sposób jak testu porównawczego hello w obszarze zwiększenie obciążenia.

Witaj testu porównawczego i jej metodologii są opisane bardziej szczegółowo poniżej.

## <a name="benchmark-summary"></a>Podsumowanie testu porównawczego
ASDB mierzy wydajność hello operacje podstawowej bazy danych, które występują najczęściej w transakcji online (OLTP) obciążeń przetwarzania. Chociaż testu porównawczego hello jest zaprojektowana z chmury obliczeniowej, pamiętając, hello schematu bazy danych, populacji danych i transakcji zostały zaprojektowane toobe szeroko reprezentatywny podstawowych elementów hello najczęściej używane w obciążeń OLTP.

## <a name="schema"></a>Schemat
Schemat Hello jest zaprojektowana toohave za mało różnych i złożoność toosupport szeroką gamę operacji. testu porównawczego Hello jest uruchamiana dla składającej się z sześciu tabel bazy danych. tabele Hello dzielą się na trzy kategorie: stałym rozmiarze, skalowanie i powiększania. Istnieją dwie tabele stałym rozmiarze; trzy tabele skalowania; i jedna tabela rosnącym. Tabele o stałym rozmiarze ma stałą liczbę wierszy. Tabele skalowania mają Kardynalność, proporcjonalne toodatabase wydajności, ale nie zmieniają się podczas testu porównawczego hello. Witaj rośnie tabeli jest o rozmiarze jak skalowania tabelę na ładowania początkowego, ale następnie Kardynalność hello zmiany w toku hello uruchomionych testów porównawczych hello jako wiersze są wstawiane i usunąć.

Witaj schematu obejmuje różne typy danych, w tym liczbę całkowitą z zakresu alfanumeryczne, znak i daty/godziny. Schemat Hello zawiera klucze podstawowe i pomocnicze, ale nie wszystkie klucze obce — to nie istnieją żadne ograniczenia integralności referencyjnej między tabelami.

Program generowania danych generuje dane hello hello początkowej bazy danych. Liczba całkowita i numeryczne dane są generowane z różnych strategii. W niektórych przypadkach wartości są dystrybuowane losowo w zakresie. W pozostałych przypadkach zestaw wartości jest losowo cieniowania tooensure utrzymania określonych dystrybucji. Pola tekstowe są generowane z długą listę słów tooproduce rzeczywistych wyglądającej danych.

Baza danych Hello jest ustalać w oparciu "współczynnik skali". Współczynnik skali Hello (skrót rz) określa hello Kardynalność hello skalowanie i powiększania tabel. Zgodnie z poniższym opisem w hello sekcji użytkowników i Pacing, hello rozmiar bazy danych, liczba użytkowników, a maksymalną wydajność wszystkich skalować w proporcji tooeach innych.

## <a name="transactions"></a>Transakcje
Obciążenie Hello składa się z typów dziewięć transakcji, jak pokazano w poniższej tabeli hello. Każdą transakcję toohighlight zaprojektowanej określony zestaw właściwości hello sprzętu systemu i aparatu bazy danych, wysoki kontrast z hello inne transakcje. Takie podejście umożliwia łatwiejsze tooassess hello wpływ na wydajność toooverall różnych składników. Na przykład "Odczytu duże" transakcji hello tworzy duża liczba operacji odczytu z dysku.

| Typ transakcji | Opis |
| --- | --- |
| Odczyt Lite |WYBIERZ; w pamięci. tylko do odczytu |
| Średnia liczba godzin odczytu |WYBIERZ; przede wszystkim w pamięci; tylko do odczytu |
| Ciężki odczytu |WYBIERZ; przede wszystkim nie w pamięci; tylko do odczytu |
| Aktualizacja Lite |AKTUALIZACJA; w pamięci. Odczyt i zapis |
| Ciężki aktualizacji |AKTUALIZACJA; przede wszystkim nie w pamięci; Odczyt i zapis |
| Wstaw Lite |WSTAW; w pamięci. Odczyt i zapis |
| Wstaw ciężkie |WSTAW; przede wszystkim nie w pamięci; Odczyt i zapis |
| Usuwanie |USUŃ; mieszane w pamięci i nie w pamięci; Odczyt i zapis |
| Silnie procesor CPU |WYBIERZ; w pamięci. stosunkowo duże obciążenie procesora CPU; tylko do odczytu |

## <a name="workload-mix"></a>Mieszane obciążenia
Transakcje są wybierane losowo w ważoną dystrybucji z powitania po ogólnej mieszanego. Witaj mieszanego ogólną ma stosunek odczytu/zapisu około 2:1.

| Typ transakcji | % mieszanego |
| --- | --- |
| Odczyt Lite |35 |
| Średnia liczba godzin odczytu |20 |
| Ciężki odczytu |5 |
| Aktualizacja Lite |20 |
| Ciężki aktualizacji |3 |
| Wstaw Lite |3 |
| Wstaw ciężkie |2 |
| Usuwanie |2 |
| Silnie procesor CPU |10 |

## <a name="users-and-pacing"></a>Użytkownicy i tempo
Witaj testu obciążenia jest wymuszany za pomocą narzędzia, który przesyła transakcji w zestawie połączeń toosimulate hello zachowanie liczby równoczesnych użytkowników. Mimo że wszystkie połączenia hello i transakcji są generowane maszyny, dla uproszczenia firma Microsoft można znaleźć połączenia toothese jako "użytkowników." Mimo że każdy użytkownik działa niezależnie od innych użytkowników, wszyscy użytkownicy wykonać hello samego cyklu kroki opisane poniżej:

1. Należy ustanowić połączenie z bazą danych.
2. Powtórz do sygnałowego tooexit:
   * Wybierz transakcję losowo (z rozkładu ważoną).
   * Wykonywanie transakcji hello zaznaczone i czas odpowiedzi hello miary.
   * Poczekaj, aż pacing opóźnienia.
3. Zamknij hello połączenia z bazą danych.
4. Zakończ.

Hello opóźnienia (w kroku 2, c) kroku wybrano losowo, ale z dystrybucji nie ma to wartość średnia drugiej 1.0. W związku z tym każdy użytkownik może średnio wygenerować co najwyżej jednej transakcji na sekundę.

## <a name="scaling-rules"></a>Skalowanie reguły
Hello użytkowników jest określana na podstawie hello rozmiar bazy danych (w jednostkach współczynnik skali). Brak jednego użytkownika, co pięć jednostek współczynnik skali. Z powodu opóźnienia kroku hello jeden użytkownik może wygenerować co najwyżej jednej transakcji na sekundę, średnia.

Na przykład — współczynnik skali 500 (rz = 500) bazy danych będą mieli 100 użytkowników i może osiągnąć maksymalną szybkość 100 TPS. toodrive wyższym TPS wymaga większej liczby użytkowników i większą bazę danych.

w poniższej tabeli Hello pokazuje liczbę hello użytkowników faktycznie przez dłuższy czas dla każdej warstwy i poziom wydajności usługi.

| Warstwy usług (poziom wydajności) | Użytkownicy | Rozmiar bazy danych |
| --- | --- | --- |
| Podstawowa |5 |720 MB |
| Standard (S0) |10 |1 GB |
| Standardowa (S1) |20 |2.1 GB |
| Standard (S2) |50 |7.1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Czas trwania pomiaru.
Nieprawidłowa uruchomienia testu porównawczego wymaga pomiaru stabilnego obowiązywania co najmniej jedną godzinę.

## <a name="metrics"></a>Metryki
Witaj kluczowe metryki w testu porównawczego hello jest przepływności i odpowiedzi.

* Przepływność wynosi hello miara wydajności niezbędne w hello testu wydajności. Przepływność jest zgłaszana w transakcji na jednostkę elementu czasu, inwentaryzacji wszystkich typów transakcji.
* Czas odpowiedzi to miara wydajności, przewidywalności. ograniczenia czasu odpowiedzi Hello zależy od rodzaju usług o wyższych klas usługi o wprowadzenie bardziej rygorystycznych wymagań czasu odpowiedzi, jak pokazano poniżej.

| Klasa usługi | Miara przepływności | Wymagania dotyczące czasu odpowiedzi |
| --- | --- | --- |
| Premium |Transakcje na sekundę |95. percentyl w sekundach 0,5 |
| Standardowa |Transakcje na minutę |90-procentowy w sekundach 1.0 |
| Podstawowa |Transakcje na godzinę |80. percentyl w sekundach 2.0 |

## <a name="conclusion"></a>Podsumowanie
Witaj testu wydajności bazy danych SQL Azure mierzy hello względną wydajność uruchomione w zakresie hello warstwy dostępność usług i poziomy wydajności bazy danych SQL Azure. Witaj testu porównawczego wykonuje operacje podstawowej bazy danych, które występują najczęściej w transakcji online (OLTP) obciążeń przetwarzania. Mierząc faktyczną wydajnością testu porównawczego hello zapewnia bardziej zrozumiałej oceny wpływu hello przepływności zmiany hello poziomu wydajności niż jest to możliwe tylko listę zasobów hello na każdym poziomie, takich jak szybkości procesora CPU, rozmiaru pamięci i IOPS . W przyszłości hello firma Microsoft będzie kontynuować tooevolve hello testu porównawczego toobroaden jej zakres i rozwiń hello dane dostarczone.

## <a name="resources"></a>Zasoby
[Wprowadzenie tooSQL bazy danych](sql-database-technical-overview.md)

[Warstwy usług i poziomy wydajności](sql-database-service-tiers.md)

[Wytyczne dotyczące wydajności dla pojedynczej bazy danych](sql-database-performance-guidance.md)
