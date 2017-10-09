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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="1d9b0-103">Migracji PostgreSQL bazy danych przy użyciu eksportowania i importowania</span><span class="sxs-lookup"><span data-stu-id="1d9b0-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="1d9b0-104">Można użyć [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bazy danych programu PostgreSQL do pliku skryptu i [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport dane hello hello docelowej bazy danych z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="1d9b0-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d9b0-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1d9b0-105">Prerequisites</span></span>
<span data-ttu-id="1d9b0-106">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="1d9b0-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="1d9b0-107">[Azure bazy danych serwera PostgreSQL](quickstart-create-server-database-portal.md) dostępu tooallow reguły zapory i bazy danych na jego podstawie.</span><span class="sxs-lookup"><span data-stu-id="1d9b0-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="1d9b0-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) zainstalowane narzędzie wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1d9b0-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="1d9b0-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) zainstalowane narzędzie wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1d9b0-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="1d9b0-110">Wykonaj te kroki tooexport i importować PostgreSQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d9b0-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="1d9b0-111">Tworzenie pliku skryptu za pomocą pg_dump zawierający toobe danych hello załadowany</span><span class="sxs-lookup"><span data-stu-id="1d9b0-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="1d9b0-112">tooexport Twojego PostgreSQL istniejące bazy danych lokalnie lub w pliku skryptu sql tooa maszyny Wirtualnej, uruchom następujące polecenie w istniejącym środowisku hello:</span><span class="sxs-lookup"><span data-stu-id="1d9b0-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="1d9b0-113">Na przykład, jeśli masz lokalny serwer i bazę danych o nazwie **programu testdb** w nim</span><span class="sxs-lookup"><span data-stu-id="1d9b0-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="1d9b0-114">Importuj dane hello docelową bazą danych Azure dla PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="1d9b0-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="1d9b0-115">Można użyć wiersza polecenia psql hello i hello -d — dbname parametru tooimport hello danych do bazy danych Azure w PostrgeSQL możemy utworzyć i ładowanie danych z pliku sql hello.</span><span class="sxs-lookup"><span data-stu-id="1d9b0-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="1d9b0-116">W tym przykładzie użyto psql narzędzie i plik skryptu o nazwie **testdb.sql** z poprzedniego kroku tooimport danych do bazy danych hello **mypgsqldb** na serwerze docelowym  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="1d9b0-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="1d9b0-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d9b0-117">Next steps</span></span>
- <span data-ttu-id="1d9b0-118">toomigrate bazy danych programu PostgreSQL przy użyciu zrzutu i przywracania, zobacz [migracji za pomocą zrzutu i przywracania bazy danych PostgreSQL](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="1d9b0-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
