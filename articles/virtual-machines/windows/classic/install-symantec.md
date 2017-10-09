---
title: aaaInstall Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfigurować rozszerzenia zabezpieczeń firmy Symantec Endpoint Protection hello na nowej lub istniejącej maszyny Wirtualnej Azure utworzone za pomocą hello klasycznego modelu wdrożenia."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Jak tooinstall i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

W tym artykule opisano sposób tooinstall i skonfigurować powitania klienta firmy Symantec Endpoint Protection na istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server. Ta pełnego klienta zawiera usług, takich jak wirusów i ochrony przed programami szpiegującymi, zapory i zapobiegania nieautoryzowanego dostępu. powitania klienta jest instalowany jako rozszerzenia zabezpieczeń przy użyciu hello agenta maszyny Wirtualnej.

Jeśli masz istniejącą subskrypcję od firmy Symantec dla rozwiązania lokalnego umożliwia tooprotect maszynach wirtualnych platformy Azure. Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej. Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz [Symantec Endpoint Protection na platformie Azure przez firmę Microsoft][Symantec]. Ta strona zawiera również linki toolicensing informacje i instrukcje dotyczące instalowania powitania klienta, jeśli już masz klienta firmy Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Zainstaluj Symantec Endpoint Protection na istniejącej maszyny Wirtualnej
Przed rozpoczęciem należy hello następujące czynności:

* Witaj modułu Azure PowerShell, wersja 0.8.2 lub nowszym, na komputerze pracy. Można sprawdzić wersji hello programu Azure PowerShell, zainstalowanym z hello **azure Get-Module | wersja formatu tabeli** polecenia. Aby uzyskać instrukcje i toohello łącze najnowszej wersji, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell][PS]. Zaloguj się przy użyciu subskrypcji platformy Azure tooyour `Add-AzureAccount`.
* Witaj agenta maszyny Wirtualnej z systemem hello maszyny wirtualnej platformy Azure.

Po pierwsze sprawdzenie hello, że Agent maszyny Wirtualnej jest już zainstalowana na maszynie wirtualnej hello. Wypełnij hello nazwa usługi w chmurze i nazwy maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora hello. Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków.

> [!TIP]
> Jeśli nie znasz nazwy maszyny wirtualnej usługi chmury hello i uruchom **Get-AzureVM** toolist hello nazwy dla wszystkich maszyn wirtualnych w ramach Twojej bieżącej subskrypcji.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Jeśli hello **hosta zapisu** polecenie wyświetla **True**, hello jest zainstalowany Agent maszyny Wirtualnej. Jeśli Wyświetla **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello Azure wpis w blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2][Agent].

Jeśli hello agenta maszyny Wirtualnej jest zainstalowany, należy uruchomić te polecenia tooinstall hello Symantec Endpoint Protection agenta.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify, który hello rozszerzenia zabezpieczeń firmy Symantec został zainstalowany i jest aktualne:

1. Zaloguj się na toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [jak tooLog na tooa maszyny wirtualnej z systemu Windows Server][Logon].
2. Dla systemu Windows Server 2008 R2, kliknij przycisk **Start > Symantec Endpoint Protection**. Dla systemu Windows Server 2012 lub Windows Server 2012 R2 z ekranu startowego hello, wpisz **firmy Symantec**, a następnie kliknij przycisk **Symantec Endpoint Protection**.
3. Z hello **stan** kartę hello **stan Symantec Endpoint Protection** okna, stosowania aktualizacji lub uruchom ponownie w razie potrzeby.

## <a name="additional-resources"></a>Dodatkowe zasoby
[Jak tooLog na tooa maszyny wirtualnej z systemu Windows Server][Logon]

[Maszyna wirtualna platformy Azure rozszerzeń i funkcji][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
