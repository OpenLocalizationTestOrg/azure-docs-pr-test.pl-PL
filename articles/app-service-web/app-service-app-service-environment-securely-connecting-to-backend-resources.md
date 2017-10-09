---
title: "aaaSecurely tooBackEnd łączenie zasobów z środowiska usługi aplikacji"
description: "Więcej informacji na temat sposobu toosecurely łączenie zasobów toobackend ze środowiska usługi aplikacji."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>Bezpieczne łączenie tooBackend zasobów ze środowiska usługi aplikacji
## <a name="overview"></a>Omówienie
Od chwili utworzenia środowiska usługi aplikacji jest zawsze w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** klasycznego modelu wdrażania [sieci wirtualnej] [ virtualnetwork], przepływ wyłącznie za pośrednictwem sieci wirtualnej hello połączenia wychodzące z zasobami zaplecza tooother środowiska usługi aplikacji.  Z ostatnie zmiany wprowadzone w czerwca 2016 ASEs można także wdrożyć w sieci wirtualnych, które używają zakresy publicznych adresów lub RFC1918 przestrzeni adresów (czyli adresy prywatne).  

Na przykład może być programu SQL Server w klastrze maszyn wirtualnych z portu 1433 zablokowana.  punkt końcowy Hello może być ACLd tooonly zezwolić na dostęp z innych zasobów na hello tej samej sieci wirtualnej.  

Inny przykład poufnych punkty końcowe może uruchomić lokalnie i być tooAzure połączonych za pośrednictwem albo [lokacja-lokacja] [ SiteToSite] lub [Azure ExpressRoute] [ ExpressRoute] połączenia.  W związku z tym zasobów tylko w sieciach wirtualnych połączona toohello lokacja-lokacja lub ExpressRoute tunele będą punkty końcowe lokalnymi tooaccess stanie.

Dla wszystkich tych scenariuszach aplikacje działające w środowisku usługi aplikacji będzie można toosecurely stanie łączyć toohello różnych serwerów i zasobów.  Ruch wychodzący z aplikacji działających w punktów końcowych tooprivate środowiska usługi aplikacji w hello tej samej sieci wirtualnej (lub podłączone toohello tej samej sieci wirtualnej), zostanie tylko przepływ hello sieci wirtualnej.  Tooprivate ruchu wychodzącego, które punkty końcowe nie będzie przepływać przez hello publicznej sieci Internet.

Jedno zastrzeżenie: dotyczy ruchu toooutbound z tooendpoints środowiska usługi aplikacji w ramach sieci wirtualnej.  Środowiska usługi App Service można nawiązać połączenia z punktami końcowymi maszyn wirtualnych znajdujących się w hello **tego samego** podsieci jako hello środowiska usługi aplikacji.  To zwykle nie powinna być problem tak długo, jak środowiska usługi App Service są wdrażane w podsieci zarezerwowane do wyłącznego użytku przez hello środowiska usługi aplikacji.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Łączność wychodząca i wymagania dotyczące systemu DNS
Dla środowiska usługi aplikacji toofunction poprawnie, wymaga punkty końcowe toovarious wychodzący dostęp. Pełną listę zewnętrzne punkty końcowe hello używane przez ASE jest hello sekcji "Wymagana łączność sieciową" hello [konfiguracji sieci ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artykułu.

Środowiska usługi aplikacji wymagają skonfigurowanej dla sieci wirtualnej hello prawidłowy infrastruktury DNS.  Jeśli dla dowolnego hello Przyczyna konfiguracji DNS została zmieniona po utworzeniu środowiska usługi aplikacji, deweloperzy można wymusić toopick środowiska usługi aplikacji hello nowej konfiguracji DNS.  Wyzwolenie stopniowego ponowny rozruch środowiska za pomocą ikony "Restart" hello, znajdujący się u góry hello hello środowiska usługi aplikacji blok zarządzania w portalu hello spowoduje toopick środowiska hello hello nowej konfiguracji DNS.

Zalecane jest również, że żadnych niestandardowych serwerów DNS w sieci wirtualnej hello należy skonfigurować przed toocreating wcześniejsze czasu środowiska usługi aplikacji.  Konfiguracja DNS sieci wirtualnej zostanie zmieniona, podczas tworzenia środowiska usługi aplikacji, która spowoduje niepowodzenie procesu tworzenia środowiska usługi aplikacji hello.  W podobny szyjnej Jeśli istnieje niestandardowy serwer DNS na powitania drugiej bramy sieci VPN, a serwer DNS hello jest hello jest nieosiągalny lub jest niedostępny, również zakończą się proces tworzenia środowiska usługi aplikacji.

## <a name="connecting-tooa-sql-server"></a>Łączenie tooa programu SQL Server
Typowe konfiguracje programu SQL Server ma punktu końcowego nasłuchiwania na porcie 1433:

![Punkt końcowy serwera SQL][SqlServerEndpoint]

Istnieją dwa podejścia do ograniczania ruchu toothis końcowego:

* [Listy kontroli dostępu do sieci] [ NetworkAccessControlLists] (listy ACL sieci)
* [Grupy zabezpieczeń sieci][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Ograniczanie dostępu do sieci listy kontroli dostępu
Port 1433 mogą być chronione przy użyciu listy kontroli dostępu do sieci.  przykład Witaj poniżej klienta whitelists adresów pochodzące z wewnątrz sieci wirtualnej i zablokuje dostęp tooall innych klientów.

![Przykład listy kontroli dostępu do sieci][NetworkAccessControlListExample]

Wszystkie aplikacje uruchomione w środowisku usługi aplikacji w tej samej sieci wirtualnej Witaj, ponieważ hello programu SQL Server będzie wystąpienia programu SQL Server toohello tooconnect możliwe przy użyciu hello **wewnętrznej sieci wirtualnej** adres IP dla maszyny wirtualnej hello programu SQL Server.  

Parametry połączenia przykład Hello poniżej odwołania hello SQL Server przy użyciu prywatnego adresu IP.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Mimo że hello maszyna wirtualna ma publiczny punkt końcowy również, próby nawiązania połączenia z użyciem hello publiczny adres IP zostanie odrzucone z powodu sieci hello listy ACL. 

## <a name="restricting-access-with-a-network-security-group"></a>Ograniczanie dostępu z sieciową grupą zabezpieczeń
Informacje o innym podejściu do zabezpieczania dostępu jest z sieciową grupą zabezpieczeń.  Grupy zabezpieczeń sieci może być zastosowane tooindividual maszyn wirtualnych lub podsieci tooa zawierających maszyny wirtualne.

Grupa zabezpieczeń sieci musi najpierw toobe utworzone:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Ograniczanie dostępu tooonly ruchu w sieci wewnętrznej jest bardzo prosty z sieciową grupą zabezpieczeń.  reguły domyślne Hello w grupie zabezpieczeń sieci tylko zezwalają na dostęp z innych klientów sieci w hello tej samej sieci wirtualnej.

W związku z tym blokowania dostępu tooSQL serwer jest tak proste, jak stosowanie sieciową grupę zabezpieczeń z jego domyślne zasady tooeither hello maszynami wirtualnymi programu SQL Server lub podsieci hello zawierającej hello maszyn wirtualnych.

Poniższy przykład Hello stosuje zabezpieczeń grupy toohello zawierający podsieci:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

wynik końcowy Hello jest zestaw reguł zabezpieczeń, które blokują dostęp zewnętrznych, umożliwiając dostęp do sieci wirtualnej:

![Reguły zabezpieczeń sieciowych domyślne][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>Wprowadzenie
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi][IntroToAppServiceEnvironment]

Szczegółowe wokół kontrolowanie ruchu przychodzącego tooyour środowiska usługi aplikacji, zobacz [kontrolowanie ruchu przychodzącego tooan środowiska usługi aplikacji][ControlInboundASE]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
