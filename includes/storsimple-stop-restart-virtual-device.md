#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="290c4-101">toostop i rozpocząć urządzenie wirtualne</span><span class="sxs-lookup"><span data-stu-id="290c4-101">toostop and start a virtual device</span></span>
<span data-ttu-id="290c4-102">toostop urządzenia wirtualnego, kliknij jego nazwę, a następnie kliknij przycisk **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="290c4-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="290c4-103">Gdy urządzenie wirtualne hello jest zamykany, jego stan jest **zatrzymywanie**.</span><span class="sxs-lookup"><span data-stu-id="290c4-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="290c4-104">Po wyłączeniu urządzenia wirtualnego hello jego stan jest **zatrzymane**.</span><span class="sxs-lookup"><span data-stu-id="290c4-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="290c4-105">Użyj następującego polecenia cmdlet toostop hello i uruchamiania urządzenia wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="290c4-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="290c4-106">toorestart urządzenie wirtualne</span><span class="sxs-lookup"><span data-stu-id="290c4-106">toorestart a virtual device</span></span>
<span data-ttu-id="290c4-107">Gdy urządzenie wirtualne działa i chcesz toorestart, kliknij jego nazwę, a następnie kliknij **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="290c4-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="290c4-108">Podczas ponownego uruchamiania urządzenia wirtualnego hello, jego stan jest **ponowne**.</span><span class="sxs-lookup"><span data-stu-id="290c4-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="290c4-109">Gdy urządzenie wirtualne hello jest gotowy do możesz toouse, jego stan jest **systemem**.</span><span class="sxs-lookup"><span data-stu-id="290c4-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="290c4-110">Użyj następującego polecenia cmdlet toorestart urządzenie wirtualne hello.</span><span class="sxs-lookup"><span data-stu-id="290c4-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

