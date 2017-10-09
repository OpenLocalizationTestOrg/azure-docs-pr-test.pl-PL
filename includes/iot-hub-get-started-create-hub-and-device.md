## <a name="create-an-iot-hub"></a><span data-ttu-id="b61c1-101">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="b61c1-101">Create an IoT hub</span></span>

1. <span data-ttu-id="b61c1-102">W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **nowy** > **Internetu rzeczy** > **Centrum IoT**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Tworzenie Centrum IoT w portalu Azure hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="b61c1-104">W hello **Centrum IoT** okienku, wprowadź następujące informacje o Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="b61c1-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="b61c1-105">**Nazwa**: Wprowadź nazwę hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b61c1-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="b61c1-106">Jeśli wprowadzona nazwa hello jest prawidłowy, zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="b61c1-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="b61c1-107">**Warstwę cenową i wartę skali**: Wybierz hello **F1 – wolnego** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b61c1-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="b61c1-108">Ta opcja jest wystarczająca na potrzeby tej demonstracji.</span><span class="sxs-lookup"><span data-stu-id="b61c1-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="b61c1-109">Aby uzyskać więcej informacji, zobacz hello [warstwa cenowa i skali](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="b61c1-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="b61c1-110">**Grupa zasobów**: Utwórz Centrum IoT zasobów grupy toohost hello lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="b61c1-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="b61c1-111">Aby uzyskać więcej informacji, zobacz [grupy zasobów Użyj toomanage zasobów platformy Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b61c1-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="b61c1-112">**Lokalizacja**: Wybierz hello najbliższego tooyou lokalizacji, której utworzono Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b61c1-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="b61c1-113">**Numer PIN toodashboard**: Wybierz tę opcję, Centrum IoT tooyour łatwy dostęp z hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b61c1-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Wprowadź informacje toocreate Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="b61c1-115">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-115">Click **Create**.</span></span> <span data-ttu-id="b61c1-116">Centrum IoT może potrwać kilka minut toocreate.</span><span class="sxs-lookup"><span data-stu-id="b61c1-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="b61c1-117">Wyświetlany postęp w hello **powiadomienia** okienka.</span><span class="sxs-lookup"><span data-stu-id="b61c1-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Wyświetlanie powiadomień z postępami dla centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="b61c1-119">Po utworzeniu Centrum IoT kliknij go na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b61c1-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="b61c1-120">Zanotuj hello **Hostname**, a następnie kliknij przycisk **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Pobierz nazwę hosta hello Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="b61c1-122">W hello **zasady dostępu współużytkowanego** okienku kliknij hello **iothubowner** zasad, a następnie Kopiuj i zanotować hello **ciąg połączenia** Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b61c1-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="b61c1-123">Aby uzyskać więcej informacji, zobacz [kontroli dostępu tooIoT Centrum](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="b61c1-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="b61c1-124">W przypadku tego samouczka konfiguracji te parametry połączenia iothubowner nie będą potrzebne.</span><span class="sxs-lookup"><span data-stu-id="b61c1-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="b61c1-125">Jednak może być potrzebny dla niektórych samouczki hello w różnych scenariuszach IoT po ukończeniu tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b61c1-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Pobieranie parametrów połączenia centrum IoT Hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="b61c1-127">Zarejestruj urządzenie w Centrum IoT hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="b61c1-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="b61c1-128">W hello [portalu Azure](https://portal.azure.com/), Otwórz Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b61c1-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="b61c1-129">Kliknij pozycję **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="b61c1-130">W okienku Eksplorator urządzenia powitania kliknij **Dodaj** tooadd Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b61c1-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="b61c1-131">Następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="b61c1-131">Then do hello following:</span></span>

   <span data-ttu-id="b61c1-132">**Identyfikator urządzenia**: Wprowadź identyfikator hello hello nowe urządzenie.</span><span class="sxs-lookup"><span data-stu-id="b61c1-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="b61c1-133">W identyfikatorach urządzeń jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b61c1-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="b61c1-134">**Typ uwierzytelniania**: wybierz pozycję **Klucz symetryczny**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="b61c1-135">**Automatyczne generowanie kluczy**: zaznacz to pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="b61c1-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="b61c1-136">**Połącz urządzenie tooIoT Centrum**: kliknij **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Dodaj urządzenie w hello Explorer urządzenie z Centrum IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="b61c1-138">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b61c1-138">Click **Save**.</span></span>
5. <span data-ttu-id="b61c1-139">Po utworzeniu urządzenia hello otworzyć urządzenia hello w hello **Explorer urządzenia** okienka.</span><span class="sxs-lookup"><span data-stu-id="b61c1-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="b61c1-140">Zanotuj klucz podstawowy hello hello parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b61c1-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Pobierz ciąg połączenia urządzenia hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
