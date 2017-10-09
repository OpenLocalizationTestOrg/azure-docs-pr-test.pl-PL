---
title: aaa "Azure Analysis Services lekcji samouczek 2: pobieranie danych | Opis elementu Microsoft Docs": w tym artykule opisano, jak tooget, a następnie zaimportuj dane w hello projekt samouczka usług Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend
---

# <a name="lesson-2-get-data"></a>Lekcja 2. Pobieranie danych

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji Pobierz dane programu SSDT tooconnect toohello AdventureWorksDW2014 — przykładowa baza danych, wybierz dane, w wersji zapoznawczej i filtr, a następnie zaimportować do modelu obszaru roboczego.  
  
Funkcja pobierania danych umożliwia importowanie danych z wielu różnych źródeł, takich jak: baza danych SQL Azure, Oracle, Sybase, kanał informacyjny OData, Teradata, pliki itp. Można również wykonywać kwerendy danych przy użyciu wyrażeń formuły Power Query M.
  
Szacowany czas toocomplete tej lekcji: **10 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [Lekcja 1: Tworzenie nowego projektu modelu tabelarycznego](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Tworzenie połączenia  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate toohello AdventureWorksDW2014 połączenia bazy danych  
  
1.  W Eksploratorze modeli tabelarycznych kliknij prawym przyciskiem myszy pozycje **Źródła danych** > **Importuj ze źródła danych**.  
  
    Spowoduje to uruchomienie pobieranie danych, który prowadzi użytkownika przez źródło danych tooa nawiązującego połączenie. Jeśli nie widzisz Eksplorator modelu tabelarycznego, w **Eksploratora rozwiązań**, kliknij dwukrotnie **Model.bim** tooopen hello modelu w Projektancie hello. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  W oknie Pobierz dane kliknij kolejno opcje **Baza danych** > **Baza danych SQL Server** > **Połącz**.  
  
3.  W hello **bazy danych programu SQL Server** okna dialogowego, w **serwera**, wpisz nazwę powitania serwera hello zainstalowaną hello AdventureWorksDW2014 bazy danych, a następnie kliknij przycisk **Connect**.  

4.  Po wyświetleniu monitu poświadczeń tooenter należy toospecify hello poświadczenia usług Analysis Services używa tooconnect toohello źródła danych podczas importowania i przetwarzania danych. W obszarze **Tryb personifikacji** wybierz pozycję **Personifikuj konto**, a następnie wprowadź poświadczenia i kliknij przycisk **Połącz**. Zaleca się, że używasz konta, gdzie hello hasło nie traci ważności.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Przy użyciu konta użytkownika systemu Windows i hasło zawiera hello najbezpieczniejszą metodą źródła danych tooa nawiązującego połączenie.
  
5.  W Nawigatorze, wybierz hello **AdventureWorksDW2014** bazy danych, a następnie kliknij przycisk **OK**. Spowoduje to utworzenie hello połączenia toohello w bazie danych. 
  
6.  W Nawigatorze, wybierz hello pola wyboru dla hello następujących tabel: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, i **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Kliknięcie przycisku OK spowoduje otwarcie edytora zapytań. W następnej sekcji hello można wybrać tylko hello dane, które mają tooimport.

  
## <a name="filter-hello-table-data"></a>Filtrowanie danych tabeli hello  
Tabele w bazie danych przykładowych AdventureWorksDW2014 hello istnieją dane, które nie jest konieczne tooinclude w modelu. Jeśli to możliwe, ma toofilter limit miejsca w pamięci toosave zbędne dane używane przez hello modelu. Możesz filtrować hello kolumn z tabel, nie zaimportowaniu do bazy danych obszaru roboczego hello hello modelu bazy danych lub po jej wdrożeniu. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>dane tabeli hello toofilter przed zaimportowaniem  
  
1.  W edytorze zapytań wybierz hello **DimCustomer** tabeli. Zostanie wyświetlony widok tabeli DimCustomer hello na powitania źródła danych (AdventureWorksDWQ2014 przykładowej bazy danych). 
  
2.  Korzystając z funkcji wyboru wielokrotnego (Ctrl + kliknięcie), wybierz pozycje **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, kliknij je prawym przyciskiem myszy, a następnie kliknij pozycję **Usuń kolumny**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Ponieważ hello wartości dla tych kolumn nie są istotne tooInternet analizy sprzedaży, nie jest brak konieczności tooimport tych kolumn. Dzięki wyeliminowaniu zbędnych kolumn model jest mniejszy i wydajniejszy.  
  
4.  Filtruj hello pozostałych tabel przez usunięcie hello następujących kolumn w każdej tabeli:  
    
    **DimDate**
    
      |Kolumna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Kolumna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Kolumna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Kolumna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Kolumna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Kolumna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importuj hello wybrane tabele i kolumny danych  
Teraz, po podglądu i odfiltrowane zbędne dane, można zaimportować hello reszty hello danych, które mają. Kreator Hello importuje hello tabeli danych oraz relacje między tabelami. Nowe tabele i kolumny są tworzone w modelu hello i dane, które można odfiltrować nie został zaimportowany.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>tooimport hello wybrane tabele i kolumny danych  
  
1.  Przejrzyj wybrane pozycje. Jeśli wszystko wygląda poprawnie, kliknij przycisk **Importuj**. Witaj przetwarzania danych w oknie dialogowym Wyświetla stan hello importowanych z Twojego źródła danych do bazy danych obszaru roboczego danych.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Kliknij przycisk **Zamknij**.  

  
## <a name="save-your-model-project"></a>Zapisanie projektu modelu  
Koniecznie toofrequently zapisać projekt z modelem.  
  
#### <a name="toosave-hello-model-project"></a>Projekt z modelem hello toosave  
  
-   Kliknij kolejno opcje **Plik** > **Zapisz wszystko**.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 3. Oznaczanie jako tabeli dat](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
