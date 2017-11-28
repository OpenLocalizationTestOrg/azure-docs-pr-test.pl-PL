---
title: "Witaj aaaReset hasła lub w konfiguracji pulpitu zdalnego na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hasło do konta lub usług pulpitu zdalnego na maszynie Wirtualnej systemu Windows utworzonego przy użyciu hello Classic deployment model przy użyciu tooreset hello portalu Azure lub programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="6e97b-103">Usługi pulpitu zdalnego hello tooreset lub jego hasło logowania na maszynie wirtualnej Windows tworzenia przy użyciu klasycznego modelu wdrożenia hello</span><span class="sxs-lookup"><span data-stu-id="6e97b-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6e97b-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6e97b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6e97b-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="6e97b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6e97b-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e97b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6e97b-107">Możesz również [wykonaj te kroki dla maszyn wirtualnych utworzonych za pomocą modelu wdrażania usługi Resource Manager hello](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="6e97b-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="6e97b-108">Jeśli nie można połączyć maszyny wirtualnej systemu Windows tooa (VM), można zresetować hasła administratora lokalnego hello lub zresetować hello w konfiguracji usługi pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6e97b-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="6e97b-109">Można użyć albo hello Azure rozszerzenia maszyny Wirtualnej dostępu do portalu lub hello w haśle hello tooreset programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e97b-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="6e97b-110">Sposoby tooreset konfiguracji lub poświadczeń</span><span class="sxs-lookup"><span data-stu-id="6e97b-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="6e97b-111">Można zresetować usług pulpitu zdalnego i poświadczenia na kilka różnych sposobów, w zależności od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="6e97b-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="6e97b-112">Resetuj przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6e97b-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="6e97b-113">Resetuj przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e97b-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="6e97b-114">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e97b-114">Azure portal</span></span>
<span data-ttu-id="6e97b-115">Można użyć hello [portalu Azure](https://portal.azure.com) hello tooreset usługi pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6e97b-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="6e97b-116">Kliknij paski hello trzech w lewym górnym rogu hello tooexpand hello portalu menu, a następnie kliknij **maszyn wirtualnych (klasyczne)**:</span><span class="sxs-lookup"><span data-stu-id="6e97b-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Przeglądaj w poszukiwaniu Azure maszyny Wirtualnej](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="6e97b-118">Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **zresetować zdalnego...** . hello następujące zostanie wyświetlone okno dialogowe tooreset hello w konfiguracji pulpitu zdalnego:</span><span class="sxs-lookup"><span data-stu-id="6e97b-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Strony konfiguracji RDP resetowania](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="6e97b-120">Można również zresetować hello nazwę użytkownika i hasło konta administratora lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="6e97b-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="6e97b-121">Z maszyny Wirtualnej, kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="6e97b-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="6e97b-122">zostanie wyświetlony blok resetowania hasła Hello:</span><span class="sxs-lookup"><span data-stu-id="6e97b-122">hello password reset blade is displayed:</span></span>

![Strona Resetowanie hasła](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="6e97b-124">Po wprowadzeniu hello nową nazwę użytkownika i hasło, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6e97b-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="6e97b-125">Rozszerzenia VMAccess i programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e97b-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="6e97b-126">Upewnij się, że Agent maszyny Wirtualnej jest zainstalowany na maszynie wirtualnej hello powitalne.</span><span class="sxs-lookup"><span data-stu-id="6e97b-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="6e97b-127">Witaj rozszerzenia VMAccess nie wymaga toobe zainstalowane przed użyciem go, dopóki hello agenta maszyny Wirtualnej jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="6e97b-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="6e97b-128">Upewnij się, że powitalne za pomocą następującego polecenia hello jest już zainstalowany Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e97b-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="6e97b-129">(Zastępuje "myCloudService" i "myVM" hello nazwy usługi w chmurze i maszyny Wirtualnej, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="6e97b-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="6e97b-130">Dowiedz się te nazwy, uruchamiając `Get-AzureVM` bez żadnych parametrów.)</span><span class="sxs-lookup"><span data-stu-id="6e97b-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="6e97b-131">Jeśli hello **hosta zapisu** polecenie wyświetla **True**, hello jest zainstalowany Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e97b-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="6e97b-132">Jeśli Wyświetla **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="6e97b-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="6e97b-133">Jeśli utworzono hello maszyny wirtualnej przy użyciu portalu hello, sprawdź, czy `$vm.GetInstance().ProvisionGuestAgent` zwraca **True**.</span><span class="sxs-lookup"><span data-stu-id="6e97b-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="6e97b-134">Jeśli nie można ustawić za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6e97b-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="6e97b-135">To polecenie uniemożliwia hello następujący błąd podczas pracy hello **AzureVMExtension zestaw** w następnych krokach hello: "Udostępniania gościa musi być włączony Agent na powitania obiektu maszyny Wirtualnej przed ustawieniem rozszerzenia dostępu do maszyn wirtualnych IaaS."</span><span class="sxs-lookup"><span data-stu-id="6e97b-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="6e97b-136">**Zresetuj hasło konta administratora lokalnego hello**</span><span class="sxs-lookup"><span data-stu-id="6e97b-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="6e97b-137">Utwórz poświadczenia logowania z hello bieżąca nazwa konta administratora lokalnego i nowe hasło, a następnie uruchom hello `Set-AzureVMAccessExtension` w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="6e97b-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="6e97b-138">Wpisz inną nazwę niż hello bieżącego konta, hello rozszerzenia VMAccess zmienia nazwę konta administratora lokalnego hello, przypisuje hello hasło toothat konta, a problemy z wylogowaniem pulpitu zdalnego. Wyłączenie konta administratora lokalnego hello hello rozszerzenia VMAccess włączy ją.</span><span class="sxs-lookup"><span data-stu-id="6e97b-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="6e97b-139">Te polecenia również zresetować hello w konfiguracji usługi pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6e97b-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="6e97b-140">**Resetuj hello w konfiguracji usługi pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="6e97b-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="6e97b-141">tooreset hello konfiguracji usługi pulpitu zdalnego, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6e97b-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="6e97b-142">Hello rozszerzenia VMAccess uruchamia dwa polecenia w maszynie wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="6e97b-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="6e97b-143">To polecenie włącza hello wbudowane zapory systemu Windows grupy, która zezwala na ruch przychodzący pulpitu zdalnego, który korzysta z portu 3389 protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="6e97b-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="6e97b-144">To polecenie ustawia hello fDenyTSConnections rejestru wartość too0, włączenie połączeń pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6e97b-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e97b-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e97b-145">Next steps</span></span>
<span data-ttu-id="6e97b-146">Jeśli hello rozszerzenia dostępu do maszyny Wirtualnej platformy Azure nie odpowiada i tooreset hello hasła, możesz [resetowania hello lokalne hasło systemu Windows w trybie offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e97b-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6e97b-147">Ta metoda jest procesem bardziej zaawansowane i wymaga tooconnect hello wirtualnego dysku twardego hello problematyczne tooanother maszyny Wirtualnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e97b-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="6e97b-148">Wykonaj czynności hello opisanych w tym artykule najpierw, a następnie spróbuj tylko metody resetowania hasła w trybie offline hello w ostateczności.</span><span class="sxs-lookup"><span data-stu-id="6e97b-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="6e97b-149">Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje</span><span class="sxs-lookup"><span data-stu-id="6e97b-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="6e97b-150">Uzyskuj dostęp do maszyny wirtualnej platformy Azure tooan RDP lub SSH</span><span class="sxs-lookup"><span data-stu-id="6e97b-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="6e97b-151">Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e97b-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

