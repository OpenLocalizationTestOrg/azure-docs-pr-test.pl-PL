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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST dla usługi SQL Data Warehouse
Wiele zadań administracyjnych usługi SQL Data Warehouse można zarządzać za pomocą poleceń cmdlet programu Azure PowerShell lub interfejsów API REST.  Poniżej przedstawiono kilka przykładów sposobu toouse PowerShell poleceń tooautomate typowych zadań w programie SQL Data Warehouse.  Dla niektórych dobre przykłady REST, zobacz artykuł hello [Zarządzanie skalowanie REST][Manage scalability with REST].

> [!NOTE]
> W kolejności toouse programu Azure PowerShell z usługą Magazyn danych SQL, potrzebujesz programu Azure PowerShell w wersji 1.0.3 lub nowszej.  Wersję można sprawdzić, uruchamiając **Get-Module - ListAvailable-Name Azure**.  Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].  Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Wprowadzenie do poleceń cmdlet programu Azure PowerShell
1. Otwórz program Windows PowerShell.
2. W wierszu polecenia programu PowerShell hello Uruchom te polecenia toosign w toohello usługi Azure Resource Manager i wyboru subskrypcji.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Przykład magazynu danych SQL Wstrzymaj
Wstrzymać bazy danych o nazwie "Database02" znajdującej się na serwerze o nazwie "Serwer01".  Serwer Hello jest w grupie zasobów platformy Azure o nazwie "ResourceGroup1."

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Zmiany, w tym przykładzie powoduje przekazanie w potoku hello pobrać obiekt zbyt[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  W związku z tym hello bazy danych zostało wstrzymane. polecenie końcowego Hello przedstawia hello wyników.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Uruchom przykład magazynu danych SQL
Wznów działanie bazy danych o nazwie "Database02" znajdującej się na serwerze o nazwie "Serwer01". powitania serwera znajduje się w grupie zasobów o nazwie "ResourceGroup1."

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Zmiany, w tym przykładzie pobierana bazy danych o nazwie "Database02" z serwerem o nazwie "Serwer01", który jest zawarty w grupie zasobów o nazwie "ResourceGroup1." Przewody hello pobrać obiekt zbyt[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Należy pamiętać, że jeśli serwer jest foo.database.windows.net, użyj "foo" hello - ServerName hello polecenia cmdlet programu PowerShell.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Inne obsługiwane polecenia cmdlet programu PowerShell
Te polecenia cmdlet programu PowerShell są obsługiwane przez Magazyn danych SQL Azure.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [Nowe AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Przywracanie AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [SELECT-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Wstrzymaj AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej przykładów programu PowerShell zobacz:

* [Utwórz magazyn danych SQL przy użyciu programu PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Przywracanie bazy danych][Database restore]

Inne zadania, których można zautomatyzować przy użyciu programu PowerShell, zobacz [polecenia cmdlet bazy danych SQL Azure][Azure SQL Database Cmdlets]. Należy pamiętać, że nie wszystkie polecenia cmdlet bazy danych SQL Azure są obsługiwane dla usługi Azure SQL Data Warehouse.  Aby uzyskać listę zadań, których można zautomatyzować z POZOSTAŁĄ, zobacz [operacje dla baz danych SQL Azure][Operations for Azure SQL Databases].

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
