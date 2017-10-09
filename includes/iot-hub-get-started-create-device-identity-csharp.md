## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia
W tej sekcji służy do tworzenia aplikacji konsoli .NET, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT. Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello. Aby uzyskać więcej informacji, zobacz część hello w "Tożsamość rejestru" hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity]. Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury. W identyfikatorach urządzeń jest uwzględniana wielkość liter.

1. W programie Visual Studio, Dodaj nowe rozwiązanie tooa projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **CreateDeviceIdentity** i nazwa rozwiązania hello **IoTHubGetStarted**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][10]
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CreateDeviceIdentity** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
3. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][11]
4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Dodaj następujące metody toohello hello **Program** klasy:
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    Ta metoda służy do tworzenia tożsamości urządzenia o identyfikatorze **myFirstDevice**. (Jeśli ten identyfikator urządzenia jest już istnieje w rejestrze tożsamości hello, hello kod po prostu pobiera informacje o urządzeniu istniejących hello.) następnie aplikacja Hello Wyświetla hello klucz podstawowy dla tej tożsamości. Należy użyć tego klucza w Centrum IoT tooyour tooconnect aplikacji hello symulowane urządzenie.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Uruchomić tę aplikację i zanotuj klucz urządzenia hello.
   
    ![Wygenerowany przez aplikację hello klucz urządzenia][12]

> [!NOTE]
> Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia. Urządzenia toouse identyfikatorów i klucze są przechowywane jako poświadczenia zabezpieczeń, a flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń. Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji. Więcej informacji znajduje się w temacie [IoT Hub Developer Guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
