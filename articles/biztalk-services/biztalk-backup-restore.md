---
title: "aaaCreate i przywracania kopii zapasowej w usługach BizTalk | Dokumentacja firmy Microsoft"
description: "Usługi BizTalk Services zawiera kopii zapasowej i przywracania. Dowiedz się, jak toocreate i przywracania kopii zapasowej i określić kopiami zapasowymi. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="92ae1-105">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="92ae1-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="92ae1-106">Usługi BizTalk Azure obejmuje możliwości tworzenia kopii zapasowych i przywracania.</span><span class="sxs-lookup"><span data-stu-id="92ae1-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="92ae1-107">W tym temacie opisano, jak toobackup i przywracania usługi BizTalk Services przy użyciu hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="92ae1-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="92ae1-108">Można również tworzyć kopie zapasowe usługi BizTalk Services przy użyciu hello [interfejsu API REST usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="92ae1-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="92ae1-109">Połączenia hybrydowe nie kopii zapasowej, niezależnie od hello Edition.</span><span class="sxs-lookup"><span data-stu-id="92ae1-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="92ae1-110">Należy ponownie utworzyć połączeń hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="92ae1-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="92ae1-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="92ae1-111">Before you Begin</span></span>
* <span data-ttu-id="92ae1-112">Kopii zapasowej i przywracania może nie być dostępne dla wszystkich wersji.</span><span class="sxs-lookup"><span data-stu-id="92ae1-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="92ae1-113">Zobacz [usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="92ae1-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="92ae1-114">Przy użyciu hello klasycznego portalu Azure, możesz utworzyć kopię zapasową na żądanie lub utworzyć zaplanowaną kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="92ae1-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="92ae1-115">Wykonaj kopię zapasową zawartości może być przywrócona toohello tej samej usługi BizTalk lub tooa nową usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="92ae1-116">toorestore hello usługi BizTalk przy użyciu powitalne nazwę istniejącej usługi BizTalk hello muszą zostać usunięte, a nazwa hello musi być dostępne.</span><span class="sxs-lookup"><span data-stu-id="92ae1-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="92ae1-117">Po usunięciu usługi BizTalk, może potrwać dłużej, niż żądana dla hello takie same nazwy toobe dostępne.</span><span class="sxs-lookup"><span data-stu-id="92ae1-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="92ae1-118">Jeśli nie może czekać na powitania sama nazwa toobe dostępne, a następnie przywrócić tooa nową usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="92ae1-119">Usługi BizTalk Services może być przywrócona toohello tej samej wersji lub nowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="92ae1-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="92ae1-120">Przywracanie usługi BizTalk Services tooa niższej wersji z po hello tworzenia kopii zapasowej, nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="92ae1-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="92ae1-121">Na przykład kopii zapasowej przy użyciu hello podstawowych wydanie można przywrócić toohello Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="92ae1-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="92ae1-122">Kopii zapasowej przy użyciu hello Premium Edition nie może być przywrócona toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="92ae1-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="92ae1-123">numery kontroli EDI Hello kopię zapasową toomaintain ciągłości hello numery kontroli.</span><span class="sxs-lookup"><span data-stu-id="92ae1-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="92ae1-124">Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej hello, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="92ae1-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="92ae1-125">Partia ma aktywne wiadomości, proces partii hello **przed** wykonywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="92ae1-126">Podczas tworzenia kopii zapasowej (jako wymagane lub zaplanowane), wiadomości w partiach nigdy nie są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="92ae1-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="92ae1-127">**Jeśli wykonywana jest kopia zapasowa z active wiadomości w partii, te komunikaty nie kopii zapasowej i w związku z tym zostaną utracone.**</span><span class="sxs-lookup"><span data-stu-id="92ae1-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="92ae1-128">Opcjonalnie: W hello Portal usługi BizTalk, Zatrzymaj wszystkie operacje zarządzania.</span><span class="sxs-lookup"><span data-stu-id="92ae1-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="92ae1-129">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-129">Create a backup</span></span>
<span data-ttu-id="92ae1-130">Kopię zapasową można wykonać w dowolnym momencie i całkowicie jest kontrolowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92ae1-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="92ae1-131">W tej sekcji przedstawiono hello kroki toocreate kopii zapasowych przy użyciu hello Azure classic portal, w tym:</span><span class="sxs-lookup"><span data-stu-id="92ae1-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="92ae1-132">Na żądanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="92ae1-133">Planowanie tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="92ae1-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="92ae1-134"><a name="backupnow"></a>Na żądanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="92ae1-135">Hello klasycznego portalu Azure, wybierz **usługi BizTalk Services**, a następnie wybierz hello ma toobackup usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="92ae1-136">W hello **pulpitu nawigacyjnego** wybierz opcję **kopię zapasową** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="92ae1-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="92ae1-137">Wprowadź nazwę kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-137">Enter a backup name.</span></span> <span data-ttu-id="92ae1-138">Na przykład wprowadź *myBizTalkService*BU*data*.</span><span class="sxs-lookup"><span data-stu-id="92ae1-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="92ae1-139">Wybierz konto magazynu obiektów blob i wybierz hello znacznikiem wyboru toostart hello w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="92ae1-140">Po wykonaniu kopii zapasowej hello kontener z wprowadzona nazwa hello kopii zapasowej jest tworzony w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="92ae1-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="92ae1-141">Ten kontener zawiera konfiguracji kopii zapasowej usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="92ae1-142"><a name="backupschedule"></a>Planowanie tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="92ae1-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="92ae1-143">Hello klasycznego portalu Azure, wybierz **usługi BizTalk Services**, wybierz hello nazwa usługi BizTalk mają tooschedule hello tworzenia kopii zapasowej, a następnie wybierz hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="92ae1-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="92ae1-144">Zestaw hello **stanu kopii zapasowej** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="92ae1-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="92ae1-145">Wybierz hello **konta magazynu** toostore hello kopii zapasowej, należy wprowadzić hello **częstotliwość** toocreate Witaj i jak długo kopii zapasowych hello tookeep (**dni przechowywania**):</span><span class="sxs-lookup"><span data-stu-id="92ae1-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="92ae1-146">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="92ae1-146">**Notes**</span></span>     
   
   * <span data-ttu-id="92ae1-147">W **dni przechowywania**, hello okres przechowywania musi być większa niż częstotliwość wykonywania kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="92ae1-148">Wybierz **zawsze Zachowuj co najmniej jedną kopię zapasową**nawet wtedy, gdy po upływie okresu przechowywania hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="92ae1-149">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="92ae1-149">Select **Save**.</span></span>

<span data-ttu-id="92ae1-150">Po uruchomieniu zaplanowanego zadania tworzenia kopii zapasowej, tworzy kontener (toostore dane kopii zapasowej) na koncie magazynu hello wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="92ae1-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="92ae1-151">nosi nazwę kontenera hello Hello *usługi BizTalk Nazwa daty i godziny*.</span><span class="sxs-lookup"><span data-stu-id="92ae1-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="92ae1-152">Jeśli wyświetlane hello pulpit nawigacyjny usługi BizTalk **** stanu:</span><span class="sxs-lookup"><span data-stu-id="92ae1-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Stan ostatniej kopii zapasowej według harmonogramu][BackupStatus] 

<span data-ttu-id="92ae1-154">Witaj łącze powoduje otwarcie hello dzienniki operacji usług zarządzania toohelp Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="92ae1-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="92ae1-155">Zobacz [usługi BizTalk Services: Rozwiązywanie problemów przy użyciu dzienników operacji](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="92ae1-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="92ae1-156">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="92ae1-156">Restore</span></span>
<span data-ttu-id="92ae1-157">Można przywrócić kopii zapasowych z hello klasycznego portalu Azure lub hello [przywrócić usług BizTalk — wersja interfejsu API REST usługi](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="92ae1-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="92ae1-158">Ta sekcja zawiera hello toorestore czynności przy użyciu klasycznego portalu hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="92ae1-159">Przed przywróceniem kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-159">Before restoring a backup</span></span>
* <span data-ttu-id="92ae1-160">Nowe śledzenie, archiwizacji i monitorowania magazynów można wprowadzić podczas przywracania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="92ae1-161">Witaj, te same dane środowiska uruchomieniowego EDI jest przywracane.</span><span class="sxs-lookup"><span data-stu-id="92ae1-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="92ae1-162">Kopia zapasowa środowiska uruchomieniowego EDI Hello przechowuje numery kontroli hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="92ae1-163">numery kontroli Hello przywrócić są w kolejności od chwili hello hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="92ae1-164">Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej hello, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="92ae1-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="92ae1-165">Przywracanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-165">Restore a backup</span></span>
1. <span data-ttu-id="92ae1-166">Hello klasycznego portalu Azure, wybierz **nowy** > **usługi aplikacji** > **usługi BizTalk** > **przywracania** :</span><span class="sxs-lookup"><span data-stu-id="92ae1-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Przywracanie kopii zapasowej][Restore]
2. <span data-ttu-id="92ae1-168">W **kopii zapasowej adresu URL**, wybierz ikonę folderu hello i rozwiń konto usługi Azure storage hello czy magazyny hello kopia zapasowa konfiguracji usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="92ae1-169">Rozwiń kontener hello i w okienku po prawej stronie powitania, wybierz hello odpowiadającego Utwórz kopię zapasową pliku txt.</span><span class="sxs-lookup"><span data-stu-id="92ae1-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="92ae1-170">Wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="92ae1-170">Select **Open**.</span></span>
3. <span data-ttu-id="92ae1-171">Na powitania **usługi BizTalk przywracania** wprowadź **nazwa usługi BizTalk** i sprawdź hello **adresu URL domeny**, **wersji**i **Region** dla hello przywrócić usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="92ae1-172">**Utwórz nowe wystąpienie bazy danych SQL** dla hello śledzenia bazy danych:</span><span class="sxs-lookup"><span data-stu-id="92ae1-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="92ae1-173">Wybierz strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="92ae1-174">Sprawdź nazwę hello hello bazy danych SQL, wprowadź powitania serwera fizycznego, której zostanie utworzona hello bazy danych SQL i nazwę użytkownika/hasło dla tego serwera.</span><span class="sxs-lookup"><span data-stu-id="92ae1-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="92ae1-175">Wersja bazy danych SQL hello tooconfigure, rozmiar i inne właściwości, wybierz opcję **skonfigurować zaawansowane ustawienia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="92ae1-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="92ae1-176">Wybierz strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="92ae1-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="92ae1-177">Utwórz nowe konto magazynu, lub wprowadź istniejącego konta magazynu hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="92ae1-178">Wybierz hello znacznikiem wyboru toostart hello przywracania.</span><span class="sxs-lookup"><span data-stu-id="92ae1-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="92ae1-179">Po pomyślnym zakończeniu przywracania hello, nową usługę BizTalk znajduje się w stanie wstrzymania na stronie usługi BizTalk Services hello hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="92ae1-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="92ae1-180"><a name="postrestore"></a>Po przywróceniu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="92ae1-181">Witaj usługi BizTalk jest zawsze przywracać w **zawieszone** stanu.</span><span class="sxs-lookup"><span data-stu-id="92ae1-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="92ae1-182">W tym stanie można wprowadzać żadnych zmian konfiguracji przed hello nowe środowisko będzie działać, w tym:</span><span class="sxs-lookup"><span data-stu-id="92ae1-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="92ae1-183">Jeśli utworzono usługę BizTalk aplikacji przy użyciu hello Azure SDK usługi BizTalk, może być konieczne tootooupdate hello kontroli dostępu (ACS) poświadczenia w tych toowork aplikacji ze środowiskiem hello przywrócona.</span><span class="sxs-lookup"><span data-stu-id="92ae1-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="92ae1-184">Możesz przywrócić tooreplicate usługi BizTalk istniejącego środowiska usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92ae1-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="92ae1-185">W takiej sytuacji jeśli są skonfigurowane w portalu usługi BizTalk Services z oryginalnego hello umowy, korzystających z folderu źródłowego FTP, może być konieczne tooupdate hello umów w nowo przywrócony hello środowiska toouse folderu FTP innego źródła.</span><span class="sxs-lookup"><span data-stu-id="92ae1-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="92ae1-186">W przeciwnym razie może być tę samą wiadomość hello dwóch różnych umów w trakcie toopull.</span><span class="sxs-lookup"><span data-stu-id="92ae1-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="92ae1-187">Jeśli toohave przywrócić wiele środowisk usługi BizTalk, upewnij się, że docelowa hello poprawne środowisko w aplikacji Visual Studio hello, poleceń cmdlet programu PowerShell, interfejsów API REST lub handlem partnera OM interfejsów API Management.</span><span class="sxs-lookup"><span data-stu-id="92ae1-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="92ae1-188">Jest tooconfigure automatyczne kopie zapasowe dobrym rozwiązaniem w środowisku usługi BizTalk hello nowo przywrócony.</span><span class="sxs-lookup"><span data-stu-id="92ae1-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="92ae1-189">toostart hello usługi BizTalk w hello klasycznego portalu Azure, wybierz hello przywracane usługi BizTalk i wybierz **Wznów** hello paska zadań.</span><span class="sxs-lookup"><span data-stu-id="92ae1-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="92ae1-190">Kopiami zapasowymi</span><span class="sxs-lookup"><span data-stu-id="92ae1-190">What gets backed up</span></span>
<span data-ttu-id="92ae1-191">Po utworzeniu kopii zapasowej hello następujące elementy są kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="92ae1-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="92ae1-192">Elementy kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="92ae1-193">
 <strong>Portal usług Azure BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="92ae1-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="92ae1-194">Konfiguracja i środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="92ae1-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="92ae1-195">Szczegóły partnera i profilu</span><span class="sxs-lookup"><span data-stu-id="92ae1-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="92ae1-196">Umowy z partnerami</span><span class="sxs-lookup"><span data-stu-id="92ae1-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="92ae1-197">Niestandardowe zestawy wdrożony</span><span class="sxs-lookup"><span data-stu-id="92ae1-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="92ae1-198">Mostków wdrożony</span><span class="sxs-lookup"><span data-stu-id="92ae1-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="92ae1-199">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="92ae1-199">Certificates</span></span></li>
<li><span data-ttu-id="92ae1-200">Transformacje wdrożony</span><span class="sxs-lookup"><span data-stu-id="92ae1-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="92ae1-201">Potoki</span><span class="sxs-lookup"><span data-stu-id="92ae1-201">Pipelines</span></span></li>
<li><span data-ttu-id="92ae1-202">Szablony utworzony i zapisany w hello Portal usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="92ae1-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="92ae1-203">X12 mapowania ST01 i GS01</span><span class="sxs-lookup"><span data-stu-id="92ae1-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="92ae1-204">Numery kontroli (EDI)</span><span class="sxs-lookup"><span data-stu-id="92ae1-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="92ae1-205">Wartości AS2 komunikat Micznych</span><span class="sxs-lookup"><span data-stu-id="92ae1-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="92ae1-206">
 <strong>Usługi BizTalk Azure</strong></span><span class="sxs-lookup"><span data-stu-id="92ae1-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="92ae1-207">Certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="92ae1-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="92ae1-208">Dane certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="92ae1-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="92ae1-209">Hasło certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="92ae1-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="92ae1-210">Ustawienia usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="92ae1-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="92ae1-211">Liczba jednostek skali</span><span class="sxs-lookup"><span data-stu-id="92ae1-211">Scale unit count</span></span></li>
<li><span data-ttu-id="92ae1-212">Wersja</span><span class="sxs-lookup"><span data-stu-id="92ae1-212">Edition</span></span></li>
<li><span data-ttu-id="92ae1-213">Wersja produktu:</span><span class="sxs-lookup"><span data-stu-id="92ae1-213">Product Version</span></span></li>
<li><span data-ttu-id="92ae1-214">Region/centrum danych</span><span class="sxs-lookup"><span data-stu-id="92ae1-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="92ae1-215">Dostęp do usługi kontroli (ACS) w przestrzeni nazw i klucza</span><span class="sxs-lookup"><span data-stu-id="92ae1-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="92ae1-216">Parametry połączenia bazy danych śledzenia</span><span class="sxs-lookup"><span data-stu-id="92ae1-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="92ae1-217">Archiwizowanie parametry połączenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="92ae1-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="92ae1-218">Monitorowanie parametrów połączenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="92ae1-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="92ae1-219">
 <strong>Dodatkowe elementy</strong></span><span class="sxs-lookup"><span data-stu-id="92ae1-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="92ae1-220">Śledzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="92ae1-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="92ae1-221">Po utworzeniu hello usługi BizTalk hello śledzenia Szczegóły bazy danych są wprowadzane w tym powitania serwera bazy danych SQL Azure i hello śledzenia nazwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92ae1-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="92ae1-222">Witaj śledzenia bazy danych nie jest automatycznie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="92ae1-223">
<strong>Ważne</strong></span><span class="sxs-lookup"><span data-stu-id="92ae1-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="92ae1-224">Jeśli hello śledzenia bazy danych są usuwane i hello odzyskane potrzeb bazy danych, musi istnieć poprzedniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="92ae1-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="92ae1-225">Jeśli kopia zapasowa nie istnieje, hello śledzenia bazy danych i jego dane nie są możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="92ae1-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="92ae1-226">W takiej sytuacji należy utworzyć nową bazę danych śledzenia z hello samej nazwie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92ae1-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="92ae1-227">Replikacja geograficzna jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="92ae1-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="92ae1-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92ae1-228">Next</span></span>
<span data-ttu-id="92ae1-229">usługi BizTalk Services Azure toocreate w hello Azure przejdź do portalu klasycznego zbyt[usługi BizTalk Services: klasycznego portalu Azure za pomocą udostępniania](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="92ae1-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="92ae1-230">toostart tworzenia aplikacji, przejdź do zbyt[usług BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="92ae1-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="92ae1-231">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="92ae1-231">See Also</span></span>
* [<span data-ttu-id="92ae1-232">Usługi BizTalk kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="92ae1-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="92ae1-233">Przywracanie z kopii zapasowej usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="92ae1-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="92ae1-234">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="92ae1-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="92ae1-235">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="92ae1-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="92ae1-236">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="92ae1-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="92ae1-237">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="92ae1-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="92ae1-238">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="92ae1-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="92ae1-239">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="92ae1-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="92ae1-240">Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="92ae1-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

