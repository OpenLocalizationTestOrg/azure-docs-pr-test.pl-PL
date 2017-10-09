## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **Internetu rzeczy** > **Centrum IoT**.

   ![Tworzenie Centrum IoT w portalu Azure hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. W hello **Centrum IoT** okienku, wprowadź następujące informacje o Centrum IoT hello:

     **Nazwa**: Wprowadź nazwę hello Centrum IoT. Jeśli wprowadzona nazwa hello jest prawidłowy, zostanie wyświetlony zielony znacznik wyboru.

     **Warstwę cenową i wartę skali**: Wybierz hello **F1 – wolnego** warstwy. Ta opcja jest wystarczająca na potrzeby tej demonstracji. Aby uzyskać więcej informacji, zobacz hello [warstwa cenowa i skali](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Grupa zasobów**: Utwórz Centrum IoT zasobów grupy toohost hello lub użyć istniejącego. Aby uzyskać więcej informacji, zobacz [grupy zasobów Użyj toomanage zasobów platformy Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Lokalizacja**: Wybierz hello najbliższego tooyou lokalizacji, której utworzono Centrum IoT hello.

     **Numer PIN toodashboard**: Wybierz tę opcję, Centrum IoT tooyour łatwy dostęp z hello pulpitu nawigacyjnego.

   ![Wprowadź informacje toocreate Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Kliknij przycisk **Utwórz**. Centrum IoT może potrwać kilka minut toocreate. Wyświetlany postęp w hello **powiadomienia** okienka.

   ![Wyświetlanie powiadomień z postępami dla centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Po utworzeniu Centrum IoT kliknij go na powitania pulpitu nawigacyjnego. Zanotuj hello **Hostname**, a następnie kliknij przycisk **zasady dostępu współużytkowanego**.

   ![Pobierz nazwę hosta hello Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. W hello **zasady dostępu współużytkowanego** okienku kliknij hello **iothubowner** zasad, a następnie Kopiuj i zanotować hello **ciąg połączenia** Centrum IoT. Aby uzyskać więcej informacji, zobacz [kontroli dostępu tooIoT Centrum](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
W przypadku tego samouczka konfiguracji te parametry połączenia iothubowner nie będą potrzebne. Jednak może być potrzebny dla niektórych samouczki hello w różnych scenariuszach IoT po ukończeniu tej konfiguracji.

   ![Pobieranie parametrów połączenia centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Zarejestruj urządzenie w Centrum IoT hello urządzenia

1. W hello [portalu Azure](https://portal.azure.com/), Otwórz Centrum IoT.

2. Kliknij pozycję **Device Explorer**.
3. W okienku Eksplorator urządzenia powitania kliknij **Dodaj** tooadd Centrum IoT tooyour urządzenia. Następnie hello następujące:

   **Identyfikator urządzenia**: Wprowadź identyfikator hello hello nowe urządzenie. W identyfikatorach urządzeń jest uwzględniana wielkość liter.

   **Typ uwierzytelniania**: wybierz pozycję **Klucz symetryczny**.

   **Automatyczne generowanie kluczy**: zaznacz to pole wyboru.

   **Połącz urządzenie tooIoT Centrum**: kliknij **włączyć**.

   ![Dodaj urządzenie w hello Explorer urządzenie z Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Kliknij pozycję **Zapisz**.
5. Po utworzeniu urządzenia hello otworzyć urządzenia hello w hello **Explorer urządzenia** okienka.
6. Zanotuj klucz podstawowy hello hello parametrów połączenia.

   ![Pobierz ciąg połączenia urządzenia hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
