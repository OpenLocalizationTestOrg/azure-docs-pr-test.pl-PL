---
title: Tworzenie magazynu danych SQL Data Warehouse w witrynie Azure Portal | Microsoft Docs
description: "Dowiedz się, jak utworzyć bazę danych w usłudze Azure SQL Data Warehouse w portalu Azure"
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
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="80073-103">Tworzenie bazy danych w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="80073-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80073-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="80073-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="80073-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="80073-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="80073-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80073-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="80073-107">Z tego samouczka dowiesz się, jak za pomocą witryny Azure Portal utworzyć bazę danych w usłudze SQL Data Warehouse zawierającą przykładową bazę danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="80073-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80073-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80073-108">Prerequisites</span></span>
<span data-ttu-id="80073-109">Aby rozpocząć pracę, potrzebne będą następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="80073-109">To get started, you need:</span></span>

* <span data-ttu-id="80073-110">**Konto platformy Azure**: aby utworzyć konto, odwiedź witrynę [Bezpłatna wersja próbna platformy Azure][Azure Free Trial] lub [Środki na korzystanie z systemu Azure w ramach usługi MSDN][MSDN Azure Credits].</span><span class="sxs-lookup"><span data-stu-id="80073-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="80073-111">**Serwer Azure SQL**: aby uzyskać więcej informacji, zobacz [Tworzenie bazy danych Azure SQL Database przy użyciu witryny Azure Portal][Create an Azure SQL database in the Azure portal].</span><span class="sxs-lookup"><span data-stu-id="80073-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="80073-112">Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="80073-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="80073-113">Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="80073-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="80073-114">Tworzenie bazy danych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="80073-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="80073-115">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80073-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="80073-116">Kliknij kolejno pozycje **+ Nowy** > **Bazy danych** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="80073-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Tworzenie](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="80073-118">W bloku **SQL Data Warehouse** podaj potrzebne informacje, a następnie naciśnij przycisk „Utwórz”, aby utworzyć usługę.</span><span class="sxs-lookup"><span data-stu-id="80073-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Tworzenie bazy danych](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="80073-120">**Serwer**: zalecamy, aby najpierw wybrać serwer.</span><span class="sxs-lookup"><span data-stu-id="80073-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="80073-121">**Nazwa bazy danych**: Nazwa używana jako odwołanie do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="80073-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="80073-122">Musi być unikatowa dla serwera.</span><span class="sxs-lookup"><span data-stu-id="80073-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="80073-123">**Wydajność**: zalecamy rozpoczynanie od 400 jednostek [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="80073-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="80073-124">Możesz przesuwać suwak w lewo lub w prawo, aby dostosować wydajność magazynu danych albo skalować w górę lub w dół po utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="80073-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="80073-125">Aby dowiedzieć się więcej o jednostkach DWU, zobacz dokumentację dotyczącą [skalowania](sql-data-warehouse-manage-compute-overview.md) lub [nasz cennik][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="80073-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="80073-126">**Subskrypcja**: Wybierz [Subskrypcja], która będzie obciążana płatnościami za tę usługę SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="80073-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="80073-127">**Grupa zasobów**: [grupy zasobów][Resource group] to kontenery, które mają ułatwiać zarządzanie kolekcją zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="80073-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="80073-128">Dowiedz się więcej o [grupach zasobów](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80073-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="80073-129">**Wybierz źródło**: kliknij kolejno **Wybierz źródło**  >  **Przykład**.</span><span class="sxs-lookup"><span data-stu-id="80073-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="80073-130">Platforma Azure automatycznie wypełni opcję **Wybierz przykład** bazą danych AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="80073-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80073-131">Sortowanie domyślne dla usługi SQL Data Warehouse to SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="80073-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="80073-132">Jeśli jest potrzebne inne sortowanie, za pomocą polecenia języka [T-SQL][T-SQL] można utworzyć bazę danych z innym sortowaniem.</span><span class="sxs-lookup"><span data-stu-id="80073-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="80073-133">Kliknij przycisk **Utwórz**, aby utworzyć usługę SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="80073-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="80073-134">Poczekaj kilka minut.</span><span class="sxs-lookup"><span data-stu-id="80073-134">Wait for a few minutes.</span></span> <span data-ttu-id="80073-135">Po utworzeniu magazynu danych powinien nastąpić powrót do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80073-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80073-136">Usługę SQL Data Warehouse można znaleźć na pulpicie nawigacyjnym, na liście Bazy danych SQL lub w grupie zasobów użytej podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="80073-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![widok portalu](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="80073-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80073-138">Next steps</span></span>
<span data-ttu-id="80073-139">Po utworzeniu bazy danych w usłudze SQL Data Warehouse można rozpocząć [nawiązywanie połączenia](sql-data-warehouse-connect-overview.md) i wykonywanie zapytań.</span><span class="sxs-lookup"><span data-stu-id="80073-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="80073-140">Aby załadować dane do usługi SQL Data Warehouse, zobacz [omówienie ładowania](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="80073-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="80073-141">Jeśli próbujesz przeprowadzić migrację z istniejącej bazy danych do usługi SQL Data Warehouse, zobacz [omówienie migracji](sql-data-warehouse-overview-migrate.md) lub użyj [narzędzia do migracji](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="80073-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="80073-142">Reguły zapory można również skonfigurować za pomocą języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="80073-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="80073-143">Aby uzyskać więcej informacji, zobacz artykuły dotyczące poleceń [sp_set_firewall_rule][sp_set_firewall_rule] i [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="80073-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="80073-144">Warto również zapoznać się z artykułem [Najlepsze praktyki][Best practices].</span><span class="sxs-lookup"><span data-stu-id="80073-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="80073-145">[Subskrypcja]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="80073-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
