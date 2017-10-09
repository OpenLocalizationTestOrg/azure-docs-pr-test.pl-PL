## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="17438-101">Pulpit nawigacyjny rozwiązania hello widoku</span><span class="sxs-lookup"><span data-stu-id="17438-101">View hello solution dashboard</span></span>

<span data-ttu-id="17438-102">pulpit nawigacyjny rozwiązania Hello umożliwia toomanage hello wdrożyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="17438-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="17438-103">Można na przykład wyświetlić dane telemetryczne, Dodaj urządzenia i wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="17438-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="17438-104">Po ukończeniu inicjowania obsługi administracyjnej hello i wskazuje hello Kafelek wstępnie skonfigurowane rozwiązanie **gotowe**, wybierz **uruchamianie** tooopen zdalnego monitorowania rozwiązania portalem na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="17438-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Uruchamianie hello wstępnie skonfigurowane rozwiązanie][img-launch-solution]

1. <span data-ttu-id="17438-106">Domyślnie hello rozwiązanie portalu pokazuje hello *pulpitu nawigacyjnego*.</span><span class="sxs-lookup"><span data-stu-id="17438-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="17438-107">Można przejść obszarów tooother hello rozwiązanie portalu przy użyciu hello menu na powitania po lewej stronie powitania strony.</span><span class="sxs-lookup"><span data-stu-id="17438-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="17438-109">Dodawanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="17438-109">Add a device</span></span>

<span data-ttu-id="17438-110">Jako rozwiązanie toohello wstępnie tooconnect urządzenia, jego musi identyfikacji tooIoT Centrum używając poprawnych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="17438-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="17438-111">Pulpit nawigacyjny rozwiązania hello może pobrać poświadczenia urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="17438-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="17438-112">Wprowadzono poświadczenia urządzeń hello w dalszej części tego samouczka aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="17438-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="17438-113">Jeśli jeszcze tego nie zrobiono, należy dodać urządzenia niestandardowe tooyour zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="17438-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="17438-114">Wykonaj następujące kroki na pulpicie nawigacyjnym rozwiązania hello hello:</span><span class="sxs-lookup"><span data-stu-id="17438-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="17438-115">W hello lewym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **dodać urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="17438-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Dodawanie urządzenia][1]

1. <span data-ttu-id="17438-117">W hello **urządzenia niestandardowe** panelu, kliknij przycisk **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="17438-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Dodawanie urządzenia niestandardowego][2]

1. <span data-ttu-id="17438-119">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="17438-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="17438-120">Wprowadź identyfikator urządzenia, takie jak **rasppi**, kliknij przycisk **Sprawdź identyfikator** tooverify nazwa hello nie zostało już używana w rozwiązaniu, a następnie kliknij przycisk **Utwórz** tooprovision hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="17438-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Dodawanie identyfikatora urządzenia][3]

1. <span data-ttu-id="17438-122">Zwiększanie urządzenia hello Uwaga poświadczeń (**identyfikator urządzenia**, **nazwy hosta Centrum IoT**, i **klucza urządzenia**).</span><span class="sxs-lookup"><span data-stu-id="17438-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="17438-123">Aplikacji klienta na powitania Pi malina musi zdalne monitorowanie rozwiązania toohello tooconnect tych wartości.</span><span class="sxs-lookup"><span data-stu-id="17438-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="17438-124">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="17438-124">Then click **Done**.</span></span>

    ![Wyświetlanie poświadczeń urządzenia][4]

1. <span data-ttu-id="17438-126">Wybierz urządzenie na liście urządzeń hello na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="17438-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="17438-127">Następnie w hello **szczegóły urządzenia** panelu, kliknij przycisk **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="17438-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="17438-128">Witaj stan urządzenia jest teraz **systemem**.</span><span class="sxs-lookup"><span data-stu-id="17438-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="17438-129">rozwiązanie monitorowania zdalnego Hello teraz może odbierać dane telemetryczne z urządzenia i wywołania metod na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="17438-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png