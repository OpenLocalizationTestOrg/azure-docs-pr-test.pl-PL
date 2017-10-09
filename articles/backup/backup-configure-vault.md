---
title: "tooback agenta usługi Kopia zapasowa Azure aaaUse zapasowe plików i folderów | Dokumentacja firmy Microsoft"
description: "Użyj tooback agenta usługi Kopia zapasowa Microsoft Azure hello się tooAzure plików i folderów systemu Windows. Tworzenie magazynu usług odzyskiwania, zainstalować agenta kopii zapasowej hello Definiowanie zasad tworzenia kopii zapasowej hello i uruchomić hello początkowa kopia zapasowa na powitania pliki i foldery."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: Magazyn kopii zapasowych; Tworzenie kopii zapasowej systemu Windows server; Kopia zapasowa systemu windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="14821-105">Tworzenie kopii zapasowej systemu Windows Server lub klienta tooAzure, przy użyciu modelu wdrażania usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="14821-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14821-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14821-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="14821-107">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="14821-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="14821-108">W tym artykule opisano, jak pliki i foldery tooAzure tooback systemu Windows Server (lub klienta systemu Windows) z usługi Kopia zapasowa Azure przy użyciu hello modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14821-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Kroki procesu tworzenia kopii zapasowej](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="14821-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="14821-110">Before you start</span></span>
<span data-ttu-id="14821-111">tooback serwera lub klienta tooAzure, potrzebne jest konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="14821-112">Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="14821-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="14821-113">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="14821-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="14821-114">Magazyn usług odzyskiwania jest jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, tworzonych w czasie.</span><span class="sxs-lookup"><span data-stu-id="14821-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="14821-115">Magazyn usług odzyskiwania Hello zawiera także hello zasad tworzenia kopii zapasowych stosowane toohello chronione pliki i foldery.</span><span class="sxs-lookup"><span data-stu-id="14821-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="14821-116">Podczas tworzenia magazynu usług odzyskiwania należy również wybrać opcji nadmiarowość magazynu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="14821-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="14821-117">toocreate magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="14821-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="14821-118">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="14821-119">W menu Centrum powitania kliknij **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania** i kliknij przycisk **Magazyny usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="14821-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="14821-121">Jeśli występują Magazyny usług odzyskiwania w ramach subskrypcji hello, magazynów hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="14821-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="14821-122">Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="14821-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="14821-124">Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="14821-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="14821-126">Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="14821-127">Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="14821-128">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="14821-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="14821-129">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="14821-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="14821-130">W hello **subskrypcji** Użyj hello menu rozwijanego toochoose hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="14821-131">Jeśli używasz tylko jedną subskrypcję, wyświetlonym subskrypcji i toohello następny krok można pominąć.</span><span class="sxs-lookup"><span data-stu-id="14821-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="14821-132">Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="14821-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="14821-133">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="14821-134">W hello **grupy zasobów** sekcji:</span><span class="sxs-lookup"><span data-stu-id="14821-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="14821-135">Wybierz **Utwórz nowy** Jeśli chcesz toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="14821-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="14821-136">Lub</span><span class="sxs-lookup"><span data-stu-id="14821-136">Or</span></span>
    * <span data-ttu-id="14821-137">Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="14821-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="14821-138">Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14821-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="14821-139">Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="14821-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="14821-140">Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="14821-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="14821-141">U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="14821-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="14821-142">Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="14821-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="14821-143">Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu.</span><span class="sxs-lookup"><span data-stu-id="14821-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="14821-144">Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="14821-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="14821-145">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="14821-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="14821-147">Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.</span><span class="sxs-lookup"><span data-stu-id="14821-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="14821-148">Nadmiarowość magazynu zestawu</span><span class="sxs-lookup"><span data-stu-id="14821-148">Set storage redundancy</span></span>
<span data-ttu-id="14821-149">Podczas tworzenia magazynu usługi Recovery Services określany jest sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="14821-150">Z hello **Magazyny usług odzyskiwania** bloku, kliknij przycisk Nowy magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="14821-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Wybierz nowy magazyn hello z listy hello magazynu usług odzyskiwania](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="14821-152">Po wybraniu magazynu hello hello **magazyn usług odzyskiwania i** narrows bloku oraz blok ustawień hello (*mającego nazwę hello magazynu hello u góry hello*) i hello magazynu szczegóły blok otwarte.</span><span class="sxs-lookup"><span data-stu-id="14821-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Widok konfiguracji magazynu hello nowy magazyn](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="14821-154">W bloku ustawienia hello nowy magazyn, użyj tooscroll pionowy slajdów hello dół toohello sekcji Zarządzaj, a następnie kliknij przycisk **infrastruktura kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="14821-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="14821-155">zostanie otwarty blok infrastruktura kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="14821-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="14821-156">W bloku infrastruktura kopii zapasowej powitania kliknij **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku.</span><span class="sxs-lookup"><span data-stu-id="14821-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Ustaw hello konfigurację magazynu dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="14821-158">Wybierz hello odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="14821-160">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="14821-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="14821-161">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych nadal toouse **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="14821-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="14821-162">Jeśli nie używasz Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, należy wybrać **lokalnie nadmiarowego**, co zmniejsza koszty usługi Azure storage hello.</span><span class="sxs-lookup"><span data-stu-id="14821-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="14821-163">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="14821-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="14821-164">Teraz, po utworzeniu magazynu, pobieranie i instalowanie agenta usług odzyskiwania Microsoft Azure hello, pobierając poświadczenia magazynu i przy użyciu tych poświadczeń tooregister hello agenta z przygotowanie tooback Twojego infrastruktury zapasowe plików i folderów Magazyn Hello.</span><span class="sxs-lookup"><span data-stu-id="14821-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="14821-165">Konfigurowanie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="14821-165">Configure hello vault</span></span>

1. <span data-ttu-id="14821-166">Na hello bloku magazyn usług odzyskiwania (dla hello właśnie utworzony magazyn), w sekcji wprowadzenie hello, kliknij przycisk **kopii zapasowej**, następnie na powitania **wprowadzenie do korzystania z kopii zapasowej** bloku, wybierz  **Celem tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="14821-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="14821-168">Witaj **cel kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="14821-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="14821-169">Jeśli wcześniej skonfigurowano hello magazyn usług odzyskiwania i następnie hello **cel kopii zapasowej** kliknięcie powoduje otwarcie bloków **kopii zapasowej** na powitania usług odzyskiwania magazynu bloku.</span><span class="sxs-lookup"><span data-stu-id="14821-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="14821-171">Z hello **gdzie działa Twoje obciążenie?** menu rozwijanego wybierz **lokalnymi**.</span><span class="sxs-lookup"><span data-stu-id="14821-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="14821-172">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="14821-173">Z hello **co chcesz toobackup?** menu, wybierz opcję **pliki i foldery**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="14821-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Konfigurowanie plików i folderów](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="14821-175">Po kliknięciu przycisku OK znacznik wyboru pojawia się dalej zbyt**cel kopii zapasowej**i hello **przygotowanie infrastruktury** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="14821-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="14821-177">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="14821-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="14821-179">Jeśli używasz systemu Windows Server podstawowych, a następnie wybierz pozycję toodownload hello agenta dla systemu Windows Server podstawowych.</span><span class="sxs-lookup"><span data-stu-id="14821-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="14821-180">Menu podręczne monit toorun lub zapisać MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="14821-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="14821-182">W menu podręcznym pobierania hello, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="14821-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="14821-183">Domyślnie program hello **MARSagentinstaller.exe** plik jest zapisywany w folderze pobrane tooyour.</span><span class="sxs-lookup"><span data-stu-id="14821-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="14821-184">Po zakończeniu działania Instalatora hello, pojawi się okno podręczne, jeśli Instalator hello toorun lub Otwórz hello folder.</span><span class="sxs-lookup"><span data-stu-id="14821-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="14821-186">Nie należy jeszcze tooinstall hello agenta.</span><span class="sxs-lookup"><span data-stu-id="14821-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="14821-187">Można zainstalować agenta hello pobrane hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="14821-188">Na powitania **przygotowanie infrastruktury** bloku, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="14821-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="14821-190">poświadczenia magazynu Hello Pobierz tooyour folderze pobrane.</span><span class="sxs-lookup"><span data-stu-id="14821-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="14821-191">Po poświadczenia magazynu hello zakończyć pobieranie, zostanie wyświetlony okno podręczne, jeśli chcesz tooopen lub Zapisz hello poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="14821-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="14821-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="14821-192">Click **Save**.</span></span> <span data-ttu-id="14821-193">Jeśli przypadkowo kliknij **Otwórz**, let okno dialogowe hello prób poświadczenia magazynu hello tooopen, zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="14821-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="14821-194">Nie można otworzyć hello poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="14821-195">Kontynuować toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="14821-195">Proceed toohello next step.</span></span> <span data-ttu-id="14821-196">poświadczenia magazynu Hello znajdują się w folderze pobrane hello.</span><span class="sxs-lookup"><span data-stu-id="14821-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="14821-198">Zainstaluj i zarejestruj hello agenta</span><span class="sxs-lookup"><span data-stu-id="14821-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="14821-199">Włączenie kopii zapasowej za pomocą portalu Azure hello nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="14821-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="14821-200">Użyj tooback agenta usług odzyskiwania Microsoft Azure hello zapasową plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="14821-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="14821-201">Zlokalizuj i kliknij dwukrotnie hello **MARSagentinstaller.exe** z hello pobieranie folderu (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="14821-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="14821-202">Instalator Hello zapewnia szereg wiadomości, ponieważ wyodrębnia on, instaluje i rejestruje hello agenta usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="14821-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="14821-204">Ukończyć powitalnych Kreatora instalacji agenta usług odzyskiwania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="14821-205">Kreator hello toocomplete, musisz:</span><span class="sxs-lookup"><span data-stu-id="14821-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="14821-206">Wybierz lokalizację dla folderu instalacji i pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="14821-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="14821-207">Podaj informacje o serwerze proxy, jeśli używasz toohello tooconnect serwera proxy internet.</span><span class="sxs-lookup"><span data-stu-id="14821-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="14821-208">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="14821-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="14821-209">Podaj poświadczenia magazynu pobrane hello</span><span class="sxs-lookup"><span data-stu-id="14821-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="14821-210">Zapisz hasło szyfrowania hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="14821-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14821-211">Jeśli użytkownik zapomni hasła hello, Microsoft nie może odzyskać hello dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="14821-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="14821-212">Zapisz plik hello w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="14821-212">Save hello file in a secure location.</span></span> <span data-ttu-id="14821-213">Jest wymagane toorestore kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="14821-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="14821-214">Hello agent jest teraz zainstalowany i komputera jest zarejestrowaną toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="14821-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="14821-215">Wszystko gotowe tooconfigure i Planowanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="14821-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="14821-216">Wymagania dotyczące sieci i łączności</span><span class="sxs-lookup"><span data-stu-id="14821-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="14821-217">Machine/serwera proxy został ograniczony dostęp do Internetu, upewnij się, że ustawienia zapory na komputerze hello/serwera proxy są hello tooallow skonfigurowane następujące adresy URL:</span><span class="sxs-lookup"><span data-stu-id="14821-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="14821-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="14821-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="14821-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="14821-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="14821-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="14821-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="14821-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="14821-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="14821-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="14821-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="14821-223">Tworzenie zasad tworzenia kopii zapasowej hello</span><span class="sxs-lookup"><span data-stu-id="14821-223">Create hello backup policy</span></span>
<span data-ttu-id="14821-224">Hello zasad tworzenia kopii zapasowej jest harmonogram hello, gdy punkty odzyskiwania są pobierane i hello czas hello punkty odzyskiwania zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="14821-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="14821-225">Przy użyciu zasad tworzenia kopii zapasowej hello kopia zapasowa Microsoft Azure agenta toocreate hello pliki i foldery.</span><span class="sxs-lookup"><span data-stu-id="14821-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="14821-226">toocreate harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="14821-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="14821-227">Otwórz hello agenta usługi Kopia zapasowa Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="14821-228">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="14821-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usługi Kopia zapasowa Azure hello](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="14821-230">W agencie kopii zapasowej hello **akcje** okienku, kliknij przycisk **harmonogram tworzenia kopii zapasowych** hello toolaunch Kreatora harmonogramu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="14821-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="14821-232">Na powitania **wprowadzenie** strony hello Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="14821-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="14821-233">Na powitania **tooBackup wybierz elementy** kliknij przycisk **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="14821-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="14821-234">zostanie otwarte okno dialogowe Wybieranie elementów Hello.</span><span class="sxs-lookup"><span data-stu-id="14821-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="14821-235">Wybierz hello pliki i foldery mają tooprotect, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="14821-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="14821-236">W hello **tooBackup wybierz elementy** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="14821-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="14821-237">Na powitania **Określanie harmonogramu tworzenia kopii zapasowej** Określ harmonogram tworzenia kopii zapasowych hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="14821-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="14821-238">Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.</span><span class="sxs-lookup"><span data-stu-id="14821-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="14821-240">Aby uzyskać więcej informacji o sposobie toospecify hello harmonogram tworzenia kopii zapasowych, zobacz artykuł hello [tooreplace kopia zapasowa Azure użycie infrastruktury taśmy](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="14821-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="14821-241">Na powitania **Wybieranie zasady przechowywania** , wybierz hello zasad przechowywania określonych powitania dla kopii zapasowej hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="14821-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="14821-242">zasady przechowywania Hello określa hello okres czasu, który hello kopia zapasowa jest przechowywana.</span><span class="sxs-lookup"><span data-stu-id="14821-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="14821-243">Zamiast określać "wspólne zasady" dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="14821-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="14821-244">Można zmodyfikować toomeet zasady przechowywania codziennie, co tydzień, miesięcznych i rocznych hello potrzeb.</span><span class="sxs-lookup"><span data-stu-id="14821-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="14821-245">Na stronie Wybieranie typu początkowej kopii zapasowej hello wybierz typ początkowej kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="14821-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="14821-246">Pozostaw opcję hello **automatycznie przez sieć hello** zaznaczone, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="14821-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="14821-247">Można tworzyć kopie zapasowe automatycznie przez sieć hello, lub w trybie offline, można tworzyć kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="14821-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="14821-248">Witaj dalszej części tego artykułu opisano proces hello automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="14821-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="14821-249">Jeśli wolisz toodo kopię zapasową offline, przejrzyj artykuł hello [w trybie Offline kopii zapasowej przepływu pracy w usłudze Kopia zapasowa Azure](backup-azure-backup-import-export.md) Aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="14821-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="14821-250">Na stronie potwierdzenia hello, przejrzyj informacje hello, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="14821-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="14821-251">Po zakończeniu pracy Kreatora hello tworzenie hello harmonogram tworzenia kopii zapasowych, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="14821-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="14821-252">Włącz ograniczanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="14821-252">Enable network throttling</span></span>
<span data-ttu-id="14821-253">agent usługi Kopia zapasowa Microsoft Azure Hello zapewnia ograniczanie przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="14821-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="14821-254">Ograniczanie kontrolek z wykorzystaniem przepustowości sieci podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="14821-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="14821-255">Ten formant może być przydatne, gdy konieczne tooback zapasową danych poza godzinami pracy, ale nie chcesz hello toointerfere procesu tworzenia kopii zapasowej z innych ruch internetowy.</span><span class="sxs-lookup"><span data-stu-id="14821-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="14821-256">Ograniczanie stosuje tooback zapasowej i przywracanie działania.</span><span class="sxs-lookup"><span data-stu-id="14821-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="14821-257">Ograniczanie przepustowości sieci nie jest dostępne w systemu Windows Server 2008 R2 z dodatkiem SP1, Windows Server 2008 z dodatkiem SP2 lub Windows 7 (dodatków service pack).</span><span class="sxs-lookup"><span data-stu-id="14821-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="14821-258">funkcji ograniczania sieci kopia zapasowa Azure Hello angażujący jakości usług (QoS) w systemie operacyjnym lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="14821-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="14821-259">Jeśli kopia zapasowa Azure może chronić tych systemów operacyjnych, wersji hello QoS dostępne na tych platformach nie działa z ograniczanie przepustowości sieci usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="14821-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="14821-260">Ograniczanie przepustowości sieci można używać na wszystkich innych [obsługiwanych systemów operacyjnych](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="14821-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="14821-261">**Ograniczanie przepustowości sieci tooenable**</span><span class="sxs-lookup"><span data-stu-id="14821-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="14821-262">W agencie kopia zapasowa Microsoft Azure hello, kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="14821-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Zmień właściwości](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="14821-264">Na powitania **ograniczania** kartę, zaznacz hello **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="14821-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Ograniczanie przepustowości sieci](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="14821-266">Po włączeniu ograniczenia przepustowości, określ hello dozwolone przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.</span><span class="sxs-lookup"><span data-stu-id="14821-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="14821-267">wartości przepustowości Hello rozpocząć 512 kilobitów na sekundę (KB/s) i można przejść w górę too1, 023 MB na sekundę (MB/s).</span><span class="sxs-lookup"><span data-stu-id="14821-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="14821-268">Można również wyznaczyć hello rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia hello są uważane dniach.</span><span class="sxs-lookup"><span data-stu-id="14821-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="14821-269">Godziny poza wyznaczonych są traktowane jako godzin pracy z systemem innym niż godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="14821-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="14821-270">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="14821-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="14821-271">tooback zapasowe plików i folderów na powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="14821-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="14821-272">W hello agenta kopii zapasowej, kliknij przycisk **wykonaj kopię zapasową teraz** hello toocomplete początkowe umieszczanie za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="14821-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="14821-274">Na stronie potwierdzenia hello Przejrzyj hello ustawień, które Witaj ponownie teraz Kreatora konfigurowania użyje tooback hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="14821-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="14821-275">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="14821-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="14821-276">Kliknij przycisk **Zamknij** tooclose hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="14821-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="14821-277">Jeśli zrobisz to przed zakończeniem procesu tworzenia kopii zapasowej hello, Kreator hello nadal toorun w tle hello.</span><span class="sxs-lookup"><span data-stu-id="14821-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="14821-278">Po zakończeniu tworzenia początkowej kopii zapasowej hello hello **zadanie zostało ukończone** stan zostanie wyświetlony w konsoli usługi Backup hello.</span><span class="sxs-lookup"><span data-stu-id="14821-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Początkowa replikacja została zakończona](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="14821-280">Pytania?</span><span class="sxs-lookup"><span data-stu-id="14821-280">Questions?</span></span>
<span data-ttu-id="14821-281">Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="14821-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="14821-282">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14821-282">Next steps</span></span>
<span data-ttu-id="14821-283">Aby uzyskać dodatkowe informacje na temat tworzenia kopii zapasowych maszyn wirtualnych lub innych obciążeń zobacz:</span><span class="sxs-lookup"><span data-stu-id="14821-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="14821-284">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="14821-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="14821-285">Toorestore kopii zapasowej, należy użyć w tym artykule zbyt[przywrócenia plików tooa systemu Windows maszyny](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="14821-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
