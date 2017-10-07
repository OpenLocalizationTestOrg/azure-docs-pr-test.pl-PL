---
title: "Wykonaj kopię zapasową maszyn wirtualnych systemu Linux platformy Azure | Dokumentacja firmy Microsoft"
description: "Ochrona maszyn wirtualnych systemu Linux przez tworzenie ich kopii zapasowych za pomocą usługi Kopia zapasowa Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="7f7a9-103">Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7f7a9-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="7f7a9-104">Możesz chronić swoje dane, tworząc kopie zapasowe w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="7f7a9-105">Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="7f7a9-106">Po przywróceniu z punktu odzyskiwania, można przywrócić hello całej maszyny Wirtualnej lub po prostu określonych plików.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="7f7a9-107">W tym artykule opisano, jak toorestore pojedynczy plik tooa nginx uruchomionej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="7f7a9-108">Jeśli nie masz jeszcze toouse maszyny Wirtualnej, możesz utworzyć jedną przy użyciu hello [szybkiego startu Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f7a9-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="7f7a9-109">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="7f7a9-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f7a9-110">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="7f7a9-111">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="7f7a9-112">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="7f7a9-113">Omówienie usługi Backup</span><span class="sxs-lookup"><span data-stu-id="7f7a9-113">Backup overview</span></span>

<span data-ttu-id="7f7a9-114">Gdy hello usługi Kopia zapasowa Azure inicjuje kopii zapasowej, wyzwala hello zapasowy numer wewnętrzny tootake migawki punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="7f7a9-115">Witaj usługi Kopia zapasowa Azure korzysta hello _VMSnapshotLinux_ rozszerzenia w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="7f7a9-116">rozszerzenie Hello jest instalowany podczas hello pierwszej kopii zapasowej maszyny Wirtualnej, jeśli hello maszyna wirtualna jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="7f7a9-117">Jeśli hello maszyna wirtualna nie jest uruchomiona, hello usługi Kopia zapasowa tworzy migawkę hello bazowy magazynu (ponieważ nie zapisy aplikacji występuje podczas powitalne zatrzymaniu maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="7f7a9-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="7f7a9-118">Domyślnie kopia zapasowa Azure przyjmuje kopia zapasowa spójna systemu plików dla maszyny Wirtualnej systemu Linux, ale może być skonfigurowany tootake [przy użyciu platformy skryptów przed i po skrypt kopii zapasowej spójnej aplikacji](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="7f7a9-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="7f7a9-119">Witaj usługi Kopia zapasowa Azure wykonuje migawkę hello, hello danych po toohello przekazanych magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="7f7a9-120">wydajność toomaximize hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="7f7a9-121">Po ukończeniu transferu danych hello hello migawka zostanie usunięta i utworzenia punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="7f7a9-122">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-122">Create a backup</span></span>
<span data-ttu-id="7f7a9-123">Tworzenie prostego zaplanowanego codziennego tworzenia kopii zapasowej tooa magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="7f7a9-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7f7a9-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7f7a9-125">W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="7f7a9-126">Wybierz tooback maszyny Wirtualnej z listy hello się.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="7f7a9-127">W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="7f7a9-128">Witaj **kopii zapasowej Włącz** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="7f7a9-129">W **magazyn usług odzyskiwania i**, kliknij przycisk **Utwórz nowy** i podaj nazwę hello hello nowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="7f7a9-130">Nowy magazyn jest tworzony w hello sam lokalizacji jako maszyna wirtualna hello i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="7f7a9-131">Kliknij przycisk **kopii zapasowej zasad**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-131">Click **Backup policy**.</span></span> <span data-ttu-id="7f7a9-132">W tym przykładzie należy zachować hello wartości domyślne, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="7f7a9-133">Na powitania **kopii zapasowej Włącz** bloku, kliknij przycisk **Włącz kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="7f7a9-134">Spowoduje to utworzenie kopii zapasowej codziennie na podstawie hello domyślnego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="7f7a9-135">toocreate początkowego punktu odzyskiwania, na powitania **kopii zapasowej** kliknij bloku **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="7f7a9-136">Na powitania **Utwórz kopię zapasową teraz** bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="7f7a9-137">W hello **kopii zapasowej** bloku dla maszyny Wirtualnej, zobaczysz hello liczbę punktów odzyskiwania, które są spełnione.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Punkty odzyskiwania](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="7f7a9-139">Hello pierwszej kopii zapasowej trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="7f7a9-140">Po zakończeniu tworzenia kopii zapasowej, należy kontynuować toohello następnej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="7f7a9-141">Przywróć plik</span><span class="sxs-lookup"><span data-stu-id="7f7a9-141">Restore a file</span></span>

<span data-ttu-id="7f7a9-142">Jeśli przypadkowo usunięte lub zmiany tooa plik, można użyć pliku hello toorecover odzyskiwanie plików z magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="7f7a9-143">Odzyskiwanie plików używa skryptu uruchamianego na powitania maszyny Wirtualnej, punkt odzyskiwania hello toomount jako dysk lokalny.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="7f7a9-144">Dyski te pozostanie zainstalowanego na 12 godzin, co można kopiować pliki z punktu odzyskiwania hello i przywracać je toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="7f7a9-145">W tym przykładzie zostanie przedstawiony sposób toorecover hello /var/www/html/index.nginx-debian.html strony sieci web nginx domyślne.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="7f7a9-146">publiczny adres IP Hello naszych maszyny wirtualnej w tym przykładzie jest *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="7f7a9-147">Można znaleźć adres IP hello przy użyciu maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="7f7a9-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="7f7a9-148">Na komputerze lokalnym otwórz przeglądarkę i typ hello publiczny adres IP maszyny Wirtualnej toosee hello domyślne nginx strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="7f7a9-150">Nawiąż połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="7f7a9-151">Usuń /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="7f7a9-152">Na komputerze lokalnym, Odśwież przeglądarkę hello przez naciśnięcie klawiszy CTRL + F5 toosee, że domyślna strona nginx został usunięty.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="7f7a9-154">Na komputerze lokalnym, zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7f7a9-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="7f7a9-155">W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="7f7a9-156">Z listy hello wybierz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="7f7a9-157">W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="7f7a9-158">Witaj **kopii zapasowej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="7f7a9-159">Witaj menu u góry bloku hello hello wybierz **odzyskiwanie plików**.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="7f7a9-160">Witaj **odzyskiwanie plików** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="7f7a9-161">W **krok 1: Wybierz punkt odzyskiwania**, wybierz punkt odzyskiwania z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="7f7a9-162">W **krok 2: Pobieranie skryptu toobrowse i odzyskiwanie plików**, kliknij przycisk hello **Pobierz plik wykonywalny** przycisk.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="7f7a9-163">Zapisz hello pobrany plik tooyour lokalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="7f7a9-164">Kliknij przycisk **pobrać skryptu** pliku skryptu hello toodownload lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="7f7a9-165">Otwórz Bash wiersz i wpisz powitania po, zastępując *Linux_myVM_05-05-2017.sh* z hello Popraw ścieżkę i nazwę skryptu hello, który został pobrany, *azureuser* z nazwą użytkownika hello hello maszyny Wirtualnej i *13.69.75.209* hello publicznego adresu IP dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="7f7a9-166">Na komputerze lokalnym otwórz toohello połączenia SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="7f7a9-167">Na maszynie Wirtualnej, należy dodać wykonać pliku skryptu toohello uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="7f7a9-168">Na maszynie Wirtualnej należy uruchomić punkt odzyskiwania hello hello skryptu toomount jako system plików.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="7f7a9-169">Witaj ścieżkę punktu instalacji hello Hello danych wyjściowych z hello zapewnia skryptu.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="7f7a9-170">dane wyjściowe Hello wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="7f7a9-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="7f7a9-171">Na maszynie Wirtualnej, skopiuj hello nginx domyślnej strony sieci web z toowhere zapasowego punktu instalacji hello usunięte hello pliku.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="7f7a9-172">Na komputerze lokalnym, otwórz kartę przeglądarki hello której są podłączone adres IP toohello hello wirtualna prezentująca hello nginx domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="7f7a9-173">Naciśnij klawisze CTRL + F5 toorefresh hello przeglądarki strony.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="7f7a9-174">Tego hello powinna zostać wyświetlona domyślna strona działa ponownie.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-174">You should now see that hello default page is working again.</span></span>

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="7f7a9-176">Na komputerze lokalnym, przejdź wstecz karty przeglądarki toohello hello portalu Azure i w **krok 3: odinstaluj dyski powitania po odzyskaniu** kliknij hello **odinstalować dyski** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="7f7a9-177">Jeśli zapomnisz toodo ten krok, punktu instalacji toohello połączenia hello jest automatycznie Zamknij po 12 godzinach.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="7f7a9-178">Po zakończeniu tych 12 godzin wymagane toodownload nowe toocreate skryptu nowego punktu instalacji.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7f7a9-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f7a9-179">Next steps</span></span>

<span data-ttu-id="7f7a9-180">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="7f7a9-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f7a9-181">Utwórz kopię zapasową maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="7f7a9-182">Harmonogram tworzenia codziennej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="7f7a9-183">Przywróć plik z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f7a9-183">Restore a file from a backup</span></span>

<span data-ttu-id="7f7a9-184">Przejdź dalej toolearn samouczka toohello dotyczące monitorowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7f7a9-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f7a9-185">Monitorowanie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="7f7a9-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

