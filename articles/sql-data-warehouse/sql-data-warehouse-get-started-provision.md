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
# <a name="create-an-azure-sql-data-warehouse"></a>Tworzenie bazy danych w usłudze Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

W tym samouczku używana hello toocreate portalu Azure SQL Data Warehouse zawierającą przykładową bazę danych AdventureWorksDW.

## <a name="prerequisites"></a>Wymagania wstępne
Rozpoczęto tooget, potrzebne są:

* **Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.
* **Azure SQL server**: zobacz [tworzenie bazy danych Azure SQL z portalu Azure hello] [ Create an Azure SQL database in hello Azure portal] więcej szczegółów.

> [!NOTE]
> Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.  Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Tworzenie bazy danych w usłudze SQL Data Warehouse
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij kolejno pozycje **+ Nowy** > **Bazy danych** > **SQL Data Warehouse**.

    ![Przycisk Utwórz](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. W hello **SQL Data Warehouse** bloku, wypełnij hello potrzebne informacje, naciśnij klawisz toocreate "Utwórz".

    ![Tworzenie bazy danych](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Serwer**: zalecamy, aby najpierw wybrać serwer.  
   * **Nazwa bazy danych**: hello nazwę, która jest używana tooreference hello SQL Data Warehouse.  Musi być unikatowy toohello serwera.
   * **Wydajność**: zalecamy rozpoczynanie od 400 jednostek [DWU][DWU]. Można przenieść hello toohello suwak w lewo lub w prawo tooadjust hello wydajności magazynu danych lub skalowania w górę lub w dół po utworzeniu.  toolearn więcej informacji na temat jednostek dwu, zobacz dokumentację dotyczącą na [skalowanie](sql-data-warehouse-manage-compute-overview.md) lub nasz [cennikiem][SQL Data Warehouse pricing].
   * **Subskrypcja**: Wybierz hello [subskrypcji] który tej usługi SQL Data Warehouse będzie naliczać opłaty do.
   * **Grupa zasobów**: [grup zasobów] [ Resource group] są toohelp kontenery, które zarządzanie kolekcją zasobów systemu Azure. Dowiedz się więcej o [grupach zasobów](../azure-resource-manager/resource-group-overview.md).
   * **Wybierz źródło**: kliknij kolejno **Wybierz źródło**  >  **Przykład**. Azure automatycznie wypełnia hello **wybierz przykład** nazwą AdventureWorksDW.

   > [!NOTE]
   > Witaj sortowanie domyślne dla magazynu danych SQL jest SQL_Latin1_General_CP1_CI_AS. W razie potrzeby posortowane w różny sposób [T-SQL] [ T-SQL] mogą być używane toocreate hello z bazy danych o różnych ustawieniach sortowania.
   >
   >

1. Kliknij przycisk **Utwórz** toocreate Twojego SQL Data Warehouse.
2. Poczekaj kilka minut. Gdy magazyn danych jest gotowy, powinien nastąpić powrót toohello [portalu Azure](https://portal.azure.com). Można znaleźć magazynu danych SQL na pulpicie nawigacyjnym, kategorii bazy danych SQL, lub w zasobie hello grupy tego toocreate można używać go.

    ![widok portalu](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Następne kroki
Po utworzeniu magazynu danych SQL, wszystko jest gotowe za[Connect](sql-data-warehouse-connect-overview.md) i wykonywanie zapytań.

tooload dane do usługi SQL Data Warehouse, zobacz hello [omówienie ładowania](sql-data-warehouse-overview-load.md).

Jeśli próbujesz toomigrate tooSQL istniejącej bazy danych magazynu danych, zobacz hello [Omówienie migracji](sql-data-warehouse-overview-migrate.md) lub użyj [narzędzia do migracji](sql-data-warehouse-migrate-migration-utility.md).

Reguły zapory można również skonfigurować za pomocą języka Transact-SQL. Aby uzyskać więcej informacji, zobacz artykuły dotyczące poleceń [sp_set_firewall_rule][sp_set_firewall_rule] i [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Istnieje również toolook pomysł na powitania [najlepsze rozwiązania][Best practices].

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
