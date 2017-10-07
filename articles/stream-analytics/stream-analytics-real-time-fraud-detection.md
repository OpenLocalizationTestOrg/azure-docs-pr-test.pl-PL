# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Rozpoczynanie pracy przy użyciu usługi Azure Stream Analytics: wykrywanie oszustw w czasie rzeczywistym

Ten samouczek zawiera ilustrację end-to-end jak toouse Azure Stream Analytics. Omawiane kwestie: 

* Przełącz strumienia zdarzeń do wystąpienia usługi Azure Event hubs. W tym samouczku użyjesz aplikacji, która udostępniamy symulujący strumienia rekordów metadanych telefonu komórkowego.

* Zapisane przypominającego SQL Stream Analytics zapytania tootransform, agregowanie informacji lub będzie zaglądać wzorców. Zobaczysz, jak toouse tooexamine zapytania hello strumienia przychodzącego i wyszukaj wywołania, które mogą być fałszywe.

* Wyślij hello wyniki tooan dane wyjściowe zbiornika (magazyn), który można analizować, aby uzyskać dodatkowe informacje szczegółowe. W takim przypadku użytkownik wyśle magazynu obiektów Blob tooAzure hello podejrzane połączenia danych.

W tym samouczku używamy przykład Witaj wykrywania oszustw w czasie rzeczywistym na podstawie danych z połączenia telefonicznego. Ale możemy ilustrują technika hello również nadaje się do innych typów wykrywania oszustw, takie jak karty kredytowej oszustwa lub kradzieży tożsamości. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Scenariusz: Telekomunikacyjnych i SIM wykrywanie oszustw w czasie rzeczywistym

Firmy telekomunikacyjnych ma duże ilości danych na połączenia przychodzące. Witaj firma chce się, że toodetect fałszywych wywoływanych w czasie rzeczywistym, aby mogli powiadamiać klientów lub wyłączyć usługi dla określonej liczby. Jeden typ oszustwa SIM obejmuje wiele wywołań z hello tej samej tożsamości wokół hello w sam czas jednak geograficznie różnych lokalizacjach. toodetect ten typ oszustwa, hello firmy potrzeb tooexamine przychodzące phone rekordów i szukania wzorców określone — w takim przypadku dla wywołań wokół hello jednocześnie w różnych krajach. Rekordy telefonu, które należą do tej kategorii są zapisywane toostorage do dalszej analizy.

## <a name="prerequisites"></a>Wymagania wstępne

W tym samouczku będzie symulować rozmowy telefonicznej danych przy użyciu aplikacji klienta, która generuje próbki rozmowy telefonicznej metadanych. Niektóre rekordy hello, które aplikacji hello tworzy wygląd fałszywych wywołania. 

Przed rozpoczęciem upewnij się, że masz następujące hello:

* Konto platformy Azure.
* Witaj zdarzenie wywołania generator aplikacji. Możesz uzyskać dostęp do tej pobierając hello [pliku TelcoGenerator.zip](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) z hello Microsoft Download Center. Rozpakuj pakiet do folderu na komputerze. Aby kod źródłowy hello toosee i aplikacji hello uruchamiania w debugerze, można pobrać kodu źródłowego aplikacji hello z [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >System Windows może blokować hello pobrany plik zip. Jeśli nie można rozpakować go, kliknij prawym przyciskiem myszy plik hello i wybierz **właściwości**. Jeśli widzisz hello komunikat "ten plik pochodzi z innego komputera i może być zablokowany toohelp ochrony tego komputera", wybierz hello **Odblokuj** opcji, a następnie kliknij przycisk **Zastosuj**.

Jeśli chcesz, aby wyniki hello tooexamine zadanie analizy przesyłania strumieniowego hello, należy również narzędzia do wyświetlania zawartości hello kontenera magazynu obiektów Blob Azure. Jeśli używasz programu Visual Studio, możesz użyć [Azure Tools dla programu Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) lub [programu Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Alternatywnie można zainstalować narzędzi autonomicznych, takich jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) lub [Eksploratora Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Utworzyć usługi Azure event hubs tooingest zdarzeń

tooanalyze strumień danych możesz *pozyskiwania* go na platformie Azure. Dane tooingest spotykaną metodą jest toouse [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), które pozwala obsługiwać miliony zdarzeń na sekundę, a następnie przetwarzania i przechowywania informacji o zdarzeniu hello. W tym samouczku tworzenia Centrum zdarzeń i mieć hello zdarzenie wywołania generator aplikacji wysyłania wywołania danych toothat Centrum zdarzeń. Aby uzyskać więcej informacji na temat usługi event hubs, zobacz hello [dokumentacji usługi Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Bardziej szczegółowe wersja tej procedury dla [tworzenie przestrzeni nazw usługi Event Hubs i Centrum zdarzeń za pomocą hello portalu Azure](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Tworzenie Centrum przestrzeń nazw i zdarzeń
W tej procedurze należy najpierw utworzyć przestrzeń nazw Centrum zdarzeń, a następnie dodaj namepsace toothat Centrum zdarzeń. Przestrzenie nazw Centrum zdarzeń są używane grupy toologically związane z wystąpień magistrali zdarzeń. 

1. Zaloguj się do hello portalu Azure i kliknij przycisk **nowy** > **Internetu rzeczy** > **Centrum zdarzeń**. 

2. W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw, takich jak `<yourname>-eh-ns-demo`. Można użyć dowolnej nazwy przestrzeni nazw hello, ale hello nazwa musi być prawidłowa dla danego adresu URL i między Azure musi być unikatowa. 
    
3. Wybierz subskrypcję i Utwórz lub wybierz grupę zasobów, a następnie kliknij przycisk **Utwórz**. 

    ![Tworzenie przestrzeni nazw Centrum zdarzeń](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Po zakończeniu przestrzeni nazw hello wdrażania można znaleźć przestrzeni nazw Centrum zdarzeń hello na liście zasobów platformy Azure. 

5. Kliknij hello nowej przestrzeni nazw, a w bloku przestrzeni nazw powitania kliknij  **+ &nbsp;Centrum zdarzeń**. 

    ![przycisk Dodaj Centrum zdarzeń Hello do tworzenia nowego Centrum zdarzeń ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Nazwa hello nowym Centrum zdarzeń `sa-eh-frauddetection-demo`. Można użyć innej nazwy. Jeśli to zrobisz, zanotuj, ponieważ potrzebna nazwa hello później. Nie trzeba tooset inne opcje dla Centrum zdarzeń powitania od razu.

    ![Blok do tworzenia nowego Centrum zdarzeń](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Kliknij przycisk **Utwórz**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Udziel Centrum zdarzeń toohello dostępu i pobrać ciągu połączenia

Aby proces może wysłać Centrum zdarzeń tooan danych, Centrum zdarzeń hello musi mieć zasadę, która umożliwia uzyskanie odpowiedniego dostępu. zasady dostępu Hello generuje ciąg połączenia, który zawiera informacje o autoryzacji.

1.  W bloku przestrzeni nazw zdarzeń powitania kliknij **usługi Event Hubs** a następnie kliknij nazwę hello nowe Centrum zdarzeń.

2.  W bloku Centrum zdarzeń hello, kliknij przycisk **zasady dostępu współużytkowanego** , a następnie kliknij przycisk  **+ &nbsp;Dodaj**.

    >[!NOTE]
    >Upewnij się, że pracujesz z Centrum zdarzeń hello, nie hello Centrum przestrzeni nazw zdarzenia.

3.  Dodaj zasady o nazwie `sa-policy-manage-demo` i **oświadczeń**, wybierz pozycję **Zarządzaj**.

    ![Blok do tworzenia nowych zasad dostępu do Centrum zdarzeń](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Kliknij przycisk **Utwórz**.

5.  Po wdrożeniu zasad powitania kliknij go hello liście zasady dostępu współdzielonego.

6.  Znajdź pole hello **klucz podstawowy ciąg połączenia** i kliknij przycisk hello kopiowania przycisku Dalej toohello parametry połączenia. 
    
    ![Kopiowanie klucza ciąg połączenia głównej hello hello zasady dostępu](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Wklej parametry połączenia hello w edytorze tekstu. Należy tego ciągu połączenia dla następnej sekcji hello, po wprowadzeniu niektórych tooit małych edycji.

    Parametry połączenia Hello wygląda następująco:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Powiadomienie, że parametry połączenia hello zawiera wiele par klucz wartość, oddzielając je średnikami: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, i `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Skonfigurować i uruchomić hello zdarzeń generator aplikacji

Przed rozpoczęciem powitalne TelcoGenerator aplikacji, możesz ją skonfigurować tak, aby wysyła Centrum zdarzeń toohello rekordów wywołania, które właśnie utworzony.

### <a name="configure-hello-telcogeneratorapp"></a>Skonfiguruj hello TelcoGeneratorapp

1.  W edytorze hello jest kopiowany hello parametry połączenia, zanotuj hello `EntityPath` wartość, a następnie usuń hello `EntityPath` pary (nie zapomnij tooremove hello średnika, przechwyceniem). 

2.  W folderze hello, gdzie można rozpakować pliku TelcoGenerator.zip hello Otwórz plik telcodatagen.exe.config hello w edytorze. (Istnieje więcej niż jednego pliku .config, dlatego należy po otwarciu prawo hello co.)

3.  W hello `<appSettings>` element, w tym:

    * Ustaw wartość hello hello `EventHubName` nazwy Centrum zdarzeń toohello klucza (czyli toohello wartość hello jednostki ścieżki).
    * Ustaw wartość hello hello `Microsoft.ServiceBus.ConnectionString` klucza toohello parametry połączenia. 

    Witaj `<appSettings>` sekcji będzie wyglądać hello poniższy przykład. (Dla uzyskania przejrzystości, możemy opakowana hello wierszy i usunąć niektóre znaki z tokenu autoryzacji hello.)

    ![Plik konfiguracji aplikacji TelcoGenerator przedstawiający hello zdarzenia koncentratora nazwy i parametry połączenia](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Zapisz plik hello. 

### <a name="start-hello-app"></a>Uruchamiają aplikację hello
1.  Otwórz okno polecenia i zmień folder toohello, w którym jest rozpakowane hello TelcoGenerator aplikacji.
2.  Wprowadź hello następujące polecenie:

        telcodatagen.exe 1000 .2 2

    Parametry Hello są: 

    * Liczba CDR na godzinę. 
    * Prawdopodobieństwo oszustwa karta SIM: Jak często jako procent wszystkich wywołań, aplikacja hello, powinny symulować fałszywych wywołania. wartość Hello.2 oznacza, że około 20% hello wywołania rekordy będą wyglądać fałszywe.
    * Czas trwania w godzinach. Witaj liczbę godzin, które hello aplikacji powinno być ono uruchomione. Można również zatrzymać aplikacji hello dowolnej chwili, naciskając klawisze Ctrl + C w wierszu polecenia hello.

    Po kilku sekundach uruchomieniu aplikacji hello wyświetlanie rekordy połączeń telefonicznych na ekranie powitania jako wysyła je toohello Centrum zdarzeń.

Niektóre pola klucza hello, które będą używane w tej aplikacji wykrywanie oszustw w czasie rzeczywistym są następujące hello:

|**Rekord**|**Definicja**|
|----------|--------------|
|`CallrecTime`|Godzina rozpoczęcia sygnatury czasowej Hello hello wywołania. |
|`SwitchNum`|Przełącznik telefonu Hello używany tooconnect hello wywołania. Na przykład przełączniki hello są ciągów reprezentujących hello kraj pochodzenia (USA, Chin, UK, Niemcy lub Australii). |
|`CallingNum`|numer telefonu Hello hello wywołującego. |
|`CallingIMSI`|Witaj międzynarodowej Mobile subskrybenta tożsamości IMSI. Jest to unikatowy identyfikator wywołującego hello hello. |
|`CalledNum`|numer telefonu Hello hello wywołania adresata. |
|`CalledIMSI`|Subskrybent międzynarodowy przenośnych tożsamość (firmy IMSI). Jest to unikatowy identyfikator hello hello wywołania odbiorcy. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Utwórz toomanage zadania Stream Analytics, przesyłanie strumieniowe danych

Teraz, gdy masz strumienia zdarzeń wywołania można skonfigurować zadania usługi analiza strumienia. zadanie Hello będzie odczytywać dane z Centrum zdarzeń hello ustawiony. 

### <a name="create-hello-job"></a>Utwórz zadanie hello 

1. W portalu Azure hello, kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.

2. Nazwa zadania hello `sa_frauddetection_job_demo`, określ subskrypcję, lokalizacji i grupy zasobów.

    Z dobrze tooplace hello zadania i hello Centrum zdarzeń w hello jest tym samym regionie, aby uzyskać najlepszą wydajność i dlatego nie zwracania tootransfer danych między regionami.

    ![Tworzenie nowego zadania usługi analiza strumienia](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Kliknij przycisk **Utwórz**.

    Utworzono zadanie Hello i hello portal Wyświetla szczegóły zadania. Nic nie jest jeszcze uruchomiona, ale — masz tooconfigure hello zadania, aby można było uruchomić.

### <a name="configure-job-input"></a>Skonfiguruj zadania w danych wejściowych

1. W pulpicie nawigacyjnym hello lub hello **wszystkie zasoby** bloku, Znajdź i wybierz hello `sa_frauddetection_job_demo` zadania usługi analiza strumienia. 
2. W hello **topologii zadania** sekcji hello bloku zadania Stream Analytics, kliknij przycisk hello **dane wejściowe** pole.

    ![Pole wprowadzania w topologii w bloku zadania przesyłania strumieniowego Analytics hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:

    * **Alias wejściowy**: Użyj nazwy hello `CallStream`. Użyj innej nazwy, aby je zapisać, ponieważ będzie on potrzebny później.
    * **Typ źródła**: Wybierz **strumienia danych**. (**Danych referencyjnych** odwołuje się toostatic wyszukiwania danych, które nie będą korzystać z tego samouczka.)
    * **Źródło**: Wybierz **Centrum zdarzeń**.
    * **Opcji importowania**: Wybierz **Użyj Centrum zdarzeń z bieżącej subskrypcji**. 
    * **Przestrzeń nazw magistrali usług**: Wybierz hello Centrum przestrzeni nazw zdarzenia utworzonego wcześniej (`<yourname>-eh-ns-demo`).
    * **Centrum zdarzeń**: Centrum zdarzeń hello wybierz utworzony wcześniej (`sa-eh-frauddetection-demo`).
    * **Nazwa zasad Centrum zdarzeń**: Wybierz zasady dostępu hello utworzonego wcześniej (`sa-policy-manage-demo`).

    ![Utwórz nowe dane wejściowe zadania przesyłania strumieniowego usługi analiza](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Kliknij przycisk **Utwórz**.

## <a name="create-queries-tootransform-real-time-data"></a>Tworzenie zapytań tootransform danych w czasie rzeczywistym

W tym momencie masz zadanie usługi Stream Analytics, skonfiguruj tooread przychodzącego strumienia danych. Witaj następnym krokiem jest toocreate transformację analizuje dane hello w czasie rzeczywistym. Można to zrobić, tworząc kwerendy. Analiza strumienia obsługuje prosty, deklaratywny model zapytań opisujący przekształceń do przetworzenia w czasie rzeczywistym. zapytania Hello używać języka przypominającego SQL, którego niektóre rozszerzenia toostream określonego analityka. 

Bardzo proste zapytanie po prostu może odczytać wszystkich danych przychodzących hello. Jednak często tworzyć zapytania, które wyglądają dla określonych danych lub w przypadku relacji w danych hello. W tej sekcji samouczka hello będzie tworzenie i testowanie kilka toolearn kwerendy na kilka sposobów, w których można przekształcać strumień wejściowy do analizy. 

tutaj tworzonych kwerend Hello wyświetli tylko hello przekształcone dane toohello ekranu. W dalszej części artykułu należy skonfigurować ujście danych wyjściowych i kwerendę, która zapisuje hello przekształcone dane toothat ujścia.

toolearn więcej informacji na temat języka hello, zobacz hello [Azure Stream Analytics zapytania Language Reference](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Pobierz przykładowe dane do testowania zapytań

Hello TelcoGenerator aplikacji wysyła Centrum zdarzeń toohello rekordów wywołania i zadania usługi Stream Analytics jest skonfigurowany tooread z Centrum zdarzeń hello. Można użyć zapytania tootest hello zadania toomake się upewnić, że jest poprawnie odczytywania. zbyt test kwerendy w hello konsoli platformy Azure, należy przykładowych danych. W ramach tego przewodnika będą Wyodrębnij przykładowych danych ze strumienia hello, która będzie dostępna w Centrum zdarzeń hello.

1. Upewnij się, aplikacja TelcoGenerator hello jest uruchomiona i tworzenie rekordów wywołania.
2. W portalu hello zwracać bloku zadanie analizy przesyłania strumieniowego toohello. (Jeśli został zamknięty hello bloku, wyszukaj `sa_frauddetection_job_demo` w hello **wszystkie zasoby** bloku.)
3. Kliknij przycisk hello **zapytania** pole. Azure zawiera dane wejściowe hello i dane wyjściowe, które są skonfigurowane dla zadania hello i pozwala utworzyć kwerendę, która umożliwia przekształcenie strumienia wejściowego hello podczas przesyłania danych wyjściowych toohello.
4. W hello **zapytania** bloku, kliknij przycisk Dalej toohello punktów hello `CallStream` danych wejściowych, a następnie wybierz **przykładowe dane z danych wejściowych**.

    ![Menu Opcje toouse przykładowych danych do hello wpis "Przykładowych danych z danych wejściowych" wybrane zadania przesyłania strumieniowego Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Spowoduje to otwarcie bloku, który pozwala określić, ile tooget dane przykładowe, zdefiniowanych pod względem jak długo tooread hello wejściowych strumienia.

5. Ustaw **minut** too3, a następnie kliknij przycisk **OK**. 
    
    ![Próbkowanie hello strumienia wejściowego, z "3 minuty" wybrane opcje.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure przykłady 3 minut, przez które danych ze strumienia wejściowego hello i powiadamia użytkownika, gdy będzie gotowy hello przykładowych danych. (Trwa to krótki czas). 

Hello przykładowe dane są tymczasowo przechowywane i jest dostępny, gdy masz hello okna kwerendy. Jeśli zamkniesz okno kwerendy hello hello przykładowe dane są usuwane i będziesz mieć toocreate nowy zestaw przykładowych danych. 

Alternatywnie, można uzyskać pliku JSON, który zawiera przykładowe dane w nim [z usługi GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), a następnie przekaż tego toouse pliku JSON jako dane przykładowe dla hello `CallStream` wejściowego. 

### <a name="test-using-a-pass-through-query"></a>Testowanie przy użyciu zapytania przekazującego

Jeśli chcesz tooarchive każde zdarzenie, można użyć tooread zapytania przekazującego wszystkie pola hello w ładunku hello hello zdarzenia.

1. W oknie zapytania hello wprowadź tego zapytania:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Podobnie jak w przypadku SQL, słowa kluczowe nie jest uwzględniana wielkość liter, a odstępem, nie ma znaczenia.

    W tym zapytaniu `CallStream` jest hello alias określony podczas tworzenia hello danych wejściowych. Jeśli używasz inny alias, należy użyć tej nazwy.

2. Kliknij przycisk **testu**.

    zadanie Stream Analytics Hello jest uruchamiana hello zapytania dla hello przykładowych danych i wyświetla dane wyjściowe hello u dołu okna hello hello. Oznacza to, że hello Centrum zdarzeń i zadanie analizy przesyłania strumieniowego hello są prawidłowo skonfigurowane. (Jak wspomniano, później należy utworzyć ujście danych wyjściowych tego hello zapytania można zapisywać danych.)

    ![Zadania usługi analiza strumienia wyjściowego, wyświetlanie 73 rekordów wygenerowany](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    Dokładna liczba rekordów wyświetlanych Hello będzie zależeć od liczbę rekordów zostały przechwycone w Twoim przykładzie 3 minuty.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Zmniejsz liczbę hello pola przy użyciu projekcji kolumny

W wielu przypadkach analizy nie potrzebuje wszystkich kolumn hello ze strumienia wejściowego hello. Możesz użyć tooproject zapytania, mniejszy zestaw zwrócony pól niż w hello zapytania przekazującego.

1. Zmień zapytanie hello w następujących toohello edytora kodu hello:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Kliknij przycisk **testu** ponownie. 

    ![Zadania Stream Analytics wyjściowego dla projekcji, wyświetlanie 25 rekordów wygenerowany](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Liczba przychodzących wywołuje według regionu: okno wirowania z agregacją

Załóżmy, że chcesz toocount hello liczba połączeń przychodzących na region. W strumieniowego przesyłania danych, należy tooperform funkcje agregujące, takie jak zliczanie, należy toosegment hello strumienia do jednostki danych czasowych (ponieważ sam strumień danych hello jest skutecznie nieskończone). Można to zrobić przy użyciu usługi analiza strumienia [funkcji okna](stream-analytics-window-functions.md). Możesz następnie pracować z danymi hello wewnątrz tego okna jako jednostka.

Dla tej transformacji sekwencja danych czasowych systemu Windows, które nie nakładają się na — każde okno będzie mieć odrębny zestaw danych, które można grupować i agregacji. Ten typ okna jest określony tooas *okno wirowania* . W ramach okno wirowania hello, możesz uzyskać liczbę przychodzących hello pogrupowane według `SwitchNum`, reprezentuje kraj hello pochodzenie hello wywołania. 

1. Zmień zapytanie hello w następujących toohello edytora kodu hello:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    To zapytanie używa hello `Timestamp By` — słowo kluczowe w hello `FROM` toospecify klauzuli pola sygnatury czasowej w hello wejściowych okno wirowania hello toodefine toouse strumienia. W takim przypadku okna hello dzieli dane hello segmentów przez hello `CallRecTime` w każdego rekordu. (Jeśli żadne pole nie zostanie określony, operacja okien hello używa czas hello każdego zdarzenia dociera hello Centrum zdarzeń. Zobacz sekcję "Godzina aplikacji Vs Godzina nadejścia" w [strumienia Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    obejmuje projekcji Hello `System.Timestamp`, która zwraca sygnatury czasowej do hello koniec każdego okna. 

    toospecify, które mają toouse okno wirowania, użyj hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) funkcji w hello `GROUP BY `klauzuli. W funkcji hello należy określić jednostkę czasu (dowolnym z dziennie tooa mikrosekund) i rozmiaru okna (liczbę jednostek). W tym przykładzie okno wirowania hello składa się z 5 sekund, tak liczba według kraju będzie uzyskać co 5 sekund, przez które wywołania.

2. Kliknij przycisk **testu** ponownie. W wynikach hello, zwróć uwagę, że sygnatury czasowe hello w obszarze **WindowEnd** w przyrostach 5 sekund.

    ![Zadania Stream Analytics dane wyjściowe do agregacji, wyświetlanie rekordów 13 wygenerowany](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Wykrywanie oszustw SIM przy użyciu samosprzężenie

Na przykład możemy Rozważ użycie fałszywych wywołania toobe, które pochodzą ze hello sam użytkownika, ale w różnych lokalizacjach w ciągu 5 sekund od siebie. Na przykład hello tego samego użytkownika nie legalnie wywoływania z hello Stanów Zjednoczonych oraz Australii na powitania tym samym czasie. 

toocheck dla tych przypadków, korzystając z własnym join hello przesyłanie strumieniowe danych toojoin hello strumienia tooitself oparte na powitania `CallRecTime` wartość. Następnie można sprawdzić dla wywołania rejestruje gdzie hello `CallingIMSI` wartość (hello pochodzących numer) jest hello takie same, ale hello `SwitchNum` wartość (kraj pochodzenia) nie jest hello takie same.

Użycie sprzężenia na danych przesyłanych strumieniowo, sprzężenia hello należy udostępnić niektóre limity jak daleko hello pasujących wierszy mogą być oddzielone w czasie. (Jak wspomniano wcześniej, hello przesyłanie strumieniowe danych jest skutecznie nieskończone). określono Hello zakresem czasu dla relacji hello wewnątrz hello `ON` klauzuli sprzężenia hello, przy użyciu hello `DATEDIFF` funkcji. W takim przypadku sprzężenia hello jest oparta na interwał 5 sekund, połączenie danych.

1. Zmień zapytanie hello w następujących toohello edytora kodu hello: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    To zapytanie jest podobna wszelkich sprzężenia SQL, z wyjątkiem hello `DATEDIFF` funkcja hello sprzężenia. To jest wersja `DATEDIFF` to tooStreaming określonego analityka i musi znajdować się w hello `ON...BETWEEN` klauzuli. Parametry Hello jest jednostka czasu (w sekundach w tym przykładzie) i aliasy hello dwóch źródeł hello w celu utworzenia sprzężenia hello. (Ta różni się od hello standardowe SQL `DATEDIFF` funkcji.) 

    Hello `WHERE` klauzula zawiera warunek hello flagi wywołania fałszywych hello: hello przełączniki źródłowego nie są hello takie same. 

2. Kliknij przycisk **testu** ponownie. 

    ![Dane wyjściowe samosprzężenie, wyświetlony 6 rekordy generowane zadania Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Kliknij pozycję **Zapisz**. Spowoduje to zapisanie hello samosprzężenie zapytania jako część zadania przesyłania strumieniowego Analytics hello. (Nie zostanie on zapisany hello przykładowe dane).

    ![Zapisz zadanie usługi analiza strumienia](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Utworzenie danych wyjściowych zbiornika toostore przekształcone dane

Zdefiniowany przez użytkownika strumienia zdarzeń, zdarzenia wejściowe tooingest Centrum zdarzeń i tooperform zapytania transformację za pośrednictwem hello strumienia. ostatni krok Hello jest toodefine ujście danych wyjściowych zadania hello — to znaczy hello toowrite miejsce przekształcone strumienia do. 

Wiele zasobów można używać jako dane wyjściowe wychwytywanie — bazy danych programu SQL Server, Magazyn tabel, Data Lake storage, usługi Power BI i nawet innej Centrum zdarzeń. W tym samouczku przedstawiono tworzenie hello strumienia tooAzure magazynu obiektów Blob, który jest typowy wyborem do zbierania informacji o zdarzeniach dotyczących późniejszej analizy, ponieważ bierze pod uwagę danych bez struktury.

Jeśli masz istniejące konto magazynu obiektów blob, można użyć, który. W tym samouczku pokażemy ci jak toocreate nowego magazynu konta tylko do celów tego samouczka.

### <a name="create-an-azure-blob-storage-account"></a>Tworzenie konta usługi Magazyn obiektów Blob Azure

1. W portalu Azure hello zwracać bloku zadanie analizy przesyłania strumieniowego toohello. (Jeśli został zamknięty hello bloku, wyszukaj `sa_frauddetection_job_demo` w hello **wszystkie zasoby** bloku.)
2. W hello **topologii zadania** kliknij hello **dane wyjściowe** pole. 
3. W hello **dane wyjściowe** bloku, kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:

    * **Alias wyjściowy**: Użyj nazwy hello `CallStream-FraudulentCalls`. 
    * **Obiekt sink**: Wybierz **magazynu obiektów Blob**.
    * **Opcje importowania**: Wybierz **Użyj magazynu obiektów blob z bieżącej subskrypcji**.
    * **Konto magazynu**. Wybierz **Utwórz nowe konto magazynu.**
    * **Konto magazynu** (drugie pole). Wprowadź `YOURNAMEsademo`, gdzie `YOURNAME` jest nazwa użytkownika lub inny unikatowy ciąg. Nazwa Hello można użyć tylko małe litery i cyfry, i między Azure musi być unikatowa. 
    * **Kontener**. Wprowadź `sa-fraudulentcalls-demo`.
    Nazwa konta magazynu Hello i nazwa kontenera są używane razem tooprovide identyfikator URI dla magazynu obiektów blob hello w następujący sposób: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Blok "Nowe dane wyjściowe" zadania usługi analiza strumienia](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Kliknij przycisk **Utwórz**. 

    Azure tworzy konto magazynu hello i automatycznie generuje klucz. 

5. Zamknij hello **dane wyjściowe** bloku. 

## <a name="start-hello-streaming-analytics-job"></a>Uruchom zadanie analizy przesyłania strumieniowego hello

zadanie Hello jest teraz skonfigurowany. Zostały określone dane wejściowe (hello Centrum zdarzeń), transformacji (hello toolook zapytania dla fałszywych wywołań) i danych wyjściowych (magazynu obiektów blob). Można teraz uruchomić zadania hello. 

1. Upewnij się, że aplikacja TelcoGenerator hello jest uruchomiona.

2. W bloku zadania powitania kliknij **Start**.

    ![Uruchom zadanie usługi Stream Analytics hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. W hello **rozpoczęcia zadania** bloku dla danych wyjściowych czas uruchomienia zadania, wybierz opcję **teraz**. 

4. Kliknij przycisk **Start**. 

    ![Blok "Uruchomić zadanie" hello zadania usługi analiza strumienia](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure sygnalizuje hello zadań została uruchomiona, a następnie w bloku zadania hello, zostanie wyświetlony stan hello **systemem**.

    ![Stan zadania Stream Analytics, przedstawiający "Uruchomiona"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Sprawdź hello przekształcenia danych

Masz teraz pełną zadanie analizy przesyłania strumieniowego. zadanie Hello jest badanie strumienia metadanych rozmowy telefonicznej, wyszukiwanie fałszywych rozmowy telefoniczne w czasie rzeczywistym i zapisywania informacji o tych toostorage fałszywych wywołania. 

toocomplete tego samouczka można toolook hello danych są przechwytywane przez zadanie analizy przesyłania strumieniowego hello. dane Hello jest zapisywana tooAzure magazynu blogu w fragmentów (pliki). Można użyć dowolnego narzędzia, które odczytuje magazynu obiektów Blob Azure. Jak wspomniano w sekcji wymagania wstępne hello, można użyć rozszerzeń Azure w programie Visual Studio lub skorzystać z narzędzia, takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) lub [Eksploratora Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

Po sprawdzeniu hello zawartości pliku w magazynie obiektów blob może wyglądać hello następujące czynności:

![Magazyn obiektów blob platformy Azure z analizy strumienia wyjściowego](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Mamy dodatkowe artykuły, które nadal ze scenariuszem wykrywanie oszustw hello, które korzystają z zasobów hello, które zostały utworzone w tym samouczku. Jeśli chcesz toocontinue, zobacz sugestie hello w obszarze **następne kroki** później.

Jednak jeśli wszystko będzie gotowe, a nie ma potrzeby hello zasoby, które zostały utworzone, można usunąć je, aby nie wiąże się z opłatami Azure niepotrzebne. W takim przypadku zaleca się, że hello następujące:

1. Zatrzymaj zadanie analizy przesyłania strumieniowego hello. W hello **zadania** bloku, kliknij przycisk **zatrzymać** u góry hello.
2. Zatrzymać hello Telco Generator aplikacji. W oknie polecenia hello pierwotnego aplikacji hello naciśnij klawisze Ctrl + C.
3. Jeśli utworzono nowe konto magazynu obiektów blob tylko do celów tego samouczka, należy ją usunąć. 
4. Usuń hello zadanie analizy przesyłania strumieniowego.
5. Usuń hello Centrum zdarzeń.
6. Usuń hello przestrzeni nazw z Centrum zdarzeń.

## <a name="get-support"></a>Uzyskiwanie pomocy technicznej

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki

W tym samouczku można kontynuować hello następujące artykuły:

* [Strumienia analizy i usługi Power BI: pulpitu nawigacyjnego analytics w czasie rzeczywistym do strumieniowego przesyłania danych](stream-analytics-power-bi-dashboard.md). W tym artykule opisano, jak hello toosend TelCo dane wyjściowe hello analiza strumienia zadania tooPower analizy Biznesowej w czasie rzeczywistym wizualizacji i analizy.
* [Jak toostore dane z usługi Azure Stream Analytics w pamięci podręcznej Redis Azure za pomocą usługi Azure Functions](stream-analytics-functions-redis.md). W tym artykule opisano, jak toowrite usługi Azure Functions toouse fałszywych wywołuje pamięci podręcznej Azure Redis tooan za pośrednictwem kolejki usługi Service Bus.

Aby uzyskać więcej informacji na temat usługi Stream Analytics ogólnie rzecz biorąc, wypróbuj następujące artykuły:

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
