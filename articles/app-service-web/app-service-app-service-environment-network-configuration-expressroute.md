---
title: "aaaNetwork szczegóły konfiguracji do pracy z Express Route"
description: "Szczegóły konfiguracji sieci do uruchamiania środowiska usługi App Service w sieciach wirtualnych połączone tooan obwodu usługi Expressroute."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Szczegóły konfiguracji sieci dla środowisk usługi App Service przy użyciu rozwiązania ExpressRoute
## <a name="overview"></a>Omówienie
Klienci mogą się łączyć [Azure ExpressRoute] [ ExpressRoute] infrastruktury sieci wirtualnej tootheir obwód, w związku z tym rozszerzanie ich tooAzure sieci lokalnej.  Środowiska usługi aplikacji mogą być tworzone w podsieci tego [sieci wirtualnej] [ virtualnetwork] infrastruktury.  Aplikacje działające na powitania środowiska usługi aplikacji można następnie ustanawiać bezpiecznych połączeń tooback-end zasoby dostępne tylko za pośrednictwem hello połączenia ExpressRoute.  

Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** sieci wirtualnej wdrożenia klasycznego modelu.  Z ostatnie zmiany wprowadzone w czerwca 2016 ASEs również teraz można wdrożyć w sieci wirtualnych, które używają zakresy publicznych adresów lub RFC1918 przestrzeni adresów (czyli adresy prywatne). 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Wymagana jest łączność
Istnieją wymagania dotyczące łączności sieciowej środowiska usługi aplikacji, które mogą nie być początkowo spełnione tooan sieci wirtualnej połączenia ExpressRoute.  Środowiska usługi aplikacji wymagają wszystkie z następujących hello w kolejności toofunction prawidłowo:

* Wychodzące połączenie tooAzure magazynu punktów końcowych sieci na całym świecie na obu portów 80 i 443.  Obejmuje to punkty końcowe znajduje się w hello tego samego regionu hello środowiska usługi aplikacji, a także punkty końcowe usługi storage znajduje się w **innych** regiony platformy Azure.  Punkty końcowe usługi Azure Storage rozwiązania w obszarze hello następujące domeny DNS: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* i *file.core.windows.net*.  
* Toohello połączenia wychodzącego usługa pliki Azure na port 445.
* Punkty końcowe tooSql DB połączenia wychodzącego znajduje się w hello sam region jako hello środowiska usługi aplikacji.  Rozwiąż punkty końcowe bazy danych SQL w obszarze hello następujące domeny: *database.windows.net*.  Wymaga to otwarcie dostępu tooports 1433, 11000 11999 i 14000 14999.  Więcej informacji można znaleźć [w tym artykule na użycie portu bazy danych Sql V12](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Wychodzące połączenie toohello zarządzania platformy Azure płaszczyzny punktów końcowych sieci (punkty końcowe zarówno ASM i ARM).  Obejmuje to łączność wychodząca tooboth *management.core.windows.net* i *management.azure.com*. 
* Wychodzące połączenia sieciowego zbyt*ocsp.msocsp.com*, *mscrl.microsoft.com* i *crl.microsoft.com*.  Jest to wymagane toosupport funkcjonalność protokołu SSL.
* Witaj konfigurację systemu DNS dla sieci wirtualnej hello musi on mieć możliwość rozpoznawania wszystkie punkty końcowe hello i domeny wymienione w hello wcześniejszych punktów.  Jeśli te punkty końcowe nie powiedzie się, próby tworzenia środowiska usługi aplikacji zakończą się niepowodzeniem i istniejącego środowiska usługi App Service zostanie oznaczona jako w złej kondycji.
* Wychodzący dostęp przez port 53 jest wymagana do komunikacji przy użyciu serwerów DNS.
* Jeśli istnieje niestandardowy serwer DNS na hello drugiej bramy sieci VPN, hello serwer DNS musi być dostępny z podsieci hello zawierającej hello środowiska usługi aplikacji. 
* Hello wychodzącego ścieżki nie może przechodzić przez wewnętrzny firmowych serwerów proxy, ani może być życie tunneled tooon lokalnego.  Grozi to zmiany hello obowiązujący adres NAT ruchu wychodzącego ruchu sieciowego z hello środowiska usługi aplikacji.  Zmiana adresu NAT hello wychodzącego ruchu sieciowego w środowisku usługi aplikacji spowoduje łączności toomany błędów punktów końcowych hello wymienionych powyżej.  Powoduje to nieudanych prób tworzenia środowiska usługi aplikacji, a także wcześniej dobrej kondycji środowiska usługi App Service jest oznaczona jako w złej kondycji.  
* Przychodzące toorequired dostępu porty dla środowiska usługi App Service musi być dozwolone, zgodnie z opisem w tym [artykułu][requiredports].

wymagania dotyczące systemu DNS Hello można spełnić przez zapewnienie im prawidłowe infrastruktura DNS jest skonfigurowany i dla sieci wirtualnej hello.  Jeśli dla dowolnego hello Przyczyna konfiguracji DNS została zmieniona po utworzeniu środowiska usługi aplikacji, deweloperzy można wymusić toopick środowiska usługi aplikacji hello nowej konfiguracji DNS.  Wyzwolenie stopniowego ponowny rozruch środowiska przy użyciu hello "Restart" znajdującą się na górze bloku zarządzania środowiska usługi aplikacji hello w hello hello [portalu Azure] [ NewPortal] spowoduje, że hello toopick środowiska Witaj nowej konfiguracji DNS.

Witaj wymagania dotyczące dostępu do sieci dla ruchu przychodzącego można spełnić przez skonfigurowanie [sieciowej grupy zabezpieczeń] [ NetworkSecurityGroups] hello środowiska usługi aplikacji w podsieci tooallow hello wymagane dostępu zgodnie z opisem w tym [artykułu][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Włączenie łączności sieciowej ruchu wychodzącego dla środowiska usługi aplikacji
Domyślnie nowo utworzony obwodu ExpressRoute anonsuje trasę domyślną, który umożliwia wychodzące połączenie z Internetem.  W tej konfiguracji do środowiska usługi aplikacji będą mogli tooconnect tooother punkty końcowe systemu Azure.

Typowa konfiguracja klienta jest toodefine własnych trasa domyślna (0.0.0.0/0), która wymusza wychodzący przepływ tooinstead ruchu internetowego lokalnymi.  Tego przepływu ruchu niezmiennie dzieli środowiska usługi App Service, ponieważ ruch wychodzący hello jest zablokowane lokalnie lub NAT d tooan nierozpoznawalną zbiór adresów, które nie będą działać z różnymi punkty końcowe systemu Azure.

rozwiązanie Hello jest toodefine jednej (lub więcej) trasy zdefiniowane przez użytkownika (Udr) na powitania podsieci, która zawiera hello środowiska usługi aplikacji.  PRZEZ definiuje tras specyficzne dla podsieci, które będą honorowane zamiast hello trasy domyślnej.

Jeśli to możliwe zaleca się hello toouse następującej konfiguracji:

* konfiguracji usługi ExpressRoute Hello anonsuje 0.0.0.0/0 i domyślnie życie tuneli wszystkich ruch wychodzący lokalnymi.
* podsieci toohello przez zastosowane Hello zawierającej hello środowiska usługi aplikacji definiuje 0.0.0.0/0 z typem następnego przeskoku Internet (na przykład jest dostępne w dół w tym artykule).

Witaj połączony wpływ tych kroków jest hello na poziomie podsieci przez ma pierwszeństwo przed hello ExpressRoute wymuszone tunelowanie, w związku z tym zapewnienie wychodzący dostęp do Internetu z hello środowiska usługi aplikacji.

> [!IMPORTANT]
> Witaj tras określonych w przez **musi** jest wystarczająco konkretny, zbyt mają wyższy priorytet nad dowolnym trasy anonsowane przez hello konfiguracji usługi ExpressRoute.  w poniższym przykładzie Hello używa zakresu adresów szerokie 0.0.0.0/0 hello i jako taki może potencjalnie być przypadkowo przesłonięta przez anonsów tras za pomocą bardziej szczegółowych zakresów adresów.
> 
> Środowiska usługi aplikacji nie są obsługiwane w przypadku konfiguracji usługi ExpressRoute który **między anonsować tras z hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka**.  Konfiguracji usługi ExpressRoute, które mają publicznej komunikacji równorzędnej skonfigurowane, otrzyma anonsów tras firmy Microsoft dla dużych zestawów zakresów adresów IP firmy Microsoft Azure.  Jeśli między anonsowany w ścieżki prywatnej komunikacji równorzędnej hello tych zakresów adresów, wynik końcowy hello jest, że wszystkie pakiety wychodzącego z podsieci środowiska hello aplikacji usługi zostaną infrastruktury sieci lokalnej odbiorcy force — tunneled tooa.  Ten przepływ sieci nie jest obecnie obsługiwane w środowiskach usługi aplikacji.  Rozwiązanie toothis problemem jest toostop tras między reklamy hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka.
> 
> 

Informacje na trasy zdefiniowane przez użytkownika jest dostępna w tym [omówienie][UDROverview].  

Szczegółowe informacje na temat tworzenia i konfigurowania trasy zdefiniowane przez użytkownika jest dostępna w tym [jak tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Przykładowa konfiguracja przez środowisko usługi aplikacji
**Wymagania wstępne**

1. Instalowanie programu Azure Powershell z hello [Azure pobiera strony] [ AzureDownloads] (czerwiec 2015 lub nowszego z).  W obszarze "Narzędzia wiersza polecenia" Brak łącza "Zainstaluj", w obszarze "Środowiska Windows Powershell" instalowanego hello najnowszych poleceń cmdlet programu Powershell.
2. Zaleca się, że unikatowej podsieci został utworzony do wyłącznego użytku przez środowisko usługi aplikacji.  Dzięki temu tej podsieci toohello Udr stosowane hello będą otwierane tylko ruchu wychodzącego dla hello środowiska usługi aplikacji.
3. **Ważne**: nie należy wdrażać hello środowiska usługi aplikacji do **po** hello następujące kroki konfiguracji zostaną wykonane.  Dzięki temu, że połączenie sieciowe ruchu wychodzącego jest dostępny przed podjęciem próby wykonania toodeploy środowiska usługi aplikacji.

**Krok 1: Tworzenie tabeli tras o nazwie**

Witaj następujący fragment kodu tworzy tabelę tras o nazwie "DirectInternetRouteTable" hello regionu zachodnie nam Azure:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Krok 2: Utworzenie co najmniej jednej trasy w tabeli tras hello**

Konieczne będzie tooadd jeden lub więcej tabeli tras toohello trasy w kolejności tooenable wychodzący dostęp do Internetu.  

Witaj zalecane podejście do konfigurowania toohello wychodzący dostęp, jest Internet toodefine trasę dla 0.0.0.0/0, jak pokazano poniżej.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Należy pamiętać, tym 0.0.0.0/0 jest zakres adresów szerokie i jako takie zostaną zastąpione przez bardziej szczegółowych zakresów adresów anonsowane przez hello ExpressRoute.  toore-iteracyjne hello wcześniejszego zalecenia, przez trasa 0.0.0.0/0 powinny być używane w połączeniu z konfiguracją ExressRoute, która tylko anonsuje także 0.0.0.0/0. 

Alternatywnie można pobrać listę zakresy CIDR używanymi przez usługę Azure kompleksowe i zaktualizowane.  Witaj plik Xml zawierający wszystkie zakresy adresów Azure IP hello jest dostępna z hello [Microsoft Download Center][DownloadCenterAddressRanges].  

Należy pamiętać jednak, że te zakresy ulegną zmianom, co wymaga okresowych aktualizacji ręcznej toohello zdefiniowane przez użytkownika tras tookeep synchronizację.  Ponadto ponieważ nie istnieje domyślny górny limit 100 tras w jednym przez, będzie konieczne zbyt "podsumowania" hello Azure adres zakresów toofit w limicie trasy hello 100, pamiętając, że przez zdefiniowanych tras muszą toobe dokładniej niż hello trasy anonsowane przez użytkownika ExpressRoute.  

**Krok 3: Skojarz hello trasy tabeli toohello podsieci zawierającego hello środowiska usługi aplikacji**

ostatni krok konfiguracji Hello jest tooassociate hello trasy tabeli toohello podsieci wdrożonym hello środowiska usługi aplikacji.  Witaj poniższe polecenie powoduje skojarzenie toohello "DirectInternetRouteTable" hello "ASESubnet", który będzie zawierać ostatecznie środowiska usługi aplikacji.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Krok 4: Końcowe czynności**

Po tabeli tras hello jest powiązane toohello podsieci, zaleca się toofirst testu i Potwierdź hello przeznaczone efekt.  Na przykład wdrożyć maszynę wirtualną do podsieci hello i upewnij się, że:

* Ruch wychodzący tooboth Azure i innych niż Azure punkty końcowe wymienione wcześniej w w tym artykule jest **nie** przepływu dół hello obwodu usługi expressroute.  Jest bardzo ważne, tooverify tego zachowania, ponieważ w przypadku ruchu wychodzącego z podsieci hello nadal wymuszone tunelowane lokalnymi, tworzenie środowiska usługi aplikacji zawsze spowoduje niepowodzenie. 
* Wyszukiwania DNS dla punktów końcowych hello wspomniano wcześniej, wszystkie rozwiązuje poprawnie. 

Po hello powyżej kroki są potwierdzone, konieczne będzie maszyny wirtualnej hello toodelete ponieważ hello podsieci musi toobe "pusty" w hello powitalne czas tworzenia środowiska usługi aplikacji.

Następnie kontynuuj tworzenie środowiska usługi aplikacji!

## <a name="getting-started"></a>Wprowadzenie
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi][IntroToAppServiceEnvironment]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
