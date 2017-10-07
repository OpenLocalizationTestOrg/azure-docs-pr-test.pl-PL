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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Usługi pulpitu zdalnego hello tooreset lub jego hasło logowania na maszynie wirtualnej Windows tworzenia przy użyciu klasycznego modelu wdrożenia hello
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Możesz również [wykonaj te kroki dla maszyn wirtualnych utworzonych za pomocą modelu wdrażania usługi Resource Manager hello](../reset-rdp.md).

Jeśli nie można połączyć maszyny wirtualnej systemu Windows tooa (VM), można zresetować hasła administratora lokalnego hello lub zresetować hello w konfiguracji usługi pulpitu zdalnego. Można użyć albo hello Azure rozszerzenia maszyny Wirtualnej dostępu do portalu lub hello w haśle hello tooreset programu Azure PowerShell.

## <a name="ways-tooreset-configuration-or-credentials"></a>Sposoby tooreset konfiguracji lub poświadczeń
Można zresetować usług pulpitu zdalnego i poświadczenia na kilka różnych sposobów, w zależności od potrzeb:

- [Resetuj przy użyciu hello portalu Azure](#azure-portal)
- [Resetuj przy użyciu programu Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
Można użyć hello [portalu Azure](https://portal.azure.com) hello tooreset usługi pulpitu zdalnego. Kliknij paski hello trzech w lewym górnym rogu hello tooexpand hello portalu menu, a następnie kliknij **maszyn wirtualnych (klasyczne)**:

![Przeglądaj w poszukiwaniu Azure maszyny Wirtualnej](./media/reset-rdp/Portal-Select-Classic-VM.png)

Wybierz maszynę wirtualną systemu Windows, a następnie kliknij przycisk **zresetować zdalnego...** . hello następujące zostanie wyświetlone okno dialogowe tooreset hello w konfiguracji pulpitu zdalnego:

![Strony konfiguracji RDP resetowania](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Można również zresetować hello nazwę użytkownika i hasło konta administratora lokalnego hello. Z maszyny Wirtualnej, kliknij przycisk **pomocy technicznej i rozwiązywania problemów** > **resetowania hasła**. zostanie wyświetlony blok resetowania hasła Hello:

![Strona Resetowanie hasła](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Po wprowadzeniu hello nową nazwę użytkownika i hasło, kliknij przycisk **zapisać**.

## <a name="vmaccess-extension-and-powershell"></a>Rozszerzenia VMAccess i programu PowerShell
Upewnij się, że Agent maszyny Wirtualnej jest zainstalowany na maszynie wirtualnej hello powitalne. Witaj rozszerzenia VMAccess nie wymaga toobe zainstalowane przed użyciem go, dopóki hello agenta maszyny Wirtualnej jest dostępna. Upewnij się, że powitalne za pomocą następującego polecenia hello jest już zainstalowany Agent maszyny Wirtualnej. (Zastępuje "myCloudService" i "myVM" hello nazwy usługi w chmurze i maszyny Wirtualnej, odpowiednio. Dowiedz się te nazwy, uruchamiając `Get-AzureVM` bez żadnych parametrów.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Jeśli hello **hosta zapisu** polecenie wyświetla **True**, hello jest zainstalowany Agent maszyny Wirtualnej. Jeśli Wyświetla **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure wpis w blogu.

Jeśli utworzono hello maszyny wirtualnej przy użyciu portalu hello, sprawdź, czy `$vm.GetInstance().ProvisionGuestAgent` zwraca **True**. Jeśli nie można ustawić za pomocą tego polecenia:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

To polecenie uniemożliwia hello następujący błąd podczas pracy hello **AzureVMExtension zestaw** w następnych krokach hello: "Udostępniania gościa musi być włączony Agent na powitania obiektu maszyny Wirtualnej przed ustawieniem rozszerzenia dostępu do maszyn wirtualnych IaaS."

### <a name="reset-hello-local-administrator-account-password"></a>**Zresetuj hasło konta administratora lokalnego hello**
Utwórz poświadczenia logowania z hello bieżąca nazwa konta administratora lokalnego i nowe hasło, a następnie uruchom hello `Set-AzureVMAccessExtension` w następujący sposób.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Wpisz inną nazwę niż hello bieżącego konta, hello rozszerzenia VMAccess zmienia nazwę konta administratora lokalnego hello, przypisuje hello hasło toothat konta, a problemy z wylogowaniem pulpitu zdalnego. Wyłączenie konta administratora lokalnego hello hello rozszerzenia VMAccess włączy ją.

Te polecenia również zresetować hello w konfiguracji usługi pulpitu zdalnego.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Resetuj hello w konfiguracji usługi pulpitu zdalnego**
tooreset hello konfiguracji usługi pulpitu zdalnego, uruchom następujące polecenie hello:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hello rozszerzenia VMAccess uruchamia dwa polecenia w maszynie wirtualnej hello:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

To polecenie włącza hello wbudowane zapory systemu Windows grupy, która zezwala na ruch przychodzący pulpitu zdalnego, który korzysta z portu 3389 protokołu TCP.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

To polecenie ustawia hello fDenyTSConnections rejestru wartość too0, włączenie połączeń pulpitu zdalnego.

## <a name="next-steps"></a>Następne kroki
Jeśli hello rozszerzenia dostępu do maszyny Wirtualnej platformy Azure nie odpowiada i tooreset hello hasła, możesz [resetowania hello lokalne hasło systemu Windows w trybie offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ta metoda jest procesem bardziej zaawansowane i wymaga tooconnect hello wirtualnego dysku twardego hello problematyczne tooanother maszyny Wirtualnej maszyny Wirtualnej. Wykonaj czynności hello opisanych w tym artykule najpierw, a następnie spróbuj tylko metody resetowania hasła w trybie offline hello w ostateczności.

[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Uzyskuj dostęp do maszyny wirtualnej platformy Azure tooan RDP lub SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Rozwiązywanie problemów z pulpitu zdalnego połączenia tooa opartych na systemie Windows Azure maszyny wirtualnej](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

