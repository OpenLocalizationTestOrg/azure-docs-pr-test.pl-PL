---
title: "aaaAnalyze danych w usłudze Data Lake Store za pomocą usługi Power BI | Dokumentacja firmy Microsoft"
description: "Użyj usługi Power BI tooanalyze danych przechowywanych w usłudze Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Analizowanie danych w usłudze Data Lake Store za pomocą usługi Power BI
W tym artykule przedstawiono sposób tooanalyze Power BI Desktop toouse i wizualizację danych przechowywanych w usłudze Azure Data Lake Store.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md). W tym artykule przyjęto założenie, że utworzono już konto usługi Data Lake Store o nazwie **mybidatalakestore**i przekazać przykładowy plik danych (**Drivers.txt**) tooit. Ten przykładowy plik jest dostępny do pobrania z [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Możesz pobrać ten z [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Tworzenie raportu w programie Power BI Desktop
1. Uruchom Power BI Desktop na tym komputerze.
2. Z hello **Home** wstążki, kliknij przycisk **Pobierz dane**, a następnie kliknij przycisk więcej. W hello **Pobierz dane** okno dialogowe, kliknij przycisk **Azure**, kliknij przycisk **Azure Data Lake Store**, a następnie kliknij przycisk **Connect**.
   
    ![Połącz tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect tooData Lake — Magazyn")
3. Jeśli zostanie wyświetlone okno dialogowe o łączniku hello jest na etapie programowania, należy wybrać toocontinue.
4. W hello **Microsoft Azure Data Lake Store** okno dialogowe, podaj konto usługi Data Lake Store tooyour adres URL hello, a następnie kliknij przycisk **OK**.
   
    ![Adres URL dla usługi Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "adres URL dla usługi Data Lake Store")
5. W hello następnym oknie dialogowym kliknij **Zaloguj** toosign do konta usługi Data Lake Store. Będzie przekierowanie na stronę logowania Twojej organizacji tooyour. Wykonaj hello monity toosign pod uwagę hello.
   
    ![Zaloguj się do usługi Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Zaloguj się do usługi Data Lake Store")
6. Po pomyślnym zalogowaniu, kliknij przycisk **Connect**.
   
    ![Połącz tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect tooData Lake — Magazyn")
7. Hello dalej wyświetlane okno dialogowe pliku hello czy przesłany tooyour konta usługi Data Lake Store. Sprawdź informacje o hello, a następnie kliknij przycisk **obciążenia**.
   
    ![Ładowanie danych z usługi Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "ładowanie danych z usługi Data Lake Store")
8. Po hello danych został pomyślnie załadowany do usługi Power BI, zobaczysz hello kolejnych pól w hello **pola** kartę.
   
    ![Zaimportowane pola](./media/data-lake-store-power-bi/imported-fields.png "zaimportowane pola")
   
    Jednak toovisualize i analizować dane hello, firma Microsoft hello toobe danych jest dostępne na powitania kolejnych pól
   
    ![Żądany pola](./media/data-lake-store-power-bi/desired-fields.png "żądanego pola")
   
    W następnych krokach hello modyfikacjom hello zapytania tooconvert hello zaimportowane dane w wybranym formacie hello.
9. Z hello **Home** wstążki, kliknij przycisk **edytowanie zapytań**.
   
    ![Edytuj zapytania](./media/data-lake-store-power-bi/edit-queries.png "edytowanie zapytań")
10. W hello edytora zapytań, w obszarze hello **zawartości** kolumny, kliknij przycisk **binarne**.
    
    ![Edytuj zapytania](./media/data-lake-store-power-bi/convert-query1.png "edytowanie zapytań")
11. Zostanie wyświetlona ikona pliku, który reprezentuje hello **Drivers.txt** pliku, który został przekazany. Kliknij prawym przyciskiem myszy plik hello, a następnie kliknij przycisk **CSV**.    
    
    ![Edytuj zapytania](./media/data-lake-store-power-bi/convert-query2.png "edytowanie zapytań")
12. Dane wyjściowe powinny być widoczne, jak pokazano poniżej. Danych jest teraz dostępna w formacie służy toocreate wizualizacji.
    
    ![Edytuj zapytania](./media/data-lake-store-power-bi/convert-query3.png "edytowanie zapytań")
13. Z hello **Home** wstążki, kliknij przycisk **zamknąć i zastosować**, a następnie kliknij przycisk **zamknąć i zastosować**.
    
    ![Edytuj zapytania](./media/data-lake-store-power-bi/load-edited-query.png "edytowanie zapytań")
14. Po zapytania hello jest aktualizowany, hello **pola** kartę wyświetli hello nowe pola dostępne dla wizualizacji.
    
    ![Zaktualizowano pola](./media/data-lake-store-power-bi/updated-query-fields.png "zaktualizowane pól")
15. Daj nam tworzyć toorepresent wykresu kołowego hello sterowniki w każdemu miastu dla danego kraju. toodo, należy hello następujące opcje.
    
    1. Na karcie wizualizacje hello kliknij symbol hello wykresu kołowego.
       
        ![Utwórz wykres kołowy](./media/data-lake-store-power-bi/create-pie-chart.png "utworzyć wykres kołowy")
    2. kolumny Hello zamierzamy są toouse **4 kolumny** (Nazwa miejscowości hello) i **7 kolumn** (nazwa kraju hello). Przeciągnij te kolumny z **pola** karcie zbyt**wizualizacje** karcie, jak pokazano poniżej.
       
        ![Tworzenie wizualizacji](./media/data-lake-store-power-bi/create-visualizations.png "tworzenie wizualizacji")
    3. Wykres kołowy Hello powinien teraz wyglądać podobnie jak hello przedstawionego poniżej.
       
        ![Wykres kołowy](./media/data-lake-store-power-bi/pie-chart.png "tworzenie wizualizacji")
16. Wybierając określonego kraju z poziomu filtrów stron hello, będą teraz widoczne hello liczbę sterowników w każdemu miastu hello wybrane kraju. Na przykład w obszarze hello **wizualizacje** , w obszarze **strony poziomu filtry**, wybierz pozycję **Brazylia**.
    
    ![Wybierz kraj](./media/data-lake-store-power-bi/select-country.png "wybierz kraj")
17. Wykres kołowy Hello jest automatycznie aktualizowane toodisplay sterowniki hello hello miast Brazylia.
    
    ![Sterowniki w danym kraju](./media/data-lake-store-power-bi/driver-per-country.png "sterowników dla każdego kraju")
18. Z hello **pliku** menu, kliknij przycisk **zapisać** wizualizacji hello toosave jako plik Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Publikowanie usługi BI tooPower raportu
Wizualizacje hello utworzone w programie Power BI Desktop możesz go udostępnić innym publikując toohello usługi Power BI. Aby uzyskać instrukcje dotyczące toodo, który zobacz [publikowania z Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Zobacz też
* [Analizowanie danych w usłudze Data Lake Store za pomocą usługi Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

