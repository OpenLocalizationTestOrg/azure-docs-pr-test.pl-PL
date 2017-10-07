---
title: "aaaAzure integracji usługi analiza strumienia i Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toouse funkcja zdefiniowana przez użytkownika i uczenia maszynowego w zadaniu Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Wykonywanie analiz wskaźniki nastrojów klientów przy użyciu usługi Azure Stream Analytics i usługi Azure Machine Learning
W tym artykule opisano sposób konfigurowania proste zadanie usługi analiza strumienia Azure, której zintegrowano usługi Azure Machine Learning tooquickly. Korzystają z modelu uczenia maszynowego wskaźniki nastrojów klientów analytics z hello dane przesyłane strumieniowo tekst tooanalyze Cortana Intelligence Gallery i określić hello wynik wskaźniki nastrojów klientów w czasie rzeczywistym. Przy użyciu pakietu Cortana Intelligence Suite hello pozwala wykonać to zadanie, nie martwiąc się o hello mogli dokładnie zapoznać tworzenia modelu analizy wskaźniki nastrojów klientów.

Należy zastosować, Dowiedz się od tooscenarios tego artykułu, takich jak te:

* Analizowanie w czasie rzeczywistym wskaźniki nastrojów klientów na przesyłanie strumieniowe danych Twitter.
* Analizowanie rekordy klienta rozmowy z pracownikami działu pomocy technicznej.
* Ocena komentarze dotyczące fora, blogi i wideo. 
* Wiele innych w czasie rzeczywistym, predykcyjnej oceniania scenariuszy.

W przypadku rzeczywistych jak hello danych bezpośrednio z serwisem Twitter strumienia danych. Samouczek hello toosimplify, możemy napisanych go tak, aby hello zadanie analizy przesyłania strumieniowego pobiera tweetów z pliku CSV w magazynie obiektów Blob Azure. Można utworzyć pliku CSV, lub można użyć przykładowy plik CSV, jak pokazano w powitania po obrazu:

![Przykładowe tweetów w pliku CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

utworzonego zadania przesyłania strumieniowego Analytics Hello stosuje modelu analizy wskaźniki nastrojów klientów hello w funkcji zdefiniowanej przez użytkownika (UDF) na powitania tekst danych z magazynu obiektów blob hello. dane wyjściowe Hello (hello wynik analizy wskaźniki nastrojów klientów hello) są zapisywane toohello tego samego magazynu obiektów blob w innym pliku CSV. 

Witaj poniższym rysunku pokazano tej konfiguracji. Jak wspomniano, dla scenariusza bardziej realistyczne można zastąpić strumienia danych Twitter z wejściem Azure Event Hubs magazynu obiektów blob. Ponadto można zbudować [Microsoft Power BI](https://powerbi.microsoft.com/) w czasie rzeczywistym wizualizację hello agregacji wskaźniki nastrojów klientów.    

![Omówienie integracji uczenia maszynowego usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem upewnij się, że masz następujące hello:

* Aktywna subskrypcja platformy Azure.
* Plik CSV z niektórych danych. Możesz pobrać plik hello przedstawiona wcześniej z [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), lub można utworzyć własny plik. W tym artykule przyjęto założenie, że używasz hello pliku z usługi GitHub.

Na wysokim poziomie toocomplete hello zadania zostało to pokazane w tym artykule należy hello następujące:

1. Tworzenie konta magazynu platformy Azure i kontener magazynu obiektów blob i przekaż kontenera toohello wejściowego pliku w formacie CSV.
3. Dodawanie modelu analizy wskaźniki nastrojów klientów z roboczym usługi Azure Machine Learning tooyour Cortana Intelligence Gallery hello i wdrożyć ten model jako usługę sieci web w hello obszaru roboczego uczenia maszynowego.
5. Utwórz zadanie usługi Stream Analytics, które wymaga tej usługi sieci web jako funkcję w kolejności toodetermine wskaźniki nastrojów klientów hello wprowadzania tekstu.
6. Uruchom zadanie usługi Stream Analytics hello i sprawdź hello danych wyjściowych.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Tworzenie kontenera magazynu i przekazywanie pliku wejściowego hello CSV
W tym kroku można użyć dowolnego pliku CSV, takich jak hello dostępna z usługi GitHub.

1. W portalu Azure hello, kliknij przycisk **nowy** &gt; **magazynu** &gt; **konta magazynu**.

   ![Utwórz nowe konto magazynu](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Podaj nazwę (`samldemo` w przykładzie hello). Nazwa Hello można użyć tylko małe litery i cyfry, i między Azure musi być unikatowa. 

3. Wybierz istniejącą grupę zasobów i określ lokalizację. Dla lokalizacji, zaleca się wszystkie zasoby hello utworzone w tym samouczku hello sam lokalizacji.

    ![Podaj szczegóły konta magazynu](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. W portalu Azure hello wybierz konto magazynu hello. W bloku konto magazynu hello, kliknij przycisk **kontenery** , a następnie kliknij przycisk  **+ &nbsp;kontenera** toocreate magazynu obiektów blob.

    ![Tworzenie kontenera obiektów blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Podaj nazwę kontenera hello (`azuresamldemoblob` w przykładzie hello) i sprawdź, czy **dostęp typu** ustawiono zbyt**obiektu Blob**. Gdy skończysz, kliknij przycisk **OK**.

    ![Określ szczegóły kontenera obiektów blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. W hello **kontenery** bloku, nowy kontener select hello, która otwiera blok powitania dla tego kontenera.

7. Kliknij pozycję **Przekaż**.

    ![Przekaż przycisk kontenera](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. W hello **przekazywanie obiektu blob** bloku, określ plik CSV hello mają toouse w tym samouczku. Dla **typu obiektu Blob**, wybierz pozycję **blokowych obiektów blob** i zestaw hello bloku rozmiar too4 MB, co jest wystarczająca dla tego samouczka.

    ![Przekaż plik obiektu blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Kliknij przycisk hello **przekazać** przycisk u dołu hello hello bloku.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Dodawanie modelu analizy hello wskaźniki nastrojów klientów z hello Cortana Intelligence Gallery

Teraz, hello przykładowe dane są w obiekcie blob, można włączyć model analizy wskaźniki nastrojów klientów hello w Cortana Intelligence Gallery.

1. Przejdź toohello [modelu analizy predykcyjnej wskaźniki nastrojów klientów](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) strony w hello Cortana Intelligence Gallery.  

2. Kliknij przycisk **Otwórz w Studio**.  
   
   ![Strumienia uczenia maszynowego analizy, otwórz Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Zaloguj się w obszarze roboczym toohello toogo. Wybierz lokalizację.

4. Kliknij przycisk **Uruchom** u dołu hello hello strony. Uruchamia proces Hello, co trwa około minuty.

   ![Uruchom eksperyment w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Po hello proces został uruchomiony pomyślnie, wybierz **wdrażanie usługi sieci Web** u dołu hello hello strony.

   ![Wdrażanie eksperymentu w usłudze Machine Learning Studio jako usługę sieci web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate, który hello wskaźniki nastrojów klientów modelu analytics jest gotowy toouse kliknij hello **testu** przycisku. Przekaż dane wejściowe, takie jak "Świetnie Microsoft". 

   ![Test eksperymentu w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Jeśli hello test działa, zostanie wyświetlony wynik toohello podobne, poniższy przykład:

   ![wyniki testu w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. W hello **aplikacji** kolumny, kliknij przycisk hello **programu Excel 2010 lub skoroszyt w starszej** toodownload łącze skoroszytu programu Excel. Witaj skoroszyt zawiera klucz hello interfejsu API i hello adres URL należy nowsze tooset hello zadania usługi analiza strumienia.

    ![Stream Analytics Machine Learning, szybkiego dostępu](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Utwórz zadanie usługi Stream Analytics, który używa modelu uczenia maszynowego hello

Można teraz utworzyć zadanie usługi Stream Analytics odczytujący hello tweetów przykładowe z pliku CSV hello w magazynie obiektów blob. 

### <a name="create-hello-job"></a>Utwórz zadanie hello

1. Przejdź toohello [portalu Azure](https://portal.azure.com).  

2. Kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**. 

   ![Azure portalu ścieżkę pobierania tooa nowego zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Nazwa zadania hello `azure-sa-ml-demo`, określ subskrypcję, określ istniejącą grupę zasobów lub Utwórz nową i wybierz lokalizację hello hello zadania.

   ![Określ ustawienia nowego zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Skonfiguruj zadania hello w danych wejściowych
zadanie Hello pobiera jej danych wejściowych z pliku CSV hello czy przesłany wcześniejszych tooblob magazynu.

1. Po hello zadania został utworzony, w obszarze **topologii zadania** w bloku zadania powitania kliknij hello **dane wejściowe** pole.  
   
   ![Pole "Dane wejściowe" w bloku zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. W hello **dane wejściowe** bloku, kliknij przycisk **+ Dodaj**.

   ![Dodawanie przycisku do dodawania zadania usługi analiza strumienia wejściowego toohello](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Wypełnianie hello **wprowadzania nowych** bloku następującymi wartościami:

    * **Alias wejściowy**: Użyj nazwy hello `datainput`.
    * **Typ źródła**: Wybierz **strumienia danych**.
    * **Źródło**: Wybierz **magazynu obiektów Blob**.
    * **Opcji importowania**: Wybierz **Użyj magazynu obiektów blob z bieżącej subskrypcji**. 
    * **Konto magazynu**. Wybierz utworzone wcześniej konto magazynu hello.
    * **Kontener**. Kontener hello wybierz wcześniej utworzony (`azuresamldemoblob`).
    * **Format serializacji zdarzeń**. Wybierz **CSV**.

    ![Ustawienia dla nowego zadania danych wejściowych.](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Kliknij przycisk **Utwórz**.

### <a name="configure-hello-job-output"></a>Skonfiguruj hello dane wyjściowe zadania
Witaj zadania wysyła wyników toohello sam obiektu blob magazynu, w którym pobiera dane wejściowe. 

1. W obszarze **topologii zadania** w bloku zadania powitania kliknij hello **dane wyjściowe** pole.  
  
   ![Utwórz nowe dane wyjściowe zadania przesyłania strumieniowego usługi analiza](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. W hello **dane wyjściowe** bloku, kliknij przycisk **+ Dodaj**, a następnie dodaj wyjście z aliasem hello `datamloutput`. 

3. Aby uzyskać **Sink**, wybierz pozycję **magazynu obiektów Blob**. Następnie wypełnij hello reszty hello output ustawień za pomocą hello takie same wartości, używane do magazynu obiektów blob powitania dla danych wejściowych:

    * **Konto magazynu**. Wybierz utworzone wcześniej konto magazynu hello.
    * **Kontener**. Kontener hello wybierz wcześniej utworzony (`azuresamldemoblob`).
    * **Format serializacji zdarzeń**. Wybierz **CSV**.

   ![Ustawienia dla nowego dane wyjściowe zadania](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Kliknij przycisk **Utwórz**.   


### <a name="add-hello-machine-learning-function"></a>Dodawanie funkcji Machine Learning hello 
Wcześniej opublikowaniu usługi sieci web tooa modelu uczenia maszynowego. W naszym scenariuszu po uruchomieniu zadanie analizy strumienia hello wysyła każdego tweet próbki z hello usługi sieci web toohello wejściowy do analizy wskaźniki nastrojów klientów. usługi sieci web uczenie maszynowe Hello zwraca wskaźniki nastrojów klientów (`positive`, `neutral`, lub `negative`) i prawdopodobieństwo tweet hello jest dodatnia. 

W tej części samouczka hello można zdefiniować funkcję hello zadanie analizy strumienia. Funkcja Hello można wywołanej toosend tweet toohello usługi sieci web i wrócić hello odpowiedzi. 

1. Upewnij się, że masz hello klucza usługi sieci web adres URL i interfejsu API pobranego wcześniej hello skoroszytu programu Excel.

2. Zwraca toohello zadania omówienie bloku.

3. W obszarze **ustawienia**, wybierz pozycję **funkcje** , a następnie kliknij przycisk **+ Dodaj**.

   ![Dodaj zadanie usługi Stream Analytics toohello — funkcja](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Wprowadź `sentiment` jako hello alias funkcji i wypełnianie hello reszty bloku hello przy użyciu następujących wartości:

    * **Typ funkcji**: Wybierz **uczenie Maszynowe Azure**.
    * **Opcji importowania**: Wybierz **importu z innej subskrypcji**. Dzięki temu można szansy tooenter hello URL i klucza.
    * **Adres URL**: Wklej adres URL usługi sieci web hello.
    * **Klucz**: Wklej w kluczu hello interfejsu API.
  
    ![Ustawienia dotyczące dodawania zadania usługi analiza strumienia toohello funkcji Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Kliknij przycisk **Utwórz**.

### <a name="create-a-query-tootransform-hello-data"></a>Utwórz zapytanie tootransform hello danych

Analiza strumienia używa danych wejściowych deklaratywne kwerendy SQL na podstawie tooexamine hello i go przetworzyć. W tej sekcji utworzysz kwerendę, która odczytuje tweet każdej z danych wejściowych, a następnie wywołuje hello uczenia maszynowego funkcja tooperform wskaźniki nastrojów klientów analizy. Zapytanie Hello wysyła następnie toohello wynik hello output zdefiniowania (magazynu obiektów blob).

1. Zwraca toohello zadania omówienie bloku.

2.  W obszarze **topologii zadania**, kliknij przycisk hello **zapytania** pole.

    ![Utwórz zapytanie dotyczące zadanie analizy przesyłania strumieniowego](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Wprowadź hello następujące zapytania:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    zapytania Hello wywołuje funkcję hello utworzonym wcześniej (`sentiment`) w kolejności tooperform wskaźniki nastrojów klientów analizy w każdym tweet w danych wejściowych hello. 

4. Kliknij przycisk **zapisać** toosave hello zapytania.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Uruchom zadanie usługi Stream Analytics hello i sprawdź dane wyjściowe hello

Można teraz uruchomić zadania Stream Analytics hello.

### <a name="start-hello-job"></a>Uruchom zadanie hello
1. Zwraca toohello zadania omówienie bloku.

2. Kliknij przycisk **Start** u góry bloku hello hello.

    ![Utwórz zapytanie dotyczące zadanie analizy przesyłania strumieniowego](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. W hello **rozpoczęcia zadania**, wybierz pozycję **niestandardowe**, a następnie wybierz jeden dzień toowhen poprzednich przesłanych magazynu tooblob pliku CSV hello. Gdy wszystko będzie gotowe, kliknij przycisk **Start**.  


### <a name="check-hello-output"></a>Sprawdź dane wyjściowe hello
1. Let hello zadanie było uruchamiane kilka minut, aż zostanie wyświetlony działania w hello **monitorowanie** pole. 

2. Jeśli masz narzędzie normalnie korzystać tooexamine hello zawartość magazynu obiektów blob, użyj tego narzędzia tooexamine hello `azuresamldemoblob` kontenera. Alternatywnie hello następujące kroki w portalu Azure hello:

    1. W portalu hello Znajdź hello `samldemo` magazynu konta, a w ramach konta hello Znajdź hello `azuresamldemoblob` kontenera. Zobacz dwa pliki w kontenerze hello: hello plik zawierający hello próbki tweetów i plik CSV wygenerowany przez zadanie usługi Stream Analytics hello.
    2. Kliknij prawym przyciskiem myszy hello wygenerowany plik, a następnie wybierz **Pobierz**. 

   ![Pobierz dane wyjściowe zadania CSV z magazynu obiektów Blob](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Otwórz hello wygenerowany plik CSV. Zostanie wyświetlony ekran podobny do hello poniższy przykład:  
   
   ![Wyświetl Stream Analytics Machine Learning, CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Wyświetlaj metryki
Można również wyświetlić metryk powiązanych funkcji usługi Azure Machine Learning. Witaj następujących metryk powiązanych funkcji są wyświetlane w hello **monitorowanie** pole w bloku zadania hello:

* **Funkcja żądania** wskazuje hello liczbę żądań wysłanych tooa usługi sieci web Machine Learning.  
* **Działania zdarzenia** wskazuje hello liczby zdarzeń w żądaniu hello. Domyślnie tooa każdego żądania usługi sieci web Machine Learning zawiera zapasową too1, 000 zdarzeń.  


## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Integracja interfejsu API REST i uczenia maszynowego](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)



