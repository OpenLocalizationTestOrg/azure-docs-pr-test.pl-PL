---
title: tooConfigure aaaHow parametry serwera w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooconfigure dostępnego serwera parametrów w bazie danych Azure przy użyciu MySQL hello portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Jak tooconfigure serwera parametrów w bazie danych Azure przy użyciu MySQL hello portalu Azure

Bazy danych platformy Azure dla programu MySQL obsługuje konfigurowanie niektórych parametrów serwera. W tym artykule opisano, jak tooconfigure tych parametrów, przy użyciu hello portalu Azure i list hello obsługiwane parametry, wartości domyślne hello i hello zakresu prawidłowych wartości. Nie wszystkie parametry serwera można dostosować. Obsługiwane są tylko hello wymienione w tym miejscu.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Przejdź do bloku parametrów tooServer w portalu Azure

Zaloguj się za toohello portalu Azure, a następnie kliknij bazy danych Azure, aby nazwa serwera MySQL. W obszarze hello **ustawienia** kliknij **parametry serwera** bloku parametrów tooopen hello serwera na powitania bazy danych Azure dla programu MySQL.

![Blok parametrów serwera portalu Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lista parametrów można skonfigurować serwera

Witaj w poniższej tabeli wymieniono hello aktualnie obsługiwane parametry serwera. Parametry Hello można skonfigurować zgodnie z tooyour wymagań aplikacji.

> [!div class="mx-tableFixed"]
|Nazwa parametru|Wartość domyślna|Zakres|Opis|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Formanty ile mikrosekundach hello dziennik binarny zatwierdzania czeka przed synchronizacją hello dziennik binarny plik toodisk.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|Witaj maksymalna liczba transakcji toowait dla przed przerwaniem hello bieżącego opóźnienia określonej za pomocą binlog grupy commit synchronizacji delay.|
|character_set_server|LATIN1|Big5 UTF8MB4, itp.|Użyj charset_name jako hello domyślny zestaw znaków serwera.|
|div_precision_increment|4|0-30|Liczba cyfr, które Skala hello tooincrease hello wyniku operacji dzielenia.|
|group_concat_max_len|1024|4-16777216|Maksymalna dozwolona długość wyniku dla hello GROUP_CONCAT() wyrażony w bajtach.|
|innodb_adaptive_hash_index|ON|WŁĄCZONY WYŁĄCZONY|Określa, czy indeksów skrótu adaptacyjną innodb są włączone lub wyłączone.|
|innodb_lock_wait_timeout|50|1-3600|Długość Hello czas w sekundach transakcji InnoDB czeka blokady wiersza zrezygnuje.|
|interactive_timeout|1800|10-1800|Liczba sekund powitania serwera czeka na działanie na interaktywne połączenia przed jego zamknięciem.|
|log_bin_trust_function_creators|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Ta zmienna ma zastosowanie, po włączeniu rejestrowania binarnego. Kontroluje, czy przechowywanej funkcji twórców może być zaufane nie funkcji toocreate przechowywane, które powodują toobe niebezpieczny zdarzenia zapisywane toohello dziennik binarny.|
|log_queries_not_using_indexes|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Dzienniki zapytań, które są oczekiwane tooretrieve wszystkie wiersze tooslow zapytania dziennika.|
|log_slow_admin_statements|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Powolne instrukcji administracyjnych #include w instrukcjach hello zapisany dziennik zapytań powolne toohello.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Limity hello liczba takich zapytań na minutę, które mogą być zapisywane toohello dziennik powolne zapytań.|
|long_query_time|10|1 1E + 100|Jeśli zapytanie trwa dłużej niż ten czas w sekundach, serwer hello zwiększa hello Slow_queries stanu zmiennej.|
|max_allowed_packet|536870912|1024-1073741824|Maksymalny rozmiar Hello jeden pakiet lub dowolny ciąg wygenerowany pośredni lub żadnego parametru wysyłane przez mysql_stmt_send_long_data() hello funkcji C API.|
|min_examined_row_limit|0|0-18446744073709551615|Rejestruje zapytania, które mają większy niż hello skonfigurowana liczba wierszy w dzienniku zapytań powolne hello. |
|server_id|3293747068|1000-4294967295|Identyfikator serwera Hello, używany w replikacji toogive każdego głównego i slave unikatową tożsamość.|
|slave_net_timeout|60|30-3600|Witaj liczbę sekund toowait więcej danych z głównego hello przed podrzędna hello uwzględnia połączenie hello przerwane, przerywa hello odczytu i próbuje tooreconnect.|
|slow_query_log|WYŁĄCZANIE|WŁĄCZONY WYŁĄCZONY|Włącz lub wyłącz hello dziennik powolne zapytań.|
|sql_mode|wybrane 0|ALLOW_INVALID_DATES IGNORE_SPACE, itp.|Witaj bieżący tryb programu SQL server.|
|użyciu|SYSTEM|Przykłady: -8:00, +05: 30|Witaj strefy czasowej serwera.|
|wait_timeout|120|60-240|Witaj liczbę sekund powitania serwera czeka na działania nieinteraktywne połączenia przed jego zamknięciem.|

## <a name="next-steps"></a>Następne kroki
- [Biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)
