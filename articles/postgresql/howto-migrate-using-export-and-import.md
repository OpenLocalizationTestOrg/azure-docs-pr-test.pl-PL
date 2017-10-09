---
title: "aaaMigrate bazy danych przy użyciu importowanie i eksportowanie w bazie danych Azure na potrzeby PostgreSQL | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wyodrębnić bazy danych programu PostgreSQL do pliku skryptu i zaimportuj dane hello do hello docelowej bazy danych z tego pliku."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migracji PostgreSQL bazy danych przy użyciu eksportowania i importowania
Można użyć [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bazy danych programu PostgreSQL do pliku skryptu i [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport dane hello hello docelowej bazy danych z tego pliku.

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- [Azure bazy danych serwera PostgreSQL](quickstart-create-server-database-portal.md) dostępu tooallow reguły zapory i bazy danych na jego podstawie.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) zainstalowane narzędzie wiersza polecenia
- [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) zainstalowane narzędzie wiersza polecenia

Wykonaj te kroki tooexport i importować PostgreSQL bazy danych.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Tworzenie pliku skryptu za pomocą pg_dump zawierający toobe danych hello załadowany
tooexport Twojego PostgreSQL istniejące bazy danych lokalnie lub w pliku skryptu sql tooa maszyny Wirtualnej, uruchom następujące polecenie w istniejącym środowisku hello:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Na przykład, jeśli masz lokalny serwer i bazę danych o nazwie **programu testdb** w nim
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Importuj dane hello docelową bazą danych Azure dla PostrgeSQL
Można użyć wiersza polecenia psql hello i hello -d — dbname parametru tooimport hello danych do bazy danych Azure w PostrgeSQL możemy utworzyć i ładowanie danych z pliku sql hello.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
W tym przykładzie użyto psql narzędzie i plik skryptu o nazwie **testdb.sql** z poprzedniego kroku tooimport danych do bazy danych hello **mypgsqldb** na serwerze docelowym  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Następne kroki
- toomigrate bazy danych programu PostgreSQL przy użyciu zrzutu i przywracania, zobacz [migracji za pomocą zrzutu i przywracania bazy danych PostgreSQL](howto-migrate-using-dump-and-restore.md)
