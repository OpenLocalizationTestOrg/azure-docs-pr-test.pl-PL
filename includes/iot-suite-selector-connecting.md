> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c77e-101">C w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="4c77e-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="4c77e-102">C w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4c77e-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="4c77e-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="4c77e-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="4c77e-104">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="4c77e-104">Scenario overview</span></span>
<span data-ttu-id="4c77e-105">W tym scenariuszu, Utwórz urządzenie, które wysyła powitania po monitorowania zdalnego toohello telemetrii [wstępnie skonfigurowane rozwiązanie][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="4c77e-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="4c77e-106">Temperatura zewnętrzna</span><span class="sxs-lookup"><span data-stu-id="4c77e-106">External temperature</span></span>
* <span data-ttu-id="4c77e-107">Temperatura wewnętrzna</span><span class="sxs-lookup"><span data-stu-id="4c77e-107">Internal temperature</span></span>
* <span data-ttu-id="4c77e-108">Wilgotność</span><span class="sxs-lookup"><span data-stu-id="4c77e-108">Humidity</span></span>

<span data-ttu-id="4c77e-109">Dla uproszczenia kodu hello na urządzeniu hello generuje przykładowe wartości, ale firma Microsoft zachęca możesz tooextend hello próbki podłączania urządzenia tooyour rzeczywistych czujników i wysyła rzeczywistych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="4c77e-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="4c77e-110">urządzenie Hello jest również toomethods toorespond można wywołać z poziomu pulpitu nawigacyjnego rozwiązania hello i potrzebne wartości właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="4c77e-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="4c77e-111">toocomplete tego samouczka potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4c77e-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="4c77e-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="4c77e-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4c77e-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="4c77e-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4c77e-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4c77e-114">Before you start</span></span>
<span data-ttu-id="4c77e-115">Przed przystąpieniem do pisania jakiegokolwiek kodu dla urządzenia musisz przeprowadzić aprowizację wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego i nowego niestandardowego urządzenia w ramach tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4c77e-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="4c77e-116">Aprowizowanie wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego</span><span class="sxs-lookup"><span data-stu-id="4c77e-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="4c77e-117">urządzenie Hello Utwórz w tym samouczku wysyła dane wystąpienia tooan hello [monitorowania zdalnego] [ lnk-remote-monitoring] wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="4c77e-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="4c77e-118">Jeśli nie zostało już przydzielona hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie w konta platformy Azure, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4c77e-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="4c77e-119">Na powitania <https://www.azureiotsuite.com/> kliknij przycisk  **+**  toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4c77e-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="4c77e-120">Kliknij przycisk **wybierz** na powitania **monitorowania zdalnego** panelu toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4c77e-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="4c77e-121">Na powitania **utworzyć zdalnego rozwiązanie monitorujące** wprowadź **Nazwa rozwiązania** wybranych przez użytkownika, wybierz hello **Region** toodeploy do, a następnie wybierz hello Azure toouse toowant subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4c77e-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="4c77e-122">Następnie kliknij pozycję **Utwórz rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="4c77e-123">Poczekaj na zakończenie procesu udostępniania hello.</span><span class="sxs-lookup"><span data-stu-id="4c77e-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="4c77e-124">rozwiązania Hello wstępnie skonfigurowane za pomocą usług Azure rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="4c77e-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="4c77e-125">Pamiętaj, że tooremove hello wstępnie skonfigurowane rozwiązanie z subskrypcji, gdy wszystko będzie gotowe z nim tooavoid opłaty niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="4c77e-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="4c77e-126">Wstępnie skonfigurowane rozwiązanie można całkowicie usunąć z subskrypcji, odwiedzając hello <https://www.azureiotsuite.com/> strony.</span><span class="sxs-lookup"><span data-stu-id="4c77e-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="4c77e-127">Po zakończeniu hello inicjowania obsługi administracyjnej proces hello zdalnego rozwiązanie monitorujące, kliknij przycisk **uruchamianie** pulpit nawigacyjny rozwiązania hello tooopen w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="4c77e-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Pulpit nawigacyjny rozwiązania][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="4c77e-129">Zapewnij urządzenia w hello zdalne monitorowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4c77e-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="4c77e-130">Jeśli już przeprowadzono aprowizację urządzenia w ramach rozwiązania, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="4c77e-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="4c77e-131">Należy tooknow hello urządzenia poświadczeń podczas tworzenia powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c77e-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="4c77e-132">Jako rozwiązanie toohello wstępnie tooconnect urządzenia, jego musi identyfikacji tooIoT Centrum używając poprawnych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4c77e-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="4c77e-133">Pulpit nawigacyjny rozwiązania hello może pobrać poświadczenia urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="4c77e-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="4c77e-134">Wprowadzono poświadczenia urządzeń hello w dalszej części tego samouczka aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="4c77e-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="4c77e-135">tooadd urządzenia tooyour zdalnego rozwiązanie monitorowania pełną hello następujące kroki na pulpicie nawigacyjnym rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="4c77e-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="4c77e-136">W hello lewym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **dodać urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Dodawanie urządzenia][1]
2. <span data-ttu-id="4c77e-138">W hello **urządzenia niestandardowe** panelu, kliknij przycisk **Dodaj nowe**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Dodawanie urządzenia niestandardowego][2]
3. <span data-ttu-id="4c77e-140">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="4c77e-141">Wprowadź identyfikator urządzenia, takie jak **mydevice**, kliknij przycisk **Sprawdź identyfikator** tooverify tej nazwie nie jest już w użyciu, a następnie kliknij **Utwórz** tooprovision hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4c77e-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Dodawanie identyfikatora urządzenia][3]
4. <span data-ttu-id="4c77e-143">Należy skonfigurować urządzenie hello Uwaga poświadczeń (identyfikator urządzenia, nazwy hosta Centrum IoT i klucz urządzenia).</span><span class="sxs-lookup"><span data-stu-id="4c77e-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="4c77e-144">Aplikacja kliencka musi zdalne monitorowanie rozwiązania toohello tooconnect tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4c77e-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="4c77e-145">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-145">Then click **Done**.</span></span>
   
    ![Wyświetlanie poświadczeń urządzenia][4]
5. <span data-ttu-id="4c77e-147">Wybierz urządzenie na liście urządzeń hello na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="4c77e-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="4c77e-148">Następnie w hello **szczegóły urządzenia** panelu, kliknij przycisk **Włącz urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="4c77e-149">Witaj stan urządzenia jest teraz **systemem**.</span><span class="sxs-lookup"><span data-stu-id="4c77e-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="4c77e-150">rozwiązanie monitorowania zdalnego Hello teraz może odbierać dane telemetryczne z urządzenia i wywołania metod na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="4c77e-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/