---
title: "Zarządzanie grupami baz danych Azure SQL | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="87670-103">Tworzenie i zarządzanie nimi skalowanej baz danych SQL Azure za pomocą zadania elastyczne (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="87670-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="87670-104">**Zadania elastyczne bazy danych** uprościć zarządzanie grupy baz danych, wykonując operacje administracyjne, takie jak zmiany schematu, Zarządzanie poświadczeniami, aktualizacje danych odwołania, gromadzenia danych wydajności lub telemetrii dzierżawy (klienta) Kolekcja.</span><span class="sxs-lookup"><span data-stu-id="87670-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="87670-105">Zadania elastyczne bazy danych jest obecnie dostępna za pośrednictwem portalu Azure i poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87670-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="87670-106">Niemniej jednak Azure powierzchni portalu zmniejszony ograniczone do wykonania dla wszystkich baz danych w funkcji [puli elastycznej (wersja zapoznawcza)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="87670-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="87670-107">Dostęp do dodatkowych funkcji i wykonywanie skryptów między grupą baz danych w tym niestandardowy kolekcji lub fragmentacji Ustaw (utworzony za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-scale-introduction.md)), zobacz [tworzenie i zarządzanie nimi zadania przy użyciu programu PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="87670-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="87670-108">Aby uzyskać więcej informacji o zadaniach, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87670-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="87670-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="87670-109">Prerequisites</span></span>
* <span data-ttu-id="87670-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="87670-110">An Azure subscription.</span></span> <span data-ttu-id="87670-111">Bezpłatnej wersji próbnej, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87670-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="87670-112">Puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="87670-112">An elastic pool.</span></span> <span data-ttu-id="87670-113">Zobacz [o pule elastyczne](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="87670-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="87670-114">Instalacja składników usługi zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="87670-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="87670-115">Zobacz [instalowania usługi zadania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="87670-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="87670-116">Tworzenie zadania</span><span class="sxs-lookup"><span data-stu-id="87670-116">Creating jobs</span></span>
1. <span data-ttu-id="87670-117">Przy użyciu [portalu Azure](https://portal.azure.com), z istniejącej elastycznej puli baz danych zadania, kliknij przycisk **Utwórz zadanie**.</span><span class="sxs-lookup"><span data-stu-id="87670-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="87670-118">Wpisz nazwę użytkownika i hasło administratora bazy danych (utworzone podczas instalacji zadania) dla bazy danych kontroli zadania (magazynu metadanych dla zadania).</span><span class="sxs-lookup"><span data-stu-id="87670-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Nazwa zadania, wpisz lub Wklej w kodzie i kliknij przycisk Uruchom][1]
3. <span data-ttu-id="87670-120">W **Utwórz zadanie** bloku, wpisz nazwę zadania.</span><span class="sxs-lookup"><span data-stu-id="87670-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="87670-121">Wpisz nazwę użytkownika i hasło, aby połączyć się z docelowymi bazami danych z wystarczającymi uprawnieniami do pomyślnego wykonania skryptów.</span><span class="sxs-lookup"><span data-stu-id="87670-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="87670-122">Wklej lub typ skryptu T-SQL.</span><span class="sxs-lookup"><span data-stu-id="87670-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="87670-123">Kliknij przycisk **zapisać** , a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="87670-123">Click **Save** and then click **Run**.</span></span>
   
    ![Tworzenie zadań i uruchom][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="87670-125">Uruchamianie zadań idempotentności</span><span class="sxs-lookup"><span data-stu-id="87670-125">Run idempotent jobs</span></span>
<span data-ttu-id="87670-126">Po uruchomieniu skryptu na podstawie zestawu baz danych, należy się upewnić, że skrypt jest idempotentności.</span><span class="sxs-lookup"><span data-stu-id="87670-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="87670-127">Oznacza to, że skryptu musi być można uruchamiać wielokrotnie, nawet jeśli go nie powiodło się przed niekompletna.</span><span class="sxs-lookup"><span data-stu-id="87670-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="87670-128">Na przykład, jeśli skrypt zakończy się niepowodzeniem, zadanie będzie automatycznie ponawiana dopóki próba powiedzie się (w granicach, jako retry logiki ostatecznie przestaną ponawianie próby).</span><span class="sxs-lookup"><span data-stu-id="87670-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="87670-129">Sposób, w tym celu jest użycie klauzuli "Jeśli ISTNIEJE" i usunąć wszystkie znalezione wystąpienia przed utworzeniem nowego obiektu.</span><span class="sxs-lookup"><span data-stu-id="87670-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="87670-130">Przykładem jest następujący:</span><span class="sxs-lookup"><span data-stu-id="87670-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="87670-131">Alternatywnie można użyć klauzuli "Jeśli nie ISTNIEJE" przed utworzeniem nowego wystąpienia:</span><span class="sxs-lookup"><span data-stu-id="87670-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="87670-132">Ten skrypt aktualizacji następnie tabeli utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="87670-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="87670-133">Sprawdzanie stanu zadania</span><span class="sxs-lookup"><span data-stu-id="87670-133">Checking job status</span></span>
<span data-ttu-id="87670-134">Po rozpoczęciu zadania, można sprawdzić jego postępu.</span><span class="sxs-lookup"><span data-stu-id="87670-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="87670-135">Na stronie puli elastycznej kliknij **zarządzać zadaniami**.</span><span class="sxs-lookup"><span data-stu-id="87670-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Kliknij pozycję "Zarządzaj zadania"][2]
2. <span data-ttu-id="87670-137">Kliknij nazwę () zadania.</span><span class="sxs-lookup"><span data-stu-id="87670-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="87670-138">**Stan** może być "Ukończone" lub "Nie powiodło się."</span><span class="sxs-lookup"><span data-stu-id="87670-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="87670-139">Szczegóły zadania zostaną wyświetlone (b) z jego datę i godzinę tworzenia i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="87670-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="87670-140">Listy (c) poniżej się, że będzie wyświetlany postęp skryptu dla każdej bazy danych w puli, podając jego szczegóły daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="87670-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Zakończono zadania sprawdzania][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="87670-142">Sprawdzanie zadania zakończone niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="87670-142">Checking failed jobs</span></span>
<span data-ttu-id="87670-143">Jeśli zadanie nie powiedzie się, można znaleźć w dzienniku wykonywania.</span><span class="sxs-lookup"><span data-stu-id="87670-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="87670-144">Kliknij nazwę zadania nie powiodło się, aby wyświetlić jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="87670-144">Click the name of the failed job to see its details.</span></span>

![Sprawdź zadanie zakończone niepowodzeniem][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


