---
title: "Zarządzanie Magazyny usług odzyskiwania Azure i serwery | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka, aby dowiedzieć się, jak zarządzać Magazyny usług odzyskiwania Azure i serwerów."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="662a8-103">Monitorowanie magazynów i serwerów usługi Azure Recovery Services i zarządzanie nimi dla maszyn z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="662a8-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="662a8-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="662a8-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="662a8-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="662a8-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="662a8-106">W tym artykule znajdziesz Omówienie kopii zapasowej zadania zarządzania i monitorowania, które są dostępne za pośrednictwem portalu Azure i agenta kopii zapasowej Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="662a8-107">W tym artykule przyjęto założenie, już mieć subskrypcję platformy Azure i został utworzony co najmniej jeden magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="662a8-108">Otwórz magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="662a8-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="662a8-109">Na pulpicie nawigacyjnym magazynu usług odzyskiwania przedstawia szczegóły lub atrybuty z magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="662a8-110">Zaloguj się do [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="662a8-111">W menu centralnym kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="662a8-111">On the Hub menu, click **More Services**.</span></span>

    ![Otwórz listę magazynów usług odzyskiwania — krok 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="662a8-113">Chcesz otworzyć magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="662a8-114">W oknie dialogowym zacznij pisać **usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="662a8-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="662a8-115">Po rozpoczęciu pisania zawartość listy będzie filtrowana w oparciu o wpisywane dane.</span><span class="sxs-lookup"><span data-stu-id="662a8-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="662a8-116">Kliknij przycisk **Magazyny usług odzyskiwania** do wyświetlenia na liście magazynów usług odzyskiwania w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="662a8-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="662a8-118">Otwiera listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-118">The list of Recovery Services vaults opens.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="662a8-120">Z listy magazynów wybierz nazwę magazynu usług odzyskiwania, który chcesz otworzyć.</span><span class="sxs-lookup"><span data-stu-id="662a8-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="662a8-121">Zostanie otwarty blok pulpitu nawigacyjnego magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![pulpitem nawigacyjnym magazynu usług odzyskiwania](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="662a8-123">Po otwarciu magazyn usług odzyskiwania wypróbować zadań monitorowania lub zarządzania.</span><span class="sxs-lookup"><span data-stu-id="662a8-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="662a8-124">Monitorowanie zadań tworzenia kopii zapasowej i alerty</span><span class="sxs-lookup"><span data-stu-id="662a8-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="662a8-125">Można monitorować, zadania i alerty na pulpicie nawigacyjnym magazynu usług odzyskiwania, w której występuje:</span><span class="sxs-lookup"><span data-stu-id="662a8-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="662a8-126">Szczegóły alerty kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-126">Backup alerts details</span></span>
* <span data-ttu-id="662a8-127">Pliki i foldery, a także chronione w chmurze maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="662a8-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="662a8-128">Całkowita ilość miejsca zużyte na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="662a8-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="662a8-129">Stan zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-129">Backup job status</span></span>

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="662a8-131">Informacje zawarte w każdej z tych kafelków kliknięcie spowoduje otwarcie bloku skojarzone, w których zarządzasz powiązanych zadań.</span><span class="sxs-lookup"><span data-stu-id="662a8-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="662a8-132">W górnej części pulpitu nawigacyjnego:</span><span class="sxs-lookup"><span data-stu-id="662a8-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="662a8-133">Ustawienia zapewnia dostęp dostępnych zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="662a8-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="662a8-134">Wykonywanie kopii zapasowej — umożliwia wykonanie kopii zapasowej nowe pliki i foldery (lub maszyn wirtualnych platformy Azure) w magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="662a8-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="662a8-135">Delete — Jeśli magazyn usług odzyskiwania jest już używana, można usunąć go w celu zwolnienia miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="662a8-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="662a8-136">DELETE jest włączona tylko po usunięciu wszystkich chronionych serwerach z magazynu.</span><span class="sxs-lookup"><span data-stu-id="662a8-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="662a8-138">Alerty kopii zapasowych za pomocą agenta kopii zapasowej systemu Azure:</span><span class="sxs-lookup"><span data-stu-id="662a8-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="662a8-139">Poziom alertu</span><span class="sxs-lookup"><span data-stu-id="662a8-139">Alert Level</span></span> | <span data-ttu-id="662a8-140">Wysyłania alertów</span><span class="sxs-lookup"><span data-stu-id="662a8-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="662a8-141">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="662a8-141">Critical</span></span> |<span data-ttu-id="662a8-142">Niepowodzenia wykonywania kopii zapasowej, niepowodzenia odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="662a8-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="662a8-143">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="662a8-143">Warning</span></span> |<span data-ttu-id="662a8-144">Kopia zapasowa zakończona z ostrzeżeniami (jeśli jest mniej niż sto nie kopii zapasowej plików z powodu uszkodzenia problemów i pomyślnie kopii zapasowej plików ponad milion)</span><span class="sxs-lookup"><span data-stu-id="662a8-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="662a8-145">Informacyjny</span><span class="sxs-lookup"><span data-stu-id="662a8-145">Informational</span></span> |<span data-ttu-id="662a8-146">Brak</span><span class="sxs-lookup"><span data-stu-id="662a8-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="662a8-147">Zarządzanie alertami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-147">Manage Backup alerts</span></span>
<span data-ttu-id="662a8-148">Kliknij przycisk **alerty kopii zapasowej** Kafelek, aby otworzyć **alerty kopii zapasowej** blok alerty i zarządzaj nimi.</span><span class="sxs-lookup"><span data-stu-id="662a8-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Alerty kopii zapasowej](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="662a8-150">Kafelek alerty kopii zapasowej jest wyświetlana liczba:</span><span class="sxs-lookup"><span data-stu-id="662a8-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="662a8-151">alerty krytyczne nierozpoznane w ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="662a8-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="662a8-152">alerty ostrzegawcze nierozpoznane w ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="662a8-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="662a8-153">Kliknięcie na każdym z nich umożliwia przejście do **alerty kopii zapasowej** bloku filtrowany widok alertów (krytyczna lub poważna).</span><span class="sxs-lookup"><span data-stu-id="662a8-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="662a8-154">W bloku alerty kopii zapasowej możesz:</span><span class="sxs-lookup"><span data-stu-id="662a8-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="662a8-155">Wybierz odpowiednie informacje, aby uwzględnić z alertami.</span><span class="sxs-lookup"><span data-stu-id="662a8-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Wybierz kolumny](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="662a8-157">Filtrowanie alertów na czas ważności, stanu i rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="662a8-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="662a8-159">Konfigurowanie powiadomień o ważności, częstotliwości i adresatów, a także włączyć alerty lub wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="662a8-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="662a8-161">Jeśli **na alertu** został wybrany jako **powiadamiania** częstotliwość nie grupowania lub zmniejszenia w wiadomościach e-mail.</span><span class="sxs-lookup"><span data-stu-id="662a8-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="662a8-162">Każdy alert powoduje 1 powiadomień.</span><span class="sxs-lookup"><span data-stu-id="662a8-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="662a8-163">To jest ustawienie domyślne i rozpoznawania wiadomości e-mail jest również wysyłane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="662a8-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="662a8-164">Jeśli **co godzinę szyfrowanego** został wybrany jako **powiadamiania** częstotliwość jeden adres e-mail jest wysyłane do użytkownika informacją, które istnieją nierozwiązane nowe alerty wygenerowane w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="662a8-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="662a8-165">Wiadomość e-mail z rozwiązania jest wysyłane na koniec godziny.</span><span class="sxs-lookup"><span data-stu-id="662a8-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="662a8-166">Alerty mogą być wysyłane do następujących poziomów ważności:</span><span class="sxs-lookup"><span data-stu-id="662a8-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="662a8-167">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="662a8-167">critical</span></span>
* <span data-ttu-id="662a8-168">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="662a8-168">warning</span></span>
* <span data-ttu-id="662a8-169">Informacje</span><span class="sxs-lookup"><span data-stu-id="662a8-169">information</span></span>

<span data-ttu-id="662a8-170">Dezaktywuj alert o **Dezaktywuj** przycisk w bloku szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="662a8-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="662a8-171">Po kliknięciu Dezaktywuj, możesz podać informacje o rozdzielczości.</span><span class="sxs-lookup"><span data-stu-id="662a8-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="662a8-172">Wybierz kolumny mają być wyświetlane jako część alert o **wybierz kolumny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="662a8-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="662a8-173">Z **ustawienia** bloku Zarządzanie alerty kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > Alerty i zdarzenia > Alerty kopii zapasowej** , a następnie klikając polecenie **filtru** lub  **Konfigurowanie powiadomień**.</span><span class="sxs-lookup"><span data-stu-id="662a8-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="662a8-174">Zarządzaj elementami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-174">Manage Backup items</span></span>
<span data-ttu-id="662a8-175">Zarządzanie lokalnymi kopiami zapasowymi jest teraz dostępna w portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="662a8-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="662a8-176">W sekcji Backup pulpitu nawigacyjnego **elementów kopii zapasowych** kafelka pokazuje liczbę elementów kopii zapasowych chronionych w magazynie.</span><span class="sxs-lookup"><span data-stu-id="662a8-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="662a8-177">Kliknij przycisk **folderów plików** w elementach kopii zapasowej kafelka.</span><span class="sxs-lookup"><span data-stu-id="662a8-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="662a8-179">Z zestaw do plików i folderów, w której występuje każdej kopii zapasowej elementów na liście filtrów zostanie otwarty blok elementów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="662a8-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Elementy kopii zapasowej](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="662a8-181">Jeśli określony element kopii zapasowej wybierz z listy, zobaczysz istotne szczegóły dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="662a8-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="662a8-182">Z **ustawienia** bloku zarządzania plikami i folderami wybierając **chronione elementy > kopii zapasowej elementów** , a następnie wybierając **folderów plików** z menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="662a8-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="662a8-184">Zarządzanie zadaniami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-184">Manage Backup jobs</span></span>
<span data-ttu-id="662a8-185">Kopia zapasowa zadania na lokalnie, (Jeśli serwer lokalny jest tworzenie kopii zapasowej na platformie Azure) i kopii zapasowych Azure są widoczne na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="662a8-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="662a8-186">W sekcji kopii zapasowej w pulpicie nawigacyjnym kafelka zadania tworzenia kopii zapasowej pokazuje liczbę zadań:</span><span class="sxs-lookup"><span data-stu-id="662a8-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="662a8-187">w toku</span><span class="sxs-lookup"><span data-stu-id="662a8-187">in progress</span></span>
* <span data-ttu-id="662a8-188">Nie można w ciągu ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="662a8-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="662a8-189">Aby zarządzać zadaniami kopii zapasowej, kliknij przycisk **zadania tworzenia kopii zapasowej** kafelka, która otwiera blok zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="662a8-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="662a8-191">Modyfikowanie informacji dostępnych w bloku zadania tworzenia kopii zapasowej z **wybierz kolumny** u góry strony.</span><span class="sxs-lookup"><span data-stu-id="662a8-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="662a8-192">Użyj **filtru** przycisk, aby wybrać między plików i folderów z kopii zapasowej maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="662a8-193">Jeśli nie widzisz z kopii zapasowej plików i folderów, kliknij przycisk **filtru** u góry strony i wybierz **pliki i foldery** typu elementu menu.</span><span class="sxs-lookup"><span data-stu-id="662a8-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="662a8-194">Z **ustawienia** bloku Zarządzanie zadania tworzenia kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > zadania > zadań tworzenia kopii zapasowej** , a następnie wybierając **folderów plików** z listy rozwijanej menu.</span><span class="sxs-lookup"><span data-stu-id="662a8-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="662a8-195">Monitorowanie użycia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="662a8-195">Monitor Backup usage</span></span>
<span data-ttu-id="662a8-196">W sekcji kopii zapasowej w pulpicie nawigacyjnym kafelka użycie kopii zapasowej zawiera magazynu używane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="662a8-197">Użycie magazynu jest dostępne:</span><span class="sxs-lookup"><span data-stu-id="662a8-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="662a8-198">Użycie magazynu LRS skojarzonego z magazynem w chmurze</span><span class="sxs-lookup"><span data-stu-id="662a8-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="662a8-199">Użycie magazynu grs w warstwie skojarzonego z magazynem w chmurze</span><span class="sxs-lookup"><span data-stu-id="662a8-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="662a8-200">Zarządzanie serwerami produkcji</span><span class="sxs-lookup"><span data-stu-id="662a8-200">Manage your production servers</span></span>
<span data-ttu-id="662a8-201">Aby zarządzać serwerów produkcyjnych, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="662a8-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="662a8-202">W obszarze Zarządzanie kliknij **infrastruktura kopii zapasowej > serwerów produkcyjnych**.</span><span class="sxs-lookup"><span data-stu-id="662a8-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="662a8-203">Wyświetla blok serwerów produkcyjnych serwerów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="662a8-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="662a8-204">Kliknij serwer, na liście, aby otworzyć szczegóły serwera.</span><span class="sxs-lookup"><span data-stu-id="662a8-204">Click on a server in the list to open the server details.</span></span>

![Elementy chronione](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="662a8-206">Otwórz agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="662a8-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="662a8-207">Otwórz **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj komputer dla *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="662a8-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="662a8-209">Z **akcje** dostępne po prawej stronie konsoli agenta kopii zapasowej, należy wykonać następujące zadania zarządzania:</span><span class="sxs-lookup"><span data-stu-id="662a8-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="662a8-210">Zarejestruj serwer</span><span class="sxs-lookup"><span data-stu-id="662a8-210">Register Server</span></span>
* <span data-ttu-id="662a8-211">Harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="662a8-211">Schedule Backup</span></span>
* <span data-ttu-id="662a8-212">Wykonaj kopię zapasową teraz</span><span class="sxs-lookup"><span data-stu-id="662a8-212">Back Up now</span></span>
* <span data-ttu-id="662a8-213">Zmień właściwości</span><span class="sxs-lookup"><span data-stu-id="662a8-213">Change Properties</span></span>

![Akcje konsoli agenta usługi Kopia zapasowa Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="662a8-215">Aby **odzyskać dane**, zobacz [przywrócić pliki do systemu Windows server lub komputer kliencki z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="662a8-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="662a8-216">Zmodyfikuj harmonogram kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="662a8-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="662a8-217">W agencie kopia zapasowa Microsoft Azure kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="662a8-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="662a8-219">W **Kreatora kopii zapasowych harmonogram** pozostaw **wprowadzanie zmian do elementów kopii zapasowych lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="662a8-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="662a8-221">Jeśli chcesz dodać lub zmienić elementy, na **Wybieranie elementów do wykonania kopii zapasowej** ekranu kliknij **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="662a8-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="662a8-222">Można również ustawić **ustawienia wykluczania** na tej stronie kreatora.</span><span class="sxs-lookup"><span data-stu-id="662a8-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="662a8-223">Jeśli chcesz wykluczyć pliki lub typów plików zapoznać się z procedurą dodawania [ustawienia wykluczania](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="662a8-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="662a8-224">Wybierz pliki i foldery, które chcesz utworzyć kopię zapasową, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="662a8-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="662a8-226">Określ **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="662a8-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="662a8-227">Można zaplanować codziennie (maksymalnie 3 razy dziennie) lub cotygodniowe kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="662a8-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="662a8-229">Określanie harmonogramu tworzenia kopii zapasowych omówiono szczegółowo w tym [artykułu](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="662a8-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="662a8-230">Wybierz **zasady przechowywania** kopii zapasowej i kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="662a8-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="662a8-232">Na **potwierdzenie** ekranu Przejrzyj informacje i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="662a8-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="662a8-233">Po zakończeniu pracy Kreatora tworzenia **harmonogram tworzenia kopii zapasowych**, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="662a8-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="662a8-234">Po zmodyfikowaniu ochrony, można potwierdzić poprawnie wyzwalają kopii zapasowych, przechodząc do **zadania** kartę i potwierdzenie, że zmiany zostaną odzwierciedlone w zadania tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="662a8-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="662a8-235">Włącz ograniczanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="662a8-235">Enable Network Throttling</span></span>

<span data-ttu-id="662a8-236">Agent usługi Kopia zapasowa Azure udostępnia na karcie ograniczenia przepustowości, dzięki czemu można kontrolować sposób używania przepustowości sieci podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="662a8-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="662a8-237">Ten formant może być przydatne, jeśli chcesz utworzyć kopię zapasową danych podczas godziny pracy, ale nie chcesz procesu tworzenia kopii zapasowej z innych ruch internetowy.</span><span class="sxs-lookup"><span data-stu-id="662a8-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="662a8-238">Ograniczanie danych transfer ma zastosowanie do kopii zapasowej i przywracania działań.</span><span class="sxs-lookup"><span data-stu-id="662a8-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="662a8-239">Aby włączyć ograniczenie przepustowości:</span><span class="sxs-lookup"><span data-stu-id="662a8-239">To enable throttling:</span></span>

1. <span data-ttu-id="662a8-240">W **agent usługi Kopia zapasowa**, kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="662a8-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="662a8-241">Na ** ograniczania kartę, zaznacz **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="662a8-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Ograniczanie przepustowości sieci](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="662a8-243">Po włączeniu ograniczenia przepustowości określić dozwolonych przepustowością transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.</span><span class="sxs-lookup"><span data-stu-id="662a8-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="662a8-244">Wartości przepustowości rozpoczynały 512 kilobajtach na sekundę (KB/s) i można przejść do 1023 MB na sekundę (MB/s).</span><span class="sxs-lookup"><span data-stu-id="662a8-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="662a8-245">Można również wyznaczyć rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia, są traktowane jako pracy dni.</span><span class="sxs-lookup"><span data-stu-id="662a8-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="662a8-246">Czas poza godzinami pracy wyznaczonych jest uważany za godzin wolnych.</span><span class="sxs-lookup"><span data-stu-id="662a8-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="662a8-247">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="662a8-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="662a8-248">Zarządzanie ustawieniami wykluczeń</span><span class="sxs-lookup"><span data-stu-id="662a8-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="662a8-249">Otwórz **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="662a8-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="662a8-251">W agencie kopia zapasowa Microsoft Azure kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="662a8-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="662a8-253">W pozostaw Kreatora kopii zapasowych harmonogram **wprowadzanie zmian do elementów kopii zapasowych lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="662a8-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="662a8-255">Kliknij przycisk **ustawienia wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="662a8-255">Click **Exclusions Settings**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="662a8-257">Kliknij przycisk **Dodaj wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="662a8-257">Click **Add Exclusion**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="662a8-259">Wybierz lokalizację, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="662a8-259">Select the location and then, click **OK**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="662a8-261">Dodaj rozszerzenie pliku w **typ pliku** pola.</span><span class="sxs-lookup"><span data-stu-id="662a8-261">Add the file extension in the **File Type** field.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="662a8-263">Dodawanie rozszerzenia MP3</span><span class="sxs-lookup"><span data-stu-id="662a8-263">Adding an .mp3 extension</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="662a8-265">Aby dodać inne rozszerzenie, kliknij przycisk **Dodawanie wykluczenia** i wprowadź inne rozszerzenie typu pliku (Dodawanie rozszerzenia .jpeg).</span><span class="sxs-lookup"><span data-stu-id="662a8-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="662a8-267">Po dodaniu wszystkich rozszerzeń, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="662a8-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="662a8-268">Kontynuuj pracę Kreatora harmonogramu kopii zapasowej, klikając **dalej** do momentu **stronę potwierdzenia**, następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="662a8-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="662a8-270">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="662a8-270">Frequently asked questions</span></span>
<span data-ttu-id="662a8-271">**1. Stan zadania tworzenia kopii zapasowej jest wyświetlana jako zakończone Azure agenta kopii zapasowej, dlaczego nie go pobrać natychmiast odzwierciedlone w portalu?**</span><span class="sxs-lookup"><span data-stu-id="662a8-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="662a8-272">Odpowiedź 1.</span><span class="sxs-lookup"><span data-stu-id="662a8-272">A1.</span></span> <span data-ttu-id="662a8-273">Jest w Maksymalne opóźnienie w ciągu 15 minut między stan zadania tworzenia kopii zapasowej zostaną uwzględnione w agenta kopii zapasowej systemu Azure i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="662a8-274">**Q.2, gdy zadanie tworzenia kopii zapasowej nie powiedzie się, jak długo trwa Zgłoś alert?**</span><span class="sxs-lookup"><span data-stu-id="662a8-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="662a8-275">A.2 alert jest uruchamiany w ciągu 20 minutach niepowodzenia wykonywania kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="662a8-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="662a8-276">**K3. Jest przypadek, w którym nie będzie wysyłana wiadomość e-mail, jeśli skonfigurowano powiadomienia?**</span><span class="sxs-lookup"><span data-stu-id="662a8-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="662a8-277">Odpowiedź 3.</span><span class="sxs-lookup"><span data-stu-id="662a8-277">A3.</span></span> <span data-ttu-id="662a8-278">Poniżej są przypadkach, gdy nie będą wysyłane powiadomienia w celu zmniejszenia szumu alertu:</span><span class="sxs-lookup"><span data-stu-id="662a8-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="662a8-279">Jeśli powiadomienia są skonfigurowane co godzinę, a alert jest uruchamiany rozwiązane w ciągu godziny</span><span class="sxs-lookup"><span data-stu-id="662a8-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="662a8-280">Zadanie zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="662a8-280">Job is canceled.</span></span>
* <span data-ttu-id="662a8-281">Drugi zadanie tworzenia kopii zapasowej nie powiodło się, ponieważ oryginalne zadanie tworzenia kopii zapasowej jest w toku.</span><span class="sxs-lookup"><span data-stu-id="662a8-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="662a8-282">Rozwiązywanie problemów monitorowania</span><span class="sxs-lookup"><span data-stu-id="662a8-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="662a8-283">**Problem:** zadania i/lub alerty z usługi Azure Backup agent nie są wyświetlane w portalu.</span><span class="sxs-lookup"><span data-stu-id="662a8-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="662a8-284">**Kroki rozwiązywania problemów:** procesu ```OBRecoveryServicesManagementAgent```, wysyła dane zadanie i alert do usługi Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="662a8-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="662a8-285">Czasami ten proces może zostać wstrzymana lub zamknięcie.</span><span class="sxs-lookup"><span data-stu-id="662a8-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="662a8-286">Aby sprawdzić, proces nie działa, otwórz **Menedżera zadań** i sprawdź, czy ```OBRecoveryServicesManagementAgent``` proces jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="662a8-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="662a8-287">Przy założeniu, że proces nie działa, otwórz **Panelu sterowania** , a następnie przejdź na liście usług.</span><span class="sxs-lookup"><span data-stu-id="662a8-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="662a8-288">Uruchom lub uruchom ponownie **agenta usług odzyskiwania Microsoft Azure w zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="662a8-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="662a8-289">Aby uzyskać więcej informacji Przejdź dzienniki na:</span><span class="sxs-lookup"><span data-stu-id="662a8-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="662a8-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Na przykład:</span><span class="sxs-lookup"><span data-stu-id="662a8-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="662a8-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="662a8-291">Next steps</span></span>
* [<span data-ttu-id="662a8-292">Przywracanie systemu Windows Server lub klienta systemu Windows z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="662a8-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="662a8-293">Aby dowiedzieć się więcej na temat tworzenia kopii zapasowej Azure, zobacz [Omówienie programu Kopia zapasowa Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="662a8-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="662a8-294">Odwiedź stronę [Forum kopii zapasowej platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="662a8-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
