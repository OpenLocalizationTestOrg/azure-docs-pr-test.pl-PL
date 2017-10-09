## <a name="create-an-iot-hub"></a><span data-ttu-id="9535d-101">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9535d-101">Create an IoT hub</span></span>
<span data-ttu-id="9535d-102">Tworzenie Centrum IoT dla Twojego tooconnect aplikacji symulowane urządzenie do.</span><span class="sxs-lookup"><span data-stu-id="9535d-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="9535d-103">Witaj poniższej procedurze pokazano, jak toocomplete to zadanie za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9535d-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="9535d-104">Zaloguj się toohello [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="9535d-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="9535d-105">W hello pasku dostępu kliknij **nowy** > **Internetu rzeczy** > **Centrum IoT**.</span><span class="sxs-lookup"><span data-stu-id="9535d-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Pasek dostępu witryny Azure Portal][1]
1. <span data-ttu-id="9535d-107">W hello **Centrum IoT** bloku, wybierz konfigurację hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9535d-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Blok centrum IoT][2]
   
   1. <span data-ttu-id="9535d-109">W hello **nazwa** wprowadź nazwę Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9535d-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="9535d-110">Jeśli hello **nazwa** jest prawidłowa i dostępna, zielony znacznik wyboru pojawia się w hello **nazwa** pole.</span><span class="sxs-lookup"><span data-stu-id="9535d-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="9535d-111">Wybierz pozycję [Warstwa cenowa i warstwa skali][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="9535d-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="9535d-112">W tym samouczku nie jest wymagane użycie określonej warstwy.</span><span class="sxs-lookup"><span data-stu-id="9535d-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="9535d-113">Dla tego samouczka użyj bezpłatnej warstwy F1 hello.</span><span class="sxs-lookup"><span data-stu-id="9535d-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="9535d-114">W obszarze **Grupa zasobów** utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="9535d-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="9535d-115">Aby uzyskać więcej informacji, zobacz [toomanage przy użyciu zasobów grup zasobów platformy Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="9535d-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="9535d-116">W **lokalizacji**, wybierz hello toohost lokalizacji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9535d-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="9535d-117">Do celów tego samouczka wybierz najbliższą lokalizację.</span><span class="sxs-lookup"><span data-stu-id="9535d-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="9535d-118">Po wybraniu opcji konfiguracji centrum IoT kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9535d-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="9535d-119">Może upłynąć kilka minut, aż Azure toocreate Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9535d-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="9535d-120">Stan hello toocheck, możesz monitorować postęp hello na powitania tablicy startowej lub w panelu powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="9535d-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Stan nowego centrum IoT][3]
1. <span data-ttu-id="9535d-122">Gdy Centrum IoT hello został utworzony pomyślnie, kliknij przycisk hello nowy Kafelek Centrum IoT w bloku hello Azure tooopen portalu hello hello nowego centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9535d-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="9535d-123">Zanotuj hello **Hostname**, a następnie kliknij przycisk **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="9535d-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Blok nowego centrum IoT][4]
1. <span data-ttu-id="9535d-125">W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk hello **iothubowner** zasad, a następnie skopiuj i zanotuj parametry połączenia Centrum IoT hello hello **iothubowner** bloku.</span><span class="sxs-lookup"><span data-stu-id="9535d-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="9535d-126">Aby uzyskać więcej informacji, zobacz [kontrola dostępu] [ lnk-access-control] w hello "Centrum IoT Podręcznik dewelopera".</span><span class="sxs-lookup"><span data-stu-id="9535d-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
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
