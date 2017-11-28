## <a name="view-the-telemetry"></a><span data-ttu-id="08421-101">Widok telemetrii</span><span class="sxs-lookup"><span data-stu-id="08421-101">View the telemetry</span></span>

<span data-ttu-id="08421-102">Pi malina teraz wysyła dane telemetryczne do zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="08421-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="08421-103">Można wyświetlić dane telemetryczne na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="08421-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="08421-104">Można również wysyłać wiadomości do Twojej Pi malina z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="08421-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="08421-105">Przejdź do pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="08421-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="08421-106">Wybierz urządzenie w **urządzenia do widoku** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="08421-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="08421-107">Dane telemetryczne z Pi malina wyświetla na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="08421-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Wyświetl dane telemetryczne z Pi malina][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="08421-109">Działania na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="08421-109">Act on the device</span></span>

<span data-ttu-id="08421-110">Na pulpicie nawigacyjnym rozwiązania można wywoływać metod w Twojej Pi malina.</span><span class="sxs-lookup"><span data-stu-id="08421-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="08421-111">Gdy Pi malina łączy się zdalnego rozwiązanie monitorowania, wysyła informacje o metodach obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="08421-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="08421-112">Na pulpicie nawigacyjnym rozwiązania kliknij **urządzeń** do odwiedzenia **urządzeń** strony.</span><span class="sxs-lookup"><span data-stu-id="08421-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="08421-113">Wybierz użytkownika malinowe Pi w **listę urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="08421-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="08421-114">Następnie wybierz pozycję **metody**:</span><span class="sxs-lookup"><span data-stu-id="08421-114">Then choose **Methods**:</span></span>

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

- <span data-ttu-id="08421-116">Na **wywołania metody** wybierz pozycję **LightBlink** w **metody** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="08421-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="08421-117">Wybierz **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="08421-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="08421-118">Symulator wyświetla komunikat w konsoli za pośrednictwem malina Pi.</span><span class="sxs-lookup"><span data-stu-id="08421-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="08421-119">Aplikacja na Pi malina wysyła potwierdzenie z powrotem do pulpitu nawigacyjnego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="08421-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Pokaż historię — metoda][img-method-history]

- <span data-ttu-id="08421-121">Możesz przełączyć LED włączać i wyłączać za pomocą **ChangeLightStatus** metody z **LightStatusValue** ustawioną **1** dla na lub **0** dla off.</span><span class="sxs-lookup"><span data-stu-id="08421-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="08421-122">Pozostawienie zdalnego monitorowania działającej na koncie Azure są rozliczane dla przy uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="08421-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="08421-123">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="08421-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="08421-124">Usuwanie wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="08421-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md