---
title: dane aaaRestore Azure tooa systemu Windows Server lub komputer z systemem Windows | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorestore dane przechowywane w Azure tooa systemu Windows Server lub komputer z systemem Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="c20e0-103">Przywróć pliki tooa systemu Windows server lub komputer kliencki z systemem Windows przy użyciu modelu wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c20e0-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c20e0-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c20e0-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="c20e0-105">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="c20e0-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="c20e0-106">W tym artykule opisano sposób toorestore danych z magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="c20e0-107">toorestore danych, należy użyć Kreatora odzyskiwania danych hello hello agenta usług odzyskiwania Azure firmy Microsoft (MARS).</span><span class="sxs-lookup"><span data-stu-id="c20e0-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="c20e0-108">Po przywróceniu danych, istnieje możliwość:</span><span class="sxs-lookup"><span data-stu-id="c20e0-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="c20e0-109">Wykonano przywrócenie danych toohello sam komputera, z których hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="c20e0-110">Przywracanie danych tooan alternatywny maszyny.</span><span class="sxs-lookup"><span data-stu-id="c20e0-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="c20e0-111">W stycznia 2017 r firma Microsoft opublikowała agenta MARS toohello aktualizacji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="c20e0-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="c20e0-112">Wraz z poprawki, ta aktualizacja umożliwia błyskawiczne przywrócić, dzięki czemu można toomount migawki punktu odzyskiwania zapisywalny jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="c20e0-113">Następnie można eksplorować hello odzyskiwania woluminu i skopiuj pliki tooa komputera lokalnego co selektywne Przywracanie plików.</span><span class="sxs-lookup"><span data-stu-id="c20e0-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="c20e0-114">Witaj [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) jest wymagany, jeśli chcesz, aby toouse błyskawicznych przywracania toorestore danych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="c20e0-115">Również dane kopii zapasowej hello muszą być chronione w magazynach wymienione w artykule pomocy technicznej hello ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="c20e0-116">Zapoznaj się hello [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) hello aktualną listę ustawień regionalnych, obsługujących błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="c20e0-117">Przywracanie błyskawicznych jest **nie** dostępne dla wszystkich ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="c20e0-118">Błyskawicznych Przywracanie jest dostępne do użycia w Magazyny usług odzyskiwania w hello portalu Azure i magazyny kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="c20e0-119">Jeśli chcesz przywrócić błyskawicznych toouse, Pobierz aktualizację MARS hello i postępuj zgodnie z procedurami hello, w których występuje błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="c20e0-120">Użyj błyskawicznych przywrócić toohello danych toorecover tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="c20e0-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="c20e0-121">Jeśli przypadkowo usunięto toorestore plików i chcą go toohello kroki tej samej maszyny (z którego hello tworzenia kopii zapasowej), po hello pomoże Ci odzyskać dane hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="c20e0-122">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w.</span><span class="sxs-lookup"><span data-stu-id="c20e0-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="c20e0-123">Jeśli nie znasz, którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="c20e0-124">Aplikacja klasyczna Hello powinny być wyświetlane w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="c20e0-125">Kliknij przycisk **odzyskać dane** toostart hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="c20e0-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="c20e0-127">Na powitania **wprowadzenie** okienka, toorestore hello danych toohello tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Wybierz ten serwer opcja toorestore hello danych toohello tym samym komputerze](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="c20e0-129">Na powitania **wybierz tryb odzyskiwania** okienku wybierz **poszczególnych plików i folderów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="c20e0-131">Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="c20e0-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="c20e0-132">Witaj kalendarza wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="c20e0-133">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="c20e0-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="c20e0-134">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="c20e0-135">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="c20e0-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Data i woluminu](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="c20e0-137">Po wybraniu toorestore punktu odzyskiwania powitania kliknij **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="c20e0-138">Kopia zapasowa Azure instaluje punkt odzyskiwania lokalne powitania i używa go jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="c20e0-139">Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.</span><span class="sxs-lookup"><span data-stu-id="c20e0-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="c20e0-141">W Eksploratorze Windows, skopiować pliki hello i/lub folderów toorestore a następnie wkleić je tooany lokalizacji toohello lokalnego serwera lub komputera.</span><span class="sxs-lookup"><span data-stu-id="c20e0-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="c20e0-142">Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Skopiuj i Wklej pliki i foldery z lokalizacji toolocal zainstalowanego woluminu](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="c20e0-144">Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="c20e0-145">Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="c20e0-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Odinstaluj hello woluminu i Potwierdź](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="c20e0-147">Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanych przez 6 godzin od czasu hello, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c20e0-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="c20e0-148">Jednak hello czas instalacji jest maksymalnie rozszerzonej maksymalnie 24 godziny, w przypadku bieżących kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="c20e0-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="c20e0-149">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c20e0-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="c20e0-150">Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="c20e0-151">Użyj błyskawicznych przywrócić toorestore danych tooan alternatywny maszyny</span><span class="sxs-lookup"><span data-stu-id="c20e0-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="c20e0-152">W przypadku utraty cały serwer, można jednak odzyskać dane z innego komputera tooa kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="c20e0-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="c20e0-153">następujące kroki Hello ilustrują hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c20e0-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="c20e0-154">obejmuje Hello terminologią używaną w następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c20e0-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="c20e0-155">*Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.</span><span class="sxs-lookup"><span data-stu-id="c20e0-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="c20e0-156">*Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="c20e0-157">*Przykładowe magazynu* — hello toowhich magazyn usług odzyskiwania hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="c20e0-158">Tworzenie kopii zapasowych nie może być przywrócona tooa komputera docelowego ze starszą wersją systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="c20e0-159">Na przykład kopii zapasowej z systemu Windows 7, komputer może być przywrócona w systemie Windows 8 lub nowszym, komputer.</span><span class="sxs-lookup"><span data-stu-id="c20e0-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="c20e0-160">Kopii zapasowej z komputera z systemem Windows 8 nie może być komputer przywróconej tooa systemu Windows 7.</span><span class="sxs-lookup"><span data-stu-id="c20e0-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="c20e0-161">Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w na powitania *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="c20e0-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="c20e0-162">Upewnij się, hello *maszyny docelowej* i hello *maszyny źródłowej* są zarejestrowane toohello magazyn usług odzyskiwania tego samego.</span><span class="sxs-lookup"><span data-stu-id="c20e0-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="c20e0-163">Kliknij przycisk **odzyskać dane** tooopen hello **Kreatora odzyskiwania danych**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="c20e0-165">Na powitania **wprowadzenie** okienku wybierz **innego serwera**</span><span class="sxs-lookup"><span data-stu-id="c20e0-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Inny serwer](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="c20e0-167">Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="c20e0-168">Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła), Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c20e0-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="c20e0-169">Po podaniu poświadczeń ważny magazyn, pojawi się nazwa hello hello odpowiadającego magazyn kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c20e0-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="c20e0-170">Na powitania **wybierz serwer zapasowy** okienku, wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn i podaj hasło hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="c20e0-171">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="c20e0-171">Then click **Next**.</span></span>

    ![Lista komputerów](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="c20e0-173">Na powitania **wybierz tryb odzyskiwania** okienku, wybierz **poszczególnych plików i folderów** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="c20e0-175">Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.</span><span class="sxs-lookup"><span data-stu-id="c20e0-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="c20e0-176">Witaj kalendarza wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="c20e0-177">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="c20e0-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="c20e0-178">Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="c20e0-179">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="c20e0-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="c20e0-181">Kliknij przycisk **instalacji** punkt odzyskiwania hello instalacji toolocally jako wolumin odzyskiwania na Twojej *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="c20e0-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="c20e0-182">Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.</span><span class="sxs-lookup"><span data-stu-id="c20e0-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="c20e0-184">W Eksploratorze Windows, skopiuj hello pliki lub foldery z hello odzyskiwania woluminu i wklej je tooyour *maszyny docelowej* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c20e0-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="c20e0-185">Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="c20e0-187">Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="c20e0-188">Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="c20e0-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="c20e0-190">Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanych przez 6 godzin od czasu hello, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c20e0-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="c20e0-191">Jednak hello czas instalacji jest maksymalnie rozszerzonej maksymalnie 24 godziny, w przypadku bieżących kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="c20e0-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="c20e0-192">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c20e0-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="c20e0-193">Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.</span><span class="sxs-lookup"><span data-stu-id="c20e0-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="c20e0-194">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c20e0-194">Troubleshooting</span></span>
<span data-ttu-id="c20e0-195">Jeśli kopia zapasowa Azure nie jest pomyślnie instalowany hello odzyskiwania woluminu nawet po kilku minutach klikanie **instalacji** lub kończy się niepowodzeniem toomount hello odzyskiwania woluminu z co najmniej jeden błąd, wykonaj kroki hello poniżej toobegin odzyskiwanie normalnie.</span><span class="sxs-lookup"><span data-stu-id="c20e0-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="c20e0-196">Anuluj proces instalacji trwającą hello na wypadek, gdyby była uruchomiona na kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c20e0-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="c20e0-197">Upewnij się, że znajdują się na powitania najnowszą wersję agenta usługi Kopia zapasowa Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c20e0-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="c20e0-198">toofind limit hello informacje o wersji agenta usługi Kopia zapasowa Azure, wybierz polecenie **o Microsoft agenta usług odzyskiwania Azure** na powitania **akcje** okienko kopia zapasowa Microsoft Azure konsoli i upewnij się, że hello  **Wersja** liczba jest równa tooor wyższa niż wersja hello wymienionych w [w tym artykule](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="c20e0-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="c20e0-199">Możesz pobrać najnowszą wersję hello z [tutaj](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="c20e0-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="c20e0-200">Przejdź za**Menedżera urządzeń** -> **kontrolerów magazynu** i upewnij się, że można zlokalizować **inicjatora iSCSI firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="c20e0-201">Jeśli mogą ją odnaleźć, przejdź bezpośrednio toostep 7 poniżej.</span><span class="sxs-lookup"><span data-stu-id="c20e0-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="c20e0-202">Jeśli nie można zlokalizować Usługa inicjatora iSCSI firmy Microsoft, jak wspomniano w kroku 3, określ, czy toosee można odnaleźć wpisu w obszarze **Menedżera urządzeń** -> **kontrolerów magazynu** o nazwie  **Nieznane urządzenie** o identyfikatorze sprzętu **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="c20e0-203">Kliknij prawym przyciskiem myszy **nieznane urządzenie** i wybierz **aktualizacji sterowników**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="c20e0-204">Sterownik hello aktualizacji, wybierając opcję hello zbyt **Wyszukaj automatycznie zaktualizowane sterowniki**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="c20e0-205">Należy zmienić ukończenia aktualizacji hello **nieznane urządzenie** za**inicjatora iSCSI firmy Microsoft** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c20e0-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="c20e0-207">Przejdź za**Menedżera zadań** -> **usługi (lokalne)** -> **Usługa inicjatora iSCSI firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="c20e0-209">Uruchom ponownie usługę inicjatora iSCSI firmy Microsoft hello przez usługę hello, klikając prawym przyciskiem myszy **zatrzymać** i ponowne kliknięcie prawym przyciskiem myszy, a następnie klikając **Start**.</span><span class="sxs-lookup"><span data-stu-id="c20e0-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="c20e0-210">Ponów odzyskiwanie przy użyciu błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="c20e0-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="c20e0-211">Jeśli nadal nie hello odzyskiwania, ponowny rozruch serwera/klienta.</span><span class="sxs-lookup"><span data-stu-id="c20e0-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="c20e0-212">Jeśli ponowne uruchomienie komputera nie jest pożądane lub hello odzyskiwania nadal kończy się niepowodzeniem nawet po ponowny rozruch serwera hello, spróbuj przeprowadzić odzyskiwanie z alternatywnych maszyny i skontaktuj się z Azure obsługuje przechodząc zbyt[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i przesyłanie żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c20e0-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c20e0-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c20e0-213">Next steps</span></span>
* <span data-ttu-id="c20e0-214">Teraz, gdy zostały odzyskane pliki i foldery, możesz [Zarządzanie kopii zapasowych](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="c20e0-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
