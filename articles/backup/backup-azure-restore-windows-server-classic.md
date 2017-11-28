---
title: "aaaRestore tooa danych systemu Windows Server lub klienta systemu Windows z platformy Azure przy użyciu hello klasycznego modelu wdrażania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorestore z systemu Windows Server lub klienta systemu Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="203ee-103">Przywróć pliki tooa systemu Windows server lub komputer kliencki z systemem Windows przy użyciu hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="203ee-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="203ee-104">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="203ee-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="203ee-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="203ee-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="203ee-106">W tym artykule opisano sposób toorecover dane z kopii zapasowej magazynu i przywróć ją tooa serwera lub komputera.</span><span class="sxs-lookup"><span data-stu-id="203ee-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="203ee-107">Począwszy od 2017 marca można już utworzyć magazynów kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="203ee-108">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="203ee-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="203ee-109">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="203ee-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="203ee-110">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="203ee-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="203ee-111">**15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie.</span><span class="sxs-lookup"><span data-stu-id="203ee-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="203ee-112">**Od 1 listopada 2017 roku**:</span><span class="sxs-lookup"><span data-stu-id="203ee-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="203ee-113">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="203ee-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="203ee-114">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="203ee-115">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="203ee-116">toorestore danych, należy użyć Kreatora odzyskiwania danych hello hello agenta usług odzyskiwania Azure firmy Microsoft (MARS).</span><span class="sxs-lookup"><span data-stu-id="203ee-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="203ee-117">Po przywróceniu danych, istnieje możliwość:</span><span class="sxs-lookup"><span data-stu-id="203ee-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="203ee-118">Wykonano przywrócenie danych toohello sam komputera, z których hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="203ee-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="203ee-119">Przywracanie danych tooan alternatywny maszyny.</span><span class="sxs-lookup"><span data-stu-id="203ee-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="203ee-120">W stycznia 2017 r firma Microsoft opublikowała agenta MARS toohello aktualizacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="203ee-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="203ee-121">Wraz z poprawki, ta aktualizacja umożliwia błyskawiczne przywrócić, dzięki czemu można toomount migawki punktu odzyskiwania zapisywalny jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="203ee-122">Następnie można eksplorować hello odzyskiwania woluminu i skopiuj pliki tooa komputera lokalnego co selektywne Przywracanie plików.</span><span class="sxs-lookup"><span data-stu-id="203ee-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="203ee-123">Witaj [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) jest wymagany, jeśli chcesz, aby toouse błyskawicznych przywracania toorestore danych.</span><span class="sxs-lookup"><span data-stu-id="203ee-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="203ee-124">Również dane kopii zapasowej hello muszą być chronione w magazynach wymienione w artykule pomocy technicznej hello ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="203ee-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="203ee-125">Zapoznaj się hello [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) hello aktualną listę ustawień regionalnych, obsługujących błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="203ee-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="203ee-126">Przywracanie błyskawicznych jest **nie** dostępne dla wszystkich ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="203ee-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="203ee-127">Błyskawicznych Przywracanie jest dostępne do użycia w Magazyny usług odzyskiwania w hello portalu Azure i magazyny kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="203ee-128">Jeśli chcesz przywrócić błyskawicznych toouse, Pobierz aktualizację MARS hello i postępuj zgodnie z procedurami hello, w których występuje błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="203ee-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="203ee-129">Użyj błyskawicznych przywrócić toohello danych toorecover tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="203ee-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="203ee-130">Jeśli przypadkowo usunięto toorestore plików i chcą go toohello kroki tej samej maszyny (z którego hello tworzenia kopii zapasowej), po hello pomoże Ci odzyskać dane hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="203ee-131">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w.</span><span class="sxs-lookup"><span data-stu-id="203ee-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="203ee-132">Jeśli nie znasz, którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="203ee-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="203ee-133">Aplikacja klasyczna Hello powinny być wyświetlane w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="203ee-134">Kliknij przycisk **odzyskać dane** toostart hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="203ee-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="203ee-136">Na powitania **wprowadzenie** okienka, toorestore hello danych toohello tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="203ee-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Wybierz ten serwer opcja toorestore hello danych toohello tym samym komputerze](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="203ee-138">Na powitania **wybierz tryb odzyskiwania** okienku wybierz **poszczególnych plików i folderów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="203ee-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="203ee-140">Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="203ee-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="203ee-141">Witaj kalendarza wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="203ee-142">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="203ee-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="203ee-143">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="203ee-144">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="203ee-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Data i woluminu](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="203ee-146">Po wybraniu toorestore punktu odzyskiwania powitania kliknij **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="203ee-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="203ee-147">Kopia zapasowa Azure instaluje punkt odzyskiwania lokalne powitania i używa go jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="203ee-148">Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.</span><span class="sxs-lookup"><span data-stu-id="203ee-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="203ee-150">W Eksploratorze Windows, skopiować pliki hello i/lub folderów toorestore a następnie wkleić je tooany lokalizacji toohello lokalnego serwera lub komputera.</span><span class="sxs-lookup"><span data-stu-id="203ee-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="203ee-151">Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="203ee-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Skopiuj i Wklej pliki i foldery z lokalizacji toolocal zainstalowanego woluminu](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="203ee-153">Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="203ee-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="203ee-154">Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="203ee-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Odinstaluj hello woluminu i Potwierdź](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="203ee-156">Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanego przez 6 godzin od czasu hello, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="203ee-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="203ee-157">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="203ee-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="203ee-158">Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.</span><span class="sxs-lookup"><span data-stu-id="203ee-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="203ee-159">Odzyskiwanie danych toohello tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="203ee-159">Recover data toohello same machine</span></span>
<span data-ttu-id="203ee-160">Jeśli przypadkowo usunięto toorestore plików i chcą go toohello kroki tej samej maszyny (z którego hello tworzenia kopii zapasowej), po hello pomoże Ci odzyskać dane hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="203ee-161">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w.</span><span class="sxs-lookup"><span data-stu-id="203ee-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="203ee-162">Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="203ee-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="203ee-164">Wybierz hello  **tego serwera (*yourmachinename*) ** hello toorestore opcji kopii zapasowej pliku na powitania sam maszyny.</span><span class="sxs-lookup"><span data-stu-id="203ee-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Tym samym komputerze](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="203ee-166">Wybierz zbyt**Przeglądaj w poszukiwaniu plików** lub **wyszukiwania plików**.</span><span class="sxs-lookup"><span data-stu-id="203ee-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="203ee-167">Pozostaw opcję domyślną hello Jeśli planujesz toorestore jeden lub więcej plików, których ścieżką jest znany.</span><span class="sxs-lookup"><span data-stu-id="203ee-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="203ee-168">Jeśli nie pewności o hello struktury folderów, ale chcesz toosearch dla pliku, wybierz hello **wyszukiwania plików** opcji.</span><span class="sxs-lookup"><span data-stu-id="203ee-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="203ee-169">W tej sekcji w celu hello firma Microsoft będzie kontynuować hello opcji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="203ee-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="203ee-171">Wybierz wolumin hello, z którego chcesz toorestore hello pliku.</span><span class="sxs-lookup"><span data-stu-id="203ee-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="203ee-172">Można przywrócić z dowolnego punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="203ee-172">You can restore from any point in time.</span></span> <span data-ttu-id="203ee-173">Daty, które są wyświetlane w **bold** w formancie kalendarza hello wskazać hello dostępność punktu przywracania.</span><span class="sxs-lookup"><span data-stu-id="203ee-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="203ee-174">Po wybraniu daty są oparte na harmonogram tworzenia kopii zapasowych (i hello powodzenie operacji tworzenia kopii zapasowej), można wybrać punkt w czasie z hello **czasu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="203ee-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Data i woluminu](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="203ee-176">Wybierz hello toorecover elementów.</span><span class="sxs-lookup"><span data-stu-id="203ee-176">Select hello items toorecover.</span></span> <span data-ttu-id="203ee-177">Możesz wybrać wiele folderów/plików mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="203ee-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Wybieranie pozycji Pliki](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="203ee-179">Określ parametry odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-179">Specify hello recovery parameters.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="203ee-181">Istnieje możliwość przywrócenia oryginalnej lokalizacji toohello (w którym hello plik lub folder, zostaną zastąpione) lub lokalizacji tooanother w hello tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="203ee-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="203ee-182">Jeśli hello plik lub folder ma toorestore istnieje w miejscu docelowym hello, można tworzyć kopie (Witaj dwie wersje tego samego pliku), Zastąp hello pliki w miejscu docelowym hello lub pominąć odzyskiwanie hello hello plików, które istnieją w celu hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="203ee-183">Zdecydowanie zaleca się pozostawienie hello domyślną opcją Przywracanie listy ACL hello na powitania pliki, które są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="203ee-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="203ee-184">Gdy te dane wejściowe są dostarczane, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="203ee-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="203ee-185">przepływu pracy odzyskiwania Hello, które przywraca hello pliki toothis maszyny, zostanie rozpoczęta.</span><span class="sxs-lookup"><span data-stu-id="203ee-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="203ee-186">Odzyskiwanie maszyny alternatywny tooan</span><span class="sxs-lookup"><span data-stu-id="203ee-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="203ee-187">W przypadku utraty cały serwer, można jednak odzyskać dane z innego komputera tooa kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="203ee-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="203ee-188">następujące kroki Hello ilustrują hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="203ee-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="203ee-189">obejmuje Hello terminologią używaną w następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="203ee-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="203ee-190">*Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.</span><span class="sxs-lookup"><span data-stu-id="203ee-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="203ee-191">*Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="203ee-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="203ee-192">*Przykładowe magazynu* — hello toowhich magazynu kopii zapasowej hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="203ee-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="203ee-193">Nie można przywrócić kopii zapasowych wykonanych na komputerze, na komputerze, na którym jest uruchomiony program wcześniejszej wersji systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="203ee-194">Na przykład jeśli kopie zapasowe są wykonywane z komputera z systemem Windows 7, jego można przywracać w systemie Windows 8 lub nowszym maszyny.</span><span class="sxs-lookup"><span data-stu-id="203ee-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="203ee-195">Jednak hello odwrotnie nie posiada wartość true.</span><span class="sxs-lookup"><span data-stu-id="203ee-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="203ee-196">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w na powitania *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="203ee-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="203ee-197">Upewnij się, że hello *maszyny docelowej* i hello *maszyny źródłowej* zarejestrowanych toohello są tego samego magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="203ee-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="203ee-198">Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="203ee-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="203ee-200">Wybierz **innego serwera**</span><span class="sxs-lookup"><span data-stu-id="203ee-200">Select **Another server**</span></span>

    ![Inny serwer](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="203ee-202">Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*.</span><span class="sxs-lookup"><span data-stu-id="203ee-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="203ee-203">Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła) Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="203ee-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="203ee-204">Gdy podany plik poświadczeń magazynu hello hello magazynu kopii zapasowych przed plik poświadczeń magazynu hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="203ee-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="203ee-205">Wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn.</span><span class="sxs-lookup"><span data-stu-id="203ee-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista komputerów](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="203ee-207">Wybierz albo hello **wyszukiwania plików** lub **Przeglądaj w poszukiwaniu plików** opcji.</span><span class="sxs-lookup"><span data-stu-id="203ee-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="203ee-208">W celu hello przedstawione w tej sekcji użyjemy hello **wyszukiwania plików** opcji.</span><span class="sxs-lookup"><span data-stu-id="203ee-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="203ee-210">W następnym ekranie powitania, wybierz wolumin hello i daty.</span><span class="sxs-lookup"><span data-stu-id="203ee-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="203ee-211">Wyszukiwania dla nazwy pliku/folderu hello ma toorestore.</span><span class="sxs-lookup"><span data-stu-id="203ee-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="203ee-213">Wybierz lokalizację hello gdzie hello pliki muszą toobe przywrócona.</span><span class="sxs-lookup"><span data-stu-id="203ee-213">Select hello location where hello files need toobe restored.</span></span>

    ![Przywracanie w lokalizacji](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="203ee-215">Podaj hasło szyfrowania hello, które zostało podane podczas *maszyny źródłowej* rejestracji zbyt*magazynu próbki*.</span><span class="sxs-lookup"><span data-stu-id="203ee-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="203ee-217">Po wprowadzono powitania kliknij **odzyskać**, która przywracania kopii zapasowej plików toohello miejsca docelowego określonego hello hello wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="203ee-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="203ee-218">Użyj błyskawicznych przywrócić toorestore danych tooan alternatywny maszyny</span><span class="sxs-lookup"><span data-stu-id="203ee-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="203ee-219">W przypadku utraty cały serwer, można jednak odzyskać dane z innego komputera tooa kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="203ee-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="203ee-220">następujące kroki Hello ilustrują hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="203ee-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="203ee-221">obejmuje Hello terminologią używaną w następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="203ee-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="203ee-222">*Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.</span><span class="sxs-lookup"><span data-stu-id="203ee-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="203ee-223">*Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="203ee-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="203ee-224">*Przykładowe magazynu* — hello toowhich magazyn usług odzyskiwania hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="203ee-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="203ee-225">Tworzenie kopii zapasowych nie może być przywrócona tooa komputera docelowego ze starszą wersją systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="203ee-226">Na przykład kopii zapasowej z systemu Windows 7, komputer może być przywrócona w systemie Windows 8 lub nowszym, komputer.</span><span class="sxs-lookup"><span data-stu-id="203ee-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="203ee-227">Kopii zapasowej z komputera z systemem Windows 8 nie może być komputer przywróconej tooa systemu Windows 7.</span><span class="sxs-lookup"><span data-stu-id="203ee-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="203ee-228">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w na powitania *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="203ee-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="203ee-229">Upewnij się, hello *maszyny docelowej* i hello *maszyny źródłowej* są zarejestrowane toohello magazyn usług odzyskiwania tego samego.</span><span class="sxs-lookup"><span data-stu-id="203ee-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="203ee-230">Kliknij przycisk **odzyskać dane** tooopen hello **Kreatora odzyskiwania danych**.</span><span class="sxs-lookup"><span data-stu-id="203ee-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="203ee-232">Na powitania **wprowadzenie** okienku wybierz **innego serwera**</span><span class="sxs-lookup"><span data-stu-id="203ee-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Inny serwer](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="203ee-234">Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="203ee-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="203ee-235">Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła), Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="203ee-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="203ee-236">Po podaniu poświadczeń ważny magazyn, pojawi się nazwa hello hello odpowiadającego magazyn kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="203ee-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="203ee-237">Na powitania **wybierz serwer zapasowy** okienku, wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn i podaj hasło hello.</span><span class="sxs-lookup"><span data-stu-id="203ee-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="203ee-238">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="203ee-238">Then click **Next**.</span></span>

    ![Lista komputerów](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="203ee-240">Na powitania **wybierz tryb odzyskiwania** okienku, wybierz **poszczególnych plików i folderów** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="203ee-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="203ee-242">Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="203ee-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="203ee-243">Witaj kalendarza wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="203ee-244">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="203ee-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="203ee-245">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="203ee-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="203ee-246">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="203ee-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="203ee-248">Kliknij przycisk **instalacji** punkt odzyskiwania hello instalacji toolocally jako wolumin odzyskiwania na Twojej *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="203ee-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="203ee-249">Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.</span><span class="sxs-lookup"><span data-stu-id="203ee-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="203ee-251">W Eksploratorze Windows, skopiuj hello pliki lub foldery z hello odzyskiwania woluminu i wklej je tooyour *maszyny docelowej* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="203ee-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="203ee-252">Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="203ee-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="203ee-254">Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="203ee-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="203ee-255">Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="203ee-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="203ee-257">Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanego przez 6 godzin od czasu hello, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="203ee-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="203ee-258">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="203ee-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="203ee-259">Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.</span><span class="sxs-lookup"><span data-stu-id="203ee-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="203ee-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="203ee-260">Next steps</span></span>
* [<span data-ttu-id="203ee-261">Azure — często zadawane pytania kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="203ee-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="203ee-262">Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="203ee-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="203ee-263">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="203ee-263">Learn more</span></span>
* [<span data-ttu-id="203ee-264">Omówienie kopii zapasowych Azure</span><span class="sxs-lookup"><span data-stu-id="203ee-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="203ee-265">Kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="203ee-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="203ee-266">Wykonywanie kopii zapasowej obciążeń firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="203ee-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
