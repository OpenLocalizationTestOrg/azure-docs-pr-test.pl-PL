---
title: grupy aaaManage baz danych Azure SQL | Dokumentacja firmy Microsoft
description: "Przeprowadzenie tworzenie i zarządzanie elastycznej zadania."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="59da4-103">Tworzenie i zarządzanie nimi skalowanej baz danych SQL Azure za pomocą zadania elastyczne (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="59da4-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="59da4-104">**Zadania elastyczne bazy danych** uprościć zarządzanie grupy baz danych, wykonując operacje administracyjne, takie jak zmiany schematu, Zarządzanie poświadczeniami, aktualizacje danych odwołania, gromadzenia danych wydajności lub telemetrii dzierżawy (klienta) Kolekcja.</span><span class="sxs-lookup"><span data-stu-id="59da4-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="59da4-105">Zadania elastyczne bazy danych jest obecnie dostępna za pośrednictwem hello portalu Azure i poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59da4-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="59da4-106">Jednak hello Azure powierzchni portalu ograniczonej funkcjonalności ograniczony tooexecution dla wszystkich baz danych w [puli elastycznej (wersja zapoznawcza)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="59da4-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="59da4-107">Ustaw dodatkowe funkcje tooaccess i wykonywanie skryptów między grupą baz danych w tym niestandardowy kolekcji lub fragmentacji (utworzone za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-scale-introduction.md)), zobacz [tworzenie i zarządzanie nimi zadania przy użyciu programu PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="59da4-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="59da4-108">Aby uzyskać więcej informacji o zadaniach, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59da4-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="59da4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59da4-109">Prerequisites</span></span>
* <span data-ttu-id="59da4-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59da4-110">An Azure subscription.</span></span> <span data-ttu-id="59da4-111">Bezpłatnej wersji próbnej, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59da4-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="59da4-112">Puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="59da4-112">An elastic pool.</span></span> <span data-ttu-id="59da4-113">Zobacz [o pule elastyczne](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="59da4-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="59da4-114">Instalacja składników usługi zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="59da4-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="59da4-115">Zobacz [instalowania usługi zadania elastycznej bazy danych hello](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="59da4-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="59da4-116">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="59da4-116">Creating jobs</span></span>
1. <span data-ttu-id="59da4-117">Przy użyciu hello [portalu Azure](https://portal.azure.com), z istniejącej elastycznej puli baz danych zadania, kliknij przycisk **Utwórz zadanie**.</span><span class="sxs-lookup"><span data-stu-id="59da4-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="59da4-118">Wpisz hello nazwę użytkownika i hasło administratora bazy danych hello (utworzone podczas instalacji zadania) dla bazy danych kontroli zadania hello (magazynu metadanych dla zadania).</span><span class="sxs-lookup"><span data-stu-id="59da4-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Nazwa zadania hello, wpisz lub Wklej w kodzie i kliknij przycisk Uruchom][1]
3. <span data-ttu-id="59da4-120">W hello **Utwórz zadanie** bloku, wpisz nazwę zadania hello.</span><span class="sxs-lookup"><span data-stu-id="59da4-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="59da4-121">Wpisz hello użytkownika nazwę i hasło tooconnect toohello docelowymi bazami danych z wystarczającymi uprawnieniami toosucceed wykonanie skryptu.</span><span class="sxs-lookup"><span data-stu-id="59da4-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="59da4-122">Wklej lub wpisz w skrypcie hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="59da4-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="59da4-123">Kliknij przycisk **zapisać** , a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="59da4-123">Click **Save** and then click **Run**.</span></span>
   
    ![Tworzenie zadań i uruchom][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="59da4-125">Uruchamianie zadań idempotentności</span><span class="sxs-lookup"><span data-stu-id="59da4-125">Run idempotent jobs</span></span>
<span data-ttu-id="59da4-126">Po uruchomieniu skryptu na podstawie zestawu baz danych, należy się, że skrypt hello idempotentności.</span><span class="sxs-lookup"><span data-stu-id="59da4-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="59da4-127">Oznacza to, hello skryptu musi być możliwe toorun wielokrotnie, nawet jeśli go nie powiodło się przed niekompletna.</span><span class="sxs-lookup"><span data-stu-id="59da4-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="59da4-128">Na przykład w przypadku awarii skryptu hello zadanie będzie automatycznie ponawiana dopóki próba powiedzie się (w granicach, jako ponawiania hello logiki ostatecznie przestaną hello ponawianie próby).</span><span class="sxs-lookup"><span data-stu-id="59da4-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="59da4-129">toodo sposób Hello jest toouse hello klauzuli "Jeśli ISTNIEJE" i usunąć wszystkie znalezione wystąpienia przed utworzeniem nowego obiektu.</span><span class="sxs-lookup"><span data-stu-id="59da4-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="59da4-130">Przykładem jest następujący:</span><span class="sxs-lookup"><span data-stu-id="59da4-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="59da4-131">Alternatywnie można użyć klauzuli "Jeśli nie ISTNIEJE" przed utworzeniem nowego wystąpienia:</span><span class="sxs-lookup"><span data-stu-id="59da4-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="59da4-132">Ten skrypt aktualizacji następnie tabeli hello utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="59da4-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="59da4-133">Sprawdzanie stanu zadania</span><span class="sxs-lookup"><span data-stu-id="59da4-133">Checking job status</span></span>
<span data-ttu-id="59da4-134">Po rozpoczęciu zadania, można sprawdzić jego postępu.</span><span class="sxs-lookup"><span data-stu-id="59da4-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="59da4-135">Na stronie puli elastycznej powitania kliknij przycisk **zarządzać zadaniami**.</span><span class="sxs-lookup"><span data-stu-id="59da4-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Kliknij pozycję "Zarządzaj zadania"][2]
2. <span data-ttu-id="59da4-137">Polecenie hello nazwę () zadania.</span><span class="sxs-lookup"><span data-stu-id="59da4-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="59da4-138">Witaj **stan** może być "Ukończone" lub "Nie powiodło się."</span><span class="sxs-lookup"><span data-stu-id="59da4-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="59da4-139">Szczegóły zadania Hello wyświetlane (b) z jego datę i godzinę tworzenia i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="59da4-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="59da4-140">Lista Hello (c) poniżej hello pokazującego postęp hello hello skryptu dla każdej bazy danych w puli hello, w ze szczegółami jego daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="59da4-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Zakończono zadania sprawdzania][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="59da4-142">Sprawdzanie zadania zakończone niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="59da4-142">Checking failed jobs</span></span>
<span data-ttu-id="59da4-143">Jeśli zadanie nie powiedzie się, można znaleźć w dzienniku wykonywania.</span><span class="sxs-lookup"><span data-stu-id="59da4-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="59da4-144">Kliknij nazwę hello hello nie powiodło się zadanie toosee jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="59da4-144">Click hello name of hello failed job toosee its details.</span></span>

![Sprawdź zadanie zakończone niepowodzeniem][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


