## <a name="view-hello-telemetry"></a>Dane telemetryczne wyświetleń hello

Hello Pi malina teraz wysyła dane telemetryczne toohello zdalnego rozwiązanie monitorowania. Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello. Można również wysłać wiadomości tooyour Pi malina z pulpitu nawigacyjnego rozwiązania hello.

- Przejdź toohello pulpit nawigacyjny rozwiązania.
- Wybierz swoje urządzenie w hello **tooView urządzenia** listy rozwijanej.
- dane telemetryczne Hello z hello Pi malina wyświetla na pulpicie nawigacyjnym hello.

![Wyświetl dane telemetryczne z hello Pi malina][img-telemetry-display]

## <a name="act-on-hello-device"></a>Działania na urządzeniu hello

Z pulpitu nawigacyjnego rozwiązania hello można wywoływać metod w Twojej Pi malina. Gdy hello Pi malina łączy toohello zdalnego rozwiązanie monitorowania, wysyła informacje o metodach hello, który go obsługuje.

- Na pulpicie nawigacyjnym rozwiązania hello, kliknij przycisk **urządzeń** toovisit hello **urządzeń** strony. Wybierz użytkownika Pi malina hello **listę urządzeń**. Następnie wybierz pozycję **metody**:

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

- Na powitania **wywołania metody** wybierz pozycję **LightBlink** w hello **metody** listy rozwijanej.

- Wybierz **InvokeMethod**. Witaj LED połączone toohello, który Pi malina miga kilka razy. Aplikacja Hello na powitania Pi malina wysyła pulpit nawigacyjny potwierdzenia wstecz toohello rozwiązania:

    ![Pokaż historię — metoda][img-method-history]

- Możesz przełączyć hello LED włączać i wyłączać za pomocą hello **ChangeLightStatus** metody z **LightStatusValue** ustawić także**1** dla na lub **0** dla off.

> [!WARNING]
> Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config]. Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md