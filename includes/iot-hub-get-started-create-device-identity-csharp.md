## <a name="create-a-device-identity"></a><span data-ttu-id="d2df5-101">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="d2df5-101">Create a device identity</span></span>
<span data-ttu-id="d2df5-102">W tej sekcji służy do tworzenia aplikacji konsoli .NET, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d2df5-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d2df5-103">Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="d2df5-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d2df5-104">Aby uzyskać więcej informacji, zobacz część hello w "Tożsamość rejestru" hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d2df5-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d2df5-105">Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d2df5-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="d2df5-106">W identyfikatorach urządzeń jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d2df5-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="d2df5-107">W programie Visual Studio, Dodaj nowe rozwiązanie tooa projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="d2df5-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d2df5-108">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d2df5-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d2df5-109">Nazwa projektu hello **CreateDeviceIdentity** i nazwa rozwiązania hello **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="d2df5-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][10]
2. <span data-ttu-id="d2df5-111">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **CreateDeviceIdentity** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d2df5-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="d2df5-112">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="d2df5-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d2df5-113">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d2df5-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][11]
4. <span data-ttu-id="d2df5-115">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="d2df5-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="d2df5-116">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="d2df5-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d2df5-117">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d2df5-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="d2df5-118">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="d2df5-118">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="d2df5-119">Ta metoda służy do tworzenia tożsamości urządzenia o identyfikatorze **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="d2df5-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="d2df5-120">(Jeśli ten identyfikator urządzenia jest już istnieje w rejestrze tożsamości hello, hello kod po prostu pobiera informacje o urządzeniu istniejących hello.) następnie aplikacja Hello Wyświetla hello klucz podstawowy dla tej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="d2df5-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="d2df5-121">Należy użyć tego klucza w Centrum IoT tooyour tooconnect aplikacji hello symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d2df5-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="d2df5-122">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="d2df5-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="d2df5-123">Uruchomić tę aplikację i zanotuj klucz urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="d2df5-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Wygenerowany przez aplikację hello klucz urządzenia][12]

> [!NOTE]
> <span data-ttu-id="d2df5-125">Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d2df5-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d2df5-126">Urządzenia toouse identyfikatorów i klucze są przechowywane jako poświadczenia zabezpieczeń, a flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d2df5-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d2df5-127">Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2df5-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d2df5-128">Więcej informacji znajduje się w temacie [IoT Hub Developer Guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="d2df5-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
