---
title: "aaaManage obliczeniowe zasilania w usłudze Azure SQL Data Warehouse (PowerShell) | Dokumentacja firmy Microsoft"
description: "Mocy obliczeniowej toomanage zadania programu PowerShell. Zasoby obliczeniowe skali przez dostosowanie wartości dwu. Lub wstrzymywanie i wznawianie koszty toosave zasoby obliczeniowe."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="8414f-105">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8414f-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8414f-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8414f-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="8414f-107">Portal</span><span class="sxs-lookup"><span data-stu-id="8414f-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="8414f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8414f-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="8414f-109">REST</span><span class="sxs-lookup"><span data-stu-id="8414f-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="8414f-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="8414f-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="8414f-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8414f-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="8414f-112">Zainstaluj najnowszą wersję hello programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8414f-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="8414f-113">toouse programu Azure PowerShell z usługą Magazyn danych SQL, potrzebujesz programu Azure PowerShell w wersji 1.0.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8414f-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="8414f-114">tooverify bieżącej wersji Uruchom polecenie hello **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="8414f-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="8414f-115">Można zainstalować najnowszą wersję hello z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="8414f-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="8414f-116">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="8414f-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="8414f-117">Wprowadzenie do poleceń cmdlet programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8414f-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="8414f-118">Rozpoczęto tooget:</span><span class="sxs-lookup"><span data-stu-id="8414f-118">tooget started:</span></span>

1. <span data-ttu-id="8414f-119">Otwórz program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8414f-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8414f-120">W wierszu polecenia programu PowerShell hello Uruchom te polecenia toosign w toohello usługi Azure Resource Manager i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8414f-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="8414f-121">Moc obliczeniową skali</span><span class="sxs-lookup"><span data-stu-id="8414f-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="8414f-122">Witaj toochange jednostek dwu, użyj hello [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8414f-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="8414f-123">Witaj poniższy przykład przedstawia hello usługi poziomu celu tooDW1000 dla bazy danych hello MySQLDW, która jest hostowana na serwerze MyServer.</span><span class="sxs-lookup"><span data-stu-id="8414f-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="8414f-124">Wstrzymaj obliczeń</span><span class="sxs-lookup"><span data-stu-id="8414f-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="8414f-125">toopause bazy danych, użyj hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8414f-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8414f-126">Witaj poniższy przykład wstrzymuje bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01.</span><span class="sxs-lookup"><span data-stu-id="8414f-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8414f-127">Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="8414f-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="8414f-128">Należy pamiętać, że jeśli serwer jest foo.database.windows.net, użyj "foo" hello - ServerName hello polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8414f-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="8414f-129">Zmiany, w tym przykładzie dalej pobiera hello bazy danych do obiektu hello $database.</span><span class="sxs-lookup"><span data-stu-id="8414f-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8414f-130">Go następnie powoduje przekazanie w potoku obiektu hello zbyt[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="8414f-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="8414f-131">wyniki Hello są przechowywane w hello resultDatabase obiektu.</span><span class="sxs-lookup"><span data-stu-id="8414f-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="8414f-132">polecenie końcowego Hello przedstawia hello wyników.</span><span class="sxs-lookup"><span data-stu-id="8414f-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="8414f-133">Wznów obliczeń</span><span class="sxs-lookup"><span data-stu-id="8414f-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="8414f-134">toostart bazy danych, użyj hello [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8414f-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8414f-135">Witaj poniższy przykład uruchamia bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01.</span><span class="sxs-lookup"><span data-stu-id="8414f-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8414f-136">Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="8414f-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="8414f-137">Zmiany, w tym przykładzie dalej pobiera hello bazy danych do obiektu hello $database.</span><span class="sxs-lookup"><span data-stu-id="8414f-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8414f-138">Go następnie powoduje przekazanie w potoku obiektu hello zbyt[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] i przechowuje wyniki hello w $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="8414f-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="8414f-139">polecenie końcowego Hello przedstawia hello wyników.</span><span class="sxs-lookup"><span data-stu-id="8414f-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="8414f-140">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="8414f-140">Check database state</span></span>

<span data-ttu-id="8414f-141">Jak pokazano na powitania powyżej przykłady, można użyć jednego [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] polecenia cmdlet tooget informacji w bazie danych, w tym samym sprawdzanie stanu hello, ale także toouse jako argument.</span><span class="sxs-lookup"><span data-stu-id="8414f-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="8414f-142">Które będą powodować coś, takich jak</span><span class="sxs-lookup"><span data-stu-id="8414f-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="8414f-143">Gdzie następnie sprawdź toosee hello *stan* hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8414f-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="8414f-144">W takim przypadku widać, że ta baza danych jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="8414f-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="8414f-145">Po uruchomieniu tego polecenia, powinien zostać wyświetlony stan wartość albo Online, wstrzymywanie, wznawianie, skalowanie i wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="8414f-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="8414f-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8414f-146">Next steps</span></span>
<span data-ttu-id="8414f-147">Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="8414f-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
