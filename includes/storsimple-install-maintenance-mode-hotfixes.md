<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9d765-101">tooinstall poprawki trybu konserwacji programu Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="9d765-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9d765-102">W trybie konserwacji najpierw należy tooapply hello poprawki na jeden kontroler i na tekst hello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="9d765-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="9d765-103">Umieść hello urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9d765-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="9d765-104">Zobacz [krok 2: tryb konserwacji wprowadź](../articles/storsimple/storsimple-update-device.md#step2) instrukcje na temat tooenter tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9d765-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="9d765-105">tooapply hello poprawek, wpisz:</span><span class="sxs-lookup"><span data-stu-id="9d765-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="9d765-106">Po wyświetleniu monitu podaj hello ścieżki toohello udostępniony folder sieciowy zawierający pliki poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="9d765-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="9d765-107">Pojawi się monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="9d765-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="9d765-108">Typ **Y** tooproceed hello instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="9d765-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="9d765-109">Po zastosowano poprawki hello na jeden kontroler, logowanie toohello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="9d765-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="9d765-110">Zastosuj poprawkę hello, jak hello poprzedniego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="9d765-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="9d765-111">Po zastosowaniu poprawki hello, wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9d765-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="9d765-112">Zobacz [krok 4: tryb konserwacji zakończenia](../articles/storsimple/storsimple-update-device.md#step4) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="9d765-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

