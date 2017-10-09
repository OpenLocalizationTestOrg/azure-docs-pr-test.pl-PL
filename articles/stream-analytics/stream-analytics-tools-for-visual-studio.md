---
title: aaaUse Azure Stream Analytics Tools for Visual Studio | Dokumentacja firmy Microsoft
description: "Pierwsze kroki samouczka dotyczącego hello Azure Stream Analytics Tools for Visual Studio"
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Użyj narzędzia Azure Stream Analytics Tools dla programu Visual Studio
## <a name="introduction"></a>Wprowadzenie
Z tego samouczka dowiesz się, jak toouse Azure Stream Analytics Tools for toocreate programu Visual Studio tworzenie, testowanie lokalnie, zarządzanie i debugowania z zadania usługi analiza strumienia. 

Po ukończeniu tego samouczka, będą mieć możliwość:
* Zapoznaj się z narzędzia do analizy strumienia dla programu Visual Studio.
* Konfigurowanie i wdrażanie zadanie usługi Stream Analytics.
* Przetestuj zadania lokalnie z lokalnym przykładowych danych.
* Użycie, monitorowanie tootroubleshoot problemów.
* Wyeksportuj istniejących tooprojects zadania.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące wymagania wstępne:
* Zakończ hello kroki, które należy poprzedzić "Utwórz zadanie usługi analiza strumienia" w hello [tworzenia rozwiązania IoT przy użyciu usługi Stream Analytics samouczek](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Użyj programu Visual Studio 2015, Visual Studio 2013 update 4 lub Visual Studio 2012. Enterprise (Ultimate/Premium), Professional i społeczności wersje są obsługiwane. Express edition nie jest obsługiwane. Visual Studio 2017 nie jest obsługiwane. 
* Użyj hello zestawu Azure SDK dla platformy .NET w wersji 2.7.1 lub nowszej. Zainstalować go za pomocą hello [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Zainstaluj hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Tworzenie projektu usługi analiza strumienia
1. W programie Visual Studio, kliknij przycisk hello **pliku** menu i wybierz **nowy projekt**. 

2. Z listy szablonów hello powitania po lewej stronie wybierz **Stream Analytics** , a następnie kliknij przycisk **Azure Stream Analytics aplikacji**.

3. Wprowadź projektu hello **nazwa**, **lokalizacji**, i **Nazwa rozwiązania** podobnie jak w przypadku innych projektów.

    ![Nowe okno projektu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    A **przez** projektu jest generowany w **Eksploratora rozwiązań**.

    ![Numer projektu generowane w Eksploratorze rozwiązań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Wybierz poprawną subskrypcję hello
1. W programie Visual Studio, kliknij przycisk hello **widoku** i otwórz menu **Eksploratora serwera**.

2. Zaloguj się przy użyciu konta platformy Azure. 

## <a name="define-hello-input-sources"></a>Definiowanie źródeł dla wejścia hello
1.  W **Eksploratora rozwiązań**, rozwiń węzeł hello **dane wejściowe** węzła i Zmień nazwę **Input.json** za**EntryStream.json**. Kliknij dwukrotnie **EntryStream.json**.
2.  Witaj **Alias wejściowy** jest teraz **EntryStream**. alias wejściowy Hello jest używany w skrypcie zapytania hello. 
3.  W **typ źródła**, wybierz pozycję **strumienia danych**.
4.  W **źródła**, wybierz pozycję **Centrum zdarzeń**.
5.  W **Namespace magistrali usługi**, wybierz pozycję hello **TollData** opcji.
6.  W **nazwy Centrum zdarzeń**, wybierz pozycję **wpis**.
7.  W **nazwy zasad Centrum zdarzeń**, wybierz pozycję **RootManageSharedAccessKey** (hello wartość domyślna).
8.  W **Format serializacji zdarzeń**, wybierz pozycję **Json**. 
9.  W **kodowanie**, wybierz pozycję **UTF8**. Ustawienia powinna wyglądać powitania po zrzut ekranu:

    ![Okna wejściowego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. toofinish hello kreatora, kliknij przycisk **zapisać**. Teraz można dodać innego źródła danych wejściowych toocreate hello zakończenia strumienia. Kliknij prawym przyciskiem myszy hello **dane wejściowe** , a następnie wybierz węzeł **nowy element**.

    ![Nowy element](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. W oknie hello wybierz **Azure Stream Analytics wprowadzania**i zmień hello **nazwa** za**ExitStream.json**. Kliknij pozycję **Dodaj**.

    ![Dodaj nowy element okna](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Kliknij dwukrotnie **ExitStream.json** w projekcie hello i hello wykonaj kroki takie same jak hello wejścia strumienia. Należy się tooenter **zakończyć** dla hello **nazwy Centrum zdarzeń** pokazane na powitania po zrzut ekranu:

    ![Okno ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Teraz zdefiniowane dwóch strumieni wejściowych:

    ![Wejście i wyjście z strumienie wejściowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Następnie dodaj odwołanie do danych wejściowych hello pliku blob, który zawiera samochodu danych rejestracji.

13. Kliknij prawym przyciskiem myszy hello **dane wejściowe** węzła w hello projektu, a następnie hello wykonaj kroki takie same jak dane wejściowe strumienia hello. W **Alias wejściowy**, wprowadź **rejestracji**, a następnie w **typ źródła**, wybierz pozycję **danych referencyjnych**.

    ![Okno rejestracji](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. W **konta magazynu**, wybierz pozycję hello **tolldata** opcji. W **kontenera**, wybierz pozycję **tolldata**, a następnie w **wzorzec ścieżki**, wprowadź **registration.json**. Nazwa pliku jest rozróżniana wielkość liter i powinna być małymi literami.
15. toofinish hello kreatora, kliknij przycisk **zapisać**.

Teraz wszystkie dane wejściowe hello są zdefiniowane.

## <a name="define-hello-output"></a>Zdefiniuj hello danych wyjściowych
1.  W **Eksploratora rozwiązań**, rozwiń węzeł hello **dane wejściowe** węzeł i kliknij dwukrotnie **Output.json**.

2.  W **Alias wyjściowy**, wprowadź **dane wyjściowe**. 
3.  W **Sink**, wybierz pozycję **bazy danych SQL**.
4.  W **bazy danych**, wybierz pozycję **TollDataDB**.
5.  W **nazwy użytkownika**, wprowadź **tolladmin**. 
6.  W **hasło**, wprowadź **123toll!**.
7.  W **tabeli**, wprowadź **TollDataRefJoin**.
8.  Kliknij pozycję **Zapisz**.

    ![Okno danych wyjściowych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Utwórz kwerendę usługi analiza strumienia
W tym samouczku prób tooanswer kilka pytania biznesowe, które są powiązane tootoll danych. Tworzy zapytań usługi Stream Analytics, które mogą być używane w odpowiedzi odpowiednich tooprovide Stream Analytics.
Przed rozpoczęciem pierwszego zadania Stream Analytics, Przyjrzyjmy się prostego scenariusza i hello składnia zapytania.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Wprowadzenie toohello język zapytań usługi Stream Analytics
Załóżmy, że należy toocount hello liczba pojazdów, które wprowadź stoisku przez. Ponieważ w tym przykładzie jest stały strumień zdarzeń, masz toodefine okres czasu. Modyfikowanie toobe pytanie hello "ilu pojazdów wprowadź stoisku przez co trzy minuty?" Ten sposób toocount, którego dane są często określane tooas hello wirowania liczba.

Obejrzyj hello Stream Analytics kwerendę, która zawiera odpowiedzi na to pytanie:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Analiza strumienia używa języka kwerend, takiego jak SQL i dodaje kilka rozszerzeń toospecify związanych z czasem aspektów hello zapytania.

Aby uzyskać więcej informacji, zobacz [zarządzanie czasem](https://msdn.microsoft.com/library/azure/mt582045.aspx) i [Okienkową](https://msdn.microsoft.com/library/azure/dn835019.aspx) konstrukcji używanych w zapytaniu hello w witrynie MSDN.

Obecnie napisano pierwszego zapytania Stream Analytics, jest czas tootest go. Użyj pliki danych przykładowych hello znajduje się w folderze TollApp w hello następującej ścieżki:

.. \TollApp\TollApp\Data

Ten folder zawiera hello następujące pliki:
*   Entry.JSON
*   Exit.JSON
*   Registration.JSON

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Liczbę hello pojazdów stoisku przez
W projekcie powitania kliknij dwukrotnie **Script.asaql** tooopen hello skryptu w hello **edytora zapytań**. Skopiuj i Wklej hello skryptu w poprzedniej sekcji hello w edytorze hello. Witaj edytora zapytań obsługuje IntelliSense, kolorowanie składni i hello błąd znacznika.

![Edytor zapytań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Testowanie zapytań usługi Stream Analytics lokalnie

1. toocompile hello zapytania toosee Jeśli występuje błąd składni, kliknij prawym przyciskiem myszy projekt hello i wybierz **kompilacji**. 

2. toovalidate to zapytanie względem przykładowe dane, można użyć lokalnego przykładowych danych. Kliknij prawym przyciskiem myszy hello danych wejściowych, a następnie wybierz **dodać lokalne dane wejściowe**.

    ![Dodaj lokalne dane wejściowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. W oknie podręcznym hello wybierz hello przykładowych danych z ścieżki lokalnej. Kliknij pozycję **Zapisz**.

    ![Dodaj lokalne okna wejściowego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Plik o nazwie **local_EntryStream.json** jest automatycznie dodawany tooyour folderu danych wejściowych.

    ![Dodano tooinputs folder pliku](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. W hello **edytora zapytań**, kliknij przycisk **uruchom lokalnie**. Lub naciśnięcie klawisza F5 hello.

    ![Uruchom lokalnie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Dane wyjściowe uruchamiania lokalnego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Naciśnij klawisz żadnych danych wyjściowych hello tooview klucza w hello **ASA lokalnego uruchamiania wynik** okna w programie Visual Studio. 

    ![Okna ASA lokalnego uruchomienia wyniku](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Kliknij przycisk **Otwórz Folder wyników** pliki wyjściowe hello toocheck, zarówno w formacie CSV i JSON.

    ![Otwórz Folder wyników w danych wyjściowych](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Przykładowe dane wejściowe hello
Można również przykładowych danych wejściowych z pliku lokalnego tooa źródeł danych wejściowych. 
1. Kliknij prawym przyciskiem myszy plik wejściowy konfiguracji hello, a następnie wybierz **przykładowych danych**. 

   ![Dane przykładowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Teraz można przykładowe tylko Centrum zdarzeń lub Centrum IoT. Innych źródeł danych wejściowych nie są obsługiwane.

2. W oknie podręcznym hello wprowadź hello ścieżka lokalna używana toosave hello przykładowych danych. Kliknij przycisk **próbki**.

    ![Przykładowe okno danych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Wyświetlany postęp hello w hello **dane wyjściowe** okna. 

    ![Okno danych wyjściowych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Przedstawia tooAzure zapytań usługi Stream Analytics
1. W hello **edytora zapytań**, kliknij przycisk **przesłać tooAzure** w Edytorze skryptów hello.

    ![Prześlij tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Wybierz **utworzyć nowego zadania usługi analiza strumienia Azure**. Wprowadź hello **Nazwa zadania**i wybierz hello poprawne **subskrypcji**. Kliknij przycisk **przesłać**.

    ![Przedstawia okno zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Uruchom zadanie
Teraz, kiedy zadanie tworzenia widoku zadania hello automatycznie jest otwarty. 
1. Witaj toostart zadania, kliknij przycisk hello **zieloną strzałkę** przycisku.

    ![Uruchom zadanie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Wybierz ustawienie domyślne hello, a następnie kliknij przycisk **Start**.
 
    ![Uruchom okno zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    zadania Hello **stan** zmiany zbyt**systemem**, i **zdarzeń wprowadzania** i **zdarzeniach wyjściowych** są wyświetlane.

    ![Bieżący stan zadania Podsumowanie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Sprawdzanie wyników hello w programie Visual Studio
1. W programie Visual Studio Otwórz **Eksploratora serwera** i powitania kliknij prawym przyciskiem myszy **TollDataRefJoin** tabeli.
2. Wybierz **Pokaż dane tabeli** toosee hello dane wyjściowe z zadania.
   
    ![Wybór danych tabeli Pokaż w Eksploratorze serwera](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Wyświetlaj hello zadania metryki
Niektóre statystyki podstawowe zadania znajdują się w **metryki zadania**. 

![Okno metryk zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Lista zadań hello w Eksploratorze serwera
W **Eksploratora serwera**, kliknij przycisk **zadania usługi analiza strumienia** , a następnie kliknij przycisk **Odśwież**. zadanie Hello jest wyświetlany w obszarze **zadania usługi analiza strumienia**.

![W Eksploratorze serwera na liście zadania usługi analiza strumienia](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Otwórz hello widoku zadania
tooopen hello widoku zadania, rozwiń węzeł zadanie i kliknij dwukrotnie hello **widoku zadania** węzła.

![Węzeł w widoku zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Eksportuj istniejącego projektu tooa zadania
Istnieją dwa sposoby można wyeksportować istniejący projekt tooa zadania.

W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello zadania węzła w hello **zadania usługi analiza strumienia** a następnie wybierz węzeł **wyeksportować tooNew Stream Analytics projektu**.

![Eksportuj tooNew projektu usługi analiza strumienia](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

Projekt Hello jest generowana w **Eksploratora rozwiązań**.

![Projekt generowane w Eksploratorze rozwiązań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Możesz również użyć widoku zadania hello i kliknij przycisk **Generowanie projektu**.

![Generowanie projektu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Znane problemy i ograniczenia
 
- Nie jest obsługiwane dla danych wyjściowych usługi Power BI i wyjścia usługi Azure Data Lake Store.
- Brak obsługi edytora w celu dodawania lub zmiana JavaScript funkcje zdefiniowane przez użytkownika.

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Rozpoczynanie pracy przy użyciu usługi Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
