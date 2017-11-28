---
title: "Użyj agenta usługi Kopia zapasowa Azure do utworzenia kopii zapasowej plików i folderów | Dokumentacja firmy Microsoft"
description: "Agent usługi Kopia zapasowa Microsoft Azure umożliwia tworzenie kopii zapasowej plików systemu Windows i folderów na platformie Azure. Tworzenie magazynu usług odzyskiwania, zainstalować agenta kopii zapasowej Definiowanie zasad tworzenia kopii zapasowej i uruchom tworzenie początkowej kopii zapasowej plików i folderów."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="6c58b-105">Tworzenie kopii zapasowych systemu Windows Server lub Client na platformie Azure przy użyciu modelu wdrażania używającego usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c58b-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c58b-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6c58b-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="6c58b-107">Portal klasyczny</span><span class="sxs-lookup"><span data-stu-id="6c58b-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="6c58b-108">W tym artykule opisano sposób wykonywania kopii zapasowej systemu Windows Server (lub klienta systemu Windows) plików i folderów na platformie Azure za pomocą usługi Kopia zapasowa Azure przy użyciu modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Kroki procesu tworzenia kopii zapasowej](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="6c58b-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6c58b-110">Before you start</span></span>
<span data-ttu-id="6c58b-111">Aby utworzyć kopię zapasową serwera lub klienta na platformie Azure, potrzebne jest konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="6c58b-112">Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6c58b-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6c58b-113">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="6c58b-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="6c58b-114">Magazyn usług odzyskiwania jest jednostka, która przechowuje wszystkie kopie zapasowe i punkty odzyskiwania, tworzonych w czasie.</span><span class="sxs-lookup"><span data-stu-id="6c58b-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="6c58b-115">Magazyn usług odzyskiwania zawiera również zasady tworzenia kopii zapasowej stosowane do chronionych plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="6c58b-116">Podczas tworzenia magazynu usług odzyskiwania, należy również wybierz opcję nadmiarowość odpowiedniego magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="6c58b-117">Aby utworzyć magazyn usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="6c58b-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="6c58b-118">Jeśli nie zostało to wcześniej zrobione, zaloguj się witryny [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="6c58b-119">W menu Centrum kliknij pozycję **Więcej usług**, na liście zasobów wpisz łańcuch **Recovery Services**, a następnie kliknij pozycję **Magazyny usługi Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="6c58b-121">Jeśli w ramach subskrypcji istnieją magazyny usług odzyskiwania, zostaną one wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="6c58b-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="6c58b-122">W menu **Magazyny usługi Recovery Services** kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="6c58b-124">Zostanie otwarty blok magazynu Usług odzyskiwania i pojawi się monit o podanie wartości w polach **Nazwa**, **Subskrypcja**, **Grupa zasobów** i **Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="6c58b-126">W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn.</span><span class="sxs-lookup"><span data-stu-id="6c58b-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="6c58b-127">Nazwa musi być unikalna w tej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="6c58b-128">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="6c58b-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="6c58b-129">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="6c58b-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="6c58b-130">W sekcji **Subskrypcja** użyj menu rozwijanego, aby wybrać subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="6c58b-131">Jeśli używasz tylko jednej subskrypcji, zostanie ona wyświetlona i możesz przejść do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6c58b-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="6c58b-132">Jeśli nie masz pewności, której subskrypcji użyć, wybierz domyślną (lub sugerowaną).</span><span class="sxs-lookup"><span data-stu-id="6c58b-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="6c58b-133">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="6c58b-134">W sekcji **Grupa zasobów**:</span><span class="sxs-lookup"><span data-stu-id="6c58b-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="6c58b-135">wybierz pozycję **Utwórz nową**, jeśli chcesz utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="6c58b-136">Lub</span><span class="sxs-lookup"><span data-stu-id="6c58b-136">Or</span></span>
    * <span data-ttu-id="6c58b-137">wybierz pozycję **Użyj istniejącej** i kliknij menu rozwijane, aby wyświetlić listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="6c58b-138">Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c58b-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="6c58b-139">Kliknij pozycję **Lokalizacja**, aby wybrać region geograficzny magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="6c58b-140">Ten wybór określa region geograficzny, do którego wysyłane są dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="6c58b-141">W dolnej części bloku magazynu usług Recovery Services kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="6c58b-142">Utworzenie magazynu usług Recovery Services może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6c58b-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="6c58b-143">Monitoruj powiadomienia o stanie wyświetlane w prawej górnej części obszaru portalu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="6c58b-144">Po utworzeniu magazynu pojawi się on na liście magazynów Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="6c58b-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="6c58b-145">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="6c58b-147">Po wyświetleniu magazynu na liście magazynów usług Recovery Services możesz rozpocząć ustawianie nadmiarowości przechowywania.</span><span class="sxs-lookup"><span data-stu-id="6c58b-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="6c58b-148">Nadmiarowość magazynu zestawu</span><span class="sxs-lookup"><span data-stu-id="6c58b-148">Set storage redundancy</span></span>
<span data-ttu-id="6c58b-149">Podczas tworzenia magazynu usługi Recovery Services określany jest sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="6c58b-150">W bloku **Magazyny usług Recovery Services** kliknij nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="6c58b-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Wybieranie nowego magazynu z listy magazynów usług Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="6c58b-152">Wybranie magazynu spowoduje zwężenie bloku **Magazyn usług Recovery Services** oraz otwarcie bloków Ustawienia (*o nazwie magazynu wskazanego w górnej części*) i szczegółów magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Wyświetlanie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="6c58b-154">W bloku ustawień nowego magazynu użyj pionowego suwaka, aby przewinąć w dół do sekcji Zarządzanie, a następnie kliknij pozycję **Infrastruktura zapasowa**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="6c58b-155">Zostanie otwarty blok Infrastruktura zapasowa.</span><span class="sxs-lookup"><span data-stu-id="6c58b-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="6c58b-156">W bloku Infrastruktura zapasowa kliknij pozycję **Konfiguracja kopii zapasowej** w celu otwarcia bloku **Konfiguracja kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Ustawianie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="6c58b-158">Wybierz odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="6c58b-160">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="6c58b-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="6c58b-161">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, kontynuuj korzystanie z magazynu **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="6c58b-162">Jeśli nie używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, wybierz pozycję **Lokalnie nadmiarowy**, co zmniejszy koszty magazynów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="6c58b-163">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="6c58b-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="6c58b-164">Teraz, po utworzeniu magazynu należy przygotować infrastrukturę do tworzenia kopii zapasowej plików i folderów pobieranie i instalowanie agenta usług odzyskiwania Microsoft Azure, pobierając poświadczenia magazynu i następnie użyciu tych poświadczeń można zarejestrować agenta z Magazyn.</span><span class="sxs-lookup"><span data-stu-id="6c58b-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="6c58b-165">Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="6c58b-165">Configure the vault</span></span>

1. <span data-ttu-id="6c58b-166">W bloku Magazyn usługi Recovery Services (dla właśnie utworzonego magazynu) w sekcji Wprowadzenie kliknij pozycję **Kopia zapasowa**, a następnie w bloku **Wprowadzenie do kopii zapasowej** wybierz pozycję **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="6c58b-168">Zostanie otwarty blok **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="6c58b-169">Jeśli wcześniej skonfigurowano Magazyn usług odzyskiwania, a następnie **cel kopii zapasowej** kliknięcie powoduje otwarcie bloków **kopii zapasowej** na usług odzyskiwania magazynu bloku.</span><span class="sxs-lookup"><span data-stu-id="6c58b-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="6c58b-171">Z menu **Gdzie działa Twoje obciążenie?** wybierz pozycję **Lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="6c58b-172">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="6c58b-173">Z menu **Dla jakich elementów chcesz utworzyć kopię zapasową?** wybierz pozycję **Pliki i foldery**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Konfigurowanie plików i folderów](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="6c58b-175">Po kliknięciu przycisku OK obok pozycji **Cel kopii zapasowej** pojawi się znacznik wyboru i zostanie otwarty blok **Przygotowywanie infrastruktury**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="6c58b-177">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="6c58b-179">Jeśli używasz systemu Windows Server Essential, wybierz opcję pobrania agenta dla systemu Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="6c58b-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="6c58b-180">Zostanie wyświetlone menu rozwijane z monitem o uruchomienie lub zapisanie pliku MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="6c58b-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="6c58b-182">W menu rozwijanym pobierania kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="6c58b-183">Domyślnie plik **MARSagentinstaller.exe** jest zapisywany w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="6c58b-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="6c58b-184">Po ukończeniu pobierania pojawi się okno podręczne z pytaniem, czy chcesz uruchomić Instalatora, czy otworzyć folder.</span><span class="sxs-lookup"><span data-stu-id="6c58b-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="6c58b-186">Nie musisz jeszcze instalować agenta.</span><span class="sxs-lookup"><span data-stu-id="6c58b-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="6c58b-187">Agenta możesz zainstalować po pobraniu poświadczeń magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c58b-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="6c58b-188">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="6c58b-190">Poświadczenia magazynu zostaną pobrane do folderu Pobrane.</span><span class="sxs-lookup"><span data-stu-id="6c58b-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="6c58b-191">Po zakończeniu pobierania poświadczeń magazynu zobaczysz okno podręczne z pytaniem, czy chcesz otworzyć poświadczenia, czy je zapisać.</span><span class="sxs-lookup"><span data-stu-id="6c58b-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="6c58b-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-192">Click **Save**.</span></span> <span data-ttu-id="6c58b-193">Jeśli przypadkowo klikniesz pozycję **Otwórz**, zaczekaj, aż działanie okna dialogowego, które spróbuje otworzyć poświadczenia magazynu, zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6c58b-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="6c58b-194">Poświadczeń magazynu nie da się otworzyć.</span><span class="sxs-lookup"><span data-stu-id="6c58b-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="6c58b-195">Przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6c58b-195">Proceed to the next step.</span></span> <span data-ttu-id="6c58b-196">Poświadczenia magazynu znajdują się w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="6c58b-196">The vault credentials are in the Downloads folder.</span></span>   

  ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="6c58b-198">Instalowanie i rejestrowanie agenta</span><span class="sxs-lookup"><span data-stu-id="6c58b-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="6c58b-199">Opcja włączania kopii zapasowych za pośrednictwem witryny Azure Portal jest jeszcze niedostępna.</span><span class="sxs-lookup"><span data-stu-id="6c58b-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="6c58b-200">Do tworzenia kopii zapasowej plików i folderów należy używać agenta usług Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6c58b-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="6c58b-201">Zlokalizuj i kliknij dwukrotnie plik **MARSagentinstaller.exe** w folderze Pobrane (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="6c58b-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="6c58b-202">Instalator wyświetli serię komunikatów w miarę wypakowywania, instalowania i rejestrowania agenta usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6c58b-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="6c58b-204">Wykonaj kroki kreatora instalacji agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6c58b-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="6c58b-205">Aby zakończyć pracę kreatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c58b-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="6c58b-206">Wybierz lokalizację folderu instalacji i folderu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="6c58b-207">Podaj informacje o serwerze proxy, jeśli korzystasz z niego do łączenia się z Internetem.</span><span class="sxs-lookup"><span data-stu-id="6c58b-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="6c58b-208">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c58b-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="6c58b-209">Udostępnianie pobranych poświadczeń magazynu</span><span class="sxs-lookup"><span data-stu-id="6c58b-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="6c58b-210">Zapisz hasło szyfrowania w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6c58b-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6c58b-211">Jeśli utracisz lub zapomnisz hasło, firma Microsoft nie będzie mogła pomóc w odzyskaniu danych kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="6c58b-212">Zapisz plik w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6c58b-212">Save the file in a secure location.</span></span> <span data-ttu-id="6c58b-213">Jest ono wymagane do przywrócenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="6c58b-214">Agent jest teraz zainstalowany, a maszyna zarejestrowana w magazynie.</span><span class="sxs-lookup"><span data-stu-id="6c58b-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="6c58b-215">Wszystko jest gotowe do skonfigurowania kopii zapasowej i zaplanowania jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="6c58b-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="6c58b-216">Wymagania dotyczące sieci i łączności</span><span class="sxs-lookup"><span data-stu-id="6c58b-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="6c58b-217">Machine/serwera proxy został ograniczony dostęp do Internetu, upewnij się, że ustawienia zapory na komputerze/serwera proxy są skonfigurowane i umożliwiają następujące adresy URL:</span><span class="sxs-lookup"><span data-stu-id="6c58b-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="6c58b-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6c58b-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="6c58b-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6c58b-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="6c58b-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="6c58b-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="6c58b-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6c58b-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="6c58b-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="6c58b-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="6c58b-223">Tworzenie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="6c58b-223">Create the backup policy</span></span>
<span data-ttu-id="6c58b-224">Zasady tworzenia kopii zapasowej jest określają harmonogram punktów odzyskiwania są pobierane i czas, punkty odzyskiwania są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="6c58b-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="6c58b-225">Użyj agenta kopii zapasowej Microsoft Azure, aby utworzyć zasady tworzenia kopii zapasowej plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="6c58b-226">Aby utworzyć harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="6c58b-226">To create a backup schedule</span></span>
1. <span data-ttu-id="6c58b-227">Otwórz agenta usługi Kopia zapasowa Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="6c58b-228">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usługi Kopia zapasowa Azure](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="6c58b-230">W agencie kopii zapasowej **akcje** okienku, kliknij przycisk **harmonogram tworzenia kopii zapasowych** można uruchomić Kreatora harmonogramu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="6c58b-232">Na **wprowadzenie** strony Kreatora harmonogramu kopii zapasowej, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="6c58b-233">Na **Wybieranie elementów do wykonania kopii zapasowej** kliknij przycisk **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="6c58b-234">Zostanie otwarte okno dialogowe Wybieranie elementów.</span><span class="sxs-lookup"><span data-stu-id="6c58b-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="6c58b-235">Wybierz pliki i foldery, które chcesz chronić, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="6c58b-236">W **Wybieranie elementów do wykonania kopii zapasowej** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="6c58b-237">Na **Określanie harmonogramu tworzenia kopii zapasowej** , określ harmonogram tworzenia kopii zapasowych i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="6c58b-238">Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.</span><span class="sxs-lookup"><span data-stu-id="6c58b-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="6c58b-240">Aby uzyskać więcej informacji o sposobie określania harmonogramu tworzenia kopii zapasowych, zobacz artykuł [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md) (Użycie usługi Azure Backup do zastąpienia infrastruktury taśm).</span><span class="sxs-lookup"><span data-stu-id="6c58b-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="6c58b-241">Na **Wybieranie zasady przechowywania** wybierz zasady przechowywania określonego dla kopii zapasowej i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="6c58b-242">Zasady przechowywania określają czas trwania, którego kopia zapasowa jest przechowywana.</span><span class="sxs-lookup"><span data-stu-id="6c58b-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="6c58b-243">Zamiast określać wspólne zasady dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania w zależności od momentu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="6c58b-244">Możliwe jest modyfikowanie, zgodnie z potrzebami, zasad przechowywania codziennych, cotygodniowych, comiesięcznych i corocznych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="6c58b-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="6c58b-245">Na stronie Wybieranie typu początkowej kopii zapasowej wybierz typ początkowej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6c58b-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="6c58b-246">Pozostaw zaznaczoną opcję **Automatycznie przez sieć**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="6c58b-247">Kopie zapasowe można tworzyć automatycznie za pośrednictwem sieci lub w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="6c58b-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="6c58b-248">W dalszej części tego artykułu opisano proces automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="6c58b-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="6c58b-249">Jeśli chcesz tworzyć kopie zapasowe w trybie offline, zapoznaj się z artykułem [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) (Przepływ pracy tworzenia kopii zapasowej w trybie offline w usłudze Azure Backup), aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6c58b-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="6c58b-250">Przejrzyj informacje na stronie Potwierdzenie, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="6c58b-251">Po ukończeniu harmonogramu tworzenia kopii zapasowej przez kreatora kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="6c58b-252">Włącz ograniczanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="6c58b-252">Enable network throttling</span></span>
<span data-ttu-id="6c58b-253">Agent usługi Kopia zapasowa Microsoft Azure udostępnia ograniczanie przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="6c58b-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="6c58b-254">Ograniczanie kontrolek z wykorzystaniem przepustowości sieci podczas transferu danych.</span><span class="sxs-lookup"><span data-stu-id="6c58b-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="6c58b-255">Ten formant może być przydatne, jeśli chcesz utworzyć kopię zapasową danych podczas godziny pracy, ale nie chcesz procesu tworzenia kopii zapasowej z innych ruch internetowy.</span><span class="sxs-lookup"><span data-stu-id="6c58b-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="6c58b-256">Ograniczenie ma zastosowanie do kopii zapasowej i przywracania działań.</span><span class="sxs-lookup"><span data-stu-id="6c58b-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6c58b-257">Ograniczanie przepustowości sieci nie jest dostępne w systemu Windows Server 2008 R2 z dodatkiem SP1, Windows Server 2008 z dodatkiem SP2 lub Windows 7 (dodatków service pack).</span><span class="sxs-lookup"><span data-stu-id="6c58b-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="6c58b-258">Funkcji ograniczania sieci kopia zapasowa Azure angażujący jakości usług (QoS) w lokalnym systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="6c58b-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="6c58b-259">Jeśli kopia zapasowa Azure może chronić tych systemów operacyjnych, wersji QoS dostępne na tych platformach nie działa z ograniczanie przepustowości sieci usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58b-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="6c58b-260">Ograniczanie przepustowości sieci można używać na wszystkich innych [obsługiwanych systemów operacyjnych](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="6c58b-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="6c58b-261">**Aby włączyć ograniczenie przepustowości sieci**</span><span class="sxs-lookup"><span data-stu-id="6c58b-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="6c58b-262">W agencie programu Kopia zapasowa Microsoft Azure, kliknij przycisk **Zmień właściwości**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Zmień właściwości](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="6c58b-264">Na **ograniczania** wybierz opcję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="6c58b-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Ograniczanie przepustowości sieci](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="6c58b-266">Po włączeniu ograniczenia przepustowości, należy określić dozwolony przepustowości dla transferu danych kopii zapasowej podczas **godzin pracy** i **godziny wolne**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="6c58b-267">Wartości przepustowości rozpocząć 512 kilobitów na sekundę (KB/s) i można przejść do 1,023 MB na sekundę (MB/s).</span><span class="sxs-lookup"><span data-stu-id="6c58b-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="6c58b-268">Można również wyznaczyć rozpoczęcia i zakończenia **godzin pracy**, i dni tygodnia są uważane dniach.</span><span class="sxs-lookup"><span data-stu-id="6c58b-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="6c58b-269">Godziny poza wyznaczonych są traktowane jako godzin pracy z systemem innym niż godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="6c58b-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="6c58b-270">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="6c58b-271">Aby utworzyć kopię zapasową plików i folderów po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="6c58b-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="6c58b-272">W agenta kopii zapasowej, kliknij przycisk **wykonaj kopię zapasową teraz** aby zakończyć początkowe umieszczanie za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="6c58b-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="6c58b-274">Na stronie Potwierdzenie przejrzyj ustawienia, które zostaną użyte przez Kreatora natychmiastowego tworzenia kopii zapasowej do utworzenia kopii zapasowej maszyny.</span><span class="sxs-lookup"><span data-stu-id="6c58b-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="6c58b-275">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="6c58b-276">Kliknij przycisk **Zamknij**, aby zamknąć kreatora.</span><span class="sxs-lookup"><span data-stu-id="6c58b-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="6c58b-277">Jeśli zrobisz to przed zakończeniem procesu tworzenia kopii zapasowej, kreator będzie nadal działał w tle.</span><span class="sxs-lookup"><span data-stu-id="6c58b-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="6c58b-278">Po zakończeniu tworzenia początkowej kopii zapasowej w konsoli usługi Backup zostanie wyświetlony stan **Ukończono zadanie**.</span><span class="sxs-lookup"><span data-stu-id="6c58b-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Początkowa replikacja została zakończona](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="6c58b-280">Pytania?</span><span class="sxs-lookup"><span data-stu-id="6c58b-280">Questions?</span></span>
<span data-ttu-id="6c58b-281">Jeśli masz pytania lub jeśli brakuje Ci jakiejś funkcji, [prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="6c58b-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c58b-282">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c58b-282">Next steps</span></span>
<span data-ttu-id="6c58b-283">Aby uzyskać dodatkowe informacje na temat tworzenia kopii zapasowych maszyn wirtualnych lub innych obciążeń zobacz:</span><span class="sxs-lookup"><span data-stu-id="6c58b-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="6c58b-284">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="6c58b-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="6c58b-285">Jeśli chcesz przywrócić kopię zapasową, w tym artykule znajdziesz informacje dotyczące [przywracania plików na maszynę z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="6c58b-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
