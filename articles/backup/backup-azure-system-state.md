---
title: "Utwórz kopię zapasową stanu systemu Windows Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się tworzyć kopie zapasowe stanu systemu Windows Server i/lub Windows komputerów Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "jak tworzyć kopie zapasowe; tworzenie kopii zapasowych; tworzenie kopii zapasowych plików i folderów"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="41f01-104">Wykonaj kopię zapasową stanu systemu Windows podczas wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41f01-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="41f01-105">W tym artykule opisano sposób wykonywania kopii zapasowej stanu systemu Windows Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="41f01-106">Ten samouczek zawiera podstawowe informacje.</span><span class="sxs-lookup"><span data-stu-id="41f01-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="41f01-107">Jeśli chcesz dowiedzieć się więcej o usłudze Azure Backup, przeczytaj to [omówienie](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="41f01-108">Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/) umożliwiające dostęp do dowolnej usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="41f01-109">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="41f01-109">Create a recovery services vault</span></span>
<span data-ttu-id="41f01-110">Aby utworzyć kopię zapasową plików i folderów, należy utworzyć magazyn usługi Recovery Services w regionie, w którym chcesz przechowywać dane.</span><span class="sxs-lookup"><span data-stu-id="41f01-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="41f01-111">Należy również określić sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="41f01-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="41f01-112">Aby utworzyć magazyn usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="41f01-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="41f01-113">Jeśli nie zostało to wcześniej zrobione, zaloguj się witryny [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="41f01-114">W menu Centrum kliknij pozycję **Więcej usług**, na liście zasobów wpisz łańcuch **Recovery Services**, a następnie kliknij pozycję **Magazyny usługi Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="41f01-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="41f01-116">Jeśli w ramach subskrypcji istnieją magazyny usług odzyskiwania, zostaną one wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="41f01-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="41f01-117">W menu **Magazyny usługi Recovery Services** kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="41f01-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="41f01-119">Zostanie otwarty blok magazynu Usług odzyskiwania i pojawi się monit o podanie wartości w polach **Nazwa**, **Subskrypcja**, **Grupa zasobów** i **Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="41f01-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="41f01-121">W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn.</span><span class="sxs-lookup"><span data-stu-id="41f01-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="41f01-122">Nazwa musi być unikalna w tej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="41f01-123">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="41f01-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="41f01-124">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="41f01-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="41f01-125">W sekcji **Subskrypcja** użyj menu rozwijanego, aby wybrać subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="41f01-126">Jeśli używasz tylko jednej subskrypcji, zostanie ona wyświetlona i możesz przejść do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="41f01-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="41f01-127">Jeśli nie masz pewności, której subskrypcji użyć, wybierz domyślną (lub sugerowaną).</span><span class="sxs-lookup"><span data-stu-id="41f01-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="41f01-128">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="41f01-129">W sekcji **Grupa zasobów**:</span><span class="sxs-lookup"><span data-stu-id="41f01-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="41f01-130">wybierz pozycję **Utwórz nową**, jeśli chcesz utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="41f01-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="41f01-131">Lub</span><span class="sxs-lookup"><span data-stu-id="41f01-131">Or</span></span>
    * <span data-ttu-id="41f01-132">wybierz pozycję **Użyj istniejącej** i kliknij menu rozwijane, aby wyświetlić listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="41f01-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="41f01-133">Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="41f01-134">Kliknij pozycję **Lokalizacja**, aby wybrać region geograficzny magazynu.</span><span class="sxs-lookup"><span data-stu-id="41f01-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="41f01-135">Ten wybór określa region geograficzny, do którego wysyłane są dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="41f01-136">W dolnej części bloku magazynu usług Recovery Services kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="41f01-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="41f01-137">Utworzenie magazynu usług Recovery Services może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="41f01-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="41f01-138">Monitoruj powiadomienia o stanie wyświetlane w prawej górnej części obszaru portalu.</span><span class="sxs-lookup"><span data-stu-id="41f01-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="41f01-139">Po utworzeniu magazynu pojawi się on na liście magazynów Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="41f01-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="41f01-140">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="41f01-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="41f01-142">Po wyświetleniu magazynu na liście magazynów usług Recovery Services możesz rozpocząć ustawianie nadmiarowości przechowywania.</span><span class="sxs-lookup"><span data-stu-id="41f01-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="41f01-143">Ustawianie nadmiarowości przechowywania dla magazynu</span><span class="sxs-lookup"><span data-stu-id="41f01-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="41f01-144">Po utworzeniu magazynu usług Recovery Services upewnij się, że nadmiarowość magazynu została skonfigurowana w preferowany sposób.</span><span class="sxs-lookup"><span data-stu-id="41f01-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="41f01-145">W bloku **Magazyny usług Recovery Services** kliknij nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="41f01-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Wybieranie nowego magazynu z listy magazynów usług Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="41f01-147">Wybranie magazynu spowoduje zwężenie bloku **Magazyn usług Recovery Services** oraz otwarcie bloków Ustawienia (*o nazwie magazynu wskazanego w górnej części*) i szczegółów magazynu.</span><span class="sxs-lookup"><span data-stu-id="41f01-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Wyświetlanie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="41f01-149">W bloku ustawień nowego magazynu użyj pionowego suwaka, aby przewinąć w dół do sekcji Zarządzanie, a następnie kliknij pozycję **Infrastruktura zapasowa**.</span><span class="sxs-lookup"><span data-stu-id="41f01-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="41f01-150">Zostanie otwarty blok Infrastruktura zapasowa.</span><span class="sxs-lookup"><span data-stu-id="41f01-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="41f01-151">W bloku Infrastruktura zapasowa kliknij pozycję **Konfiguracja kopii zapasowej** w celu otwarcia bloku **Konfiguracja kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Ustawianie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="41f01-153">Wybierz odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="41f01-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="41f01-155">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="41f01-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="41f01-156">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, kontynuuj korzystanie z magazynu **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="41f01-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="41f01-157">Jeśli nie używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, wybierz pozycję **Lokalnie nadmiarowy**, co zmniejszy koszty magazynów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="41f01-158">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="41f01-159">Teraz, po utworzeniu magazynu, należy go skonfigurować do tworzenia kopii zapasowej stanu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="41f01-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="41f01-160">Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="41f01-160">Configure the vault</span></span>
1. <span data-ttu-id="41f01-161">W bloku Magazyn usługi Recovery Services (dla właśnie utworzonego magazynu) w sekcji Wprowadzenie kliknij pozycję **Kopia zapasowa**, a następnie w bloku **Wprowadzenie do kopii zapasowej** wybierz pozycję **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="41f01-163">Zostanie otwarty blok **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-163">The **Backup Goal** blade opens.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="41f01-165">Z menu **Gdzie działa Twoje obciążenie?** wybierz pozycję **Lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="41f01-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="41f01-166">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="41f01-167">Z **co chcesz utworzyć kopię zapasową?** menu, wybierz opcję **stanu systemu**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f01-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Konfigurowanie plików i folderów](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="41f01-169">Po kliknięciu przycisku OK obok pozycji **Cel kopii zapasowej** pojawi się znacznik wyboru i zostanie otwarty blok **Przygotowywanie infrastruktury**.</span><span class="sxs-lookup"><span data-stu-id="41f01-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="41f01-171">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="41f01-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="41f01-173">Jeśli używasz systemu Windows Server Essential, wybierz opcję pobrania agenta dla systemu Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="41f01-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="41f01-174">Zostanie wyświetlone menu rozwijane z monitem o uruchomienie lub zapisanie pliku MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="41f01-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="41f01-176">W menu rozwijanym pobierania kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="41f01-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="41f01-177">Domyślnie plik **MARSagentinstaller.exe** jest zapisywany w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="41f01-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="41f01-178">Po ukończeniu pobierania pojawi się okno podręczne z pytaniem, czy chcesz uruchomić Instalatora, czy otworzyć folder.</span><span class="sxs-lookup"><span data-stu-id="41f01-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="41f01-180">Nie musisz jeszcze instalować agenta.</span><span class="sxs-lookup"><span data-stu-id="41f01-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="41f01-181">Agenta możesz zainstalować po pobraniu poświadczeń magazynu.</span><span class="sxs-lookup"><span data-stu-id="41f01-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="41f01-182">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="41f01-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="41f01-184">Poświadczenia magazynu zostaną pobrane do folderu Pobrane.</span><span class="sxs-lookup"><span data-stu-id="41f01-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="41f01-185">Po zakończeniu pobierania poświadczeń magazynu zobaczysz okno podręczne z pytaniem, czy chcesz otworzyć poświadczenia, czy je zapisać.</span><span class="sxs-lookup"><span data-stu-id="41f01-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="41f01-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="41f01-186">Click **Save**.</span></span> <span data-ttu-id="41f01-187">Jeśli przypadkowo klikniesz pozycję **Otwórz**, zaczekaj, aż działanie okna dialogowego, które spróbuje otworzyć poświadczenia magazynu, zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="41f01-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="41f01-188">Poświadczeń magazynu nie da się otworzyć.</span><span class="sxs-lookup"><span data-stu-id="41f01-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="41f01-189">Przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="41f01-189">Proceed to the next step.</span></span> <span data-ttu-id="41f01-190">Poświadczenia magazynu znajdują się w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="41f01-190">The vault credentials are in the Downloads folder.</span></span>   

    ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="41f01-192">Instalowanie i rejestrowanie agenta</span><span class="sxs-lookup"><span data-stu-id="41f01-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="41f01-193">Opcja włączania kopii zapasowych za pośrednictwem witryny Azure Portal jest jeszcze niedostępna.</span><span class="sxs-lookup"><span data-stu-id="41f01-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="41f01-194">Aby utworzyć kopię zapasową stanu systemu Windows Server, użyj agenta usług odzyskiwania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="41f01-195">Zlokalizuj i kliknij dwukrotnie plik **MARSagentinstaller.exe** w folderze Pobrane (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="41f01-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="41f01-196">Instalator wyświetli serię komunikatów w miarę wypakowywania, instalowania i rejestrowania agenta usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="41f01-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="41f01-198">Wykonaj kroki kreatora instalacji agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="41f01-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="41f01-199">Aby zakończyć pracę kreatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="41f01-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="41f01-200">Wybierz lokalizację folderu instalacji i folderu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="41f01-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="41f01-201">Podaj informacje o serwerze proxy, jeśli korzystasz z niego do łączenia się z Internetem.</span><span class="sxs-lookup"><span data-stu-id="41f01-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="41f01-202">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="41f01-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="41f01-203">Udostępnianie pobranych poświadczeń magazynu</span><span class="sxs-lookup"><span data-stu-id="41f01-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="41f01-204">Zapisz hasło szyfrowania w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="41f01-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="41f01-205">Jeśli utracisz lub zapomnisz hasło, firma Microsoft nie będzie mogła pomóc w odzyskaniu danych kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="41f01-206">Zapisz plik w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="41f01-206">Save the file in a secure location.</span></span> <span data-ttu-id="41f01-207">Jest ono wymagane do przywrócenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="41f01-208">Agent jest teraz zainstalowany, a maszyna zarejestrowana w magazynie.</span><span class="sxs-lookup"><span data-stu-id="41f01-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="41f01-209">Wszystko jest gotowe do skonfigurowania kopii zapasowej i zaplanowania jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="41f01-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="41f01-210">Wykonaj kopię zapasową stanu systemu Windows Server (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="41f01-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="41f01-211">Początkowa kopia zapasowa obejmuje trzy zadania:</span><span class="sxs-lookup"><span data-stu-id="41f01-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="41f01-212">Włącz kopii zapasowej stanu systemu przy użyciu agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="41f01-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="41f01-213">Planowanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="41f01-213">Schedule the backup</span></span>
* <span data-ttu-id="41f01-214">Tworzenie kopii zapasowej plików i folderów po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="41f01-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="41f01-215">Aby utworzyć początkową kopię zapasową, użyj agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="41f01-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="41f01-216">Aby włączyć za pomocą usługi Kopia zapasowa Azure agenta kopii zapasowej stanu systemu</span><span class="sxs-lookup"><span data-stu-id="41f01-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="41f01-217">W sesji programu PowerShell uruchom następujące polecenie, aby zatrzymać aparat kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="41f01-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="41f01-218">Otwórz rejestr systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="41f01-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="41f01-219">Dodaj następujący klucz rejestru z określoną wartością DWord.</span><span class="sxs-lookup"><span data-stu-id="41f01-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="41f01-220">Ścieżka rejestru</span><span class="sxs-lookup"><span data-stu-id="41f01-220">Registry path</span></span> | <span data-ttu-id="41f01-221">Klucz rejestru</span><span class="sxs-lookup"><span data-stu-id="41f01-221">Registry key</span></span> | <span data-ttu-id="41f01-222">Wartość DWord</span><span class="sxs-lookup"><span data-stu-id="41f01-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="41f01-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="41f01-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="41f01-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="41f01-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="41f01-225">2</span><span class="sxs-lookup"><span data-stu-id="41f01-225">2</span></span> |

4. <span data-ttu-id="41f01-226">Uruchom ponownie Aparat kopii zapasowej, wykonując następujące polecenie w wierszu polecenia z pełnymi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="41f01-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="41f01-227">Aby zaplanować zadanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="41f01-227">To schedule the backup job</span></span>

1. <span data-ttu-id="41f01-228">Otwórz agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="41f01-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="41f01-229">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="41f01-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usługi Azure Recovery Services](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="41f01-231">W agencie usługi Recovery Services kliknij pozycję **Zaplanuj wykonywanie kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="41f01-233">Na stronie Wprowadzenie Kreatora harmonogramu kopii zapasowej kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="41f01-234">Na stronie Wybieranie elementów do wykonania kopii zapasowej kliknij pozycję **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="41f01-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="41f01-235">Wybierz **stanu systemu** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f01-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="41f01-236">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="41f01-236">Click **Next**.</span></span>

7. <span data-ttu-id="41f01-237">Automatycznie ustawiono harmonogramu kopii zapasowej stanu systemu i przechowywania kopii zapasowej każdą niedzielę o 21:00:00 czasu lokalnego, a okres przechowywania wynosi 60 dni.</span><span class="sxs-lookup"><span data-stu-id="41f01-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41f01-238">Automatycznie skonfigurowano zasad przechowywania i kopii zapasowych stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="41f01-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="41f01-239">Po utworzeniu kopii zapasowej plików i folderów oprócz stanu systemu Windows Server, należy określić tylko zasady kopii zapasowych pliku z poziomu Kreatora tworzenia kopii zapasowej i przechowywania.</span><span class="sxs-lookup"><span data-stu-id="41f01-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="41f01-240">Przejrzyj informacje na stronie Potwierdzenie, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="41f01-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="41f01-241">Po ukończeniu harmonogramu tworzenia kopii zapasowej przez kreatora kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="41f01-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="41f01-242">Aby utworzyć kopię zapasową stanu systemu Windows Server po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="41f01-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="41f01-243">Upewnij się, że nie ma żadnych oczekujących aktualizacji dla systemu Windows Server, które wymagają ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="41f01-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="41f01-244">W agencie Usług odzyskiwania kliknij pozycję **Wykonaj kopię zapasową teraz**, aby zakończyć początkowe umieszczanie za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="41f01-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="41f01-246">Na stronie Potwierdzenie przejrzyj ustawienia, które zostaną użyte przez Kreatora natychmiastowego tworzenia kopii zapasowej do utworzenia kopii zapasowej maszyny.</span><span class="sxs-lookup"><span data-stu-id="41f01-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="41f01-247">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="41f01-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="41f01-248">Kliknij przycisk **Zamknij**, aby zamknąć kreatora.</span><span class="sxs-lookup"><span data-stu-id="41f01-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="41f01-249">Jeśli zamkniesz kreatora przed zakończeniem procesu tworzenia kopii zapasowej, kreator będzie nadal działać w tle.</span><span class="sxs-lookup"><span data-stu-id="41f01-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="41f01-250">Po utworzeniu kopii zapasowej plików i folderów na serwerze, oprócz stanu systemu Windows Server, kreator Utwórz kopię zapasową teraz tylko wykona kopię zapasową plików.</span><span class="sxs-lookup"><span data-stu-id="41f01-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="41f01-251">Aby wykonać ad hoc stanu systemu wykonaj kopię zapasową, użyj następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41f01-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="41f01-252">Po zakończeniu tworzenia początkowej kopii zapasowej w konsoli usługi Backup zostanie wyświetlony stan **Ukończono zadanie**.</span><span class="sxs-lookup"><span data-stu-id="41f01-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![Początkowa replikacja została zakończona](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="41f01-254">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="41f01-254">Frequently asked questions</span></span>

<span data-ttu-id="41f01-255">Następujące pytania i odpowiedzi zawierają dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="41f01-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="41f01-256">Co to jest woluminem przemieszczania?</span><span class="sxs-lookup"><span data-stu-id="41f01-256">What is the Staging Volume?</span></span>

<span data-ttu-id="41f01-257">Wielkość przemieszczania stanowi pośredni lokalizacji, gdzie dostępna natywnie, kopia zapasowa systemu Windows Server przygotuje kopii zapasowej stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="41f01-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="41f01-258">Agent usługi Kopia zapasowa Azure, a następnie kompresuje i szyfruje pośredniego kopia zapasowa i wysyła je za pośrednictwem bezpiecznego protokołu HTTPS na skonfigurowanym magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="41f01-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="41f01-259">**Stanowczo zaleca się, że ustanowić woluminu tymczasowe na woluminie z systemem innym niż systemu Windows. Jeśli zauważysz problemy z kopii zapasowych stanu systemu, Sprawdzanie lokalizacji woluminu przemieszczania jest pierwszym krokiem rozwiązywania problemów.**</span><span class="sxs-lookup"><span data-stu-id="41f01-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="41f01-260">Jak zmienić ścieżkę woluminu przemieszczania określone w agenta usługi Kopia zapasowa Azure?</span><span class="sxs-lookup"><span data-stu-id="41f01-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="41f01-261">Wolumin przemieszczania znajduje się w folderze z pamięcią podręczną domyślnie.</span><span class="sxs-lookup"><span data-stu-id="41f01-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="41f01-262">Aby zmienić tę lokalizację, wpisz następujące polecenie (w wierszu polecenia z podwyższonym poziomem uprawnień):</span><span class="sxs-lookup"><span data-stu-id="41f01-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="41f01-263">Następnie zaktualizuj następujące wpisy rejestru ze ścieżką do nowego folderu przemieszczania woluminu.</span><span class="sxs-lookup"><span data-stu-id="41f01-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="41f01-264">Ścieżka rejestru</span><span class="sxs-lookup"><span data-stu-id="41f01-264">Registry path</span></span>|<span data-ttu-id="41f01-265">Klucz rejestru</span><span class="sxs-lookup"><span data-stu-id="41f01-265">Registry key</span></span>|<span data-ttu-id="41f01-266">Wartość</span><span class="sxs-lookup"><span data-stu-id="41f01-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="41f01-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="41f01-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="41f01-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="41f01-268">SSBStagingPath</span></span> | <span data-ttu-id="41f01-269">Nowa lokalizacja woluminu przemieszczania</span><span class="sxs-lookup"><span data-stu-id="41f01-269">new staging volume location</span></span> |

<span data-ttu-id="41f01-270">Ścieżka przemieszczania jest rozróżniana wielkość liter i muszą być dokładnie odpowiadać tej samej jako co istnieje na serwerze.</span><span class="sxs-lookup"><span data-stu-id="41f01-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="41f01-271">Po zmianie ścieżki woluminu przemieszczania, uruchom ponownie Aparat kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="41f01-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="41f01-272">Aby pobrać zmieniona ścieżka, otwórz agenta usług odzyskiwania Microsoft Azure i Wyzwól ad hoc kopię zapasową stanu systemu.</span><span class="sxs-lookup"><span data-stu-id="41f01-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="41f01-273">Dlaczego ustawiono przechowywania domyślnego stanu systemu do 60 dni</span><span class="sxs-lookup"><span data-stu-id="41f01-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="41f01-274">Użytkowania kopii zapasowej stanu systemu jest taka sama jak ustawienie "okresu istnienia reliktu" dla roli usługi Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="41f01-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="41f01-275">Wartość domyślna dla wpisu okresu istnienia reliktu wynosi 60 dni.</span><span class="sxs-lookup"><span data-stu-id="41f01-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="41f01-276">Tę wartość można ustawić dla obiektu konfiguracji usługi Directory (NTDS).</span><span class="sxs-lookup"><span data-stu-id="41f01-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="41f01-277">Jak zmienić domyślny kopii zapasowej i zasad przechowywania dla stanu systemu?</span><span class="sxs-lookup"><span data-stu-id="41f01-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="41f01-278">Aby zmienić domyślne kopii zapasowej i zasad przechowywania dla stanu systemu:</span><span class="sxs-lookup"><span data-stu-id="41f01-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="41f01-279">Zatrzymaj Aparat kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-279">Stop the Backup engine.</span></span> <span data-ttu-id="41f01-280">Uruchom następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="41f01-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="41f01-281">Dodaj lub zaktualizuj następujących wpisach kluczy rejestru w HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="41f01-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="41f01-282">Nazwa rejestru</span><span class="sxs-lookup"><span data-stu-id="41f01-282">Registry Name</span></span>|<span data-ttu-id="41f01-283">Opis</span><span class="sxs-lookup"><span data-stu-id="41f01-283">Description</span></span>|<span data-ttu-id="41f01-284">Wartość</span><span class="sxs-lookup"><span data-stu-id="41f01-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="41f01-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="41f01-285">SSBScheduleTime</span></span>|<span data-ttu-id="41f01-286">Służy do konfigurowania tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="41f01-287">Domyślna to 21: 00 czasu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="41f01-287">Default is 9PM local time.</span></span>|<span data-ttu-id="41f01-288">DWord: Format hh: mm (dziesiętna) na przykład 2130 dla 21:30:00 czasu lokalnego</span><span class="sxs-lookup"><span data-stu-id="41f01-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="41f01-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="41f01-289">SSBScheduleDays</span></span>|<span data-ttu-id="41f01-290">Służy do konfigurowania dni, kiedy należy wykonać kopii zapasowej stanu systemu w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="41f01-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="41f01-291">Poszczególnych cyfr określ dni tygodnia.</span><span class="sxs-lookup"><span data-stu-id="41f01-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="41f01-292">0 oznacza niedzielę, 1 oznacza poniedziałek, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="41f01-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="41f01-293">Dzień domyślny dla kopii zapasowej oznacza niedzielę.</span><span class="sxs-lookup"><span data-stu-id="41f01-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="41f01-294">DWord: dni tygodnia uruchamianie tworzenia kopii zapasowej (dziesiętna), na przykład 1230 harmonogramy tworzenia kopii zapasowych w poniedziałek, Wtorek, środę i niedzielę.</span><span class="sxs-lookup"><span data-stu-id="41f01-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="41f01-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="41f01-295">SSBRetentionDays</span></span>|<span data-ttu-id="41f01-296">Służy do konfigurowania dni przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="41f01-297">Wartość domyślna to 60.</span><span class="sxs-lookup"><span data-stu-id="41f01-297">Default value is 60.</span></span> <span data-ttu-id="41f01-298">Maksymalna dozwolona wartość to 180.</span><span class="sxs-lookup"><span data-stu-id="41f01-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="41f01-299">DWord: Dni przechowywania kopii zapasowych (dziesiętna).</span><span class="sxs-lookup"><span data-stu-id="41f01-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="41f01-300">Użyj następującego polecenia, aby ponownie uruchomić aparatu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="41f01-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="41f01-301">Otwórz agenta usług odzyskiwania Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41f01-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="41f01-302">Kliknij przycisk **harmonogram tworzenia kopii zapasowych** , a następnie kliknij przycisk **dalej** do momentu wyświetlenia wprowadzonych zmian.</span><span class="sxs-lookup"><span data-stu-id="41f01-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="41f01-303">Kliknij przycisk **Zakończ** Aby zastosować zmiany.</span><span class="sxs-lookup"><span data-stu-id="41f01-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="41f01-304">Pytania?</span><span class="sxs-lookup"><span data-stu-id="41f01-304">Questions?</span></span>
<span data-ttu-id="41f01-305">Jeśli masz pytania lub jeśli brakuje Ci jakiejś funkcji, [prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="41f01-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41f01-306">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41f01-306">Next steps</span></span>
* <span data-ttu-id="41f01-307">Dowiedz się więcej o [tworzeniu kopii zapasowej maszyn z systemem Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="41f01-308">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="41f01-309">Jeśli chcesz przywrócić kopię zapasową, w tym artykule znajdziesz informacje dotyczące [przywracania plików na maszynę z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="41f01-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
