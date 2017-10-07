---
title: "aaaLayered Architektura zabezpieczeń ze środowiska usługi App Service"
description: "Implementacja architektury zabezpieczeń warstwowych, ze środowiska usługi App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implementacja architektury zabezpieczeń warstwowych, ze środowiska usługi aplikacji
## <a name="overview"></a>Omówienie
Ponieważ środowiska usługi App Service udostępniają odizolowanym środowisku uruchomieniowym wdrożony w sieci wirtualnej, deweloperzy mogą tworzyć architektury zabezpieczeń warstwowych, zapewniając różne poziomy dostępu do sieci dla każdej warstwy aplikacji fizycznych.

Wspólne dążenie jest toohide interfejsu API zapleczy z dostępem do Internetu ogólne i Zezwalaj tylko na interfejsy API toobe wywoływany przez aplikacje sieci web nadrzędnego.  [Sieciowe grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] mogą być używane w podsieci zawierający aplikacje tooAPI dostępu publicznego toorestrict środowiska usługi App Service.

Hello Poniższy diagram przedstawia architekturę przykład z aplikacją WebAPI na podstawie wdrożony w środowisku usługi aplikacji.  Trzy wystąpienia aplikacji sieci web w osobnych, wdrożone na trzy osobne środowiska usługi aplikacji należy toohello zaplecza wywołania tej samej aplikacji WebAPI.

![Architektura koncepcyjna][ConceptualArchitecture] 

Witaj zielony znak plus wskazać, że hello sieciowej grupy zabezpieczeń w podsieci hello zawierający "apiase" umożliwia wywołania z hello aplikacji sieci web nadrzędnego jako dobrze wywołania po sobie samym.  Jednak hello tej samej grupy zabezpieczeń sieci jawnie nie zezwala na dostęp do toogeneral ruchu przychodzącego ruchu z hello Internet. 

Witaj pozostałej części tego tematu przeprowadzi Cię przez hello kroki potrzebne tooconfigure hello sieciowej grupy zabezpieczeń w podsieci hello zawierający "apiase".

## <a name="determining-hello-network-behavior"></a>Określanie hello zachowanie sieci
W kolejności tooknow zabezpieczenia sieci, jakie potrzebne są zasady, konieczne toodetermine klientów sieci, które mogą być tooreach hello środowiska usługi aplikacji zawierającego hello aplikacji interfejsu API i których klienci będą blokowane.

Ponieważ [sieciowej grupy zabezpieczeń (NSG)] [ NetworkSecurityGroups] są stosowane toosubnets i środowiska usługi App Service są wdrażane na podsieci, hello reguły zawarte w grupy NSG stosuje się zbyt**wszystkie** aplikacje działające w środowisku usługi aplikacji.  Przy użyciu hello przykładowa architektura tego artykułu, grupy zabezpieczeń sieci po podsieci zastosowane toohello zawierającej "apiase", wszystkie aplikacje uruchomione na powitania "apiase" środowiska usługi aplikacji, które będą chronione za pomocą hello sam zestaw reguł zabezpieczeń. 

* **Określić hello wychodzący adres IP nadrzędnego obiektów wywołujących:** co to jest hello adres lub adresy IP z wywołań nadrzędnego hello?  Te adresy muszą toobe jawnie dozwolone w hello NSG dostępu.  Ponieważ wywołań między środowiska usługi App Service są traktowane jako wywołania "Internet", oznacza to hello wychodzącego IP przypisany adres tooeach z hello trzy nadrzędnego środowiska usługi App Service musi toobe zezwolenie na dostęp w hello NSG dla podsieci "apiase" hello.   Aby uzyskać więcej informacji na temat określania hello wychodzący adres IP, aplikacje działające w środowisku usługi aplikacji można znaleźć hello [architektury sieci] [ NetworkArchitecture] artykuł z omówieniem.
* **Aplikacja interfejsu API zaplecza hello należy toocall się?**  Czasami ich i niewielkie punkt jest scenariusz hello których hello zaplecza aplikacji wymaga toocall samej siebie.  Jeśli w aplikacji interfejsu API zaplecza w środowisku usługi aplikacji wymaga toocall samego, to także traktowane jako wywołanie "Internet".  W architekturze próbki hello wymaga zezwalania na dostęp z hello wychodzący adres IP hello "apiase" środowiska usługi aplikacji oraz.

## <a name="setting-up-hello-network-security-group"></a>Konfigurowanie hello grupy zabezpieczeń sieci
Po ustawieniu hello z wychodzących adresów IP są znane, hello następnym krokiem jest tooconstruct grupy zabezpieczeń sieci.  Można utworzyć grupy zabezpieczeń sieci dla obu Menedżera zasobów opartych na sieci wirtualnych, a także klasycznych sieci wirtualnych.  Poniższe przykłady Hello Pokaż tworzenia i konfigurowania grupy NSG w klasycznym sieci wirtualnej przy użyciu programu Powershell.

Dla architektury próbki hello środowisk hello znajdują się w południowo-środkowe stany, więc pusta grupa NSG jest tworzona w tym regionie:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

Najpierw jawnie zezwolić na reguła jest dodawana hello infrastruktury zarządzania platformy Azure, zgodnie z opisem w artykule hello na [ruch przychodzący] [ InboundTraffic] dla środowiska usługi App Service.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Następnie dwie reguły są dodawane tooallow HTTP i HTTPS wywołania z hello pierwszy nadrzędnego środowiska usługi aplikacji ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Płukania i powtórz te czynności dla hello drugiego i trzeciego nadrzędnego środowiska usługi App Service ("fe2ase" i "fe3ase").

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Ponadto należy udzielić dostępu toohello wychodzący adres IP środowiska usługi aplikacji hello zaplecza interfejsu API, dzięki czemu można wywołania zwrotnego do samej siebie.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Nie inne reguły zabezpieczeń sieciowych muszą toobe skonfigurowany, ponieważ co grupa NSG zawiera zestaw reguł domyślnych, które blokują dostęp przychodzące z Internetu hello domyślnie.

Poniżej przedstawiono pełną listę reguł w grupie zabezpieczeń sieci hello Hello.  Należy zwrócić uwagę, jak reguły ostatniego hello, który zostanie wyróżniona, blokuje przychodzące dostęp z wszystkich wywołań innych niż te, które jawnie przyznano dostęp.

![Konfiguracja grupy NSG][NSGConfiguration] 

Ostatnim krokiem Hello jest tooapply hello NSG toohello podsieci, która zawiera hello "apiase" środowiska usługi aplikacji.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Z podsiecią toohello grupa NSG stosowana hello hello trzy nadrzędnego środowiska usługi App Service i hello środowiska usługi aplikacji hello zawierającego zaplecza interfejsu API, dozwolone są tylko toocall do środowiska "apiase" hello.

## <a name="additional-links-and-information"></a>Linki do dodatkowych i informacji
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Informacje o [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md). 

Opis [wychodzących adresów IP] [ NetworkArchitecture] i środowiska usługi App Service.

[Porty sieciowe] [ InboundTraffic] używane przez środowiska usługi App Service.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
