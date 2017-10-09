---
title: "kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage i monitorowanie kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="fbedb-103">Zarządzanie kopiami zapasowymi maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fbedb-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbedb-104">Zarządzanie kopiami zapasowymi maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="fbedb-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="fbedb-105">Zarządzanie kopiami zapasowymi klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fbedb-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="fbedb-106">Ten artykuł zawiera wskazówki dotyczące zarządzania kopii zapasowych maszyn wirtualnych i wyjaśniono, hello alerty kopii zapasowej informacji dostępnych na pulpicie nawigacyjnym portalu hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="fbedb-107">wskazówki Hello w tym artykule dotyczą maszyn wirtualnych toousing o Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="fbedb-108">W tym artykule nie opisano hello tworzenia maszyn wirtualnych ani jest wyjaśniają sposób tooprotect maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fbedb-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="fbedb-109">Aby Elementarz o ochronie usługi Azure Resource Manager wdrożone maszyny wirtualne na platformie Azure w magazynie usług odzyskiwania, zobacz [Pierwsze spojrzenie: Utwórz kopię zapasową maszyn wirtualnych tooa magazyn usług odzyskiwania i](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fbedb-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="fbedb-110">Zarządzanie magazynami i chronione maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fbedb-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="fbedb-111">W portalu Azure hello pulpitem nawigacyjnym magazynu usług odzyskiwania hello zapewnia tooinformation dostępu o tym magazynie hello:</span><span class="sxs-lookup"><span data-stu-id="fbedb-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="fbedb-112">Hello najnowszej kopii zapasowej migawki, która jest również najnowszy punkt przywracania hello < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="fbedb-113">Witaj zasad tworzenia kopii zapasowej < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-113">hello backup policy <br\></span></span>
* <span data-ttu-id="fbedb-114">Całkowity rozmiar wszystkich migawek kopii zapasowych < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="fbedb-115">Liczba maszyn wirtualnych, które są chronione przy użyciu magazynu hello < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="fbedb-116">Wiele zadań zarządzania z kopii zapasowej maszyny wirtualnej zaczynać otwierania magazynu hello hello w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fbedb-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="fbedb-117">Jednak ponieważ magazynów, mogą być używane tooprotect wielu elementów (lub wiele maszyn wirtualnych), tooview szczegółowych informacji o określonej maszyny Wirtualnej, Otwórz pulpit nawigacyjny elementu magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="fbedb-118">Witaj poniższej procedurze wyjaśniono, jak tooopen hello *pulpitem nawigacyjnym magazynu* , a następnie kontynuuj toohello *pulpitem nawigacyjnym magazynu elementu*.</span><span class="sxs-lookup"><span data-stu-id="fbedb-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="fbedb-119">W obu tych procedur, które wskazują sposób tooadd hello magazynu i magazynu toohello elementu pulpitu nawigacyjnego Azure za pomocą polecenia toodashboard numeru Pin hello są "porady".</span><span class="sxs-lookup"><span data-stu-id="fbedb-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="fbedb-120">Toodashboard numer PIN jest sposób tworzenia skrótów toohello magazynu lub elementów.</span><span class="sxs-lookup"><span data-stu-id="fbedb-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="fbedb-121">Można również wykonywać typowe polecenia ze skrótu hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="fbedb-122">Jeśli masz wiele pulpitów nawigacyjnych i otworzyć bloków, za pomocą suwaka dark blue hello u dołu hello hello okna tooslide hello Azure pulpitu nawigacyjnego i z powrotem.</span><span class="sxs-lookup"><span data-stu-id="fbedb-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Pełny widok z suwaka](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="fbedb-124">Otwórz pulpit nawigacyjny hello magazynu usług odzyskiwania:</span><span class="sxs-lookup"><span data-stu-id="fbedb-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="fbedb-125">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fbedb-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fbedb-126">W menu Centrum powitania kliknij **Przeglądaj** i hello listy zasobów, wpisz **usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="fbedb-127">Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="fbedb-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="fbedb-128">Kliknij opcję **Magazyn Usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-128">Click **Recovery Services vault**.</span></span>

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="fbedb-130">wyświetli się lista Hello Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="fbedb-131">Lista usług odzyskiwania magazynów</span><span class="sxs-lookup"><span data-stu-id="fbedb-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="fbedb-132">Jeśli przypniesz toohello magazyn Azure pulpitu nawigacyjnego tego magazynu jest natychmiast dostępna po otwarciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fbedb-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="fbedb-133">toopin magazynu toohello pulpitu nawigacyjnego, na liście hello magazynu, kliknij prawym przyciskiem myszy hello magazynu, a następnie wybierz **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="fbedb-134">Witaj wybierz z listy magazynów hello magazynu tooopen jego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbedb-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="fbedb-135">Po wybraniu magazynu hello, hello pulpitem nawigacyjnym magazynu i hello **ustawienia** Otwórz blok.</span><span class="sxs-lookup"><span data-stu-id="fbedb-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="fbedb-136">W hello po obrazu, hello **magazynu Contoso** zostanie wyróżniona pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbedb-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Otwórz pulpit nawigacyjny magazynu i blok ustawień](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="fbedb-138">Otwórz pulpit nawigacyjny elementu magazynu</span><span class="sxs-lookup"><span data-stu-id="fbedb-138">Open a vault item dashboard</span></span>
<span data-ttu-id="fbedb-139">W poprzedniej procedurze hello możesz otworzyć hello pulpitem nawigacyjnym magazynu.</span><span class="sxs-lookup"><span data-stu-id="fbedb-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="fbedb-140">tooopen hello elementu pulpitem nawigacyjnym magazynu:</span><span class="sxs-lookup"><span data-stu-id="fbedb-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="fbedb-141">Na pulpicie nawigacyjnym magazynu hello, na powitania **kopii zapasowej elementów** Kafelek, kliknij przycisk **maszyny wirtualne Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Kafelek otwarte elementy kopii zapasowej](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="fbedb-143">Witaj **elementów kopii zapasowych** hello ostatnie zadanie tworzenia kopii zapasowej dla każdego elementu listy bloku.</span><span class="sxs-lookup"><span data-stu-id="fbedb-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="fbedb-144">W tym przykładzie Brak jednej maszyny wirtualnej, demovm-markgal chronione przez ten magazyn.</span><span class="sxs-lookup"><span data-stu-id="fbedb-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="fbedb-146">W celu ułatwienia dostępu można przypiąć toohello elementu magazynu Azure pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbedb-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="fbedb-147">toopin elementu magazynu w hello magazyn elementu listy, element powitania kliknij prawym przyciskiem myszy i wybierz **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="fbedb-148">W hello **kopii zapasowej elementów** bloku, kliknij element hello tooopen magazynu hello elementów pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fbedb-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="fbedb-150">pulpit nawigacyjny elementu magazynu Hello i jego **ustawienia** Otwórz blok.</span><span class="sxs-lookup"><span data-stu-id="fbedb-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Pulpit nawigacyjny elementów kopii zapasowych z bloku ustawień](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="fbedb-152">Z hello magazyn elementów pulpitu nawigacyjnego można wykonywać wiele zadań zarządzania kluczami, takich jak:</span><span class="sxs-lookup"><span data-stu-id="fbedb-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="fbedb-153">Zmiana zasad lub utworzyć nowe zasady tworzenia kopii zapasowej < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="fbedb-154">Wyświetl punkty przywracania i wyświetlić ich stan spójności < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="fbedb-155">na żądanie kopii zapasowej maszyny wirtualnej < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="fbedb-156">Zatrzymaj ochronę maszyn wirtualnych < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="fbedb-157">wznowić ochronę maszyny wirtualnej < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="fbedb-158">Usuwanie danych kopii zapasowej (lub punktu odzyskiwania) < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="fbedb-159">[Przywracanie kopii zapasowych dysków](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="fbedb-160">W przypadku hello zgodnie z procedurami hello punkt początkowy jest pulpit nawigacyjny elementu magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="fbedb-161">Zarządzanie zasadami tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="fbedb-161">Manage backup policies</span></span>
1. <span data-ttu-id="fbedb-162">Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **wszystkie ustawienia** tooopen hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="fbedb-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Blok zasady tworzenia kopii zapasowej](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="fbedb-164">Na powitania **ustawienia** bloku, kliknij przycisk **kopii zapasowej zasad** tooopen tego bloku.</span><span class="sxs-lookup"><span data-stu-id="fbedb-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="fbedb-165">W bloku hello hello kopii zapasowej częstotliwości i przechowywania zakresu są wyświetlane szczegóły.</span><span class="sxs-lookup"><span data-stu-id="fbedb-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Blok zasady tworzenia kopii zapasowej](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="fbedb-167">Z hello **wybierz zasady tworzenia kopii zapasowej** menu:</span><span class="sxs-lookup"><span data-stu-id="fbedb-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="fbedb-168">toochange zasady, wybierz inne zasady i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="fbedb-169">nowe zasady Hello jest natychmiast zastosowane toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="fbedb-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="fbedb-170">< br\></span><span class="sxs-lookup"><span data-stu-id="fbedb-170"><br\></span></span>
   * <span data-ttu-id="fbedb-171">Wybierz zasady, toocreate **Utwórz nowy**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-171">toocreate a policy, select **Create New**.</span></span>

     ![Kopia zapasowa maszyny wirtualnej](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="fbedb-173">Aby uzyskać instrukcje na temat tworzenia zasad tworzenia kopii zapasowej, zobacz [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="fbedb-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="fbedb-174">Zasady tworzenia kopii zapasowej i zarządzania nimi, upewnij się, że hello toofollow [najlepsze rozwiązania](backup-azure-vms-introduction.md#best-practices) do uzyskania optymalnej wydajności tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="fbedb-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="fbedb-175">Na żądanie kopii zapasowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fbedb-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="fbedb-176">Skonfigurowane dla ochrony na żądanie można wykonać kopii zapasowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="fbedb-177">Jeśli oczekuje początkowa kopia zapasowa hello kopii zapasowej na żądanie tworzy pełną kopię hello maszyny wirtualnej w powitalne magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="fbedb-178">Jeśli hello początkowa kopia zapasowa została wykonana, na żądanie kopii zapasowej tylko wysłać zmiany z hello poprzednią migawkę toohello magazyn usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="fbedb-179">Oznacza to, że kolejne kopie zapasowe są zawsze przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="fbedb-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="fbedb-180">zakres przechowywania kopii zapasowych na żądanie Hello jest hello wartość przechowywania określona dla hello codziennego punktu kopii zapasowej w zasadach hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="fbedb-181">Jeśli wybrano opcję nie codziennego punktu kopii zapasowej, tygodniowego punktu kopii zapasowej hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="fbedb-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="fbedb-182">tootrigger na żądanie kopii zapasowej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="fbedb-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="fbedb-183">Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Kopię zapasową teraz przycisku.](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="fbedb-185">Hello portal upewnia się, że chcesz toostart zadanie tworzenia kopii zapasowej na żądanie.</span><span class="sxs-lookup"><span data-stu-id="fbedb-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="fbedb-186">Kliknij przycisk **tak** toostart hello — zadanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-186">Click **Yes** toostart hello backup job.</span></span>

    ![Kopię zapasową teraz przycisku.](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="fbedb-188">zadanie tworzenia kopii zapasowej Hello tworzy punkt odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="fbedb-189">zakres przechowywania Hello hello punkt odzyskiwania jest hello taki sam jak zakres przechowywania określonym w zasadach hello skojarzonych z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="fbedb-190">postęp hello tootrack hello zadania, na pulpicie nawigacyjnym magazynu hello, kliknij przycisk hello **zadania tworzenia kopii zapasowej** kafelka.</span><span class="sxs-lookup"><span data-stu-id="fbedb-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="fbedb-191">Zatrzymaj ochronę maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="fbedb-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="fbedb-192">Jeśli wybierzesz toostop ochrony maszyny wirtualnej, są pytanie, czy punkty odzyskiwania hello tooretain.</span><span class="sxs-lookup"><span data-stu-id="fbedb-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="fbedb-193">Istnieją dwa sposoby toostop ochrona maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="fbedb-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="fbedb-194">zatrzymanie wszystkich przyszłych zadań kopii zapasowej i usunięcie wszystkich punktów odzyskiwania lub</span><span class="sxs-lookup"><span data-stu-id="fbedb-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="fbedb-195">zatrzymanie wszystkich przyszłych zadań kopii zapasowej, ale pozostawić hello punktów odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="fbedb-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="fbedb-196">Brak kosztów związanych z pozostawienie hello punktów odzyskiwania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="fbedb-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="fbedb-197">Jednak zaletą hello pozostawienie hello punktów odzyskiwania jest hello maszyny wirtualnej można przywrócić później, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="fbedb-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="fbedb-198">Aby dowiedzieć koszt hello opuszczania hello punktów odzyskiwania, zobacz hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="fbedb-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="fbedb-199">Jeśli wybierzesz toodelete wszystkich punktów odzyskiwania, nie można przywrócić hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="fbedb-200">toostop ochrony dla maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="fbedb-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="fbedb-201">Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **kopii zapasowej Zatrzymaj**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="fbedb-203">zostanie otwarty blok tworzenia kopii zapasowej Zatrzymaj Hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-203">hello Stop Backup blade opens.</span></span>

    ![Zatrzymywanie tworzenia kopii zapasowej bloku](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="fbedb-205">Na powitania **zatrzymać kopii zapasowej** bloku, wybierz, czy tooretain lub usuń hello dane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="fbedb-206">pole informacje Hello zawiera szczegółowe informacje o wybranym.</span><span class="sxs-lookup"><span data-stu-id="fbedb-206">hello information box provides details about your choice.</span></span>

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="fbedb-208">W przypadku wybrania dane kopii zapasowej hello tooretain Pomiń toostep 4.</span><span class="sxs-lookup"><span data-stu-id="fbedb-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="fbedb-209">W przypadku wybrania toodelete dane kopii zapasowej potwierdzić, że mają zadania tworzenia kopii zapasowej hello toostop i usunąć punktów odzyskiwania hello — Nazwa typu hello hello elementu.</span><span class="sxs-lookup"><span data-stu-id="fbedb-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Zatrzymaj weryfikacji](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="fbedb-211">Jeśli nie masz pewności co nazwa elementu hello, umieść kursor nad hello wykrzyknik tooview hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="fbedb-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="fbedb-212">Nazwa hello elementu hello jest również w obszarze **zatrzymać kopii zapasowej** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="fbedb-213">Opcjonalnie wprowadź **Przyczyna** lub **komentarz**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="fbedb-214">Kliknij zadanie tworzenia kopii zapasowej hello toostop dla bieżącego elementu hello, ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="fbedb-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="fbedb-215">Komunikat z powiadomieniem informuje o tym, że zadania tworzenia kopii zapasowej hello zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="fbedb-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Upewnij się, Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="fbedb-217">Wznów ochronę maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fbedb-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="fbedb-218">Jeśli hello **Zachowaj dane kopii zapasowej** została wybrana opcja podczas ochrony dla maszyny wirtualnej hello została zatrzymana, wówczas jest możliwe tooresume ochrony.</span><span class="sxs-lookup"><span data-stu-id="fbedb-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="fbedb-219">Jeśli hello **usunąć dane z kopii zapasowej** została wybrana opcja, a następnie nie można wznowić ochronę hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="fbedb-220">ochronę tooresume hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fbedb-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="fbedb-221">Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **Wznów wykonywanie kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Wznów ochronę](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="fbedb-223">zostanie otwarty blok zasad tworzenia kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbedb-224">Podczas ponownie ochrona powitalnych maszyny wirtualnej, można wybrać inne zasady niż zasady hello, z którą maszyny wirtualnej został początkowo chronić.</span><span class="sxs-lookup"><span data-stu-id="fbedb-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="fbedb-225">Wykonaj kroki hello w [Zarządzanie zasadami tworzenia kopii zapasowej](backup-azure-manage-vms.md#manage-backup-policies) zasad hello tooassign hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fbedb-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="fbedb-226">Po hello zasad tworzenia kopii zapasowej jest stosowane toohello maszyny wirtualnej, zapoznaj się hello następującą wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fbedb-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Pomyślnie chronionej maszyny Wirtualnej](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="fbedb-228">Usuwanie danych kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="fbedb-228">Delete Backup data</span></span>
<span data-ttu-id="fbedb-229">Można usunąć danych kopii zapasowej hello skojarzonych z maszyną wirtualną podczas hello **kopii zapasowej Zatrzymaj** zadania, albo w dowolnym momencie po hello zadanie tworzenia kopii zapasowej została ukończona.</span><span class="sxs-lookup"><span data-stu-id="fbedb-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="fbedb-230">Alternatywą może być korzystne toowait dni lub tygodnie przed usunięciem hello punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="fbedb-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="fbedb-231">W odróżnieniu od przywracanie punktów odzyskiwania, podczas usuwania danych kopii zapasowej, nie można wybrać określonego odzyskiwania toodelete punktów.</span><span class="sxs-lookup"><span data-stu-id="fbedb-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="fbedb-232">Jeśli wybierzesz toodelete danych kopii zapasowych, należy usunąć wszystkie punkty odzyskiwania skojarzone z elementem hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="fbedb-233">Witaj poniższej procedurze przyjęto hello zadanie tworzenia kopii zapasowej dla maszyny wirtualnej hello została zatrzymana lub wyłączona.</span><span class="sxs-lookup"><span data-stu-id="fbedb-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="fbedb-234">Po wyłączeniu zadanie tworzenia kopii zapasowej hello hello **Wznów wykonywanie kopii zapasowej** i **kopii zapasowej Delete** opcje są dostępne na pulpicie nawigacyjnym elementu magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Wznów i usuń przyciski](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="fbedb-236">toodelete dane kopii zapasowej na maszynie wirtualnej z hello *kopii zapasowej wyłączone*:</span><span class="sxs-lookup"><span data-stu-id="fbedb-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="fbedb-237">Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **usunięcia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="fbedb-239">Witaj **usunąć dane z kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="fbedb-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="fbedb-241">Nazwa typu hello hello elementu tooconfirm ma punktów odzyskiwania hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="fbedb-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Zatrzymaj weryfikacji](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="fbedb-243">Jeśli nie masz pewności co nazwa elementu hello, umieść kursor nad hello wykrzyknik tooview hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="fbedb-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="fbedb-244">Nazwa hello elementu hello jest również w obszarze **usunąć dane z kopii zapasowej** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="fbedb-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="fbedb-245">Opcjonalnie wprowadź **Przyczyna** lub **komentarz**.</span><span class="sxs-lookup"><span data-stu-id="fbedb-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="fbedb-246">dane kopii zapasowej hello toodelete dla bieżącego elementu hello, kliknij przycisk ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="fbedb-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="fbedb-247">Komunikat z powiadomieniem informuje hello danych kopii zapasowych została usunięta.</span><span class="sxs-lookup"><span data-stu-id="fbedb-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbedb-248">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbedb-248">Next steps</span></span>
<span data-ttu-id="fbedb-249">Informacje dotyczące ponownego tworzenia maszyny wirtualnej z punktu odzyskiwania, zapoznaj się z [przywracanie maszyn wirtualnych Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="fbedb-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="fbedb-250">Jeśli potrzebujesz informacji na temat ochrony maszyn wirtualnych, zobacz [Pierwsze spojrzenie: Utwórz kopię zapasową maszyn wirtualnych tooa magazyn usług odzyskiwania i](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fbedb-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="fbedb-251">Aby uzyskać informacje dotyczące monitorowania zdarzeń, zobacz [monitorowania alertów dla kopii zapasowych maszyn wirtualnych Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="fbedb-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
