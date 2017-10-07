---
title: "Witaj aaaReset hasła lub w konfiguracji pulpitu zdalnego na maszynie Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooreset hasło do konta lub usług pulpitu zdalnego na maszynę Wirtualną systemu Windows przy użyciu hello portalu Azure lub programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="059cd-103">Jak tooreset hello usługi pulpitu zdalnego lub jego hasło logowania na maszynie wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="059cd-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="059cd-104">Jeśli nie można połączyć maszyny wirtualnej systemu Windows tooa (VM), można zresetować hasła administratora lokalnego hello lub zresetować hello w konfiguracji usługi pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="059cd-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="059cd-105">Można użyć albo hello Azure rozszerzenia maszyny Wirtualnej dostępu do portalu lub hello w haśle hello tooreset programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="059cd-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="059cd-106">Jeśli używasz programu PowerShell, upewnij się, że masz hello [najnowsze modułu PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview) i będą one podpisane w tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="059cd-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="059cd-107">Możesz również [wykonaj te kroki dla maszyn wirtualnych utworzonych za pomocą klasycznego modelu wdrożenia hello](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="059cd-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="059cd-108">Sposoby tooreset konfiguracji lub poświadczeń</span><span class="sxs-lookup"><span data-stu-id="059cd-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="059cd-109">Można zresetować usług pulpitu zdalnego i poświadczenia na kilka różnych sposobów, w zależności od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="059cd-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="059cd-110">Resetuj przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="059cd-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="059cd-111">Resetuj przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="059cd-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="059cd-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="059cd-112">Azure portal</span></span>
<span data-ttu-id="059cd-113">Kliknij paski hello trzech w lewym górnym rogu hello tooexpand hello portalu menu, a następnie kliknij **maszyn wirtualnych**:</span><span class="sxs-lookup"><span data-stu-id="059cd-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Przeglądaj w poszukiwaniu Azure maszyny Wirtualnej](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="059cd-115">**Zresetuj hasło konta administratora lokalnego hello**</span><span class="sxs-lookup"><span data-stu-id="059cd-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="059cd-116">Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="059cd-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="059cd-117">zostanie wyświetlony blok resetowania hasła Hello:</span><span class="sxs-lookup"><span data-stu-id="059cd-117">hello password reset blade is displayed:</span></span>

![Strona Resetowanie hasła](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="059cd-119">Wprowadź nazwę użytkownika hello i nowe hasło, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="059cd-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="059cd-120">Spróbuj ponownie połączyć tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="059cd-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="059cd-121">**Resetuj hello w konfiguracji usługi pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="059cd-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="059cd-122">Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="059cd-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="059cd-123">Blok resetowania hasła Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="059cd-123">hello password reset blade is displayed.</span></span> 

![Zresetowanie konfiguracji RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="059cd-125">Wybierz **Resetowanie tylko konfiguracji** z menu rozwijanego hello, następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="059cd-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="059cd-126">Spróbuj ponownie połączyć tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="059cd-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="059cd-127">Rozszerzenia VMAccess i programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="059cd-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="059cd-128">Upewnij się, że masz hello [najnowsze modułu PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview) i będą one podpisane w tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="059cd-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="059cd-129">**Zresetuj hasło konta administratora lokalnego hello**</span><span class="sxs-lookup"><span data-stu-id="059cd-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="059cd-130">Resetowanie hello administratora hasło lub nazwa użytkownika z hello [AzureRmVMAccessExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmaccessextension) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="059cd-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="059cd-131">Utwórz poświadczenia konta w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="059cd-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="059cd-132">Wpisz inną nazwę niż hello bieżącego konta administratora lokalnego na maszynie Wirtualnej, hello rozszerzenia VMAccess zmienia nazwę konta administratora lokalnego hello, przypisuje toothat określone hasło konta, a problemy zdarzenia wylogowania pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="059cd-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="059cd-133">Po wyłączeniu hello konta administratora lokalnego na maszynie Wirtualnej hello rozszerzenia VMAccess włączy ją.</span><span class="sxs-lookup"><span data-stu-id="059cd-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="059cd-134">Po aktualizacji przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup` toohello poświadczeń określonych.</span><span class="sxs-lookup"><span data-stu-id="059cd-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="059cd-135">**Resetuj hello w konfiguracji usługi pulpitu zdalnego**</span><span class="sxs-lookup"><span data-stu-id="059cd-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="059cd-136">Zresetuj dostęp zdalny tooyour maszyny Wirtualnej z hello [AzureRmVMAccessExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmaccessextension) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="059cd-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="059cd-137">Witaj poniższy przykład resetuje hello rozszerzenie dostępu o nazwie `myVMAccess` na powitania maszyny Wirtualnej o nazwie `myVM` w hello `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="059cd-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="059cd-138">W dowolnym momencie maszyna wirtualna może mieć tylko jednego agenta dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="059cd-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="059cd-139">pomyślnie, hello tooset hello maszyny Wirtualnej dostępu do agenta właściwości `-ForceRerun` opcja może być używana.</span><span class="sxs-lookup"><span data-stu-id="059cd-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="059cd-140">Korzystając z `-ForceRerun`, upewnij się, że toouse hello tej samej nazwy dla hello agent dostęp maszyny Wirtualnej w poprzednie polecenia.</span><span class="sxs-lookup"><span data-stu-id="059cd-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="059cd-141">Jeśli nadal nie możesz połączyć zdalnie tooyour maszyny wirtualnej, zobacz więcej czynności tootry w [Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="059cd-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="059cd-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="059cd-142">Next steps</span></span>
<span data-ttu-id="059cd-143">Jeśli hello rozszerzenia dostępu do maszyny Wirtualnej platformy Azure nie odpowiada i tooreset hello hasła, możesz [resetowania hello lokalne hasło systemu Windows w trybie offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="059cd-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="059cd-144">Ta metoda jest procesem bardziej zaawansowane i wymaga tooconnect hello wirtualnego dysku twardego hello problematyczne tooanother maszyny Wirtualnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="059cd-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="059cd-145">Wykonaj czynności hello opisanych w tym artykule najpierw, a następnie spróbuj tylko metody resetowania hasła w trybie offline hello w ostateczności.</span><span class="sxs-lookup"><span data-stu-id="059cd-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="059cd-146">Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje</span><span class="sxs-lookup"><span data-stu-id="059cd-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="059cd-147">Uzyskuj dostęp do maszyny wirtualnej platformy Azure tooan RDP lub SSH</span><span class="sxs-lookup"><span data-stu-id="059cd-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="059cd-148">Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="059cd-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

