---
title: "aaaBuild rozwiązania IoT przy użyciu usługi Stream Analytics | Dokumentacja firmy Microsoft"
description: "Pierwsze kroki samouczka dotyczącego hello rozwiązania IoT analizy strumienia scenariusza budki"
keywords: "rozwiązania iot, funkcje okna"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Tworzenie rozwiązania IoT przy użyciu usługi analiza strumienia
## <a name="introduction"></a>Wprowadzenie
W tym samouczku przedstawiono sposób toouse Azure Stream Analytics tooget w czasie rzeczywistym wgląd w dane. Deweloperzy mogą łatwo łączyć strumienie danych, takich jak kliknij strumieni, dzienników i zdarzenia generowane przez urządzenie, rekordy historyczne lub odwołanie do danych tooderive biznesowych. Jako usługa obliczeń strumienia w pełni zarządzana, w czasie rzeczywistym, która jest hostowana na platformie Microsoft Azure Azure Stream Analytics zawiera wbudowane odporności, małe opóźnienia i skalowalność tooget czasu i uruchomiona w minutach.

Po ukończeniu tego samouczka, będą mieć możliwość:

* Zapoznaj się z portalu usługi Azure Stream Analytics hello.
* Konfigurowanie i wdrażanie zadanie przesyłania strumieniowego.
* Zwrócone rzeczywistych problemów i ich rozwiązanie przy użyciu języka zapytań usługi Stream Analytics hello.
* Tworzenie strumienia rozwiązania dla klientów za pomocą usługi Stream Analytics bez obaw.
* Użyj hello monitorowanie i rejestrowanie środowisko tootroubleshoot problemów.

## <a name="prerequisites"></a>Wymagania wstępne
Można będzie konieczne hello następujące wymagania wstępne toocomplete tego samouczka:

* Witaj najnowszą wersję [programu Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017 r 2015 lub hello wolnego [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* [Subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
* Uprawnienia administracyjne na komputerze hello
* Pobieranie [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) z witryny Microsoft Download Center hello
* Opcjonalnie: Źródła kodu dla generatora zdarzeń TollApp hello w [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Wprowadzenie do scenariusza: "tekst Hello, przez!"
Stacja przez jest zjawiskiem wspólnej. Wystąpią ich na wielu trasy szybkiego ruchu, mostki i tunele między hello world. Każda stacja przez ma wiele kabiny przez. Na ręczne kabiny zatrzymaniu toopay hello przez tooan attendant. Na automatyczne kabiny czujnik u góry każdego stoisku skanuje RFID karta szyby umieszczone toohello Twojego pojazdów przy przesuwaniu stoisku przez hello. Jest łatwy toovisualize fragment hello pojazdów przez te stacje przez jako strumień zdarzeń, w którym interesujące operacje mogą być wykonywane.

![Obraz samochodów na kabiny przez](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Dane przychodzące
W tym samouczku współpracuje z dwóch strumieni danych. Czujniki zainstalowany na wejściu hello i zakończenia hello przez stacje tworzy strumień pierwszy hello. strumień drugi Hello jest statyczny wyszukiwania zestawu danych, który zawiera dane rejestracji pojazdów.

### <a name="entry-data-stream"></a>Wpis strumienia danych
strumień danych Hello wpis zawiera informacje o samochodów, wejście przez stacje.

| TollID | EntryTime | LicensePlate | Stan | Wprowadź | Model | VehicleType | VehicleWeight | Przez | Tag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |IERZ |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |IERZ |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CRP 1007 |NJ |Toyota |4 x 4 |1 |0 |6 |321987654 |

Poniżej przedstawiono krótki opis kolumn hello:

| Kolumna | Opis |
| --- | --- |
| TollID |Hello przez stoisku identyfikator, który unikatowo identyfikuje stoisku przez |
| EntryTime |Witaj Data i godzina wpisu hello vehicle toohello przez stoisku w formacie UTC |
| LicensePlate |numer rejestracyjny Hello pojazdów hello |
| Stan |Stan w Stanach Zjednoczonych |
| Wprowadź |Witaj producenta samochodów hello |
| Model |numer modelu Hello hello samochodów |
| VehicleType |1 dla samochodów osobowych lub 2 dla pojazdów |
| WeightType |Vehicle wagi w tonach; 0 dla pojazdów pasażerów |
| Przez |Witaj przez wartość w USD |
| Tag |Witaj e-Tag na powitania samochodów, który zautomatyzuje payment; puste w przypadku, gdy płatności hello została wykonana ręcznie |

### <a name="exit-data-stream"></a>Strumień danych zakończenia
strumień danych zakończenia Hello zawiera informacje o samochodów, pozostawiając hello przez stacji.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |BNJ 1007 |
| 2 |2014-09-10T12:07:00.0000000Z |CRP 1007 |

Poniżej przedstawiono krótki opis kolumn hello:

| Kolumna | Opis |
| --- | --- |
| TollID |Hello przez stoisku identyfikator, który unikatowo identyfikuje stoisku przez |
| ExitTime |Hello Data i godzina zakończenia hello vehicle z stoisku przez w formacie UTC |
| LicensePlate |numer rejestracyjny Hello pojazdów hello |

### <a name="commercial-vehicle-registration-data"></a>Dane rejestracji pojazdów użytkowych
Witaj samouczku statyczna migawka bazy danych rejestracji pojazdów użytkowych.

| LicensePlate | RegistrationId | Ważność |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| WYKONAJ KOPIĘ 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Poniżej przedstawiono krótki opis kolumn hello:

| Kolumna | Opis |
| --- | --- |
| LicensePlate |numer rejestracyjny Hello pojazdów hello |
| RegistrationId |Identyfikator rejestracji Hello vehicle |
| Ważność |Stan rejestracji hello vehicle Hello: 0, jeśli rejestracji pojazdów jest aktywny, 1, jeśli wygaśnięcia rejestracji |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Konfigurowanie środowiska powitania dla usługi Azure Stream Analytics
toocomplete tego samouczka, musisz mieć subskrypcję Microsoft Azure. Firma Microsoft oferuje bezpłatna wersja próbna usług Microsoft Azure.

Jeśli nie masz konta platformy Azure, możesz [żądania bezpłatną wersję próbną](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign dla bezpłatnej wersji próbnej, należy urządzenia przenośnego, które mogą odbierać wiadomości SMS oraz ważnej karty kredytowej.
> 
> 

Upewnij się, że toofollow hello kroki opisane w sekcji "Wyczyść konta platformy Azure" hello na końcu hello w tym artykule tak, aby można było wprowadzać hello najlepsze stosowania środków platformy Azure.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Udostępnianie zasobów platformy Azure wymagane przez samouczek hello
Ten samouczek wymaga dwóch tooreceive centra zdarzeń *wpis* i *zakończyć* strumieni danych. Baza danych SQL Azure generuje wyniki hello hello zadania usługi analiza strumienia. Usługa Azure Storage przechowuje dane odwołanie rejestracji pojazdów.

Używając hello Setup.ps1 skryptu w folderze TollApp hello na GitHub toocreate wszystkich wymaganych zasobów. W hello odsetek czasu firma Microsoft zaleca, uruchom go. Aby uzyskać więcej informacji na temat sposobu tooconfigure tych zasobów hello portalu Azure, zobacz toolearn toohello dodatku "Konfigurowanie samouczek zasobów w portalu Azure".

Pobierz i Zapisz obsługi hello [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) folderów i plików.

Otwórz **Microsoft Azure PowerShell** okna *jako administrator*. Jeśli nie masz jeszcze programu Azure PowerShell, postępuj zgodnie z instrukcjami hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall go.

Ponieważ system Windows blokuje automatycznie .ps1, dll i plików .exe, należy zasady wykonywania hello tooset, przed uruchomieniem skryptu hello. Upewnij się, że okno programu Azure PowerShell hello jest uruchomione *jako administrator*. Uruchom **Set-ExecutionPolicy unrestricted**. Po wyświetleniu monitu wpisz **Y**.

![Zrzut ekranu przedstawiający "Set-ExecutionPolicy unrestricted" uruchomione w oknie programu Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Uruchom **Get-ExecutionPolicy** toomake się upewnić, że polecenie hello działał.

![Zrzut ekranu przedstawiający "Get-ExecutionPolicy" uruchomione w oknie programu Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Przejdź toohello katalogu, który ma hello skryptów i generator aplikacji.

![Zrzut ekranu przedstawiający "cd .\TollApp\TollApp" uruchomione w oknie programu PowerShell Azure hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Typ **.\\ Setup.ps1** tooset konto platformy Azure, utworzyć i skonfigurować wszystkich wymaganych zasobów i uruchomić toogenerate zdarzenia. skrypt Hello losowo wybiera region toocreate zasobów. tooexplicitly Określ region, można przekazać hello **-lokalizacji** parametru jak hello poniższy przykład:

**. \\Setup.ps1 — lokalizacja "Środkowe stany USA"**

![Zrzut ekranu przedstawiający stronę hello Azure logowania](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

skrypt Hello otwiera hello **logowania** strony platformy Microsoft Azure. Wprowadź poświadczenia konta.

> [!NOTE]
> Jeśli konto ma dostęp toomultiple subskrypcji, będzie Nazwa subskrypcji hello zadawane tooenter mają toouse samouczek hello.
> 
> 

Witaj skryptu może zająć kilka minut toorun. Po jej zakończeniu, dane wyjściowe hello powinien wyglądać hello następującego zrzutu ekranu.

![Zrzut ekranu przedstawiający dane wyjściowe skryptu hello hello okno programu Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Widoczne będzie także innego okna, które jest podobne toohello następującego zrzutu ekranu. Ta aplikacja jest wysyłanie zdarzeń tooAzure Event Hubs, co jest wymagane toorun hello samouczka. Tak nie zatrzymania aplikacji hello lub zamknąć to okno, do momentu zakończenia hello samouczka.

![Zrzut ekranu przedstawiający "Wysyłanie zdarzeń centrum danych"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Użytkownik powinien być stanie toosee zasobów w portalu Azure teraz. Przejdź za<https://portal.azure.com>i zaloguj się przy użyciu poświadczeń konta. Należy pamiętać, obecnie niektóre funkcje wykorzystuje hello klasycznego portalu. Te kroki będzie widoczna.

### <a name="azure-event-hubs"></a>Azure Event Hubs
W portalu Azure hello, kliknij przycisk **więcej usług** na powitania dolnej części okienka po lewej stronie zarządzania hello. Typ **usługi Event hubs** w hello polu i kliknij przycisk **usługi Event hubs**. Spowoduje to uruchomienie nowej hello toodisplay okna przeglądarki **usługi SERVICE BUS** obszar hello **klasyczny portal**. Tutaj można zobaczyć hello Centrum zdarzeń utworzonych przez hello Setup.ps1 skryptu.

![Service Bus](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Kliknij przycisk hello, który rozpoczyna się od *tolldata*. Kliknij przycisk hello **usługi EVENT HUBS** kartę. Zobaczysz dwa elementy Hub zdarzenia o nazwie *wpis* i *zakończyć* utworzone w tej przestrzeni nazw.

![Karta centra zdarzeń w portalu klasycznym hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Kontener magazynu Azure
1. Przejdź wstecz kartę toohello w przeglądarce otwórz tooAzure portalu. Kliknij przycisk **MAGAZYNU** na powitania po lewej stronie powitania toosee portalu Azure hello Azure Storage kontenera, który jest używany w samouczku hello.
   
    ![Element menu magazynu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Kliknij przycisk hello jedną rozpoczynających się od *tolldata*. Kliknij przycisk hello **kontenery** kartę toosee hello utworzyć kontener.
   
    ![Karta kontenery w hello portalu Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Kliknij przycisk hello **tolldata** hello toosee kontenera przekazać pliku JSON, który zawiera dane rejestracji pojazdów.
   
    ![Zrzut ekranu przedstawiający plik registration.json hello w kontenerze hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Usługa Azure SQL Database
1. Przejdź wstecz toohello portalu Azure na pierwszej karcie hello, która została otwarta w przeglądarce hello. Kliknij przycisk **baz danych SQL** na powitania po lewej stronie powitania toosee portalu Azure hello bazy danych SQL, który będzie używany w samouczku hello, a następnie kliknij przycisk **tolldatadb**.
   
    ![Zrzut ekranu przedstawiający hello utworzył bazę danych SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Nazwa serwera hello kopiowania bez hello numer portu (*servername*. database.windows.net, na przykład).
    ![Zrzut ekranu przedstawiający hello utworzone bazy danych z bazy danych SQL.](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Połącz toohello bazy danych z programu Visual Studio
Użyj wyników zapytania tooaccess programu Visual Studio w danych wyjściowych hello w bazie danych.

Połączenie bazy danych SQL toohello (hello docelowy) z programu Visual Studio:

1. Otwórz program Visual Studio, a następnie kliknij przycisk **narzędzia** > **połączyć tooDatabase**.
2. Jeśli pojawi się monit, kliknij przycisk **programu Microsoft SQL Server** jako źródła danych.
   
    ![Okno dialogowe Zmienianie źródła danych](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. W hello **nazwy serwera** pól, Wklej nazwę hello, skopiowany z portalu Azure hello w poprzedniej sekcji hello (to znaczy *servername*. database.windows.net).
4. Kliknij przycisk **używać uwierzytelniania programu SQL Server**.
5. Wprowadź **tolladmin** w hello **nazwy użytkownika** pola i **123toll!** w hello **hasło** pola.
6. Kliknij przycisk **wybierz lub wprowadź nazwę bazy danych**i wybierz **TollDataDB** jako hello bazy danych.
   
    ![Dodaj połączenie — okno dialogowe](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Kliknij przycisk **OK**.
8. Otwórz Eksploratora serwera.
   
    ![Eksplorator serwera](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Zobacz cztery tabele w bazie danych TollDataDB hello.
   
    ![Tabele w bazie danych TollDataDB hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Generator zdarzeń: TollApp przykładowy projekt
zdarzenia toosend jest automatycznie uruchamiana, Hello skrypt programu PowerShell przy użyciu hello TollApp przykładowej aplikacji programu. Tooperform nie wymagają żadnych dodatkowych czynności.

Jednak jeśli interesuje Cię szczegóły implementacji, można znaleźć kodu źródłowego hello hello TollApp aplikacji w usłudze GitHub [przykłady/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Zrzut ekranu przedstawiający przykładowy kod wyświetlany w programie Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics
1. W portalu Azure hello kliknij przycisk hello zielony znak plus w hello lewego górnego rogu toocreate strony hello nowe zadanie usługi Stream Analytics. Wybierz **analizy i analiza** , a następnie kliknij przycisk **zadanie usługi Stream Analytics**.
   
    ![Przycisk Nowy](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Podaj nazwę zadania, sprawdzanie poprawności subskrypcji hello poprawić, a następnie utworzyć nową grupę zasobów w hello tego samego regionu hello magazynu Centrum zdarzeń (wartość domyślna to południowo-środkowe stany hello skryptu).
3. Kliknij przycisk **toodashboard numeru Pin** , a następnie **Utwórz** u dołu hello hello strony.
   
    ![Utwórz opcję zadania usługi analiza strumienia](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Definiowanie źródeł dla wejścia
1. Hello zadania spowoduje utworzenie i otwarcie strony zadania hello. Lub kliknięciu hello utworzone zadanie analizy na powitania pulpitu nawigacyjnego portalu.

2. Kliknij przycisk hello **dane wejściowe** karcie toodefine hello źródła danych.
   
    ![Karta dane wejściowe Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Kliknij przycisk **dodać dane wejściowe**.
   
    ![Witaj, dodaj opcję dane wejściowe](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Wprowadź **EntryStream** jako **ALIAS wejściowy**.
5. Typ źródła jest **strumienia danych**
6. Źródło jest **Centrum zdarzeń**.
7. **Przestrzeń nazw magistrali usług** powinna być hello TollData jeden w hello listy rozwijanej.
8. **Nazwa Centrum zdarzeń** powinna być ustawiona zbyt**wpis**.
9. **Nazwa zasad Centrum zdarzeń*jest **RootManageSharedAccessKey** (hello wartość domyślna).
10. Wybierz **JSON** dla **FORMAT SERIALIZACJI zdarzeń** i **UTF8** dla **KODOWANIE**.
   
    Ustawienia będą wyglądać:
   
    ![Ustawienia Centrum zdarzeń](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Kliknij przycisk **Utwórz** u dołu hello hello strony toofinish hello kreatora.
    
    Teraz, po utworzeniu hello wejścia strumienia zastosują hello samego kroki toocreate hello zakończenia strumienia. Należy się, że wartości tooenter na powitania po zrzut ekranu.
    
    ![Ustawienia dla hello zakończenia strumienia](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Zdefiniowano dwóch strumieni wejściowych:
    
    ![Zdefiniowany w portalu Azure hello strumienie wejściowe](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Następnie można dodać wejściowych danych referencyjnych hello pliku obiektu blob, który zawiera dane rejestracji samochodu.
11. Kliknij przycisk **dodać**, a następnie wykonaj hello sam proces hello strumienia w danych wejściowych, ale wybierz **danych referencyjnych** zamiast **strumienia danych** i hello **Alias wejściowy**  jest **rejestracji**.

12. Konto magazynu, który rozpoczyna się od **tolldata**. Nazwa kontenera Hello powinna być **tolldata**i hello **wzorzec ścieżki** powinien być **registration.json**. Nazwa pliku jest rozróżniana wielkość liter i powinna być **małych**.
    
    ![Blog dotyczący miejsca do magazynowania](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Kliknij przycisk **Utwórz** toofinish hello kreatora.

Teraz wszystkie dane wejściowe są zdefiniowane.

## <a name="define-output"></a>Definiowanie danych wyjściowych
1. W okienku omówienie zadania usługi analiza strumienia hello wybierz **dane wyjściowe**.
   
    ![Karta danych wyjściowych Hello i opcję "Dodaj wyjścia"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Kliknij pozycję **Dodaj**.
3. Zestaw hello **alias wyjściowy** too'output ", a następnie **Sink** za**bazy danych SQL**.
3. Wybierz hello nazwę serwera, który został użyty w hello sekcji "Connect tooDatabase z programu Visual Studio" hello artykułu. Nazwa bazy danych Hello jest **TollDataDB**.
4. Wprowadź **tolladmin** w hello **USERNAME** pola **123toll!** w hello **hasło** pola i **TollDataRefJoin** w hello **tabeli** pola.
   
    ![Ustawienia bazy danych SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Kliknij przycisk **Utwórz**.

## <a name="azure-stream-analytics-query"></a>Azure Stream analytics zapytania
Witaj **zapytania** karta zawiera zapytanie SQL, że transformacje hello przychodzących danych.

![Karta Zapytanie toohello dodane zapytania](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

W tym samouczku prób tooanswer kilka pytania biznesowe dotyczące danych tootoll oraz elementów składowych Stream Analytics zapytań może być używane w tooprovide Azure Stream Analytics odpowiednich odpowiedzi.

Przed rozpoczęciem pierwszego zadania Stream Analytics, Przyjrzyjmy się kilka scenariuszy i hello składnia zapytania.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Wprowadzenie tooAzure język zapytań usługi Stream Analytics
- - -
Załóżmy, że należy toocount hello liczba pojazdów, które wprowadź stoisku przez. Ponieważ jest to stały strumień zdarzeń, masz toodefine "okresu czasu." Zmodyfikujmy toobe pytanie hello "ilu pojazdów wprowadź stoisku przez co trzy minuty?". Jest to często określonego tooas hello wirowania liczby.

Przyjrzyjmy się hello Azure Stream Analytics kwerendę, która zawiera odpowiedzi na to pytanie:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Jak widać, usługi Azure Stream Analytics korzysta z języka kwerend, takiego jak SQL i dodaje kilka rozszerzeń toospecify związanych z czasem aspektów hello zapytania.

Aby uzyskać więcej informacji, przeczytaj o [zarządzanie czasem](https://msdn.microsoft.com/library/azure/mt582045.aspx) i [Okienkową](https://msdn.microsoft.com/library/azure/dn835019.aspx) konstrukcji używanych w zapytaniu hello w witrynie MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Testowanie zapytań usługi Azure Stream Analytics
Obecnie masz napisanych pierwszego zapytania usługi Azure Stream Analytics, jest tootest czas go przy użyciu przykładowych plików danych znajdujących się w folderze TollApp w hello ze ścieżką:

**.. \\TollApp\\TollApp\\danych**

Ten folder zawiera hello następujące pliki:

* Entry.JSON
* Exit.JSON
* Registration.JSON

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Pytanie 1: Liczba pojazdów stoisku przez
1. Otwórz hello portalu Azure i zadania usługi analiza strumienia Azure Przejdź tooyour utworzony. Kliknij przycisk hello **zapytania** karcie i Wklej zapytanie z hello w poprzedniej sekcji.

2. toovalidate tego zapytania dotyczącego przykładowych danych, przekazywanie danych hello do hello EntryStream danych wejściowych, klikając hello... symboli i wybierając **przekazać dane przykładowe z pliku**.

    ![Zrzut ekranu przedstawiający hello Entry.json pliku](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. W okienku hello, wyświetlonym hello wybierz plik (Entry.json) na komputerze lokalnym i kliknij przycisk **OK**. Witaj **testu** ikona teraz oświetlenia i być aktywne.
   
    ![Zrzut ekranu przedstawiający hello Entry.json pliku](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Sprawdź, czy dane wyjściowe hello zapytania hello jest zgodnie z oczekiwaniami:
   
    ![Wyniki testu hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Pytanie 2: Całkowity czas raport dla każdego toopass samochodu za pośrednictwem stoisku przez hello
Hello Średni czas, które są wymagane dla toopass samochodu, za pośrednictwem przez hello pomaga tooassess hello wydajności procesu hello i hello obsługi klienta.

Łączny czas hello toofind należy toojoin hello EntryTime strumienia hello ExitTime strumienia. Dołączy strumieni hello TollId i LicencePlate kolumn. Witaj **JOIN** operator wymaga toospecify swobodę danych czasowych opisujące czas dopuszczalne hello różnica między hello przyłączone do zdarzenia. Użyjesz **DATEDIFF** funkcji toospecify, że zdarzenia nie powinny być dłużej niż 15 minut od siebie. Stosuje się również hello **DATEDIFF** tooexit funkcji i wprowadzenia razy toocompute hello rzeczywistą wartość czasu spędzanego samochodu w hello numer stacji. Należy zwrócić uwagę hello różnica użycia hello **DATEDIFF** gdy jest używana w **wybierz** instrukcji zamiast **JOIN** warunku.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest to zapytanie kwerendy hello aktualizacji na powitania **zapytania** hello zadania. Dodaj plik testu powitania dla **ExitStream** podobnie jak **EntryStream** wprowadzono powyżej.
   
2. Kliknij przycisk **testu**.

3. Wybierz hello pole wyboru tootest hello zapytań i widoków hello danych wyjściowych:
   
    ![Dane wyjściowe hello testu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Pytanie 3: Raport wszystkich pojazdów użytkowych z wygaśnięcie rejestracji
Usługa Azure Stream Analytics za pomocą statycznego migawki danych toojoin strumieni danych czasowych. toodemonstrate tej możliwości, użyj hello następujące przykładowe zapytania.

Jeśli pojazdów użytkowych jest zarejestrowany w systemie firmy przez hello, można przekazać za pośrednictwem stoisku przez hello bez zatrzymania inspekcji. Użyjesz tooidentify tabeli odnośników rejestracji pojazdów użytkowych wszystkich pojazdów handlowych, które wygasły rejestracji.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest zapytania przy użyciu danych referencyjnych należy toodefine źródło danych wejściowych danych referencyjnych hello, która została już utworzona.

tootest to zapytanie, Wklej zapytanie hello na powitania **zapytania** , kliknij pozycję **testu**i określ hello dwóch źródeł danych wejściowych i rejestracji hello przykładowe dane i kliknij przycisk **testu**.  
   
![Dane wyjściowe hello testu](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Uruchom zadanie usługi Stream Analytics hello
Teraz nadszedł czas toofinish hello konfiguracji, a następnie rozpocznij hello zadania. Zapisz zapytanie hello z 3 zapytania, które spowoduje utworzenie danych wyjściowych, że dopasowań hello schematu hello **TollDataRefJoin** tabeli wyników.

Zadanie Przejdź toohello **pulpitu NAWIGACYJNEGO**i kliknij przycisk **START**.

![Zrzut ekranu przedstawiający przycisk Start hello hello zadania w pulpicie nawigacyjnym](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Okno dialogowe hello otwiera, zmień hello **START dane wyjściowe** czasu za**czasu niestandardowe**. Zmień godzinę tooone godzina hello przed hello bieżący czas. Ta zmiana zapewnia, że wszystkie zdarzenia z Centrum zdarzeń hello są przetwarzane od czasu uruchomienia zdarzenia hello toogenerate na początku hello hello samouczka. Teraz kliknij hello **Start** przycisk toostart hello zadania.

![Wybór czasu niestandardowych](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Rozpoczynanie zadania hello może potrwać kilka minut. Stan hello na powitania strony najwyższego poziomu widoczny dla usługi Stream Analytics.

![Zrzut ekranu przedstawiający stan hello hello zadania](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Sprawdź wyniki w programie Visual Studio
1. Otwórz Eksploratora serwera w usłudze Visual Studio, a następnie kliknij prawym przyciskiem myszy hello **TollDataRefJoin** tabeli.
2. Kliknij przycisk **Pokaż dane tabeli** toosee hello dane wyjściowe z zadania.
   
    ![Wybór "Pokaż tabeli danych" w Eksploratorze serwera](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Skalowanie usługi Azure Stream Analytics zadania
Usługa Azure Stream Analytics zaprojektowano tooelastically skalować, aby mogły obsługiwać dużą ilość danych. można użyć Hello Azure Stream Analytics query **PARTITION BY** klauzuli tootell hello system, który w tym kroku zostanie skalowanie w poziomie. **PartitionId** jest specjalne kolumny, która hello systemu dodaje identyfikator partycji: hello toomatch hello danych wejściowych (Centrum zdarzeń).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Zatrzymaj hello bieżące zadanie, zapytania hello aktualizacji w hello **zapytania** kartę i otwórz hello **ustawienia** narzędzi hello zadania w pulpicie nawigacyjnym. Kliknij przycisk **skali**.
   
    **JEDNOSTKI przesyłania STRUMIENIOWEGO** zdefiniuj może odbierać hello ilości mocy obliczeniowej, który hello zadania.
2. Zmień hello listy rozwijanej z 1 z 6.
   
    ![Zrzut ekranu przedstawiający wybranie 6 jednostki przesyłania strumieniowego](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Przejdź toohello **dane wyjściowe** karcie i Zmień nazwę tabeli SQL hello hello zbyt**TollDataTumblingCountPartitioned**.

Po uruchomieniu zadania hello teraz Azure Stream Analytics można rozpraszających między większą ilością zasobów obliczeniowych i osiągnąć lepszą przepustowość. Należy pamiętać, że ten TollApp aplikacji hello również wysyła zdarzenia partycjonowanego TollId.

## <a name="monitor"></a>Monitorowanie
Witaj **MONITOR** obszar zawiera Statystyka hello uruchomienia zadania. Po raz pierwszy konfiguracja jest potrzebne konto magazynu hello toouse w hello tym samym regionie (nazwa przez jak hello pozostałej części tego dokumentu).   

![Zrzut ekranu przedstawiający monitor](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Dostęp można uzyskać **Dzienniki aktywności** z pulpitu nawigacyjnego zadania hello **ustawienia** również obszaru.


## <a name="conclusion"></a>Podsumowanie
W tym samouczku wprowadzono toohello usługi Azure Stream Analytics. Konieczne wykazanie, jak tooconfigure wejścia i wyjścia dla hello zadania usługi analiza strumienia. Scenariusz danych przez hello hello samouczku wyjaśniono typowych problemów, które powstają w hello przestrzeni danych w ruchu i jak można rozwiązać za pomocą prostego zapytania przypominającego SQL w Azure Stream Analytics. Samouczek Hello opisane konstrukcje rozszerzenia SQL do pracy z danymi danych czasowych. Pokazano, jak strumieni danych toojoin, jak strumienia danych hello tooenrich z statyczne dane referencyjne i jak tooscale limit wyższej przepustowości tooachieve zapytania.

Chociaż ten samouczek zawiera wprowadzenie dobry, nie została ukończona w jakikolwiek sposób. Można znaleźć więcej wzorców zapytań przy użyciu języka SAQL hello na [zapytania przykłady typowych wzorców użycia usługi Stream Analytics](stream-analytics-stream-analytics-query-patterns.md).
Zobacz toohello [dokumentacji online](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn więcej informacji na temat usługi Azure Stream Analytics.

## <a name="clean-up-your-azure-account"></a>Wyczyść konta platformy Azure
1. Zatrzymaj zadanie usługi Stream Analytics hello w hello portalu Azure.
   
    Witaj Setup.ps1 skrypt tworzy dwa centra zdarzeń i bazy danych SQL. Witaj następujące instrukcje pomagają wyczyścić zasoby na końcu hello hello samouczka.
2. W oknie programu PowerShell, wpisz **.\\ CleanUp.ps1** toostart hello skrypt, który usuwa zasoby używane w samouczku hello.
   
   > [!NOTE]
   > Zasoby są identyfikowane przez nazwę hello. Upewnij się, że dokładnie przejrzyj poszczególne elementy przed potwierdzeniem usuwania.
   > 
   > 


