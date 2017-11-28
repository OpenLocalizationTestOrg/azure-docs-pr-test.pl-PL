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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="0e84e-103">Migrowanie bazy danych PostgreSQL przy użyciu zrzutu i przywracania</span><span class="sxs-lookup"><span data-stu-id="0e84e-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="0e84e-104">Można użyć [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract bazy danych programu PostgreSQL w pliku zrzutu i [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore bazą danych PostgreSQL hello z utworzonych przez pg_dump pliku archiwum.</span><span class="sxs-lookup"><span data-stu-id="0e84e-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e84e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0e84e-105">Prerequisites</span></span>
<span data-ttu-id="0e84e-106">toostep za pośrednictwem tego jak tooguide, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="0e84e-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="0e84e-107">[Azure bazy danych serwera PostgreSQL](quickstart-create-server-database-portal.md) dostępu tooallow reguły zapory i bazy danych na jego podstawie.</span><span class="sxs-lookup"><span data-stu-id="0e84e-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="0e84e-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) i [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) zainstalowane narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0e84e-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="0e84e-109">Wykonaj te kroki toodump i przywrócenia bazy danych programu PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="0e84e-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="0e84e-110">Tworzenie pliku zrzutu z wykorzystaniem pg_dump zawierający toobe danych hello załadowany</span><span class="sxs-lookup"><span data-stu-id="0e84e-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="0e84e-111">tooback się PostgreSQL istniejącej bazy danych lokalnie lub na maszynie wirtualnej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0e84e-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="0e84e-112">Na przykład, jeśli masz lokalny serwer i bazę danych o nazwie **programu testdb** w nim</span><span class="sxs-lookup"><span data-stu-id="0e84e-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="0e84e-113">Przywróć hello danych do obiektu docelowego hello Azure bazy danych dla PostrgeSQL przy użyciu pg_restore</span><span class="sxs-lookup"><span data-stu-id="0e84e-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="0e84e-114">Po utworzeniu hello docelowej bazy danych, można użyć polecenia pg_restore hello i hello -d — dbname parametru toorestore hello dane hello docelowej bazy danych z pliku zrzutu hello.</span><span class="sxs-lookup"><span data-stu-id="0e84e-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="0e84e-115">W tym przykładzie należy przywrócić hello dane z pliku zrzutu hello **testdb.dump** do bazy danych hello **mypgsqldb** na serwerze docelowym **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="0e84e-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="0e84e-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e84e-116">Next steps</span></span>
- <span data-ttu-id="0e84e-117">toomigrate bazy danych programu PostgreSQL przy użyciu eksportu i importu, zobacz [migracji PostgreSQL bazy danych przy użyciu eksportowania i importowania](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="0e84e-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
