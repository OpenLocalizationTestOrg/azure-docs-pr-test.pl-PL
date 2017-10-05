---
title: "Tworzenie i przywracanie kopii zapasowej w usługach BizTalk | Dokumentacja firmy Microsoft"
description: "Usługi BizTalk Services zawiera kopii zapasowej i przywracania. Informacje o sposobie tworzenia i przywracania kopii zapasowej, aby ustalić kopiami zapasowymi. MABS, WABS"
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
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="cccd2-105">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="cccd2-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="cccd2-106">Usługi BizTalk Azure obejmuje możliwości tworzenia kopii zapasowych i przywracania.</span><span class="sxs-lookup"><span data-stu-id="cccd2-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="cccd2-107">W tym temacie opisano, jak utworzyć kopii zapasowej i przywracania usługi BizTalk Services przy użyciu klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cccd2-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="cccd2-108">Można również tworzyć kopie zapasowe przy użyciu usługi BizTalk Services [interfejsu API REST usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="cccd2-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="cccd2-109">Połączenia hybrydowe nie kopii zapasowej, niezależnie od wersji.</span><span class="sxs-lookup"><span data-stu-id="cccd2-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="cccd2-110">Należy ponownie utworzyć połączeń hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="cccd2-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="cccd2-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="cccd2-111">Before you Begin</span></span>
* <span data-ttu-id="cccd2-112">Kopii zapasowej i przywracania może nie być dostępne dla wszystkich wersji.</span><span class="sxs-lookup"><span data-stu-id="cccd2-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="cccd2-113">Zobacz [usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="cccd2-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="cccd2-114">Przy użyciu klasycznego portalu Azure, możesz utworzyć kopię zapasową na żądanie lub utworzyć zaplanowaną kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="cccd2-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="cccd2-115">Zawartość kopii zapasowej można przywrócić do tej samej usługi BizTalk lub nową usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="cccd2-116">Aby przywrócić usługi BizTalk, przy użyciu takiej samej nazwie, należy usunąć istniejącej usługi BizTalk i nazwa musi być dostępna.</span><span class="sxs-lookup"><span data-stu-id="cccd2-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="cccd2-117">Po usunięciu usługi BizTalk, może potrwać dłużej, niż żądana dla tej samej nazwie, które mają być dostępne.</span><span class="sxs-lookup"><span data-stu-id="cccd2-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="cccd2-118">Jeśli użytkownik nie może czekać na tej samej nazwie, które mają być dostępne, następnie przywróć nową usługę BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="cccd2-119">Usługi BizTalk Services można przywrócić do tej samej wersji lub nowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="cccd2-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="cccd2-120">Przywracanie usługi BizTalk Services do niższej wersji, z po wykonaniu kopii zapasowej, nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cccd2-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="cccd2-121">Na przykład można przywrócić kopii zapasowej przy użyciu podstawowych wydanie do wersji Premium.</span><span class="sxs-lookup"><span data-stu-id="cccd2-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="cccd2-122">Nie można przywrócić kopii zapasowej przy użyciu wersji Premium do Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="cccd2-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="cccd2-123">Numery kontroli EDI kopię zapasową do kontynuacji numery kontroli.</span><span class="sxs-lookup"><span data-stu-id="cccd2-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="cccd2-124">Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="cccd2-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="cccd2-125">Partia ma aktywne wiadomości, proces partii **przed** wykonywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="cccd2-126">Podczas tworzenia kopii zapasowej (jako wymagane lub zaplanowane), wiadomości w partiach nigdy nie są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="cccd2-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="cccd2-127">**Jeśli wykonywana jest kopia zapasowa z active wiadomości w partii, te komunikaty nie kopii zapasowej i w związku z tym zostaną utracone.**</span><span class="sxs-lookup"><span data-stu-id="cccd2-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="cccd2-128">Opcjonalnie: W portalu usługi BizTalk, Zatrzymaj wszystkie operacje zarządzania.</span><span class="sxs-lookup"><span data-stu-id="cccd2-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="cccd2-129">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-129">Create a backup</span></span>
<span data-ttu-id="cccd2-130">Kopię zapasową można wykonać w dowolnym momencie i całkowicie jest kontrolowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cccd2-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="cccd2-131">W tej sekcji przedstawiono kroki, aby utworzyć kopie zapasowe przy użyciu klasycznego portalu Azure, w tym:</span><span class="sxs-lookup"><span data-stu-id="cccd2-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="cccd2-132">Na żądanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="cccd2-133">Planowanie tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="cccd2-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="cccd2-134"><a name="backupnow"></a>Na żądanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="cccd2-135">W klasycznym portalu Azure, wybierz **usługi BizTalk Services**, a następnie wybierz usługę BizTalk, aby utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="cccd2-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="cccd2-136">W **pulpitu nawigacyjnego** wybierz opcję **kopię zapasową** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="cccd2-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="cccd2-137">Wprowadź nazwę kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-137">Enter a backup name.</span></span> <span data-ttu-id="cccd2-138">Na przykład wprowadź *myBizTalkService*BU*data*.</span><span class="sxs-lookup"><span data-stu-id="cccd2-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="cccd2-139">Wybierz konto magazynu obiektów blob, a następnie wybierz znacznik wyboru, aby rozpocząć tworzenie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="cccd2-140">Po wykonaniu kopii zapasowej, kontener z kopii zapasowej wprowadzona nazwa jest tworzony na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="cccd2-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="cccd2-141">Ten kontener zawiera konfiguracji kopii zapasowej usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="cccd2-142"><a name="backupschedule"></a>Planowanie tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="cccd2-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="cccd2-143">W klasycznym portalu Azure, wybierz **usługi BizTalk Services**, wybierz nazwę usługi BizTalk, aby zaplanować tworzenie kopii zapasowej, a następnie wybierz **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="cccd2-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="cccd2-144">Ustaw **kopię zapasową stanu** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="cccd2-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="cccd2-145">Wybierz **konta magazynu** zapisana kopia zapasowa, wprowadź **częstotliwość** do tworzenia kopii zapasowych, a czas przechowywania kopii zapasowych (**dni przechowywania**):</span><span class="sxs-lookup"><span data-stu-id="cccd2-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="cccd2-146">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="cccd2-146">**Notes**</span></span>     
   
   * <span data-ttu-id="cccd2-147">W **dni przechowywania**, okres przechowywania musi być większa niż częstotliwość wykonywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="cccd2-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="cccd2-148">Wybierz **zawsze Zachowuj co najmniej jedną kopię zapasową**nawet wtedy, gdy po upływie okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="cccd2-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="cccd2-149">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cccd2-149">Select **Save**.</span></span>

<span data-ttu-id="cccd2-150">Po uruchomieniu zaplanowanego zadania tworzenia kopii zapasowej, tworzy kontener (do przechowywania danych kopii zapasowej) na koncie magazynu, który został wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="cccd2-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="cccd2-151">Nazwa kontenera o nazwie *usługi BizTalk Nazwa daty i godziny*.</span><span class="sxs-lookup"><span data-stu-id="cccd2-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="cccd2-152">Jeśli wyświetlane na pulpicie nawigacyjnym usługi BizTalk **** stanu:</span><span class="sxs-lookup"><span data-stu-id="cccd2-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Stan ostatniej kopii zapasowej według harmonogramu][BackupStatus] 

<span data-ttu-id="cccd2-154">To łącze powoduje otwarcie dzienniki operacji usług zarządzania do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cccd2-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="cccd2-155">Zobacz [usługi BizTalk Services: Rozwiązywanie problemów przy użyciu dzienników operacji](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="cccd2-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="cccd2-156">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="cccd2-156">Restore</span></span>
<span data-ttu-id="cccd2-157">Możesz przywracać kopie zapasowe, z klasycznego portalu Azure lub [przywrócić usług BizTalk — wersja interfejsu API REST usługi](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="cccd2-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="cccd2-158">W tej sekcji wymieniono kroki, aby przywrócić przy użyciu klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="cccd2-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="cccd2-159">Przed przywróceniem kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-159">Before restoring a backup</span></span>
* <span data-ttu-id="cccd2-160">Nowe śledzenie, archiwizacji i monitorowania magazynów można wprowadzić podczas przywracania usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="cccd2-161">Te same dane środowiska uruchomieniowego EDI został przywrócony.</span><span class="sxs-lookup"><span data-stu-id="cccd2-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="cccd2-162">Kopia zapasowa środowiska uruchomieniowego EDI przechowuje numery kontroli.</span><span class="sxs-lookup"><span data-stu-id="cccd2-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="cccd2-163">Numery przywróconej kontroli znajdują się w sekwencji z tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="cccd2-164">Wiadomości są przetwarzane po utworzeniu ostatniej kopii zapasowej, przywrócenia tej kopii zapasowej zawartości może spowodować numery zduplikowane kontroli.</span><span class="sxs-lookup"><span data-stu-id="cccd2-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="cccd2-165">Przywracanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-165">Restore a backup</span></span>
1. <span data-ttu-id="cccd2-166">W klasycznym portalu Azure, wybierz **nowy** > **usługi aplikacji** > **usługi BizTalk** > **przywrócić**:</span><span class="sxs-lookup"><span data-stu-id="cccd2-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Przywracanie kopii zapasowej][Restore]
2. <span data-ttu-id="cccd2-168">W **kopii zapasowej adresu URL**, wybierz ikonę folderu i rozwiń konto magazynu Azure, która przechowuje kopię zapasową konfiguracji usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="cccd2-169">Rozwiń kontener i w okienku po prawej stronie, wybierz odpowiedni plik kopii zapasowej .txt.</span><span class="sxs-lookup"><span data-stu-id="cccd2-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="cccd2-170">Wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="cccd2-170">Select **Open**.</span></span>
3. <span data-ttu-id="cccd2-171">Na **usługi BizTalk przywracania** wprowadź **nazwa usługi BizTalk** i sprawdź **adresu URL domeny**, **wersji**, i **Region** przywróconej usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="cccd2-172">**Utwórz nowe wystąpienie bazy danych SQL** dla bazy danych śledzenia:</span><span class="sxs-lookup"><span data-stu-id="cccd2-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="cccd2-173">Wybierz strzałkę dalej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-173">Select the next arrow.</span></span>
4. <span data-ttu-id="cccd2-174">Sprawdź nazwę bazy danych SQL, wprowadź serwerze fizycznym, w której zostanie utworzona z bazą danych SQL i nazwę użytkownika/hasło dla tego serwera.</span><span class="sxs-lookup"><span data-stu-id="cccd2-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="cccd2-175">Jeśli chcesz skonfigurować wersji bazy danych SQL, rozmiar i inne właściwości, wybierz **skonfigurować zaawansowane ustawienia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="cccd2-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="cccd2-176">Wybierz strzałkę dalej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-176">Select the next arrow.</span></span>

1. <span data-ttu-id="cccd2-177">Utwórz nowe konto magazynu, lub wprowadź istniejącego konta magazynu dla usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="cccd2-178">Wybierz znacznik wyboru, aby rozpocząć przywracanie.</span><span class="sxs-lookup"><span data-stu-id="cccd2-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="cccd2-179">Po pomyślnym zakończeniu przywracania, nową usługę BizTalk znajduje się w stanie wstrzymania na stronie usługi BizTalk Services w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cccd2-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="cccd2-180"><a name="postrestore"></a>Po przywróceniu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="cccd2-181">Usługi BizTalk zawsze jest przywracany **zawieszone** stanu.</span><span class="sxs-lookup"><span data-stu-id="cccd2-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="cccd2-182">W tym stanie można wprowadzać żadnych zmian konfiguracji, zanim nowe środowisko będzie działać, w tym:</span><span class="sxs-lookup"><span data-stu-id="cccd2-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="cccd2-183">Jeśli utworzono usługę BizTalk aplikacji przy użyciu zestawu SDK usługi Azure BizTalk, może być konieczne można zaktualizować poświadczeń kontroli dostępu (ACS) w tych aplikacji, aby pracować z przywróconą środowiska.</span><span class="sxs-lookup"><span data-stu-id="cccd2-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="cccd2-184">Możesz przywrócić usługi BizTalk do replikowania istniejącego środowiska usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="cccd2-185">W takiej sytuacji, jeśli są skonfigurowane w portalu usługi BizTalk Services oryginalnej Umowy, korzystających z folderu źródłowego FTP, może być konieczne Aktualizacja umów w środowisku nowo przywrócony do korzystania z folderu FTP innego źródła.</span><span class="sxs-lookup"><span data-stu-id="cccd2-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="cccd2-186">W przeciwnym razie może być dwóch różnych umów próby pobierać ten sam komunikat.</span><span class="sxs-lookup"><span data-stu-id="cccd2-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="cccd2-187">Jeśli przywracany mają wiele środowisk usługi BizTalk, upewnij się, że poprawne środowisko w aplikacji Visual Studio, poleceń cmdlet programu PowerShell, interfejsów API REST lub handlem partnera OM interfejsów API Management są przeznaczone.</span><span class="sxs-lookup"><span data-stu-id="cccd2-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="cccd2-188">Jest dobrym rozwiązaniem, aby skonfigurować automatyczne tworzenie kopii zapasowych na nowo przywrócony środowiska usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cccd2-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="cccd2-189">Aby uruchomić usługę BizTalk w klasycznym portalu Azure, wybierz usługę BizTalk przywrócone, a następnie wybierz **Wznów** na pasku zadań.</span><span class="sxs-lookup"><span data-stu-id="cccd2-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="cccd2-190">Kopiami zapasowymi</span><span class="sxs-lookup"><span data-stu-id="cccd2-190">What gets backed up</span></span>
<span data-ttu-id="cccd2-191">Po utworzeniu kopii zapasowej, tworzy kopię zapasową następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="cccd2-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="cccd2-192">Elementy kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="cccd2-193">
 <strong>Portal usług Azure BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="cccd2-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cccd2-194">Konfiguracja i środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="cccd2-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cccd2-195">Szczegóły partnera i profilu</span><span class="sxs-lookup"><span data-stu-id="cccd2-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="cccd2-196">Umowy z partnerami</span><span class="sxs-lookup"><span data-stu-id="cccd2-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="cccd2-197">Niestandardowe zestawy wdrożony</span><span class="sxs-lookup"><span data-stu-id="cccd2-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="cccd2-198">Mostków wdrożony</span><span class="sxs-lookup"><span data-stu-id="cccd2-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="cccd2-199">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="cccd2-199">Certificates</span></span></li>
<li><span data-ttu-id="cccd2-200">Transformacje wdrożony</span><span class="sxs-lookup"><span data-stu-id="cccd2-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="cccd2-201">Potoki</span><span class="sxs-lookup"><span data-stu-id="cccd2-201">Pipelines</span></span></li>
<li><span data-ttu-id="cccd2-202">Szablony utworzony i zapisany w portalu usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="cccd2-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="cccd2-203">X12 mapowania ST01 i GS01</span><span class="sxs-lookup"><span data-stu-id="cccd2-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="cccd2-204">Numery kontroli (EDI)</span><span class="sxs-lookup"><span data-stu-id="cccd2-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="cccd2-205">Wartości AS2 komunikat Micznych</span><span class="sxs-lookup"><span data-stu-id="cccd2-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="cccd2-206">
 <strong>Usługi BizTalk Azure</strong></span><span class="sxs-lookup"><span data-stu-id="cccd2-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cccd2-207">Certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="cccd2-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cccd2-208">Dane certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="cccd2-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="cccd2-209">Hasło certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="cccd2-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="cccd2-210">Ustawienia usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="cccd2-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cccd2-211">Liczba jednostek skali</span><span class="sxs-lookup"><span data-stu-id="cccd2-211">Scale unit count</span></span></li>
<li><span data-ttu-id="cccd2-212">Wersja</span><span class="sxs-lookup"><span data-stu-id="cccd2-212">Edition</span></span></li>
<li><span data-ttu-id="cccd2-213">Wersja produktu:</span><span class="sxs-lookup"><span data-stu-id="cccd2-213">Product Version</span></span></li>
<li><span data-ttu-id="cccd2-214">Region/centrum danych</span><span class="sxs-lookup"><span data-stu-id="cccd2-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="cccd2-215">Dostęp do usługi kontroli (ACS) w przestrzeni nazw i klucza</span><span class="sxs-lookup"><span data-stu-id="cccd2-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="cccd2-216">Parametry połączenia bazy danych śledzenia</span><span class="sxs-lookup"><span data-stu-id="cccd2-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="cccd2-217">Archiwizowanie parametry połączenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="cccd2-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="cccd2-218">Monitorowanie parametrów połączenia konta magazynu</span><span class="sxs-lookup"><span data-stu-id="cccd2-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="cccd2-219">
 <strong>Dodatkowe elementy</strong></span><span class="sxs-lookup"><span data-stu-id="cccd2-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cccd2-220">Śledzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="cccd2-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="cccd2-221">Po utworzeniu usługi BizTalk, Szczegóły śledzenia bazy danych zostały wprowadzone, łącznie z serwerem bazy danych SQL Azure i Nazwa śledzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cccd2-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="cccd2-222">Baza danych śledzenia nie jest automatycznie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="cccd2-223">
<strong>Ważne</strong></span><span class="sxs-lookup"><span data-stu-id="cccd2-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="cccd2-224">Jeśli baza danych śledzenia zostaje usunięta i odzyskać na potrzeby bazy danych, musi istnieć poprzedniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cccd2-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="cccd2-225">Jeśli kopia zapasowa nie istnieje, bazy danych śledzenia i jego dane nie są możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="cccd2-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="cccd2-226">W takiej sytuacji należy utworzyć nową bazę danych śledzenia o takiej samej nazwie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cccd2-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="cccd2-227">Replikacja geograficzna jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="cccd2-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="cccd2-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cccd2-228">Next</span></span>
<span data-ttu-id="cccd2-229">Aby utworzyć usługi BizTalk Azure w klasycznym portalu Azure, przejdź do [usługi BizTalk Services: klasycznego portalu Azure za pomocą udostępniania](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="cccd2-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="cccd2-230">Aby rozpocząć tworzenie aplikacji, przejdź do artykułu [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197) (Usługa Azure BizTalk Services).</span><span class="sxs-lookup"><span data-stu-id="cccd2-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="cccd2-231">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cccd2-231">See Also</span></span>
* [<span data-ttu-id="cccd2-232">Usługi BizTalk kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cccd2-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="cccd2-233">Przywracanie z kopii zapasowej usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="cccd2-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="cccd2-234">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="cccd2-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="cccd2-235">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="cccd2-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="cccd2-236">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="cccd2-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="cccd2-237">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="cccd2-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="cccd2-238">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="cccd2-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="cccd2-239">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="cccd2-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="cccd2-240">Jak rozpocząć pracę z zestawem SDK usługi Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="cccd2-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

