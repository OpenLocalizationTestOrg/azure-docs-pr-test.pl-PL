---
title: Magazyn danych Azure tooyour danych aaaUse Redgate tooload | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Redgate danych platformy Studio scenariuszach dotyczących magazynów danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Ładowanie danych za pomocą usługi Data Platform Studio firmy Redgate
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

W tym samouczku przedstawiono sposób toouse [Studio platforma danych firmy Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (punktu dystrybucji) toomove danych z lokalnego programu SQL Server tooAzure SQL Data Warehouse. Studio platformy danych stosuje poprawki zgodności najbardziej odpowiednia hello i optymalizacje, co powoduje hello najkrótszej tooget sposób pracy z usługą Magazyn danych SQL.

> [!NOTE]
> Firma [Redgate](http://www.red-gate.com) to wieloletni partner firmy Microsoft, który dostarcza różne narzędzia programu SQL Server. Ta funkcja w usłudze Data Platform Studio została udostępniona bezpłatnie do użytku komercyjnego i niekomercyjnego.
> 
> 

## <a name="before-you-begin"></a>Przed rozpoczęciem
### <a name="create-or-identify-resources"></a>Tworzenie lub identyfikowanie zasobów
Przed rozpoczęciem tego samouczka należy toohave:

* **lokalnej bazy danych SQL Server**: hello dane, które mają tooSQL tooimport magazyn danych wymaga toocome z lokalnego programu SQL Server (w wersji 2008 R2 lub nowszy). Usługa Data Platform Studio nie może bezpośrednio importować danych z usługi Azure SQL Database ani z plików tekstowych.
* **Konto usługi Azure Storage**: Studio platformy danych przygotuje hello danych w magazynie obiektów Blob Azure przed załadowaniem go do usługi SQL Data Warehouse. konta magazynu Hello muszą używać modelu wdrażania hello "Resource Manager" (wartość domyślna hello) zamiast modelu wdrażania "Klasycznym" hello. Dowiedz się, jeśli nie masz konta magazynu, jak tooCreate konta magazynu. 
* **Usługa SQL Data Warehouse**: w tym samouczku przenosi hello dane z lokalnymi tooSQL programu SQL Server magazynu danych, więc należy toohave magazynu danych w trybie online. Jeśli nie masz już magazyn danych, Dowiedz się jak tooCreate magazyn danych SQL Azure.

> [!NOTE]
> Lepsza wydajność, jeśli konto magazynu hello i magazynu danych hello są tworzone w hello sam region.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Krok 1: Zaloguj się tooData Studio platformy z Twoim kontem platformy Azure
Otwórz przeglądarkę sieci web i przejdź toohello [Studio platformy danych](https://www.dataplatformstudio.com/) witryny sieci Web. Logowania z hello tego samego konta Azure tego możesz używane toocreate hello magazynu konta i magazynu danych. Jeśli adres e-mail jest skojarzony z służbowy lub konto służbowe i konto Microsoft, należy się toochoose hello konta, które ma dostęp do zasobów tooyour.

> [!NOTE]
> Jeśli jest to pierwsza przy użyciu danych Studio platformy, są zadawane toomanage uprawnienia aplikacji hello toogrant zasobów platformy Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Krok 2: Uruchom Kreatora importu hello
Z hello ekranu głównego punktu dystrybucji wybierz hello importu tooAzure SQL Data Warehouse łącze toostart hello importu Kreator.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Krok 3: Instalowanie hello bramy Studio platformy danych
tooconnect tooyour lokalną bazą danych programu SQL Server, należy tooinstall hello bramy punktu dystrybucji. Brama Hello jest agenta klienta, który zapewnia dostęp tooyour w lokalnym środowisku, wyodrębnia dane hello i przekazanie jej tooyour konta magazynu. Dane nigdy nie przechodzą przez serwery firmy Redgate. Witaj tooinstall bramy:

1. Kliknij przycisk hello **Tworzenie bramy** łącza
2. Pobierz i zainstaluj hello bramę, używając hello podana Instalatora

![][2]

> [!NOTE]
> Witaj bramy można zainstalować na dowolnym komputerze z bazy danych SQL Server źródła toohello dostępu do sieci. Uzyskuje dostęp do bazy danych programu SQL Server hello przy użyciu uwierzytelniania systemu Windows przy użyciu poświadczeń hello hello bieżącego użytkownika.
> 
> 

Po zakończeniu instalacji hello tooConnected zmiany stanu bramy i wybraniu dalej.

## <a name="step-4-identify-hello-source-database"></a>Krok 4: Zidentyfikować hello źródłowej bazy danych
W hello *wprowadź nazwę serwera* pole tekstowe, wprowadź nazwę hello powitania serwera, który jest hostem bazy danych i wybierz **dalej**. Następnie z menu rozwijanego hello, wybierz tooimport danych z bazy danych hello.

![][3]

Punktu dystrybucji sprawdza hello wybranej bazy danych dla tooimport tabel. Domyślnie punktu dystrybucji importuje wszystkie tabele hello hello bazy danych. Można wybrać, lub Anuluj wybór tabel, rozwijając powitalne link wszystkie tabele. Wybierz hello dalej przycisk toomove do przodu.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Krok 5: Wybierz konto magazynu toostage hello danych
Punktu dystrybucji wyświetla monit o podanie danych hello toostage lokalizacji. Wybierz istniejące konto magazynu z subskrypcji, a następnie wybierz przycisk **Next** (Dalej).

> [!NOTE]
> Punktu dystrybucji utworzy nowy kontener obiektów blob w hello wybranego konta magazynu i użyć różnych folderu dla każdej operacji importowania.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Krok 6. Wybieranie magazynu danych
Następnie należy wybrać online [magazyn danych SQL Azure](http://aka.ms/sqldw) bazy danych hello tooimport do. Po wybraniu bazy danych należy tooenter hello poświadczenia tooconnect toohello bazy danych, a następnie wybierz **dalej**.

![][5]

> [!NOTE]
> Punktu dystrybucji scala tabel danych źródłowych hello hello hurtowni danych. Punktu dystrybucji wyświetlane jest ostrzeżenie, jeśli nazwa tabeli hello wymaga toooverwrite istniejące tabele w magazynie danych hello. Można opcjonalnie usunąć istniejących obiektów w magazynie danych hello wg Usuń wszystkie istniejące obiekty przed rozpoczęciem importowania.
> 
> 

## <a name="step-7-import-hello-data"></a>Krok 7: Importowanie danych hello
Punktu dystrybucji potwierdza chcieliby tooimport hello danych. Po prostu kliknij importu danych hello toobegin przycisk hello rozpoczęcia importowania.

![][6]

Punktu dystrybucji Wyświetla wizualizację pokazujący postęp hello wyodrębnianie i przekazywanie danych hello z hello postępu programu SQL Server i hello lokalne powitania importu do usługi SQL Data Warehouse.

![][7]

Po zakończeniu importowania hello punktu dystrybucji Wyświetla podsumowanie importu danych hello i raport o zmianach hello zgodności poprawek, które mogły zostać wykonane.

![][8]

## <a name="next-steps"></a>Następne kroki
tooexplore danych w usłudze SQL Data Warehouse, Rozpocznij od wyświetlenia:

* [Tworzenie zapytań względem usługi Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Wizualizacja danych przy użyciu usługi Power BI][Visualize data with Power BI]

więcej informacji na temat Studio platforma danych firmy Redgate toolearn:

* [Odwiedź stronę główną punktu dystrybucji hello](http://www.dataplatformstudio.com/)
* [Obejrzyj pokaz usługi DPS w witrynie Channel9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Omówienie inne sposoby toomigrate i ładowania danych w usłudze SQL Data Warehouse zobacz:

* [Migrowanie tooSQL Twojego rozwiązania magazynu danych][Migrate your solution tooSQL Data Warehouse]
* [Ładowanie danych do usługi Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md)

Aby uzyskać więcej porad programistycznych, zobacz hello [omówienie programowania w usłudze SQL Data Warehouse](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
