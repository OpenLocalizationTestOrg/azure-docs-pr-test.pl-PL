## <a name="view-hello-telemetry"></a>Dane telemetryczne wyświetleń hello

Hello Pi malina teraz wysyła dane telemetryczne toohello zdalnego rozwiązanie monitorowania. Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello. Można również wysłać wiadomości tooyour Pi malina z pulpitu nawigacyjnego rozwiązania hello.

- Przejdź toohello pulpit nawigacyjny rozwiązania.
- Wybierz swoje urządzenie w hello **tooView urządzenia** listy rozwijanej.
- dane telemetryczne Hello z hello Pi malina wyświetla na pulpicie nawigacyjnym hello.

![Wyświetl dane telemetryczne z hello Pi malina][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Zainicjuj hello aktualizację oprogramowania układowego

proces aktualizacji oprogramowania układowego Hello pobiera i instaluje zaktualizowaną wersję aplikacji klienckiej urządzenia hello na powitania malina Pi. Aby uzyskać więcej informacji na temat procesu aktualizacji oprogramowania układowego hello, zobacz opis hello wzorca aktualizacji oprogramowania układowego hello w [omówienie zarządzania urządzeniami z Centrum IoT][lnk-update-pattern].

Inicjuje proces aktualizacji oprogramowania układowego hello przez wywołanie metody hello urządzenia. Ta metoda jest asynchroniczne i zwraca natychmiast rozpoczyna się proces aktualizacji hello. używa urządzenia Hello zgłosił właściwości toonotify hello rozwiązania dotyczące postępu hello hello aktualizacji.

W Twojej Pi malina z pulpitu nawigacyjnego rozwiązania hello jest wywoływania metod. Witaj Pi malina pierwszy raz łączy toohello zdalnego rozwiązanie monitorowania, wysyła informacje o metodach hello, który go obsługuje. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
