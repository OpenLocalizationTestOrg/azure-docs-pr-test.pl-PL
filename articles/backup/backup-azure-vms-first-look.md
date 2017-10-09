---
title: "Pierwsze spojrzenie — tworzenie kopii zapasowej maszyn wirtualnych platformy Azure przy użyciu magazynu kopii zapasowych | Microsoft Docs"
description: "Użyj klasycznego portalu tooback hello zapasowej magazyn kopii zapasowych tooa maszynach wirtualnych platformy Azure. W tym samouczku opisano wszystkich faz, w tym tworzenie magazynu kopii zapasowych hello, rejestrowanie hello maszyn wirtualnych, tworzenia zasad tworzenia kopii zapasowej i uruchamianie hello początkowej zadanie tworzenia kopii zapasowej."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="a6fba-104">Pierwsze spojrzenie: tworzenie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a6fba-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6fba-105">Ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a6fba-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="a6fba-106">Ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Backup</span><span class="sxs-lookup"><span data-stu-id="a6fba-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="a6fba-107">Ten samouczek przedstawia kroki hello tworzenia kopii zapasowej maszyny wirtualnej platformy Azure (VM) tooa magazynu kopii zapasowych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a6fba-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="a6fba-108">W tym artykule opisano hello klasycznego modelu lub model wdrażania programu Service Manager, tworzenie kopii zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="a6fba-109">Witaj poniższe kroki mają zastosowanie tylko tooBackup magazynów utworzone w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="a6fba-110">Firma Microsoft zaleca używanie hello modelu Menedżera zasobów dla nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="a6fba-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="a6fba-111">Jeśli interesuje Cię w tworzeniu kopii zapasowych w magazynie usług odzyskiwania tooa maszyny Wirtualnej należy tooa grupy zasobów, zobacz [Pierwsze spojrzenie: ochrona maszyn wirtualnych z magazynu usług odzyskiwania](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a6fba-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="a6fba-112">toosuccessfully wykonaj następujące czynności hello samouczek, musi istnieć te wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="a6fba-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="a6fba-113">Utworzona została maszyna wirtualna w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6fba-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="a6fba-114">Hello maszyna wirtualna ma łączność tooAzure publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a6fba-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="a6fba-115">Aby uzyskać więcej informacji, zobacz [Network connectivity](backup-azure-vms-prepare.md#network-connectivity) (Łączność sieciowa).</span><span class="sxs-lookup"><span data-stu-id="a6fba-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="a6fba-116">Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6fba-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a6fba-117">W tym samouczku jest przeznaczona do użytku z maszyn wirtualnych utworzonych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="a6fba-118">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="a6fba-118">Create a backup vault</span></span>
<span data-ttu-id="a6fba-119">Magazyn kopii zapasowych to jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, które zostały utworzone w czasie.</span><span class="sxs-lookup"><span data-stu-id="a6fba-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="a6fba-120">Witaj magazynu kopii zapasowych zawiera również hello zasad tworzenia kopii zapasowej, które są toohello zastosowane maszyn wirtualnych, których powstaje kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="a6fba-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6fba-121">Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="a6fba-122">Można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="a6fba-123">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="a6fba-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="a6fba-124">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="a6fba-125">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6fba-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="a6fba-126">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="a6fba-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="a6fba-127">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="a6fba-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="a6fba-128">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="a6fba-129">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a6fba-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="a6fba-130">Odnajdywanie i rejestrowanie maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a6fba-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="a6fba-131">Przed zarejestrowaniem hello maszyny Wirtualnej w magazynie, uruchom tooidentify procesu odnajdywania hello wszelkie nowe maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="a6fba-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="a6fba-132">Zwraca listę maszyn wirtualnych hello subskrypcji, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu.</span><span class="sxs-lookup"><span data-stu-id="a6fba-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="a6fba-133">Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="a6fba-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="a6fba-134">W hello klasycznego portalu Azure, kliknij przycisk **usług odzyskiwania** tooopen hello listę magazynów usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a6fba-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="a6fba-135">![Wybór obciążenia](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="a6fba-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="a6fba-136">Z listy hello magazynów wybierz tooback magazynu hello zapasowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="a6fba-137">Po wybraniu magazyn zostanie otwarty w hello **Szybki Start** strony</span><span class="sxs-lookup"><span data-stu-id="a6fba-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="a6fba-138">W menu magazynu powitania kliknij **zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Wybieranie obciążenia](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="a6fba-140">Z hello **typu** menu, wybierz opcję **maszyny wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="a6fba-142">Kliknij przycisk **ODNAJDOWANIA** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="a6fba-143">![Przycisk Odnajdź](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="a6fba-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="a6fba-144">Hello proces odnajdowania może zająć kilka minut hello maszyny wirtualne są wyszczególniane.</span><span class="sxs-lookup"><span data-stu-id="a6fba-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="a6fba-145">Brak powiadomienie u dołu hello ekranu hello, który informuje o tym, że proces hello jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Odnajdywanie maszyn wirtualnych](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="a6fba-147">Witaj powiadomienie ulega zmianie po zakończeniu procesu hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-147">hello notification changes when hello process is complete.</span></span>

    ![Odnajdywanie zostało zakończone](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="a6fba-149">Kliknij przycisk **ZAREJESTROWAĆ** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="a6fba-150">![Przycisk Zarejestruj](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="a6fba-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="a6fba-151">W hello **Zarejestruj elementy** menu skrótów, wybierz hello maszyn wirtualnych, które mają tooregister.</span><span class="sxs-lookup"><span data-stu-id="a6fba-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="a6fba-152">W tym samym czasie można zarejestrować wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="a6fba-153">Zadanie jest tworzone dla każdej maszyny wirtualnej, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="a6fba-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="a6fba-154">Kliknij przycisk **zadania** w hello powiadomień toogo toohello **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Rejestrowanie zadania](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="a6fba-156">Maszyna wirtualna Hello pojawia się również hello liście zarejestrowanych elementów wraz ze stanu hello hello rejestracji operacji.</span><span class="sxs-lookup"><span data-stu-id="a6fba-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Rejestrowanie — stan 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="a6fba-158">Po zakończeniu operacji hello hello stan zmienia się tooreflect hello *zarejestrowany* stanu.</span><span class="sxs-lookup"><span data-stu-id="a6fba-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Rejestrowanie — stan 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="a6fba-160">Zainstaluj hello agenta maszyny Wirtualnej na maszynie wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="a6fba-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="a6fba-161">Witaj Agent maszyny Wirtualnej musi być zainstalowany na powitania maszyny wirtualnej platformy Azure dla hello kopii zapasowej rozszerzenia toowork.</span><span class="sxs-lookup"><span data-stu-id="a6fba-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="a6fba-162">Jeśli maszyna wirtualna została utworzona z hello galerii Azure, hello agenta maszyny Wirtualnej jest już obecny na powitania wirtualna; można pominąć zbyt[ochroną maszyn wirtualnych](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="a6fba-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="a6fba-163">Migracji maszyny Wirtualnej z lokalnego centrum danych, hello wirtualna prawdopodobnie nie ma hello zainstalowanego agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="a6fba-164">Hello agenta maszyny Wirtualnej należy zainstalować na maszynie wirtualnej hello przed kontynuowaniem tooprotect hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="a6fba-165">Aby uzyskać szczegółowe instrukcje dotyczące instalowania hello agenta maszyny Wirtualnej, zobacz hello [sekcję VM Agent hello kopii zapasowych maszyn wirtualnych artykułu](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="a6fba-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="a6fba-166">Tworzenie zasad tworzenia kopii zapasowej hello</span><span class="sxs-lookup"><span data-stu-id="a6fba-166">Create hello backup policy</span></span>
<span data-ttu-id="a6fba-167">Przed wyzwoleniem hello początkowej zadanie tworzenia kopii zapasowej Ustaw harmonogram hello, gdy migawek kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="a6fba-168">Witaj Zaplanuj, kiedy migawek kopii zapasowych są pobierane i hello czas te migawki są przechowywane, jest hello zasad tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="a6fba-169">informacje dotyczące przechowywania Hello jest oparty na schemacie rotacji kopii zapasowej dziadek ojciec syn..</span><span class="sxs-lookup"><span data-stu-id="a6fba-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="a6fba-170">Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello klasycznego portalu Azure i kliknij przycisk **zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="a6fba-171">Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Wybieranie obciążenia w portalu](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="a6fba-173">Kliknij przycisk **Chroń** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="a6fba-174">![Klikanie pozycji Chroń](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="a6fba-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="a6fba-175">Witaj **Kreator ochrony elementów** i zostanie wyświetlona lista *tylko* maszyn wirtualnych, które są zarejestrowane i nie są chronione.</span><span class="sxs-lookup"><span data-stu-id="a6fba-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Konfigurowanie ochrony w dużej skali](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="a6fba-177">Wybierz hello maszyn wirtualnych, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="a6fba-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="a6fba-178">Jeśli istnieją dwa lub więcej maszyn wirtualnych z hello takie same nazwy, użyj hello toodistinguish usługi w chmurze między maszynami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="a6fba-179">Na powitania **skonfiguruj ochronę** menu Wybierz istniejące zasady lub Utwórz nowy tooprotect zasad zidentyfikowanych maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="a6fba-180">Nowe magazynami kopii zapasowych są skojarzone z magazynem hello zasady domyślne.</span><span class="sxs-lookup"><span data-stu-id="a6fba-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="a6fba-181">Ta zasada ma dziennym określają tworzenie każdego wieczoru i hello dziennej migawki są przechowywane przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="a6fba-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="a6fba-182">Z jednymi zasadami tworzenia kopii zapasowych może być skojarzonych wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="a6fba-183">Jednak hello maszyny wirtualnej można skojarzyć tylko z jednymi zasadami naraz.</span><span class="sxs-lookup"><span data-stu-id="a6fba-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Ochrona za pomocą nowych zasad](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="a6fba-185">Zasady tworzenia kopii zapasowych obejmują schemat przechowywania hello zaplanowanych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="a6fba-186">W przypadku wybrania istniejących zasad tworzenia kopii zapasowej będzie opcje przechowywania hello toomodify w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="a6fba-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="a6fba-187">Na **zakres przechowywania** zdefiniuj hello codziennie, co tydzień, miesięcznych i rocznych zakres hello określonych punktów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="a6fba-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="a6fba-189">Zasady przechowywania określa hello czas przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="a6fba-190">Można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="a6fba-191">Kliknij przycisk **zadania** tooview hello lista **konfiguracji ochrony** zadania.</span><span class="sxs-lookup"><span data-stu-id="a6fba-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Zadanie konfigurowania ochrony](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="a6fba-193">Po ustanowieniu zasad hello, przejdź do następnego kroku toohello i uruchom tworzenie początkowej kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="a6fba-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="a6fba-194">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="a6fba-194">Initial backup</span></span>
<span data-ttu-id="a6fba-195">Po chronionej maszyny wirtualnej za pomocą zasad można wyświetlić tę relację na powitania **chronione elementy** kartę. Dopóki hello utworzona początkowa kopia zapasowa, hello **stanu ochrony** jest pokazywana jako **chroniona — (oczekiwanie początkowa kopia zapasowa)**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="a6fba-196">Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello *początkowa kopia zapasowa*.</span><span class="sxs-lookup"><span data-stu-id="a6fba-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="a6fba-198">toostart hello początkową kopię zapasową teraz:</span><span class="sxs-lookup"><span data-stu-id="a6fba-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="a6fba-199">Na powitania **chronione elementy** kliknij przycisk **Utwórz kopię zapasową teraz** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a6fba-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="a6fba-200">![Ikona Utwórz kopię zapasową teraz](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="a6fba-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="a6fba-201">Hello usługi Azure Backup tworzy zadanie tworzenia kopii zapasowej hello początkowej operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="a6fba-202">Kliknij przycisk hello **zadania** kartę tooview hello listy zadań.</span><span class="sxs-lookup"><span data-stu-id="a6fba-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Tworzenie kopii zapasowej w toku](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="a6fba-204">Po zakończeniu tworzenia początkowej kopii zapasowej, stan hello hello maszyny wirtualnej w hello **chronione elementy** jest karta *chronione*.</span><span class="sxs-lookup"><span data-stu-id="a6fba-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="a6fba-206">Tworzenie kopii zapasowych maszyn wirtualnych jest procesem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="a6fba-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="a6fba-207">Nie można utworzyć kopii zapasowych maszyn wirtualnych z jednego regionu tooa magazynu kopii zapasowych w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="a6fba-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="a6fba-208">Tak dla każdego regionu Azure, który ma maszyn wirtualnych, które wymagają toobe kopii zapasowej, co najmniej jeden magazyn kopii zapasowych należy utworzyć w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="a6fba-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="a6fba-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6fba-209">Next steps</span></span>
<span data-ttu-id="a6fba-210">Po pomyślnym utworzeniu kopii zapasowej maszyny wirtualnej można wykonać jeden z kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="a6fba-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="a6fba-211">najbardziej logicznym krokiem Hello jest toofamiliarize sobie z przywracaniem danych tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a6fba-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="a6fba-212">Istnieją jednak zadań zarządzania, które ułatwią zrozumienie sposobu tookeep bezpiecznych danych i ograniczania kosztów.</span><span class="sxs-lookup"><span data-stu-id="a6fba-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="a6fba-213">Monitorowanie maszyn wirtualnych i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="a6fba-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="a6fba-214">Przywracanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="a6fba-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="a6fba-215">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="a6fba-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="a6fba-216">Pytania?</span><span class="sxs-lookup"><span data-stu-id="a6fba-216">Questions?</span></span>
<span data-ttu-id="a6fba-217">Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="a6fba-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
