> [!div class="op_single_selector"]
> * [<span data-ttu-id="fdf2b-101">C w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="fdf2b-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="fdf2b-102">C w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="fdf2b-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="fdf2b-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="fdf2b-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="fdf2b-104">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="fdf2b-104">Scenario overview</span></span>
<span data-ttu-id="fdf2b-105">W tym scenariuszu utworzysz urządzenie, które wysyła następujące dane telemetryczne do [wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="fdf2b-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="fdf2b-106">Temperatura zewnętrzna</span><span class="sxs-lookup"><span data-stu-id="fdf2b-106">External temperature</span></span>
* <span data-ttu-id="fdf2b-107">Temperatura wewnętrzna</span><span class="sxs-lookup"><span data-stu-id="fdf2b-107">Internal temperature</span></span>
* <span data-ttu-id="fdf2b-108">Wilgotność</span><span class="sxs-lookup"><span data-stu-id="fdf2b-108">Humidity</span></span>

<span data-ttu-id="fdf2b-109">Dla uproszczenia kod na urządzeniu generuje przykładowe wartości, ale zachęcamy do rozszerzenia przykładu przez podłączenie rzeczywistych czujników do urządzenia i wysyłanie rzeczywistych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="fdf2b-110">Urządzenie potrafi także odpowiadać na metody wywołane z poziomu pulpitu nawigacyjnego rozwiązania i wartości żądanych właściwości ustawione na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="fdf2b-111">Do wykonania kroków tego samouczka jest potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="fdf2b-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fdf2b-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="fdf2b-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fdf2b-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fdf2b-114">Before you start</span></span>
<span data-ttu-id="fdf2b-115">Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="fdf2b-116">Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="fdf2b-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="fdf2b-117">Urządzenie, które utworzysz w ramach tego samouczka, będzie wysyłać dane do wystąpienia wstępnie skonfigurowanego rozwiązania do [monitorowania zdalnego][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="fdf2b-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="fdf2b-118">Jeśli jeszcze nie przeprowadzono aprowizacji wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego na Twoim koncie platformy Azure, wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="fdf2b-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="fdf2b-119">Na stronie <https://www.azureiotsuite.com/> kliknij pozycję **+**, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="fdf2b-120">Kliknij pozycję **Wybierz** w panelu **Monitorowanie zdalne**, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="fdf2b-121">Na stronie **Tworzenie rozwiązania do monitorowania zdalnego** w polu **Nazwa rozwiązania** wprowadź wybraną nazwę rozwiązania, w polu **Region** wybierz region, w którym chcesz przeprowadzić wdrożenie, a następnie wybierz subskrypcję platformy Azure, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="fdf2b-122">Następnie kliknij pozycję **Utwórz rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="fdf2b-123">Zaczekaj na ukończenie procesu aprowizowania.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="fdf2b-124">Wstępnie skonfigurowane rozwiązania korzystają z płatnych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="fdf2b-125">Pamiętaj o usunięciu wstępnie skonfigurowanego rozwiązania ze swojej subskrypcji po zakończeniu pracy z nim, aby uniknąć wszelkich zbędnych opłat.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="fdf2b-126">Możesz całkowicie usunąć wstępnie skonfigurowane rozwiązanie ze swojej subskrypcji, odwiedzając stronę <https://www.azureiotsuite.com/>.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="fdf2b-127">Po zakończeniu procesu aprowizowania rozwiązania do monitorowania zdalnego kliknij pozycję **Uruchom**, aby otworzyć pulpit nawigacyjny rozwiązania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="fdf2b-129">Aprowizowanie urządzenia w ramach rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="fdf2b-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="fdf2b-130">Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="fdf2b-131">Podczas tworzenia aplikacji klienckiej musisz znać poświadczenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="fdf2b-132">Aby urządzenie mogło nawiązać połączenie ze wstępnie skonfigurowanym rozwiązaniem, musi ono zidentyfikować się względem usługi IoT Hub za pomocą prawidłowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="fdf2b-133">Poświadczenia urządzenia możesz pobrać z pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="fdf2b-134">W dalszej części tego samouczka podasz te poświadczenia urządzenia w Twojej aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="fdf2b-135">Aby dodać urządzenie do swojego rozwiązania do monitorowania zdalnego, wykonaj poniższe kroki na pulpicie nawigacyjnym rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="fdf2b-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="fdf2b-136">W lewym dolnym rogu pulpitu nawigacyjnego kliknij pozycję **Dodaj urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Dodawanie urządzenia][1]
2. <span data-ttu-id="fdf2b-138">W panelu **Urządzenie niestandardowe** kliknij pozycję **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Dodawanie urządzenia niestandardowego][2]
3. <span data-ttu-id="fdf2b-140">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="fdf2b-141">Wprowadź identyfikator urządzenia, na przykład **moje_urządzenie**, kliknij pozycję **Sprawdź identyfikator**, aby sprawdzić, czy dana nazwa nie jest już używana, a następnie kliknij pozycję **Utwórz**, aby przeprowadzić aprowizację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Dodawanie identyfikatora urządzenia][3]
4. <span data-ttu-id="fdf2b-143">Zanotuj poświadczenia urządzenia (identyfikator urządzenia, nazwę hosta usługi IoT Hub i klucz urządzenia).</span><span class="sxs-lookup"><span data-stu-id="fdf2b-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="fdf2b-144">Twoja aplikacja kliencka potrzebuje tych wartości, aby mogła nawiązać połączenie z rozwiązaniem do monitorowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="fdf2b-145">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-145">Then click **Done**.</span></span>
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. <span data-ttu-id="fdf2b-147">Wybierz urządzenie na liście urządzeń na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="fdf2b-148">Następnie w panelu **Szczegóły urządzenia** kliknij pozycję **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="fdf2b-149">Stan Twojego urządzenia to teraz **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="fdf2b-150">Rozwiązanie do monitorowania zdalnego może teraz odbierać dane telemetryczne z Twojego urządzenia i wywoływać metody na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="fdf2b-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/