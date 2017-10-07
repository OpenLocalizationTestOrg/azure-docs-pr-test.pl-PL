---
title: "aaaAzure limity zasobów bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano niektóre typowe limity zasobów bazy danych SQL Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limitom zasobów bazy danych SQL Azure
## <a name="overview"></a>Omówienie
Baza danych SQL Azure zarządza hello zasoby dostępne tooa bazy danych przy użyciu dwóch różnych mechanizmów: **ładu zasobów** i **wymuszania ograniczeń**. W tym temacie opisano te dwa główne obszary zarządzania zasobami.

## <a name="resource-governance"></a>Zarządzanie zasobów
Jednym z celów projektu hello warstwy usług podstawowa, standardowa, Premium i Premium RS hello jest dla bazy danych SQL Azure toobehave tak, jakby hello bazy danych jest uruchomiona na jego własnej maszynie izolowane od innych baz danych. Zarządzanie zasobów emuluje to zachowanie. Zagregowane hello wykorzystania zasobów osiągnie hello maksymalne dostępne Procesora, pamięci, we/wy dziennika i bazy danych toohello przypisane zasoby danych we/wy, zasobów ładu kolejek zapytania podczas wykonywania i przypisać toohello w kolejce zapytań ich zwolnić zasoby.

Jako dedykowane maszyny, przy użyciu wszystkich dostępnych zasobów powoduje dłużej wykonywania aktualnie wykonywanych zapytań, co może spowodować polecenia przekroczeń limitu czasu na powitania klienta. Aplikacjom logiki agresywne ponawiania próby i aplikacje, które wykonywanie zapytań względem bazy danych hello o wysokiej częstotliwości może wystąpić błędy komunikaty podczas próby tooexecute nowego zapytania po osiągnięciu limitu hello równoczesnych żądań.

### <a name="recommendations"></a>Zalecenia:
Monitorowanie wykorzystania zasobów hello i czasy odpowiedzi średni hello zapytań Jeśli niedługo hello maksymalne wykorzystanie bazy danych. Gdy wystąpią większych opóźnień zapytania ogólnie dostępne są trzy opcje:

1. Zmniejsz hello liczbę przychodzących żądań toohello bazy danych tooprevent limitu czasu i hello stosu zapasowej żądań.
2. Przypisz wyższej bazy danych toohello poziomu wydajności.
3. Optymalizacja wykorzystania zasobów hello tooreduce zapytania każdego zapytania. Aby uzyskać więcej informacji, zobacz sekcję zapytania dostrajania/Hinting w artykule wskazówki wydajności bazy danych SQL Azure hello hello.

## <a name="enforcement-of-limits"></a>Wymuszania ograniczeń
Zasoby innych niż Procesora, pamięci, we/wy dziennika i dane We/Wy są wymuszane przez po osiągnięciu limitu zezwalających na nowe żądania. Bazy danych osiągnie limit maksymalnego rozmiaru hello skonfigurowane, INSERT i aktualizacje, które zwiększają rozmiar danych zakończyć się niepowodzeniem, wybiera i usuwa nadal toowork. Klienci odbierają [komunikat o błędzie](sql-database-develop-error-messages.md) w zależności od hello limit został osiągnięty.

Na przykład liczba hello bazy danych SQL tooa połączeń i hello liczbę jednoczesnych żądań, które mogą być przetwarzane są ograniczone. Baza danych SQL pozwala hello liczba połączeń toohello bazy danych toobe większa niż liczba hello puli połączeń toosupport równoczesnych żądań. Gdy hello liczbę połączeń, które są dostępne łatwo mogą być kontrolowane przez aplikacji hello, hello liczba równoległych żądań jest często tooestimate przeszkodę razy i toocontrol. Szczególnie podczas obciążenia szczytowego przy aplikacji hello wysyła albo zbyt wiele żądań lub bazy danych hello osiągnięty limit zasobów i gromadzeniu się wątków roboczych powodu toolonger uruchomione zapytania zostanie uruchomiony, można napotkano błędy.

## <a name="service-tiers-and-performance-levels"></a>Warstwy usługi i poziomy wydajności
Brak warstwy usług i poziomy wydajności dla pojedynczej bazy danych i elastyczne pule.

### <a name="single-databases"></a>Pojedyncze bazy danych
Dla jednej bazy danych limity hello bazy danych są definiowane przez hello bazy danych usługi warstwę i poziom wydajności. Witaj w poniższej tabeli opisano cechy hello baz danych Basic, Standard, Premium i Premium RS na różne poziomy wydajności.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Klienci korzystający z P11 i P15 poziomy wydajności można użyć zapasowej TB too4 dołączone magazynu bez dodatkowych opłat. Ta opcja 4 TB jest obecnie dostępna w następujących regionach hello: East2 nam, zachodnie stany USA, Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Niemcy centralnej, Południowej, Azja Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada centralnej i Kanada Wschodnia.
>

### <a name="elastic-pools"></a>Pule elastyczne
[Pule elastyczne](sql-database-elastic-pool.md) współużytkowanie zasobów między bazami danych w puli hello. Witaj w poniższej tabeli opisano cechy hello Basic, Standard, Premium i Premium RS elastyczne pule.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Rozwinięte definicji wszystkich zasobów wymienionych w poprzednich tabelach hello, zobacz opisy hello w [usługi zestawieniu możliwości i ograniczeń](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Omówienie warstwy usług, zobacz [warstwach usług bazy danych SQL Azure i poziomy wydajności](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Limity inne bazy danych SQL
| Obszar | Limit | Opis |
| --- | --- | --- |
| Baz danych przy użyciu zautomatyzowanego eksportu dla subskrypcji |10 |Zautomatyzowanym eksporcie umożliwia toocreate harmonogramu niestandardowego do utworzenia kopii zapasowej bazy danych SQL. tej funkcji w wersji zapoznawczej Hello kończy się 1 marca 2017 r.  |
| Baz danych na serwerze |Zapasowej too5000 |Zapasowej too5000 baz danych są dozwolone na serwerze. |
| Liczba jednostek Dtu na serwer |45000 |45000 jednostek Dtu są dozwolone na serwerze do rozbudowy autonomicznej bazy danych i elastyczne pule. Łączna liczba Hello autonomicznej bazy danych i pul dozwolonych dla jednego serwera jest ograniczona tylko przez hello liczbę jednostek Dtu.  

> [!IMPORTANT]
> Azure bazy danych zautomatyzowanego eksportu danych SQL jest obecnie w wersji zapoznawczej i zostaną wycofane w 1 marca 2017 r. Od 1 grudnia 2016, nie będzie już stanie tooconfigure zautomatyzowanego eksportu na dowolną bazą danych SQL. Wszystkie istniejące zadania zautomatyzowanym eksporcie będzie toowork dnia 1 marca 2017 r. Po 1 grudnia 2016, można użyć [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md) lub [usługi Automatyzacja Azure](../automation/automation-intro.md) tooarchive baz danych okresowo przy użyciu programu PowerShell okresowo według harmonogramu tooa wybranych przez użytkownika. Przykładowego skryptu można pobrać hello [przykładowy skrypt z usługi GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Zasoby
[Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md)

[Warstwy usługi bazy danych Azure SQL i poziomy wydajności](sql-database-service-tiers.md)

[Komunikaty o błędach dotyczących programów klienckich usługi SQL Database](sql-database-develop-error-messages.md)
