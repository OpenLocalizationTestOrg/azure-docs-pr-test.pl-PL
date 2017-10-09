## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia

W tej sekcji użyjesz hello [portalu Azure] [ lnk-azure-portal] toocreate tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT. Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello. Aby uzyskać więcej informacji, zobacz część hello w "Tożsamość rejestru" hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity]. Witaj **Explorer urządzenia** w hello portalu pomaga Wygeneruj Unikatowy identyfikator urządzenia i klucz urządzenia można użyć tooidentify się podczas łączenia tooIoT koncentratora. W identyfikatorach urządzeń jest uwzględniana wielkość liter.

1. Upewnij się, że użytkownik jest zalogowany toohello [portalu Azure][lnk-azure-portal].

1. W hello pasku dostępu kliknij **wszystkie zasoby** i Znajdź zasobu Centrum IoT.

    ![Przejdź do Centrum Iot tooyour][img-find-iothub]

1. Po otwarciu zasobu Centrum IoT kliknij hello **Explorer urządzenia** narzędzia, a następnie kliknij przycisk **Dodaj** u góry hello. Podaj nazwę hello nowe urządzenie, takie jak **myDeviceId**i kliknij przycisk **zapisać**.

    ![Tworzenie tożsamości urządzenia w portalu][img-create-device]

   Spowoduje to utworzenie nowej tożsamości urządzenia Centrum IoT.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. W hello **Explorer urządzenia**na listę urządzeń, kliknij urządzenie hello nowo utworzona i zanotuj hello **ciąg połączenia---klucz podstawowy**. 

    ![Ciąg połączenia urządzenia][img-connection-string]

> [!NOTE]
> Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia. Urządzenia toouse identyfikatorów i klucze są przechowywane jako poświadczenia zabezpieczeń, a flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń. Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji. Więcej informacji znajduje się w temacie [IoT Hub Developer Guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

