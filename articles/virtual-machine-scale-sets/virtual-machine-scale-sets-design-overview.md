---
title: "Zagadnienia dotyczące zestawy skalowania maszyny wirtualnej Azure aaaDesign | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat projektowania sieci zestawy skalowania maszyny wirtualnej Azure"
keywords: zestawy skalowania maszyny wirtualnej w przypadku maszyny wirtualnej systemu Linux
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
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
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Zagadnienia dotyczące projektowania dla zestawów skalowania
W tym temacie omówiono zagadnienia dotyczące projektowania dla zestawy skalowania maszyny wirtualnej. Informacje dotyczące są zestawy skalowania maszyny wirtualnej, można znaleźć zbyt[omówienie zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Gdy zestawach skali toouse zamiast maszyn wirtualnych?
Ogólnie rzecz biorąc zestawy skalowania są przydatne w przypadku wdrażania infrastruktury wysokiej dostępności której zestaw maszyn mają podobnej konfiguracji. Jednak niektóre funkcje są dostępne tylko w zestawach skali, podczas gdy inne funkcje są dostępne tylko w maszynach wirtualnych. W celu toomake świadomej decyzji o tym, kiedy toouse poszczególnych technologii możemy należy najpierw Przyjrzyjmy się niektóre hello najczęściej używane funkcje, które są dostępne w zestawy skalowania, ale nie do maszyn wirtualnych:

### <a name="scale-set-specific-features"></a>Funkcje specyficzne dla zestawu skalowania

- Po określeniu Konfiguracja zestawu skali hello możesz po prostu zaktualizować hello "pojemności" właściwość toodeploy więcej maszyn wirtualnych jednocześnie. Jest znacznie prostsze niż zapisywania tooorchestrate skryptu wdrażania wiele poszczególnych maszyn wirtualnych jednocześnie.
- Możesz [Użyj tooautomatically Azure skalowania automatycznego skalowania zestaw skali](./virtual-machine-scale-sets-autoscale-overview.md) , ale nie poszczególnych maszyn wirtualnych.
- Możesz [maszyn wirtualnych zestawu skalowania odtworzenia z obrazu](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) , ale [nie poszczególnych maszyn wirtualnych](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Możesz [nadmiernej aprowizacji](./virtual-machine-scale-sets-design-overview.md) zestawu skalowania maszyn wirtualnych dla bardziej niezawodne i szybsze czas wdrażania. Nie można w tym poszczególnych maszyn wirtualnych, chyba że pisanie kodu niestandardowego toodo, to.
- Można określić [uaktualnienia zasad](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake go łatwo tooroll uaktualnień na maszynach wirtualnych w zestawie skali. Poszczególnych maszyn wirtualnych użytkownik musi organizowania aktualizacji samodzielnie.

### <a name="vm-specific-features"></a>Funkcje specyficzne dla maszyny Wirtualnej

Na hello drugiej strony, niektóre funkcje są dostępne tylko w maszynach wirtualnych (co najmniej hello chwili obecnej):

- Możesz dołączyć toospecific dysków danych poszczególnych maszyn wirtualnych, ale dysków dołączonych danych są skonfigurowane dla wszystkich maszyn wirtualnych w zestawie skalowania.
- Możesz dołączyć tooindividual dysków danych niepustym maszyn wirtualnych, ale nie maszyn wirtualnych w zestawie skalowania.
- Można migawek poszczególnych maszyn wirtualnych, ale nie maszyny Wirtualnej w zestawie skalowania.
- Można przechwycić obrazu z poszczególnych maszyn wirtualnych, ale nie z maszyny Wirtualnej w zestawie skalowania.
- Można przeprowadzić migrację poszczególnych maszyn wirtualnych z dysków toomanaged macierzystych dyskach, ale nie możesz tego zrobić dla maszyn wirtualnych w zestawie skalowania.
- Można przypisać publicznych adresów IP protokołu IPv6 kart sieciowych maszyny Wirtualnej tooindividual, ale nie można zrobić dla maszyn wirtualnych w zestawie skalowania. Należy pamiętać, że publicznych adresów IP protokołu IPv6 można przypisać równoważenia tooload przed albo poszczególnych maszyn wirtualnych lub zestawu skalowania maszyn wirtualnych.

## <a name="storage"></a>Magazyn

### <a name="scale-sets-with-azure-managed-disks"></a>Zestawy skalowania z dyskami zarządzane Azure
Zestawy skalowania można tworzyć za pomocą [dysków zarządzanych Azure](../virtual-machines/windows/managed-disks-overview.md) zamiast kont tradycyjnego magazynu Azure. Dyski zarządzane zapewniają hello następujące korzyści:
- Nie masz toopre — Utwórz zestaw z kontami magazynu Azure dla maszyn wirtualnych zestawu skalowania hello.
- Można zdefiniować [dołączone dyski danych](virtual-machine-scale-sets-attached-disks.md) hello maszyn wirtualnych w skali sieci można ustawić.
- Zestawy skalowania można skonfigurować za[obsługuje konto too1, 000 maszyn wirtualnych w zestawie](virtual-machine-scale-sets-placement-groups.md). 

Jeśli masz istniejący szablon, możesz również [zaktualizować hello szablonu toouse dysków zarządzane](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Magazynów zarządzana przez użytkownika
Zestaw skali, który nie jest zdefiniowana z dysków zarządzanych Azure opiera się na dyski toostore kont magazynu utworzonych przez użytkownika systemu operacyjnego hello maszyn wirtualnych hello hello zestawu. Zaleca się stosunku 20 maszyn wirtualnych na konto magazynu lub mniej tooachieve maksymalną we/wy, a także korzystanie z zalet _nadmiarowe Inicjowanie obsługi administracyjnej_ (patrz poniżej). Zalecane jest również rozłożyć hello początku znaków nazw kont magazynu hello na powitania alfabetu. Grozi to pomaga rozkładu obciążenia w różnych systemach wewnętrznego. 


## <a name="overprovisioning"></a>Nadmiarowe Inicjowanie obsługi administracyjnej
Skala ustawia obecnie domyślne zbyt "wymaga" maszyn wirtualnych. Z nadmiarowe Inicjowanie obsługi administracyjnej włączona, skala hello Ustaw faktycznie obroty zapasowych więcej maszyn wirtualnych nie zostanie wyświetlony monit o podanie, a następnie usuwa powitalne pomyślnie przydzielania dodatkowych maszyn wirtualnych po hello żądana liczba maszyn wirtualnych. Nadmiarowe Inicjowanie obsługi administracyjnej zwiększa odsetka pomyślnych inicjowania obsługi administracyjnej i skraca czas wdrażania. Rozliczenie jest przeprowadzane nie dla hello dodatkowe maszyny wirtualne i ich nie są wliczane do swoje limity przydziału.

Podczas nadmiarowe Inicjowanie obsługi administracyjnej poprawy szybkości Powodzenie inicjowania obsługi administracyjnej, może spowodować mylące zachowanie dla aplikacji, która jest zaprojektowana nie toohandle dodatkowych maszyn wirtualnych znajdujących się i znika następnie. tooturn nadmiarowe Inicjowanie obsługi administracyjnej, upewnij się, masz powitania po ciągu w szablonie: `"overprovision": "false"`. Więcej informacji można znaleźć w hello [dokumentacja interfejsu API REST ustawić skali](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Jeśli zestaw skalowania używa magazynu zarządzana przez użytkownika i Wyłącz nadmiarowe Inicjowanie obsługi administracyjnej, może mieć więcej niż 20 maszyn wirtualnych na konto magazynu, ale toogo powyżej 40 ze względu na wydajność We/Wy nie jest zalecane. 

## <a name="limits"></a>Limity
Zestaw skali w oparciu obrazu z witryny Marketplace (znanej także jako obrazu platformy) i skonfigurować toouse dysków zarządzanych Azure obsługuje pojemności zapasowej too1, 000 maszyn wirtualnych. Jeśli konfigurujesz Twojej toosupport zestaw skalowania więcej niż 100 maszyn wirtualnych, nie wszystkie scenariusze pracy hello takie same (na przykład równoważenia obciążenia). Aby uzyskać więcej informacji, zobacz [Praca z dużą maszynę wirtualną zestawy skalowania](virtual-machine-scale-sets-placement-groups.md). 

Skala ustawić skonfigurowany z użyciem konta magazynu zarządzanego przez użytkownika jest obecnie ograniczone too100 maszyny wirtualne (i 5 konta magazynu są zalecane w przypadku tej skali).

Zestaw skali w oparciu niestandardowego obrazu (jeden utworzony przez użytkownika) mogą mieć pojemności zapasowej VMs too100, gdy skonfigurowano dysków Azure zarządzanych. Jeśli zestaw skali hello jest skonfigurowany z kontami magazynu zarządzana przez użytkownika, musi utworzyć wszystkie dyski VHD dysku systemu operacyjnego w ramach jednego konta magazynu. W związku z tym hello maksymalna zalecana liczba maszyn wirtualnych w zestawie skalowania obraz niestandardowy w oparciu i zarządzana przez użytkownika magazynu wynosi 20. Jeśli wyłączysz nadmiarowe Inicjowanie obsługi administracyjnej, można przejść się too40.

Dla maszyn wirtualnych więcej niż dozwolone tych ograniczeń, należy toodeploy ustawia wiele skali, jak pokazano w [ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

