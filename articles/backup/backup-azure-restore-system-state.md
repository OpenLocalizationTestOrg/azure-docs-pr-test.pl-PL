---
title: 'Kopia zapasowa Azure: Tooa Przywracanie stanu systemu Windows Server | Dokumentacja firmy Microsoft'
description: "Krok wyjaśnienie krok przywracania stanu systemu Windows Server z kopii zapasowej na platformie Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="7ab8a-103">Przywracanie stanu systemu tooWindows serwera</span><span class="sxs-lookup"><span data-stu-id="7ab8a-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="7ab8a-104">W tym artykule opisano, jak magazyn kopii zapasowych stanu systemu Windows Server toorestore z usług odzyskiwania Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="7ab8a-105">toorestore stanu systemu, musi mieć kopię zapasową stanu systemu (utworzone za pomocą instrukcji hello w [Utwórz kopię zapasową stanu systemu](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) i upewnij się, że zainstalowano hello [najnowszą wersję programu Microsoft Azure Recovery hello Agent usług (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="7ab8a-106">Odzyskiwanie stanu systemu Windows Server danych z magazynu usług odzyskiwania Azure jest procesem dwuetapowym:</span><span class="sxs-lookup"><span data-stu-id="7ab8a-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="7ab8a-107">Przywróć stan systemu jako pliki kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="7ab8a-108">Podczas przywracania stanu systemu plików z kopii zapasowej Azure, można wykonać jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="7ab8a-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="7ab8a-109">Przywracanie stanu systemu toohello tym samym serwerze, na których wykonano kopie zapasowe hello, lub</span><span class="sxs-lookup"><span data-stu-id="7ab8a-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="7ab8a-110">Przywracanie stanu systemu tooan alternatywny serwer plików.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="7ab8a-111">Zastosuj hello przywrócić stan systemu plików tooa systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="7ab8a-112">Odzyskać stan systemu plików toohello tym samym serwerze</span><span class="sxs-lookup"><span data-stu-id="7ab8a-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="7ab8a-113">Witaj, wykonaj czynności wyjaśniają, jak tooroll kopii programu Windows Server konfiguracji tooa poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="7ab8a-114">Wycofanie serwera konfiguracji tooa wstecz znane stabilności, może być bardzo istotne.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="7ab8a-115">Witaj poniższych stan systemu serwera kroków przywracania hello z magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="7ab8a-116">Otwórz hello **kopia zapasowa Microsoft Azure** przystawki.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="7ab8a-117">Jeśli nie wiadomo, w którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="7ab8a-118">Aplikacja klasyczna Hello powinny być wyświetlane w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="7ab8a-119">Kliknij przycisk **odzyskać dane** toostart hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="7ab8a-121">Na powitania **wprowadzenie** okienka, toorestore hello danych toohello tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Wybierz ten serwer opcja toorestore hello danych toohello tym samym komputerze](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="7ab8a-123">Na powitania **wybierz tryb odzyskiwania** okienku wybierz **stanu systemu** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Przeglądanie plików](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="7ab8a-125">W kalendarzu hello w **Wybierz wolumin i data** punktu okienku, wybierz odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="7ab8a-126">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="7ab8a-127">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="7ab8a-128">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Data i woluminu](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="7ab8a-130">Po wybraniu toorestore punktu odzyskiwania powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="7ab8a-131">Kopia zapasowa Azure instaluje punkt odzyskiwania lokalne powitania i używa go jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="7ab8a-132">W okienku dalej hello, określ lokalizację docelową hello hello odzyskać stan systemu plików, a następnie kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery mają.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="7ab8a-133">Witaj opcji **kopie tak, aby obie wersje**, tworzy kopie poszczególnych plików w istniejącego archiwum pliku stanu systemu zamiast tworzenia kopii hello hello całe archiwum stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="7ab8a-135">Sprawdź szczegóły hello odzyskiwania na powitania **potwierdzenie** okienko i kliknij przycisk **odzyskać**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Kliknij przycisk Odzyskaj tooacknowledge hello Odzyskaj akcji](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="7ab8a-137">Kopiuj hello *WindowsImageBackup* katalogu w hello niekrytyczne woluminu tooa miejsce docelowe odzyskiwania powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="7ab8a-138">Zwykle woluminu systemu operacyjnego Windows hello jest hello wolumin krytyczny.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="7ab8a-139">Po hello odzyskiwania zakończy się pomyślnie, wykonaj kroki hello w sekcji hello [Zastosuj przywrócić stan systemu plików toohello systemu Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete proces odzyskiwania stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="7ab8a-140">Alternatywny serwer tooan pliki odzyskać stan systemu</span><span class="sxs-lookup"><span data-stu-id="7ab8a-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="7ab8a-141">Jeśli serwera z systemem Windows jest uszkodzony lub jest niedostępny, i chcesz toorestore on tooa stabilności przez odzyskiwanie hello stanu systemu Windows Server, można przywrócić stan systemu serwera uszkodzony hello z innego serwera.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="7ab8a-142">Użyj hello następujące kroki toohello Przywracanie stanu systemu na osobnym serwerze.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="7ab8a-143">obejmuje Hello terminologią używaną w następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7ab8a-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="7ab8a-144">*Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="7ab8a-145">*Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="7ab8a-146">*Przykładowe magazynu* — hello toowhich magazyn usług odzyskiwania hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="7ab8a-147">Kopie zapasowe wykonane z jednego komputera nie może być tooa przywróconej maszyny ze starszą wersją systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="7ab8a-148">Na przykład kopii zapasowych wykonanych z systemem Windows Server 2016 maszyny nie może być przywrócona tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="7ab8a-149">Jednak odwrotność hello jest możliwe.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-149">However, hello inverse is possible.</span></span> <span data-ttu-id="7ab8a-150">Możesz użyć kopii zapasowych z toorestore systemu Windows Server 2012 R2, Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="7ab8a-151">Otwórz hello **kopia zapasowa Microsoft Azure** przystawki na powitania *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="7ab8a-152">Upewnij się, że hello *maszyny docelowej* i hello *maszyny źródłowej* są zarejestrowane toohello magazyn usług odzyskiwania tego samego.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="7ab8a-153">Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="7ab8a-155">Wybierz **innego serwera**</span><span class="sxs-lookup"><span data-stu-id="7ab8a-155">Select **Another server**</span></span>

    ![Inny serwer](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="7ab8a-157">Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="7ab8a-158">Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła), Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="7ab8a-159">Po podany plik poświadczeń magazynu hello hello magazyn usług odzyskiwania skojarzonych z plik poświadczeń magazynu hello zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="7ab8a-160">W okienku wybierz pozycję Utwórz kopię zapasową serwera hello wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista komputerów](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="7ab8a-162">W okienku wybierz tryb odzyskiwania hello, wybierz **stanu systemu** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Wyszukiwanie](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="7ab8a-164">Na powitania kalendarza w hello **Wybierz wolumin i data** punktu okienku, wybierz odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="7ab8a-165">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="7ab8a-166">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="7ab8a-167">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Wyszukiwanie elementów](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="7ab8a-169">Po wybraniu toorestore punktu odzyskiwania powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="7ab8a-170">Na powitania **wybierz tryb odzyskiwania stanu systemu** okienka, określ docelowy hello miejscu toobe odzyskane pliki stanu systemu, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="7ab8a-172">Witaj opcji **kopie tak, aby obie wersje**, tworzy kopie poszczególnych plików w istniejącego archiwum pliku stanu systemu zamiast tworzenia kopii hello hello całe archiwum stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="7ab8a-173">Sprawdź szczegóły hello odzyskiwania w okienku potwierdzenie hello, a następnie kliknij przycisk **odzyskać**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![proces odzyskiwania hello tooconfirm przycisk Odzyskaj powitania kliknij](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="7ab8a-175">Kopiuj hello *WindowsImageBackup* katalogu tooa niekrytyczne woluminu powitania serwera (na przykład D:\).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="7ab8a-176">Wolumin systemu operacyjnego Windows hello jest zazwyczaj hello wolumin krytyczny.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="7ab8a-177">proces odzyskiwania hello toocomplete, użyj następujących hello sekcji zbyt[zastosować hello przywrócić stan systemu plików w systemie Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="7ab8a-178">Zastosuj przywróconego stanu systemu w systemie Windows Server</span><span class="sxs-lookup"><span data-stu-id="7ab8a-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="7ab8a-179">Po odzyskały stan systemu jako plików za pomocą agenta usług odzyskiwania Azure, użyj hello kopia zapasowa systemu Windows Server narzędzie tooapply hello odzyskać tooWindows stanu systemu serwera.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="7ab8a-180">Witaj narzędzie Kopia zapasowa systemu Windows Server jest już dostępny na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="7ab8a-181">Hello następujące kroki opisano, jak tooapply hello odzyskać stan systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="7ab8a-182">Użyj następujących hello polecenia tooreboot serwera w *trybie naprawy usług katalogowych*.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="7ab8a-183">W wierszu polecenia z podwyższonym poziomem uprawnień:</span><span class="sxs-lookup"><span data-stu-id="7ab8a-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="7ab8a-184">Po ponownym uruchomieniu hello Otwórz przystawkę narzędzia Kopia zapasowa systemu Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="7ab8a-185">Jeśli nie wiadomo, w którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa systemu Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="7ab8a-186">Aplikacja klasyczna Hello pojawia się w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="7ab8a-187">W przystawce hello, wybierz **lokalna kopia zapasowa**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Wybierz z tego miejsca toorestore lokalna kopia zapasowa](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="7ab8a-189">Na powitania lokalna kopia zapasowa w konsoli hello **okienka Akcje**, kliknij przycisk **odzyskać** hello tooopen Kreatora odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="7ab8a-190">Wybierz opcję hello **kopia zapasowa jest przechowywana w innej lokalizacji**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Wybierz inny serwer tooa toorecover](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="7ab8a-192">Podczas określania typu lokalizacji hello, wybierz **zdalnego folderu udostępnionego** Jeśli kopia zapasowa stanu systemu serwera tooanother odzyskane.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="7ab8a-193">Jeśli stan systemu został odzyskany lokalnie, następnie wybierz **dyski lokalne**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Wybierz czy toorecovery z serwera lokalnego lub innego](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="7ab8a-195">Wprowadź hello ścieżki toohello *WindowsImageBackup* katalogu, lub wybrać dysk lokalne powitania zawierający ten katalog (na przykład D:\WindowsImageBackup) odzyskiwane podczas odzyskiwania pliki stanu systemu hello za pomocą odzyskiwania Azure Usługi agenta i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![Ścieżka toohello udostępnionych plików](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="7ab8a-197">Wybierz hello stanu systemu wersji mają toorestore i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="7ab8a-198">Wybierz w okienku Wybieranie typu odzyskiwania hello **stanu systemu** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="7ab8a-199">Dla lokalizacji hello hello odzyskiwania stanu systemu, wybierz **oryginalnej lokalizacji**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="7ab8a-200">Przejrzyj szczegóły potwierdzenie hello, sprawdź ustawienia ponowny rozruch hello, a następnie kliknij przycisk **odzyskać** tooapplly hello przywrócić stan systemu plików.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![hello uruchamiania Przywracanie stanu systemu plików](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="7ab8a-202">Uwagi dotyczące odzyskiwania stanu systemu na serwerze usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ab8a-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="7ab8a-203">Kopia zapasowa stanu systemu zawiera danych usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="7ab8a-204">Użyj hello poniższych kroków toorestore usług domenowych w usłudze Active Directory (AD DS) z jego bieżącym stanie tooa poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="7ab8a-205">Uruchom ponownie kontroler domeny hello w trybie przywracania usług katalogowych (DSRM).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="7ab8a-206">Wykonaj kroki hello [tutaj](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover poleceń cmdlet narzędzia Kopia zapasowa systemu Windows Server toouse usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="7ab8a-207">Rozwiązywanie problemów z niepowodzeniem Przywracanie stanu systemu</span><span class="sxs-lookup"><span data-stu-id="7ab8a-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="7ab8a-208">Jeśli hello poprzedniego procesu stosowania stan systemu nie zakończy się pomyślnie, należy użyć toorecover środowisko odzyskiwania systemu Windows (Windows RE) powitania serwera z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="7ab8a-209">Witaj poniższych krokach opisano sposób toorecover przy użyciu środowiska Windows RE.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="7ab8a-210">Użyj tej opcji tylko wtedy, gdy system Windows Server nie normalny rozruch po przywróceniu stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="7ab8a-211">powitania po procesie powoduje usunięcie danych z systemem innym niż system, ostrożność.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="7ab8a-212">Przeprowadź rozruch serwera z systemem Windows w hello środowisko odzyskiwania systemu Windows (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="7ab8a-213">Wybierz Rozwiązywanie problemów z trzech dostępnych opcji hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-213">Select Troubleshoot from hello three available options.</span></span>

    ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="7ab8a-215">Z hello **zaawansowane opcje** ekranu wybierz **wiersza polecenia** i podaj nazwę użytkownika administratora serwera hello i hasło.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="7ab8a-217">Podaj nazwę użytkownika administratora serwera hello i hasło.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-217">Provide hello server administrator username and password.</span></span>

    ![Otwieranie menu](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="7ab8a-219">Po otwarciu hello wiersza polecenia w trybie administratora, uruchom następujące polecenie tooget hello stanu systemu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="7ab8a-221">Uruchom następujące polecenie tooget hello wszystkich woluminów dostępnych w programie Kopia zapasowa hello.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="7ab8a-223">Witaj następujące polecenie przywraca wszystkie woluminy, które są częścią hello kopii zapasowej stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="7ab8a-224">Należy pamiętać, że ten krok umożliwia odzyskiwanie tylko hello woluminów krytycznych, które są częścią hello stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="7ab8a-225">Wszystkie dane z systemem innym niż System jest usunięte.</span><span class="sxs-lookup"><span data-stu-id="7ab8a-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Pobieranie wersji kopii zapasowej stanu systemu](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="7ab8a-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ab8a-227">Next steps</span></span>
* <span data-ttu-id="7ab8a-228">Teraz, gdy zostały odzyskane pliki i foldery, możesz [Zarządzanie kopii zapasowych](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7ab8a-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
