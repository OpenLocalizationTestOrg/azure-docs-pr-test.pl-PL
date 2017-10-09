---
title: "aaaVisualize danych magazynu danych SQL za pomocą Power BI | Microsoft Azure"
description: "Wizualizacja danych usługi SQL Data Warehouse przy użyciu usługi Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Wizualizacja danych przy użyciu usługi Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

W tym samouczku przedstawiono sposób toouse usługi Power BI tooconnect tooSQL magazynu danych oraz tworzenia podstawowych wizualizacji.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toostep opisanych w tym samouczku, potrzebne są:

* Magazyn danych SQL są wstępnie załadowane z bazą danych AdventureWorksDW hello. tooprovision tego, zobacz [Tworzenie usługi SQL Data Warehouse] [ Create a SQL Data Warehouse] i wybierz polecenie tooload hello przykładowych danych. Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Połącz tooyour bazy danych
tooopen usługi Power BI i Połącz z bazą danych AdventureWorksDW tooyour:

1. Zaloguj się na powitania [portalu Azure][Azure portal].
2. Kliknij pozycję **Bazy danych SQL** i wybierz bazę danych AdventureWorks usługi SQL Data Warehouse.
   
    ![Znajdowanie bazy danych][1]
3. Kliknij przycisk "Otwórz w usłudze Power BI" hello.
   
    ![Przycisk usługi Power BI][2]
4. Powinna zostać wyświetlona strona połączenia SQL Data Warehouse hello wyświetlanie adres sieci web bazy danych. Kliknij przycisk Dalej.
   
    ![Połączenie z usługą Power BI][3]
5. Wprowadź nazwę użytkownika serwera Azure SQL i hasło i będzie bazy danych magazynu danych SQL tooyour pełni połączonych.
   
    ![Logowanie w usłudze Power BI][4]
6. Po zalogowaniu się do usługi Power BI, kliknij przycisk hello zestaw danych AdventureWorksDW w lewym bloku hello. Spowoduje to otwarcie hello bazy danych.
   
    ![Otwieranie bazy danych AdventureWorksDW w usłudze Power BI][5]

## <a name="2-create-a-report"></a>2. Tworzenie raportu
Użytkownik jest teraz gotowy toouse usługi Power BI tooanalyze przykładowe dane AdventureWorksDW. Analiza hello tooperform, AdventureWorksDW ma widok o nazwie widoku AggregateSales. Ten widok zawiera kilka hello kluczowych metryk do analizowania sprzedaży firmy hello hello.

1. toocreate mapę kwot sprzedaży, zgodnie z toopostal kodu, w okienku pól po prawej stronie powitania kliknij hello widoku AggregateSales widoku tooexpand go. Kliknij przycisk hello KodPocztowy i kwoty sprzedaży tooselect kolumn je.
   
    ![Wybór widoku AggregateSales w usłudze Power BI][6]
   
    Usługa Power BI automatycznie rozpoznaje dane geograficzne i umieszcza je na mapie.
   
    ![Mapa w usłudze Power BI][7]
2. W tym kroku zostanie utworzony wykres słupkowy przedstawiający kwotę sprzedaży w odniesieniu do dochodu klienta. toocreate to przejdź toohello widoku AggregateSales widok rozszerzony. Kliknij pole kwoty sprzedaży hello. Przeciągnij hello dochód klienta pola toohello lewo i upuść ją na osi.
   
    ![Wybór osi w usłudze Power BI][8]
   
    Przenieśliśmy wykres słupkowy hello na lewą hello.
   
    ![Wykres słupkowy w usłudze Power BI][9]
3. W tym kroku utworzymy wykres liniowy, który przedstawia kwoty sprzedaży według dat zamówienia. toocreate to przejdź toohello widoku AggregateSales widok rozszerzony. Kliknij pola SalesAmount (Kwota sprzedaży) i OrderDate (Data zamówienia). W kolumnie wizualizacje powitania kliknij ikonę wykres liniowy hello; jest to pierwsza ikona hello w hello drugim wierszu w obszarze wizualizacji.
   
    ![Wybór wykresu liniowego w usłudze Power BI][10]
   
    Masz teraz raport wyświetlający trzy różne wizualizacje danych hello.
   
    ![Wykres liniowy w usłudze Power BI][11]

W dowolnym momencie możesz kliknąć menu **Plik** i wybrać polecenie **Zapisz**, aby zapisać postęp.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy firma Microsoft została podana możesz niektórych toowarm czasu hello przykładowych danych, zobacz temat jak zbyt[opracowanie][develop], [załadować][load], lub [ Migrowanie][migrate]. Lub Spójrz na powitania [witryny sieci Web usługi Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
