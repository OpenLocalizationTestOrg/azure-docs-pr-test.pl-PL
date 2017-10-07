---
title: aaa "samouczek lekcji dodatkowych usług Azure Analysis Services: wiersze szczegółów | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate, a wyrażenie wiersze szczegółów w hello Samouczek usług Azure Analysis Services.
usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Lekcja uzupełniająca — wiersze szczegółów

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji uzupełniające służą hello toodefine edytora języka DAX wyrażenia niestandardowego wiersze szczegółów. Wyrażenie wiersze szczegółów jest właściwością w miarę, zapewniając użytkownikom końcowym więcej informacji na temat wyników hello agregować miary. 
  
Szacowany czas toocomplete tej lekcji: **10 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego. Przed wykonaniem zadania hello w tym uzupełniające lekcji, powinno mieć ukończone wszystkie poprzednie — lekcje lub zakończonych projektu modelu przykładowej firmy Adventure Works Internet sprzedaży.  
  
## <a name="what-do-we-need-toosolve"></a>Co zrobić, potrzebujemy toosolve?
Przyjrzyjmy się hello szczegóły naszych miary InternetTotalSales przed dodaniem wyrażenia do szczegółów wierszy.

1.  Programu SSDT, kliknij przycisk hello **modelu** menu > **analizy w programie Excel** tooopen programu Excel i Utwórz pustą tabelę przestawną.
  
2.  W **pól tabeli przestawnej**, Dodaj hello **InternetTotalSales** miarę Tabela FactInternetSales hello zbyt**wartości**, **CalendarYear**z hello DimDate tabeli zbyt**kolumn**, i **EnglishCountryRegionName** za**wierszy**. Nasze tabeli przestawnej teraz daje wyników zagregowany z miary InternetTotalSales hello regiony i roku. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. W tabeli przestawnej hello kliknij dwukrotnie wartość zagregowana roku i nazwę regionu. W tym miejscu możemy podwójnie hello wartość dla klientów w Australii i hello 2014 roku. Otwarty został nowy arkusz zawierający dane, które jednak nie są użyteczne.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Co mamy ma tutaj toosee to tabela zawierająca kolumn i wierszy współtworzenia toohello agregowana wynik naszych InternetTotalSales miary. toodo, że wyrażenie wiersze szczegółów można dodać jako właściwość hello miary.

## <a name="add-a-detail-rows-expression"></a>Dodawanie wyrażenia wierszy szczegółów

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate wyrażenie wiersze szczegółów 
  
1. Programu SSDT, w siatce miar Tabela FactInternetSales hello, kliknij przycisk hello **InternetTotalSales** miary. 

2. W **właściwości** > **wyrażenie wiersze szczegółów**, kliknij przycisk hello Edytor przycisk tooopen hello edytora języka DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. W edytorze języka DAX wprowadź powitania po wyrażeniu:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    To wyrażenie określa nazwy kolumny i miary z powiązanych tabel i tabela FactInternetSales hello są zwracane, gdy użytkownik kliknie dwukrotnie wyników zagregowany w tabeli przestawnej lub raportu.

4. W programie Excel Usuń arkusz hello utworzony w kroku 3, a następnie kliknij dwukrotnie wartość zagregowana. Tym razem z właściwością wyrażenie wiersze szczegółów zdefiniowane dla miary hello, nowy arkusz zostanie otwarty zawierający przydatne znacznie więcej danych.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Wykonaj ponowne wdrożenie modelu.

  
## <a name="see-also"></a>Zobacz też  
[Funkcja SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lekcja uzupełniająca — niewyrównane hierarchie](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
