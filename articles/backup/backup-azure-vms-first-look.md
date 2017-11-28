---
title: "Pierwsze spojrzenie — tworzenie kopii zapasowej maszyn wirtualnych platformy Azure przy użyciu magazynu kopii zapasowych | Microsoft Docs"
description: "Użyj portalu klasycznego do tworzenia kopii zapasowych maszyn wirtualnych platformy Azure w magazynie kopii zapasowych. W tym samouczku wyjaśniono wszystkie etapy, m.in. tworzenie magazynu kopii zapasowych, rejestrowanie maszyn wirtualnych, tworzenie zasad kopii zapasowych i uruchamianie początkowego zadania tworzenia kopii zapasowej."
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
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="c905c-104">Pierwsze spojrzenie: tworzenie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c905c-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c905c-105">Ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="c905c-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="c905c-106">Ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Backup</span><span class="sxs-lookup"><span data-stu-id="c905c-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="c905c-107">Ten samouczek przedstawia kroki tworzenia kopii zapasowej maszyny wirtualnej platformy Azure w magazynie usługi Backup na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c905c-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="c905c-108">W tym artykule opisano klasyczny model wdrażania (model wdrażania Service Manager) na potrzeby tworzenia kopii zapasowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c905c-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="c905c-109">Poniższa procedura dotyczy tylko magazynów kopii zapasowych tworzonych w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="c905c-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="c905c-110">W przypadku nowych wdrożeń firma Microsoft zaleca używanie modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c905c-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="c905c-111">Jeśli chcesz tworzyć kopie zapasowe maszyny wirtualnej w magazynie usługi Recovery Services należącym do grupy zasobów, zobacz [Pierwsze spojrzenie: ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c905c-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="c905c-112">Do pomyślnego ukończenia tego samouczka muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="c905c-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="c905c-113">Utworzona została maszyna wirtualna w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c905c-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="c905c-114">Maszyna wirtualna ma łączność z publicznymi adresami IP platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c905c-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="c905c-115">Aby uzyskać więcej informacji, zobacz [Network connectivity](backup-azure-vms-prepare.md#network-connectivity) (Łączność sieciowa).</span><span class="sxs-lookup"><span data-stu-id="c905c-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="c905c-116">Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c905c-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c905c-117">Ten samouczek jest przeznaczony dla maszyn wirtualnych utworzonych w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="c905c-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="c905c-118">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="c905c-118">Create a backup vault</span></span>
<span data-ttu-id="c905c-119">Magazyn kopii zapasowych to jednostka, w której przechowywane są wszystkie kopie zapasowe i punkty odzyskiwania, które zostały utworzone na przestrzeni czasu.</span><span class="sxs-lookup"><span data-stu-id="c905c-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="c905c-120">Magazyn kopii zapasowych zawiera również zasady tworzenia kopii zapasowych stosowane względem maszyn wirtualnych, których kopie zapasowe są tworzone.</span><span class="sxs-lookup"><span data-stu-id="c905c-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c905c-121">Począwszy od marca 2017 r. nie można już tworzyć magazynów kopii zapasowych za pomocą klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="c905c-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="c905c-122">Magazyny kopii zapasowych możesz uaktualnić do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="c905c-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="c905c-123">Więcej szczegółów znajduje się w artykule [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Uaktualnianie magazynu kopii zapasowych do magazynu usługi Recovery Services).</span><span class="sxs-lookup"><span data-stu-id="c905c-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="c905c-124">Firma Microsoft zachęca do przeprowadzenia uaktualnienia magazynów kopii zapasowych do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="c905c-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="c905c-125">Po 15 października 2017 r. nie będzie można tworzyć magazynów kopii zapasowych za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c905c-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="c905c-126">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="c905c-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="c905c-127">Wszystkie pozostałe magazyny kopii zapasowych zostaną automatycznie uaktualnione do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="c905c-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="c905c-128">Nie będzie możliwe uzyskanie dostępu do danych kopii zapasowych w portalu klasycznym.</span><span class="sxs-lookup"><span data-stu-id="c905c-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="c905c-129">Zamiast tego należy użyć witryny Azure Portal, aby uzyskać dostęp do danych kopii zapasowych w magazynach usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="c905c-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="c905c-130">Odnajdywanie i rejestrowanie maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c905c-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="c905c-131">Przed zarejestrowaniem maszyny wirtualnej w magazynie uruchom proces wykrywania, aby zidentyfikować wszelkie nowe maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c905c-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="c905c-132">Proces ten zwraca listę maszyn wirtualnych w ramach subskrypcji wraz z dodatkowymi informacjami, takimi jak nazwa usługi w chmurze i region.</span><span class="sxs-lookup"><span data-stu-id="c905c-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="c905c-133">Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c905c-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="c905c-134">W klasycznym portalu Azure kliknij pozycję **Usługi odzyskiwania**, aby otworzyć listę magazynów Usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c905c-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="c905c-135">![Wybór obciążenia](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="c905c-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="c905c-136">Z listy magazynów wybierz magazyn, w którym zostanie utworzona kopia zapasowa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c905c-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="c905c-137">Po wybraniu magazyn zostanie otwarty na stronie **Szybki start**.</span><span class="sxs-lookup"><span data-stu-id="c905c-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="c905c-138">W menu magazynu kliknij pozycję **Zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="c905c-138">From the vault menu, click **Registered Items**.</span></span>

    ![Wybieranie obciążenia](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="c905c-140">Z menu **Typ** wybierz polecenie **Maszyna wirtualna platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="c905c-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Wybór obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="c905c-142">Kliknij pozycję **ODNAJDŹ** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="c905c-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="c905c-143">![Przycisk Odnajdź](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="c905c-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="c905c-144">Proces odnajdywania może zająć kilka minut, gdy maszyny wirtualne są wyszczególniane.</span><span class="sxs-lookup"><span data-stu-id="c905c-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="c905c-145">W dolnej części ekranu znajduje się powiadomienie informujące, że proces jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="c905c-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Odnajdywanie maszyn wirtualnych](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="c905c-147">Powiadomienie ulega zmianie, gdy proces zostanie zakończony.</span><span class="sxs-lookup"><span data-stu-id="c905c-147">The notification changes when the process is complete.</span></span>

    ![Odnajdywanie zostało zakończone](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="c905c-149">Kliknij pozycję **ZAREJESTRUJ** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="c905c-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="c905c-150">![Przycisk Zarejestruj](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="c905c-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="c905c-151">W menu skrótów **Zarejestruj elementy** wybierz maszyny wirtualne, które chcesz zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="c905c-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="c905c-152">W tym samym czasie można zarejestrować wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c905c-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="c905c-153">Zadanie jest tworzone dla każdej maszyny wirtualnej, która zostanie wybrana.</span><span class="sxs-lookup"><span data-stu-id="c905c-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="c905c-154">W powiadomieniu kliknij pozycję **Wyświetl zadanie**, aby przejść do strony **Zadania**.</span><span class="sxs-lookup"><span data-stu-id="c905c-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Rejestrowanie zadania](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="c905c-156">Maszyna wirtualna pojawia się również na liście zarejestrowanych elementów wraz ze stanem operacji rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="c905c-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Rejestrowanie — stan 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="c905c-158">Po zakończeniu operacji stan zostanie zmieniony w celu odzwierciedlenia stanu oznaczającego *zarejestrowanie*.</span><span class="sxs-lookup"><span data-stu-id="c905c-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Rejestrowanie — stan 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="c905c-160">Instalowanie agenta maszyny wirtualnej na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c905c-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="c905c-161">Aby rozszerzenie usługi Backup mogło działać, na maszynie wirtualnej Azure musi być zainstalowany agent maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c905c-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="c905c-162">Jeśli maszyna wirtualna została utworzona z poziomu galerii Azure, agent maszyny wirtualnej znajduje się już na maszynie wirtualnej. Możesz przejść do sekcji związanej z [ochroną maszyn wirtualnych](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="c905c-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="c905c-163">Jeśli Twoja maszyna wirtualna została zmigrowana z lokalnego centrum danych, to prawdopodobnie nie ma na niej zainstalowanego agenta maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c905c-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="c905c-164">Konieczne jest zainstalowanie agenta maszyny wirtualnej na maszynie wirtualnej zanim możliwe będzie chronienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c905c-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="c905c-165">Aby uzyskać szczegółowy opis kroków instalowania agenta maszyny wirtualnej, zobacz [sekcję VM Agent (Agent maszyny wirtualnej) w artykule dotyczącym tworzenia kopii zapasowych maszyn wirtualnych](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="c905c-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="c905c-166">Tworzenie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="c905c-166">Create the backup policy</span></span>
<span data-ttu-id="c905c-167">Przed wyzwoleniem zadania tworzenia początkowej kopii zapasowej ustaw harmonogram tworzenia migawek kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c905c-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="c905c-168">Zasady tworzenia kopii zapasowej określają harmonogram tworzenia migawek kopii zapasowych oraz okres, przez który te migawki są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="c905c-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="c905c-169">Informacje dotyczące przechowywania są oparte na schemacie rotacji kopii zapasowej dziadek-ojciec-syn.</span><span class="sxs-lookup"><span data-stu-id="c905c-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="c905c-170">Przejdź do magazynu kopii zapasowych w obszarze **Usługi odzyskiwania** klasycznego portalu Azure, a następnie kliknij pozycję **Zarejestrowane elementy**.</span><span class="sxs-lookup"><span data-stu-id="c905c-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="c905c-171">Z menu rozwijanego wybierz pozycję **Maszyna wirtualna platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="c905c-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Wybieranie obciążenia w portalu](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="c905c-173">Kliknij pozycję **CHROŃ** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="c905c-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="c905c-174">![Klikanie pozycji Chroń](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="c905c-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="c905c-175">Zostanie wyświetlony **kreator ochrony elementów** i zostanie wyświetlona lista *tylko* tych maszyn wirtualnych, które są zarejestrowane i nie są chronione.</span><span class="sxs-lookup"><span data-stu-id="c905c-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Konfigurowanie ochrony w dużej skali](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="c905c-177">Wybierz maszyny wirtualne, które chcesz chronić.</span><span class="sxs-lookup"><span data-stu-id="c905c-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="c905c-178">Jeśli istnieje więcej niż jedna maszyna wirtualna o tej samej nazwie, użyj usługi Cloud Services w celu rozróżnienia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c905c-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="c905c-179">W menu **Konfigurowanie ochrony** wybierz istniejące zasady lub utwórz nowe zasady w celu ochrony zidentyfikowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c905c-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="c905c-180">Z nowymi magazynami kopii zapasowych są skojarzone zasady domyślne.</span><span class="sxs-lookup"><span data-stu-id="c905c-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="c905c-181">Te zasady określają tworzenie każdego wieczoru codziennych migawek, które są przechowywane przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="c905c-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="c905c-182">Z jednymi zasadami tworzenia kopii zapasowych może być skojarzonych wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c905c-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="c905c-183">Maszyna wirtualna może być jednak jednocześnie skojarzona tylko z jednymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="c905c-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Ochrona za pomocą nowych zasad](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="c905c-185">Zasady tworzenia kopii zapasowych obejmują schemat przechowywania dla zaplanowanych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c905c-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="c905c-186">W przypadku wybrania istniejących zasad tworzenia kopii zapasowych w następnym kroku nie będzie możliwe zmodyfikowanie opcji przechowywania.</span><span class="sxs-lookup"><span data-stu-id="c905c-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="c905c-187">W polu **Zakres przechowywania** zdefiniuj codzienny, cotygodniowy, comiesięczny i coroczny zakres dla określonych punktów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c905c-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="c905c-189">Zasady przechowywania określają czas przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c905c-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="c905c-190">Możliwe jest określenie różnych zasad przechowywania na podstawie czasu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c905c-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="c905c-191">Kliknij pozycję **Zadania**, aby wyświetlić listę zadań **Konfiguracja ochrony**.</span><span class="sxs-lookup"><span data-stu-id="c905c-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Zadanie konfigurowania ochrony](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="c905c-193">Po ustanowieniu zasad przejdź do następnego kroku i uruchom tworzenie początkowej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c905c-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="c905c-194">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="c905c-194">Initial backup</span></span>
<span data-ttu-id="c905c-195">Gdy zostanie ustawiona ochrona maszyny wirtualnej za pomocą zasad, można wyświetlić tę relację na karcie **Chronione elementy**. Dopóki nie zostanie utworzona początkowa kopia zapasowa, pole **Stan ochrony** będzie miało wartość **Chroniona — (oczekiwanie na początkową kopię zapasową)**.</span><span class="sxs-lookup"><span data-stu-id="c905c-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="c905c-196">Domyślnie pierwszą zaplanowaną kopią zapasową jest *początkowa kopia zapasowa*.</span><span class="sxs-lookup"><span data-stu-id="c905c-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="c905c-198">Aby uruchomić proces tworzenia początkowej kopii zapasowej natychmiast:</span><span class="sxs-lookup"><span data-stu-id="c905c-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="c905c-199">Na stronie **Chronione elementy** kliknij pozycję **Utwórz kopię zapasową teraz** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="c905c-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="c905c-200">![Ikona Utwórz kopię zapasową teraz](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="c905c-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="c905c-201">Usługa Azure Backup tworzy zadanie dla operacji tworzenia początkowej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c905c-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="c905c-202">Kliknij kartę **Zadania**, aby wyświetlić listę zadań.</span><span class="sxs-lookup"><span data-stu-id="c905c-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Tworzenie kopii zapasowej w toku](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="c905c-204">Po zakończeniu tworzenia początkowej kopii zapasowej stan maszyny wirtualnej na karcie **Chronione elementy** ma wartość *Chroniona*.</span><span class="sxs-lookup"><span data-stu-id="c905c-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="c905c-206">Tworzenie kopii zapasowych maszyn wirtualnych jest procesem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c905c-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="c905c-207">Nie można tworzyć kopii zapasowych maszyn wirtualnych z jednego regionu w magazynie kopii zapasowych znajdującym się w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="c905c-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="c905c-208">W związku z tym w każdym regionie Azure, dla którego mają zostać utworzone kopie zapasowe maszyn wirtualnych, należy utworzyć co najmniej jeden magazyn kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c905c-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="c905c-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c905c-209">Next steps</span></span>
<span data-ttu-id="c905c-210">Po pomyślnym utworzeniu kopii zapasowej maszyny wirtualnej można wykonać jeden z kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="c905c-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="c905c-211">Najbardziej logicznym krokiem jest zapoznanie się z przywracaniem danych do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c905c-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="c905c-212">Istnieją jednak również zadania zarządzania, które ułatwią zrozumienie sposobu zapewniania bezpieczeństwa danych i ograniczania kosztów.</span><span class="sxs-lookup"><span data-stu-id="c905c-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="c905c-213">Monitorowanie maszyn wirtualnych i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="c905c-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="c905c-214">Przywracanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c905c-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="c905c-215">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="c905c-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="c905c-216">Pytania?</span><span class="sxs-lookup"><span data-stu-id="c905c-216">Questions?</span></span>
<span data-ttu-id="c905c-217">Jeśli masz pytania lub jeśli brakuje Ci jakiejś funkcji, [prześlij nam opinię](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="c905c-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
