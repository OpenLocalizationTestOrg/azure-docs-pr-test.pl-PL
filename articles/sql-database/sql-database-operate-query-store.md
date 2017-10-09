---
title: "aaaOperating magazyn zapytań w bazie danych SQL Azure"
description: "Dowiedz się, jak toooperate hello magazyn zapytań w bazie danych SQL Azure"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Działania hello magazyn zapytań w bazie danych SQL Azure
Magazyn zapytań w usłudze Azure to funkcja bazy danych w pełni zarządzana, nieustannie zbiera i wyświetla szczegółowe informacje historyczne na temat wszystkich zapytań. Temat funkcji magazyn zapytań można traktować jako rejestrator danych podobne samolotowy tooan znacząco upraszcza wydajność zapytań, rozwiązywanie problemów z zarówno w chmurze i lokalnych klientów. W tym artykule opisano aspekty określonego systemu operacyjnego magazynu zapytań na platformie Azure. Przy użyciu to wstępnie zebrane dane, można szybkie diagnozowanie i rozwiązywanie problemów z wydajnością i w związku z tym poświęcić więcej czasu na koncentrujących się na swojej działalności. 

Magazyn zapytań był [globalnie dostępną](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) w bazie danych SQL Azure od listopada 2015 r. Magazyn zapytań jest podstawą hello analizy wydajności i dostrajania funkcji, takich jak [doradcy bazy danych SQL i pulpit nawigacyjny wydajności](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). W momencie hello publikowania w tym artykule magazyn zapytań jest uruchomiony w więcej niż 200 000 baz danych użytkowników na platformie Azure, zbieranie informacji związanych z zapytania dla kilku miesięcy, bez przeszkód.

> [!IMPORTANT]
> Firma Microsoft dokłada w hello proces aktywacji magazyn zapytań dla wszystkich baz danych Azure SQL (istniejących i nowych). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Konfiguracja optymalna magazyn zapytań
W tej sekcji opisano ustawienia domyślne optymalną konfigurację, które są zaprojektowane tooensure niezawodnego działania hello magazyn zapytań i funkcje zależne, takie jak [doradcy bazy danych SQL i pulpit nawigacyjny wydajności](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Domyślna konfiguracja jest zoptymalizowany do zbierania danych ciągłego, to minimalny czas przeznaczony na OFF/READ_ONLY stanów.

| Konfiguracja | Opis | Domyślne | Komentarz |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Określa limit hello przestrzeni danych hello prowadzące przez Magazyn zapytań w bazie danych klientów z |100 |Wymuszane dla nowych baz danych |
| PARAMETR INTERVAL_LENGTH_MINUTES |Określa rozmiar przedział czasu, podczas którego statystyk zebranych środowiska uruchomieniowego dla planów zapytania są agregowane i utrwalone. Każdy plan aktywnej kwerendzie ma co najwyżej jeden wiersz w danym okresie czasu zdefiniowanego w tej konfiguracji |60 |Wymuszane dla nowych baz danych |
| PARAMETR STALE_QUERY_THRESHOLD_DAYS |Zasady oparte na czasie oczyszczania, które kontrolują hello okres przechowywania statystyk utrwalonego środowiska uruchomieniowego i nieaktywne zapytania |30 |Wymuszane dla nowych baz danych i baz danych z poprzedniej domyślne (367) |
| PARAMETR SIZE_BASED_CLEANUP_MODE |Określa, czy automatyczne oczyszczania ma miejsce, gdy zbliża się hello limit rozmiar danych w magazynie zapytań |AUTOMATYCZNIE |Wymuszone dla wszystkich baz danych |
| PARAMETR QUERY_CAPTURE_MODE |Określa, czy są śledzone wszystkich zapytań czy tylko podzbiór zapytań |AUTOMATYCZNIE |Wymuszone dla wszystkich baz danych |
| FLUSH_INTERVAL_SECONDS |Określa maksymalny okres, w którym statystyki przechwyconych działania są przechowywane w pamięci, przed opróżnianie toodisk |900 |Wymuszane dla nowych baz danych |
|  | | | |

> [!IMPORTANT]
> Te wartości domyślne są automatycznie stosowane w ostatnim etapie hello aktywacji magazyn zapytań w wszystkich baz danych Azure SQL (zobacz ważna uwaga poprzedniego). Po powyższe w górę baza danych SQL Azure nie będzie zmiana wartości konfiguracji ustawione przez klientów, chyba że ich niekorzystnie wpłynąć na podstawowe obciążenie lub niezawodnego działania hello magazynu zapytań.
> 
> 

Toostay z ustawienia niestandardowe, należy użyć [ALTER DATABASE z użyciem opcji magazynu zapytań](https://msdn.microsoft.com/library/bb522682.aspx) toorevert konfiguracji toohello poprzedniego stanu. Zapoznaj się z [najlepsze rozwiązania z hello magazynu zapytań](https://msdn.microsoft.com/library/mt604821.aspx) w kolejności toolearn jak górny wybrany parametry optymalną konfigurację.

## <a name="next-steps"></a>Następne kroki
[Szczegółowe informacje o wydajności bazy danych SQL](sql-database-performance.md)

## <a name="additional-resources"></a>Dodatkowe zasoby
Aby uzyskać więcej informacji o wyewidencjonowanie hello następujące artykuły:

* [Rejestrator danych dla bazy danych](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Monitorowanie wydajności za pomocą magazynu zapytań hello](https://msdn.microsoft.com/library/dn817826.aspx)
* [Scenariusze użycia magazynu zapytań](https://msdn.microsoft.com/library/mt614796.aspx)
* [Monitorowanie wydajności za pomocą magazynu zapytań hello](https://msdn.microsoft.com/library/dn817826.aspx) 

