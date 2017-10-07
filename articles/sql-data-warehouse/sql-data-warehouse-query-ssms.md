---
title: "aaaConnect tooAzure SQL Data Warehouse — SSMS | Dokumentacja firmy Microsoft"
description: "Użyj programu SQL Server Management Studio (SSMS) tooconnect tooand zapytania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Połącz tooSQL magazynu danych z programu SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Użyj programu SQL Server Management Studio (SSMS) tooconnect tooand zapytania usługi Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Wymagania wstępne
toouse tego samouczka należy:

* Istniejący magazyn danych SQL. Zobacz toocreate, [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) zainstalowany. [Zainstaluj narzędzia SSMS] [ Install SSMS] bezpłatnie, jeśli nie masz jeszcze go.
* Witaj w pełni kwalifikowana nazwa serwera SQL. toofind tego, zobacz [połączyć tooSQL hurtowni danych][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Połącz tooyour SQL Data Warehouse
1. Otwórz program SSMS.
2. Otwórz Eksplorator obiektów. toodo ten, wybierz **pliku** > **połączyć Eksplorator obiektów**.
   
    ![Eksplorator obiektów SQL Server][1]
3. Wypełnij pola hello hello Connect tooServer okna.
   
    ![Połącz tooServer][2]
   
   * **Nazwa serwera**. Wprowadź hello **nazwy serwera** wcześniej ustaloną.
   * **Uwierzytelnianie**. Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.
   * **Nazwa użytkownika** i **Hasło**. Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.
   * Kliknij przycisk **Połącz**.
4. tooexplore, rozwiń węzeł serwera Azure SQL. Witaj baz danych skojarzonego z serwerem hello jest widoczny. Rozwiń węzeł AdventureWorksDW toosee hello tabele w przykładowej bazie danych.
   
    ![Poznawanie bazy danych AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2. Uruchamianie przykładowego zapytania
Teraz, gdy połączenie zostało nawiązane tooyour bazy danych, napiszemy zapytanie.

1. Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.
2. Wybierz pozycję **Nowe zapytanie**. Otworzy się okno nowego zapytania.
   
    ![Nowe zapytanie][4]
3. Skopiuj to zapytanie TSQL do okna zapytania hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Kwerenda hello. toodo tego, kliknij `Execute` lub hello Użyj następującego skrótu: `F5`.
   
    ![Uruchamianie zapytania][5]
5. Spójrz na powitania wyników zapytania. W tym przykładzie hello Tabela FactInternetSales ma 60398 wierszy.
   
    ![Wyniki zapytania][6]

## <a name="next-steps"></a>Następne kroki
Teraz, możesz łączyć i zapytania, spróbuj [wizualizacji danych hello z usługą Power BI][visualizing hello data with PowerBI].

tooconfigure środowiska pod kątem uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania tooSQL hurtowni danych][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
