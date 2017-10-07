---
title: "aaaHow tooDump i przywrócić w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooextract PostgreSQL bazy danych w pliku zrzutu i Przywróć bazę danych PostgreSQL hello z pliku archiwum utworzone przez pg_dump w bazie danych Azure dla PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migrowanie bazy danych PostgreSQL przy użyciu zrzutu i przywracania
Można użyć [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bazy danych programu PostgreSQL w pliku zrzutu i [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore bazą danych PostgreSQL hello z utworzonych przez pg_dump pliku archiwum.

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- [Azure bazy danych serwera PostgreSQL](quickstart-create-server-database-portal.md) dostępu tooallow reguły zapory i bazy danych na jego podstawie.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) i [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) zainstalowane narzędzia wiersza polecenia

Wykonaj te kroki toodump i przywrócenia bazy danych programu PostgreSQL:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Tworzenie pliku zrzutu z wykorzystaniem pg_dump zawierający toobe danych hello załadowany
tooback się PostgreSQL istniejącej bazy danych lokalnie lub na maszynie wirtualnej, uruchom następujące polecenie hello:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Na przykład, jeśli masz lokalny serwer i bazę danych o nazwie **programu testdb** w nim
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Przywróć hello danych do obiektu docelowego hello Azure bazy danych dla PostrgeSQL przy użyciu pg_restore
Po utworzeniu hello docelowej bazy danych, można użyć polecenia pg_restore hello i hello -d — dbname parametru toorestore hello dane hello docelowej bazy danych z pliku zrzutu hello.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
W tym przykładzie należy przywrócić hello dane z pliku zrzutu hello **testdb.dump** do bazy danych hello **mypgsqldb** na serwerze docelowym **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Następne kroki
- toomigrate bazy danych programu PostgreSQL przy użyciu eksportu i importu, zobacz [migracji PostgreSQL bazy danych przy użyciu eksportowania i importowania](howto-migrate-using-export-and-import.md)
