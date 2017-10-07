---
title: "czas aaaReal Twitter wskaźniki nastrojów klientów analizy z usługą Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse analiza strumienia w czasie rzeczywistym analizy wskaźniki nastrojów klientów usługi Twitter. Wskazówki krok po kroku z toodata generowania zdarzeń na pulpicie nawigacyjnym na żywo."
keywords: "Analiza trendu w czasie rzeczywistym usługi twitter, analizy wskaźniki nastrojów klientów, analizy mediów społecznościowych, przykład analizy trendów"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>W czasie rzeczywistym analizy usługi Azure Stream Analytics wskaźniki nastrojów klientów usługi Twitter

Dowiedz się, jak toobuild wskaźniki nastrojów klientów rozwiązania analizy w celu wykonania analizy mediów społecznościowych przełączając w czasie rzeczywistym w usłudze Twitter zdarzeń w usłudze Azure Event Hubs. Następnie można zapisywać danych hello Azure Stream Analytics query tooanalyze i albo zapisać hello wyniki do późniejszego użycia i przy użyciu pulpitu nawigacyjnego i [usługi Power BI](https://powerbi.com/) tooprovide wgląd w czasie rzeczywistym.

Narzędzia do analizy mediów społecznościowych pomagające organizacjom Zrozumienie trendów tematów. Tematy trendów są tematy i stanowisk, w których znajduje się duża liczba wpisów w mediów społecznościowych. Wskaźniki nastrojów klientów analizy, która jest również nazywany *wyszukiwania opinii*, korzysta z mediami społecznościowymi analytics narzędzia toodetermine stanowisk kierunku produktu, pomysł i tak dalej. 

W czasie rzeczywistym analizy trendów w serwisie Twitter jest doskonałym przykładem narzędzia analizy, ponieważ hello hasztagiem subskrypcji modelu pozwala słowa kluczowe toospecific toolisten (hashtagów) i utworzyć wskaźniki nastrojów klientów analizy hello źródła danych.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Scenariusz: Mediów społecznościowych wskaźniki nastrojów klientów analizy w czasie rzeczywistym

Firma, która ma nośnika wiadomości witryny sieci Web jest zainteresowana uzyskanie korzyści wyprzedzenia konkurencji przez zawierających zawartość witryny, która jest natychmiast odpowiednich tooits czytników. Witaj w firmie analizy mediów społecznościowych dotyczące kwestii, które są odpowiednie tooreaders wykonując wskaźniki nastrojów klientów w czasie rzeczywistym analizy danych Twitter.

tooidentify tematy trendów w czasie rzeczywistym w serwisie Twitter, hello analiz w czasie rzeczywistym potrzeb firmy dotyczących hello tweet woluminów i wskaźniki nastrojów klientów tematy klucza. Innymi słowy hello jest aparat analizy analytics wskaźniki nastrojów klientów, oparty na tym nośniku społecznościowych źródła danych.

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku użyjesz aplikacji klienta, który jest podłączany tooTwitter i wyszukuje tweetów mających niektórych hashtagów (które można ustawić). W kolejności toorun hello aplikacji i analizować hello tweetów przy użyciu usługi analiza strumienia Azure, musi mieć następujące hello:

* Subskrypcja platformy Azure
* Konto w serwisie Twitter 
* Aplikacja usługi Twitter i hello [token dostępu OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) dla tej aplikacji. Firma Microsoft udostępnia ogólne instrukcje toocreate aplikacji Twitter, który jest później.
* Witaj TwitterWPFClient aplikacji, która odczytuje hello Twitter źródła danych. tooget tej aplikacji, pobierania hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) plików z witryny GitHub i następnie Rozpakuj pakiet hello do folderu na komputerze. Jeśli chcesz, aby kod źródłowy hello toosee i uruchomić aplikację hello w debugerze, możesz uzyskać hello kodu źródłowego z [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Tworzenie Centrum zdarzeń dla analizy strumienia danych wejściowych

Hello Przykładowa aplikacja generuje zdarzenia i umieszcza je tooan Centrum zdarzeń platformy Azure. Usługa Azure event hubs są hello preferowana metoda wprowadzanie zdarzeń dla usługi Stream Analytics. Aby uzyskać więcej informacji, zobacz hello [dokumentacji usługi Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Tworzenie Centrum zdarzeń w przestrzeni nazw i Centrum zdarzeń
W tej procedurze należy najpierw utworzyć przestrzeń nazw Centrum zdarzeń, a następnie dodaj do przestrzeni nazw toothat Centrum zdarzeń. Przestrzenie nazw Centrum zdarzeń są używane grupy toologically związane z wystąpień magistrali zdarzeń. 

1. Zaloguj się za toohello portalu Azure, a następnie kliknij przycisk **nowy** > **Internetu rzeczy** > **Centrum zdarzeń**. 

2. W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw, takich jak `<yourname>-socialtwitter-eh-ns`. Można użyć dowolnej nazwy przestrzeni nazw hello, ale hello nazwa musi być prawidłowa dla danego adresu URL i między Azure musi być unikatowa. 
    
3. Wybierz subskrypcję i Utwórz lub wybierz grupę zasobów, a następnie kliknij przycisk **Utwórz**. 

    ![Tworzenie przestrzeni nazw Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Po zakończeniu przestrzeni nazw hello wdrażania można znaleźć przestrzeni nazw Centrum zdarzeń hello na liście zasobów platformy Azure. 

5. Kliknij hello nowej przestrzeni nazw, a w bloku przestrzeni nazw powitania kliknij  **+ &nbsp;Centrum zdarzeń**. 

    ![przycisk Dodaj Centrum zdarzeń Hello do tworzenia nowego Centrum zdarzeń ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Nazwa hello nowym Centrum zdarzeń `socialtwitter-eh`. Można użyć innej nazwy. Jeśli to zrobisz, zanotuj, ponieważ potrzebna nazwa hello później. Nie trzeba tooset inne opcje dla hello Centrum zdarzeń.

    ![Blok do tworzenia nowego Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Kliknij przycisk **Utwórz**.


### <a name="grant-access-toohello-event-hub"></a>Centrum zdarzeń toohello dostępu GRANT

Aby proces może wysłać Centrum zdarzeń tooan danych, Centrum zdarzeń hello musi mieć zasadę, która umożliwia uzyskanie odpowiedniego dostępu. zasady dostępu Hello generuje ciąg połączenia, który zawiera informacje o autoryzacji.

1.  W bloku przestrzeni nazw zdarzeń powitania kliknij **usługi Event Hubs** a następnie kliknij nazwę hello nowe Centrum zdarzeń.

2.  W bloku Centrum zdarzeń hello, kliknij przycisk **zasady dostępu współużytkowanego** , a następnie kliknij przycisk  **+ &nbsp;Dodaj**.

    >[!NOTE]
    >Upewnij się, że pracujesz z Centrum zdarzeń hello, nie hello Centrum przestrzeni nazw zdarzenia.

3.  Dodaj zasady o nazwie `socialtwitter-access` i **oświadczeń**, wybierz pozycję **Zarządzaj**.

    ![Blok do tworzenia nowych zasad dostępu do Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Kliknij przycisk **Utwórz**.

5.  Po wdrożeniu zasad powitania kliknij go hello liście zasady dostępu współdzielonego.

6.  Znajdź pole hello **klucz podstawowy ciąg połączenia** i kliknij przycisk hello kopiowania przycisku Dalej toohello parametry połączenia. 
    
    ![Kopiowanie klucza ciąg połączenia głównej hello hello zasady dostępu](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Wklej parametry połączenia hello w edytorze tekstu. Należy tego ciągu połączenia dla następnej sekcji hello, po wprowadzeniu niektórych tooit małych edycji.

    Parametry połączenia Hello wygląda następująco:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Powiadomienie, że parametry połączenia hello zawiera wiele par klucz wartość, oddzielając je średnikami: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, i `EntityPath`.  

    > [!NOTE]
    > Dla bezpieczeństwa części hello parametry połączenia w przykładzie hello zostały usunięte.

8.  W edytorze tekstu hello, Usuń hello `EntityPath` parę z parametrów połączenia hello (nie zapomnij tooremove hello średnika, przechwyceniem). Gdy wszystko będzie gotowe, ciąg połączenia hello wygląda następująco:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Skonfiguruj i uruchom aplikację klienta usługi Twitter hello
Aplikacja kliencka Hello pobiera zdarzenia tweet bezpośrednio z usługą Twitter. W celu toodo tak, musi on hello toocall uprawnienia w usłudze Twitter interfejsów API przesyłania strumieniowego. tooconfigure, że uprawnienia do tworzenia aplikacji w usłudze Twitter, generowany unikatowy poświadczeń (takich jak token OAuth). Następnie można skonfigurować powitania klienta aplikacji toouse tych poświadczeń podczas wykonywania wywołań interfejsu API. 

### <a name="create-a-twitter-application"></a>Utwórz aplikację usługi Twitter
Jeśli nie masz już aplikację usługi Twitter, która służy do celów tego samouczka, można go utworzyć. Musi już konta w usłudze Twitter.

> [!NOTE]
> proces dokładnego Hello w Twitter do tworzenia aplikacji i uzyskiwanie hello kluczy, kluczy tajnych i token mogą ulec zmianie. Jeśli te instrukcje nie są zgodne, można znaleźć w witrynie Twitter hello, zapoznaj się z dokumentacją dewelopera Twitter toohello.

1. Przejdź toohello [strony zarządzania aplikacji Twitter](https://apps.twitter.com/). 

2. Utwórz nową aplikację. 

    * Witaj adresu URL witryny sieci Web Określ prawidłowy adres URL. Toobe nie ma lokacji na żywo. (Nie można określić tylko `localhost`.)
    * Witaj wywołania zwrotnego pole puste. Aplikacja kliencka Hello używanej w tym samouczku nie wymagają wywołań zwrotnych.

    ![Tworzenie aplikacji w usłudze Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Opcjonalnie można zmienić uprawnienia aplikacji hello tylko tooread.

4. Po utworzeniu aplikacji hello Przejdź toohello **kluczy i tokenów dostępu** strony.

5. Kliknij przycisk toogenerate przycisk hello token dostępu i klucz tajny tokenu dostępu.

Zachowaj te informacje przydatne, ponieważ będzie potrzebny w następnej procedurze hello.

>[!NOTE]
>Hello kluczy i kluczy tajnych dla aplikacji Twitter hello zapewniają dostęp do konta w usłudze Twitter tooyour. Traktować te informacje jako poufne, hello takie same, jak hasło usługi Twitter. Na przykład nie osadzaj te informacje w aplikacji, że podajesz tooothers. 


### <a name="configure-hello-client-application"></a>Konfigurowanie aplikacji klienta hello
Utworzyliśmy aplikacji klienckiej, która łączy się przy użyciu danych tooTwitter [API przesyłania strumieniowego w serwisie Twitter](https://dev.twitter.com/streaming/overview) toocollect tweet zdarzenia o określony zbiór tematów. Aplikacja Hello używa hello [Sentiment140](http://help.sentiment140.com/) narzędzie typu open source, który przypisuje powitania po tweet tooeach wartość wskaźniki nastrojów klientów:

* 0 = ujemna
* 2 = neutral
* 4 = dodatnią

Po przypisaniu zdarzenia tweet hello wartość wskaźniki nastrojów klientów, są one wypychana toohello Centrum zdarzeń, który został utworzony wcześniej.

Przed uruchomieniem aplikacji hello, wymaga pewne informacje, takie jak klucze Twitter hello i parametry połączenia Centrum zdarzeń hello. Można podać informacje o konfiguracji hello w następujący sposób:

* Uruchamianie aplikacji hello, a następnie użyj aplikacji hello interfejsu użytkownika tooenter hello kluczy, kluczy tajnych i parametry połączenia. Jeśli to zrobisz, informacje o konfiguracji hello jest używany dla bieżącej sesji, ale nie jest on zapisany.
* Edytowanie pliku config aplikacji hello i wartości hello zestawu. Takie podejście będzie nadal występował, informacje o konfiguracji hello, ale oznacza to również, że te potencjalnie wrażliwe informacje są przechowywane w postaci zwykłego tekstu na komputerze.

Witaj poniższej procedury dokumentów obu podejść. 

1. Upewnij się, że zostały pobrane i rozpakowane hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplikacji, wymienione w hello wymagania wstępne.

2. tooset hello wartości w czasie wykonywania (i tylko dla bieżącej sesji hello), uruchom hello `TwitterWPFClient.exe` aplikacji. Gdy aplikacja hello monit, wprowadź hello następujące wartości:

    * Witaj w usłudze Twitter konsumenta (klucz interfejsu API).
    * Witaj w usłudze Twitter klucz tajny klienta (klucz tajny interfejsu API).
    * Witaj w usłudze Twitter tokenu dostępu.
    * Witaj w usłudze Twitter klucz tajny tokenu dostępu.
    * Hello informacje ciągu połączenia, który został wcześniej zapisany. Upewnij się, że użyto parametrów połączenia hello usunięcie hello `EntityPath` pary klucz wartość z.
    * Witaj Twitter słów kluczowych, które mają toodetermine wskaźniki nastrojów klientów dla.

   ![Aplikacja TwitterWpfClient uruchomiony, pokazujący ustawienia pośrednie](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. wartości hello tooset trwale, użyj pliku TwitterWpfClient.exe.config hello tooopen edytora tekstu. Następnie w hello `<appSettings>` element, w tym:

    * Ustaw `oauth_consumer_key` toohello klucz klienta usługi Twitter (klucz interfejsu API). 
    * Ustaw `oauth_consumer_secret` toohello Twitter klucz tajny klienta (klucz tajny interfejsu API).
    * Ustaw `oauth_token` toohello Token dostępu w usłudze Twitter.
    * Ustaw `oauth_token_secret` toohello Twitter klucz tajny tokenu dostępu.

    Dalszej części hello `<appSettings>` element, wprowadź następujące zmiany:

    * Ustaw `EventHubName` nazwy Centrum zdarzeń toohello (to znaczy toohello wartość hello jednostki ścieżki).
    * Ustaw `EventHubNameConnectionString` toohello parametry połączenia. Upewnij się, że użyto parametrów połączenia hello usunięcie hello `EntityPath` pary klucz wartość z.

    Witaj `<appSettings>` sekcji wygląda hello poniższy przykład. (Dla jasności i zabezpieczeń, możemy opakowana wiersze i usunąć niektóre znaki.)

    ![TwitterWpfClient pliku konfiguracji aplikacji w edytorze tekstów, przedstawiający hello Twitter kluczy i kluczy tajnych i informacje o parametrach połączenia Centrum zdarzeń hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Jeśli nie został już uruchomiony aplikacji hello, uruchom teraz TwitterWpfClient.exe. 

5. Kliknij przycisk hello start zielony przycisk toocollect społecznościowych wskaźniki nastrojów klientów. Zobacz Tweet zdarzeń o hello **CreatedAt**, **tematu**, i **SentimentScore** wartości wysyłane tooyour Centrum zdarzeń.

    ![Uruchomiona jest aplikacja TwitterWpfClient, przedstawiający listę tweetów](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Jeśli występuje błąd, a strumień tweetów wyświetlane w dolnej części okna hello hello jest niewidoczny, należy dokładnie sprawdzić hello kluczy i kluczy tajnych. Sprawdź również parametry połączenia hello (Upewnij się, że nie ma hello `EntityPath` kluczy i wartości.)


## <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics

Teraz, gdy zdarzenia tweet strumieniowe w czasie rzeczywistym z serwisem Twitter, skonfigurowaniem tooanalyze zadania usługi analiza strumienia tych zdarzeń w czasie rzeczywistym.

1. W portalu Azure hello, kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.

2. Nazwa zadania hello `socialtwitter-sa-job` i określ subskrypcję, lokalizacji i grupy zasobów.

    Z dobrze tooplace hello zadania i hello Centrum zdarzeń w hello jest tym samym regionie, aby uzyskać najlepszą wydajność i dlatego nie zwracania tootransfer danych między regionami.

    ![Tworzenie nowego zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Kliknij przycisk **Utwórz**.

    Utworzono zadanie Hello i hello portal Wyświetla szczegóły zadania.


## <a name="specify-hello-job-input"></a>Określ dane wejściowe zadania hello

1. W przypadku zadania Stream Analytics w obszarze **topologii zadania** w środku hello hello zadania bloku, kliknij przycisk **dane wejściowe**. 

2. W hello **dane wejściowe** bloku, kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:

    * **Alias wejściowy**: Użyj nazwy hello `TwitterStream`. Użyj innej nazwy, aby je zapisać, ponieważ będzie potrzebny później.
    * **Typ źródła**: Wybierz **strumienia danych**.
    * **Źródło**: Wybierz **Centrum zdarzeń**.
    * **Opcji importowania**: Wybierz **Użyj Centrum zdarzeń z bieżącej subskrypcji**. 
    * **Przestrzeń nazw magistrali usług**: Wybierz hello Centrum przestrzeni nazw zdarzenia utworzonego wcześniej (`<yourname>-socialtwitter-eh-ns`).
    * **Centrum zdarzeń**: Centrum zdarzeń hello wybierz utworzony wcześniej (`socialtwitter-eh`).
    * **Nazwa zasad Centrum zdarzeń**: Wybierz zasady dostępu hello utworzonego wcześniej (`socialtwitter-access`).

    ![Utwórz nowe dane wejściowe zadania przesyłania strumieniowego usługi analiza](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Kliknij przycisk **Utwórz**.


## <a name="specify-hello-job-query"></a>Określ zapytanie dotyczące zadań hello

Analiza strumienia obsługuje prosty, deklaratywny model zapytań opisujący przekształcenia. toolearn więcej informacji na temat języka hello, zobacz hello [Azure Stream Analytics zapytania Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Ten samouczek ułatwia tworzenie i testowanie kilka zapytań za pośrednictwem danych Twitter.

toocompare hello liczby uwagi między tematami, można użyć [okno wirowania](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello liczba uwagi w temacie co pięć sekund.

1. Zamknij hello **dane wejściowe** bloku, jeśli nie jest jeszcze.

2. W bloku zadania powitania kliknij hello **zapytania** pole. Azure zawiera dane wejściowe hello i dane wyjściowe, które są skonfigurowane dla zadania hello i pozwala utworzyć kwerendę, która umożliwia przekształcenie strumienia wejściowego hello podczas przesyłania danych wyjściowych toohello.

3. Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona. 

3. W hello **zapytania** bloku, kliknij przycisk Dalej toohello punktów hello `TwitterStream` danych wejściowych, a następnie wybierz **przykładowe dane z danych wejściowych**.

    ![Menu Opcje toouse przykładowych danych do hello wpis "Przykładowych danych z danych wejściowych" wybrane zadania przesyłania strumieniowego Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Spowoduje to otwarcie bloku, który pozwala określić, ile tooget dane przykładowe, zdefiniowanych pod względem jak długo tooread hello wejściowych strumienia.

4. Ustaw **minut** too3, a następnie kliknij przycisk **OK**. 
    
    ![Próbkowanie hello strumienia wejściowego, z "3 minuty" wybrane opcje.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure przykłady 3 minut, przez które danych ze strumienia wejściowego hello i powiadamia użytkownika, gdy będzie gotowy hello przykładowych danych. (Trwa to krótki czas). 

    Hello przykładowe dane są tymczasowo przechowywane i jest dostępny, gdy masz hello okna kwerendy. Jeśli zamkniesz okno kwerendy hello hello przykładowe dane są usuwane, a masz toocreate nowy zestaw przykładowych danych. 

5. Zmień zapytanie hello w następujących toohello edytora kodu hello:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Jeśli nie użyto `TwitterStream` jako hello aliasu dla danych wejściowych hello, Zastąp aliasu dla `TwitterStream` w zapytaniu hello.  

    To zapytanie używa hello **TIMESTAMP BY** toospecify — słowo kluczowe w toobe ładunku hello używany w obliczeniach danych czasowych hello pola sygnatury czasowej. Jeśli to pole nie zostanie określona, hello okien operacja została wykonana za pomocą czas hello każdego zdarzenia dotarły hello Centrum zdarzeń. Dowiedz się więcej w sekcji hello "Godzina nadejścia vs czas aplikacji" [Stream Analytics kwerendy odwołania](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    To zapytanie również uzyskuje dostęp do sygnatury czasowej do hello koniec każdego okna przy użyciu hello **System.Timestamp** właściwości.

5. Kliknij przycisk **testu**. Zapytanie Hello jest uruchamiana dla danych hello pobrano.
    
6. Kliknij pozycję **Zapisz**. Spowoduje to zapisanie hello zapytania jako część zadania przesyłania strumieniowego Analytics hello. (Nie zostanie on zapisany hello przykładowe dane).


## <a name="experiment-using-different-fields-from-hello-stream"></a>Przy użyciu różnych pól ze strumienia hello eksperymentu 

Witaj poniższej tabeli wymieniono hello pola, które są częścią hello dane przesyłane strumieniowo JSON. Możesz wolnego tooexperiment w edytorze zapytań hello.

|Właściwość JSON | Definicja|
|--- | ---|
|CreatedAt | czas Hello tego tweet hello został utworzony|
|Temat | temat Hello, który odpowiada hello określone słowo kluczowe|
|SentimentScore | wskaźniki nastrojów klientów Hello wyniku Sentiment140|
|Autor | dojście Twitter Hello wysyłane hello tweet|
|Tekst | Pełna treść Hello hello tweet|


## <a name="create-an-output-sink"></a>Utwórz ujście danych wyjściowych

Teraz zdefiniowano strumienia zdarzeń, zdarzenia wejściowe tooingest Centrum zdarzeń i tooperform zapytania transformację za pośrednictwem hello strumienia. ostatni krok Hello jest toodefine ujście danych wyjściowych zadania hello.  

W tym samouczku pisania hello zagregowane tweet zdarzenia z hello zadania kwerendy tooAzure magazynu obiektów Blob.  Możesz również wypchnąć z wyników tooAzure bazy danych SQL, magazynem tabel Azure Event Hubs lub usługa Power BI, w zależności od aplikacji wymaga.

## <a name="specify-hello-job-output"></a>Określ hello dane wyjściowe zadania

1. W hello **topologii zadania** kliknij hello **dane wyjściowe** pole. 

2. W hello **dane wyjściowe** bloku, kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:

    * **Alias wyjściowy**: Użyj nazwy hello `TwitterStream-Output`. 
    * **Obiekt sink**: Wybierz **magazynu obiektów Blob**.
    * **Opcje importowania**: Wybierz **Użyj magazynu obiektów blob z bieżącej subskrypcji**.
    * **Konto magazynu**. Wybierz **Utwórz nowe konto magazynu.**
    * **Konto magazynu** (drugie pole). Wprowadź `YOURNAMEsa`, gdzie `YOURNAME` jest nazwa użytkownika lub inny unikatowy ciąg. Nazwa Hello można użyć tylko małe litery i cyfry, i między Azure musi być unikatowa. 
    * **Kontener**. Wprowadź `socialtwitter`.
    Nazwa konta magazynu Hello i nazwa kontenera są używane razem tooprovide identyfikator URI dla magazynu obiektów blob hello w następujący sposób: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Blok "Nowe dane wyjściowe" zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Kliknij przycisk **Utwórz**. 

    Azure tworzy konto magazynu hello i automatycznie generuje klucz. 

5. Zamknij hello **dane wyjściowe** bloku. 


## <a name="start-hello-job"></a>Uruchom zadanie hello

Dane wejściowe zadania, zapytań i dane wyjściowe zostały określone. To zadanie usługi Stream Analytics hello toostart gotowe.

1. Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona. 

2. W bloku zadania powitania kliknij **Start**.

    ![Uruchom zadanie usługi Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. W hello **rozpoczęcia zadania** bloku dla **dane wyjściowe zadania godzina rozpoczęcia**, wybierz pozycję **teraz** , a następnie kliknij przycisk **Start**. 

    ![Blok "Uruchomić zadanie" hello zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure sygnalizuje hello zadań została uruchomiona, a następnie w bloku zadania hello, zostanie wyświetlony stan hello **systemem**.

    ![Uruchomione zadanie](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Widok danych wyjściowych analizy wskaźniki nastrojów klientów

Po uruchomieniu zadania przetwarza hello strumienia w czasie rzeczywistym w serwisie Twitter, można wyświetlić dane wyjściowe hello analizy wskaźniki nastrojów klientów.

Można użyć narzędzia, takiego jak [Eksploratora usługi Storage Azure](https://http://storageexplorer.com/) lub [Eksploratora Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview w czasie rzeczywistym danych wyjściowych zadania. W tym miejscu, można użyć [usługi Power BI](https://powerbi.com/) tooextend Twojego tooinclude aplikacji dostosowany pulpit nawigacyjny, takich jak Witaj, co pokazano na powitania po zrzut ekranu:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Utwórz zapytanie innego tooidentify trendów — tematy

Inne zapytanie, można użyć toounderstand Twitter wskaźniki nastrojów klientów jest oparta na [przedłużanie okna](https://msdn.microsoft.com/library/azure/dn835051.aspx). Tematy trendów tooidentify, możesz wyszukiwać tematy przekraczających wartość progową uwagi w określonym czasie.

Do celów tego samouczka hello możesz sprawdzić tematów, które są wymienione więcej niż 20 razy w hello ostatnich 5 sekund.

1. W bloku zadania powitania kliknij **zatrzymać** toostop hello zadania. 

2. W hello **topologii zadania** kliknij hello **zapytania** pole. 

3. Zmień hello zapytania toohello poniżej:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Kliknij pozycję **Zapisz**.

5. Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona. 

6. Kliknij przycisk **Start** toorestart hello zadania przy użyciu hello nowe zapytanie.


## <a name="get-support"></a>Uzyskiwanie pomocy technicznej
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
