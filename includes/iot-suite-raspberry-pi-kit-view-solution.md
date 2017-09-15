## <a name="view-the-solution-dashboard"></a><span data-ttu-id="7a58c-101">Wyświetlanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="7a58c-101">View the solution dashboard</span></span>

<span data-ttu-id="7a58c-102">Pulpit nawigacyjny pozwala zarządzać wdrożonym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="7a58c-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="7a58c-103">Można na przykład wyświetlić dane telemetryczne, Dodaj urządzenia i wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="7a58c-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="7a58c-104">Jeśli aprowizacja została ukończona, a na kafelku wstępnie skonfigurowanego rozwiązania jest wyświetlany stan **Gotowe**, wybierz pozycję **Uruchom**, aby otworzyć portal rozwiązania do monitorowania zdalnego na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="7a58c-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Uruchamianie wstępnie skonfigurowanego rozwiązania][img-launch-solution]

1. <span data-ttu-id="7a58c-106">Domyślnie w portalu rozwiązania jest wyświetlany *pulpit nawigacyjny*.</span><span class="sxs-lookup"><span data-stu-id="7a58c-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="7a58c-107">Korzystając z menu po lewej stronie, można przejść do innych obszarów portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7a58c-107">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="7a58c-109">Dodawanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="7a58c-109">Add a device</span></span>

<span data-ttu-id="7a58c-110">Aby urządzenie mogło nawiązać połączenie ze wstępnie skonfigurowanym rozwiązaniem, musi ono zidentyfikować się względem usługi IoT Hub za pomocą prawidłowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7a58c-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="7a58c-111">Poświadczenia urządzenia możesz pobrać z pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7a58c-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="7a58c-112">W dalszej części tego samouczka podasz te poświadczenia urządzenia w Twojej aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="7a58c-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="7a58c-113">Jeśli jeszcze tego nie zrobiono, należy dodać niestandardowe urządzenie do zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="7a58c-113">If you haven't already done so, add a custom device to your remote monitoring solution.</span></span> <span data-ttu-id="7a58c-114">Wykonaj następujące czynności na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="7a58c-114">Complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="7a58c-115">W lewym dolnym rogu pulpitu nawigacyjnego kliknij pozycję **Dodaj urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-115">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Dodawanie urządzenia][1]

1. <span data-ttu-id="7a58c-117">W panelu **Urządzenie niestandardowe** kliknij pozycję **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-117">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Dodawanie urządzenia niestandardowego][2]

1. <span data-ttu-id="7a58c-119">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="7a58c-120">Wprowadź identyfikator urządzenia, takie jak **rasppi**, kliknij przycisk **Sprawdź identyfikator** można zweryfikować już nie użyto nazwy rozwiązania, a następnie kliknij przycisk **Utwórz** do obsługi administracyjnej urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="7a58c-120">Enter a Device ID such as **rasppi**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Dodawanie identyfikatora urządzenia][3]

1. <span data-ttu-id="7a58c-122">Zanotuj poświadczenia urządzenia (**identyfikator urządzenia**, **nazwy hosta Centrum IoT**, i **klucza urządzenia**).</span><span class="sxs-lookup"><span data-stu-id="7a58c-122">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="7a58c-123">Aplikacja kliencka na Pi malina wymaga tych wartości, aby nawiązać połączenie zdalne rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="7a58c-123">Your client application on the Raspberry Pi needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="7a58c-124">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-124">Then click **Done**.</span></span>

    ![Wyświetlanie poświadczeń urządzenia][4]

1. <span data-ttu-id="7a58c-126">Wybierz urządzenie na liście urządzeń na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7a58c-126">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="7a58c-127">Następnie w panelu **Szczegóły urządzenia** kliknij pozycję **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-127">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="7a58c-128">Stan Twojego urządzenia to teraz **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="7a58c-128">The status of your device is now **Running**.</span></span> <span data-ttu-id="7a58c-129">Rozwiązanie do monitorowania zdalnego może teraz odbierać dane telemetryczne z Twojego urządzenia i wywoływać metody na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="7a58c-129">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png