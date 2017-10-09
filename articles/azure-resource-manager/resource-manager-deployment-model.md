---
title: "aaaResource Manager oraz wdrażania klasycznego | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano model wdrażania hello różnice między modelu wdrażania usługi Resource Manager hello i hello klasyczny (lub Usługa zarządzania)."
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
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Usługa Azure Resource Manager, a wdrożenie klasyczne: omówienie modele wdrażania i hello stan zasobów
W tym temacie opisano usługi Azure Resource Manager i klasycznych modeli wdrażania, stan hello zasobów, i do czego zasoby zostały wdrożone z co najmniej hello innych. Hello Resource Manager i klasycznych modeli wdrażania reprezentować dwie różne sposoby wdrażania i zarządzania nimi rozwiązań platformy Azure. Pracować z nimi za pomocą dwóch różnych zestawów interfejsu API i hello wdrożonych zasobów może zawierać istotnych różnic. Witaj dwa modele nie są całkowicie zgodne ze sobą. W tym temacie opisano różnic.

toosimplify hello wdrażania i zarządzania zasobami, firma Microsoft zaleca używanie Menedżera zasobów dla wszystkich nowych zasobów. Jeśli to możliwe firma Microsoft zaleca, należy ponownie wdrożyć istniejących zasobów za pomocą Menedżera zasobów.

W przypadku nowych tooResource Manager może być terminologii hello przeglądu toofirst zdefiniowane w hello [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Historia hello modele wdrażania
Dostarczana przez platformę Azure pierwotnie tylko hello klasycznego modelu wdrażania. W tym modelu każdy zasób istniał niezależnie; nie było możliwości wykonania toogroup ze sobą powiązane zasoby. Zamiast tego miał toomanually śledzenie zasobów, które składają się rozwiązania lub aplikacji i Zapamiętaj toomanage w skoordynowany sposób podejście. toodeploy rozwiązania, trzeba było tooeither tworzenie każdego zasobu indywidualnie za pośrednictwem portalu klasycznego hello lub utworzyć skrypt, który wdrożony wszystkie zasoby hello w odpowiedniej kolejności hello. toodelete rozwiązania, trzeba było toodelete każdego zasobu pojedynczo. Nie można zastosować i zaktualizuj zasady kontroli dostępu dla powiązanych zasobów. Ponadto nie można zastosować tagi tooresources toolabel je za pomocą warunków, które ułatwiają monitorowanie zasobów i Zarządzanie rozliczeniami.

W 2014 r. Azure wprowadzono Menedżera zasobów dodane koncepcji hello grupy zasobów. Grupa zasobów to kontener dla zasobów, które mają wspólne cyklu życia. model wdrażania Hello Resource Manager zapewnia kilka korzyści:

* Można wdrażania, zarządzania i monitorowania wszystkich usług hello do rozwiązania jako grupę, a nie pojedynczo obsługi tych usług.
* Można wielokrotnie wdrażania rozwiązania przez cały cykl życia i mieć pewność, zasoby są wdrażane w spójnym stanie.
* Dostęp do zasobów tooall formant można zastosować w grupie zasobów, a te zasady są stosowane automatycznie, gdy dodawane są nowe zasoby, grupy zasobów toohello.
* Możliwość dodawania tagów tooresources toologically organizowanie wszystkie zasoby hello w ramach subskrypcji.
* Infrastruktura hello toodefine JavaScript Object Notation (JSON) można użyć dla rozwiązania. Plik JSON Hello jest nazywany szablonem usługi Resource Manager.
* Można zdefiniować hello zależności między zasobami w celu wdrażania ich w odpowiedniej kolejności hello.

Podczas dodawania usługi Resource Manager wszystkie zasoby wstecznie dodano toodefault grup zasobów. W przypadku utworzenia zasobu za pośrednictwem klasycznego wdrożenia teraz, zasobów hello jest tworzony automatycznie w domyślnej grupie zasobów dla tej usługi, nawet jeśli nie określono tej grupy zasobów na wdrożenie. Jednak tylko istniejących w grupie zasobów nie oznacza, że hello zasobów został przekonwertowany toohello modelu Resource Manager. Wyjaśniono, jak każda usługa obsługuje dwa modele wdrażania hello w następnej sekcji hello. 

## <a name="understand-support-for-hello-models"></a>Informacje pomocy technicznej dla modeli hello
Podczas wybierania który toouse model wdrażania zasobów, istnieją trzy scenariusze toobe uwagę:

1. Usługa Hello obsługuje Resource Manager i zapewnia tylko jednego typu.
2. Witaj usługi Resource Manager obsługuje, ale zapewnia dwa typy — jeden dla Menedżera zasobów i jeden klasycznego. Ten scenariusz dotyczy tylko toovirtual maszyny, konta magazynu i sieci wirtualnych.
3. Usługa Hello nie obsługuje usługi Resource Manager.

toodiscover, czy usługa obsługuje Resource Manager, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).

Jeśli usługa hello mają toouse nie obsługuje usługi Resource Manager, można nadal przy użyciu klasycznego wdrożenia.

Jeśli usługa hello obsługuje Resource Manager i **nie jest** maszyny wirtualnej, konta magazynu lub sieci wirtualnej, a Resource Manager można użyć bez żadnych komplikacje.

Maszyny wirtualne, konta magazynu i sieci wirtualnych Jeśli hello zasób został utworzony za pomocą wdrażania klasycznego, należy nadal toooperate na nim za pośrednictwem klasycznego operacji. Jeśli hello maszyny wirtualnej, konta magazynu lub sieci wirtualnej został utworzony przez wdrożenie usługi Resource Manager, można nadal przy użyciu usługi Resource Manager operacji. Ta różnica można uzyskać mylące po subskrypcja zawiera różnych zasobów został utworzony za pomocą usługi Resource Manager oraz wdrażania klasycznego. Ta kombinacja zasobów można utworzyć nieoczekiwane wyniki, ponieważ nie obsługują zasobów hello hello tej samej operacji.

W niektórych przypadkach polecenia Menedżera zasobów mogą pobierać informacje o zasobie, została utworzona za pośrednictwem klasycznego wdrożenia, lub można wykonywać zadań administracyjnych, takich jak przeniesienie grupy zasobów tooanother klasyczne zasoby. Jednak w tych przypadkach nie należy nadawać hello wrażenie, że typ hello obsługuje operacje Menedżera zasobów. Na przykład załóżmy, że masz grupy zasobów, która zawiera maszynę wirtualną, który został utworzony przy użyciu wdrażania klasycznego. Jeśli uruchomisz hello następującego polecenia programu PowerShell Menedżera zasobów:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Zwraca hello maszyny wirtualnej:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Jednak hello poleceń cmdlet Menedżera zasobów **Get AzureRmVM** zwraca tylko maszyn wirtualnych wdrożonych przez Menedżera zasobów. Witaj następujące polecenie nie zwraca hello maszyna wirtualna została utworzona za pośrednictwem klasycznego wdrożenia.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Tylko zasoby utworzone za pomocą Menedżera zasobów pomocy technicznej tagów. Nie można zastosować tagi tooclassic zasobów.

## <a name="resource-manager-characteristics"></a>Właściwości Menedżera zasobów
toohelp zrozumieć hello dwa modele, umożliwia przeglądanie właściwości hello typów Menedżera zasobów:

* Został utworzony za pomocą hello [portalu Azure](https://portal.azure.com/).
  
     ![Azure Portal](./media/resource-manager-deployment-model/portal.png)
  
     Dla zasobów obliczeniowych, magazynu i zasobów sieciowych można skorzystać z opcji hello przy użyciu usługi Resource Manager lub Classic wdrożenia. Wybierz **Menedżera zasobów**.
  
     ![Wdrożenie usługi Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Utworzone za pomocą wersji Menedżera zasobów hello hello poleceń cmdlet programu Azure PowerShell. Te polecenia mają hello format *AzureRmNoun zlecenie*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Został utworzony za pomocą hello [Azure Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) dla operacji REST.
* Został utworzony za pomocą polecenia wiersza polecenia platformy Azure, uruchom w hello **arm** tryb.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* nie ma typu zasobu Hello **(klasyczne)** w nazwie hello. Witaj poniższy obraz przedstawia hello typu jako **konta magazynu**.
  
    ![aplikacji sieci Web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Właściwości wdrażania klasycznego
Hello klasycznego modelu wdrażania może również wiedzieć, jak model zarządzania usługami hello.

Zasoby utworzone w hello wdrażania klasycznego modelu udziału hello następujące cechy:

* Został utworzony za pomocą hello [klasyczny portal](https://manage.windowsazure.com)
  
     ![Portal klasyczny](./media/resource-manager-deployment-model/classic-portal.png)
  
     Lub, hello portalu Azure i określeniu **klasycznego** wdrażania (do obliczeń, magazynu i sieci).
  
     ![Wdrożenie klasyczne](./media/resource-manager-deployment-model/select-classic.png)
* Utworzone za pomocą wersji usługi zarządzania hello hello poleceń cmdlet programu Azure PowerShell. Te nazwy polecenia mają hello format *AzureNoun zlecenie*.

  ```powershell
  New-AzureVM
  ```

* Został utworzony za pomocą hello [interfejs API REST zarządzania usługami](https://msdn.microsoft.com/library/azure/ee460799.aspx) dla operacji REST.
* Został utworzony za pomocą interfejsu wiersza polecenia Azure polecenia uruchamiane w **asm** tryb.

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* zawiera typ zasobu Hello **(klasyczne)** w nazwie hello. Witaj poniższy obraz przedstawia hello typu jako **konta magazynu (klasyczne)**.
  
    ![typu klasycznego](./media/resource-manager-deployment-model/classic-type.png)

Można użyć hello Azure toomanage portalu zasobów, które zostały utworzone za pośrednictwem klasycznego wdrożenia.

## <a name="changes-for-compute-network-and-storage"></a>Zmiany dla zasobów obliczeniowych, sieci i magazynu
Witaj Poniższy diagram przedstawia zasobów obliczeniowych, sieci i magazynu wdrożone za pomocą Menedżera zasobów.

![Menedżer zasobów — architektura](./media/resource-manager-deployment-model/arm_arch3.png)

Należy uwzględnić następujące relacje między zasobami hello hello:

* Wszystkie zasoby hello istnieje w grupie zasobów.
* Witaj maszyny wirtualnej zależy od konta magazynu określonych zdefiniowane w toostore dostawcy zasobów magazynu hello jej dyski w obiektu blob magazynu (wymagane).
* Maszyna wirtualna Hello odwołuje się do określonej karty Sieciowej zdefiniowany w dostawcy zasobów sieciowych hello (wymagane) i zestaw się zdefiniowanych dostawcy zasobów obliczeniowych hello (opcjonalnie) dostępności.
* Hello kart odwołania hello maszyny wirtualnej przypisany adres IP (wymagane), podsieć hello hello sieci wirtualnej dla maszyny wirtualnej hello (wymagane) i tooa grupy zabezpieczeń sieci (opcjonalnie).
* Witaj podsieci sieci wirtualnej odwołuje się do grupy zabezpieczeń sieci (opcjonalnie).
* wystąpienie usługi równoważenia obciążenia Hello odwołuje się do puli zaplecza hello adresy IP, które zawierają hello karty Sieciowej maszyny wirtualnej (opcjonalnie) i odwołuje się do adres usługi równoważenia obciążenia publicznych lub prywatnych IP (opcjonalnie).

Poniżej przedstawiono składniki hello oraz ich relacji wdrożenia klasycznego:

![Architektura klasycznego](./media/resource-manager-deployment-model/arm_arch1.png)

Hello klasycznego rozwiązanie do obsługi maszyny wirtualnej zawiera:

* Usługi w chmurze wymagana, który działa jako kontener dla hostingu maszyn wirtualnych (obliczeniowe). Maszyny wirtualne są automatycznie udostępniane z karty interfejsu sieciowego (NIC) i adres IP przypisany przez platformę Azure. Ponadto usługa w chmurze hello zawiera wystąpienia usługi równoważenia obciążenia zewnętrznych, publiczny adres IP i domyślne punkty końcowe tooallow zdalnego pulpitu i zdalnej programu PowerShell ruchu dla maszyn wirtualnych z systemem Windows i ruchu protokołu Secure Shell (SSH) dla opartych na systemie Linux maszyny wirtualne.
* Konto magazynu wymagane, czy magazyny hello wirtualne dyski twarde dla maszyny wirtualnej, włączając hello systemu operacyjnego, dyski tymczasowego i dodatkowych danych (magazyn).
* Opcjonalne sieci wirtualnej, który działa jako dodatkowy kontener, można utworzyć strukturę podsieciami i wyznaczyć hello podsieci, na które hello znajduje się maszyna wirtualna (sieć).

Witaj w poniższej tabeli opisano zmiany w interakcje dostawców zasobów obliczeniowych, sieci i magazynu:

| Element | Wdrożenie klasyczne | Resource Manager |
| --- | --- | --- |
| Usługa w chmurze dla maszyn wirtualnych |Usługi w chmurze została stanowiła kontener do przechowywania maszyn wirtualnych hello wymagających dostępności hello platformie oraz równoważenia obciążenia. |Usługi w chmurze nie jest już obiektem wymaganym do utworzenia maszyny wirtualnej przy użyciu nowego modelu hello. |
| Sieci wirtualne |Sieć wirtualna jest opcjonalne dla hello maszyny wirtualnej. Jeśli uwzględniona, hello sieci wirtualnej nie można wdrożyć za pomocą Menedżera zasobów. |Maszyna wirtualna wymaga sieci wirtualnej, która została wdrożona za pomocą Menedżera zasobów. |
| Konta magazynu |Maszyna wirtualna Hello wymaga konta magazynu przechowującym hello wirtualne dyski twarde dla systemu operacyjnego hello, dane tymczasowe i dodatkowych dysków. |Maszyna wirtualna Hello wymaga toostore konta magazynu jego dysków w magazynie obiektów blob. |
| Zestawy dostępności |Dostępność toohello platformy była wskazywana przez skonfigurowanie hello tego samego "AvailabilitySetName" na powitania maszyn wirtualnych. Maksymalna liczba domen błędów Hello: 2. |Zestaw dostępności to zasób udostępniany przez dostawcę Microsoft.Compute. Maszyny wirtualne, które wymagają wysokiej dostępności muszą być zawarte w hello zestawu dostępności. Witaj maksymalna liczba domen błędów wynosi obecnie 3. |
| Grupy koligacji |Grupy koligacji były wymagane do tworzenia sieci wirtualnych. Jednak z hello wprowadzeniem regionalnych sieci wirtualnych, która nie jest wymagane już. |toosimplify, hello pojęcie grup koligacji nie istnieje w hello interfejsach API udostępnianych za pośrednictwem usługi Azure Resource Manager. |
| Równoważenie obciążenia |Tworzenie usługi w chmurze zapewnia niejawny moduł Równoważenie obciążenia hello maszyn wirtualnych wdrożonych. |Witaj modułu równoważenia obciążenia jest stanowi zasób udostępniany przez dostawcę Microsoft.Network hello. Witaj podstawowy interfejs sieciowy hello maszyn wirtualnych wymagający równoważenia obciążenia toobe powinien odwoływać się do usługi równoważenia obciążenia hello. Moduły równoważenia obciążenia mogą być wewnętrzne lub zewnętrzne. Wystąpienie usługi równoważenia obciążenia odwołuje się do puli zaplecza hello adresy IP, które zawierają hello karty Sieciowej maszyny wirtualnej (opcjonalnie) i odwołuje się do adres usługi równoważenia obciążenia publicznych lub prywatnych IP (opcjonalnie). [Dowiedz się więcej.](../virtual-network/resource-groups-networking.md) |
| Wirtualny adres IP |Usługi w chmurze Pobierz domyślny adres VIP (wirtualny adres IP), po dodaniu tooa usługi w chmurze maszyny Wirtualnej. Witaj wirtualny adres IP jest adresem hello skojarzone z hello niejawnym modułem równoważenia obciążenia. |Publiczny adres IP jest stanowi zasób udostępniany przez dostawcę Microsoft.Network hello. Publiczny adres IP może być statyczny (zastrzeżony) lub dynamiczny. Dynamiczne publiczne adresy IP można przypisać tooa modułu równoważenia obciążenia. Publiczne adresy IP mogą być chronione przy użyciu grup zabezpieczeń. |
| Zastrzeżony adres IP |Można zastrzec adresu IP w usłudze Azure i skojarz z tooensure usługi w chmurze, która hello adres IP jest trwałe. |Publiczny adres IP można tworzyć w trybie "Statyczny" i oferuje hello sama funkcja jako "Zastrzeżonego adresu IP". Statyczne publiczne adresy IP można przypisać tylko tooa modułu równoważenia obciążenia w tej chwili. |
| Publiczny adres IP (PIP) dla maszyny wirtualnej |Publiczne adresy IP można także tooa skojarzonego VM bezpośrednio. |Publiczny adres IP jest stanowi zasób udostępniany przez dostawcę Microsoft.Network hello. Publiczny adres IP może być statyczny (zastrzeżony) lub dynamiczny. Jednak tylko dynamiczne publiczne adresy IP można tooget interfejsu sieciowego przypisanej tooa publicznego adresu IP dla maszyny Wirtualnej w tej chwili. |
| Punkty końcowe |Otwarcie łączności dla określonych portów wejściowych toobe wymagane punkty końcowe skonfigurowane na toobe maszyny wirtualnej. Jeden z hello często używanych trybów łączenia z maszynami toovirtual ustawienie wejściowych punktów końcowych. |Można skonfigurować reguły NAT ruchu przychodzącego na usługi równoważenia obciążenia tooachieve hello samej możliwości włączania punktów końcowych dla określonych portów na potrzeby łączenia toohello maszyn wirtualnych. |
| Nazwa DNS |Usługa w chmurze otrzymuje niejawną, globalnie unikatową nazwę DNS. Na przykład: `mycoffeeshop.cloudapp.net`. |Nazwy DNS są opcjonalnymi parametrami, które można określić w zasobie publicznego adresu IP. Witaj FQDN znajduje się w następujących hello format - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfejsy sieciowe |Podstawowy i pomocniczy interfejs sieciowy oraz ich właściwości zostały zdefiniowane jako konfiguracja sieci maszyny wirtualnej. |Interfejs sieciowy stanowi zasób udostępniany przez dostawcę Microsoft.Network. cykl życia Hello powitalne interfejsu sieciowego nie jest powiązany tooa maszyny wirtualnej. Odwołuje się maszyna wirtualna hello przypisany adres IP (wymagane), podsieć hello hello sieci wirtualnej dla maszyny wirtualnej hello (wymagane) i tooa grupy zabezpieczeń sieci (opcjonalnie). |

toolearn dotyczące łączenia sieci wirtualne od różne modele wdrażania, zobacz [połączyć sieci wirtualnych z różne modele wdrażania w portalu hello](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Migracja z klasycznego tooResource Manager
Jeśli wszystko jest gotowe toomigrate zasobów z tooResource wdrożenie klasyczne Manager deployment, zobacz:

1. [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Platformy obsługiwane migracji zasobów IaaS z klasycznym tooAzure Resource Manager](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migracja zasobów IaaS z klasycznym tooAzure Resource Manager przy użyciu programu Azure PowerShell](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migracja zasobów IaaS z klasycznym tooAzure Menedżera zasobów przy użyciu wiersza polecenia platformy Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Można utworzyć maszynę wirtualną za pomocą usługi Azure Resource Manager toodeploy w sieci wirtualnej utworzonej przy użyciu klasycznego wdrożenia?**

Jest to nieobsługiwane. Nie można używać usługi Azure Resource Manager toodeploy maszynę wirtualną w sieci wirtualnej, który został utworzony przy użyciu klasycznego wdrożenia.

**Można utworzyć maszyny wirtualnej z wykorzystaniem hello Azure Resource Manager z obrazu użytkownika, który został utworzony przy użyciu hello interfejsów API usługi Azure Service Management?**

Jest to nieobsługiwane. Można jednak skopiować pliki VHD hello z konta magazynu, który został utworzony przy użyciu hello interfejsów API usługi Service Management i dodaj je tooa nowe konto utworzone za pomocą usługi Azure Resource Manager.

**Jaki jest wpływ hello na powitania przydział dla mojej subskrypcji?**

przydziały Hello hello maszyn wirtualnych, sieci wirtualnych i kont magazynu utworzonych za pomocą usługi Azure Resource Manager hello są niezależne od innych przydziałów. Każda subskrypcja pobiera przydziały toocreate hello zasobów przy użyciu hello nowych interfejsów API. Więcej o dodatkowych przydziałach hello [tutaj](../azure-subscription-service-limits.md).

**Czy mogę nadal toouse moich zautomatyzowanych skryptów do inicjowania obsługi maszyn wirtualnych, sieci wirtualnych i kont magazynu za pośrednictwem interfejsów API Menedżera zasobów hello?**

Wszystkie hello automatyzacji i skrypty, które zostały wbudowane nadal toowork dla hello istniejących maszyn wirtualnych, sieci wirtualne utworzone w trybie zarządzania usługą Azure hello. Skrypty hello jednak toobe toouse zaktualizowane hello nowego schematu tworzenia tych samych zasobów tryb usługi Resource Manager hello hello.

**Gdzie znajdę przykłady szablonów usługi Azure Resource Manager?**

Kompleksowy zestaw szablonów startowych można znaleźć w [szablonów Szybki Start usługi Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Następne kroki
* toowalk za pośrednictwem hello tworzenia szablonu, który definiuje maszyny wirtualnej, konta magazynu i sieci wirtualnej, można znaleźć [Przewodnik po szablonie usługi Resource Manager](resource-manager-template-walkthrough.md).
* toosee hello poleceń wdrażania szablonu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

