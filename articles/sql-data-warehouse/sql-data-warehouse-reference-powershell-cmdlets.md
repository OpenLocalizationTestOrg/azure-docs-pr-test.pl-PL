---
title: polecenia cmdlet aaaPowerShell dla magazynu danych SQL Azure
description: "Znajdź hello top poleceń cmdlet programu PowerShell dla usługi Azure SQL Data Warehouse w tym jak toopause i wznowić bazy danych."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="1176a-103">Polecenia cmdlet programu PowerShell i interfejsów API REST dla usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1176a-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="1176a-104">Wiele zadań administracyjnych usługi SQL Data Warehouse można zarządzać za pomocą poleceń cmdlet programu Azure PowerShell lub interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="1176a-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="1176a-105">Poniżej przedstawiono kilka przykładów sposobu toouse PowerShell poleceń tooautomate typowych zadań w programie SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1176a-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="1176a-106">Dla niektórych dobre przykłady REST, zobacz artykuł hello [Zarządzanie skalowanie REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="1176a-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="1176a-107">W kolejności toouse programu Azure PowerShell z usługą Magazyn danych SQL, potrzebujesz programu Azure PowerShell w wersji 1.0.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1176a-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="1176a-108">Wersję można sprawdzić, uruchamiając **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="1176a-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="1176a-109">Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="1176a-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="1176a-110">Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="1176a-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="1176a-111">Wprowadzenie do poleceń cmdlet programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1176a-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="1176a-112">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1176a-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1176a-113">W wierszu polecenia programu PowerShell hello Uruchom te polecenia toosign w toohello usługi Azure Resource Manager i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1176a-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="1176a-114">Przykład magazynu danych SQL Wstrzymaj</span><span class="sxs-lookup"><span data-stu-id="1176a-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="1176a-115">Wstrzymać bazy danych o nazwie "Database02" znajdującej się na serwerze o nazwie "Serwer01".</span><span class="sxs-lookup"><span data-stu-id="1176a-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="1176a-116">Serwer Hello jest w grupie zasobów platformy Azure o nazwie "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="1176a-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="1176a-117">Zmiany, w tym przykładzie powoduje przekazanie w potoku hello pobrać obiekt zbyt[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1176a-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="1176a-118">W związku z tym hello bazy danych zostało wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="1176a-118">As a result, hello database is paused.</span></span> <span data-ttu-id="1176a-119">polecenie końcowego Hello przedstawia hello wyników.</span><span class="sxs-lookup"><span data-stu-id="1176a-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="1176a-120">Uruchom przykład magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="1176a-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="1176a-121">Wznów działanie bazy danych o nazwie "Database02" znajdującej się na serwerze o nazwie "Serwer01".</span><span class="sxs-lookup"><span data-stu-id="1176a-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="1176a-122">powitania serwera znajduje się w grupie zasobów o nazwie "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="1176a-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="1176a-123">Zmiany, w tym przykładzie pobierana bazy danych o nazwie "Database02" z serwerem o nazwie "Serwer01", który jest zawarty w grupie zasobów o nazwie "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="1176a-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="1176a-124">Przewody hello pobrać obiekt zbyt[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1176a-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="1176a-125">Należy pamiętać, że jeśli serwer jest foo.database.windows.net, użyj "foo" hello - ServerName hello polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1176a-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="1176a-126">Inne obsługiwane polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1176a-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="1176a-127">Te polecenia cmdlet programu PowerShell są obsługiwane przez Magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1176a-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="1176a-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="1176a-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="1176a-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="1176a-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="1176a-131">[Nowe AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-133">[Przywracanie AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-135">[SELECT-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="1176a-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="1176a-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1176a-137">[Wstrzymaj AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1176a-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1176a-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1176a-138">Next steps</span></span>
<span data-ttu-id="1176a-139">Aby uzyskać więcej przykładów programu PowerShell zobacz:</span><span class="sxs-lookup"><span data-stu-id="1176a-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="1176a-140">[Utwórz magazyn danych SQL przy użyciu programu PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="1176a-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="1176a-141">[Przywracanie bazy danych][Database restore]</span><span class="sxs-lookup"><span data-stu-id="1176a-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="1176a-142">Inne zadania, których można zautomatyzować przy użyciu programu PowerShell, zobacz [polecenia cmdlet bazy danych SQL Azure][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="1176a-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="1176a-143">Należy pamiętać, że nie wszystkie polecenia cmdlet bazy danych SQL Azure są obsługiwane dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1176a-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="1176a-144">Aby uzyskać listę zadań, których można zautomatyzować z POZOSTAŁĄ, zobacz [operacje dla baz danych SQL Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="1176a-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
