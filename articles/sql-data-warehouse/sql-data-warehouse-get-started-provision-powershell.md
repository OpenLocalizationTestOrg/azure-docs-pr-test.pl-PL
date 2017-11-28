---
title: "aaaCreate SQL Data Warehouse przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Tworzenie bazy danych w usłudze SQL Data Warehouse za pomocą programu PowerShell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="afc39-103">Tworzenie bazy danych w usłudze SQL Data Warehouse przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc39-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afc39-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="afc39-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="afc39-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="afc39-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="afc39-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc39-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="afc39-107">W tym artykule opisano, jak toocreate SQL Data Warehouse przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc39-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afc39-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afc39-108">Prerequisites</span></span>
<span data-ttu-id="afc39-109">Rozpoczęto tooget, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="afc39-109">tooget started, you need:</span></span>

* <span data-ttu-id="afc39-110">**Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="afc39-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="afc39-111">**Serwer SQL Azure**: zobacz [tworzenie bazy danych Azure SQL w portalu Azure hello] [ Create an Azure SQL database in hello Azure Portal] lub [tworzenie bazy danych Azure SQL przy użyciu programu PowerShell] [ Create an Azure SQL database with PowerShell] więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="afc39-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="afc39-112">**Grupa zasobów**: Użyj hello zasobów w tej samej grupy jako serwer Azure SQL, lub zobacz [jak toocreate grupę zasobów](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="afc39-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="afc39-113">Masz program **PowerShell w wersji 1.0.3 lub nowszej**: wersję można sprawdzić za pomocą polecenia **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="afc39-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="afc39-114">Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="afc39-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="afc39-115">Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="afc39-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="afc39-116">Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="afc39-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="afc39-117">Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="afc39-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="afc39-118">Tworzenie bazy danych w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="afc39-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="afc39-119">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc39-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="afc39-120">Uruchom to polecenie cmdlet toologin tooAzure Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="afc39-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="afc39-121">Wybierz subskrypcję hello ma toouse dla bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="afc39-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="afc39-122">Utwórz bazę danych.</span><span class="sxs-lookup"><span data-stu-id="afc39-122">Create database.</span></span> <span data-ttu-id="afc39-123">W tym przykładzie tworzy bazę danych o nazwie "mynewsqldw" z poziomem celu usługi "DW400" toohello serwer o nazwie "sqldwserver1", który znajduje się w hello grupy zasobów o nazwie "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="afc39-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="afc39-124">Wymagane parametry:</span><span class="sxs-lookup"><span data-stu-id="afc39-124">Required Parameters are:</span></span>

* <span data-ttu-id="afc39-125">**RequestedServiceObjectiveName**: hello ilość [DWU] [ DWU] żądania dostępu.</span><span class="sxs-lookup"><span data-stu-id="afc39-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="afc39-126">Obsługiwane są następujące wartości: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 i DW6000.</span><span class="sxs-lookup"><span data-stu-id="afc39-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="afc39-127">**DatabaseName**: Nazwa hello hello magazyn danych SQL, który tworzysz.</span><span class="sxs-lookup"><span data-stu-id="afc39-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="afc39-128">**ServerName**: hello nazwę serwera hello, używanej do tworzenia (musi być w wersji 12).</span><span class="sxs-lookup"><span data-stu-id="afc39-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="afc39-129">**ResourceGroupName**: używana grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="afc39-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="afc39-130">toofind dostępnych grup zasobów w ramach subskrypcji, użyj Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="afc39-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="afc39-131">**Wersja**: musi być "DataWarehouse" toocreate SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="afc39-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="afc39-132">Opcjonalne parametry:</span><span class="sxs-lookup"><span data-stu-id="afc39-132">Optional Parameters are:</span></span>

* <span data-ttu-id="afc39-133">**CollationName**: SQL_Latin1_General_CP1_CI_AS jest sortowanie domyślne hello, jeśli nie zostanie określony.</span><span class="sxs-lookup"><span data-stu-id="afc39-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="afc39-134">Nie można zmienić sortowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="afc39-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="afc39-135">**MaxSizeBytes**: hello domyślny maksymalny rozmiar bazy danych wynosi 10 GB.</span><span class="sxs-lookup"><span data-stu-id="afc39-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="afc39-136">Więcej szczegółów na temat opcji parametrów hello, zobacz [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] i [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="afc39-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="afc39-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afc39-137">Next steps</span></span>
<span data-ttu-id="afc39-138">Po zakończeniu SQL Data Warehouse aprowizacji może być tootry [załadować przykładowe dane] [ loading sample data] lub zbyt poznać sposób[opracowanie] [ develop] , [załadować][load], lub [migracji][migrate].</span><span class="sxs-lookup"><span data-stu-id="afc39-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="afc39-139">Jeśli interesuje Cię więcej informacji na temat toomanage SQL Data Warehouse programowo, zapoznaj się z artykułem na temat toouse [poleceń cmdlet programu PowerShell i interfejsów API REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="afc39-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
