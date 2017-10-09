## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT
Tworzenie Centrum IoT dla Twojego tooconnect aplikacji symulowane urządzenie do. Witaj poniższej procedurze pokazano, jak toocomplete to zadanie za pomocą hello portalu Azure.

1. Zaloguj się toohello [portalu Azure][lnk-portal].
1. W hello pasku dostępu kliknij **nowy** > **Internetu rzeczy** > **Centrum IoT**.
   
    ![Pasek dostępu witryny Azure Portal][1]
1. W hello **Centrum IoT** bloku, wybierz konfigurację hello Centrum IoT.
   
    ![Blok centrum IoT][2]
   
   1. W hello **nazwa** wprowadź nazwę Centrum IoT. Jeśli hello **nazwa** jest prawidłowa i dostępna, zielony znacznik wyboru pojawia się w hello **nazwa** pole.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Wybierz pozycję [Warstwa cenowa i warstwa skali][lnk-pricing]. W tym samouczku nie jest wymagane użycie określonej warstwy. Dla tego samouczka użyj bezpłatnej warstwy F1 hello.
   1. W obszarze **Grupa zasobów** utwórz grupę zasobów lub wybierz istniejącą. Aby uzyskać więcej informacji, zobacz [toomanage przy użyciu zasobów grup zasobów platformy Azure][lnk-resource-groups].
   1. W **lokalizacji**, wybierz hello toohost lokalizacji Centrum IoT. Do celów tego samouczka wybierz najbliższą lokalizację.
1. Po wybraniu opcji konfiguracji centrum IoT kliknij pozycję **Utwórz**.  Może upłynąć kilka minut, aż Azure toocreate Centrum IoT. Stan hello toocheck, możesz monitorować postęp hello na powitania tablicy startowej lub w panelu powiadomienia hello.
   
    ![Stan nowego centrum IoT][3]
1. Gdy Centrum IoT hello został utworzony pomyślnie, kliknij przycisk hello nowy Kafelek Centrum IoT w bloku hello Azure tooopen portalu hello hello nowego centrum IoT. Zanotuj hello **Hostname**, a następnie kliknij przycisk **zasady dostępu współużytkowanego**.
   
    ![Blok nowego centrum IoT][4]
1. W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk hello **iothubowner** zasad, a następnie skopiuj i zanotuj parametry połączenia Centrum IoT hello hello **iothubowner** bloku. Aby uzyskać więcej informacji, zobacz [kontrola dostępu] [ lnk-access-control] w hello "Centrum IoT Podręcznik dewelopera".
   
    ![Blok Zasady dostępu współużytkowanego][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
