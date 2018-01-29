---
title: "Zagadnienia dotyczące zestawy skalowania maszyny wirtualnej platformy Azure projektu | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat projektowania sieci zestawy skalowania maszyny wirtualnej Azure"
keywords: zestawy skalowania maszyny wirtualnej w przypadku maszyny wirtualnej systemu Linux
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: efb9f7f7daa5dbb8cd3120b21ef812106fdc7fb9
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="design-considerations-for-scale-sets"></a>Zagadnienia dotyczące projektowania dla zestawów skalowania
W tym artykule omówiono zagadnienia dotyczące projektowania dla zestawy skalowania maszyny wirtualnej. Informacje są zestawy skalowania maszyny wirtualnej, można znaleźć w [omówienie zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).

## <a name="when-to-use-scale-sets-instead-of-virtual-machines"></a>Kiedy należy używać skali ustawia zamiast maszyn wirtualnych?
Ogólnie rzecz biorąc zestawy skalowania są przydatne w przypadku wdrażania infrastruktury wysokiej dostępności której zestaw maszyn mają podobnej konfiguracji. Jednak niektóre funkcje są dostępne tylko w zestawach skali, podczas gdy inne funkcje są dostępne tylko w maszynach wirtualnych. Aby można było podjąć świadomej decyzji o tym, kiedy należy używać tych technologii, należy najpierw wykonać przyjrzeć się niektóre z często używane funkcje, które są dostępne w zestawy skalowania, ale nie do maszyn wirtualnych:

### <a name="scale-set-specific-features"></a>Funkcje specyficzne dla zestawu skalowania

- Po określeniu zestawu skali konfiguracji, należy zaktualizować właściwości "pojemność", aby wdrożyć więcej maszyn wirtualnych jednocześnie. Jest znacznie prostsze niż napisanie skryptu do organizowania wdrażania wiele poszczególnych maszyn wirtualnych jednocześnie.
- Możesz [umożliwia automatycznie skalować zestaw skalowania automatycznego skalowania Azure](./virtual-machine-scale-sets-autoscale-overview.md) , ale nie poszczególnych maszyn wirtualnych.
- Możesz [maszyn wirtualnych zestawu skalowania odtworzenia z obrazu](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) , ale [nie poszczególnych maszyn wirtualnych](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Możesz [nadmiernej aprowizacji](./virtual-machine-scale-sets-design-overview.md) zestawu skalowania maszyn wirtualnych dla bardziej niezawodne i szybsze czas wdrażania. Nie można w tym poszczególnych maszyn wirtualnych, chyba że pisanie kodu niestandardowego, w tym celu.
- Można określić [uaktualnienia zasad](./virtual-machine-scale-sets-upgrade-scale-set.md) ułatwia wdrażanie uaktualnień na maszynach wirtualnych w zestawie skali. Poszczególnych maszyn wirtualnych użytkownik musi organizowania aktualizacji samodzielnie.

### <a name="vm-specific-features"></a>Funkcje specyficzne dla maszyny Wirtualnej

Niektóre funkcje są obecnie dostępne tylko na maszynach wirtualnych:

- Do określonych poszczególnych maszyn wirtualnych można dołączać dysków z danymi, ale dyski dołączone danych są skonfigurowane dla wszystkich maszyn wirtualnych w zestawie skalowania.
- Dyski danych niepustym można dołączyć do poszczególnych maszyn wirtualnych, ale nie maszyn wirtualnych w zestawie skalowania.
- Można migawek poszczególnych maszyn wirtualnych, ale nie maszyny Wirtualnej w zestawie skalowania.
- Można przechwycić obrazu z poszczególnych maszyn wirtualnych, ale nie z maszyny Wirtualnej w zestawie skalowania.
- Można przeprowadzić migrację poszczególnych maszyn wirtualnych z macierzystych dyskach do dysków zarządzanych, ale nie możesz tego zrobić dla maszyn wirtualnych w zestawie skalowania.
- Można przypisać publicznych adresów IP protokołu IPv6 do poszczególnych kart sieciowych maszyny Wirtualnej, ale nie można zrobić dla maszyn wirtualnych w zestawie skalowania. Można przypisać publicznych adresów IP protokołu IPv6 można załadować równoważenia przed albo poszczególnych maszyn wirtualnych lub zestawu skalowania maszyn wirtualnych.

## <a name="storage"></a>Magazyn

### <a name="scale-sets-with-azure-managed-disks"></a>Zestawy skalowania z dyskami zarządzane Azure
Zestawy skalowania można tworzyć za pomocą [dysków zarządzanych Azure](../virtual-machines/windows/managed-disks-overview.md) zamiast kont tradycyjnego magazynu Azure. Dyski zarządzane zapewniają następujące korzyści:
- Nie trzeba wstępnie utworzyć zestaw kont magazynu Azure dla zestawu skalowania maszyn wirtualnych.
- Można zdefiniować [dołączone dyski danych](virtual-machine-scale-sets-attached-disks.md) dla maszyn wirtualnych w skali sieci należy ustawić.
- Zestawy skalowania można skonfigurować do [obsługuje maksymalnie 1000 maszyn wirtualnych w zestawie](virtual-machine-scale-sets-placement-groups.md). 

Jeśli masz istniejący szablon, możesz również [zaktualizować szablon do zarządzanych dysków](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Magazynów zarządzana przez użytkownika
Zestaw skali, który nie jest zdefiniowana z dysków zarządzanych Azure korzysta z kont magazynu utworzonych przez użytkownika do przechowywania dysków systemu operacyjnego maszyn wirtualnych w zestawie. Aby osiągnąć maksymalną we/wy, a także korzystać z zaleca się stosunku 20 maszyn wirtualnych na konto magazynu lub mniej _nadmiarowe Inicjowanie obsługi administracyjnej_ (patrz poniżej). Zalecane jest również rozłożyć znaków początku nazwy konta magazynu na alfabetu. Grozi to pomaga rozkładu obciążenia w różnych systemach wewnętrznego. 


## <a name="overprovisioning"></a>Nadmiarowe Inicjowanie obsługi administracyjnej
Skala obecnie ustawia domyślną wartość "wymaga" maszyn wirtualnych. Z nadmiarowe Inicjowanie obsługi administracyjnej włączona, skali Ustaw faktycznie obroty zapasowych więcej maszyn wirtualnych nie zostanie wyświetlony monit o podanie, a następnie usuwa dodatkowe maszyny wirtualne, gdy żądana liczba maszyn wirtualnych są pomyślnie udostępnione. Nadmiarowe Inicjowanie obsługi administracyjnej zwiększa odsetka pomyślnych inicjowania obsługi administracyjnej i skraca czas wdrażania. Możesz nie są rozliczane za dodatkowe maszyny wirtualne i uwzględniane swoje limity przydziału.

Chociaż nadmiarowe Inicjowanie obsługi administracyjnej poprawić odsetka pomyślnych inicjowania obsługi administracyjnej, może to spowodować mylące zachowanie dla aplikacji, która nie jest przeznaczony do obsługi dodatkowych maszyn wirtualnych znajdujących się i znika następnie. Aby włączyć nadmiarowe Inicjowanie obsługi administracyjnej, wyłącz, upewnij się, masz następujące parametry w szablonie: `"overprovision": "false"`. Więcej informacji można znaleźć w [dokumentacja interfejsu API REST ustawić skali](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Jeśli zestaw skalowania używa magazynu zarządzana przez użytkownika i Wyłącz nadmiarowe Inicjowanie obsługi administracyjnej, może mieć więcej niż 20 maszyn wirtualnych na konto magazynu, ale Przejdź powyżej 40 ze względu na wydajność We/Wy nie jest zalecane. 

## <a name="limits"></a>Limity
Zestaw skali w oparciu obrazu z witryny Marketplace (znanej także jako obrazu platformy) i skonfigurowany do używania dysków zarządzanych Azure obsługuje pojemności maszyn wirtualnych do 1000. Jeśli konfigurujesz na skalę ustawioną obsługuje więcej niż 100 maszyn wirtualnych, nie wszystkie scenariusze takie same (na przykład równoważenia obciążenia). Aby uzyskać więcej informacji, zobacz [Praca z dużą maszynę wirtualną zestawy skalowania](virtual-machine-scale-sets-placement-groups.md). 

Skala ustawić skonfigurowany z użyciem konta magazynu zarządzanego przez użytkownika jest obecnie ograniczona do 100 maszyn wirtualnych (i 5 konta magazynu są zalecane w przypadku tej skali).

Zestaw skali w oparciu niestandardowego obrazu (jeden utworzony przez użytkownika) mogą mieć pojemności do 300 maszyn wirtualnych, gdy skonfigurowano dysków Azure zarządzanych. Jeśli zestaw skalowania jest skonfigurowany z kontami magazynu zarządzana przez użytkownika, musi utworzyć wszystkie dyski VHD dysku systemu operacyjnego w ramach jednego konta magazynu. W związku z tym maksymalna zalecana liczba maszyn wirtualnych w zestawie skalowania obraz niestandardowy w oparciu i zarządzana przez użytkownika magazynu wynosi 20. Jeśli wyłączysz nadmiarowe Inicjowanie obsługi administracyjnej, można przejść do 40.

Dla maszyn wirtualnych więcej niż dozwolone tych ograniczeń, należy wdrożyć wiele zestawów skalowania, jak pokazano w [ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

