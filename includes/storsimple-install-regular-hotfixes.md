<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="df75d-101">Aby zainstalować regularne poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="df75d-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="df75d-102">Łączenie z konsolą szeregową urządzenia.</span><span class="sxs-lookup"><span data-stu-id="df75d-102">Connect to the device serial console.</span></span> <span data-ttu-id="df75d-103">Aby uzyskać więcej informacji, zobacz [krok 1: łączenie z konsolą szeregową](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="df75d-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="df75d-104">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="df75d-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="df75d-105">Wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="df75d-105">Type the password.</span></span> <span data-ttu-id="df75d-106">Domyślne hasło jest **Password1**.</span><span class="sxs-lookup"><span data-stu-id="df75d-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="df75d-107">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="df75d-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="df75d-108">To polecenie dotyczy tylko regularne poprawki.</span><span class="sxs-lookup"><span data-stu-id="df75d-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="df75d-109">Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="df75d-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="df75d-110">Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji; jednak tryb failover nie wpłynie na dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="df75d-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="df75d-111">Po wyświetleniu monitu podaj ścieżkę do udostępnionego folderu sieciowego, który zawiera pliki poprawek.</span><span class="sxs-lookup"><span data-stu-id="df75d-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="df75d-112">Pojawi się monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="df75d-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="df75d-113">Typ **Y** kontynuować instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="df75d-113">Type **Y** to proceed with the hotfix installation.</span></span>

