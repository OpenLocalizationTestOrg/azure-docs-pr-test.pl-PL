---
title: aaaCreate SQL Data Warehouse w portalu Azure hello | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak hello przez toocreate usługi Azure SQL Data Warehouse w portalu Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="7a703-103">Tworzenie bazy danych w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7a703-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a703-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a703-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="7a703-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="7a703-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="7a703-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a703-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="7a703-107">W tym samouczku używana hello toocreate portalu Azure SQL Data Warehouse zawierającą przykładową bazę danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7a703-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a703-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7a703-108">Prerequisites</span></span>
<span data-ttu-id="7a703-109">Rozpoczęto tooget, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="7a703-109">tooget started, you need:</span></span>

* <span data-ttu-id="7a703-110">**Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="7a703-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="7a703-111">**Azure SQL server**: zobacz [tworzenie bazy danych Azure SQL z portalu Azure hello] [ Create an Azure SQL database in hello Azure portal] więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="7a703-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="7a703-112">Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="7a703-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="7a703-113">Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="7a703-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="7a703-114">Tworzenie bazy danych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7a703-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="7a703-115">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a703-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7a703-116">Kliknij kolejno pozycje **+ Nowy** > **Bazy danych** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="7a703-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Przycisk Utwórz](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="7a703-118">W hello **SQL Data Warehouse** bloku, wypełnij hello potrzebne informacje, naciśnij klawisz toocreate "Utwórz".</span><span class="sxs-lookup"><span data-stu-id="7a703-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Tworzenie bazy danych](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="7a703-120">**Serwer**: zalecamy, aby najpierw wybrać serwer.</span><span class="sxs-lookup"><span data-stu-id="7a703-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="7a703-121">**Nazwa bazy danych**: hello nazwę, która jest używana tooreference hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7a703-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="7a703-122">Musi być unikatowy toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="7a703-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="7a703-123">**Wydajność**: zalecamy rozpoczynanie od 400 jednostek [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="7a703-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="7a703-124">Można przenieść hello toohello suwak w lewo lub w prawo tooadjust hello wydajności magazynu danych lub skalowania w górę lub w dół po utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="7a703-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="7a703-125">toolearn więcej informacji na temat jednostek dwu, zobacz dokumentację dotyczącą na [skalowanie](sql-data-warehouse-manage-compute-overview.md) lub nasz [cennikiem][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="7a703-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="7a703-126">**Subskrypcja**: Wybierz hello [subskrypcji] który tej usługi SQL Data Warehouse będzie naliczać opłaty do.</span><span class="sxs-lookup"><span data-stu-id="7a703-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="7a703-127">**Grupa zasobów**: [grup zasobów] [ Resource group] są toohelp kontenery, które zarządzanie kolekcją zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="7a703-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="7a703-128">Dowiedz się więcej o [grupach zasobów](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a703-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="7a703-129">**Wybierz źródło**: kliknij kolejno **Wybierz źródło**  >  **Przykład**.</span><span class="sxs-lookup"><span data-stu-id="7a703-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="7a703-130">Azure automatycznie wypełnia hello **wybierz przykład** nazwą AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7a703-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a703-131">Witaj sortowanie domyślne dla magazynu danych SQL jest SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="7a703-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="7a703-132">W razie potrzeby posortowane w różny sposób [T-SQL] [ T-SQL] mogą być używane toocreate hello z bazy danych o różnych ustawieniach sortowania.</span><span class="sxs-lookup"><span data-stu-id="7a703-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="7a703-133">Kliknij przycisk **Utwórz** toocreate Twojego SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7a703-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="7a703-134">Poczekaj kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7a703-134">Wait for a few minutes.</span></span> <span data-ttu-id="7a703-135">Gdy magazyn danych jest gotowy, powinien nastąpić powrót toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a703-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7a703-136">Można znaleźć magazynu danych SQL na pulpicie nawigacyjnym, kategorii bazy danych SQL, lub w zasobie hello grupy tego toocreate można używać go.</span><span class="sxs-lookup"><span data-stu-id="7a703-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![widok portalu](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="7a703-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a703-138">Next steps</span></span>
<span data-ttu-id="7a703-139">Po utworzeniu magazynu danych SQL, wszystko jest gotowe za[Connect](sql-data-warehouse-connect-overview.md) i wykonywanie zapytań.</span><span class="sxs-lookup"><span data-stu-id="7a703-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="7a703-140">tooload dane do usługi SQL Data Warehouse, zobacz hello [omówienie ładowania](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="7a703-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="7a703-141">Jeśli próbujesz toomigrate tooSQL istniejącej bazy danych magazynu danych, zobacz hello [Omówienie migracji](sql-data-warehouse-overview-migrate.md) lub użyj [narzędzia do migracji](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="7a703-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="7a703-142">Reguły zapory można również skonfigurować za pomocą języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="7a703-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="7a703-143">Aby uzyskać więcej informacji, zobacz artykuły dotyczące poleceń [sp_set_firewall_rule][sp_set_firewall_rule] i [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="7a703-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="7a703-144">Istnieje również toolook pomysł na powitania [najlepsze rozwiązania][Best practices].</span><span class="sxs-lookup"><span data-stu-id="7a703-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[subskrypcji]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
