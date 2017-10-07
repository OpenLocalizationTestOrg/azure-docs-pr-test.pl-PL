---
title: "aaaBack się magazynu kopii zapasowych tooa wdrożone w klasycznej maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Odnajdowanie, rejestrowania i utworzyć kopię zapasową maszyn wirtualnych z tych procedur do utworzenia kopii zapasowej maszyny wirtualnej platformy Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: kopii zapasowej maszyny wirtualnej. Tworzenie kopii zapasowej maszyny wirtualnej; Kopia zapasowa i odzyskiwanie po awarii; kopii zapasowej maszyny wirtualnej
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="11dca-104">Tworzenie kopii zapasowej maszyn wirtualnych platformy Azure (klasyczny portal)</span><span class="sxs-lookup"><span data-stu-id="11dca-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11dca-105">Wykonaj kopię zapasową magazynu usług tooRecovery maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="11dca-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="11dca-106">Wykonaj kopię zapasową magazynu tooBackup maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="11dca-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="11dca-107">Ten artykuł zawiera hello procedur tworzenia kopii zapasowych w magazynie kopii zapasowej tooa wdrożone w klasycznej maszyny wirtualnej platformy Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="11dca-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="11dca-108">Istnieje kilka zadań, które należy tootake care z przed utworzeniem kopii zapasowej maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="11dca-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="11dca-109">Jeśli jeszcze tak, pełną hello [wymagania wstępne](backup-azure-vms-prepare.md) tooprepare środowiska do tworzenia kopii zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11dca-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="11dca-110">Aby uzyskać dodatkowe informacje, zobacz artykuły hello na [planowania infrastruktury kopii zapasowych maszyn wirtualnych na platformie Azure](backup-azure-vms-introduction.md) i [maszyn wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="11dca-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="11dca-111">Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="11dca-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="11dca-112">Magazyn kopii zapasowych może chronić tylko wdrożone w klasycznej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11dca-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="11dca-113">Nie można chronić wdrożonych przez Menedżera zasobów maszyn wirtualnych w magazynie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="11dca-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="11dca-114">Zobacz [kopii zapasowych maszyn wirtualnych tooRecovery usług magazynu](backup-azure-arm-vms.md) szczegółowe informacje na temat pracy z usług odzyskiwania magazynów.</span><span class="sxs-lookup"><span data-stu-id="11dca-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="11dca-115">Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure obejmuje trzy kroki klucza:</span><span class="sxs-lookup"><span data-stu-id="11dca-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Trzy kroki tooback zapasowej maszyny Wirtualnej platformy Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="11dca-117">Tworzenie kopii zapasowych maszyn wirtualnych jest procesem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="11dca-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="11dca-118">Nie można utworzyć kopii zapasowych maszyn wirtualnych w jeden region tooa magazyn kopii zapasowych w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="11dca-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="11dca-119">Dlatego należy utworzyć magazyn kopii zapasowych w każdym regionie Azure, gdy istnieją maszyny wirtualne, które zostaną umieszczone w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="11dca-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="11dca-120">Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="11dca-121">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="11dca-122">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="11dca-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="11dca-123">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="11dca-124">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11dca-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="11dca-125">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="11dca-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="11dca-126">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="11dca-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="11dca-127">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="11dca-128">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="11dca-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="11dca-129">Krok 1 — odnajdywanie maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="11dca-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="11dca-130">tooensure wszelkie nową subskrypcję dodano toohello maszynach wirtualnych (VM) są identyfikowane przed zarejestrowaniem, uruchom proces wykrywania hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="11dca-131">kwerendy procesu Hello Azure hello listę maszyn wirtualnych w subskrypcji hello, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu.</span><span class="sxs-lookup"><span data-stu-id="11dca-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="11dca-132">Zaloguj się toohello [klasyczny portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="11dca-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="11dca-133">Na liście hello usług platformy Azure, kliknij **usług odzyskiwania** tooopen hello lista magazynów kopii zapasowych i odzyskiwania lokacji.</span><span class="sxs-lookup"><span data-stu-id="11dca-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="11dca-134">![Otwórz magazyn listy](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="11dca-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="11dca-135">Na liście hello magazyny kopii zapasowych wybierz tooback magazynu hello zapasowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="11dca-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="11dca-136">Jeśli jest to nowy portal hello magazynu otwiera toohello **Szybki Start** strony.</span><span class="sxs-lookup"><span data-stu-id="11dca-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Otwórz zarejestrowane elementy menu](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="11dca-138">Jeśli wcześniej skonfigurowano Magazyn hello, hello portal otwiera menu toohello ostatnio używane.</span><span class="sxs-lookup"><span data-stu-id="11dca-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="11dca-139">W menu magazynu hello (u góry hello hello strony), kliknij **zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="11dca-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Otwórz zarejestrowane elementy menu](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="11dca-141">Z hello **typu** menu, wybierz opcję **maszyny wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="11dca-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="11dca-143">Kliknij przycisk **ODNAJDOWANIA** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11dca-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="11dca-144">![Przycisk Odnajdź](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="11dca-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="11dca-145">Hello proces odnajdowania może zająć kilka minut hello maszyny wirtualne są wyszczególniane.</span><span class="sxs-lookup"><span data-stu-id="11dca-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="11dca-146">Brak powiadomienie u dołu hello ekranu hello, który informuje o tym, że proces hello jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="11dca-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Odnajdywanie maszyn wirtualnych](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="11dca-148">Witaj powiadomienie ulega zmianie po zakończeniu procesu hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="11dca-149">Jeśli proces odnajdywania hello nie znaleziono maszyn wirtualnych hello, najpierw upewnij się, że istnieje hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11dca-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="11dca-150">Jeśli istnieje hello maszyn wirtualnych, upewnij się, hello maszyny wirtualne są w hello sam region jako hello magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="11dca-151">Jeśli hello maszyn wirtualnych istnieją i są w tym samym regionie Witaj, upewnij się, że hello maszyny wirtualne nie są już zarejestrowane tooa magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="11dca-152">Jeśli maszyna wirtualna jest przypisany tooa magazynu kopii zapasowych nie jest magazynów kopii zapasowych tooother dostępne toobe przypisane.</span><span class="sxs-lookup"><span data-stu-id="11dca-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Odnajdywanie zostało zakończone](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="11dca-154">Po hello nowe elementy zostały odnalezione, przejdź tooStep 2 i zarejestruj maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="11dca-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="11dca-155">Krok 2 — rejestrowanie maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="11dca-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="11dca-156">Zarejestruj tooassociate maszyny wirtualnej platformy Azure za pomocą hello usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="11dca-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="11dca-157">Jest to zazwyczaj jednorazowe działania.</span><span class="sxs-lookup"><span data-stu-id="11dca-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="11dca-158">Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello portalu Azure, a następnie kliknij przycisk **zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="11dca-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="11dca-159">Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="11dca-161">Kliknij przycisk **ZAREJESTROWAĆ** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11dca-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="11dca-162">![Przycisk Zarejestruj](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="11dca-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="11dca-163">W hello **Zarejestruj elementy** menu skrótów, wybierz hello maszyn wirtualnych, które mają tooregister.</span><span class="sxs-lookup"><span data-stu-id="11dca-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="11dca-164">Jeśli istnieje co najmniej dwie maszyny wirtualne z hello takie same nazwy, użyj toodistinguish usługi chmury hello między nimi.</span><span class="sxs-lookup"><span data-stu-id="11dca-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="11dca-165">W tym samym czasie można zarejestrować wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11dca-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="11dca-166">Zadanie jest tworzone dla każdej maszyny wirtualnej, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="11dca-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="11dca-167">Kliknij przycisk **zadania** w hello powiadomień toogo toohello **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="11dca-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Rejestrowanie zadania](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="11dca-169">Maszyna wirtualna Hello pojawia się również hello liście zarejestrowanych elementów wraz ze stanu hello hello rejestracji operacji.</span><span class="sxs-lookup"><span data-stu-id="11dca-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Rejestrowanie — stan 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="11dca-171">Po zakończeniu operacji hello hello stan zmienia się tooreflect hello *zarejestrowany* stanu.</span><span class="sxs-lookup"><span data-stu-id="11dca-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Rejestrowanie — stan 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="11dca-173">Krok 3 — ochrona maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="11dca-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="11dca-174">Teraz można skonfigurować zasady tworzenia kopii zapasowej i przechowywania hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="11dca-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="11dca-175">Wiele maszyn wirtualnych mogą być chronione przy użyciu pojedynczej chronić akcji.</span><span class="sxs-lookup"><span data-stu-id="11dca-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="11dca-176">Azure magazyny kopii zapasowych utworzonych po 2015 może pochodzić z domyślnych zasad wbudowany w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="11dca-177">Ta zasada domyślna zawiera zachowanie domyślne, 30 dni i harmonogram tworzenia kopii zapasowych raz dziennie.</span><span class="sxs-lookup"><span data-stu-id="11dca-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="11dca-178">Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello portalu Azure, a następnie kliknij przycisk **zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="11dca-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="11dca-179">Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Wybieranie obciążenia w portalu](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="11dca-181">Kliknij przycisk **Chroń** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11dca-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="11dca-182">Witaj **Kreator ochrony elementów** pojawi się.</span><span class="sxs-lookup"><span data-stu-id="11dca-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="11dca-183">Kreator Hello wyświetla tylko maszyny wirtualne, które są zarejestrowane i nie są chronione.</span><span class="sxs-lookup"><span data-stu-id="11dca-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="11dca-184">Wybierz hello maszyn wirtualnych, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="11dca-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="11dca-185">Jeśli istnieje co najmniej dwie maszyny wirtualne z hello takie same nazwy, użyj toodistinguish usługi chmury hello między maszynami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="11dca-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="11dca-186">Można chronić wiele maszyn wirtualnych w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="11dca-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Konfigurowanie ochrony w dużej skali](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="11dca-188">Wybierz **harmonogram tworzenia kopii zapasowych** tooback zapasowych hello maszyn wirtualnych, które zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="11dca-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="11dca-189">Można wybierać z istniejącego zestawu zasad lub zdefiniuj nowy.</span><span class="sxs-lookup"><span data-stu-id="11dca-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="11dca-190">Z jednymi zasadami tworzenia kopii zapasowych może być skojarzonych wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11dca-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="11dca-191">Jednak hello maszyny wirtualnej może być skojarzony tylko z jedną zasadę na dowolnym etapie w czasie.</span><span class="sxs-lookup"><span data-stu-id="11dca-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Ochrona za pomocą nowych zasad](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="11dca-193">Zasady tworzenia kopii zapasowych obejmują schemat przechowywania hello zaplanowanych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="11dca-194">W przypadku wybrania istniejących zasad tworzenia kopii zapasowej nie można zmodyfikować opcje przechowywania hello w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="11dca-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="11dca-195">Wybierz **zakres przechowywania** tooassociate z hello kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="11dca-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Chroń za pomocą elastycznych przechowywania](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="11dca-197">Zasady przechowywania określa hello czas przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="11dca-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="11dca-198">Można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="11dca-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="11dca-199">Na przykład punktu kopii zapasowej pobierane raz dziennie (która służy jako punkt odzyskiwania operacyjne) mogą zostać zachowane przez 90 dni.</span><span class="sxs-lookup"><span data-stu-id="11dca-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="11dca-200">Z kolei toobe przechowywane przez wiele miesięcy lub lat. może być konieczne punktu kopii zapasowej wykonywaną na końcu hello co kwartał (na potrzeby inspekcji).</span><span class="sxs-lookup"><span data-stu-id="11dca-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="11dca-202">W tym obrazie przykładzie:</span><span class="sxs-lookup"><span data-stu-id="11dca-202">In this example image:</span></span>

   * <span data-ttu-id="11dca-203">**Zasady przechowywania codziennych**: kopii zapasowych wykonanych codziennie są przechowywane przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="11dca-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="11dca-204">**Co tydzień zasady przechowywania**: kopii zapasowych wykonanych co tydzień w niedzielę zostaną zachowane w celu 104 tygodni.</span><span class="sxs-lookup"><span data-stu-id="11dca-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="11dca-205">**Miesięczne zasady przechowywania**: kopie zapasowe wykonane w hello niedziela ostatniego dnia każdego miesiąca są zachowywane przez 120 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="11dca-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="11dca-206">**Zasady przechowywania corocznych**: kopie zapasowe wykonane w hello Pierwsza niedziela co stycznia zostaną zachowane w celu 99 lat.</span><span class="sxs-lookup"><span data-stu-id="11dca-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="11dca-207">Zadanie tworzenia zasad ochrony hello tooconfigure i skojarz hello maszyn wirtualnych toothat zasad dla każdej maszyny wirtualnej, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="11dca-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="11dca-208">Lista hello tooview **konfiguracji ochrony** zadań, z menu magazynów hello, kliknij przycisk **zadania** i wybierz **konfiguracji ochrony** z hello **operacji**  filtru.</span><span class="sxs-lookup"><span data-stu-id="11dca-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Zadanie konfigurowania ochrony](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="11dca-210">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="11dca-210">Initial backup</span></span>
<span data-ttu-id="11dca-211">Gdy maszyna wirtualna hello jest chroniona za pomocą zasad, jest wyświetlane w obszarze hello **chronione elementy** kartę ze stanem hello *chroniona — (oczekiwanie początkowa kopia zapasowa)*.</span><span class="sxs-lookup"><span data-stu-id="11dca-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="11dca-212">Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello *początkowa kopia zapasowa*.</span><span class="sxs-lookup"><span data-stu-id="11dca-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="11dca-213">tootrigger hello tworzenia początkowej kopii zapasowej natychmiast po skonfigurowaniu ochrony:</span><span class="sxs-lookup"><span data-stu-id="11dca-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="11dca-214">U dołu hello hello **chronione elementy** kliknij przycisk **Utwórz kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="11dca-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="11dca-215">Hello usługi Azure Backup tworzy zadanie tworzenia kopii zapasowej hello początkowej operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="11dca-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="11dca-216">Kliknij przycisk hello **zadania** kartę tooview hello listy zadań.</span><span class="sxs-lookup"><span data-stu-id="11dca-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Tworzenie kopii zapasowej w toku](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="11dca-218">Podczas operacji tworzenia kopii zapasowej hello hello usługi Kopia zapasowa Azure problemy z rozszerzeniem kopii zapasowej polecenia toohello w każdej tooflush maszyny wirtualnej, wszystkie zadania zapisu i migawki spójne.</span><span class="sxs-lookup"><span data-stu-id="11dca-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="11dca-219">Po zakończeniu tworzenia początkowej kopii zapasowej hello, stan hello hello maszyny wirtualnej w hello **chronione elementy** jest karta *chronione*.</span><span class="sxs-lookup"><span data-stu-id="11dca-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="11dca-221">Wyświetlanie stanu kopii zapasowej i szczegóły</span><span class="sxs-lookup"><span data-stu-id="11dca-221">Viewing backup status and details</span></span>
<span data-ttu-id="11dca-222">Gdy chroniony, liczba maszyn wirtualnych hello również wzrost hello **pulpitu nawigacyjnego** strony podsumowania.</span><span class="sxs-lookup"><span data-stu-id="11dca-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="11dca-223">Hello **pulpitu nawigacyjnego** strona zawiera również hello numer zadania z ostatnich 24 godzin, które były hello *pomyślnie*, ma *nie powiodło się*i są *w toku*.</span><span class="sxs-lookup"><span data-stu-id="11dca-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="11dca-224">Na powitania **zadania** Użyj hello **stan**, **operacji**, lub **z** i **do** toofilter menu Witaj zadania.</span><span class="sxs-lookup"><span data-stu-id="11dca-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Stan tworzenia kopii zapasowej na stronie pulpitu nawigacyjnego](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="11dca-226">Wartości na pulpicie nawigacyjnym hello są odświeżane co 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="11dca-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="11dca-227">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="11dca-227">Troubleshooting errors</span></span>
<span data-ttu-id="11dca-228">Jeśli wystąpiły problemy podczas tworzenia kopii zapasowej maszyny wirtualnej przyjrzeć się hello [maszyny Wirtualnej artykuł dotyczący rozwiązywania problemów](backup-azure-vms-troubleshoot.md) Aby uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="11dca-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11dca-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11dca-229">Next steps</span></span>
* [<span data-ttu-id="11dca-230">Monitorowanie maszyn wirtualnych i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="11dca-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="11dca-231">Przywracanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="11dca-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
