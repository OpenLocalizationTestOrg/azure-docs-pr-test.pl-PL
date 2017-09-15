#### <a name="to-stop-and-start-a-virtual-device"></a><span data-ttu-id="daed5-101">Aby zatrzymać i ponownie uruchomić urządzenie wirtualne</span><span class="sxs-lookup"><span data-stu-id="daed5-101">To stop and start a virtual device</span></span>
<span data-ttu-id="daed5-102">Aby zatrzymać urządzenie wirtualne, kliknij jego nazwę, a następnie kliknij pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="daed5-102">To stop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="daed5-103">Stan zamykanego urządzenia wirtualnego to **Zatrzymywanie**.</span><span class="sxs-lookup"><span data-stu-id="daed5-103">While the virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="daed5-104">Stan zamkniętego urządzenia wirtualnego to **Zatrzymane**.</span><span class="sxs-lookup"><span data-stu-id="daed5-104">After the virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="daed5-105">Użyj poniższych poleceń cmdlet do zatrzymywania i uruchamiania urządzenia wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="daed5-105">Use the following cmdlets to stop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a><span data-ttu-id="daed5-106">Aby ponownie uruchomić urządzenia wirtualne</span><span class="sxs-lookup"><span data-stu-id="daed5-106">To restart a virtual device</span></span>
<span data-ttu-id="daed5-107">Jeśli urządzenie wirtualne działa i chcesz uruchomić je ponownie, kliknij nazwę urządzenia, a następnie kliknij pozycję **Uruchom ponownie**.</span><span class="sxs-lookup"><span data-stu-id="daed5-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="daed5-108">Stan ponownie uruchamianego urządzenia wirtualnego to **Ponowne uruchamianie**.</span><span class="sxs-lookup"><span data-stu-id="daed5-108">While the virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="daed5-109">Gdy urządzenie wirtualne jest gotowe do użycia, jego stan to **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="daed5-109">When the virtual device is ready for you to use, its status is **Running**.</span></span>

<span data-ttu-id="daed5-110">Użyj poniższego polecenia cmdlet, aby ponownie uruchomić urządzenie wirtualne.</span><span class="sxs-lookup"><span data-stu-id="daed5-110">Use the following cmdlet to restart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

