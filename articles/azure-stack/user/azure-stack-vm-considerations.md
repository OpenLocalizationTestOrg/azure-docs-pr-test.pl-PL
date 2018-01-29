---
title: "Różnice i zagadnienia dotyczące maszyn wirtualnych w stosie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat różnic i zagadnienia dotyczące podczas pracy z maszynami wirtualnymi Azure stosu."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 6613946D-114C-441A-9F74-38E35DF0A7D7
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2018
ms.author: brenduns
ms.openlocfilehash: 6eafa2a5058ef1309cbf50be069ea1bb12f7e5b9
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Zagadnienia dotyczące maszyn wirtualnych Azure stosu

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Maszyny wirtualne są na żądanie, skalowalnych zasobów obliczeniowych oferowane przez stos Azure. Korzystając z maszyn wirtualnych, należy zrozumieć, czy istnieją różnice między stosie Azure i funkcje, które są dostępne w systemie Azure. Ten artykuł zawiera omówienie unikatowy zagadnień dotyczących maszyn wirtualnych i jego funkcji w stosie Azure. Aby uzyskać informacje ogólne różnice między stosu Azure i usługi Azure, zobacz [kluczowe zagadnienia dotyczące](azure-stack-considerations.md) artykułu.

## <a name="cheat-sheet-virtual-machine-differences"></a>Ściągawka: różnice maszyny wirtualnej

| Cecha | Azure (globalna) | Azure Stack |
| --- | --- | --- |
| Obrazy maszyny wirtualnej | W portalu Azure Marketplace zawiera obrazy, których można użyć do utworzenia maszyny wirtualnej. Zobacz [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) strony w celu wyświetlenia listy obrazów, które są dostępne w portalu Azure Marketplace. | Domyślnie nie ma żadnych obrazów dostępne w witrynie marketplace stosu Azure. Administrator chmury Azure stosu należy opublikować lub pobrać obrazów do stosu Azure marketplace, zanim użytkownicy mogą korzystać z nich. |
| Rozmiary maszyn wirtualnych | Azure obsługuje różnych rozmiarów maszyn wirtualnych. Aby dowiedzieć się więcej na temat dostępne rozmiary i opcji, zapoznaj się [rozmiary maszyn wirtualnych systemu Windows](../../virtual-machines/virtual-machines-windows-sizes.md) i [rozmiarów maszyn wirtualnych systemu Linux](../../virtual-machines/linux/sizes.md) tematów. | Stos Azure obsługuje podzbiór rozmiarów maszyn wirtualnych, które są dostępne w systemie Azure. Aby wyświetlić listę obsługiwanych rozmiarów, zobacz [rozmiarów maszyn wirtualnych](#virtual-machine-sizes) sekcji tego artykułu. |
| Przydziały maszyny wirtualnej | [Limity przydziału](../../azure-subscription-service-limits.md#service-specific-limits) są ustawiane przez firmę Microsoft | Administrator chmury Azure stosu przypisać przydziały przed oferują maszyn wirtualnych dla użytkowników. |
| Rozszerzenia maszyny wirtualnej |Azure obsługuje wiele rozszerzeń maszyny wirtualnej. Aby dowiedzieć się więcej o dostępnych rozszerzeń, zapoznaj się [rozszerzenia maszyn wirtualnych i funkcji](../../virtual-machines/windows/extensions-features.md) artykułu.| Stos Azure obsługuje podzbiór rozszerzeń, które są dostępne w systemie Azure i rozszerzenia o określonych wersji. Administrator chmury Azure stosu może zdecydować, które rozszerzenia udostępniane na rzecz własnych użytkowników. Aby wyświetlić listę obsługiwanych rozszerzeń, zobacz [rozszerzenia maszyny wirtualnej](#virtual-machine-extensions) sekcji tego artykułu. |
| Sieć maszyny wirtualnej | Publiczne adresy IP przypisane do dzierżawy maszyny wirtualnej są dostępne za pośrednictwem Internetu.<br><br><br>Maszyny wirtualne platformy Azure ma stały nazwy DNS | Publiczne adresy IP przypisane do maszyny wirtualnej dzierżawcy są dostępne tylko w środowisku Azure stosu Development Kit. Użytkownik musi mieć dostęp do zestaw deweloperski stosu Azure za pośrednictwem [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) lub [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) nawiązać połączenia z maszyny wirtualnej, która jest tworzona w stosie Azure.<br><br>Maszyny wirtualne utworzone w ramach określonego wystąpienia stosu Azure mają nazw DNS na podstawie wartości, który został skonfigurowany przez administratora chmury. |
| Magazyn maszyny wirtualnej | Obsługuje [dyskach zarządzanych.](../../virtual-machines/windows/managed-disks-overview.md) | Dyski zarządzane nie są jeszcze obsługiwane w stosie Azure. |
| Wersje interfejsu API | Platforma Azure ma zawsze najnowsze wersje interfejsu API dla wszystkich funkcji maszyny wirtualnej. | Stos Azure obsługuje określonych usług platformy Azure i określonych wersji interfejsu API dla tych usług. Aby wyświetlić listę obsługiwanych wersji interfejsu API, zobacz [wersji interfejsu API](#api-versions) sekcji tego artykułu. |
|Zestawy dostępności maszyny wirtualnej|Wiele domen błędów (2 lub 3 dla regionu)<br>Wiele domen aktualizacji<br>Obsługa dysku zarządzanego|Domena awarii jednego<br>Jedna aktualizacja domeny<br>Brak obsługi dysków zarządzanych|
|Zestawy skalowania maszyn wirtualnych|Obsługiwane automatycznego skalowania|Automatycznego skalowania nie jest obsługiwane.<br>Dodaj więcej wystąpień do skali ustawić za pomocą portalu, szablony usługi Resource Manager lub programu PowerShell.

## <a name="virtual-machine-sizes"></a>Rozmiary maszyn wirtualnych

Stos Azure obsługuje następujące wymiary:

| Typ | Rozmiar | Zakres obsługiwanych rozmiarów. |
| --- | --- | --- |
|Zastosowania ogólne |Podstawowa A|A0 - A4|
|Zastosowania ogólne |Standard A|A0–A7|
|Zastosowania ogólne |Seria D|D1 - D4|
|Zastosowania ogólne |Seria Dv2|D1_v2 - D5_v2|
|Zastosowania ogólne |Seria DS|DS1 - DS4|
|Zastosowania ogólne |Seria DSv2|DS1_v2 - DS5_v2|
|Optymalizacja pod kątem pamięci|Seria DS|DS11 - DS14|
|Optymalizacja pod kątem pamięci |Seria DSv2|DS11_v2 - DS14_v2|

Rozmiary maszyn wirtualnych i ich ilości zasobów są spójne stosu Azure i na platformie Azure. Na przykład ten spójności zawiera ilość pamięci, liczby rdzeni i numer/rozmiaru dysków z danymi, które mogą zostać utworzone. Jednak wydajność ten sam rozmiar maszyny Wirtualnej Azure stosu zależy od podstawowej właściwości określonym środowisku Azure stosu.

## <a name="virtual-machine-extensions"></a>Rozszerzenia maszyny wirtualnej

 Stos Azure obsługuje następujące wersje rozszerzenia maszyny wirtualnej:

![Rozszerzenia maszyn wirtualnych](media/azure-stack-vm-considerations/vm-extensions.png)

Użyj następującego skryptu programu PowerShell można pobrać listy rozszerzeń maszyny wirtualnej, które są dostępne w środowisku Azure stosu:

```powershell
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize
```

## <a name="api-versions"></a>Wersje interfejsu API

Funkcje maszyny wirtualnej w stosie Azure obsługuje następujące wersje interfejsu API:

![Typy zasobów maszyny Wirtualnej](media/azure-stack-vm-considerations/vm-resoource-types.png)

Poniższy skrypt programu PowerShell umożliwia pobieranie wersji interfejsu API dla funkcji maszyny wirtualnej, które są dostępne w środowisku Azure stosu:

```powershell
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
Lista obsługiwane typy zasobów i wersje interfejsu API może się różnić, jeśli operatorowi chmury aktualizacji środowiska Azure stosu do nowszej wersji.

## <a name="next-steps"></a>Kolejne kroki

[Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell w stosie Azure](azure-stack-quick-create-vm-windows-powershell.md)
