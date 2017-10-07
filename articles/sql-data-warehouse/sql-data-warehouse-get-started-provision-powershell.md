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
# <a name="create-sql-data-warehouse-using-powershell"></a>Tworzenie bazy danych w usłudze SQL Data Warehouse przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

W tym artykule opisano, jak toocreate SQL Data Warehouse przy użyciu programu PowerShell.

## <a name="prerequisites"></a>Wymagania wstępne
Rozpoczęto tooget, potrzebne są:

* **Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.
* **Serwer SQL Azure**: zobacz [tworzenie bazy danych Azure SQL w portalu Azure hello] [ Create an Azure SQL database in hello Azure Portal] lub [tworzenie bazy danych Azure SQL przy użyciu programu PowerShell] [ Create an Azure SQL database with PowerShell] więcej szczegółów.
* **Grupa zasobów**: Użyj hello zasobów w tej samej grupy jako serwer Azure SQL, lub zobacz [jak toocreate grupę zasobów](../azure-resource-manager/resource-group-portal.md).
* Masz program **PowerShell w wersji 1.0.3 lub nowszej**: wersję można sprawdzić za pomocą polecenia **Get-Module -ListAvailable -Name Azure**.  Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].  Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.  Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Tworzenie bazy danych w usłudze SQL Data Warehouse
1. Otwórz program Windows PowerShell.
2. Uruchom to polecenie cmdlet toologin tooAzure Menedżera zasobów.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Wybierz subskrypcję hello ma toouse dla bieżącej sesji.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Utwórz bazę danych. W tym przykładzie tworzy bazę danych o nazwie "mynewsqldw" z poziomem celu usługi "DW400" toohello serwer o nazwie "sqldwserver1", który znajduje się w hello grupy zasobów o nazwie "mywesteuroperesgp1".

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Wymagane parametry:

* **RequestedServiceObjectiveName**: hello ilość [DWU] [ DWU] żądania dostępu.  Obsługiwane są następujące wartości: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 i DW6000.
* **DatabaseName**: Nazwa hello hello magazyn danych SQL, który tworzysz.
* **ServerName**: hello nazwę serwera hello, używanej do tworzenia (musi być w wersji 12).
* **ResourceGroupName**: używana grupa zasobów.  toofind dostępnych grup zasobów w ramach subskrypcji, użyj Get-AzureResource.
* **Wersja**: musi być "DataWarehouse" toocreate SQL Data Warehouse.

Opcjonalne parametry:

* **CollationName**: SQL_Latin1_General_CP1_CI_AS jest sortowanie domyślne hello, jeśli nie zostanie określony.  Nie można zmienić sortowania bazy danych.
* **MaxSizeBytes**: hello domyślny maksymalny rozmiar bazy danych wynosi 10 GB.

Więcej szczegółów na temat opcji parametrów hello, zobacz [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] i [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Następne kroki
Po zakończeniu SQL Data Warehouse aprowizacji może być tootry [załadować przykładowe dane] [ loading sample data] lub zbyt poznać sposób[opracowanie] [ develop] , [załadować][load], lub [migracji][migrate].

Jeśli interesuje Cię więcej informacji na temat toomanage SQL Data Warehouse programowo, zapoznaj się z artykułem na temat toouse [poleceń cmdlet programu PowerShell i interfejsów API REST][PowerShell cmdlets and REST APIs].

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
