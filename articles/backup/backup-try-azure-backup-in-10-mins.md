---
title: "Tworzenie kopii zapasowych plików i folderów systemu Windows na platformie Azure (Resource Manager) | Microsoft Docs"
description: "Dowiedz się, jak tworzyć kopie zapasowe plików i folderów systemu Windows na platformie Azure w ramach wdrożenia usługi Resource Manager."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "jak tworzyć kopie zapasowe; tworzenie kopii zapasowych; tworzenie kopii zapasowych plików i folderów"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: b21edb70eca3ec9552dc157ee3bb658d243b8fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="4fb17-104">Pierwsze spojrzenie: tworzenie kopii zapasowych plików i folderów w ramach wdrożenia usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4fb17-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="4fb17-105">W tym artykule opisano sposób tworzenia kopii zapasowych plików i folderów systemu Windows Server (lub komputera z systemem Windows) na platformie Azure w ramach wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fb17-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="4fb17-106">Ten samouczek zawiera podstawowe informacje.</span><span class="sxs-lookup"><span data-stu-id="4fb17-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="4fb17-107">Jeśli chcesz rozpocząć korzystanie z usługi Azure Backup, to jesteś w odpowiednim miejscu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="4fb17-108">Jeśli chcesz dowiedzieć się więcej o usłudze Azure Backup, przeczytaj to [omówienie](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="4fb17-109">Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/) umożliwiające dostęp do dowolnej usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4fb17-110">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4fb17-110">Create a recovery services vault</span></span>
<span data-ttu-id="4fb17-111">Aby utworzyć kopię zapasową plików i folderów, należy utworzyć magazyn usługi Recovery Services w regionie, w którym chcesz przechowywać dane.</span><span class="sxs-lookup"><span data-stu-id="4fb17-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="4fb17-112">Należy również określić sposób replikowania magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="4fb17-113">Aby utworzyć magazyn usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4fb17-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="4fb17-114">Jeśli nie zostało to wcześniej zrobione, zaloguj się witryny [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="4fb17-115">W menu Centrum kliknij pozycję **Więcej usług**, na liście zasobów wpisz łańcuch **Recovery Services**, a następnie kliknij pozycję **Magazyny usługi Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="4fb17-117">Jeśli w ramach subskrypcji istnieją magazyny usług odzyskiwania, zostaną one wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="4fb17-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="4fb17-118">W menu **Magazyny usługi Recovery Services** kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="4fb17-120">Zostanie otwarty blok magazynu Usług odzyskiwania i pojawi się monit o podanie wartości w polach **Nazwa**, **Subskrypcja**, **Grupa zasobów** i **Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="4fb17-122">W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn.</span><span class="sxs-lookup"><span data-stu-id="4fb17-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="4fb17-123">Nazwa musi być unikalna w tej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="4fb17-124">Wpisz nazwę o długości od 2 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="4fb17-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="4fb17-125">Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="4fb17-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="4fb17-126">W sekcji **Subskrypcja** użyj menu rozwijanego, aby wybrać subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="4fb17-127">Jeśli używasz tylko jednej subskrypcji, zostanie ona wyświetlona i możesz przejść do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="4fb17-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="4fb17-128">Jeśli nie masz pewności, której subskrypcji użyć, wybierz domyślną (lub sugerowaną).</span><span class="sxs-lookup"><span data-stu-id="4fb17-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="4fb17-129">Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="4fb17-130">W sekcji **Grupa zasobów**:</span><span class="sxs-lookup"><span data-stu-id="4fb17-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="4fb17-131">wybierz pozycję **Utwórz nową**, jeśli chcesz utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="4fb17-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="4fb17-132">Lub</span><span class="sxs-lookup"><span data-stu-id="4fb17-132">Or</span></span>
    * <span data-ttu-id="4fb17-133">wybierz pozycję **Użyj istniejącej** i kliknij menu rozwijane, aby wyświetlić listę dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="4fb17-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="4fb17-134">Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="4fb17-135">Kliknij pozycję **Lokalizacja**, aby wybrać region geograficzny magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="4fb17-136">Ten wybór określa region geograficzny, do którego wysyłane są dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="4fb17-137">W dolnej części bloku magazynu usług Recovery Services kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="4fb17-138">Utworzenie magazynu usług Recovery Services może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="4fb17-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="4fb17-139">Monitoruj powiadomienia o stanie wyświetlane w prawej górnej części obszaru portalu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="4fb17-140">Po utworzeniu magazynu pojawi się on na liście magazynów Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="4fb17-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="4fb17-141">Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="4fb17-143">Po wyświetleniu magazynu na liście magazynów usług Recovery Services możesz rozpocząć ustawianie nadmiarowości przechowywania.</span><span class="sxs-lookup"><span data-stu-id="4fb17-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="4fb17-144">Ustawianie nadmiarowości przechowywania dla magazynu</span><span class="sxs-lookup"><span data-stu-id="4fb17-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="4fb17-145">Po utworzeniu magazynu usług Recovery Services upewnij się, że nadmiarowość magazynu została skonfigurowana w preferowany sposób.</span><span class="sxs-lookup"><span data-stu-id="4fb17-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="4fb17-146">W bloku **Magazyny usług Recovery Services** kliknij nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="4fb17-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Wybieranie nowego magazynu z listy magazynów usług Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="4fb17-148">Wybranie magazynu spowoduje zwężenie bloku **Magazyn usług Recovery Services** oraz otwarcie bloków Ustawienia (*o nazwie magazynu wskazanego w górnej części*) i szczegółów magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Wyświetlanie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="4fb17-150">W bloku ustawień nowego magazynu użyj pionowego suwaka, aby przewinąć w dół do sekcji Zarządzanie, a następnie kliknij pozycję **Infrastruktura zapasowa**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="4fb17-151">Zostanie otwarty blok Infrastruktura zapasowa.</span><span class="sxs-lookup"><span data-stu-id="4fb17-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="4fb17-152">W bloku Infrastruktura zapasowa kliknij pozycję **Konfiguracja kopii zapasowej** w celu otwarcia bloku **Konfiguracja kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Ustawianie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="4fb17-154">Wybierz odpowiednią opcję replikacji dla magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="4fb17-156">Domyślnie magazyn jest nadmiarowy geograficznie.</span><span class="sxs-lookup"><span data-stu-id="4fb17-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="4fb17-157">Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, kontynuuj korzystanie z magazynu **geograficznie nadmiarowego**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="4fb17-158">Jeśli nie używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, wybierz pozycję **Lokalnie nadmiarowy**, co zmniejszy koszty magazynów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="4fb17-159">Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="4fb17-160">Teraz, kiedy został utworzony magazyn, należy go skonfigurować do tworzenia kopii zapasowych plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="4fb17-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="4fb17-161">Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="4fb17-161">Configure the vault</span></span>
1. <span data-ttu-id="4fb17-162">W bloku Magazyn usługi Recovery Services (dla właśnie utworzonego magazynu) w sekcji Wprowadzenie kliknij pozycję **Kopia zapasowa**, a następnie w bloku **Wprowadzenie do kopii zapasowej** wybierz pozycję **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="4fb17-164">Zostanie otwarty blok **Cel kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-164">The **Backup Goal** blade opens.</span></span>

    ![Otwieranie bloku celu kopii zapasowej](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="4fb17-166">Z menu **Gdzie działa Twoje obciążenie?** wybierz pozycję **Lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="4fb17-167">Pozycję **Lokalnie** trzeba wybrać, ponieważ Twój serwer lub komputer z systemem Windows jest maszyną fizyczną spoza platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb17-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="4fb17-168">Z menu **Dla jakich elementów chcesz utworzyć kopię zapasową?** wybierz pozycję **Pliki i foldery**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Konfigurowanie plików i folderów](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="4fb17-170">Po kliknięciu przycisku OK obok pozycji **Cel kopii zapasowej** pojawi się znacznik wyboru i zostanie otwarty blok **Przygotowywanie infrastruktury**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Cel kopii zapasowej został skonfigurowany, następnym krokiem jest przygotowanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="4fb17-172">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz agenta dla systemu Windows Server lub klienta systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="4fb17-174">Jeśli używasz systemu Windows Server Essential, wybierz opcję pobrania agenta dla systemu Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="4fb17-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="4fb17-175">Zostanie wyświetlone menu rozwijane z monitem o uruchomienie lub zapisanie pliku MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="4fb17-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Okno dialogowe MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="4fb17-177">W menu rozwijanym pobierania kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="4fb17-178">Domyślnie plik **MARSagentinstaller.exe** jest zapisywany w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fb17-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="4fb17-179">Po ukończeniu pobierania pojawi się okno podręczne z pytaniem, czy chcesz uruchomić Instalatora, czy otworzyć folder.</span><span class="sxs-lookup"><span data-stu-id="4fb17-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Przygotowywanie infrastruktury](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="4fb17-181">Nie musisz jeszcze instalować agenta.</span><span class="sxs-lookup"><span data-stu-id="4fb17-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="4fb17-182">Agenta możesz zainstalować po pobraniu poświadczeń magazynu.</span><span class="sxs-lookup"><span data-stu-id="4fb17-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="4fb17-183">W bloku **Przygotowywanie infrastruktury** kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Pobieranie poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="4fb17-185">Poświadczenia magazynu zostaną pobrane do folderu Pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fb17-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="4fb17-186">Po zakończeniu pobierania poświadczeń magazynu zobaczysz okno podręczne z pytaniem, czy chcesz otworzyć poświadczenia, czy je zapisać.</span><span class="sxs-lookup"><span data-stu-id="4fb17-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="4fb17-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-187">Click **Save**.</span></span> <span data-ttu-id="4fb17-188">Jeśli przypadkowo klikniesz pozycję **Otwórz**, zaczekaj, aż działanie okna dialogowego, które spróbuje otworzyć poświadczenia magazynu, zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="4fb17-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="4fb17-189">Poświadczeń magazynu nie da się otworzyć.</span><span class="sxs-lookup"><span data-stu-id="4fb17-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="4fb17-190">Przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="4fb17-190">Proceed to the next step.</span></span> <span data-ttu-id="4fb17-191">Poświadczenia magazynu znajdują się w folderze Pobrane.</span><span class="sxs-lookup"><span data-stu-id="4fb17-191">The vault credentials are in the Downloads folder.</span></span>   

    ![Zakończenie pobierania poświadczeń magazynu](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="4fb17-193">Instalowanie i rejestrowanie agenta</span><span class="sxs-lookup"><span data-stu-id="4fb17-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="4fb17-194">Opcja włączania kopii zapasowych za pośrednictwem witryny Azure Portal jest jeszcze niedostępna.</span><span class="sxs-lookup"><span data-stu-id="4fb17-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="4fb17-195">Do tworzenia kopii zapasowej plików i folderów należy używać agenta usług Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb17-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="4fb17-196">Zlokalizuj i kliknij dwukrotnie plik **MARSagentinstaller.exe** w folderze Pobrane (lub innej lokalizacji).</span><span class="sxs-lookup"><span data-stu-id="4fb17-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="4fb17-197">Instalator wyświetli serię komunikatów w miarę wypakowywania, instalowania i rejestrowania agenta usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb17-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Uruchamianie Instalatora agenta usługi Recovery Services — poświadczenia](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="4fb17-199">Wykonaj kroki kreatora instalacji agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb17-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="4fb17-200">Aby zakończyć pracę kreatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4fb17-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="4fb17-201">Wybierz lokalizację folderu instalacji i folderu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="4fb17-202">Podaj informacje o serwerze proxy, jeśli korzystasz z niego do łączenia się z Internetem.</span><span class="sxs-lookup"><span data-stu-id="4fb17-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="4fb17-203">Podaj swoją nazwę użytkownika i hasło, jeśli korzystasz z uwierzytelnionego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="4fb17-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="4fb17-204">Udostępnianie pobranych poświadczeń magazynu</span><span class="sxs-lookup"><span data-stu-id="4fb17-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="4fb17-205">Zapisz hasło szyfrowania w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4fb17-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4fb17-206">Jeśli utracisz lub zapomnisz hasło, firma Microsoft nie będzie mogła pomóc w odzyskaniu danych kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="4fb17-207">Zapisz plik w bezpiecznej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4fb17-207">Save the file in a secure location.</span></span> <span data-ttu-id="4fb17-208">Jest ono wymagane do przywrócenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="4fb17-209">Agent jest teraz zainstalowany, a maszyna zarejestrowana w magazynie.</span><span class="sxs-lookup"><span data-stu-id="4fb17-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="4fb17-210">Wszystko jest gotowe do skonfigurowania kopii zapasowej i zaplanowania jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="4fb17-210">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="4fb17-211">Wymagania dotyczące sieci i łączności</span><span class="sxs-lookup"><span data-stu-id="4fb17-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="4fb17-212">Jeśli Twój komputer/serwer proxy ma ograniczony dostęp do Internetu, upewnij się, że ustawienia zapory na komputerze/serwerze proxy są skonfigurowane w taki sposób, że zezwalają na łączenie się z następującymi adresami URL:</span><span class="sxs-lookup"><span data-stu-id="4fb17-212">If your machine/proxy has limited internet access, ensure that firewall settings on the mcahine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="4fb17-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="4fb17-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="4fb17-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="4fb17-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="4fb17-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="4fb17-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="4fb17-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4fb17-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="4fb17-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="4fb17-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="4fb17-218">Tworzenie kopii zapasowej plików i folderów</span><span class="sxs-lookup"><span data-stu-id="4fb17-218">Back up your files and folders</span></span>
<span data-ttu-id="4fb17-219">Tworzenie początkowej kopii zapasowej obejmuje dwa kluczowe zadania:</span><span class="sxs-lookup"><span data-stu-id="4fb17-219">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="4fb17-220">Planowanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="4fb17-220">Schedule the backup</span></span>
* <span data-ttu-id="4fb17-221">Tworzenie kopii zapasowej plików i folderów po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="4fb17-221">Back up files and folders for the first time</span></span>

<span data-ttu-id="4fb17-222">Aby utworzyć początkową kopię zapasową, użyj agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb17-222">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="4fb17-223">Aby zaplanować zadanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="4fb17-223">To schedule the backup job</span></span>
1. <span data-ttu-id="4fb17-224">Otwórz agenta usługi Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb17-224">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="4fb17-225">Aby go znaleźć, wyszukaj na maszynie łańcuch **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Uruchamianie agenta usługi Azure Recovery Services](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="4fb17-227">W agencie usługi Recovery Services kliknij pozycję **Zaplanuj wykonywanie kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-227">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planowanie tworzenia kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="4fb17-229">Na stronie Wprowadzenie Kreatora harmonogramu kopii zapasowej kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-229">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="4fb17-230">Na stronie Wybieranie elementów do wykonania kopii zapasowej kliknij pozycję **Dodaj elementy**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-230">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="4fb17-231">Wybierz pliki i foldery, których kopię zapasową chcesz utworzyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-231">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="4fb17-232">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-232">Click **Next**.</span></span>
7. <span data-ttu-id="4fb17-233">Na stronie **Określanie harmonogramu tworzenia kopii zapasowych** określ **harmonogram tworzenia kopii zapasowej**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-233">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="4fb17-234">Można zaplanować tworzenie kopii zapasowych codziennie (maksymalnie trzy razy) lub co tydzień.</span><span class="sxs-lookup"><span data-stu-id="4fb17-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementy związane z tworzeniem kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="4fb17-236">Aby uzyskać więcej informacji o sposobie określania harmonogramu tworzenia kopii zapasowych, zobacz artykuł [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md) (Użycie usługi Azure Backup do zastąpienia infrastruktury taśm).</span><span class="sxs-lookup"><span data-stu-id="4fb17-236">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="4fb17-237">Na stronie **Wybieranie zasady przechowywania** wybierz pozycję **Zasady przechowywania** dla kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-237">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="4fb17-238">Zasady przechowywania określają, jak długo dane kopii zapasowej są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="4fb17-238">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="4fb17-239">Zamiast określać wspólne zasady dla wszystkich punktów kopii zapasowej, można określić różne zasady przechowywania w zależności od momentu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="4fb17-240">Możliwe jest modyfikowanie, zgodnie z potrzebami, zasad przechowywania codziennych, cotygodniowych, comiesięcznych i corocznych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4fb17-240">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="4fb17-241">Na stronie Wybieranie typu początkowej kopii zapasowej wybierz typ początkowej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="4fb17-241">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="4fb17-242">Pozostaw zaznaczoną opcję **Automatycznie przez sieć**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-242">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="4fb17-243">Kopie zapasowe można tworzyć automatycznie za pośrednictwem sieci lub w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="4fb17-243">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="4fb17-244">W dalszej części tego artykułu opisano proces automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4fb17-244">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="4fb17-245">Jeśli chcesz tworzyć kopie zapasowe w trybie offline, zapoznaj się z artykułem [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) (Przepływ pracy tworzenia kopii zapasowej w trybie offline w usłudze Azure Backup), aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="4fb17-245">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="4fb17-246">Przejrzyj informacje na stronie Potwierdzenie, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-246">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="4fb17-247">Po ukończeniu harmonogramu tworzenia kopii zapasowej przez kreatora kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-247">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="4fb17-248">Aby utworzyć kopię zapasową plików i folderów po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="4fb17-248">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="4fb17-249">W agencie Usług odzyskiwania kliknij pozycję **Wykonaj kopię zapasową teraz**, aby zakończyć początkowe umieszczanie za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="4fb17-249">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Natychmiastowe tworzenie kopii zapasowej systemu Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="4fb17-251">Na stronie Potwierdzenie przejrzyj ustawienia, które zostaną użyte przez Kreatora natychmiastowego tworzenia kopii zapasowej do utworzenia kopii zapasowej maszyny.</span><span class="sxs-lookup"><span data-stu-id="4fb17-251">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="4fb17-252">Następnie kliknij pozycję **Utwórz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="4fb17-253">Kliknij przycisk **Zamknij**, aby zamknąć kreatora.</span><span class="sxs-lookup"><span data-stu-id="4fb17-253">Click **Close** to close the wizard.</span></span> <span data-ttu-id="4fb17-254">Jeśli zamkniesz kreatora przed zakończeniem procesu tworzenia kopii zapasowej, kreator będzie nadal działać w tle.</span><span class="sxs-lookup"><span data-stu-id="4fb17-254">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="4fb17-255">Po zakończeniu tworzenia początkowej kopii zapasowej w konsoli usługi Backup zostanie wyświetlony stan **Ukończono zadanie**.</span><span class="sxs-lookup"><span data-stu-id="4fb17-255">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Początkowa replikacja została zakończona](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="4fb17-257">Pytania?</span><span class="sxs-lookup"><span data-stu-id="4fb17-257">Questions?</span></span>
<span data-ttu-id="4fb17-258">Jeśli masz pytania lub jeśli brakuje Ci jakiejś funkcji, [prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="4fb17-258">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fb17-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4fb17-259">Next steps</span></span>
* <span data-ttu-id="4fb17-260">Dowiedz się więcej o [tworzeniu kopii zapasowej maszyn z systemem Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="4fb17-261">Teraz, gdy utworzono kopię zapasową plików i folderów, możesz [zarządzać swoimi magazynami i serwerami](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="4fb17-262">Jeśli chcesz przywrócić kopię zapasową, w tym artykule znajdziesz informacje dotyczące [przywracania plików na maszynę z systemem Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4fb17-262">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
