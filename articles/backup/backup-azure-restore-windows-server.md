---
title: Odzyskiwanie danych na platformie Azure do systemu Windows Server lub komputer z systemem Windows | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak przywrócić dane przechowywane na platformie Azure do systemu Windows Server lub komputer z systemem Windows."
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
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="e25ad-103">Przywracanie plików do maszyny z systemem Windows Server lub Client przy użyciu modelu wdrażania używającego usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e25ad-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e25ad-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e25ad-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="e25ad-105">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="e25ad-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="e25ad-106">W tym artykule wyjaśniono, jak przywrócić dane z magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="e25ad-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="e25ad-107">Aby przywrócić dane, używasz Kreatora odzyskiwania danych w agencie usług odzyskiwania Azure firmy Microsoft (MARS).</span><span class="sxs-lookup"><span data-stu-id="e25ad-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="e25ad-108">Po przywróceniu danych, istnieje możliwość:</span><span class="sxs-lookup"><span data-stu-id="e25ad-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="e25ad-109">Przywróć dane do tego samego komputera, z którego wykonano kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="e25ad-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="e25ad-110">Przywracanie danych do alternatywnej maszyny.</span><span class="sxs-lookup"><span data-stu-id="e25ad-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="e25ad-111">W stycznia 2017 r firma Microsoft opublikowała Podgląd aktualizacji agenta MARS.</span><span class="sxs-lookup"><span data-stu-id="e25ad-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="e25ad-112">Wraz z poprawki ta aktualizacja umożliwia błyskawiczne przywrócić, dzięki czemu można zainstalować migawkę punktu odzyskiwania zapisywalny, jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="e25ad-113">Następnie można eksplorować odzyskiwania woluminu i kopiować pliki na komputerze lokalnym, a tym samym selektywne Przywracanie plików.</span><span class="sxs-lookup"><span data-stu-id="e25ad-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="e25ad-114">[Stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) jest wymagany, jeśli chcesz użyć błyskawicznych przywracania, aby przywrócić dane.</span><span class="sxs-lookup"><span data-stu-id="e25ad-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="e25ad-115">Również dane kopii zapasowej muszą być chronione w magazynach przy ustawieniach regionalnych wymienione w artykule pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="e25ad-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="e25ad-116">Zapoznaj się [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) najbardziej aktualną listę ustawień regionalnych, obsługujących błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="e25ad-117">Przywracanie błyskawicznych jest **nie** dostępne dla wszystkich ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="e25ad-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="e25ad-118">Błyskawicznych Przywracanie jest dostępne do użycia w Magazyny usług odzyskiwania w portalu Azure i magazyny kopii zapasowych w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="e25ad-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="e25ad-119">Jeśli chcesz użyć błyskawicznych przywracania, Pobierz aktualizację MARS i postępuj zgodnie z procedurami, których występuje błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="e25ad-120">Użyj błyskawicznych przywracania, aby odzyskać dane do tej samej maszyny</span><span class="sxs-lookup"><span data-stu-id="e25ad-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="e25ad-121">Jeśli przypadkowo usunięto plik i chcesz przywrócić go do tego samego komputera (z którego jest pobierany kopii zapasowej), poniższe kroki pomoże Ci odzyskania danych.</span><span class="sxs-lookup"><span data-stu-id="e25ad-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="e25ad-122">Otwórz **kopia zapasowa Microsoft Azure** przyciągania w.</span><span class="sxs-lookup"><span data-stu-id="e25ad-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="e25ad-123">Jeśli nie znasz, którym zainstalowano przystawkę, wyszukiwanie w komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="e25ad-124">Aplikacja klasyczna powinny być wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="e25ad-125">Kliknij przycisk **odzyskać dane** Aby uruchomić kreatora.</span><span class="sxs-lookup"><span data-stu-id="e25ad-125">Click **Recover Data** to start the wizard.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="e25ad-127">Na **wprowadzenie** okienko, aby przywrócić dane do tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Wybierz tę opcję serwera, aby przywrócić dane do tej samej maszyny](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="e25ad-129">Na **wybierz tryb odzyskiwania** okienku wybierz **poszczególnych plików i folderów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="e25ad-131">Na **Wybierz wolumin i data** okienku, wybierz wolumin, który zawiera pliki lub foldery, które mają zostać przywrócone.</span><span class="sxs-lookup"><span data-stu-id="e25ad-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="e25ad-132">W kalendarzu wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="e25ad-133">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="e25ad-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e25ad-134">Daty w **bold** wskazuje dostępność co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="e25ad-135">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, należy wybrać określony punkt odzyskiwania z **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="e25ad-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Data i woluminu](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="e25ad-137">Kliknij wybrany punkt odzyskiwania, aby przywrócić **instalacji**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="e25ad-138">Kopia zapasowa Azure instaluje punkt odzyskiwania lokalnych i używa go jako wolumin odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="e25ad-139">Na **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** Otwórz Eksploratora Windows i wyszukiwanie plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="e25ad-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="e25ad-141">W Eksploratorze Windows skopiuj pliki lub foldery, które chcesz przywrócić i wklej je do dowolnej lokalizacji do serwera lub komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e25ad-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="e25ad-142">Można otworzyć lub strumienia pliki bezpośrednio z woluminu odzyskiwania i sprawdź, czy poprawne wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="e25ad-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Skopiuj i Wklej pliki i foldery z zainstalowanego woluminu do lokalizacji lokalnej](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="e25ad-144">Po zakończeniu przywracania plików i/lub folderów, na **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="e25ad-145">Następnie kliknij przycisk **tak** potwierdzenie dezinstalacji woluminu.</span><span class="sxs-lookup"><span data-stu-id="e25ad-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Dezinstalacji woluminu i Potwierdź](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="e25ad-147">Jeśli nie kliknij polecenie Odinstaluj, wolumin odzyskiwania pozostaną zainstalowane przez 6 godzin od momentu, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e25ad-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="e25ad-148">Czas instalacji jest jednak rozszerzonej maksymalnie maksymalnie 24 godziny, w przypadku bieżących kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="e25ad-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="e25ad-149">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e25ad-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="e25ad-150">Żadnej operacji tworzenia kopii zapasowej zaplanowane do uruchomienia w czasie, gdy wolumin jest zainstalowany, zostanie uruchomiony po odinstalowane woluminu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="e25ad-151">Umożliwia błyskawiczne przywrócić przywracania danych do alternatywnej maszyny</span><span class="sxs-lookup"><span data-stu-id="e25ad-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="e25ad-152">W przypadku utraty cały serwer można jednak odzyskać dane z kopii zapasowej Azure na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e25ad-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="e25ad-153">Poniższe kroki przedstawiają przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="e25ad-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="e25ad-154">Składa się z terminologią używaną w następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e25ad-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="e25ad-155">*Maszyna źródłowa* — oryginalnego komputera, z którego wykonano kopię zapasową i który jest obecnie niedostępny.</span><span class="sxs-lookup"><span data-stu-id="e25ad-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="e25ad-156">*Maszyna docelowa* — komputera, do którego dane są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="e25ad-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="e25ad-157">*Przykładowe magazynu* — magazyn usług odzyskiwania i do którego *maszyny źródłowej* i *maszyny docelowej* są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="e25ad-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="e25ad-158">Nie można przywrócić kopii zapasowych na komputerze docelowym, ze starszą wersją systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e25ad-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="e25ad-159">Na przykład kopii zapasowej z systemu Windows 7, komputer może być przywrócona w systemie Windows 8 lub nowszym, komputer.</span><span class="sxs-lookup"><span data-stu-id="e25ad-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="e25ad-160">Nie można przywrócić kopii zapasowej z komputera z systemem Windows 8 na komputerze z systemem Windows 7.</span><span class="sxs-lookup"><span data-stu-id="e25ad-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="e25ad-161">Otwórz **kopia zapasowa Microsoft Azure** przyciągania w na *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="e25ad-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="e25ad-162">Upewnij się, *maszyny docelowej* i *maszyny źródłowej* są rejestrowane w tym samym magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="e25ad-163">Kliknij przycisk **odzyskać dane** otworzyć **Kreatora odzyskiwania danych**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="e25ad-165">Na **wprowadzenie** okienku wybierz **innego serwera**</span><span class="sxs-lookup"><span data-stu-id="e25ad-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Inny serwer](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="e25ad-167">Podaj plik poświadczeń magazynu, który odpowiada *magazynu próbki*i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="e25ad-168">Jeśli plik poświadczeń magazynu jest nieprawidłowa (lub wygasła), Pobierz nowy plik poświadczeń magazynu z *magazynu próbki* w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e25ad-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="e25ad-169">Po podaniu poświadczeń ważny magazyn, zostanie wyświetlony nazwę odpowiedniego magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e25ad-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="e25ad-170">Na **wybierz serwer zapasowy** okienku, wybierz *maszyny źródłowej* z listy wyświetlanych maszyn i podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="e25ad-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="e25ad-171">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="e25ad-171">Then click **Next**.</span></span>

    ![Lista komputerów](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="e25ad-173">Na **wybierz tryb odzyskiwania** okienku, wybierz **poszczególnych plików i folderów** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="e25ad-175">Na **Wybierz wolumin i data** okienku, wybierz wolumin, który zawiera pliki lub foldery, które mają zostać przywrócone.</span><span class="sxs-lookup"><span data-stu-id="e25ad-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="e25ad-176">W kalendarzu wybierz punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="e25ad-177">Można przywrócić z dowolnego punktu odzyskiwania w czasie.</span><span class="sxs-lookup"><span data-stu-id="e25ad-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="e25ad-178">Daty w **bold** wskazuje dostępność co najmniej jeden punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="e25ad-179">Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, należy wybrać określony punkt odzyskiwania z **czasu** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="e25ad-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="e25ad-181">Kliknij przycisk **instalacji** można lokalnie zainstalować jako woluminu odzyskiwania punkt odzyskiwania na Twojej *maszyny docelowej*.</span><span class="sxs-lookup"><span data-stu-id="e25ad-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="e25ad-182">Na **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** Otwórz Eksploratora Windows i wyszukiwanie plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="e25ad-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="e25ad-184">W Eksploratorze Windows, skopiuj pliki lub foldery z tego woluminu, odzyskiwania i wklej je do Twojej *maszyny docelowej* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e25ad-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="e25ad-185">Można otworzyć lub strumienia pliki bezpośrednio z woluminu odzyskiwania i sprawdź, czy poprawne wersje są odzyskiwane.</span><span class="sxs-lookup"><span data-stu-id="e25ad-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="e25ad-187">Po zakończeniu przywracania plików i/lub folderów, na **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="e25ad-188">Następnie kliknij przycisk **tak** potwierdzenie dezinstalacji woluminu.</span><span class="sxs-lookup"><span data-stu-id="e25ad-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="e25ad-190">Jeśli nie kliknij polecenie Odinstaluj, wolumin odzyskiwania pozostaną zainstalowane przez 6 godzin od momentu, gdy został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e25ad-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="e25ad-191">Czas instalacji jest jednak rozszerzonej maksymalnie maksymalnie 24 godziny, w przypadku bieżących kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="e25ad-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="e25ad-192">Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e25ad-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="e25ad-193">Żadnej operacji tworzenia kopii zapasowej zaplanowane do uruchomienia w czasie, gdy wolumin jest zainstalowany, zostanie uruchomiony po odinstalowane woluminu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="e25ad-194">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e25ad-194">Troubleshooting</span></span>
<span data-ttu-id="e25ad-195">Jeśli kopia zapasowa Azure nie jest pomyślnie instalowany woluminu odzyskiwania nawet po kilku minutach klikanie **instalacji** lub kończy się niepowodzeniem, można zainstalować woluminu odzyskiwania z co najmniej jeden błąd, wykonaj poniższe kroki, aby rozpocząć odzyskiwanie normalnie.</span><span class="sxs-lookup"><span data-stu-id="e25ad-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="e25ad-196">Anuluj proces trwającej instalacji w przypadku uruchomienia na kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e25ad-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="e25ad-197">Upewnij się, że jesteś w najnowszej wersji agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="e25ad-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="e25ad-198">Aby uzyskać informacje o wersji agenta usługi Kopia zapasowa Azure, kliknij **o Microsoft agenta usług odzyskiwania Azure** na **akcje** kopia zapasowa Microsoft Azure w okienku konsoli i upewnij się, że **Wersji** liczba jest równa lub wyższa niż wersja wspomnianego [w tym artykule](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="e25ad-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="e25ad-199">Możesz pobrać najnowszą wersję ze [tutaj](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="e25ad-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="e25ad-200">Przejdź do **Menedżera urządzeń** -> **kontrolerów magazynu** i upewnij się, że można zlokalizować **inicjatora iSCSI firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="e25ad-201">Jeśli mogą ją odnaleźć, bezpośrednio przejść do kroku 7 poniżej.</span><span class="sxs-lookup"><span data-stu-id="e25ad-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="e25ad-202">Jeśli nie można zlokalizować Usługa inicjatora iSCSI firmy Microsoft, jak wspomniano w kroku 3, sprawdź, jeśli można odnaleźć wpisu w obszarze **Menedżera urządzeń** -> **kontrolerów magazynu** o nazwie  **Nieznane urządzenie** o identyfikatorze sprzętu **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="e25ad-203">Kliknij prawym przyciskiem myszy **nieznane urządzenie** i wybierz **aktualizacji sterowników**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="e25ad-204">Aktualizacja sterownika, wybierając opcję **Wyszukaj automatycznie zaktualizowane sterowniki**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="e25ad-205">Zakończenie aktualizacji należy zmienić **nieznane urządzenie** do **inicjatora iSCSI firmy Microsoft** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e25ad-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="e25ad-207">Przejdź do **Menedżera zadań** -> **usługi (lokalne)** -> **Usługa inicjatora iSCSI firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="e25ad-209">Ponownie uruchom usługę inicjatora iSCSI firmy Microsoft przez usługę, klikając prawym przyciskiem myszy **zatrzymać** i ponowne kliknięcie prawym przyciskiem myszy, a następnie klikając **Start**.</span><span class="sxs-lookup"><span data-stu-id="e25ad-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="e25ad-210">Ponów odzyskiwanie przy użyciu błyskawicznych przywracania.</span><span class="sxs-lookup"><span data-stu-id="e25ad-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="e25ad-211">W przypadku odzyskiwania nadal niepowodzenia ponownego uruchomienia serwera/klienta.</span><span class="sxs-lookup"><span data-stu-id="e25ad-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="e25ad-212">Jeśli ponowne uruchomienie komputera nie jest pożądane lub odzyskiwania nadal kończy się niepowodzeniem nawet po ponownego uruchomienia serwera, spróbuj przeprowadzić odzyskiwanie z alternatywnych maszyny i skontaktuj się z Azure obsługuje, przechodząc do [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i przesyłanie żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="e25ad-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e25ad-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e25ad-213">Next steps</span></span>
* <span data-ttu-id="e25ad-214">Teraz, gdy zostały odzyskane pliki i foldery, możesz [Zarządzanie kopii zapasowych](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e25ad-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
