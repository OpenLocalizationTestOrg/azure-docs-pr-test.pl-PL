---
title: "aaaReset lokalne hasło systemu Windows bez agenta platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak tooreset hello hasła lokalnego konta użytkownika systemu Windows, gdy agent gościa Azure hello nie jest zainstalowany i działa na maszynie Wirtualnej"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="65985-103">Jak tooreset lokalnego hasła systemu Windows dla maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="65985-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="65985-104">Można zresetować hasła lokalnego systemu Windows hello maszyny wirtualnej na platformie Azure przy użyciu hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pod warunkiem hello Azure gościa agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="65985-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="65985-105">Ta metoda jest hello podstawowy sposób tooreset hasła dla maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65985-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="65985-106">Jeśli wystąpią problemy z hello Azure gościa agent nie odpowiada, lub niepowodzeniem tooinstall po przekazaniu niestandardowego obrazu, można ręcznie zresetować hasło systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="65985-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="65985-107">W tym artykule szczegółowo sposób tooreset hasła konta lokalnego, dołączając hello tooanother wirtualnego dysku systemu operacyjnego źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="65985-108">Ten proces można używać tylko w ostateczności.</span><span class="sxs-lookup"><span data-stu-id="65985-108">Only use this process as a last resort.</span></span> <span data-ttu-id="65985-109">Zawsze spróbuj tooreset hasło za pomocą hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pierwszy.</span><span class="sxs-lookup"><span data-stu-id="65985-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="65985-110">Omówienie procesu hello</span><span class="sxs-lookup"><span data-stu-id="65985-110">Overview of hello process</span></span>
<span data-ttu-id="65985-111">Witaj podstawowych kroków resetowania dla maszyny Wirtualnej systemu Windows na platformie Azure, gdy brak dostępu agenta gościa Azure toohello hasła lokalnego jest następujący:</span><span class="sxs-lookup"><span data-stu-id="65985-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="65985-112">Usuń hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-112">Delete hello source VM.</span></span> <span data-ttu-id="65985-113">dyski wirtualne Hello są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="65985-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="65985-114">Dołącz tooanother dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej VM na powitania tej samej lokalizacji, w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65985-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="65985-115">Ta maszyna wirtualna jest hello tooas określonego Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="65985-116">Za pomocą hello Rozwiązywanie problemów z maszyny Wirtualnej, Utwórz niektóre pliki konfiguracji na dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="65985-117">Odłączanie dysku systemu operacyjnego hello maszyny Wirtualnej z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="65985-118">Użyj Menedżera zasobów toocreate szablonu maszyny Wirtualnej za pomocą hello oryginalny dysk wirtualny.</span><span class="sxs-lookup"><span data-stu-id="65985-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="65985-119">Witaj Uruchamianie nowej maszyny Wirtualnej, hello plików konfiguracji powoduje utworzenie aktualizacji hello hasła użytkownika hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="65985-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="65985-120">Szczegółowe procedury</span><span class="sxs-lookup"><span data-stu-id="65985-120">Detailed steps</span></span>
<span data-ttu-id="65985-121">Zawsze spróbuj tooreset hasło za pomocą hello [portalu Azure lub programu Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed podjęciem próby hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="65985-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="65985-122">Upewnij się, że masz kopię zapasową maszyny wirtualnej, przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="65985-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="65985-123">Usuń hello dotyczy maszyny Wirtualnej w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65985-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="65985-124">Hello usuwania maszyny Wirtualnej usuwa tylko metadane hello, odwołanie hello hello maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="65985-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="65985-125">dyski wirtualne Hello są zachowywane po usunięciu hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="65985-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="65985-126">Wybierz hello maszyny Wirtualnej w hello portalu Azure, kliknij przycisk *usunąć*:</span><span class="sxs-lookup"><span data-stu-id="65985-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Usuń istniejącą maszynę Wirtualną](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="65985-128">Dołącz toohello dysku systemu operacyjnego hello źródła wirtualna Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="65985-129">Witaj, rozwiązywanie problemów z maszyny Wirtualnej musi być w hello tym samym regionie co dysk systemu operacyjnego hello źródłowej maszyny Wirtualnej (takie jak `West US`):</span><span class="sxs-lookup"><span data-stu-id="65985-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="65985-130">Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65985-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="65985-131">Kliknij przycisk *dysków* | *Attach istniejących*:</span><span class="sxs-lookup"><span data-stu-id="65985-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Dołączanie istniejącego dysku](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="65985-133">Wybierz *pliku VHD* , a następnie wybierz konto magazynu hello, która zawiera źródło maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="65985-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Wybieranie konta magazynu](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="65985-135">Wybierz kontener źródła hello.</span><span class="sxs-lookup"><span data-stu-id="65985-135">Select hello source container.</span></span> <span data-ttu-id="65985-136">kontener źródła Hello jest zwykle *wirtualne dyski twarde*:</span><span class="sxs-lookup"><span data-stu-id="65985-136">hello source container is typically *vhds*:</span></span>
     
     ![Wybierz kontener magazynu](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="65985-138">Wybierz hello tooattach wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="65985-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="65985-139">Kliknij przycisk *wybierz* toocomplete hello proces:</span><span class="sxs-lookup"><span data-stu-id="65985-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Wybierz wirtualny dysk źródłowy](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="65985-141">Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu pulpitu zdalnego i upewnij się, że dysk systemu operacyjnego hello źródłowej maszyny Wirtualnej jest widoczna:</span><span class="sxs-lookup"><span data-stu-id="65985-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="65985-142">Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello i kliknij przycisk *Connect*.</span><span class="sxs-lookup"><span data-stu-id="65985-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="65985-143">Otwórz plik RDP hello pliki do pobrania.</span><span class="sxs-lookup"><span data-stu-id="65985-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="65985-144">Wprowadź hello użytkownika i hasło hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="65985-145">W Eksploratorze plików poszukaj dysku danych hello podłączony.</span><span class="sxs-lookup"><span data-stu-id="65985-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="65985-146">Witaj źródło maszyny Wirtualnej wirtualny dysk twardy jest hello toohello dysku tylko dane Rozwiązywanie problemów z maszyny Wirtualnej, należy hello F: dysku:</span><span class="sxs-lookup"><span data-stu-id="65985-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Wyświetlanie dysków dołączonych danych](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="65985-148">Utwórz `gpt.ini` w `\Windows\System32\GroupPolicy` na dysku hello źródłowej maszyny Wirtualnej (jeśli istnieje gpt.ini, Zmień nazwę toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="65985-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="65985-149">Upewnij się, możesz przypadkowo utworzyć hello następujące pliki w C:\Windows, hello dysku systemu operacyjnego hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="65985-150">Utwórz hello następujące pliki w stacji hello systemu operacyjnego dla maszyny Wirtualnej, który jest dołączony jako dysk danych źródła.</span><span class="sxs-lookup"><span data-stu-id="65985-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="65985-151">Dodaj następujące wiersze do hello hello `gpt.ini` utworzony plik:</span><span class="sxs-lookup"><span data-stu-id="65985-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Utwórz gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="65985-153">Utwórz `scripts.ini` w `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="65985-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="65985-154">Upewnij się, że są wyświetlane w folderach ukrytych.</span><span class="sxs-lookup"><span data-stu-id="65985-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="65985-155">W razie potrzeby utwórz hello `Machine` lub `Scripts` folderów.</span><span class="sxs-lookup"><span data-stu-id="65985-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="65985-156">Dodaj następujące wiersze hello hello `scripts.ini` utworzony plik:</span><span class="sxs-lookup"><span data-stu-id="65985-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Utwórz scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="65985-158">Utwórz `FixAzureVM.cmd` w `\Windows\System32` z powitania po zawartości, zastępując `<username>` i `<newpassword>` z własne wartości:</span><span class="sxs-lookup"><span data-stu-id="65985-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Utwórz FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="65985-160">Podczas definiowania hello nowe hasło, musi spełniać wymagania dotyczące złożoności hasła hello skonfigurowane dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="65985-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="65985-161">W portalu Azure odłączyć dysku powitania od hello Rozwiązywanie problemów z maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="65985-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="65985-162">Kliknij pozycję Wybierz hello Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello *dysków*.</span><span class="sxs-lookup"><span data-stu-id="65985-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="65985-163">Wybierz hello danych dysk dołączony w kroku 2, kliknij przycisk *Detach*:</span><span class="sxs-lookup"><span data-stu-id="65985-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Odłączanie dysku](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="65985-165">Przed utworzeniem maszyny Wirtualnej, należy uzyskać dysk systemu operacyjnego źródłowej tooyour URI hello:</span><span class="sxs-lookup"><span data-stu-id="65985-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="65985-166">Wybierz hello konta magazynu w hello portalu Azure, kliknij przycisk *obiekty BLOB*.</span><span class="sxs-lookup"><span data-stu-id="65985-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="65985-167">Wybierz kontener hello.</span><span class="sxs-lookup"><span data-stu-id="65985-167">Select hello container.</span></span> <span data-ttu-id="65985-168">kontener źródła Hello jest zwykle *wirtualne dyski twarde*:</span><span class="sxs-lookup"><span data-stu-id="65985-168">hello source container is typically *vhds*:</span></span>
     
     ![Wybierz obiekt blob z konta magazynu](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="65985-170">Wybierz źródło wirtualnego dysku twardego systemu operacyjnego maszyny Wirtualnej, a następnie kliknij przycisk hello *kopiowania* przycisku Dalej toohello *adres URL* nazwy:</span><span class="sxs-lookup"><span data-stu-id="65985-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Skopiuj identyfikator URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="65985-172">Tworzenie maszyny Wirtualnej z dysku systemu operacyjnego hello źródłowej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="65985-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="65985-173">Użyj [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate maszyny Wirtualnej z dysku VHD specjalne.</span><span class="sxs-lookup"><span data-stu-id="65985-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="65985-174">Kliknij przycisk hello `Deploy tooAzure` przycisk tooopen hello portalu Azure przy użyciu szczegółów opartego na szablonie hello wypełnione.</span><span class="sxs-lookup"><span data-stu-id="65985-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="65985-175">Jeśli chcesz tooretain wszystkich poprzednich ustawień hello hello maszyny Wirtualnej, wybierz opcję *Edytuj szablon* tooprovide istniejącej sieci wirtualnej, podsieci, karty sieciowej lub publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="65985-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="65985-176">W hello `OSDISKVHDURI` parametru pola tekstowego, Wklej hello uzyskać identyfikator URI dysku VHD źródła w hello poprzedzających krok:</span><span class="sxs-lookup"><span data-stu-id="65985-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Utwórz maszynę Wirtualną z szablonu](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="65985-178">Po hello nowa maszyna wirtualna jest uruchomiona, należy połączyć toohello maszyny Wirtualnej przy użyciu pulpitu zdalnego z nowego hasła hello określone w hello `FixAzureVM.cmd` skryptu.</span><span class="sxs-lookup"><span data-stu-id="65985-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="65985-179">Z toohello Twojego sesji zdalnej nowej maszyny Wirtualnej, hello Usuń następujące pliki tooclean hello środowiska:</span><span class="sxs-lookup"><span data-stu-id="65985-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="65985-180">Z %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="65985-180">From %windir%\System32</span></span>
      * <span data-ttu-id="65985-181">Usuń FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="65985-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="65985-182">Z %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="65985-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="65985-183">Usuń scripts.ini</span><span class="sxs-lookup"><span data-stu-id="65985-183">remove scripts.ini</span></span>
    * <span data-ttu-id="65985-184">Z %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="65985-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="65985-185">Usuń gpt.ini (jeśli istniał gpt.ini wcześniej i zmieniona toogpt.ini.bak, toogpt.ini wstecz Plik bak hello zmiany nazwy)</span><span class="sxs-lookup"><span data-stu-id="65985-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="65985-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65985-186">Next steps</span></span>
<span data-ttu-id="65985-187">Jeśli nadal nie możesz połączyć przy użyciu pulpitu zdalnego, zobacz hello [przewodnik rozwiązywania problemów RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65985-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="65985-188">Witaj [szczegółowy przewodnik rozwiązywania problemów RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) analizuje Rozwiązywanie problemów z metody zamiast wykonania określonych kroków.</span><span class="sxs-lookup"><span data-stu-id="65985-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="65985-189">Możesz również [otwarcia żądania pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) praktyczne pomocy.</span><span class="sxs-lookup"><span data-stu-id="65985-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

