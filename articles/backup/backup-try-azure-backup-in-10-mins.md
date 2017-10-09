---
title: "aaaBack się Windows pliki i foldery tooAzure (Resource Manager) | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooback się tooAzure plików i folderów w ramach wdrożenia Menedżera zasobów systemu Windows."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "jak toobackup; jak tooback; kopii zapasowej plików i folderów"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="12fb6-104">Pierwsze spojrzenie: tworzenie kopii zapasowych plików i folderów w ramach wdrożenia usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="12fb6-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="12fb6-105">W tym artykule opisano sposób tooAzure pliki i foldery tooback systemu Windows Server (lub komputer z systemem Windows) przy użyciu wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12fb6-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="12fb6-106">Jest samouczek toowalk danego użytkownika przez proces hello podstawy.</span><span class="sxs-lookup"><span data-stu-id="12fb6-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="12fb6-107">Jeśli chcesz tooget została uruchomiona przy użyciu usługi Kopia zapasowa Azure, możesz w odpowiednim miejscu hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="12fb6-108">Więcej informacji na temat tworzenia kopii zapasowej Azure tooknow należy przeczytać ten tekst [omówienie](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="12fb6-109">Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/) umożliwiające dostęp do dowolnej usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="12fb6-110">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="12fb6-110">Create a recovery services vault</span></span>
<span data-ttu-id="12fb6-111">tooback zapasową plików i folderów, należy toocreate magazynu usług odzyskiwania w regionie hello miejscu toostore hello danych.</span><span class="sxs-lookup"><span data-stu-id="12fb6-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="12fb6-112">Należy również toodetermine sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="12fb6-113">toocreate magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="12fb6-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="12fb6-114">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="12fb6-115">W menu Centrum powitania kliknij **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania** i kliknij przycisk **Magazyny usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="12fb6-117">Jeśli występują Magazyny usług odzyskiwania w ramach subskrypcji hello, magazynów hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="12fb6-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="12fb6-118">Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="12fb6-120">Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="12fb6-122">Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="12fb6-123">Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="12fb6-124">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="12fb6-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="12fb6-125">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="12fb6-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="12fb6-126">W hello **subskrypcji** Użyj hello menu rozwijanego toochoose hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="12fb6-127">Jeśli używasz tylko jedną subskrypcję, wyświetlonym subskrypcji i toohello następny krok można pominąć.</span><span class="sxs-lookup"><span data-stu-id="12fb6-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="12fb6-128">Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="12fb6-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="12fb6-129">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="12fb6-130">W hello **grupy zasobów** sekcji:</span><span class="sxs-lookup"><span data-stu-id="12fb6-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="12fb6-131">Wybierz **Utwórz nowy** Jeśli chcesz toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="12fb6-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="12fb6-132">Lub</span><span class="sxs-lookup"><span data-stu-id="12fb6-132">Or</span></span>
    * <span data-ttu-id="12fb6-133">Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="12fb6-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="12fb6-134">Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="12fb6-135">Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="12fb6-136">Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="12fb6-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="12fb6-137">U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="12fb6-138">Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="12fb6-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="12fb6-139">Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="12fb6-140">Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="12fb6-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="12fb6-141">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="12fb6-143">Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.</span><span class="sxs-lookup"><span data-stu-id="12fb6-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="12fb6-144">Ustaw nadmiarowość magazynu dla magazynu hello</span><span class="sxs-lookup"><span data-stu-id="12fb6-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="12fb6-145">Podczas tworzenia magazynu usług odzyskiwania, upewnij się, że sposób skonfigurowanych hello jest nadmiarowość magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="12fb6-146">Z hello **Magazyny usług odzyskiwania** bloku, kliknij przycisk Nowy magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Wybierz nowy magazyn hello z listy hello magazynu usług odzyskiwania](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="12fb6-148">Po wybraniu magazynu hello hello **magazyn usług odzyskiwania i** narrows bloku oraz blok ustawień hello (*mającego nazwę hello magazynu hello u góry hello*) i hello magazynu szczegóły blok otwarte.</span><span class="sxs-lookup"><span data-stu-id="12fb6-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Widok konfiguracji magazynu hello nowy magazyn](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="12fb6-150">W bloku ustawienia hello nowy magazyn, użyj tooscroll pionowy slajdów hello dół toohello sekcji Zarządzaj, a następnie kliknij przycisk **infrastruktura kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="12fb6-151">zostanie otwarty blok infrastruktura kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="12fb6-152">W bloku infrastruktura kopii zapasowej powitania kliknij **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku.</span><span class="sxs-lookup"><span data-stu-id="12fb6-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Ustaw hello konfigurację magazynu dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="12fb6-154">Wybierz hello odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="12fb6-156">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="12fb6-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="12fb6-157">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych nadal toouse **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="12fb6-158">Jeśli nie używasz Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, należy wybrać **lokalnie nadmiarowego**, co zmniejsza koszty usługi Azure storage hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="12fb6-159">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="12fb6-160">Teraz, kiedy został utworzony magazyn, należy go skonfigurować do tworzenia kopii zapasowych plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="12fb6-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="12fb6-161">Konfigurowanie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="12fb6-161">Configure hello vault</span></span>
1. <span data-ttu-id="12fb6-162">Na hello bloku magazyn usług odzyskiwania (dla hello właśnie utworzony magazyn), w sekcji wprowadzenie hello, kliknij przycisk **kopii zapasowej**, następnie na powitania **wprowadzenie do korzystania z kopii zapasowej** bloku, wybierz  **Celem tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="12fb6-164">Witaj **cel kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="12fb6-164">hello **Backup Goal** blade opens.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="12fb6-166">Z hello **gdzie działa Twoje obciążenie?** menu rozwijanego wybierz **lokalnymi**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="12fb6-167">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="12fb6-168">Z hello **co chcesz toobackup?** menu, wybierz opcję **pliki i foldery**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Konfigurowanie plików i folderów](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="12fb6-170">Po kliknięciu przycisku OK znacznik wyboru pojawia się dalej zbyt**cel kopii zapasowej**i hello **przygotowanie infrastruktury** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="12fb6-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="12fb6-172">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="12fb6-174">Jeśli używasz systemu Windows Server podstawowych, a następnie wybierz pozycję toodownload hello agenta dla systemu Windows Server podstawowych.</span><span class="sxs-lookup"><span data-stu-id="12fb6-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="12fb6-175">Menu podręczne monit toorun lub zapisać MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="12fb6-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="12fb6-177">W menu podręcznym pobierania hello, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="12fb6-178">Domyślnie program hello **MARSagentinstaller.exe** plik jest zapisywany w folderze pobrane tooyour.</span><span class="sxs-lookup"><span data-stu-id="12fb6-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="12fb6-179">Po zakończeniu działania Instalatora hello, pojawi się okno podręczne, jeśli Instalator hello toorun lub Otwórz hello folder.</span><span class="sxs-lookup"><span data-stu-id="12fb6-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="12fb6-181">Nie należy jeszcze tooinstall hello agenta.</span><span class="sxs-lookup"><span data-stu-id="12fb6-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="12fb6-182">Można zainstalować agenta hello pobrane hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="12fb6-183">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="12fb6-185">poświadczenia magazynu Hello Pobierz tooyour folderze pobrane.</span><span class="sxs-lookup"><span data-stu-id="12fb6-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="12fb6-186">Po poświadczenia magazynu hello zakończyć pobieranie, zostanie wyświetlony okno podręczne, jeśli chcesz tooopen lub Zapisz hello poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="12fb6-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="12fb6-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-187">Click **Save**.</span></span> <span data-ttu-id="12fb6-188">Jeśli przypadkowo kliknij **Otwórz**, let okno dialogowe hello prób poświadczenia magazynu hello tooopen, zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="12fb6-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="12fb6-189">Nie można otworzyć hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="12fb6-190">Kontynuować toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="12fb6-190">Proceed toohello next step.</span></span> <span data-ttu-id="12fb6-191">poświadczenia magazynu Hello znajdują się w folderze pobrane hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="12fb6-193">Zainstaluj i zarejestruj hello agenta</span><span class="sxs-lookup"><span data-stu-id="12fb6-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="12fb6-194">Włączenie kopii zapasowej za pomocą portalu Azure hello nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="12fb6-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="12fb6-195">Użyj tooback agenta usług odzyskiwania Microsoft Azure hello zapasową plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="12fb6-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="12fb6-196">Zlokalizuj i kliknij dwukrotnie hello **MARSagentinstaller.exe** z hello pobieranie folderu (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="12fb6-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="12fb6-197">Instalator Hello zapewnia szereg wiadomości, ponieważ wyodrębnia on, instaluje i rejestruje hello agenta usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="12fb6-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="12fb6-199">Ukończyć powitalnych Kreatora instalacji agenta usług odzyskiwania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12fb6-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="12fb6-200">Kreator hello toocomplete, musisz:</span><span class="sxs-lookup"><span data-stu-id="12fb6-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="12fb6-201">Wybierz lokalizację dla folderu instalacji i pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="12fb6-202">Podaj informacje o serwerze proxy, jeśli używasz toohello tooconnect serwera proxy internet.</span><span class="sxs-lookup"><span data-stu-id="12fb6-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="12fb6-203">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="12fb6-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="12fb6-204">Podaj poświadczenia magazynu pobrane hello</span><span class="sxs-lookup"><span data-stu-id="12fb6-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="12fb6-205">Zapisz hasło szyfrowania hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="12fb6-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="12fb6-206">Jeśli użytkownik zapomni hasła hello, Microsoft nie może odzyskać hello dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="12fb6-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="12fb6-207">Zapisz plik hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="12fb6-207">Save hello file in a secure location.</span></span> <span data-ttu-id="12fb6-208">Jest wymagane toorestore kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="12fb6-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="12fb6-209">Hello agent jest teraz zainstalowany i komputera jest zarejestrowaną toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="12fb6-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="12fb6-210">Wszystko gotowe tooconfigure i Planowanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="12fb6-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="12fb6-211">Wymagania dotyczące sieci i łączności</span><span class="sxs-lookup"><span data-stu-id="12fb6-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="12fb6-212">Machine/serwera proxy został ograniczony dostęp do Internetu, upewnij się, że ustawienia zapory na powitania mcahine/serwera proxy są hello tooallow skonfigurowane następujące adresy URL:</span><span class="sxs-lookup"><span data-stu-id="12fb6-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="12fb6-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="12fb6-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="12fb6-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="12fb6-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="12fb6-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="12fb6-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="12fb6-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="12fb6-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="12fb6-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="12fb6-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="12fb6-218">Tworzenie kopii zapasowej plików i folderów</span><span class="sxs-lookup"><span data-stu-id="12fb6-218">Back up your files and folders</span></span>
<span data-ttu-id="12fb6-219">Witaj początkowa kopia zapasowa obejmuje dwa kluczowe zadania:</span><span class="sxs-lookup"><span data-stu-id="12fb6-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="12fb6-220">Witaj harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="12fb6-220">Schedule hello backup</span></span>
* <span data-ttu-id="12fb6-221">Tworzenie kopii zapasowej plików i folderów na powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="12fb6-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="12fb6-222">toocomplete hello początkowa kopia zapasowa, agent usług odzyskiwania Microsoft Azure hello użycia.</span><span class="sxs-lookup"><span data-stu-id="12fb6-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="12fb6-223">zadanie tworzenia kopii zapasowej hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="12fb6-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="12fb6-224">Otwórz agenta usług odzyskiwania Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="12fb6-225">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usług odzyskiwania Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="12fb6-227">W agencie usług odzyskiwania hello, kliknij przycisk **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="12fb6-229">Na powitania wprowadzenie strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="12fb6-230">Na stronie tooBackup wybierz elementy powitania kliknij **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="12fb6-231">Wybierz hello pliki i foldery, które mają tooback w górę, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="12fb6-232">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-232">Click **Next**.</span></span>
7. <span data-ttu-id="12fb6-233">Na powitania **Określanie harmonogramu tworzenia kopii zapasowej** Określ hello **harmonogram tworzenia kopii zapasowych** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="12fb6-234">Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.</span><span class="sxs-lookup"><span data-stu-id="12fb6-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="12fb6-236">Aby uzyskać więcej informacji o sposobie toospecify hello harmonogram tworzenia kopii zapasowych, zobacz artykuł hello [tooreplace kopia zapasowa Azure użycie infrastruktury taśmy](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="12fb6-237">Na powitania **Wybieranie zasady przechowywania** strona, wybierz hello **zasady przechowywania** dla hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="12fb6-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="12fb6-238">zasady przechowywania Hello Określa, jak długo są przechowywane dane kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="12fb6-239">Zamiast określania "wspólne zasady" dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="12fb6-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="12fb6-240">Można zmodyfikować toomeet zasady przechowywania codziennie, co tydzień, miesięcznych i rocznych hello potrzeb.</span><span class="sxs-lookup"><span data-stu-id="12fb6-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="12fb6-241">Na stronie Wybieranie typu początkowej kopii zapasowej hello wybierz typ początkowej kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="12fb6-242">Pozostaw opcję hello **automatycznie przez sieć hello** zaznaczone, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="12fb6-243">Można tworzyć kopie zapasowe automatycznie przez sieć hello, lub w trybie offline, można tworzyć kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="12fb6-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="12fb6-244">Witaj dalszej części tego artykułu opisano proces hello automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="12fb6-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="12fb6-245">Jeśli wolisz toodo kopię zapasową offline, przejrzyj artykuł hello [w trybie Offline kopii zapasowej przepływu pracy w usłudze Kopia zapasowa Azure](backup-azure-backup-import-export.md) Aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="12fb6-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="12fb6-246">Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="12fb6-247">Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="12fb6-248">tooback zapasowe plików i folderów na powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="12fb6-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="12fb6-249">W agencie usług odzyskiwania hello, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="12fb6-251">Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="12fb6-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="12fb6-252">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="12fb6-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="12fb6-253">Kliknij przycisk **Zamknij** tooclose hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="12fb6-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="12fb6-254">Jeśli zamkniesz Kreatora hello przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="12fb6-255">Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.</span><span class="sxs-lookup"><span data-stu-id="12fb6-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Początkowa replikacja została zakończona](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="12fb6-257">Pytania?</span><span class="sxs-lookup"><span data-stu-id="12fb6-257">Questions?</span></span>
<span data-ttu-id="12fb6-258">Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="12fb6-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12fb6-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="12fb6-259">Next steps</span></span>
* <span data-ttu-id="12fb6-260">Dowiedz się więcej o [tworzeniu kopii zapasowej maszyn z systemem Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="12fb6-261">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="12fb6-262">Toorestore kopii zapasowej, należy użyć w tym artykule zbyt[przywrócenia plików tooa systemu Windows maszyny](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="12fb6-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
