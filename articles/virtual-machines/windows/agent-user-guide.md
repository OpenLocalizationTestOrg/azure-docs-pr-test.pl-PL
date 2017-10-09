---
title: "Omówienie agenta maszyny wirtualnej aaaAzure | Dokumentacja firmy Microsoft"
description: "Omówienie agenta maszyny wirtualnej platformy Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Omówienie usługi Azure agenta maszyny wirtualnej

Hello agenta maszyny wirtualnej programu Microsoft Azure (AM Agent) jest zabezpieczonych, lekkie procesu, który zarządza wirtualna interakcji z hello Azure kontrolera sieci szkieletowej. Witaj agenta maszyny Wirtualnej ma podstawową rolą włączenie i wykonywania rozszerzenia maszyny wirtualnej platformy Azure. Włączanie rozszerzenia maszyny Wirtualnej po konfiguracji wdrożenia maszyn wirtualnych, takie jak instalowanie i konfigurowanie oprogramowania. Rozszerzenia maszyn wirtualnych również włączyć funkcje odzyskiwania, np. zresetowania hasła administracyjnego hello maszyny wirtualnej. Bez hello Agent maszyny Wirtualnej nie można uruchomić rozszerzenia maszyny wirtualnej.

Ten dokument zawiera szczegóły dotyczące instalacji, wykrywanie i usuwanie hello agenta maszyny wirtualnej Azure.

## <a name="install-hello-vm-agent"></a>Zainstaluj hello agenta maszyny Wirtualnej

### <a name="azure-gallery-image"></a>Obraz w galerii Azure

Hello Agent maszyny Wirtualnej jest instalowana domyślnie na żadnej maszyny wirtualnej systemu Windows wdrożone z obrazu w galerii Azure. Podczas wdrażania obrazu galerii Azure z hello portalu, programu PowerShell, interfejsu wiersza polecenia lub szablonu usługi Azure Resource Manager, można zainstalować hello jest również Agent maszyny Wirtualnej. 

### <a name="manual-installation"></a>Instalacja ręczna

agent maszyny Wirtualnej systemu Windows Hello można ręcznie zainstalować za pomocą pakietu Instalatora Windows. Instalacja ręczna może być konieczne, podczas tworzenia obrazu niestandardowego maszyny wirtualnej, który zostanie wdrożony na platformie Azure. toomanually hello Zainstaluj agenta maszyny Wirtualnej systemu Windows, Pobierz Instalator agenta maszyny Wirtualnej hello z tej lokalizacji [Pobierz agenta maszyny Wirtualnej systemu Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789). 

Witaj agenta maszyny Wirtualnej mogą być instalowane przez dwukrotne kliknięcie pliku Instalatora windows hello. Automatyczna lub z instalacji nienadzorowanej instalacji agenta maszyny Wirtualnej hello Uruchom hello następujące polecenia.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Wykryj hello agenta maszyny Wirtualnej

### <a name="powershell"></a>PowerShell

Moduł programu PowerShell usługi Azure Resource Manager Hello może być używane tooretrieve informacji o maszynach wirtualnych platformy Azure. Uruchomiona `Get-AzureRmVM` zwraca dość nieco informacji w tym hello udostępniania stanu hello Agent maszyny Wirtualnej.

```PowerShell
Get-AzureRmVM
```

Witaj poniżej znajduje się tylko podzbiór hello `Get-AzureRmVM` danych wyjściowych. Powiadomienie hello `ProvisionVMAgent` zagnieżdżona właściwość `OSProfile`, ta właściwość może być toodetermine używane, jeśli hello agenta maszyny Wirtualnej został wdrożony toohello maszyny wirtualnej.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Witaj następującego skryptu może być używane tooreturn listę krótkie nazwy maszyn wirtualnych i stan hello hello agenta maszyny Wirtualnej.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Ręczne wykrywania

Gdy zalogowany tooa maszyny Wirtualnej systemu Windows Azure, Menedżer zadań mogą być używane tooexamine uruchomionych procesów. toocheck dla hello agenta maszyny Wirtualnej Azure, otwórz Menedżera zadań > kliknij kartę Szczegóły hello i wyszukaj nazwę procesu `WindowsAzureGuestAgent.exe`. obecność Hello tego procesu wskazuje, że hello agenta maszyny Wirtualnej jest zainstalowany.

## <a name="upgrade-hello-vm-agent"></a>Witaj uaktualniania agenta maszyny Wirtualnej

Hello Azure VM Agent dla systemu Windows zostanie automatycznie uaktualniony. Nowe maszyny wirtualne są wdrożone tooAzure, otrzymają hello najnowsza wersja agenta maszyny Wirtualnej. Niestandardowe obrazy maszyny Wirtualnej należy ręcznie zaktualizowanych tooinclude hello nowego agenta maszyny Wirtualnej.
