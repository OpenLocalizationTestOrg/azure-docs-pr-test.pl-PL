<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="5c192-101">Aby zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="5c192-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="5c192-102">Otwieranie konsoli szeregowej urządzenia i wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="5c192-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="5c192-103">Wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="5c192-103">Type the password.</span></span> <span data-ttu-id="5c192-104">Domyślne hasło jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="5c192-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="5c192-105">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="5c192-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="5c192-106">Jeśli aktualizacje są dostępne i czy są aktualizacje destrukcyjne lub Brak, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="5c192-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="5c192-107">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="5c192-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="5c192-108">Rozpocznie się proces aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5c192-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="5c192-109">To polecenie dotyczy tylko regularne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="5c192-109">This command applies only to regular updates.</span></span> <span data-ttu-id="5c192-110">Uruchom to polecenie na tylko jeden kontroler, ale zostaną zaktualizowane obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="5c192-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="5c192-111">Tryb failover kontrolera mogą pojawić się podczas procesu aktualizacji; jednak tryb failover nie wpłynie na dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="5c192-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

