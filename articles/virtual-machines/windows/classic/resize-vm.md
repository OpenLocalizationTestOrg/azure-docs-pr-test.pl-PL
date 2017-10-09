---
title: "aaaResize maszyny Wirtualnej systemu Windows w hello klasycznego modelu wdrażania - Azure | Dokumentacja firmy Microsoft"
description: "Zmień rozmiar maszyny wirtualnej systemu Windows utworzonej w hello klasycznego modelu wdrażania, przy użyciu programu Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Zmień rozmiar maszyny Wirtualnej systemu Windows utworzonych w hello klasycznego modelu wdrażania
W tym artykule opisano, jak tooresize maszyny Wirtualnej systemu Windows, utworzonej w hello klasycznego modelu wdrażania przy użyciu programu Azure Powershell.

Podczas określania hello tooresize możliwości maszyny Wirtualnej, istnieją dwa pojęcia kontrolujące hello zakres maszyny wirtualnej hello tooresize dostępne rozmiary. koncepcja pierwszy Hello jest hello regionu, w którym wdrożonej maszyny Wirtualnej. Witaj listę dostępnych rozmiarów maszyny Wirtualnej w regionie jest karcie usług hello strony sieci web hello regiony platformy Azure. koncepcja drugi Hello jest sprzętem fizycznym hello obecnie udostępnia maszyny Wirtualnej. serwery fizyczne Hello hostingu maszyn wirtualnych są grupowane w klastrach wspólnej sprzętu fizycznego. Metoda Hello zmiany rozmiaru maszyny Wirtualnej różni się w zależności od, jeśli hello żądany nowy rozmiar maszyny Wirtualnej jest obsługiwany przez hello sprzętu klastra aktualnie obsługujący hello maszyny Wirtualnej.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Możesz również [Zmień rozmiar maszyny Wirtualnej utworzonej w modelu wdrażania usługi Resource Manager hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Dodaj swoje konto
Należy skonfigurować toowork programu Azure PowerShell z klasycznym zasobów platformy Azure. Wykonaj kroki hello poniżej tooconfigure zasoby klasyczne toomanage programu Azure PowerShell.

1. W wierszu polecenia programu PowerShell hello, wpisz `Add-AzureAccount` i kliknij przycisk **Enter**. 
2. Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**. 
3. Wpisz hasło powitania dla Twojego konta. 
4. Kliknij przycisk **Zaloguj**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Zmiana rozmiaru w hello sam sprzętu klastra
tooresize rozmiar tooa maszyny Wirtualnej dostępne w klastrze sprzętu hello hosting hello maszyny Wirtualnej, wykonaj hello następujące kroki.

1. Uruchom hello następującego polecenia programu PowerShell dostępnych w klastrze sprzętu hello hosting usługi hello w chmurze, który zawiera rozmiarów maszyn wirtualnych hello toolist hello maszyny Wirtualnej.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Witaj uruchom następujące polecenia hello tooresize maszyny Wirtualnej.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Zmiana rozmiaru w nowym klastrze sprzętu
tooresize rozmiar tooa maszyny Wirtualnej nie jest dostępna w hello sprzętu klastra hostingu hello maszyny Wirtualnej, hello usługa w chmurze i wszystkich maszyn wirtualnych w usłudze w chmurze hello muszą zostać ponownie utworzone. Każdą usługę w chmurze jest hostowanych w klastrze pojedynczego sprzętu, więc wszystkie maszyny wirtualne w usłudze w chmurze hello musi mieć rozmiar, który jest obsługiwany w klastrze sprzętu. Witaj następujące kroki opisano, jak tooresize maszyn wirtualnych przez usunięcie i ponowne utworzenie następnie hello chmury usługi.

1. Uruchom hello następującego środowiska PowerShell polecenie toolist hello rozmiarów maszyn wirtualnych dostępne w regionie hello. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Zanotuj wszystkie ustawienia konfiguracji dla każdej maszyny Wirtualnej w usłudze w chmurze hello zawierającą hello wirtualna toobe zmiany rozmiaru. 
3. Usuń wszystkie maszyny wirtualne w usłudze w chmurze hello wybór hello opcja tooretain hello dysków dla każdej maszyny Wirtualnej.
4. Utwórz ponownie hello wirtualna toobe zmiany rozmiaru przy użyciu hello żądany rozmiar maszyny Wirtualnej.
5. Utwórz ponownie wszystkich innych maszyn wirtualnych będących hello w usłudze w chmurze przy użyciu rozmiaru maszyny Wirtualnej dostępne w klastrze sprzętu hello teraz hosting hello usługi w chmurze.

Przykładowy skrypt do usuwania i ponowne utworzenie usługi w chmurze przy użyciu nowego rozmiaru maszyny Wirtualnej można znaleźć [tutaj](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Następne kroki
* [Zmień rozmiar maszyny Wirtualnej utworzonej w modelu wdrażania usługi Resource Manager hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

