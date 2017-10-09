<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="8d59a-101">tooinstall regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="8d59a-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="8d59a-102">Otwieranie konsoli szeregowej urządzenia hello i wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="8d59a-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="8d59a-103">Wpisz hasło hello.</span><span class="sxs-lookup"><span data-stu-id="8d59a-103">Type hello password.</span></span> <span data-ttu-id="8d59a-104">Witaj domyślne hasło jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="8d59a-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="8d59a-105">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="8d59a-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="8d59a-106">Jeśli aktualizacje są dostępne i czy są aktualizacje hello destrukcyjne lub Brak, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="8d59a-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="8d59a-107">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="8d59a-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="8d59a-108">rozpocznie się proces aktualizacji Hello.</span><span class="sxs-lookup"><span data-stu-id="8d59a-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="8d59a-109">Polecenie to ma zastosowanie tylko tooregular aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="8d59a-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="8d59a-110">Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="8d59a-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="8d59a-111">Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji hello; jednak hello trybu failover nie wpłynie na dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="8d59a-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

