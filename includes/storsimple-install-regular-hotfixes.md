<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b17cd-101">tooinstall regularne poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="b17cd-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b17cd-102">Łączenie z konsolą szeregową urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="b17cd-102">Connect toohello device serial console.</span></span> <span data-ttu-id="b17cd-103">Aby uzyskać więcej informacji, zobacz [krok 1: połączenie konsoli szeregowej toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="b17cd-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="b17cd-104">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="b17cd-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b17cd-105">Wpisz hasło hello.</span><span class="sxs-lookup"><span data-stu-id="b17cd-105">Type hello password.</span></span> <span data-ttu-id="b17cd-106">Witaj domyślne hasło jest **Password1**.</span><span class="sxs-lookup"><span data-stu-id="b17cd-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="b17cd-107">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="b17cd-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="b17cd-108">Polecenie to ma zastosowanie tylko tooregular poprawki.</span><span class="sxs-lookup"><span data-stu-id="b17cd-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="b17cd-109">Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="b17cd-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="b17cd-110">Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji hello; jednak hello trybu failover nie wpłynie na dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="b17cd-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="b17cd-111">Po wyświetleniu monitu podaj hello ścieżki toohello udostępniony folder sieciowy zawierający pliki poprawek hello.</span><span class="sxs-lookup"><span data-stu-id="b17cd-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="b17cd-112">Pojawi się monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="b17cd-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="b17cd-113">Typ **Y** tooproceed hello instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="b17cd-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

