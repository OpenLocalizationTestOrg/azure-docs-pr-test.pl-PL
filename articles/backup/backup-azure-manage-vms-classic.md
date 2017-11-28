---
title: monitor i aaaManage kopii zapasowych maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak monitor wirtualnej platformy Azure i toomanage komputera kopii zapasowych"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="c8a26-103">Zarządzanie typowych zadań kopia zapasowa Azure i alerty wyzwalacza w portalu klasycznym hello</span><span class="sxs-lookup"><span data-stu-id="c8a26-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8a26-104">Zarządzanie kopiami zapasowymi maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="c8a26-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="c8a26-105">Zarządzanie kopiami zapasowymi klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c8a26-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="c8a26-106">Ten artykuł zawiera informacje o wspólnego zarządzania i monitorowania zadań związanych z klasycznego modelu maszyny wirtualne chronione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a26-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="c8a26-107">Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c8a26-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c8a26-108">Zobacz [przygotowanie Twojego środowiska tooback zapasowych maszyn wirtualnych Azure](backup-azure-vms-prepare.md) szczegółowe informacje na temat pracy z Classic deployment model maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c8a26-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="c8a26-109">Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="c8a26-110">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c8a26-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="c8a26-111">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="c8a26-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="c8a26-112">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c8a26-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="c8a26-113">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8a26-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="c8a26-114">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="c8a26-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="c8a26-115">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="c8a26-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="c8a26-116">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="c8a26-117">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c8a26-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="c8a26-118">Zarządzanie chronione maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c8a26-118">Manage protected virtual machines</span></span>
<span data-ttu-id="c8a26-119">toomanage chronione maszyny wirtualne:</span><span class="sxs-lookup"><span data-stu-id="c8a26-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="c8a26-120">tooview i zarządzanie nimi ustawienia kopii zapasowej dla maszyny wirtualnej kliknij hello **chronione elementy** kartę.</span><span class="sxs-lookup"><span data-stu-id="c8a26-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="c8a26-121">Kliknij nazwę hello hello toosee chronionego elementu **szczegóły kopii zapasowej** kartę, która pokazuje informacje dotyczące hello ostatniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Kopia zapasowa maszyny wirtualnej](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="c8a26-123">tooview i zarządzanie nimi ustawień zasad tworzenia kopii zapasowej dla maszyny wirtualnej kliknij hello **zasady** kartę.</span><span class="sxs-lookup"><span data-stu-id="c8a26-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Zasady maszyny wirtualnej](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="c8a26-125">Witaj **zasady tworzenia kopii zapasowej** karcie pokazuje hello istniejące zasady.</span><span class="sxs-lookup"><span data-stu-id="c8a26-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="c8a26-126">Można zmodyfikować zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c8a26-126">You can modify as needed.</span></span> <span data-ttu-id="c8a26-127">Jeśli potrzebujesz toocreate nowych zasad kliknij **Utwórz** na powitania **zasady** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="c8a26-128">Należy pamiętać, że tooremove zasady go nie powinny być skojarzone z nią żadne maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c8a26-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Zasady maszyny wirtualnej](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="c8a26-130">Możesz też uzyskać więcej informacji na temat akcji lub stan maszyny wirtualnej na powitania **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="c8a26-131">Kliknij zadanie w tooget listy hello więcej szczegółów lub filtrowania zadań dla określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Zadania](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="c8a26-133">Na żądanie kopii zapasowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c8a26-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="c8a26-134">Skonfigurowane dla ochrony na żądanie można wykonać kopii zapasowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="c8a26-135">Jeśli trwa oczekiwanie na początkową kopię zapasową hello hello maszyny wirtualnej, tworzenia kopii zapasowej na żądanie utworzy pełną kopię hello maszyny wirtualnej w magazynie kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a26-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="c8a26-136">Jeśli pierwsza kopia zapasowa została wykonana, na żądanie kopii zapasowej będzie tylko do wysyłania zmiany z poprzedniej kopii zapasowej tooAzure kopii zapasowej tj. Magazyn on mają zawsze wartości rosnące.</span><span class="sxs-lookup"><span data-stu-id="c8a26-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="c8a26-137">Zakres przechowywania kopii zapasowej na żądanie ustawiono tooretention wartość określona dla przechowywania codziennych w toohello odpowiednie zasady tworzenia kopii zapasowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="c8a26-138">tootake na żądanie kopii zapasowej maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c8a26-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="c8a26-139">Przejdź toohello **chronione elementy** i wybrać opcję **maszyny wirtualnej Azure** jako **typu** (jeśli jeszcze nie został wybrany) i wybierz polecenie **wybierz**przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8a26-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="c8a26-141">Wybierz maszynę wirtualną hello, na którym tootake na żądanie kopii zapasowej i kliknij na **Utwórz kopię zapasową teraz** przycisk u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Wykonaj kopię zapasową teraz](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="c8a26-143">Spowoduje to utworzenie zadania tworzenia kopii zapasowej na maszynie wirtualnej hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="c8a26-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="c8a26-144">Zakres przechowywania punktu odzyskiwania został utworzony za pomocą tego zadania będzie taka sama jak określona w zasad hello skojarzoną z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Tworzenie zadania tworzenia kopii zapasowej](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="c8a26-146">tooview hello zasady skojarzone z maszyną wirtualną, Drąż w dół do maszyny wirtualnej w hello **chronione elementy** karta zasad Przejdź toobackup i strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="c8a26-147">Po utworzeniu zadania hello, możesz kliknąć **zadania** przycisk wyskakujące hello paska toosee hello odpowiedniego zadania na stronie zadań hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Utworzono zadanie kopii zapasowej](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="c8a26-149">Po pomyślnym ukończeniu zadania hello, zostanie utworzony punkt odzyskiwania, którego można użyć maszyny wirtualnej hello toorestore.</span><span class="sxs-lookup"><span data-stu-id="c8a26-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="c8a26-150">To powoduje również zwiększenie wartości kolumny punktu odzyskiwania hello 1 w **chronione elementy** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="c8a26-151">Zatrzymaj ochronę maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c8a26-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="c8a26-152">Możesz wybrać toostop hello kolejnych kopii zapasowych maszyny wirtualnej z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="c8a26-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="c8a26-153">Zachowaj dane kopii zapasowej skojarzonego z maszyną wirtualną w magazynie usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="c8a26-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="c8a26-154">Usuwanie danych kopii zapasowej skojarzonego z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="c8a26-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="c8a26-155">Jeśli zostały wybrane dane kopii zapasowej tooretain skojarzoną z maszyną wirtualną, można użyć maszyny wirtualnej hello toorestore dane kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="c8a26-156">O cenach szczegóły takich maszyn wirtualnych, kliknij przycisk [tutaj](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="c8a26-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="c8a26-157">tooStop ochrony dla maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c8a26-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="c8a26-158">Przejdź za**chronione elementy** i wybrać opcję **maszyny wirtualnej platformy Azure** jako typ filtru hello (jeśli jeszcze nie został wybrany) i kliknięcie **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8a26-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="c8a26-160">Wybierz maszynę wirtualną hello i wybierz polecenie **Zatrzymaj ochronę** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="c8a26-162">Domyślnie kopia zapasowa Azure nie powoduje usunięcia danych kopii zapasowej hello skojarzoną z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Upewnij się, Zatrzymaj ochronę](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="c8a26-164">Jeśli chcesz toodelete dane kopii zapasowej, zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Pole wyboru](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="c8a26-166">Wybierz przyczynę zatrzymywanie hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="c8a26-167">Jest to opcjonalne, podania przyczyny będzie pomocy toowork kopia zapasowa Azure na powitania opinii i priorytety hello scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="c8a26-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="c8a26-168">Polecenie **przesyłania** hello toosubmit przycisk **Zatrzymaj ochronę** zadania.</span><span class="sxs-lookup"><span data-stu-id="c8a26-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="c8a26-169">Polecenie **zadania** toosee hello odpowiedniego zadania hello w **zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="c8a26-171">Jeśli nie wybrano **Usuń skojarzone dane kopii zapasowej** opcję podczas **Zatrzymaj ochronę** ochrony kreatora, a następnie po zakończeniu zadania, stan zmienia się zbyt**ochrony zatrzymana**.</span><span class="sxs-lookup"><span data-stu-id="c8a26-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="c8a26-172">Hello dane pozostają z usługi Kopia zapasowa Azure, dopóki zostanie jawnie usunięty.</span><span class="sxs-lookup"><span data-stu-id="c8a26-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="c8a26-173">Należy zawsze usunąć dane hello, wybierając hello maszyny wirtualnej w hello **chronione elementy** strony i klikając **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c8a26-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Zatrzymania ochrony](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="c8a26-175">Jeśli wybrano hello **Usuń skojarzone dane kopii zapasowej** opcji, hello maszyny wirtualnej nie będzie częścią hello **chronione elementy** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="c8a26-176">Ponownie włączyć ochronę maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c8a26-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="c8a26-177">Jeśli nie wybrano hello **Skojarz dane kopii zapasowej usunięcia** opcji w **Zatrzymaj ochronę**, można ponownie włączyć ochronę maszyny wirtualnej hello, wykonując następujące toobacking podobne kroki hello się zarejestrować wirtualnego maszyny.</span><span class="sxs-lookup"><span data-stu-id="c8a26-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="c8a26-178">Gdy chroniony, tej maszyny wirtualnej zostanie zachowane dane kopii zapasowej poprzedniego toostop ochrony i punkty odzyskiwania utworzone po ponownie ochronę.</span><span class="sxs-lookup"><span data-stu-id="c8a26-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="c8a26-179">Po ponownego włączenia ochrony stanu ochrony maszyny wirtualnej hello zostaną zmienione za**chronione** jeżeli istnieją punkty odzyskiwania wcześniejsze zbyt**Zatrzymaj ochronę**.</span><span class="sxs-lookup"><span data-stu-id="c8a26-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Maszyny Wirtualnej przełączonej](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="c8a26-181">Podczas ponownie ochrona powitalnych maszyny wirtualnej, można wybrać inne zasady niż zasady hello, z którą maszyny wirtualnej został początkowo chronić.</span><span class="sxs-lookup"><span data-stu-id="c8a26-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="c8a26-182">Wyrejestruj maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c8a26-182">Unregister virtual machines</span></span>
<span data-ttu-id="c8a26-183">Jeśli chcesz, aby maszyna wirtualna hello tooremove z magazynu kopii zapasowych hello:</span><span class="sxs-lookup"><span data-stu-id="c8a26-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="c8a26-184">Polecenie hello **UNREGISTER** przycisk u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Wyłącz ochronę](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="c8a26-186">Powiadomienie wyskakujące będą wyświetlane u dołu hello ekranu hello żądania potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="c8a26-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="c8a26-187">Kliknij przycisk **tak** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c8a26-187">Click **YES** toocontinue.</span></span>

    ![Wyłącz ochronę](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="c8a26-189">Usuwanie danych kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="c8a26-189">Delete Backup data</span></span>
<span data-ttu-id="c8a26-190">Można usunąć danych kopii zapasowej hello skojarzonych z maszyną wirtualną, albo:</span><span class="sxs-lookup"><span data-stu-id="c8a26-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="c8a26-191">Podczas zadanie zatrzymania ochrony</span><span class="sxs-lookup"><span data-stu-id="c8a26-191">During Stop Protection Job</span></span>
* <span data-ttu-id="c8a26-192">Po Zatrzymaj ochronę ukończenia zadania na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c8a26-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="c8a26-193">toodelete dane kopii zapasowej na maszynie wirtualnej, który znajduje się w hello *ochrony zatrzymana* stanu po pomyślnym zarejestrowaniu **zatrzymać kopii zapasowej** zadania:</span><span class="sxs-lookup"><span data-stu-id="c8a26-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="c8a26-194">Przejdź toohello **chronione elementy** i wybrać opcję **maszyny wirtualnej Azure** jako *typu* i kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8a26-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="c8a26-196">Wybierz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-196">Select hello virtual machine.</span></span> <span data-ttu-id="c8a26-197">Maszyna wirtualna Hello będzie w **ochrony zatrzymana** stanu.</span><span class="sxs-lookup"><span data-stu-id="c8a26-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Ochrona zatrzymana](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="c8a26-199">Kliknij przycisk hello **usunąć** przycisk u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Usuwanie kopii zapasowej](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="c8a26-201">W hello **usunąć danych kopii zapasowej** kreatora wybierz przyczynę usuwanie danych kopii zapasowej (zdecydowanie zalecane) i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="c8a26-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="c8a26-203">Spowoduje to utworzenie zadania toodelete kopii zapasowych danych z wybraną maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c8a26-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="c8a26-204">Kliknij przycisk **zadania** toosee odpowiedniego zadania na stronie zadań.</span><span class="sxs-lookup"><span data-stu-id="c8a26-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Pomyślnie usunięto danych](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="c8a26-206">Po zakończeniu zadania hello hello wpis odpowiednią maszynę wirtualną toohello zostaną usunięte z **chronione elementy** strony.</span><span class="sxs-lookup"><span data-stu-id="c8a26-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="c8a26-207">Pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="c8a26-207">Dashboard</span></span>
<span data-ttu-id="c8a26-208">Na powitania **pulpitu nawigacyjnego** stronie można przejrzeć informacje o maszynach wirtualnych platformy Azure, magazynu i zadań skojarzonych z nimi w hello ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="c8a26-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="c8a26-209">Można wyświetlić stanu kopii zapasowej oraz wszelkie skojarzone błędy tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-209">You can view backup status and any associated backup errors.</span></span>

![Pulpit nawigacyjny](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="c8a26-211">Wartości na pulpicie nawigacyjnym hello są odświeżane co 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="c8a26-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="c8a26-212">Operacje inspekcji</span><span class="sxs-lookup"><span data-stu-id="c8a26-212">Auditing Operations</span></span>
<span data-ttu-id="c8a26-213">Kopia zapasowa Azure udostępnia przegląd hello "dzienniki operacji" operacje tworzenia kopii zapasowej wyzwalane przez powitania klienta, dzięki czemu można łatwo toosee dokładnie jakie operacje zarządzania były wykonywane na powitania magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c8a26-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="c8a26-214">Dzienniki operacji włączyć doskonałe których post i inspekcji obsługę hello operacje tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="c8a26-215">Hello następujące operacje są rejestrowane w dziennikach operacji:</span><span class="sxs-lookup"><span data-stu-id="c8a26-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="c8a26-216">Zarejestruj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="c8a26-216">Register</span></span>
* <span data-ttu-id="c8a26-217">Unregister</span><span class="sxs-lookup"><span data-stu-id="c8a26-217">Unregister</span></span>
* <span data-ttu-id="c8a26-218">Konfigurowanie ochrony</span><span class="sxs-lookup"><span data-stu-id="c8a26-218">Configure protection</span></span>
* <span data-ttu-id="c8a26-219">Kopia zapasowa (zarówno zaplanowanych oraz kopii zapasowej na żądanie za pomocą BackupNow)</span><span class="sxs-lookup"><span data-stu-id="c8a26-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="c8a26-220">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="c8a26-220">Restore</span></span>
* <span data-ttu-id="c8a26-221">Zatrzymaj ochronę</span><span class="sxs-lookup"><span data-stu-id="c8a26-221">Stop protection</span></span>
* <span data-ttu-id="c8a26-222">Usuwanie danych kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="c8a26-222">Delete backup data</span></span>
* <span data-ttu-id="c8a26-223">Dodawanie zasad</span><span class="sxs-lookup"><span data-stu-id="c8a26-223">Add policy</span></span>
* <span data-ttu-id="c8a26-224">Usuń zasady</span><span class="sxs-lookup"><span data-stu-id="c8a26-224">Delete policy</span></span>
* <span data-ttu-id="c8a26-225">Zaktualizuj zasady</span><span class="sxs-lookup"><span data-stu-id="c8a26-225">Update policy</span></span>
* <span data-ttu-id="c8a26-226">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="c8a26-226">Cancel job</span></span>

<span data-ttu-id="c8a26-227">odpowiedni magazyn kopii zapasowych tooa dzienniki operacji tooview:</span><span class="sxs-lookup"><span data-stu-id="c8a26-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="c8a26-228">Przejdź za**usług zarządzania** w portalu Azure, a następnie kliknij przycisk hello **dzienniki operacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="c8a26-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Dzienniki operacji](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="c8a26-230">Filtry hello wybierz **kopii zapasowej** jako *typu* i określ nazwę magazynu kopii zapasowych hello w *nazwa usługi* i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="c8a26-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtr dzienniki operacji](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="c8a26-232">W dziennikach operacji hello, wybierz żadnej operacji, a następnie kliknij przycisk **szczegóły** toosee szczegóły odpowiadająca mu operacja tooan.</span><span class="sxs-lookup"><span data-stu-id="c8a26-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Szczegóły pobierania dzienników operacji](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="c8a26-234">Witaj **kreatora szczegóły** zawiera informacje na temat operacji hello wyzwoleniu zadania. identyfikator zasobu, na którym ta operacja zostanie wywołany i godzina rozpoczęcia operacji hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Szczegóły operacji](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="c8a26-236">Powiadomienia o alertach</span><span class="sxs-lookup"><span data-stu-id="c8a26-236">Alert notifications</span></span>
<span data-ttu-id="c8a26-237">Niestandardowe powiadomień o alertach hello zadań można uzyskać w portalu.</span><span class="sxs-lookup"><span data-stu-id="c8a26-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="c8a26-238">Jest to osiągane przez zdefiniowanie opartych na środowisku PowerShell reguł alertów na operacyjne dzienniki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c8a26-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="c8a26-239">Firma Microsoft zaleca używanie *środowiska PowerShell w wersji 1.3.0 lub nowszej*.</span><span class="sxs-lookup"><span data-stu-id="c8a26-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="c8a26-240">toodefine tooalert niestandardowe powiadomienie w przypadku niepowodzenia tworzenia kopii zapasowej będzie wyglądać przykład polecenia:</span><span class="sxs-lookup"><span data-stu-id="c8a26-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="c8a26-241">**ResourceId**: można uzyskać tę z menu podręczne dzienniki operacji zgodnie z opisem w powyżej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c8a26-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="c8a26-242">ResourceUri w oknie podręcznym szczegóły operacji jest toobe ResourceId hello podany dla tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8a26-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="c8a26-243">**OperationName**: są to hello formatu "Microsoft.Backup/backupvault/<EventName>" w przypadku, gdy EventName jest jednym z rejestru, Unregister, ConfigureProtection, kopii zapasowych, przywracania, StopProtection, DeleteBackupData, UpdateProtectionPolicy CreateProtectionPolicy, DeleteProtectionPolicy,</span><span class="sxs-lookup"><span data-stu-id="c8a26-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="c8a26-244">**Stan**: obsługiwane wartości są Started zakończyło się pomyślnie, a nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="c8a26-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="c8a26-245">**Grupa zasobów**: Grupa zasobów hello zasobu, na którym zostanie wywołany operacji.</span><span class="sxs-lookup"><span data-stu-id="c8a26-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="c8a26-246">Możesz go uzyskać z ResourceId wartość.</span><span class="sxs-lookup"><span data-stu-id="c8a26-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="c8a26-247">Wartość między polami */resourceGroups/* i */providers/* w ResourceId wartość jest wartością hello grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="c8a26-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="c8a26-248">**Nazwa**: Nazwa hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="c8a26-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="c8a26-249">**CustomEmail**: Określ toowhich adres e-mail niestandardowych hello ma toosend powiadomień o alertach</span><span class="sxs-lookup"><span data-stu-id="c8a26-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="c8a26-250">**SendToServiceOwners**: Ta opcja wysyła powiadomienie o alercie tooall Administratorzy i współadministratorzy hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c8a26-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="c8a26-251">Mogą być używane w **AzureRmAlertRuleEmail nowy** polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="c8a26-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="c8a26-252">Ograniczenia dotyczące alertów</span><span class="sxs-lookup"><span data-stu-id="c8a26-252">Limitations on Alerts</span></span>
<span data-ttu-id="c8a26-253">Alerty oparte na zdarzeniu są poddane toohello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="c8a26-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="c8a26-254">Alerty są wyzwalane na wszystkich maszynach wirtualnych w magazynie kopii zapasowych hello.</span><span class="sxs-lookup"><span data-stu-id="c8a26-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="c8a26-255">Nie można go dostosować tooget alertów dla określonej grupy maszyn wirtualnych w magazynie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c8a26-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="c8a26-256">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="c8a26-256">This feature is in Preview.</span></span> [<span data-ttu-id="c8a26-257">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="c8a26-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="c8a26-258">Będą wysyłane alerty z "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="c8a26-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="c8a26-259">Obecnie nie można zmodyfikować hello nadawcą wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="c8a26-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8a26-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8a26-260">Next steps</span></span>
* [<span data-ttu-id="c8a26-261">Przywracanie maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c8a26-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
