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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Omówienie](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Przed rozpoczęciem
### <a name="install-hello-latest-version-of-azure-powershell"></a>Zainstaluj najnowszą wersję hello programu Azure PowerShell
> [!NOTE]
> toouse programu Azure PowerShell z usługą Magazyn danych SQL, potrzebujesz programu Azure PowerShell w wersji 1.0.3 lub nowszej.  tooverify bieżącej wersji Uruchom polecenie hello **Get-Module - ListAvailable-Name Azure**. Można zainstalować najnowszą wersję hello z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].  Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Wprowadzenie do poleceń cmdlet programu Azure PowerShell
Rozpoczęto tooget:

1. Otwórz program Azure PowerShell.
2. W wierszu polecenia programu PowerShell hello Uruchom te polecenia toosign w toohello usługi Azure Resource Manager i wyboru subskrypcji.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Moc obliczeniową skali
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Witaj toochange jednostek dwu, użyj hello [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] polecenia cmdlet programu PowerShell. Witaj poniższy przykład przedstawia hello usługi poziomu celu tooDW1000 dla bazy danych hello MySQLDW, która jest hostowana na serwerze MyServer.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Wstrzymaj obliczeń
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause bazy danych, użyj hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] polecenia cmdlet. Witaj poniższy przykład wstrzymuje bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01. Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.

> [!NOTE]
> Należy pamiętać, że jeśli serwer jest foo.database.windows.net, użyj "foo" hello - ServerName hello polecenia cmdlet programu PowerShell.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Zmiany, w tym przykładzie dalej pobiera hello bazy danych do obiektu hello $database. Go następnie powoduje przekazanie w potoku obiektu hello zbyt[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. wyniki Hello są przechowywane w hello resultDatabase obiektu. polecenie końcowego Hello przedstawia hello wyników.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Wznów obliczeń
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart bazy danych, użyj hello [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] polecenia cmdlet. Witaj poniższy przykład uruchamia bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01. Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Zmiany, w tym przykładzie dalej pobiera hello bazy danych do obiektu hello $database. Go następnie powoduje przekazanie w potoku obiektu hello zbyt[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] i przechowuje wyniki hello w $resultDatabase. polecenie końcowego Hello przedstawia hello wyników.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Sprawdź stan bazy danych

Jak pokazano na powitania powyżej przykłady, można użyć jednego [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] polecenia cmdlet tooget informacji w bazie danych, w tym samym sprawdzanie stanu hello, ale także toouse jako argument. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

Które będą powodować coś, takich jak 

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

Gdzie następnie sprawdź toosee hello *stan* hello bazy danych. W takim przypadku widać, że ta baza danych jest w trybie online. 

Po uruchomieniu tego polecenia, powinien zostać wyświetlony stan wartość albo Online, wstrzymywanie, wznawianie, skalowanie i wstrzymana.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Następne kroki
Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].

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
