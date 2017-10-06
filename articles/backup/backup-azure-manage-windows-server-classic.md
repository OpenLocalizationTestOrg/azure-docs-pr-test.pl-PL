---
title: "magazynami kopii zapasowych Azure aaaManage i hello klasycznego modelu wdrażania przy użyciu serwerów Azure | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toolearn jak magazyny toomanage kopia zapasowa Azure i serwerów."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="54a5c-103">Zarządzanie magazynami kopia zapasowa Azure i serwerami przy użyciu hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="54a5c-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54a5c-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54a5c-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="54a5c-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="54a5c-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="54a5c-106">W tym artykule znajdziesz Przegląd zadań zarządzania kopiami zapasowymi hello dostępne za pośrednictwem hello klasycznego portalu Azure i hello agenta kopii zapasowej Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="54a5c-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a5c-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="54a5c-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="54a5c-108">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="54a5c-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54a5c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54a5c-110">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="54a5c-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="54a5c-111">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="54a5c-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="54a5c-112">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="54a5c-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="54a5c-113">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54a5c-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="54a5c-114">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="54a5c-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="54a5c-115">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="54a5c-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="54a5c-116">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="54a5c-117">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="54a5c-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="54a5c-118">Zadania portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="54a5c-118">Management portal tasks</span></span>
1. <span data-ttu-id="54a5c-119">Zaloguj się toohello [portalu zarządzania](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="54a5c-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="54a5c-120">Kliknij przycisk **usług odzyskiwania**, następnie kliknij nazwę magazynu kopii zapasowych strony Szybki Start hello tooview hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Usługi odzyskiwania](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="54a5c-122">Wybierając opcje hello u góry strony Szybki Start hello hello widać hello dostępnych zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="54a5c-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Zarządzanie karty](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="54a5c-124">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="54a5c-124">Dashboard</span></span>
<span data-ttu-id="54a5c-125">Wybierz **pulpitu nawigacyjnego** przegląd wykorzystania hello toosee powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="54a5c-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="54a5c-126">Witaj **przegląd wykorzystania** obejmuje:</span><span class="sxs-lookup"><span data-stu-id="54a5c-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="54a5c-127">toocloud zarejestrowany Hello liczby serwerów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="54a5c-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="54a5c-128">Witaj liczbę maszyn wirtualnych platformy Azure chroniona w chmurze</span><span class="sxs-lookup"><span data-stu-id="54a5c-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="54a5c-129">Całkowita ilość miejsca Hello zużyte na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54a5c-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="54a5c-130">Witaj stan ostatnich zadań</span><span class="sxs-lookup"><span data-stu-id="54a5c-130">hello status of recent jobs</span></span>

<span data-ttu-id="54a5c-131">U dołu hello hello pulpit nawigacyjny umożliwia wykonywanie hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="54a5c-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="54a5c-132">**Zarządzanie certyfikatami** — Jeśli certyfikat został użyty tooregister powitania serwera, a następnie użycie tego certyfikatu hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="54a5c-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="54a5c-133">Jeśli używane są poświadczenia magazynu, nie używaj **Zarządzaj certyfikatem**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="54a5c-134">**Usuń** — usuwa hello bieżącego magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="54a5c-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="54a5c-135">Jeśli magazyn kopii zapasowych jest już używana, można usunąć toofree miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="54a5c-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="54a5c-136">**Usuń** jest włączona tylko po wszystkie zarejestrowane serwery zostały usunięte z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Zadania tworzenia kopii zapasowej pulpitu nawigacyjnego](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="54a5c-138">Zarejestrowanych elementów</span><span class="sxs-lookup"><span data-stu-id="54a5c-138">Registered items</span></span>
<span data-ttu-id="54a5c-139">Wybierz **zarejestrowane elementy** nazwy hello tooview hello serwerów, które są zarejestrowane toothis magazynu.</span><span class="sxs-lookup"><span data-stu-id="54a5c-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Zarejestrowanych elementów](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="54a5c-141">Witaj **typu** filtru domyślne tooAzure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54a5c-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="54a5c-142">nazwy hello tooview hello serwerów, które są zarejestrowane toothis magazynu, wybierz **systemu Windows server** z hello menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="54a5c-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="54a5c-143">W tym miejscu można wykonywać następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="54a5c-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="54a5c-144">**Zezwalaj na ponowną rejestrację** — po wybraniu tej opcji można użyć serwera hello **Kreatora rejestracji** hello lokalnymi kopia zapasowa Microsoft Azure agenta tooregister hello Server z magazynem kopii zapasowych powitania po raz drugi .</span><span class="sxs-lookup"><span data-stu-id="54a5c-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="54a5c-145">Może być konieczne toore rejestru ze względu na błąd tooan hello certyfikatu lub jeśli serwer ma toobe odbudowane.</span><span class="sxs-lookup"><span data-stu-id="54a5c-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="54a5c-146">**Usuń** — usuwa serwer z magazynu kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="54a5c-147">Wszystkie hello przechowywane dane skojarzone z serwerem hello zostaną natychmiast usunięte.</span><span class="sxs-lookup"><span data-stu-id="54a5c-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Zarejestrowanych elementów zadań](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="54a5c-149">Elementy chronione</span><span class="sxs-lookup"><span data-stu-id="54a5c-149">Protected items</span></span>
<span data-ttu-id="54a5c-150">Wybierz **chronione elementy** tooview hello elementy, które kopii zapasowej z hello serwerów.</span><span class="sxs-lookup"><span data-stu-id="54a5c-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Elementy chronione](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="54a5c-152">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="54a5c-152">Configure</span></span>
<span data-ttu-id="54a5c-153">Z hello **Konfiguruj** karcie można wybrać opcję nadmiarowość magazynu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="54a5c-154">Hello najlepszym czasu tooselect hello magazynu nadmiarowość rozwiązaniem jest bezpośrednio po utworzenie magazynu i przed tooit zarejestrowane są wszystkie maszyny.</span><span class="sxs-lookup"><span data-stu-id="54a5c-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="54a5c-155">Po powiązaniu elementu z magazynu zarejestrowanych toohello opcji nadmiarowość magazynu hello jest zablokowany i nie może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="54a5c-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Konfigurowanie](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="54a5c-157">Zobacz ten artykuł, aby uzyskać więcej informacji [nadmiarowość magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="54a5c-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="54a5c-158">Zadania agenta usługi Kopia zapasowa Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="54a5c-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="54a5c-159">Konsola</span><span class="sxs-lookup"><span data-stu-id="54a5c-159">Console</span></span>
<span data-ttu-id="54a5c-160">Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="54a5c-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agent usługi Kopia zapasowa](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="54a5c-162">Z hello **akcje** dostępne pod adresem hello rogu konsoli agenta kopii zapasowej hello można wykonywać na powitania następujące zadania związane z zarządzaniem:</span><span class="sxs-lookup"><span data-stu-id="54a5c-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="54a5c-163">Zarejestruj serwer</span><span class="sxs-lookup"><span data-stu-id="54a5c-163">Register Server</span></span>
* <span data-ttu-id="54a5c-164">Harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="54a5c-164">Schedule Backup</span></span>
* <span data-ttu-id="54a5c-165">Wykonaj kopię zapasową teraz</span><span class="sxs-lookup"><span data-stu-id="54a5c-165">Back Up now</span></span>
* <span data-ttu-id="54a5c-166">Zmień właściwości</span><span class="sxs-lookup"><span data-stu-id="54a5c-166">Change Properties</span></span>

![Akcje konsoli agentów.](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="54a5c-168">zbyt**odzyskać dane**, zobacz [przywrócić pliki tooa systemu Windows server lub komputer kliencki z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="54a5c-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="54a5c-169">Modyfikowanie istniejącej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="54a5c-169">Modify an existing backup</span></span>
1. <span data-ttu-id="54a5c-170">W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="54a5c-172">W hello **Kreatora harmonogramu kopii zapasowej** pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modyfikowanie zaplanowanego tworzenia kopii zapasowej](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="54a5c-174">Jeśli chcesz tooadd lub zmienić elementy na powitania **tooBackup wybierz elementy** ekranu kliknij **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="54a5c-175">Można również ustawić **ustawienia wykluczania** na tej stronie kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="54a5c-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="54a5c-176">Jeśli pliki tooexclude lub typów plików odczytu hello procedurę dodawania [ustawienia wykluczania](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="54a5c-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="54a5c-177">Wybierz hello pliki i foldery mają tooback w górę i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Dodaj elementy](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="54a5c-179">Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="54a5c-180">Można zaplanować codziennie (maksymalnie 3 razy dziennie) lub cotygodniowe kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="54a5c-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Określ harmonogram tworzenia kopii zapasowej](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="54a5c-182">Określanie harmonogramu tworzenia kopii zapasowych hello omówiono szczegółowo w tym [artykułu](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="54a5c-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="54a5c-183">Wybierz hello **zasady przechowywania** hello kopii zapasowej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Wybierz zasady przechowywania](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="54a5c-185">Na powitania **potwierdzenie** ekran Przegląd hello informacji i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="54a5c-186">Gdy Kreator hello zakończy tworzenie hello **harmonogram tworzenia kopii zapasowych**, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="54a5c-187">Po zmodyfikowaniu ochrony, można potwierdzić poprawnie wyzwalają kopii zapasowych przez przejście toohello **zadania** kartę i potwierdzenie, że zmiany zostaną odzwierciedlone w hello kopii zapasowej zadania.</span><span class="sxs-lookup"><span data-stu-id="54a5c-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="54a5c-188">Włącz ograniczanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="54a5c-188">Enable Network Throttling</span></span>
<span data-ttu-id="54a5c-189">agent usługi Kopia zapasowa Azure Hello zawiera kartę ograniczenia przepustowości, co pozwala toocontrol wykorzystaniem przepustowości sieci podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="54a5c-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="54a5c-190">Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy.</span><span class="sxs-lookup"><span data-stu-id="54a5c-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="54a5c-191">Ograniczanie danych transfer stosuje tooback zapasową i przywrócić działań.</span><span class="sxs-lookup"><span data-stu-id="54a5c-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="54a5c-192">Ograniczanie tooenable:</span><span class="sxs-lookup"><span data-stu-id="54a5c-192">tooenable throttling:</span></span>

1. <span data-ttu-id="54a5c-193">W hello **agent usługi Kopia zapasowa**, kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="54a5c-194">Wybierz hello **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** wyboru.</span><span class="sxs-lookup"><span data-stu-id="54a5c-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Ograniczanie przepustowości sieci](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="54a5c-196">Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="54a5c-197">wartości przepustowości Hello rozpoczynały 512 kilobajtach na sekundę (KB/s) i można przejść w górę too1023 MB na sekundę (MB/s).</span><span class="sxs-lookup"><span data-stu-id="54a5c-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="54a5c-198">Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są traktowane jako pracy dni.</span><span class="sxs-lookup"><span data-stu-id="54a5c-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="54a5c-199">czas Hello poza Witaj wyznaczone godzin pracy jest godzin wolnych toobe rozważenia.</span><span class="sxs-lookup"><span data-stu-id="54a5c-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="54a5c-200">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="54a5c-201">Ustawienia wykluczania</span><span class="sxs-lookup"><span data-stu-id="54a5c-201">Exclusion settings</span></span>
1. <span data-ttu-id="54a5c-202">Otwórz hello **agenta usługi Kopia zapasowa Microsoft Azure** (można go znaleźć, wyszukaj na maszynie łańcuch *kopia zapasowa Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="54a5c-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Otwórz agenta kopii zapasowej](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="54a5c-204">W agencie kopia zapasowa Microsoft Azure powitania kliknij **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planowanie kopii zapasowych serwera systemu Windows](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="54a5c-206">W hello Kreatora harmonogramu kopii zapasowej pozostaw hello **wprowadzanie zmian elementów toobackup lub razy** zaznaczono opcję i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modyfikowanie harmonogramu](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="54a5c-208">Kliknij przycisk **ustawienia wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-208">Click **Exclusions Settings**.</span></span>

    ![Wybierz elementy tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="54a5c-210">Kliknij przycisk **Dodaj wykluczenia**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-210">Click **Add Exclusion**.</span></span>

    ![Dodaj wykluczenia](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="54a5c-212">Wybierz lokalizację hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-212">Select hello location and then, click **OK**.</span></span>

    ![Wybierz lokalizację do wykluczenia](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="54a5c-214">Dodaj rozszerzenie pliku hello w hello **typ pliku** pola.</span><span class="sxs-lookup"><span data-stu-id="54a5c-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Wyklucz według typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="54a5c-216">Dodawanie rozszerzenia MP3</span><span class="sxs-lookup"><span data-stu-id="54a5c-216">Adding an .mp3 extension</span></span>

    ![Przykład typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="54a5c-218">tooadd inne rozszerzenie, kliknij przycisk **Dodawanie wykluczenia** i wprowadź inne rozszerzenie typu pliku (Dodawanie rozszerzenia .jpeg).</span><span class="sxs-lookup"><span data-stu-id="54a5c-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Innym przykładem typu pliku](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="54a5c-220">Po dodaniu wszystkich rozszerzeń powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="54a5c-221">Kontynuuj hello Kreatora harmonogramu kopii zapasowej, klikając **dalej** do hello **stronę potwierdzenia**, następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="54a5c-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Potwierdzenie wyłączenia](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="54a5c-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54a5c-223">Next steps</span></span>
* [<span data-ttu-id="54a5c-224">Przywracanie systemu Windows Server lub klienta systemu Windows z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54a5c-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="54a5c-225">toolearn więcej informacji na temat usługi Kopia zapasowa Azure, zobacz [Omówienie programu Kopia zapasowa Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="54a5c-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="54a5c-226">Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="54a5c-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
