---
title: "usług odzyskiwania Azure aaaManage magazynami i serwerami | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toolearn jak magazyny usług odzyskiwania Azure toomanage i serwerów."
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
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="2d190-103">Monitorowanie magazynów i serwerów usługi Azure Recovery Services i zarządzanie nimi dla maszyn z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="2d190-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d190-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d190-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="2d190-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="2d190-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="2d190-106">W tym artykule znajdziesz omówienie hello zadania tworzenia kopii zapasowych monitorowanie i zarządzanie dostępne za pośrednictwem hello Azure portal i hello agenta kopii zapasowej Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2d190-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="2d190-107">W tym artykule przyjęto założenie, już mieć subskrypcję platformy Azure i został utworzony co najmniej jeden magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="2d190-108">Otwórz magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="2d190-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="2d190-109">pulpitem nawigacyjnym magazynu usług odzyskiwania Hello przedstawia szczegóły hello lub atrybuty z magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="2d190-110">Zaloguj się toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d190-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="2d190-111">W menu Centrum powitania kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="2d190-111">On hello Hub menu, click **More Services**.</span></span>

    ![Otwórz listę magazynów usług odzyskiwania — krok 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="2d190-113">Ma tooopen magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="2d190-114">Okno dialogowe hello, zacznij pisać **usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="2d190-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="2d190-115">Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="2d190-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="2d190-116">Kliknij przycisk **Magazyny usług odzyskiwania** magazyny toodisplay hello listę usług odzyskiwania w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2d190-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="2d190-118">Otwiera Hello listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-118">hello list of Recovery Services vaults opens.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="2d190-120">Z listy hello magazynów wybierz nazwę hello hello ma tooopen magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="2d190-121">zostanie otwarty blok pulpitu nawigacyjnego magazynu usług odzyskiwania Hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![pulpitem nawigacyjnym magazynu usług odzyskiwania](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="2d190-123">Po otwarciu magazyn usług odzyskiwania hello wypróbować hello zadań monitorowania lub zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2d190-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="2d190-124">Monitorowanie zadań tworzenia kopii zapasowej i alerty</span><span class="sxs-lookup"><span data-stu-id="2d190-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="2d190-125">Monitoruj zadania i alerty z hello magazyn usług odzyskiwania i pulpitu nawigacyjnego, której występuje:</span><span class="sxs-lookup"><span data-stu-id="2d190-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="2d190-126">Szczegóły alerty kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-126">Backup alerts details</span></span>
* <span data-ttu-id="2d190-127">Pliki i foldery, a także chroniona w chmurze hello maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d190-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="2d190-128">Całkowita ilość miejsca zużyte na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="2d190-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="2d190-129">Stan zadania tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-129">Backup job status</span></span>

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="2d190-131">Kliknięcie przycisku hello informacji w każdym z tych kafelków spowoduje otwarcie bloku skojarzone hello, w których zarządzasz powiązanych zadań.</span><span class="sxs-lookup"><span data-stu-id="2d190-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="2d190-132">Z góry hello hello pulpitu nawigacyjnego:</span><span class="sxs-lookup"><span data-stu-id="2d190-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="2d190-133">Ustawienia zapewnia dostęp dostępnych zadań tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2d190-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="2d190-134">Magazyn kopii zapasowych — umożliwia wykonanie kopii zapasowej nowe pliki i foldery (lub maszyn wirtualnych platformy Azure) toohello usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="2d190-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="2d190-135">Delete — Jeśli magazyn usług odzyskiwania jest już używana, można usunąć toofree miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="2d190-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="2d190-136">DELETE jest włączona tylko po usunięciu wszystkich chronionych serwerach z hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="2d190-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="2d190-138">Alerty kopii zapasowych za pomocą agenta kopii zapasowej systemu Azure:</span><span class="sxs-lookup"><span data-stu-id="2d190-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="2d190-139">Poziom alertu</span><span class="sxs-lookup"><span data-stu-id="2d190-139">Alert Level</span></span> | <span data-ttu-id="2d190-140">Wysyłania alertów</span><span class="sxs-lookup"><span data-stu-id="2d190-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="2d190-141">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="2d190-141">Critical</span></span> |<span data-ttu-id="2d190-142">Niepowodzenia wykonywania kopii zapasowej, niepowodzenia odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="2d190-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="2d190-143">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="2d190-143">Warning</span></span> |<span data-ttu-id="2d190-144">Kopia zapasowa zakończona z ostrzeżeniami (jeśli jest mniej niż sto nie kopii zapasowej plików powodu toocorruption problemów i pomyślnie kopii zapasowej plików ponad milion)</span><span class="sxs-lookup"><span data-stu-id="2d190-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="2d190-145">Informacyjny</span><span class="sxs-lookup"><span data-stu-id="2d190-145">Informational</span></span> |<span data-ttu-id="2d190-146">Brak</span><span class="sxs-lookup"><span data-stu-id="2d190-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="2d190-147">Zarządzanie alertami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-147">Manage Backup alerts</span></span>
<span data-ttu-id="2d190-148">Kliknij przycisk hello **alerty kopii zapasowej** hello tooopen kafelka **alerty kopii zapasowej** blok alerty i zarządzaj nimi.</span><span class="sxs-lookup"><span data-stu-id="2d190-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Alerty kopii zapasowej](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="2d190-150">Witaj alerty kopii zapasowej kafelka pokazuje hello liczba:</span><span class="sxs-lookup"><span data-stu-id="2d190-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="2d190-151">alerty krytyczne nierozpoznane w ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="2d190-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="2d190-152">alerty ostrzegawcze nierozpoznane w ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="2d190-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="2d190-153">Kliknięcie na każdym z tych łączy powoduje toohello **alerty kopii zapasowej** bloku filtrowany widok alertów (krytyczna lub poważna).</span><span class="sxs-lookup"><span data-stu-id="2d190-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="2d190-154">W bloku hello alerty kopii zapasowej możesz:</span><span class="sxs-lookup"><span data-stu-id="2d190-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="2d190-155">Wybierz hello tooinclude odpowiednie informacje o alerty.</span><span class="sxs-lookup"><span data-stu-id="2d190-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Wybierz kolumny](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="2d190-157">Filtrowanie alertów na czas ważności, stanu i rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="2d190-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="2d190-159">Konfigurowanie powiadomień o ważności, częstotliwości i adresatów, a także włączyć alerty lub wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="2d190-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrowanie alertów](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="2d190-161">Jeśli **na alertu** został wybrany jako hello **powiadamiania** częstotliwość nie grupowania lub zmniejszenia w wiadomościach e-mail.</span><span class="sxs-lookup"><span data-stu-id="2d190-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="2d190-162">Każdy alert powoduje 1 powiadomień.</span><span class="sxs-lookup"><span data-stu-id="2d190-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="2d190-163">To jest ustawienie domyślne hello i hello rozpoznawania e-mail jest również wysyłane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="2d190-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="2d190-164">Jeśli **co godzinę szyfrowanego** został wybrany jako hello **powiadamiania** częstotliwość jeden adres e-mail jest wysyłana użytkownika toohello informacją, które istnieją nierozwiązane nowe alerty wygenerowane w hello ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="2d190-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="2d190-165">Wiadomość e-mail z rozwiązania jest wysyłane na końcu hello hello godzinę.</span><span class="sxs-lookup"><span data-stu-id="2d190-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="2d190-166">Alerty mogą być wysyłane do hello następujące poziomy ważności:</span><span class="sxs-lookup"><span data-stu-id="2d190-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="2d190-167">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="2d190-167">critical</span></span>
* <span data-ttu-id="2d190-168">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="2d190-168">warning</span></span>
* <span data-ttu-id="2d190-169">Informacje</span><span class="sxs-lookup"><span data-stu-id="2d190-169">information</span></span>

<span data-ttu-id="2d190-170">Dezaktywuj alert hello z hello **Dezaktywuj** przycisku na powitania zadania szczegóły blok.</span><span class="sxs-lookup"><span data-stu-id="2d190-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="2d190-171">Po kliknięciu Dezaktywuj, możesz podać informacje o rozdzielczości.</span><span class="sxs-lookup"><span data-stu-id="2d190-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="2d190-172">Wybierz kolumny hello ma tooappear jako część hello alertu o hello **wybierz kolumny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d190-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="2d190-173">Z hello **ustawienia** bloku Zarządzanie alerty kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > Alerty i zdarzenia > Alerty kopii zapasowej** , a następnie klikając polecenie **filtru** lub  **Konfigurowanie powiadomień**.</span><span class="sxs-lookup"><span data-stu-id="2d190-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="2d190-174">Zarządzaj elementami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-174">Manage Backup items</span></span>
<span data-ttu-id="2d190-175">Zarządzanie lokalnymi kopiami zapasowymi jest teraz dostępna w portalu zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="2d190-176">W sekcji kopii zapasowej hello pulpitu nawigacyjnego hello hello **elementów kopii zapasowych** kafelka zawiera hello liczbę elementów kopii zapasowych chronionych toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="2d190-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="2d190-177">Kliknij przycisk **folderów plików** w hello kafelka elementy kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2d190-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="2d190-179">Hello elementów kopii zapasowych, który zostanie otwarty blok z hello filtrować tooFile zestaw folderów, której występuje każdej kopii zapasowej elementów na liście.</span><span class="sxs-lookup"><span data-stu-id="2d190-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Elementy kopii zapasowej](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="2d190-181">W przypadku wybrania określonego elementu kopii zapasowej z listy hello widzisz hello niezbędne szczegóły dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="2d190-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="2d190-182">Z hello **ustawienia** bloku zarządzania plikami i folderami wybierając **chronione elementy > kopii zapasowej elementów** , a następnie wybierając **folderów plików** z hello menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="2d190-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="2d190-184">Zarządzanie zadaniami kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-184">Manage Backup jobs</span></span>
<span data-ttu-id="2d190-185">Zadania tworzenia kopii zapasowej zarówno na lokalnym (Jeśli serwer lokalne powitania wykonuje kopię zapasową tooAzure), jak i kopii zapasowych Azure są widoczne na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="2d190-186">W hello kopii zapasowej części pulpitu nawigacyjnego hello kafelka zadania tworzenia kopii zapasowej hello pokazuje hello liczbę zadań:</span><span class="sxs-lookup"><span data-stu-id="2d190-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="2d190-187">w toku</span><span class="sxs-lookup"><span data-stu-id="2d190-187">in progress</span></span>
* <span data-ttu-id="2d190-188">Wystąpił błąd na powitania ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="2d190-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="2d190-189">toomanage zadań kopii zapasowych, kliknij przycisk hello **zadania tworzenia kopii zapasowej** kafelka, która otwiera blok zadań tworzenia kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Elementy kopii zapasowej z ustawień](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="2d190-191">Modyfikowanie hello informacje są dostępne w bloku zadania tworzenia kopii zapasowej hello z hello **wybierz kolumny** przycisk u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="2d190-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="2d190-192">Użyj hello **filtru** tooselect przycisk między plików i folderów z kopii zapasowej maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d190-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="2d190-193">Jeśli nie widzisz z kopii zapasowej plików i folderów, kliknij przycisk **filtru** u góry hello hello strony i wybierz **pliki i foldery** hello typu elementu menu.</span><span class="sxs-lookup"><span data-stu-id="2d190-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="2d190-194">Z hello **ustawienia** bloku Zarządzanie zadania tworzenia kopii zapasowej przez zaznaczenie **monitorowanie i Raporty > zadania > zadań tworzenia kopii zapasowej** , a następnie wybierając **folderów plików** z listy hello menu.</span><span class="sxs-lookup"><span data-stu-id="2d190-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="2d190-195">Monitorowanie użycia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="2d190-195">Monitor Backup usage</span></span>
<span data-ttu-id="2d190-196">W kopii zapasowej części pulpitu nawigacyjnego hello hello Kafelek użycie kopii zapasowej hello pokazuje magazynu hello zużyte na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2d190-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="2d190-197">Użycie magazynu jest dostępne:</span><span class="sxs-lookup"><span data-stu-id="2d190-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="2d190-198">Użycie magazynu LRS skojarzony z magazynem hello w chmurze</span><span class="sxs-lookup"><span data-stu-id="2d190-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="2d190-199">Użycie magazynu GRS skojarzony z magazynem hello w chmurze</span><span class="sxs-lookup"><span data-stu-id="2d190-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="2d190-200">Zarządzanie serwerami produkcji</span><span class="sxs-lookup"><span data-stu-id="2d190-200">Manage your production servers</span></span>
<span data-ttu-id="2d190-201">toomanage serwerów produkcyjnych, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="2d190-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="2d190-202">W obszarze Zarządzanie kliknij **infrastruktura kopii zapasowej > serwerów produkcyjnych**.</span><span class="sxs-lookup"><span data-stu-id="2d190-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="2d190-203">Witaj list bloku serwerów produkcyjnych serwerów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="2d190-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="2d190-204">Kliknij serwer w szczegóły hello listy tooopen powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="2d190-204">Click on a server in hello list tooopen hello server details.</span></span>

![Elementy chronione](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="2d190-206">Otwórz hello agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="2d190-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="2d190-207">Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj komputer dla *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="2d190-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="2d190-209">Z hello **akcje** dostępne pod adresem hello rogu konsoli agenta kopii zapasowej hello, należy wykonać następujące zadania zarządzania hello:</span><span class="sxs-lookup"><span data-stu-id="2d190-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="2d190-210">Zarejestruj serwer</span><span class="sxs-lookup"><span data-stu-id="2d190-210">Register Server</span></span>
* <span data-ttu-id="2d190-211">Harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="2d190-211">Schedule Backup</span></span>
* <span data-ttu-id="2d190-212">Wykonaj kopię zapasową teraz</span><span class="sxs-lookup"><span data-stu-id="2d190-212">Back Up now</span></span>
* <span data-ttu-id="2d190-213">Zmień właściwości</span><span class="sxs-lookup"><span data-stu-id="2d190-213">Change Properties</span></span>

![Akcje konsoli agenta usługi Kopia zapasowa Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="2d190-215">zbyt**odzyskać dane**, zobacz [przywrócić pliki tooa systemu Windows server lub komputer kliencki z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="2d190-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="2d190-216">Zmodyfikuj harmonogram kopii zapasowych hello</span><span class="sxs-lookup"><span data-stu-id="2d190-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="2d190-217">W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="2d190-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="2d190-219">W hello **Kreatora harmonogramu kopii zapasowej** pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2d190-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="2d190-221">Jeśli chcesz tooadd lub zmienić elementy na powitania **tooBackup wybierz elementy** ekranu kliknij **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="2d190-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="2d190-222">Można również ustawić **ustawienia wykluczania** na tej stronie kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="2d190-223">Jeśli pliki tooexclude lub typów plików odczytu hello procedurę dodawania [ustawienia wykluczania](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="2d190-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="2d190-224">Wybierz hello pliki i foldery mają tooback w górę i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d190-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="2d190-226">Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2d190-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="2d190-227">Można zaplanować codziennie (maksymalnie 3 razy dziennie) lub cotygodniowe kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="2d190-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="2d190-229">Określanie harmonogramu tworzenia kopii zapasowych hello omówiono szczegółowo w tym [artykułu](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="2d190-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="2d190-230">Wybierz hello **zasady przechowywania** hello kopii zapasowej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2d190-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="2d190-232">Na powitania **potwierdzenie** ekran Przegląd hello informacji i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2d190-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="2d190-233">Gdy Kreator hello zakończy tworzenie hello **harmonogram tworzenia kopii zapasowych**, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="2d190-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="2d190-234">Po zmodyfikowaniu ochrony, można potwierdzić poprawnie wyzwalają kopii zapasowych przez przejście toohello **zadania** kartę i potwierdzenie, że zmiany zostaną odzwierciedlone w hello kopii zapasowej zadania.</span><span class="sxs-lookup"><span data-stu-id="2d190-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="2d190-235">Włącz ograniczanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="2d190-235">Enable Network Throttling</span></span>

<span data-ttu-id="2d190-236">agent usługi Kopia zapasowa Azure Hello zawiera kartę ograniczenia przepustowości, co pozwala toocontrol wykorzystaniem przepustowości sieci podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="2d190-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="2d190-237">Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy.</span><span class="sxs-lookup"><span data-stu-id="2d190-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="2d190-238">Ograniczanie danych transfer stosuje tooback zapasową i przywrócić działań.</span><span class="sxs-lookup"><span data-stu-id="2d190-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="2d190-239">Ograniczanie tooenable:</span><span class="sxs-lookup"><span data-stu-id="2d190-239">tooenable throttling:</span></span>

1. <span data-ttu-id="2d190-240">W hello **agent usługi Kopia zapasowa**, kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2d190-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="2d190-241">Na powitania ** ograniczania kartę, zaznacz **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="2d190-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Ograniczanie przepustowości sieci](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="2d190-243">Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.</span><span class="sxs-lookup"><span data-stu-id="2d190-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="2d190-244">wartości przepustowości Hello rozpoczynały 512 kilobajtach na sekundę (KB/s) i można przejść w górę too1023 MB na sekundę (MB/s).</span><span class="sxs-lookup"><span data-stu-id="2d190-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="2d190-245">Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są traktowane jako pracy dni.</span><span class="sxs-lookup"><span data-stu-id="2d190-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="2d190-246">czas Hello poza Witaj wyznaczone godzin pracy jest godzin wolnych toobe rozważenia.</span><span class="sxs-lookup"><span data-stu-id="2d190-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="2d190-247">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d190-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="2d190-248">Zarządzanie ustawieniami wykluczeń</span><span class="sxs-lookup"><span data-stu-id="2d190-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="2d190-249">Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="2d190-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="2d190-251">W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="2d190-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="2d190-253">W hello Kreatora harmonogramu kopii zapasowej pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2d190-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="2d190-255">Kliknij przycisk **ustawienia wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="2d190-255">Click **Exclusions Settings**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="2d190-257">Kliknij przycisk **Dodaj wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="2d190-257">Click **Add Exclusion**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="2d190-259">Wybierz lokalizację hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d190-259">Select hello location and then, click **OK**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="2d190-261">Dodaj rozszerzenie pliku hello w hello **typ pliku** pola.</span><span class="sxs-lookup"><span data-stu-id="2d190-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="2d190-263">Dodawanie rozszerzenia MP3</span><span class="sxs-lookup"><span data-stu-id="2d190-263">Adding an .mp3 extension</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="2d190-265">tooadd inne rozszerzenie, kliknij przycisk **Dodawanie wykluczenia** i wprowadź inne rozszerzenie typu pliku (Dodawanie rozszerzenia .jpeg).</span><span class="sxs-lookup"><span data-stu-id="2d190-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="2d190-267">Po dodaniu wszystkich rozszerzeń powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d190-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="2d190-268">Kontynuuj hello Kreatora harmonogramu kopii zapasowej, klikając **dalej** do hello **stronę potwierdzenia**, następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2d190-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="2d190-270">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="2d190-270">Frequently asked questions</span></span>
<span data-ttu-id="2d190-271">**1. Stan zadania tworzenia kopii zapasowej Hello jest wyświetlana jako zakończone hello Azure agenta kopii zapasowej, dlaczego nie go pobrać natychmiast odzwierciedlone w portalu?**</span><span class="sxs-lookup"><span data-stu-id="2d190-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="2d190-272">Odpowiedź 1.</span><span class="sxs-lookup"><span data-stu-id="2d190-272">A1.</span></span> <span data-ttu-id="2d190-273">Jest w Maksymalne opóźnienie 15 minutach między hello stan zadania tworzenia kopii zapasowej zostaną uwzględnione w hello agenta kopii zapasowej systemu Azure i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2d190-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="2d190-274">**Q.2, gdy zadanie tworzenia kopii zapasowej nie powiedzie się, jak długo trwa tooraise alert?**</span><span class="sxs-lookup"><span data-stu-id="2d190-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="2d190-275">A.2 alert jest uruchamiany w ciągu 20 minutach hello Azure niepowodzenia wykonywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="2d190-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="2d190-276">**K3. Jest przypadek, w którym nie będzie wysyłana wiadomość e-mail, jeśli skonfigurowano powiadomienia?**</span><span class="sxs-lookup"><span data-stu-id="2d190-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="2d190-277">Odpowiedź 3.</span><span class="sxs-lookup"><span data-stu-id="2d190-277">A3.</span></span> <span data-ttu-id="2d190-278">Poniżej przedstawiono hello przypadków podczas hello powiadomienia nie będą wysyłane w kolejności tooreduce hello alertu szumu:</span><span class="sxs-lookup"><span data-stu-id="2d190-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="2d190-279">Jeśli powiadomienia są skonfigurowane co godzinę, a alert jest uruchamiany rozwiązane w ciągu godziny hello</span><span class="sxs-lookup"><span data-stu-id="2d190-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="2d190-280">Zadanie zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="2d190-280">Job is canceled.</span></span>
* <span data-ttu-id="2d190-281">Drugi zadanie tworzenia kopii zapasowej nie powiodło się, ponieważ oryginalne zadanie tworzenia kopii zapasowej jest w toku.</span><span class="sxs-lookup"><span data-stu-id="2d190-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="2d190-282">Rozwiązywanie problemów monitorowania</span><span class="sxs-lookup"><span data-stu-id="2d190-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="2d190-283">**Problem:** zadania i/lub alerty z hello Azure Backup agent nie są wyświetlane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2d190-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="2d190-284">**Kroki rozwiązywania problemów:** hello procesu ```OBRecoveryServicesManagementAgent```, wysyła hello zadania i alert toohello danych usługi Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="2d190-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="2d190-285">Czasami ten proces może zostać wstrzymana lub zamknięcie.</span><span class="sxs-lookup"><span data-stu-id="2d190-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="2d190-286">proces hello tooverify nie jest uruchomiony, otwórz **Menedżera zadań** i sprawdź, czy hello ```OBRecoveryServicesManagementAgent``` proces jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="2d190-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="2d190-287">Przy założeniu, że proces hello nie jest uruchomiony, otwórz **Panelu sterowania** i Przeglądaj hello Lista usług.</span><span class="sxs-lookup"><span data-stu-id="2d190-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="2d190-288">Uruchom lub uruchom ponownie **agenta usług odzyskiwania Microsoft Azure w zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="2d190-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="2d190-289">Aby uzyskać więcej informacji Przejdź dzienniki hello na:</span><span class="sxs-lookup"><span data-stu-id="2d190-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="2d190-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2d190-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="2d190-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d190-291">Next steps</span></span>
* [<span data-ttu-id="2d190-292">Przywracanie systemu Windows Server lub klienta systemu Windows z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d190-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="2d190-293">toolearn więcej informacji na temat usługi Kopia zapasowa Azure, zobacz [Omówienie programu Kopia zapasowa Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="2d190-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="2d190-294">Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="2d190-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
