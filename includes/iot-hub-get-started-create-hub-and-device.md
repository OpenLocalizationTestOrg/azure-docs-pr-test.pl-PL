## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

[!INCLUDE [iot-hub-create-hub](iot-hub-create-hub.md)]

Teraz, po utworzeniu Centrum IoT, zlokalizuj ważne informacje, które są używane do łączenia urządzeń i aplikacji do Centrum IoT. 

1. Po utworzeniu centrum IoT Hub kliknij je na pulpicie nawigacyjnym. Zanotuj wartość z pola **Nazwa hosta**, a następnie kliknij polecenie **Zasady dostępu współużytkowanego**.

   ![Pobieranie nazwy hosta centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

1. W okienku **Zasady dostępu współużytkowanego** kliknij zasady **iothubowner**, a następnie skopiuj i zanotuj **Parametry połączenia** centrum IoT Hub. Aby uzyskać więcej informacji, zobacz [Kontrola dostępu do centrum IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
W przypadku tego samouczka konfiguracji te parametry połączenia iothubowner nie będą potrzebne. Niemniej mogą być potrzebne w ramach innych samouczków dotyczących innych scenariuszy IoT po zakończeniu tej konfiguracji.

   ![Pobieranie parametrów połączenia centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a>Rejestracja urządzenia w centrum IoT Hub dla Twojego urządzenia

1. W witrynie [Azure Portal](https://portal.azure.com/) otwórz swoje centrum IoT Hub.

2. Kliknij pozycję **Device Explorer**.
3. W okienku Device Explorer kliknij pozycję **Dodaj**, aby dodać urządzenie do centrum IoT Hub. Następnie wykonaj poniższe czynności:

   **Identyfikator urządzenia**: wprowadź identyfikator nowego urządzenia. W identyfikatorach urządzeń jest uwzględniana wielkość liter.

   **Typ uwierzytelniania**: wybierz pozycję **Klucz symetryczny**.

   **Automatyczne generowanie kluczy**: zaznacz to pole wyboru.

   **Połącz urządzenie z IoT Hub**: kliknij pozycję **Włącz**.

   ![Dodawanie urządzeń do centrum IoT Hub w programie Device Explorer](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Kliknij pozycję **Zapisz**.
5. Po utworzeniu urządzenia otwórz je w okienku **Device Explorer**.
6. Zanotuj klucz podstawowy parametrów połączenia.

   ![Pobieranie parametrów połączenia urządzenia](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
