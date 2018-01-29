---
title: "Połączyć się z magazynem danych Azure SQL - SSMS | Dokumentacja firmy Microsoft"
description: "Użyj programu SQL Server Management Studio (SSMS) do nawiązania połączenia i wykonywać zapytania usługi Azure SQL Data Warehouse."
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a>Nawiązać połączenia SQL Data Warehouse przy użyciu programu SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Użyj programu SQL Server Management Studio (SSMS) do nawiązania połączenia i wykonywać zapytania usługi Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Wymagania wstępne
Aby użyć tego samouczka, potrzebne są następujące elementy:

* Istniejący magazyn danych SQL. Aby go utworzyć, zobacz artykuł [Tworzenie bazy danych w usłudze SQL Data Warehouse][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) zainstalowany. [Zainstaluj narzędzia SSMS] [ Install SSMS] bezpłatnie, jeśli nie masz jeszcze go.
* W pełni kwalifikowana nazwa serwera SQL. Aby ją znaleźć, zobacz [Nawiązywanie połączenia z usługą SQL Data Warehouse][Connect to SQL Data Warehouse].

## <a name="1-connect-to-your-sql-data-warehouse"></a>1. Nawiązywanie połączenia z usługą SQL Data Warehouse
1. Otwórz program SSMS.
2. Otwórz Eksplorator obiektów. Aby to zrobić, wybierz **pliku** > **połączyć Eksplorator obiektów**.
   
    ![Eksplorator obiektów SQL Server][1]
3. Wypełnij pola w oknie łączenia z serwerem.
   
    ![Łączenie z serwerem][2]
   
   * **Nazwa serwera**. Wprowadź wcześniej ustaloną **nazwę serwera**.
   * **Uwierzytelnianie**. Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.
   * **Nazwa użytkownika** i **Hasło**. Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.
   * Kliknij przycisk **Połącz**.
4. W celach poznawczych rozwiń węzeł serwera Azure SQL. Możesz przejrzeć skojarzone z serwerem bazy danych. Rozwiń węzeł AdventureWorksDW, aby zobaczyć tabele w przykładowej bazie danych.
   
    ![Poznawanie bazy danych AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2. Uruchamianie przykładowego zapytania
Teraz, po nawiązaniu połączenia z bazą danych, napiszemy zapytanie.

1. Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.
2. Wybierz pozycję **Nowe zapytanie**. Otworzy się okno nowego zapytania.
   
    ![Nowe zapytanie][4]
3. Skopiuj to zapytanie TSQL do okna zapytania:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Uruchom zapytanie. Aby to zrobić, kliknij przycisk `Execute` lub użyj następującego skrótu: `F5`.
   
    ![Uruchamianie zapytania][5]
5. Przejrzyj wyniki zapytania. W tym przykładzie tabela FactInternetSales ma 60398 wierszy.
   
    ![Wyniki zapytania][6]

## <a name="next-steps"></a>Kolejne kroki
Teraz, kiedy umiesz nawiązywać połączenia i wykonywać zapytania, spróbuj wykonać [wizualizację danych przy użyciu usługi Power BI][visualizing the data with PowerBI].

Aby skonfigurować środowisko do uwierzytelniania usługi Azure Active Directory, zobacz artykuł [Uwierzytelnianie w usłudze SQL Data Warehouse][Authenticate to SQL Data Warehouse].

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
