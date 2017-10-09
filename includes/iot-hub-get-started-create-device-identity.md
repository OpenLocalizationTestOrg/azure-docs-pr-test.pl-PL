## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia

W tej sekcji można użyć narzędzia Node.js o nazwie [explorer Centrum iothub] [ iot-hub-explorer] toocreate tożsamość urządzenia w ramach tego samouczka. W identyfikatorach urządzeń jest uwzględniana wielkość liter.

1. Uruchom następujące hello w środowisku wiersza polecenia:

    `npm install -g iothub-explorer@latest`

1. Następnie uruchom hello następujące polecenia toologin tooyour koncentratora. SUBSTITUTE `{iot hub connection string}` z hello skopiowane wcześniej parametry połączenia Centrum IoT:

    `iothub-explorer login "{iot hub connection string}"`

1. Na koniec utworzy nową tożsamość urządzenia o nazwie `myDeviceId` za pomocą polecenia hello:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Zanotuj parametry połączenia urządzenia powitania od wyniku hello. Ten ciąg połączenia urządzenia jest używany przez hello urządzenia aplikacji tooconnect tooyour Centrum IoT jako urządzenie.

![][img-identity]

Odwołuje się zbyt[wprowadzenie do korzystania z Centrum IoT] [ lnk-getstarted] tooprogrammatically tworzenia tożsamości urządzenia.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
