## <a name="view-device-telemetry-in-hello-dashboard"></a>Telemetrii urządzenia widoku na pulpicie nawigacyjnym hello
pulpit nawigacyjny Hello w hello zdalne monitorowanie umożliwia rozwiązanie możesz tooview hello telemetrii urządzenia wysyłania tooIoT koncentratora.

1. W przeglądarce zwracany toohello zdalnego monitorowania rozwiązania pulpitu nawigacyjnego, kliknij przycisk **urządzeń** w hello lewym panelu toonavigate toohello **listy urządzeń**.
2. W hello **listy urządzeń**, powinny być widoczne czy hello stan urządzenia jest **systemem**. Jeśli nie, kliknij przycisk **Włącz urządzenie** w hello **szczegóły urządzenia** panelu.
   
    ![Wyświetlanie stanu urządzenia][18]
3. Kliknij przycisk **pulpitu nawigacyjnego** tooreturn toohello pulpitu nawigacyjnego, wybierz swoje urządzenie w hello **tooView urządzenia** tooview listy rozwijanej jego telemetrii. telemetrii Hello z hello przykładowej aplikacji jest 50 jednostek dla wewnętrznej temperatury, 55 jednostki dla zewnętrznych temperatury oraz 50 urządzeń wilgotności.
   
    ![Wyświetlanie danych telemetrycznych z urządzenia][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Wywoływanie metody na urządzeniu
pulpit nawigacyjny Hello w zdalnym rozwiązanie monitorowania hello umożliwia metody tooinvoke na urządzeniach za pośrednictwem Centrum IoT. Na przykład w hello zdalnego rozwiązanie monitorujące, można wywoływać toosimulate metody, ponowne uruchomienie urządzenia.

1. W hello zdalnego monitorowania rozwiązania pulpitu nawigacyjnego, kliknij przycisk **urządzeń** w hello lewym panelu toonavigate toohello **listy urządzeń**.
2. Kliknij przycisk **identyfikator urządzenia** dla urządzenia w hello **listy urządzeń**.
3. W hello **szczegóły urządzenia** panelu, kliknij przycisk **metody**.
   
    ![Metody urządzenia][13]
4. W hello **metody** listy rozwijanej, wybierz pozycję **InitiateFirmwareUpdate**, a następnie w **FWPACKAGEURI** fikcyjny adres URL. Kliknij przycisk **wywołania metody** metody hello toocall hello urządzenia.
   
    ![Wywoływanie metody urządzenia][14]
   

5. Zostanie wyświetlony komunikat w konsoli hello systemem kodu urządzenia, obsługując urządzenia hello hello — metoda. wyniki Hello metody hello są dodawane historii toohello w portalu rozwiązania hello:

    ![Wyświetlanie historii metod][img-method-history]

## <a name="next-steps"></a>Następne kroki
Artykuł Hello [Dostosowywanie wstępnie rozwiązań] [ lnk-customize] opisano kilka metod, można rozszerzyć w tym przykładzie. Możliwe rozszerzenia obejmują użycie rzeczywistych czujników i implementację dodatkowych poleceń.

Dowiedz się więcej o hello [uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
