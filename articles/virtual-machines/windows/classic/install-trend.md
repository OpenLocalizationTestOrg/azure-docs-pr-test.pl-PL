---
title: "aaaInstall Trend Micro głębokie zabezpieczeń na maszynie Wirtualnej | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooinstall i skonfigurować zabezpieczenia Trend Micro maszyny Wirtualnej utworzonej z hello klasycznego modelu wdrożenia na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Jak tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej systemu Windows
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

W tym artykule opisano sposób tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na nowej lub istniejącej maszyny wirtualnej (VM) system operacyjny Windows Server. Głębokie zabezpieczeń jako usługa obejmuje ochrony przed złośliwym oprogramowaniem, zapory systemu zapobiegania nieautoryzowanego dostępu i kontroli integralności.

Witaj klient jest instalowany jako rozszerzenie zabezpieczeń za pomocą hello agenta maszyny Wirtualnej. Na nowej maszyny wirtualnej należy zainstalować hello głębokie Agent zabezpieczeń, jako hello agenta maszyny Wirtualnej jest tworzona automatycznie przez hello portalu Azure.

Istniejącej maszyny Wirtualnej utworzone przy użyciu klasycznego portalu hello, hello wiersza polecenia platformy Azure lub programu PowerShell może nie mieć agenta maszyny Wirtualnej. Dla istniejącej maszyny wirtualnej, która nie ma hello agenta maszyny Wirtualnej należy toodownload i najpierw go zainstalować. W tym artykule opisano zarówno sytuacji.

Jeśli masz bieżącej subskrypcji z Trend Micro dla rozwiązania lokalnego, można użyć jej toohelp ochrony maszyn wirtualnych platformy Azure. Jeśli nie jesteś klientem jeszcze, można założyć dla subskrypcji wersji próbnej. Aby uzyskać więcej informacji o tym rozwiązaniu, zobacz Trend Micro blogu hello [zabezpieczeń firmy Microsoft Azure VM Agent rozszerzenia dla bezpośrednich](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Zainstaluj hello głębokie Agent zabezpieczeń na nowej maszyny Wirtualnej

Witaj [portalu Azure](http://portal.azure.com) umożliwia instalowanie rozszerzenia zabezpieczeń Trend Micro hello, korzystając z obrazu z hello **Marketplace** maszyny wirtualnej hello toocreate. Jeśli tworzysz jednej maszyny wirtualnej za pomocą portalu hello jest łatwy sposób ochrony tooadd z Trend Micro.

Za pomocą wpisu z hello **Marketplace** Otwiera kreatora, który pomaga skonfigurować maszynę wirtualną hello. Użyj hello **ustawienia** bloku, panel trzeci hello hello kreatora hello tooinstall Trend Micro rozszerzenia zabezpieczeń.  Aby uzyskać ogólne instrukcje, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure hello](tutorial.md).

Jeśli otrzymasz toohello **ustawienia** bloku kreatora hello hello następujące kroki:

1. Kliknij przycisk **rozszerzenia**, następnie kliknij przycisk **dodanie rozszerzenia** w hello następne okienko.

   ![Rozpocznij dodawanie rozszerzenia hello][1]

2. Wybierz **głębokie Agent zabezpieczeń** w hello **nowy zasób** okienka. W okienku głębokie Agent zabezpieczeń powitania kliknij **Utwórz**.

   ![Identyfikowanie agenta głębokie zabezpieczeń][2]

3. Wprowadź hello **identyfikator dzierżawy** i **hasło aktywacji dzierżawy** hello rozszerzenia. Opcjonalnie możesz wprowadzić **identyfikator zasad zabezpieczeń**. Następnie kliknij przycisk **OK** tooadd powitania klienta.

   ![Podaj szczegóły rozszerzenia][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Zainstaluj hello głębokie Agent zabezpieczeń na istniejącej maszyny Wirtualnej
agent hello tooinstall na istniejącej maszyny Wirtualnej, należy hello następujące elementy:

* Witaj modułu Azure PowerShell, wersja 0.8.2 lub nowszej, zainstalowanych na komputerze lokalnym. Można sprawdzić wersji hello programu Azure PowerShell, który został zainstalowany przy użyciu hello **azure Get-Module | wersja formatu tabeli** polecenia. Aby uzyskać instrukcje i toohello łącze najnowszej wersji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Zaloguj się przy użyciu subskrypcji platformy Azure tooyour `Add-AzureAccount`.
* Witaj Agent maszyny Wirtualnej został zainstalowany na powitania docelowej maszyny wirtualnej.

Po pierwsze sprawdzenie hello, że Agent maszyny Wirtualnej jest już zainstalowana. Wypełnij hello nazwa usługi w chmurze i nazwy maszyny wirtualnej, a następnie uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell poziomie administratora hello. Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Jeśli nie znasz hello usługi w chmurze i nazwy maszyny wirtualnej, należy uruchomić **Get-AzureVM** toodisplay, że informacje dla wszystkich hello maszyn wirtualnych w ramach Twojej bieżącej subskrypcji.

Jeśli hello **hosta zapisu** polecenie zwraca **True**, hello jest zainstalowany Agent maszyny Wirtualnej. Jeśli zmienna zwraca **False**, zobacz instrukcje hello i toohello łącza, Pobierz w hello Azure wpis w blogu [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Jeśli hello agenta maszyny Wirtualnej jest zainstalowany, uruchom następujące polecenia.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Następne kroki
Trwa kilka minut, aż toostart agenta hello uruchomiona po jej zainstalowaniu. Po wykonaniu tej należy tooactivate głębokie zabezpieczeń na maszynie wirtualnej hello, można nim zarządzać za głębokie Menedżera zabezpieczeń. Zobacz następujące artykuły, aby uzyskać dodatkowe instrukcje hello:

* Trend w artykule o tym rozwiązaniu [Instant-On Cloud Security platformy Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [przykładowy skrypt programu Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) maszyny wirtualnej hello tooconfigure
* [Instrukcje](http://go.microsoft.com/fwlink/?LinkId=404099) hello próbki

## <a name="additional-resources"></a>Dodatkowe zasoby
[Jak toolog na tooa maszyny wirtualnej z systemem Windows Server]

[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Jak toolog na tooa maszyny wirtualnej z systemem Windows Server]:connect-logon.md
[Rozszerzenia maszyny Wirtualnej platformy Azure i funkcje]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
