> [!div class="op_single_selector"]
> * [C w systemie Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C w systemie Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Omówienie scenariusza
W tym scenariuszu, Utwórz urządzenie, które wysyła powitania po monitorowania zdalnego toohello telemetrii [wstępnie skonfigurowane rozwiązanie][lnk-what-are-preconfig-solutions]:

* Temperatura zewnętrzna
* Temperatura wewnętrzna
* Wilgotność

Dla uproszczenia kodu hello na urządzeniu hello generuje przykładowe wartości, ale firma Microsoft zachęca możesz tooextend hello próbki podłączania urządzenia tooyour rzeczywistych czujników i wysyła rzeczywistych danych telemetrycznych.

urządzenie Hello jest również toomethods toorespond można wywołać z poziomu pulpitu nawigacyjnego rozwiązania hello i potrzebne wartości właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello.

toocomplete tego samouczka potrzebne aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].

## <a name="before-you-start"></a>Przed rozpoczęciem
Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego
urządzenie Hello Utwórz w tym samouczku wysyła dane wystąpienia tooan hello [monitorowania zdalnego] [ lnk-remote-monitoring] wstępnie skonfigurowane rozwiązanie. Jeśli nie zostało już przydzielona hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie w konta platformy Azure, użyj hello następujące kroki:

1. Na powitania <https://www.azureiotsuite.com/> kliknij przycisk  **+**  toocreate rozwiązania.
2. Kliknij przycisk **wybierz** na powitania **monitorowania zdalnego** panelu toocreate rozwiązania.
3. Na powitania **utworzyć zdalnego rozwiązanie monitorujące** wprowadź **Nazwa rozwiązania** wybranych przez użytkownika, wybierz hello **Region** toodeploy do, a następnie wybierz hello Azure toouse toowant subskrypcji. Następnie kliknij pozycję **Utwórz rozwiązanie**.
4. Poczekaj na zakończenie procesu udostępniania hello.

> [!WARNING]
> rozwiązania Hello wstępnie skonfigurowane za pomocą usług Azure rozliczeniowy. Pamiętaj, że tooremove hello wstępnie skonfigurowane rozwiązanie z subskrypcji, gdy wszystko będzie gotowe z nim tooavoid opłaty niepotrzebne. Wstępnie skonfigurowane rozwiązanie można całkowicie usunąć z subskrypcji, odwiedzając hello <https://www.azureiotsuite.com/> strony.
> 
> 

Po zakończeniu hello inicjowania obsługi administracyjnej proces hello zdalnego rozwiązanie monitorujące, kliknij przycisk **uruchamianie** pulpit nawigacyjny rozwiązania hello tooopen w przeglądarce.

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Zapewnij urządzenia w hello zdalne monitorowanie rozwiązania
> [!NOTE]
> Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok. Należy tooknow hello urządzenia poświadczeń podczas tworzenia powitania klienta aplikacji.
> 
> 

Jako rozwiązanie toohello wstępnie tooconnect urządzenia, jego musi identyfikacji tooIoT Centrum używając poprawnych poświadczeń. Pulpit nawigacyjny rozwiązania hello może pobrać poświadczenia urządzeń hello. Wprowadzono poświadczenia urządzeń hello w dalszej części tego samouczka aplikacji klienta.

tooadd urządzenia tooyour zdalnego rozwiązanie monitorowania pełną hello następujące kroki na pulpicie nawigacyjnym rozwiązania hello:

1. W hello lewym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **dodać urządzenie**.
   
   ![Dodawanie urządzenia][1]
2. W hello **urządzenia niestandardowe** panelu, kliknij przycisk **Dodaj nowe**.
   
   ![Dodawanie urządzenia niestandardowego][2]
3. Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**. Wprowadź identyfikator urządzenia, takie jak **mydevice**, kliknij przycisk **Sprawdź identyfikator** tooverify tej nazwie nie jest już w użyciu, a następnie kliknij **Utwórz** tooprovision hello urządzenia.
   
   ![Dodawanie identyfikatora urządzenia][3]
4. Należy skonfigurować urządzenie hello Uwaga poświadczeń (identyfikator urządzenia, nazwy hosta Centrum IoT i klucz urządzenia). Aplikacja kliencka musi zdalne monitorowanie rozwiązania toohello tooconnect tych wartości. Następnie kliknij przycisk **Gotowe**.
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. Wybierz urządzenie na liście urządzeń hello na pulpicie nawigacyjnym rozwiązania hello. Następnie w hello **szczegóły urządzenia** panelu, kliknij przycisk **Włącz urządzenie**. Witaj stan urządzenia jest teraz **systemem**. rozwiązanie monitorowania zdalnego Hello teraz może odbierać dane telemetryczne z urządzenia i wywołania metod na urządzeniu hello.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/