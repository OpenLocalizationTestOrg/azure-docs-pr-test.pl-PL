## <a name="view-the-solution-dashboard"></a><span data-ttu-id="55505-101">Wyświetlanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="55505-101">View the solution dashboard</span></span>

<span data-ttu-id="55505-102">Pulpit nawigacyjny pozwala zarządzać wdrożonym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="55505-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="55505-103">Można na przykład wyświetlić dane telemetryczne, Dodaj urządzenia i wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="55505-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="55505-104">Jeśli aprowizacja została ukończona, a na kafelku wstępnie skonfigurowanego rozwiązania jest wyświetlany stan **Gotowe**, wybierz pozycję **Uruchom**, aby otworzyć portal rozwiązania do monitorowania zdalnego na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="55505-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Uruchamianie wstępnie skonfigurowanego rozwiązania][img-launch-solution]

1. <span data-ttu-id="55505-106">Domyślnie w portalu rozwiązania jest wyświetlany *pulpit nawigacyjny*.</span><span class="sxs-lookup"><span data-stu-id="55505-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="55505-107">Przejdź do innych obszarach portalu rozwiązania przy użyciu menu po lewej stronie strony.</span><span class="sxs-lookup"><span data-stu-id="55505-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="55505-109">Dodawanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="55505-109">Add a device</span></span>

<span data-ttu-id="55505-110">Aby urządzenie mogło nawiązać połączenie ze wstępnie skonfigurowanym rozwiązaniem, musi ono zidentyfikować się względem usługi IoT Hub za pomocą prawidłowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="55505-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="55505-111">Poświadczenia urządzenia możesz pobrać z pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="55505-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="55505-112">W dalszej części tego samouczka podasz te poświadczenia urządzenia w Twojej aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="55505-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="55505-113">Aby dodać urządzenie do swojego rozwiązania do monitorowania zdalnego, wykonaj poniższe kroki na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="55505-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="55505-114">W lewym dolnym rogu pulpitu nawigacyjnego kliknij pozycję **Dodaj urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="55505-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Dodawanie urządzenia][1]

1. <span data-ttu-id="55505-116">W panelu **Urządzenie niestandardowe** kliknij pozycję **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="55505-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Dodawanie urządzenia niestandardowego][2]

1. <span data-ttu-id="55505-118">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="55505-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="55505-119">Wprowadź identyfikator urządzenia, takie jak **device01**, kliknij przycisk **Sprawdź identyfikator** można zweryfikować już nie użyto nazwy rozwiązania, a następnie kliknij przycisk **Utwórz** do obsługi administracyjnej urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="55505-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Dodawanie identyfikatora urządzenia][3]

1. <span data-ttu-id="55505-121">Zanotuj poświadczenia urządzenia (**identyfikator urządzenia**, **nazwy hosta Centrum IoT**, i **klucza urządzenia**).</span><span class="sxs-lookup"><span data-stu-id="55505-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="55505-122">Aplikacja kliencka na Intel NUC musi tych wartości, aby nawiązać połączenie zdalne rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="55505-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="55505-123">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="55505-123">Then click **Done**.</span></span>

    ![Wyświetlanie poświadczeń urządzenia][4]

1. <span data-ttu-id="55505-125">Wybierz urządzenie na liście urządzeń na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="55505-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="55505-126">Następnie w panelu **Szczegóły urządzenia** kliknij pozycję **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="55505-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="55505-127">Stan Twojego urządzenia to teraz **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="55505-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="55505-128">Rozwiązanie do monitorowania zdalnego może teraz odbierać dane telemetryczne z Twojego urządzenia i wywoływać metody na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="55505-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png