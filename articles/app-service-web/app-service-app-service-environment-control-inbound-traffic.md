---
title: "aaaHow tooControl ruch przychodzący tooan środowiska usługi aplikacji"
description: "Więcej informacji na temat sposobu toocontrol reguły zabezpieczeń sieci tooconfigure ruchu przychodzącego ruchu tooan środowiska usługi aplikacji."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Jak tooControl ruch przychodzący tooan środowiska usługi aplikacji
## <a name="overview"></a>Omówienie
Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** klasycznego modelu wdrażania [sieci wirtualnej][virtualnetwork].  Można zdefiniować nowej sieci wirtualnej i nową podsieć w czasie hello tworzenia środowiska usługi aplikacji.  Alternatywnie można utworzyć środowiska usługi aplikacji w istniejącej sieci wirtualnej i wstępnie istniejącą podsieć.  Wraz ze zmianą w czerwca 2016 ASEs można także wdrożyć w sieci wirtualnych, które używają zakresy publicznych adresów lub RFC1918 przestrzeni adresów (czyli adresy prywatne).  Więcej informacji na temat tworzenia środowiska usługi aplikacji można znaleźć [jak tooCreate środowiska usługi aplikacji][HowToCreateAnAppServiceEnvironment].

Środowiska usługi aplikacji zawsze należy utworzyć w podsieci, ponieważ podsieć zawiera granic sieci, które mogą być używane toolock przychodzący ruch związany z nadrzędnego urządzeń i usług w dół tak, aby ruchu HTTP i HTTPS jest dopuszczalne tylko z określonych nadrzędnego Adresy IP.

Przychodzący i wychodzący ruch sieciowy w podsieci jest kontrolowany przy użyciu [sieciowej grupy zabezpieczeń][NetworkSecurityGroups]. Kontrolowanie ruchu przychodzącego wymaga tworzenia reguły zabezpieczeń sieciowych w grupie zabezpieczeń sieci, a następnie przypisanie hello sieci zabezpieczeń grupy hello podsieci zawierającego hello środowiska usługi aplikacji.

Gdy grupa zabezpieczeń sieci jest przypisany tooa podsieci, tooapps ruch przychodzący w powitalne środowiska usługi aplikacji może być dozwolone/blokowane na podstawie hello zezwalania i odmowy reguł zdefiniowanych w hello sieciowej grupy zabezpieczeń.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Przychodzący porty używane w środowisku usługi aplikacji
Przed blokowania przychodzącego ruchu sieciowego z sieciową grupą zabezpieczeń, jest ważne tooknow hello zbiór wymaganych i opcjonalnych porty używane przez środowisko usługi aplikacji.  Przypadkowo zamknięcia poza porty toosome ruchu może spowodować utratę funkcjonalności w środowisku usługi aplikacji.

Witaj poniżej znajduje się lista portów używanych przez środowisko usługi aplikacji. Wszystkie porty są **TCP**, chyba że wyraźnie inaczej:

* 454: **wymagany port** używanych przez infrastrukturę platformy Azure do zarządzania i obsługi środowiska usługi App Service za pomocą protokołu SSL.  Nie należy blokować ruchu toothis portu.  Port ten jest zawsze publiczny VIP toohello związanego z ASE.
* 455: **wymagany port** używanych przez infrastrukturę platformy Azure do zarządzania i obsługi środowiska usługi App Service za pomocą protokołu SSL.  Nie należy blokować ruchu toothis portu.  Port ten jest zawsze publiczny VIP toohello związanego z ASE.
* 80: domyślny port dla ruchu przychodzącego tooapps ruch HTTP w plany usługi App Service w środowisku usługi aplikacji.  W elemencie ASE włączone ILB ten port jest adresem ILB toohello powiązane hello ASE.
* 443: domyślny port dla ruchu przychodzącego tooapps ruchu protokołu SSL w plany usługi App Service w środowisku usługi aplikacji.  W elemencie ASE włączone ILB ten port jest adresem ILB toohello powiązane hello ASE.
* 21: kanału kontroli w przypadku usługi FTP.  Ten port można bezpiecznie zablokowane, jeśli nie jest używany FTP.  W elemencie ASE włączone ILB ten port może być powiązane toohello adres ILB ASE.
* 990: kanał kontrolny dla FTPS.  Ten port można bezpiecznie zablokowane, jeśli nie jest używany FTPS.  W elemencie ASE włączone ILB ten port może być powiązane toohello adres ILB ASE.
* 10001 10020: kanały danych w przypadku usługi FTP.  Zgodnie z hello kanału kontroli, te porty mogą bezpiecznie zablokowane, jeśli FTP nie jest używany.  W elemencie ASE włączone ILB ten port może być adresem ILB powiązane toohello ASE na.
* 4016: używanej do zdalnego debugowania w programie Visual Studio 2012.  Ten port można bezpiecznie zablokowane, jeśli nie jest używana funkcja hello.  W elemencie ASE włączone ILB ten port jest adresem ILB toohello powiązane hello ASE.
* 4018: używany do zdalnego debugowania za pomocą programu Visual Studio 2013.  Ten port można bezpiecznie zablokowane, jeśli nie jest używana funkcja hello.  W elemencie ASE włączone ILB ten port jest adresem ILB toohello powiązane hello ASE.
* 4020: używany do zdalnego debugowania za pomocą programu Visual Studio 2015.  Ten port można bezpiecznie zablokowane, jeśli nie jest używana funkcja hello.  W elemencie ASE włączone ILB ten port jest adresem ILB toohello powiązane hello ASE.

## <a name="outbound-connectivity-and-dns-requirements"></a>Łączność wychodząca i wymagania dotyczące systemu DNS
Dla środowiska usługi aplikacji toofunction poprawnie, wymagany jest również punktami końcowymi toovarious wychodzący dostęp. Pełną listę zewnętrzne punkty końcowe hello używane przez ASE jest hello sekcji "Wymagana łączność sieciową" hello [konfiguracji sieci ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) artykułu.

Środowiska usługi aplikacji wymagają skonfigurowanej dla sieci wirtualnej hello prawidłowy infrastruktury DNS.  Jeśli dla dowolnego hello Przyczyna konfiguracji DNS została zmieniona po utworzeniu środowiska usługi aplikacji, deweloperzy można wymusić toopick środowiska usługi aplikacji hello nowej konfiguracji DNS.  Wyzwolenie stopniowego ponowny rozruch środowiska przy użyciu hello "Restart" znajdującą się na górze bloku zarządzania środowiska usługi aplikacji hello w hello hello [portalu Azure] [ NewPortal] spowoduje, że hello toopick środowiska Witaj nowej konfiguracji DNS.

Zalecane jest również, że żadnych niestandardowych serwerów DNS w sieci wirtualnej hello należy skonfigurować przed toocreating wcześniejsze czasu środowiska usługi aplikacji.  Konfiguracja DNS sieci wirtualnej zostanie zmieniona, podczas tworzenia środowiska usługi aplikacji, która spowoduje niepowodzenie procesu tworzenia środowiska usługi aplikacji hello.  W podobny szyjnej Jeśli istnieje niestandardowy serwer DNS na powitania drugiej bramy sieci VPN, a serwer DNS hello jest hello jest nieosiągalny lub jest niedostępny, również zakończą się proces tworzenia środowiska usługi aplikacji.

## <a name="creating-a-network-security-group"></a>Tworzenie grupy zabezpieczeń sieci
Szczegółowe informacje o sposobie działania grup zabezpieczeń sieci można znaleźć w następujących hello [informacji][NetworkSecurityGroups].  przykład Witaj zarządzania usługą Azure poniżej poprawki na prezentuje grup zabezpieczeń sieci, nacisk na konfigurowanie i stosowanie podsieci tooa grupy zabezpieczeń sieci, która zawiera środowiska usługi aplikacji.

**Uwaga:** grup zabezpieczeń sieci można skonfigurować, używając graficznie hello [Azure Portal](https://portal.azure.com) lub za pomocą programu Azure PowerShell.

Grupy zabezpieczeń sieci najpierw są tworzone jako element autonomiczny skojarzone z subskrypcją. Ponieważ grupy zabezpieczeń sieci są tworzone w regionie Azure, upewnij się, tę grupę zabezpieczeń sieci hello jest tworzony w hello sam region jako hello środowiska usługi aplikacji.

Hello poniżej przedstawiono tworzenie grupy zabezpieczeń sieci:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Po utworzeniu grupy zabezpieczeń sieci, co najmniej jednej reguły zabezpieczeń sieci są dodawane tooit.  Ponieważ hello zestawu reguł może ulec zmianie, zaleca się toospace limit hello schematu numerowania używane w przypadku toomake priorytety reguł go łatwo tooinsert dodatkowe reguły wraz z upływem czasu.

Witaj w poniższym przykładzie przedstawiono regułę, która jawnie udziela dostępu toohello zarządzania portów przez hello toomanage infrastruktury platformy Azure i obsługa środowiska usługi aplikacji.  Należy pamiętać, że cały ruch zarządzania przepływa za pośrednictwem protokołu SSL i jest zabezpieczone certyfikaty klienta, nawet jeśli są otwarte porty hello są niedostępne dla dowolnej jednostki inne niż infrastruktura zarządzania platformy Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Podczas blokowania dostępu tooport 80 i 443 zbyt "ukryć" środowiska usługi aplikacji za nadrzędnego urządzenia lub usługi, konieczne będzie tooknow hello nadrzędnego adresu IP.  Na przykład, jeśli używasz zapory aplikacji sieci web (WAF) hello zapory aplikacji sieci Web będzie mieć własny adres IP (lub adresy), których używa podczas obliczania tooa ruchu pośredniczenie podrzędne środowiska usługi aplikacji.  Konieczne będzie toouse ten adres IP w hello *SourceAddressPrefix* parametru reguły zabezpieczeń sieci.

W poniższym przykładzie hello ruch przychodzący z określonego adresu IP nadrzędnego jest jawnie dozwolone.  Witaj adres *1.2.3.4* jest używany jako symbol zastępczy dla adresu IP hello nadrzędnego zapory aplikacji sieci Web.  Zmień hello wartość toomatch hello adres używany przez urządzenie nadrzędnego lub usługi.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

W razie potrzeby Obsługa FTP hello reguły może służyć jako port kontroli szablonu toogrant dostępu toohello FTP i portów kanału danych.  Ponieważ FTP jest protokołem stanowe, mogą nie być możliwe tooroute FTP ruchu za pośrednictwem tradycyjnych urządzenia zapory lub serwera proxy HTTP/HTTPS.  W takim przypadku należy tooset hello *SourceAddressPrefix* tooa innej wartości — na przykład hello IP zakres maszyn deweloperem lub wdrażania na FTP, które działają klienci adresów. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Uwaga:** zakres portów kanału danych hello mogą ulec zmianie podczas okresu zapoznawczego hello.)

Jeśli debugowanie zdalne z programem Visual Studio jest używany, hello reguły pokazują, jak uzyskać dostęp do toogrant.  Istnieje reguła osobne dla każdej obsługiwanej wersji programu Visual Studio, ponieważ każda wersja używa innego portu do zdalnego debugowania.  Podobnie jak w przypadku dostępu FTP zdalnego debugowania ruchu może nie odzwierciedlać prawidłowo za pośrednictwem tradycyjnych zapory aplikacji sieci Web lub serwera proxy urządzenia.  Witaj *SourceAddressPrefix* zamiast tego można ustawić zakresu adresów IP toohello maszyn developer działanie programu Visual Studio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Przypisywanie sieciowej grupy zabezpieczeń tooa podsieci
Grupa zabezpieczeń sieci ma domyślną regułę zabezpieczeń, która nie zezwala na ruch zewnętrzny tooall dostępu.  Witaj w wyniku łączenia reguły zabezpieczeń sieciowych hello opisano powyżej i hello domyślną regułę zabezpieczeń blokuje ruch przychodzący, jest, że tylko na ruch z zakresów adresów źródłowy skojarzony z *Zezwalaj* będzie akcji tooapps ruchu toosend uruchomione w środowisku usługi aplikacji.

Po sieciowej grupy zabezpieczeń jest wypełniane przy użyciu reguły zabezpieczeń, musi podsieci toohello toobe przypisane zawierającej hello środowiska usługi aplikacji.  polecenie przypisania Hello odwołuje się zarówno nazwę hello hello sieci wirtualnej, której hello środowiska usługi aplikacji znajduje się oraz hello nazwy podsieci hello, w której utworzono hello środowiska usługi aplikacji.  

przykład Witaj poniżej przedstawia sieciowej grupy zabezpieczeń przypisywane tooa podsieci i sieci wirtualnej:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Po pomyślnym hello przypisanie do grupy zabezpieczeń sieci (przypisania hello jest długotrwałych operacji i może potrwać kilka minut toocomplete), tylko ruchu przychodzącego ruchu dopasowania *Zezwalaj* reguły pomyślnie osiągną aplikacji w aplikacji hello Środowisko usługi.

Witaj kompletności poniższy przykład przedstawia, jak tooremove i w związku z tym zabezpieczenia sieci hello rozłączone kojarzenia grupy z podsieci hello:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Uwagi dotyczące protokołu SSL jawnego adresu IP
Jeśli aplikacja jest konfigurowana jawne adresów IP protokołu SSL (dotyczy *tylko* tooASEs, który ma publicznego adresu VIP), zamiast używać hello domyślny adres IP hello środowiska usługi aplikacji, HTTP i HTTPS ruchu, jest przenoszony do podsieci hello za pośrednictwem innego zestawu porty inne niż porty 80 i 443.

Poszczególne pary Hello porty używane przez każdy adres IP SSL można znaleźć w interfejsie użytkownika portalu hello z bloku UX szczegóły środowiska hello aplikacji usługi.  Wybierz opcję "wszystkie ustawienia"--> "Adresów IP".  Blok Hello "adresów IP" zawiera spis wszystkich jawnie skonfigurowanych adresów IP protokołu SSL dla hello środowiska usługi aplikacji, wraz z pary port specjalny hello, która jest używana tooroute ruchu HTTP i HTTPS skojarzone z poszczególnych adresów IP protokołu SSL.  Jest to pary portu, wymagającym toobe używane dla parametrów DestinationPortRange hello, podczas konfigurowania reguły do grupy zabezpieczeń sieci.

Aplikację na elemencie ASE po skonfigurowanym toouse IP SSL klientów zewnętrznych nie będą widzieć i nie ma potrzeby tooworry o hello port specjalny pary mapowania.  Aplikacje toohello ruch będzie przepływać zwykle toohello skonfigurowany adres IP SSL.  Hello tłumaczenia toohello port specjalny pary automatycznie odbywa się wewnętrznie podczas końcowej gałęzi hello routingu ruchu w hello podsieci zawierającego hello ASE. 

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi][IntroToAppServiceEnvironment]

Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Szczegółowe wokół aplikacji bezpiecznego połączenia toobackend zasobów ze środowiska usługi aplikacji, zobacz [bezpieczne łączenie zasobów tooBackend ze środowiska usługi aplikacji][SecurelyConnecttoBackend]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

