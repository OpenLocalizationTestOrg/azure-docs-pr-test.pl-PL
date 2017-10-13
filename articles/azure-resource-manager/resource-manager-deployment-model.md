---
title: "Wdrożenie usługi Resource Manager i Model Klasyczny | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano różnice między modelu wdrażania usługi Resource Manager i model klasyczny (lub zarządzania usługami) modelu wdrażania."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: 060680fd4a7ce6e0cde406cc4a8f6f3a21d3c588
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-the-state-of-your-resources"></a>Usługa Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów
W tym temacie opisano usługi Azure Resource Manager i klasycznych modeli wdrażania, stan zasobów, i do czego zasoby zostały wdrożone z jednego lub drugiego. Resource Manager i klasycznych modeli wdrażania reprezentować dwie różne sposoby wdrażania i zarządzania nimi rozwiązań platformy Azure. Pracować z nimi za pomocą dwóch różnych zestawów interfejsu API i wdrożonych zasobów może zawierać istotnych różnic. Te dwa modele nie są ze sobą w pełni zgodne. W tym temacie opisano różnic.

Aby uprościć wdrażanie i zarządzanie zasobami, firma Microsoft zaleca używanie Menedżera zasobów dla wszystkich nowych zasobów. Jeśli to możliwe firma Microsoft zaleca, należy ponownie wdrożyć istniejących zasobów za pomocą Menedżera zasobów.

Jeśli dopiero zaczynasz do Menedżera zasobów, można przejrzeć zdefiniowane w terminologii [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

## <a name="history-of-the-deployment-models"></a>Historia modele wdrażania
Dostarczana przez platformę Azure pierwotnie tylko klasycznym modelu wdrażania. W tym modelu każdy zasób istniał niezależnie; nie było możliwości wykonania do grupowania powiązanych zasobów. Zamiast tego trzeba było ręcznie śledzić zasoby, które składają się rozwiązania lub aplikacji i pamiętaj, aby zarządzać nimi w skoordynowany sposób podejście. Aby wdrożyć rozwiązanie, trzeba było utworzyć każdego zasobu indywidualnie za pośrednictwem klasycznego portalu lub utworzyć skrypt wdrożone wszystkie zasoby w odpowiedniej kolejności. Aby usunąć rozwiązania, trzeba było indywidualnie usunąć wszystkie zasoby. Nie można zastosować i zaktualizuj zasady kontroli dostępu dla powiązanych zasobów. Na koniec, nie możesz zastosować tagów do zasobów się z postanowieniami, które ułatwiają monitorowanie zasobów i Zarządzanie rozliczeniami.

W 2014 r. Azure wprowadzono Menedżera zasobów dodane pojęcie grupę zasobów. Grupa zasobów to kontener dla zasobów, które mają wspólne cyklu życia. Model wdrażania usługi Resource Manager zapewnia kilka korzyści:

* Można wdrożyć, zarządzanie i monitorowanie wszystkich usług do rozwiązania jako grupy, zamiast obsługi tych usług indywidualnie.
* Można wielokrotnie wdrażania rozwiązania przez cały cykl życia i mieć pewność, zasoby są wdrażane w spójnym stanie.
* Możliwość stosowania kontroli dostępu do wszystkich zasobów w grupie zasobów, a te zasady są stosowane automatycznie, gdy nowe zasoby są dodawane do grupy zasobów.
* Możliwość dodawania tagów do zasobów w celu logicznego uporządkowania wszystkich zasobów w ramach subskrypcji.
* JavaScript Object Notation (JSON) służy do definiowania infrastruktury dla rozwiązania. Plik JSON jest nazywany szablonem usługi Resource Manager.
* Możliwość definiowania zależności między zasobami, aby wdrażać je w odpowiedniej kolejności.

Podczas dodawania usługi Resource Manager wszystkie zasoby wstecznie zostały dodane do domyślnej grupy zasobów. Jeśli utworzysz zasobów za pośrednictwem klasycznego wdrożenia teraz zasobu jest tworzony automatycznie w domyślnej grupie zasobów dla tej usługi, nawet jeśli nie określono tej grupy zasobów wdrożenia. Jednak tylko istniejących w grupie zasobów nie oznacza, że zasób został przekonwertowany na modelu Resource Manager. Wyjaśniono, jak każda usługa obsługuje modele dwa wdrożenia w następnej sekcji. 

## <a name="understand-support-for-the-models"></a>Informacje pomocy technicznej dla modeli
Podczas wybierania który model wdrożenia do użycia zasobów, istnieją trzy scenariusze pod uwagę:

1. Usługa Resource Manager obsługuje i zawiera tylko jednego typu.
2. Usługa Resource Manager obsługuje, ale zapewnia dwa typy — jeden dla Menedżera zasobów i jeden klasycznego. Ten scenariusz dotyczy tylko maszyny wirtualne, konta magazynu i sieci wirtualnych.
3. Usługa nie obsługuje usługi Resource Manager.

Aby sprawdzić, czy usługa obsługuje Resource Manager, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).

Jeśli chcesz użyć wybranej usługi nie obsługuje Menedżera zasobów, można nadal przy użyciu klasycznego wdrożenia.

Czy usługa obsługuje Resource Manager i **nie jest** maszyny wirtualnej, konta magazynu lub sieci wirtualnej, a Resource Manager można użyć bez żadnych komplikacje.

Maszyny wirtualne, konta magazynu i sieci wirtualnych Jeśli zasób został utworzony za pośrednictwem klasycznego wdrożenia, nadal należy wykonywać na nich operacje za pośrednictwem klasycznego operacji. Jeśli maszyny wirtualne, konta magazynu lub sieci wirtualnej został utworzony przez wdrożenie usługi Resource Manager, można nadal przy użyciu usługi Resource Manager operacji. Ta różnica można uzyskać mylące po subskrypcja zawiera różnych zasobów został utworzony za pomocą usługi Resource Manager oraz wdrażania klasycznego. Ta kombinacja zasobów można utworzyć nieoczekiwane wyniki, ponieważ zasoby nie obsługują tej samej operacji.

W niektórych przypadkach polecenia Menedżera zasobów mogą pobierać informacje o zasobie, została utworzona za pośrednictwem klasycznego wdrożenia, lub można wykonywać zadań administracyjnych, takich jak przeniesienie zasobów klasycznych do innej grupy zasobów. Jednak w tych przypadkach nie należy nadawać wrażenie, aby typ obsługiwał operacje Menedżera zasobów. Na przykład załóżmy, że masz grupy zasobów, która zawiera maszynę wirtualną, który został utworzony przy użyciu wdrażania klasycznego. Jeśli uruchomisz następujące polecenia programu PowerShell Menedżera zasobów:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Zwraca maszyny wirtualnej:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Jednak polecenia cmdlet usługi Resource Manager **Get AzureRmVM** zwraca tylko maszyn wirtualnych wdrożonych przez Menedżera zasobów. Polecenie nie zwraca została utworzona za pośrednictwem klasycznego wdrożenia maszyny wirtualnej.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Tylko zasoby utworzone za pomocą Menedżera zasobów pomocy technicznej tagów. Nie można zastosować tagów do zasobów klasycznych.

## <a name="resource-manager-characteristics"></a>Właściwości Menedżera zasobów
Aby ułatwić zrozumienie dwa modele, umożliwia Przejrzyj właściwości typów Menedżera zasobów:

* Został utworzony za pomocą [portalu Azure](https://portal.azure.com/).
  
     ![Azure Portal](./media/resource-manager-deployment-model/portal.png)
  
     Dla zasobów obliczeniowych, magazynu i zasobów sieciowych istnieje możliwość używania usługi Resource Manager lub Classic deployment. Wybierz **Menedżera zasobów**.
  
     ![Wdrożenie usługi Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Utworzona z wersją poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Te polecenia mają format *AzureRmNoun zlecenie*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Został utworzony za pomocą [Azure Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) dla operacji REST.
* Został utworzony za pomocą interfejsu wiersza polecenia Azure polecenia uruchamiane w **arm** tryb.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* Typ zasobu nie zawiera **(klasyczne)** w nazwie. Na poniższej ilustracji przedstawiono typu jako **konta magazynu**.
  
    ![aplikacji sieci Web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Właściwości wdrażania klasycznego
Klasycznym modelu wdrażania może również wiedzieć, jak model zarządzania usługami.

Zasoby utworzone w klasycznym modelu wdrożenia mają następującą charakterystykę:

* Został utworzony za pomocą [klasyczny portal](https://manage.windowsazure.com)
  
     ![Portal klasyczny](./media/resource-manager-deployment-model/classic-portal.png)
  
     Lub, w portalu Azure i podasz **klasycznego** wdrażania (do obliczeń, magazynu i sieci).
  
     ![Wdrożenie klasyczne](./media/resource-manager-deployment-model/select-classic.png)
* Utworzone za pomocą wersji usługi zarządzania poleceń cmdlet programu Azure PowerShell. Te nazwy polecenia mają format *AzureNoun zlecenie*.

  ```powershell
  New-AzureVM
  ```

* Został utworzony za pomocą [interfejs API REST zarządzania usługami](https://msdn.microsoft.com/library/azure/ee460799.aspx) dla operacji REST.
* Został utworzony za pomocą interfejsu wiersza polecenia Azure polecenia uruchamiane w **asm** tryb.

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* Typ zasobu zawiera **(klasyczne)** w nazwie. Na poniższej ilustracji przedstawiono typu jako **konta magazynu (klasyczne)**.
  
    ![typu klasycznego](./media/resource-manager-deployment-model/classic-type.png)

Portalu Azure można użyć do zarządzania zasobami, które zostały utworzone za pośrednictwem klasycznego wdrożenia.

## <a name="changes-for-compute-network-and-storage"></a>Zmiany dla zasobów obliczeniowych, sieci i magazynu
Poniższy diagram przedstawia zasobów obliczeniowych, sieci i magazynu wdrożone za pomocą Menedżera zasobów.

![Menedżer zasobów — architektura](./media/resource-manager-deployment-model/arm_arch3.png)

Należy uwzględnić następujące relacje między zasobami:

* Istnieje wszystkie zasoby w grupie zasobów.
* Maszyny wirtualnej jest zależny od konta magazynu określonych zdefiniowany w dostawcy zasobów magazynu do przechowywania jego dysków w magazynie obiektów blob (wymagane).
* Maszyny wirtualnej odwołuje się do określonej karty Sieciowej zdefiniowany w dostawcy zasobów sieciowych (wymagane) i dostępności ustawić się zdefiniowanych dostawcy zasobów obliczeniowych (opcjonalnie).
* Karta sieciowa odwołuje się do maszyny wirtualnej przypisany adres IP (wymagane), podsieć sieci wirtualnej dla maszyny wirtualnej (wymagane) i do grupy zabezpieczeń sieci (opcjonalnie).
* Podsieć sieci wirtualnej odwołuje się do grupy zabezpieczeń sieci (opcjonalnie).
* Wystąpienie usługi równoważenia obciążenia odwołuje się do puli adresów IP, które obejmują karty Sieciowej maszyny wirtualnej (opcjonalnie) i adres usługi równoważenia obciążenia publicznych lub prywatnych IP (opcjonalnie) odwołuje się do wewnętrznej bazy danych.

Poniżej przedstawiono składniki oraz ich relacji klasycznego wdrożenia:

![Architektura klasycznego](./media/resource-manager-deployment-model/arm_arch1.png)

Klasycznym rozwiązanie do obsługi maszyny wirtualnej zawiera:

* Usługi w chmurze wymagana, który działa jako kontener dla hostingu maszyn wirtualnych (obliczeniowe). Maszyny wirtualne są automatycznie udostępniane z karty interfejsu sieciowego (NIC) i adres IP przypisany przez platformę Azure. Ponadto usługa w chmurze zawiera wystąpienia usługi równoważenia obciążenia zewnętrznych, publiczny adres IP i domyślne punkty końcowe zezwalająca na ruch protokołu Secure Shell (SSH) dla maszyn wirtualnych z systemem Linux i zdalnego pulpitu i zdalnej programu PowerShell ruch maszyn wirtualnych z systemem Windows.
* Konto magazynu wymagane są przechowywane pliki VHD dla maszyny wirtualnej, w tym system operacyjny, dyski tymczasowego i dodatkowych danych (magazyn).
* Opcjonalne sieci wirtualnej, który działa jako dodatkowy kontener, można utworzyć podsieci struktury i wyznaczyć podsieci, na którym znajduje się maszyna wirtualna (sieć).

W poniższej tabeli opisano zmiany w interakcje dostawców zasobów obliczeniowych, sieci i magazynu:

| Element | Wdrożenie klasyczne | Resource Manager |
| --- | --- | --- |
| Usługa w chmurze dla maszyn wirtualnych |Usługa w chmurze stanowiła kontener do przechowywania maszyn wirtualnych wymagających dostępności na platformie oraz równoważenia obciążenia. |Usługa w chmurze nie jest już obiektem wymaganym do utworzenia maszyny wirtualnej przy użyciu nowego modelu. |
| Sieci wirtualne |Sieć wirtualna jest opcjonalne dla maszyny wirtualnej. Jeśli uwzględniona, sieci wirtualnej nie można wdrożyć za pomocą Menedżera zasobów. |Maszyna wirtualna wymaga sieci wirtualnej, która została wdrożona za pomocą Menedżera zasobów. |
| Konta magazynu |Maszyna wirtualna wymaga konta magazynu przechowującym wirtualne dyski twarde dla systemu operacyjnego, dane tymczasowe i dodatkowych dysków. |Maszyna wirtualna wymaga konta magazynu do przechowywania jego dysków w magazynie obiektów blob. |
| Zestawy dostępności |Dostępność dla platformy była wskazywana przez skonfigurowanie na maszynach wirtualnych takiego samego parametru „AvailabilitySetName”. Maksymalna liczba domen błędów wynosiła 2. |Zestaw dostępności to zasób udostępniany przez dostawcę Microsoft.Compute. Maszyny wirtualne wymagające wysokiej dostępności muszą należeć do zestawu dostępności. Maksymalna liczba domen błędów wynosi obecnie 3. |
| Grupy koligacji |Grupy koligacji były wymagane do tworzenia sieci wirtualnych. Przestały być wymagane wraz z wprowadzeniem regionalnych sieci wirtualnych. |Dla uproszczenia pojęcie grup koligacji nie jest stosowane w interfejsach API udostępnianych za pośrednictwem usługi Azure Resource Manager. |
| Równoważenie obciążenia |Utworzenie usługi w chmurze zapewnia niejawny moduł równoważenie obciążenia dla wdrożonych maszyn wirtualnych. |Usługa Load Balancer stanowi zasób udostępniany przez dostawcę Microsoft.Network. Podstawowy interfejs sieciowy maszyn wirtualnych wymagający równoważenia obciążenia powinien odwoływać się do modułu równoważenia obciążenia. Moduły równoważenia obciążenia mogą być wewnętrzne lub zewnętrzne. Wystąpienie usługi równoważenia obciążenia odwołuje się do puli adresów IP, które obejmują karty Sieciowej maszyny wirtualnej (opcjonalnie) i adres usługi równoważenia obciążenia publicznych lub prywatnych IP (opcjonalnie) odwołuje się do wewnętrznej bazy danych. [Dowiedz się więcej.](../virtual-network/resource-groups-networking.md) |
| Wirtualny adres IP |Usługi w chmurze Pobierz domyślny adres VIP (wirtualny adres IP), gdy maszyna wirtualna zostanie dodany do usługi w chmurze. Wirtualny adres IP to adres skojarzony z niejawnym modułem równoważenia obciążenia. |Publiczny adres IP stanowi zasób udostępniany przez dostawcę Microsoft.Network. Publiczny adres IP może być statyczny (zastrzeżony) lub dynamiczny. Dynamiczne publiczne adresy IP można przypisać do usługi Load Balancer. Publiczne adresy IP mogą być chronione przy użyciu grup zabezpieczeń. |
| Zastrzeżony adres IP |Istnieje możliwość zastrzeżenia adresu IP na platformie Azure i skojarzenia go z usługą w chmurze w celu zapewnienia jego umocowania. |Publiczny adres IP, który można utworzyć w trybie statycznym, oferuje te same możliwości, co zastrzeżony adres IP. Obecnie statyczne publiczne adresy IP można przypisać tylko do modułu równoważenia obciążenia. |
| Publiczny adres IP (PIP) dla maszyny wirtualnej |Publiczne adresy IP można także skojarzone z maszyną wirtualną bezpośrednio. |Publiczny adres IP stanowi zasób udostępniany przez dostawcę Microsoft.Network. Publiczny adres IP może być statyczny (zastrzeżony) lub dynamiczny. Obecnie w celu uzyskania publicznego adresu IP dla maszyny wirtualnej do interfejsu sieciowego można jednak przypisywać tylko dynamiczne publiczne adresy IP. |
| Punkty końcowe |Wejściowe punkty końcowe wymagały skonfigurowania na maszynie wirtualnej w celu uzyskania otwartej łączności z określonymi portami. Jednym z często używanych trybów łączenia się z maszynami wirtualnymi jest ustawienie wejściowych punktów końcowych. |Można skonfigurować reguły ruchu przychodzącego translatora adresów sieciowych w usługach Load Balancer w celu uzyskania tej samej możliwości włączania punktów końcowych dla określonych portów na potrzeby połączeń z maszynami wirtualnymi. |
| Nazwa DNS |Usługa w chmurze otrzymuje niejawną, globalnie unikatową nazwę DNS. Na przykład: `mycoffeeshop.cloudapp.net`. |Nazwy DNS są opcjonalnymi parametrami, które można określić w zasobie publicznego adresu IP. Nazwa FQDN to w następującym formacie - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfejsy sieciowe |Podstawowy i pomocniczy interfejs sieciowy oraz ich właściwości zostały zdefiniowane jako konfiguracja sieci maszyny wirtualnej. |Interfejs sieciowy stanowi zasób udostępniany przez dostawcę Microsoft.Network. Cykl życia interfejsu sieciowego nie jest powiązany z maszyną wirtualną. Odwołuje się maszyny wirtualnej przypisany adres IP (wymagane), podsieć sieci wirtualnej dla maszyny wirtualnej (wymagane) i do grupy zabezpieczeń sieci (opcjonalnie). |

Aby dowiedzieć się więcej o nawiązywaniu połączeń sieci wirtualne od różne modele wdrażania, zobacz [połączyć sieci wirtualnych z różne modele wdrażania w portalu](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-to-resource-manager"></a>Migracja z klasycznego do Menedżera zasobów
Jeśli wszystko jest gotowe do migracji zasobów z wdrażania klasycznego do wdrożenia usługi Resource Manager, zobacz:

1. [Techniczne szczegółowe informacje na temat obsługiwanych platform migracji ze środowiska klasycznego do usługi Azure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Platformy obsługiwane migracji zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu programu Azure PowerShell](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migracja zasobów IaaS ze środowiska klasycznego do usługi Azure Resource Manager przy użyciu wiersza polecenia platformy Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Można utworzyć maszynę wirtualną do wdrożenia w sieci wirtualnej utworzonej przy użyciu klasycznego wdrożenia przy użyciu usługi Azure Resource Manager?**

Jest to nieobsługiwane. Nie można użyć usługi Azure Resource Manager, aby wdrożyć maszynę wirtualną w sieci wirtualnej, który został utworzony przy użyciu klasycznego wdrożenia.

**Można utworzyć maszynę wirtualną za pomocą usługi Azure Resource Manager z obrazu użytkownika, który został utworzony przy użyciu interfejsów API usługi Azure Service Management?**

Jest to nieobsługiwane. Można jednak skopiować pliki VHD z konta magazynu, który został utworzony przy użyciu interfejsów API usługi Service Management i dodaj je do nowego konta za pośrednictwem usługi Azure Resource Manager.

**Jaki jest wpływ na przydziały obowiązujące dla mojej subskrypcji?**

Przydziały dla maszyn wirtualnych, sieci wirtualnych i kont magazynu utworzonych za pomocą Menedżera zasobów Azure są niezależne od innych przydziałów. Każda subskrypcja otrzymuje przydziały na tworzenie zasobów przy użyciu nowych interfejsów API. Więcej informacji o dodatkowych przydziałach można znaleźć [tutaj](../azure-subscription-service-limits.md).

**Można nadal używać moich zautomatyzowanych skryptów do inicjowania obsługi maszyn wirtualnych, sieci wirtualnych i kont magazynu za pośrednictwem interfejsów API usługi Resource Manager?**

Do automatyzacji oraz skrypty, które zostały utworzone nadal działa w przypadku istniejących maszyn wirtualnych, sieci wirtualne utworzone w trybie zarządzania usługami Azure. Jednak skrypty musi zostać zaktualizowany w celu zastosowania nowego schematu tworzenia tych samych zasobów w trybie Menedżera zasobów.

**Gdzie znajdę przykłady szablonów usługi Azure Resource Manager?**

Kompleksowy zestaw szablonów startowych można znaleźć w [szablonów Szybki Start usługi Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Następne kroki
* Aby zapoznać się z tworzenia szablonu, który definiuje maszyny wirtualnej, konta magazynu i sieci wirtualnej, zobacz [Przewodnik po szablonie usługi Resource Manager](resource-manager-template-walkthrough.md).
* Aby wyświetlić polecenia do wdrożenia szablonu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

