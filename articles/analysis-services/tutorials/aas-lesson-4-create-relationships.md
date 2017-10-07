---
title: aaa "lekcji samouczka usług Azure Analysis Services 4: tworzenie relacji | Opis elementu Microsoft Docs": w tym artykule opisano, jak relacje toocreate w hello projekt samouczka usług Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>Lekcja 4. Tworzenie relacji

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji Sprawdź hello relacje, które zostały automatycznie utworzone po zaimportowaniu danych i dodać nowe relacje między tabelami w różnych. Relacja to połączenie między dwiema tabelami, które określa, jak powinna zostać skorelowane hello danych w tych tabelach. Na przykład tabela DimProduct hello i tabela DimProductSubcategory hello relacją oparte na hello fakt, że każdy z produktów należy podkategorii tooa. toolearn więcej, zobacz [relacje](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Szacowany czas toocomplete tej lekcji: **10 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 3: Oznacz jako tabelę dat](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Przegląd istniejących relacji i dodawanie nowych  
Podczas importowania danych za pomocą Pobierz dane uzyskano siedmiu tabel z bazy danych AdventureWorksDW2014 hello. Ogólnie rzecz biorąc gdy użytkownik importuje dane ze źródła relacyjne istniejące relacje są automatycznie importowane oraz hello dane. Jednak przed przystąpieniem do tworzenia modelu należy sprawdzić, czy relacje między tabelami zostały utworzone prawidłowo. W tym samouczku zostaną dodane trzy nowe relacje.  
  
#### <a name="tooreview-existing-relationships"></a>istniejące relacje tooreview  
  
1.  Kliknij przycisk hello **modelu** menu > **widok modelu** > **widoku diagramu**.  

    Witaj Projektant modelu jest teraz wyświetlany w widoku diagramu, postaci graficznej wyświetlanie wszystkich tabel hello zaimportowane linie między nimi. Witaj linie między tabelami wskazują hello relacje, które zostały automatycznie utworzone po zaimportowaniu danych hello.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Dołączyć jako wiele tabel hello możliwie za pomocą formantów minimapa w prawym dolnym narożniku hello hello Projektant modelu. Można również kliknij i przeciągnij lokalizacje toodifferent tabel, łącząc bliżej tabel lub umieszczania ich w określonej kolejności. Przenoszenie tabel nie ma wpływu na relacje hello już między tabelami hello. tooview wszystkie kolumny hello w określonej tabeli, kliknij i przeciągnij na tooexpand krawędzi tabeli lub zmniejszyć jego rozmiar.  
  
2.  Kliknij przycisk Linia ciągła hello między hello **DimCustomer** tabeli i hello **DimGeography** tabeli. Linia ciągła Hello między tymi dwiema tabelami pokazuje ta relacja jest aktywna, oznacza to, że jest używany domyślnie podczas obliczania formuły języka DAX.  
  
    Powiadomienie hello **GeographyKey** kolumny w hello **DimCustomer** tabeli i hello **GeographyKey** kolumny w hello **DimGeography** tabeli teraz każdy znajdować się w polu. Te kolumny są używane w hello relacji. Witaj we właściwościach relacji również pojawiają się teraz hello **właściwości** okna.  
  
    > [!TIP]  
    > Ponadto toousing hello Projektant modelu w widoku diagramu, można również użyć hello zarządzanie relacjami okna dialogowego pole tooshow hello relacje między wszystkie tabele w formacie tabeli. W Eksploratorze modeli tabelarycznych kliknij prawym przyciskiem myszy pozycje **Relacje** > **Zarządzanie relacjami**.
  
3.  Sprawdź następujące relacje hello zostały utworzone podczas każdej z tabel hello zostały zaimportowane z bazy danych AdventureWorksDW hello:  
  
    |Aktywne|Tabela|Pokrewna tabela odnośników|  
    |----------|---------|------------------------|  
    |Tak|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Tak|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Tak|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Tak|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Tak|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Jeśli którekolwiek z relacji hello brakuje, sprawdź, czy model zawiera następujące tabele hello: DimCustomer, DimDate DimGeography, DimProduct, DimProductCategory, DimProductSubcategory i FactInternetSales. Jeśli tabel z tego samego połączenia źródła danych zostaną zaimportowane na powitania rozdzielić razy, wszystkie relacje między tabelami te nie są tworzone i muszą być utworzone ręcznie.  

### <a name="take-a-closer-look"></a>Przyjrzyjmy się temu bliżej
W widoku diagramu Zwróć uwagę, Strzałka gwiazdkę i numer w wierszach hello, które zawierają hello relacji między tabelami.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

Strzałka Hello pokazuje hello kierunek filtru. gwiazdki Hello pokazano, że ta tabela jest hello wiele relacji hello kardynalności i hello jedną pokazuje ta tabela jest hello na jednej stronie relacji hello. Jeśli potrzebujesz tooedit relacji; na przykład zmienić kierunek filtru relacji hello lub Kardynalność, kliknij dwukrotnie hello relacji wiersza tooopen hello Edytuj relację z okna dialogowego.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Te funkcje są przeznaczone dla zaawansowanych modelowania danych i są poza zakresem hello tego samouczka. toolearn więcej, zobacz [dwukierunkowego krzyżowego filtry dla modeli tabelarycznych w usługach Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

W niektórych przypadkach może być konieczne toocreate dodatkowe relacje między tabelami w Twojej toosupport modelu niektórych logiki biznesowej. W tym samouczku należy toocreate trzy dodatkowe relacje między tabelami FactInternetSales hello i DimDate hello.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd nowe relacje między tabelami  
  
1.  W Konstruktorze modelu hello w hello **FactInternetSales** tabeli, kliknij i przytrzymaj hello **OrderDate** kolumny, a następnie przeciągnij hello kursora toohello **data** kolumny w hello  **DimDate** tabeli, a następnie zwolnij.  

    Linia ciągła wyświetleniu utworzono aktywna relacja między hello **OrderDate** kolumny w hello **sprzedaży Internet** tabeli i hello **data** kolumny w hello **Data** tabeli. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Podczas tworzenia relacji, hello kardynalność i Filtruj kierunku między hello tabeli podstawowej i tabeli odnośników pokrewne hello jest automatycznie wybierany.  
  
2.  W hello **FactInternetSales** tabeli, kliknij i przytrzymaj hello **Data ukończenia** kolumny, a następnie przeciągnij hello kursora toohello **data** kolumny w hello **DimDate** tabeli, a następnie zwolnij.  
  
    Linia kropkowana wyświetleniu utworzono nieaktywne relacji między hello **Data ukończenia** kolumny w hello **FactInternetSales** tabeli i hello **data** kolumny Witaj **DimDate** tabeli. Między tabelami może istnieć wiele relacji, ale tylko jedna z nich może być aktywna w danym momencie. Nieaktywne relacje można podjąć aktywne tooperform specjalne agregacji w niestandardowych wyrażenia języka DAX.  
  
3.  Na koniec utwórz jeszcze jedną relację. W hello **FactInternetSales** tabeli, kliknij i przytrzymaj hello **DataWysyłki** kolumny, a następnie przeciągnij hello kursora toohello **data** kolumny w hello **DimDate** tabeli, a następnie zwolnij.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 5. Tworzenie kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
