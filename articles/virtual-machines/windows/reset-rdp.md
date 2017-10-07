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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Jak tooreset hello usługi pulpitu zdalnego lub jego hasło logowania na maszynie wirtualnej systemu Windows
Jeśli nie można połączyć maszyny wirtualnej systemu Windows tooa (VM), można zresetować hasła administratora lokalnego hello lub zresetować hello w konfiguracji usługi pulpitu zdalnego. Można użyć albo hello Azure rozszerzenia maszyny Wirtualnej dostępu do portalu lub hello w haśle hello tooreset programu Azure PowerShell. Jeśli używasz programu PowerShell, upewnij się, że masz hello [najnowsze modułu PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview) i będą one podpisane w tooyour subskrypcji platformy Azure. Możesz również [wykonaj te kroki dla maszyn wirtualnych utworzonych za pomocą klasycznego modelu wdrożenia hello](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Sposoby tooreset konfiguracji lub poświadczeń
Można zresetować usług pulpitu zdalnego i poświadczenia na kilka różnych sposobów, w zależności od potrzeb:

- [Resetuj przy użyciu hello portalu Azure](#azure-portal)
- [Resetuj przy użyciu programu Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
Kliknij paski hello trzech w lewym górnym rogu hello tooexpand hello portalu menu, a następnie kliknij **maszyn wirtualnych**:

![Przeglądaj w poszukiwaniu Azure maszyny Wirtualnej](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Zresetuj hasło konta administratora lokalnego hello**

Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**. zostanie wyświetlony blok resetowania hasła Hello:

![Strona Resetowanie hasła](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Wprowadź nazwę użytkownika hello i nowe hasło, a następnie kliknij przycisk **aktualizacji**. Spróbuj ponownie połączyć tooyour maszyny Wirtualnej.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Resetuj hello w konfiguracji usługi pulpitu zdalnego**

Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**. Blok resetowania hasła Hello jest wyświetlany. 

![Zresetowanie konfiguracji RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Wybierz **Resetowanie tylko konfiguracji** z menu rozwijanego hello, następnie kliknij przycisk **aktualizacji**. Spróbuj ponownie połączyć tooyour maszyny Wirtualnej.


## <a name="vmaccess-extension-and-powershell"></a>Rozszerzenia VMAccess i programu PowerShell
Upewnij się, że masz hello [najnowsze modułu PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview) i będą one podpisane w tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` polecenia cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**Zresetuj hasło konta administratora lokalnego hello**
Resetowanie hello administratora hasło lub nazwa użytkownika z hello [AzureRmVMAccessExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmaccessextension) polecenia cmdlet programu PowerShell. Utwórz poświadczenia konta w następujący sposób:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Wpisz inną nazwę niż hello bieżącego konta administratora lokalnego na maszynie Wirtualnej, hello rozszerzenia VMAccess zmienia nazwę konta administratora lokalnego hello, przypisuje toothat określone hasło konta, a problemy zdarzenia wylogowania pulpitu zdalnego. Po wyłączeniu hello konta administratora lokalnego na maszynie Wirtualnej hello rozszerzenia VMAccess włączy ją.

Po aktualizacji przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup` toohello poświadczeń określonych.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Resetuj hello w konfiguracji usługi pulpitu zdalnego**
Zresetuj dostęp zdalny tooyour maszyny Wirtualnej z hello [AzureRmVMAccessExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmaccessextension) polecenia cmdlet programu PowerShell. Witaj poniższy przykład resetuje hello rozszerzenie dostępu o nazwie `myVMAccess` na powitania maszyny Wirtualnej o nazwie `myVM` w hello `myResourceGroup` grupy zasobów:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> W dowolnym momencie maszyna wirtualna może mieć tylko jednego agenta dostęp do maszyny Wirtualnej. pomyślnie, hello tooset hello maszyny Wirtualnej dostępu do agenta właściwości `-ForceRerun` opcja może być używana. Korzystając z `-ForceRerun`, upewnij się, że toouse hello tej samej nazwy dla hello agent dostęp maszyny Wirtualnej w poprzednie polecenia.

Jeśli nadal nie możesz połączyć zdalnie tooyour maszyny wirtualnej, zobacz więcej czynności tootry w [Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Następne kroki
Jeśli hello rozszerzenia dostępu do maszyny Wirtualnej platformy Azure nie odpowiada i tooreset hello hasła, możesz [resetowania hello lokalne hasło systemu Windows w trybie offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ta metoda jest procesem bardziej zaawansowane i wymaga tooconnect hello wirtualnego dysku twardego hello problematyczne tooanother maszyny Wirtualnej maszyny Wirtualnej. Wykonaj czynności hello opisanych w tym artykule najpierw, a następnie spróbuj tylko metody resetowania hasła w trybie offline hello w ostateczności.

[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Uzyskuj dostęp do maszyny wirtualnej platformy Azure tooan RDP lub SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

