---
title: "aaaConnect tooAzure SQL Data Warehouse — VSTS | Dokumentacja firmy Microsoft"
description: "Tworzenie zapytań względem usługi SQL Data Warehouse przy użyciu programu Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Połączenie tooSQL magazynu danych z programu Visual Studio i narzędzi SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Użyj programu Visual Studio tooquery Azure SQL Data Warehouse w zaledwie kilka minut. Ta metoda używa hello rozszerzenia SQL Server Data Tools (SSDT) w programie Visual Studio. 

## <a name="prerequisites"></a>Wymagania wstępne
toouse tego samouczka należy:

* Istniejący magazyn danych SQL. Zobacz toocreate, [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].
* Rozszerzenie SSDT dla programu Visual Studio. Jeśli masz program Visual Studio, prawdopodobnie masz też to rozszerzenie. Aby uzyskać instrukcje instalacji i informacje na temat dostępnych opcji, zobacz artykuł [Instalowanie programu Visual Studio i narzędzi SSDT][Installing Visual Studio and SSDT].
* Witaj w pełni kwalifikowana nazwa serwera SQL. toofind tego, zobacz [połączyć tooSQL hurtowni danych][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Połącz tooyour SQL Data Warehouse
1. Otwórz program Visual Studio 2013 lub 2015.
2. Otwórz Eksplorator obiektów SQL Server. toodo ten, wybierz **widoku** > **Eksplorator obiektów SQL Server**.
   
    ![Eksplorator obiektów SQL Server][1]
3. Kliknij przycisk hello **dodawania serwera SQL** ikony.
   
    ![Dodawanie serwera SQL][2]
4. Wypełnij pola hello hello Connect tooServer okna.
   
    ![Połącz tooServer][3]
   
   * **Nazwa serwera**. Wprowadź hello **nazwy serwera** wcześniej ustaloną.
   * **Uwierzytelnianie**. Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.
   * **Nazwa użytkownika** i **Hasło**. Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.
   * Kliknij przycisk **Połącz**.
5. tooexplore, rozwiń węzeł serwera Azure SQL. Witaj baz danych skojarzonego z serwerem hello jest widoczny. Rozwiń węzeł AdventureWorksDW toosee hello tabele w przykładowej bazie danych.
   
    ![Poznawanie bazy danych AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Uruchamianie przykładowego zapytania
Teraz, gdy połączenie zostało nawiązane tooyour bazy danych, napiszemy zapytanie.

1. Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.
2. Wybierz pozycję **Nowe zapytanie**. Otworzy się okno nowego zapytania.
   
    ![Nowe zapytanie][5]
3. Skopiuj to zapytanie TSQL do okna zapytania hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Kwerenda hello. toodo, hello zieloną strzałkę lub użyj następującego skrótu hello: `CTRL` + `SHIFT` + `E`.
   
    ![Uruchamianie zapytania][6]
5. Spójrz na powitania wyników zapytania. W tym przykładzie hello Tabela FactInternetSales ma 60398 wierszy.
   
    ![Wyniki zapytania][7]

## <a name="next-steps"></a>Następne kroki
Teraz, możesz łączyć i zapytania, spróbuj [wizualizacji danych hello z usługą Power BI][visualizing hello data with PowerBI].

tooconfigure środowiska pod kątem uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania tooSQL hurtowni danych][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
