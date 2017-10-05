---
title: "Jak skonfigurować parametry serwera w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania parametrów dostępnego serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 718bbf359253849fbc989c563ffd6d1099f92348
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-server-parameters-in-azure-database-for-mysql-using-the-azure-portal"></a>Jak skonfigurować parametry serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure

Bazy danych platformy Azure dla programu MySQL obsługuje konfigurowanie niektórych parametrów serwera. W tym artykule opisano sposób konfigurowania tych parametrów, przy użyciu portalu Azure i wymieniono obsługiwane parametry, wartości domyślne i zakresem prawidłowych wartości. Nie wszystkie parametry serwera można dostosować. Obsługiwane są tylko te, które zostały przedstawione w tym miejscu.

## <a name="navigate-to-server-parameters-blade-on-azure-portal"></a>Przejdź do bloku parametrów serwera w portalu Azure

Zaloguj się do portalu Azure, a następnie kliknij bazy danych Azure, aby nazwa serwera MySQL. W obszarze **ustawienia** kliknij **parametry serwera** aby otworzyć blok parametrów serwera bazy danych Azure dla programu MySQL.

![Blok parametrów serwera portalu Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lista parametrów można skonfigurować serwera

Poniższa tabela zawiera listę parametrów aktualnie obsługiwany serwer. Parametry można skonfigurować zgodnie z wymaganiami aplikacji.

> [!div class="mx-tableFixed"]
|Nazwa parametru|Wartość domyślna|Zakres|Opis|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Formanty ile mikrosekundach zatwierdzania dziennik binarny czeka przed synchronizacją binarny plik dziennika na dysku.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|Maksymalna liczba transakcji oczekiwania przed przerwaniem bieżącego opóźnienia, określonej za pomocą binlog grupy commit synchronizacji delay.|
|character_set_server|LATIN1|Big5 UTF8MB4, itp.|Użyj charset_name jako domyślny zestaw znaków serwera.|
|div_precision_increment|4|0-30|Liczba cyfr, o którą należy zwiększyć skalę wyniku operacji dzielenia.|
|group_concat_max_len|1024|4-16777216|Maksymalna dozwolona długość wyniku w bajtach dla GROUP_CONCAT().|
|innodb_adaptive_hash_index|ON|WŁĄCZONY WYŁĄCZONY|Określa, czy indeksów skrótu adaptacyjną innodb są włączone lub wyłączone.|
|innodb_lock_wait_timeout|50|1-3600|Czas w sekundach transakcji InnoDB oczekuje na blokadę wiersza zrezygnuje.|
|interactive_timeout|1800|10-1800|Liczba sekund oczekiwania przez serwer dla działań w interaktywne połączenia przed jego zamknięciem.|
|log_bin_trust_function_creators|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Ta zmienna ma zastosowanie, po włączeniu rejestrowania binarnego. Kontroluje, czy nie, aby utworzyć składowanych funkcji, które powodują niebezpieczny zdarzenia są zapisywane w dzienniku binarne mogą być zaufane twórców przechowywanej funkcji.|
|log_queries_not_using_indexes|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Rejestruje zapytania, które mogą pobrać wszystkie wiersze w dzienniku powolne zapytania.|
|log_slow_admin_statements|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Powolne instrukcji administracyjnych #include w instrukcjach zapisywane w dzienniku powolne zapytania.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Ogranicza liczbę takich zapytań na minutę, które mogą być zapisywane w dzienniku powolne zapytania.|
|long_query_time|10|1 1E + 100|Jeśli zapytanie trwa dłużej niż ten czas w sekundach, serwer zwiększa Slow_queries zmiennej stanu.|
|max_allowed_packet|536870912|1024-1073741824|Maksymalny rozmiar jeden pakiet lub dowolny ciąg wygenerowany pośredni lub żadnego parametru wysyłane przez mysql_stmt_send_long_data() funkcji C API.|
|min_examined_row_limit|0|0-18446744073709551615|Rejestruje zapytania, które mają większy niż skonfigurowana liczba wierszy w dzienniku powolne zapytania. |
|server_id|3293747068|1000-4294967295|Identyfikator serwera używana w replikacji wszystkich wzorców, a slave unikatową tożsamość.|
|slave_net_timeout|60|30-3600|Liczbę sekund oczekiwania przed podrzędnej uważa połączenie uszkodzony, większej ilości danych z wzorca przerywa odczytu i próbuje połączyć się ponownie.|
|slow_query_log|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Włącz lub Wyłącz dziennik powolne zapytań.|
|sql_mode|wybrane 0|ALLOW_INVALID_DATES IGNORE_SPACE, itp.|Bieżący tryb programu SQL server.|
|użyciu|SYSTEM|Przykłady: -8:00, +05: 30|Strefa czasowa serwera.|
|wait_timeout|120|60-240|Liczba sekund oczekiwania przez serwer dla działania nieinteraktywne połączenia przed jego zamknięciem.|

## <a name="next-steps"></a>Następne kroki
- [Biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)
