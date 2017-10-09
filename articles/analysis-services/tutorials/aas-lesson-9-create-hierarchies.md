---
title: aaa "lekcji samouczka usług Azure Analysis Services 9: tworzenie hierarchii | Opis Microsoft Docs": usługi: documentationcenter usług analysis services:" Autor: minewiskan Menedżera: Edytor erikre: "tagów:"

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>Lekcja 9. Tworzenie hierarchii

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz hierarchie. Hierarchie to grupy kolumn uporządkowane według poziomów. Na przykład hierarchia Geografia może zawierać poziomy podrzędne Kraj, Województwo, Powiat i Miasto. Hierarchie można pojawiają się niezależnie od innych kolumn w raportowania listy pól aplikacji klienta, dzięki czemu łatwiej klienta toonavigate użytkowników i zawarte w raporcie. toolearn więcej, zobacz [hierarchii](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
hierarchie toocreate za pomocą projektanta modelu hello w *widoku diagramu*. Tworzenie hierarchii i zarządzanie nimi nie jest obsługiwane w widoku danych.  
  
Szacowany czas toocomplete tej lekcji: **20 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 8: Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Tworzenie hierarchii  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>Hierarchia kategorii w tabeli DimProduct hello toocreate  
  
1.  W Projektancie modeli hello (widoku diagramu), kliknij prawym przyciskiem myszy hello **DimProduct** tabeli > **tworzenie hierarchii**. Nowej hierarchii pojawi się u dołu okna tabeli hello hello. Zmień nazwę hierarchii hello **kategorii**.  
  
2.  Kliknij i przeciągnij hello **ProductCategoryName** toohello kolumny nowy **kategorii** hierarchii.  
  
3.  W hello **kategorii** hierarchii, kliknij prawym przyciskiem myszy hello **ProductCategoryName** > **zmienić**, a następnie wpisz **kategorii**.  
  
    > [!NOTE]  
    > Zmiana nazwy kolumny w hierarchii nie powoduje zmiany nazwy tej kolumny w tabeli hello. Kolumna w hierarchii jest po prostu reprezentację hello kolumny w tabeli hello.  
  
4.  Kliknij i przeciągnij hello **ProductSubcategoryName** toohello kolumny **kategorii** hierarchii. Zmień jej nazwę na **Subcategory** (Podkategoria). 
  
5.  Powitania kliknij prawym przyciskiem myszy **ModelName** kolumny > **dodać toohierarchy**, a następnie wybierz **kategorii**. Zmień jej nazwę na **Model**.

6.  Na koniec należy dodać **EnglishProductName** toohello hierarchia kategorii. Zmień jej nazwę na **Product** (Produkt).  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>hierarchie toocreate hello DimDate tabeli  
  
1.  W hello **DimDate** tabeli, należy utworzyć hierarchię o nazwie **kalendarza**.  
  
3.  Dodaj hello następujących kolumn w kolejności:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  W hello **DimDate** tabeli, należy utworzyć **obrachunkowym** hierarchii. Dołącz hello następujących kolumn w kolejności:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Ponadto w hello **DimDate** tabeli, należy utworzyć **ProductionCalendar** hierarchii. Dołącz hello następujących kolumn w kolejności:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Co dalej?
[Lekcja 10. Tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
