---
title: aaaBack maszyny wirtualne platformy Azure | Dokumentacja firmy Microsoft
description: "Odnajdowanie, rejestrowania i utworzyć kopię zapasową magazynu usług odzyskiwania tooa maszyn wirtualnych platformy Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: kopii zapasowej maszyny wirtualnej. Tworzenie kopii zapasowej maszyny wirtualnej; Kopia zapasowa i odzyskiwanie po awarii; ARM kopii zapasowej maszyny wirtualnej
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="88eb6-104">Magazyn usług odzyskiwania tooa i wykonywanie kopii zapasowych maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88eb6-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88eb6-105">Wykonaj kopię zapasową magazynu usług tooRecovery maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="88eb6-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="88eb6-106">Wykonaj kopię zapasową magazynu tooBackup maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="88eb6-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="88eb6-107">W tym artykule szczegółowo sposób magazynu tooback się tooa maszynach wirtualnych platformy Azure (wdrożone usługi Resource Manager i wdrożone w klasycznej) usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="88eb6-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="88eb6-108">Większość pracy hello tworzenia kopii zapasowych maszyn wirtualnych jest przygotowanie hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="88eb6-109">Zanim można utworzyć kopię zapasową lub ochrony maszyny Wirtualnej, należy wykonać hello [wymagania wstępne](backup-azure-arm-vms-prepare.md) tooprepare środowiska z ochroną maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88eb6-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="88eb6-110">Po zakończeniu hello wymagań wstępnych, można zainicjować hello operacji tworzenia kopii zapasowej tootake migawki maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88eb6-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="88eb6-111">Aby uzyskać więcej informacji, zobacz artykuły hello na [planowania infrastruktury kopii zapasowych maszyn wirtualnych na platformie Azure](backup-azure-vms-introduction.md) i [maszyn wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="88eb6-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="88eb6-112">Wyzwolenie hello zadanie tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="88eb6-112">Triggering hello backup job</span></span>
<span data-ttu-id="88eb6-113">zasady tworzenia kopii zapasowej Hello skojarzone z powitalne magazyn usług odzyskiwania i definiuje kiedy i jak często jest uruchamiana hello operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="88eb6-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="88eb6-114">Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello początkowa kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="88eb6-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="88eb6-115">Dopóki nie wystąpi hello początkowa kopia zapasowa, hello stan ostatniej kopii zapasowej na powitania **zadania tworzenia kopii zapasowej** bloku jest pokazywana jako **ostrzeżenie (początkowa kopia zapasowa oczekujących)**.</span><span class="sxs-lookup"><span data-stu-id="88eb6-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="88eb6-117">O ile nie przypada tworzenia początkowej kopii zapasowej toobegin wkrótce, zalecane jest uruchomienie **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="88eb6-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="88eb6-118">Po uruchomieniu procedury z pulpitem nawigacyjnym magazynu hello Hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="88eb6-119">Ta procedura służy do uruchamiania hello początkowej zadanie tworzenia kopii zapasowej po zakończeniu wszystkie wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="88eb6-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="88eb6-120">Jeśli jest już uruchomione zadanie tworzenia kopii zapasowej początkowej hello, ta procedura nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="88eb6-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="88eb6-121">Witaj skojarzonych zasad tworzenia kopii zapasowej określa hello następne zadanie tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="88eb6-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="88eb6-122">toorun hello początkowej zadanie tworzenia kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="88eb6-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="88eb6-123">Na pulpicie nawigacyjnym magazynu hello, kliknij przycisk numer hello pod **kopii zapasowej elementów**, lub kliknij przycisk hello **kopii zapasowej elementów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="88eb6-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="88eb6-124">
  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="88eb6-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="88eb6-125">Witaj **kopii zapasowej elementów** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="88eb6-125">hello **Backup Items** blade opens.</span></span>

  ![Tworzenie kopii zapasowych elementów](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="88eb6-127">Na powitania **kopii zapasowej elementów** bloku, wybierz hello elementu.</span><span class="sxs-lookup"><span data-stu-id="88eb6-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="88eb6-129">Witaj **kopii zapasowej elementów** listy zostanie otwarta.</span><span class="sxs-lookup"><span data-stu-id="88eb6-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Zadanie tworzenia kopii zapasowej zostało wyzwolone](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="88eb6-131">Na powitania **kopii zapasowej elementów** kliknij wielokropek hello **...**  menu kontekstowe hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="88eb6-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="88eb6-133">zostanie wyświetlone menu kontekstowe Hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-133">hello Context menu appears.</span></span>

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="88eb6-135">W menu kontekstowym hello, kliknij przycisk **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="88eb6-135">On hello Context menu, click **Backup now**.</span></span>

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="88eb6-137">zostanie otwarty blok Utwórz kopię zapasową teraz Hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-137">hello Backup Now blade opens.</span></span>

  ![Pokazuje hello Utwórz kopię zapasową teraz bloku](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="88eb6-139">Na powitania Utwórz kopię zapasową teraz bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="88eb6-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![Ustaw hello ostatni dzień hello Utwórz kopię zapasową teraz punktu odzyskiwania są przechowywane.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="88eb6-141">Wdrożenie powiadomień informujący zostało wyzwolone zadanie tworzenia kopii zapasowej hello i monitorować postęp hello hello zadania na stronie zadań tworzenia kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="88eb6-142">W zależności od rozmiaru hello maszyny Wirtualnej tworzenie początkowej kopii zapasowej hello może chwilę potrwać.</span><span class="sxs-lookup"><span data-stu-id="88eb6-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="88eb6-143">tooview lub Śledź stan hello hello tworzenia początkowej kopii zapasowej, na pulpicie nawigacyjnym magazynu hello, na powitania **zadania tworzenia kopii zapasowej** kliknij Kafelek **w toku**.</span><span class="sxs-lookup"><span data-stu-id="88eb6-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="88eb6-145">zostanie otwarty blok zadania tworzenia kopii zapasowej Hello.</span><span class="sxs-lookup"><span data-stu-id="88eb6-145">hello Backup Jobs blade opens.</span></span>

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="88eb6-147">W hello **kopii zapasowej zadania** bloku widać hello stan wszystkich zadań.</span><span class="sxs-lookup"><span data-stu-id="88eb6-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="88eb6-148">Sprawdź, czy hello kopii zapasowej dla maszyny Wirtualnej jest nadal w toku, czy zakończyło się.</span><span class="sxs-lookup"><span data-stu-id="88eb6-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="88eb6-149">Po zakończeniu zadania tworzenia kopii zapasowej stanu hello jest *Ukończono*.</span><span class="sxs-lookup"><span data-stu-id="88eb6-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="88eb6-150">W ramach operacji tworzenia kopii zapasowej hello hello usługi Kopia zapasowa Azure problemy z rozszerzeniem kopii zapasowej polecenia toohello w każdej tooflush maszyna wirtualna, wszystkie zapisuje i migawki spójne.</span><span class="sxs-lookup"><span data-stu-id="88eb6-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="88eb6-151">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="88eb6-151">Troubleshooting errors</span></span>
<span data-ttu-id="88eb6-152">Jeśli wystąpiły problemy podczas tworzenia kopii zapasowej maszyny wirtualnej, zobacz hello [maszyny Wirtualnej artykuł dotyczący rozwiązywania problemów](backup-azure-vms-troubleshoot.md) Aby uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="88eb6-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88eb6-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88eb6-153">Next steps</span></span>
<span data-ttu-id="88eb6-154">Teraz, ochrony maszyny Wirtualnej, zobacz hello następujące artykuły toolearn o zadaniach zarządzania maszyny Wirtualnej i w jaki sposób toorestore maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="88eb6-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="88eb6-155">Monitorowanie maszyn wirtualnych i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="88eb6-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="88eb6-156">Przywracanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="88eb6-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
