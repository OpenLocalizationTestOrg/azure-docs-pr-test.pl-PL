---
title: "aaaBack się tooAzure stanu systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooback hello stanu systemu Windows Server i/lub tooAzure komputerów z systemem Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "jak toobackup; jak tooback; kopii zapasowej plików i folderów"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="8338c-104">Wykonaj kopię zapasową stanu systemu Windows podczas wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8338c-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="8338c-105">W tym artykule opisano, jak stan tooAzure: tooback systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8338c-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="8338c-106">Jest samouczek toowalk danego użytkownika przez proces hello podstawy.</span><span class="sxs-lookup"><span data-stu-id="8338c-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="8338c-107">Więcej informacji na temat tworzenia kopii zapasowej Azure tooknow należy przeczytać ten tekst [omówienie](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="8338c-108">Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/) umożliwiające dostęp do dowolnej usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8338c-109">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="8338c-109">Create a recovery services vault</span></span>
<span data-ttu-id="8338c-110">tooback zapasową plików i folderów, należy toocreate magazynu usług odzyskiwania w regionie hello miejscu toostore hello danych.</span><span class="sxs-lookup"><span data-stu-id="8338c-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="8338c-111">Należy również toodetermine sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="8338c-112">toocreate magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="8338c-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="8338c-113">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="8338c-114">W menu Centrum powitania kliknij **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania** i kliknij przycisk **Magazyny usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="8338c-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="8338c-116">Jeśli występują Magazyny usług odzyskiwania w ramach subskrypcji hello, magazynów hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="8338c-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="8338c-117">Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8338c-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="8338c-119">Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="8338c-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="8338c-121">Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="8338c-122">Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="8338c-123">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="8338c-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="8338c-124">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="8338c-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="8338c-125">W hello **subskrypcji** Użyj hello menu rozwijanego toochoose hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="8338c-126">Jeśli używasz tylko jedną subskrypcję, wyświetlonym subskrypcji i toohello następny krok można pominąć.</span><span class="sxs-lookup"><span data-stu-id="8338c-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="8338c-127">Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8338c-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="8338c-128">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="8338c-129">W hello **grupy zasobów** sekcji:</span><span class="sxs-lookup"><span data-stu-id="8338c-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="8338c-130">Wybierz **Utwórz nowy** Jeśli toocreate grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="8338c-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="8338c-131">Lub</span><span class="sxs-lookup"><span data-stu-id="8338c-131">Or</span></span>
    * <span data-ttu-id="8338c-132">Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="8338c-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="8338c-133">Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="8338c-134">Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="8338c-135">Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="8338c-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="8338c-136">U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8338c-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="8338c-137">Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="8338c-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="8338c-138">Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu.</span><span class="sxs-lookup"><span data-stu-id="8338c-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="8338c-139">Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="8338c-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="8338c-140">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="8338c-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="8338c-142">Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.</span><span class="sxs-lookup"><span data-stu-id="8338c-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="8338c-143">Ustaw nadmiarowość magazynu dla magazynu hello</span><span class="sxs-lookup"><span data-stu-id="8338c-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="8338c-144">Podczas tworzenia magazynu usług odzyskiwania, upewnij się, że sposób skonfigurowanych hello jest nadmiarowość magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="8338c-145">Z hello **Magazyny usług odzyskiwania** bloku, kliknij przycisk Nowy magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Wybierz nowy magazyn hello z listy hello magazynu usług odzyskiwania](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="8338c-147">Po wybraniu magazynu hello hello **magazyn usług odzyskiwania i** narrows bloku oraz blok ustawień hello (*mającego nazwę hello magazynu hello u góry hello*) i hello magazynu szczegóły blok otwarte.</span><span class="sxs-lookup"><span data-stu-id="8338c-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Widok konfiguracji magazynu hello nowy magazyn](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="8338c-149">W bloku ustawienia hello nowy magazyn, użyj tooscroll pionowy slajdów hello dół toohello sekcji Zarządzaj, a następnie kliknij przycisk **infrastruktura kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="8338c-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="8338c-150">zostanie otwarty blok infrastruktura kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="8338c-151">W bloku infrastruktura kopii zapasowej powitania kliknij **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku.</span><span class="sxs-lookup"><span data-stu-id="8338c-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Ustaw hello konfigurację magazynu dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="8338c-153">Wybierz hello odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="8338c-155">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="8338c-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="8338c-156">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych nadal toouse **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="8338c-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="8338c-157">Jeśli nie używasz Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, należy wybrać **lokalnie nadmiarowego**, co zmniejsza koszty usługi Azure storage hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="8338c-158">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="8338c-159">Teraz, po utworzeniu magazynu, należy go skonfigurować do tworzenia kopii zapasowej stanu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8338c-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="8338c-160">Konfigurowanie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="8338c-160">Configure hello vault</span></span>
1. <span data-ttu-id="8338c-161">Na hello bloku magazyn usług odzyskiwania (dla hello właśnie utworzony magazyn), w sekcji wprowadzenie hello, kliknij przycisk **kopii zapasowej**, następnie na powitania **wprowadzenie do korzystania z kopii zapasowej** bloku, wybierz  **Celem tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="8338c-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="8338c-163">Witaj **cel kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="8338c-163">hello **Backup Goal** blade opens.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="8338c-165">Z hello **gdzie działa Twoje obciążenie?** menu rozwijanego wybierz **lokalnymi**.</span><span class="sxs-lookup"><span data-stu-id="8338c-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="8338c-166">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="8338c-167">Z hello **co chcesz toobackup?** menu, wybierz opcję **stanu systemu**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8338c-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Konfigurowanie plików i folderów](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="8338c-169">Po kliknięciu przycisku OK znacznik wyboru pojawia się dalej zbyt**cel kopii zapasowej**i hello **przygotowanie infrastruktury** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="8338c-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="8338c-171">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="8338c-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="8338c-173">Jeśli używasz systemu Windows Server podstawowych, a następnie wybierz pozycję toodownload hello agenta dla systemu Windows Server podstawowych.</span><span class="sxs-lookup"><span data-stu-id="8338c-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="8338c-174">Menu podręczne monit toorun lub zapisać MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="8338c-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="8338c-176">W menu podręcznym pobierania hello, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8338c-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="8338c-177">Domyślnie program hello **MARSagentinstaller.exe** plik jest zapisywany w folderze pobrane tooyour.</span><span class="sxs-lookup"><span data-stu-id="8338c-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="8338c-178">Po zakończeniu działania Instalatora hello, pojawi się okno podręczne, jeśli Instalator hello toorun lub Otwórz hello folder.</span><span class="sxs-lookup"><span data-stu-id="8338c-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="8338c-180">Nie należy jeszcze tooinstall hello agenta.</span><span class="sxs-lookup"><span data-stu-id="8338c-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="8338c-181">Można zainstalować agenta hello pobrane hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="8338c-182">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="8338c-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="8338c-184">poświadczenia magazynu Hello Pobierz tooyour folderze pobrane.</span><span class="sxs-lookup"><span data-stu-id="8338c-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="8338c-185">Po poświadczenia magazynu hello zakończyć pobieranie, zostanie wyświetlony okno podręczne, jeśli chcesz tooopen lub Zapisz hello poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8338c-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="8338c-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8338c-186">Click **Save**.</span></span> <span data-ttu-id="8338c-187">Jeśli przypadkowo kliknij **Otwórz**, let okno dialogowe hello prób poświadczenia magazynu hello tooopen, zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8338c-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="8338c-188">Nie można otworzyć hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="8338c-189">Kontynuować toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="8338c-189">Proceed toohello next step.</span></span> <span data-ttu-id="8338c-190">poświadczenia magazynu Hello znajdują się w folderze pobrane hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="8338c-192">Zainstaluj i zarejestruj hello agenta</span><span class="sxs-lookup"><span data-stu-id="8338c-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="8338c-193">Włączenie kopii zapasowej za pomocą portalu Azure hello nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="8338c-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="8338c-194">Użyj tooback agenta usług odzyskiwania Microsoft Azure hello stanu systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8338c-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="8338c-195">Zlokalizuj i kliknij dwukrotnie hello **MARSagentinstaller.exe** z hello pobieranie folderu (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="8338c-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="8338c-196">Instalator Hello zapewnia szereg wiadomości, ponieważ wyodrębnia on, instaluje i rejestruje hello agenta usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="8338c-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="8338c-198">Ukończyć powitalnych Kreatora instalacji agenta usług odzyskiwania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8338c-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="8338c-199">Kreator hello toocomplete, musisz:</span><span class="sxs-lookup"><span data-stu-id="8338c-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="8338c-200">Wybierz lokalizację dla folderu instalacji i pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="8338c-201">Podaj informacje o serwerze proxy, jeśli używasz toohello tooconnect serwera proxy internet.</span><span class="sxs-lookup"><span data-stu-id="8338c-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="8338c-202">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="8338c-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="8338c-203">Podaj poświadczenia magazynu pobrane hello</span><span class="sxs-lookup"><span data-stu-id="8338c-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="8338c-204">Zapisz hasło szyfrowania hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8338c-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8338c-205">Jeśli użytkownik zapomni hasła hello, Microsoft nie może odzyskać hello dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="8338c-206">Zapisz plik hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8338c-206">Save hello file in a secure location.</span></span> <span data-ttu-id="8338c-207">Jest wymagane toorestore kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="8338c-208">Hello agent jest teraz zainstalowany i komputera jest zarejestrowaną toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="8338c-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="8338c-209">Wszystko gotowe tooconfigure i Planowanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="8338c-210">Wykonaj kopię zapasową stanu systemu Windows Server (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8338c-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="8338c-211">Witaj początkowa kopia zapasowa obejmuje trzy zadania:</span><span class="sxs-lookup"><span data-stu-id="8338c-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="8338c-212">Włącz kopii zapasowej stanu systemu przy użyciu hello agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="8338c-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="8338c-213">Witaj harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="8338c-213">Schedule hello backup</span></span>
* <span data-ttu-id="8338c-214">Tworzenie kopii zapasowej plików i folderów na powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="8338c-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="8338c-215">toocomplete hello początkowa kopia zapasowa, agent usług odzyskiwania Microsoft Azure hello użycia.</span><span class="sxs-lookup"><span data-stu-id="8338c-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="8338c-216">tooenable kopii zapasowej stanu systemu przy użyciu hello agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="8338c-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="8338c-217">W sesji programu PowerShell Uruchom hello następujące polecenia toostop hello kopia zapasowa Azure aparatu.</span><span class="sxs-lookup"><span data-stu-id="8338c-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="8338c-218">Otwórz hello rejestru systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8338c-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="8338c-219">Dodaj następującego klucza rejestru o hello hello określona wartość typu DWord.</span><span class="sxs-lookup"><span data-stu-id="8338c-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="8338c-220">Ścieżka rejestru</span><span class="sxs-lookup"><span data-stu-id="8338c-220">Registry path</span></span> | <span data-ttu-id="8338c-221">Klucz rejestru</span><span class="sxs-lookup"><span data-stu-id="8338c-221">Registry key</span></span> | <span data-ttu-id="8338c-222">Wartość DWord</span><span class="sxs-lookup"><span data-stu-id="8338c-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="8338c-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="8338c-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="8338c-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="8338c-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="8338c-225">2</span><span class="sxs-lookup"><span data-stu-id="8338c-225">2</span></span> |

4. <span data-ttu-id="8338c-226">Uruchom ponownie Aparat kopii zapasowej hello, wykonując następujące polecenie w wierszu polecenia z pełnymi uprawnieniami hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="8338c-227">zadanie tworzenia kopii zapasowej hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="8338c-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="8338c-228">Otwórz agenta usług odzyskiwania Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="8338c-229">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="8338c-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usług odzyskiwania Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="8338c-231">W agencie usług odzyskiwania hello, kliknij przycisk **harmonogram tworzenia kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="8338c-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="8338c-233">Na powitania wprowadzenie strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8338c-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="8338c-234">Na stronie tooBackup wybierz elementy powitania kliknij **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="8338c-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="8338c-235">Wybierz **stanu systemu** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8338c-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="8338c-236">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8338c-236">Click **Next**.</span></span>

7. <span data-ttu-id="8338c-237">Witaj harmonogramu kopii zapasowej stanu systemu i przechowywania zostanie automatycznie ustawione tooback się każdą niedzielę o 21:00:00 czasu lokalnego, i okresu przechowywania hello jest ustawiony too60 dni.</span><span class="sxs-lookup"><span data-stu-id="8338c-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8338c-238">Automatycznie skonfigurowano zasad przechowywania i kopii zapasowych stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="8338c-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="8338c-239">Po utworzeniu kopii zapasowej plików i folderów oprócz toohello systemu Windows Server System stanu, określ tylko hello kopii zapasowej i przechowywania zasady kopii zapasowych pliku z hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="8338c-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="8338c-240">Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="8338c-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="8338c-241">Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="8338c-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="8338c-242">tooback zapasowa stanu systemu Windows Server dla powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="8338c-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="8338c-243">Upewnij się, że nie ma żadnych oczekujących aktualizacji dla systemu Windows Server, które wymagają ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8338c-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="8338c-244">W agencie usług odzyskiwania hello, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="8338c-246">Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="8338c-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="8338c-247">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="8338c-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="8338c-248">Kliknij przycisk **Zamknij** tooclose hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="8338c-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="8338c-249">Jeśli zamkniesz Kreatora hello przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="8338c-250">Po utworzeniu kopii zapasowej plików i folderów na serwerze, także stan systemu serwera Windows toohello, kreator Utwórz kopię zapasową teraz hello tylko wykona kopię zapasową plików.</span><span class="sxs-lookup"><span data-stu-id="8338c-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="8338c-251">tooperform ad hoc stanu systemu wykonaj kopię zapasową, użyj następującego polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="8338c-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="8338c-252">Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![Początkowa replikacja została zakończona](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="8338c-254">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="8338c-254">Frequently asked questions</span></span>

<span data-ttu-id="8338c-255">Witaj następujące pytania i odpowiedzi zawierają dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8338c-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="8338c-256">Co to jest hello przemieszczania woluminu?</span><span class="sxs-lookup"><span data-stu-id="8338c-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="8338c-257">Witaj woluminu przemieszczania reprezentuje lokalizację pośrednich hello gdzie hello natywnie dostępna kopia zapasowa systemu Windows Server przygotuje hello kopii zapasowej stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="8338c-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="8338c-258">Agent usługi Kopia zapasowa Azure, a następnie kompresuje i szyfruje pośredniego kopia zapasowa i wysyła on za pośrednictwem bezpiecznego protokołu HTTPS toohello skonfigurowany magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="8338c-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="8338c-259">**Stanowczo zaleca się, że ustanowić hello woluminu tymczasowe na woluminie z systemem innym niż systemu Windows. Jeśli zauważysz problemy z kopii zapasowych stanu systemu Sprawdzanie lokalizacji hello woluminu przemieszczania jest hello pierwszy krok rozwiązywania problemów.**</span><span class="sxs-lookup"><span data-stu-id="8338c-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="8338c-260">Jak zmienić hello przemieszczania woluminu ścieżce określonej w hello agenta usługi Kopia zapasowa Azure?</span><span class="sxs-lookup"><span data-stu-id="8338c-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="8338c-261">Witaj woluminu przemieszczania znajduje się w folderu pamięci podręcznej hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="8338c-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="8338c-262">toochange tej lokalizacji hello Użyj następującego polecenia (w wierszu polecenia z podwyższonym poziomem uprawnień):</span><span class="sxs-lookup"><span data-stu-id="8338c-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="8338c-263">Następnie zaktualizuj hello następujące wpisy rejestru z hello ścieżki toohello nowego woluminu przemieszczania folderu.</span><span class="sxs-lookup"><span data-stu-id="8338c-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="8338c-264">Ścieżka rejestru</span><span class="sxs-lookup"><span data-stu-id="8338c-264">Registry path</span></span>|<span data-ttu-id="8338c-265">Klucz rejestru</span><span class="sxs-lookup"><span data-stu-id="8338c-265">Registry key</span></span>|<span data-ttu-id="8338c-266">Wartość</span><span class="sxs-lookup"><span data-stu-id="8338c-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="8338c-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="8338c-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="8338c-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="8338c-268">SSBStagingPath</span></span> | <span data-ttu-id="8338c-269">Nowa lokalizacja woluminu przemieszczania</span><span class="sxs-lookup"><span data-stu-id="8338c-269">new staging volume location</span></span> |

<span data-ttu-id="8338c-270">Hello ścieżki tymczasowej jest rozróżniana wielkość liter i muszą być dokładnie odpowiadać tej samej hello jej co istnieje na serwerze hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="8338c-271">Po zmianie ścieżki woluminu przemieszczania hello ponownego uruchomienia aparatu kopii zapasowej hello:</span><span class="sxs-lookup"><span data-stu-id="8338c-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="8338c-272">toopick hello zmieniona ścieżka, hello Otwórz agenta usług odzyskiwania Microsoft Azure i wyzwalacza ad hoc kopii zapasowej stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="8338c-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="8338c-273">Dlaczego jest stan systemu hello przechowywania domyślne ustawić dni too60?</span><span class="sxs-lookup"><span data-stu-id="8338c-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="8338c-274">Witaj użytkowania kopii zapasowej stanu systemu jest hello taki sam jak ustawienie hello "okresu istnienia reliktu" hello roli usługi Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8338c-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="8338c-275">Wartość domyślna Hello wpis okresu istnienia reliktu hello wynosi 60 dni.</span><span class="sxs-lookup"><span data-stu-id="8338c-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="8338c-276">Tę wartość można ustawić dla obiektu konfiguracji usługi Directory (NTDS) hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="8338c-277">Jak zmienić domyślne hello kopii zapasowej i zasad przechowywania dla stanu systemu?</span><span class="sxs-lookup"><span data-stu-id="8338c-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="8338c-278">domyślne hello toochange kopii zapasowej i zasad przechowywania dla stanu systemu:</span><span class="sxs-lookup"><span data-stu-id="8338c-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="8338c-279">Zatrzymaj hello Aparat kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-279">Stop hello Backup engine.</span></span> <span data-ttu-id="8338c-280">Uruchom następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień, hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="8338c-281">Dodaj lub zaktualizuj hello następujące wpisy klucza rejestru HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="8338c-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="8338c-282">Nazwa rejestru</span><span class="sxs-lookup"><span data-stu-id="8338c-282">Registry Name</span></span>|<span data-ttu-id="8338c-283">Opis</span><span class="sxs-lookup"><span data-stu-id="8338c-283">Description</span></span>|<span data-ttu-id="8338c-284">Wartość</span><span class="sxs-lookup"><span data-stu-id="8338c-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="8338c-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="8338c-285">SSBScheduleTime</span></span>|<span data-ttu-id="8338c-286">Używane tooconfigure hello hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="8338c-287">Domyślna to 21: 00 czasu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="8338c-287">Default is 9PM local time.</span></span>|<span data-ttu-id="8338c-288">DWord: Format hh: mm (dziesiętna) na przykład 2130 dla 21:30:00 czasu lokalnego</span><span class="sxs-lookup"><span data-stu-id="8338c-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="8338c-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="8338c-289">SSBScheduleDays</span></span>|<span data-ttu-id="8338c-290">Dni hello tooconfigure używane podczas tworzenia kopii zapasowej stanu systemu należy przeprowadzić na powitania określony czas.</span><span class="sxs-lookup"><span data-stu-id="8338c-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="8338c-291">Poszczególnych cyfr określ dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="8338c-292">0 oznacza niedzielę, 1 oznacza poniedziałek, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="8338c-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="8338c-293">Dzień domyślny dla kopii zapasowej oznacza niedzielę.</span><span class="sxs-lookup"><span data-stu-id="8338c-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="8338c-294">DWord: dni hello tygodnia toorun tworzenia kopii zapasowej (dziesiętna), na przykład 1230 harmonogramy tworzenia kopii zapasowych w poniedziałek, Wtorek, środę i niedzielę.</span><span class="sxs-lookup"><span data-stu-id="8338c-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="8338c-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="8338c-295">SSBRetentionDays</span></span>|<span data-ttu-id="8338c-296">Używane tooconfigure hello dni tooretain kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8338c-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="8338c-297">Wartość domyślna to 60.</span><span class="sxs-lookup"><span data-stu-id="8338c-297">Default value is 60.</span></span> <span data-ttu-id="8338c-298">Maksymalna dozwolona wartość to 180.</span><span class="sxs-lookup"><span data-stu-id="8338c-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="8338c-299">DWord: Dni tooretain kopii zapasowej (dziesiętne).</span><span class="sxs-lookup"><span data-stu-id="8338c-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="8338c-300">Hello Użyj następującego polecenia toorestart hello kopii zapasowej aparatu.</span><span class="sxs-lookup"><span data-stu-id="8338c-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="8338c-301">Otwórz agenta usług odzyskiwania Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="8338c-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="8338c-302">Kliknij przycisk **harmonogram tworzenia kopii zapasowych** , a następnie kliknij przycisk **dalej** do momentu wyświetlenia hello zmiany zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="8338c-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="8338c-303">Kliknij przycisk **Zakończ** tooapply hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="8338c-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="8338c-304">Pytania?</span><span class="sxs-lookup"><span data-stu-id="8338c-304">Questions?</span></span>
<span data-ttu-id="8338c-305">Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="8338c-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8338c-306">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8338c-306">Next steps</span></span>
* <span data-ttu-id="8338c-307">Dowiedz się więcej o [tworzeniu kopii zapasowej maszyn z systemem Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="8338c-308">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="8338c-309">Toorestore kopii zapasowej, należy użyć w tym artykule zbyt[przywrócenia plików tooa systemu Windows maszyny](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8338c-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
