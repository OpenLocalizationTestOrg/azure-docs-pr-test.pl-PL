---
title: "aaaGeo skalowalność środowiska usługi aplikacji rozproszonych"
description: "Dowiedz się, jak toohorizontally skalowanie aplikacji przy użyciu dystrybucji geograficznie z Menedżera ruchu i środowiska usługi App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Rozproszona geograficznie skala przy użyciu środowisk usługi App Service
## <a name="overview"></a>Omówienie
Scenariusze aplikacji, które wymagają bardzo dużej skali może przekroczyć hello obliczeń zasobów pojemność dostępna tooa pojedynczego wdrożenia aplikacji.  Głosowanie aplikacji, sportowych i zdarzenia programu Rozrywka są wszystkie przykładowe scenariusze, które wymagają bardzo dużej skali. Wymagania dotyczące wysokiej skali można spełnić przez poziomie skalowania aplikacji z wieloma wdrożeniami aplikacji odbywa się w jednym regionie, a także w regionach, wymagania dotyczące ładowania extreme toohandle.

Środowiska usługi aplikacji jest idealną platformą dla poziomych skalowania w poziomie.  Po dokonaniu wyboru konfiguracji środowiska usługi aplikacji obsługujących współczynnika żądań znane, deweloperzy mogą wdrożyć dodatkowe środowiska usługi App Service w "krajarki plik cookie" sposób tooattain obciążenie żądaną godzinami szczytu.

Załóżmy na przykład aplikacji uruchomionej na konfiguracji środowiska usługi aplikacji został przetestowany toohandle 20 K żądań na sekundę (RPS).  Jeśli obciążenia szczytowego żądaną hello pojemność wynosi 100 KB RPS, następnie pięć (5) środowiska usługi App Service można tworzyć i aplikacji hello skonfigurowanego tooensure może obsłużyć hello maksymalne obciążenie planowane.

Ponieważ klienci zwykle uzyskują dostęp do aplikacji przy użyciu domeny niestandardowe (lub niestandardowych), należy deweloperzy aplikacji toodistribute sposób żądania dla wszystkich wystąpień środowiska usługi aplikacji hello.  Tooaccomplish doskonały sposób, to przy użyciu domeny niestandardowej hello tooresolve [profilu Menedżera ruchu Azure][AzureTrafficManagerProfile].  Witaj Traffic Manager profil może być skonfigurowany toopoint we wszystkich hello poszczególnych środowiska usługi App Service.  Menedżer ruchu obsługiwać automatycznie dystrybucję wszystkie hello środowiska usługi aplikacji opartych na ustawienia w profilu usługi Traffic Manager hello równoważenia obciążenia hello klientów.  Ta metoda działa niezależnie od tego, czy wszystkie środowiska usługi aplikacji hello są wdrożone w pojedynczym regionie Azure, lub wdrażanych na całym świecie, w wielu regionach platformy Azure.

Ponadto ponieważ klientom dostęp do aplikacji za pośrednictwem domeny niestandardowych hello, klienci są bez "świadomości" hello liczby środowiska usługi App Service uruchomiona aplikacja.  W związku z tym deweloperzy mogą szybko i łatwo dodawania i usuwania, oparte na obciążenie sieci obserwowanych środowiska usługi App Service.

Poniższy diagram koncepcyjny Hello przedstawia aplikacji, skalowanie w poziomie między trzy środowiska usługi App Service w pojedynczym regionie.

![Architektura koncepcyjna][ConceptualArchitecture] 

Witaj pozostałej części tematu przeprowadzi Cię przez etapy hello Konfigurowanie topologii rozproszonej hello przykładowej aplikacji przy użyciu wielu środowiska usługi App Service.

## <a name="planning-hello-topology"></a>Planowanie hello topologii
Przed rozpoczęciem budowania limit rozmiaru aplikacji rozproszonej, pomaga toohave kilka fragmentów informacji wcześniejsze.

* **Domeny niestandardowej dla aplikacji hello:** co to jest nazwa domeny niestandardowej hello, że użytkownicy będą używać aplikacji hello tooaccess?  Nazwa domeny niestandardowej hello przykładowej aplikacji hello jest *www.scalableasedemo.com*
* **Domeny usługi Traffic Manager:** nazwa domeny musi toobe wybierany podczas tworzenia [profilu Menedżera ruchu Azure][AzureTrafficManagerProfile].  Ta nazwa będzie połączona z hello *trafficmanager.net* sufiks tooregister wpisu domeny, który jest zarządzany przez Menedżera ruchu.  Dla aplikacji przykładowej hello jest wybrana nazwa hello *skalowalne pokaz ase*.  W związku z tym hello pełną nazwę domeny, który jest zarządzany przez Menedżera ruchu jest *skalowalne demo.trafficmanager.net ase*.
* **Strategia skalowania została zrozumiana. dzięki aplikacji hello:** będą zużycie aplikacji hello być rozproszone na wielu środowiska usługi App Service w pojedynczym regionie?  Wiele regionów?  Mieszane i dopasowywać w obu przypadkach efekt?  decyzja Hello powinny być oparte na oczekiwań gdzie ruchu klientów pochodzą, oraz jak dobrze hello reszty aplikacji obsługujących zaplecza infrastruktury można skalować.  Na przykład przy użyciu aplikacji bezstanowych 100% aplikacji może być ogromną skalę skalowany przy użyciu kombinacji wielu środowiska usługi App Service dla regionu Azure, pomnożona przez wdrożone w różnych regionach platformy Azure środowiska usługi App Service.  Z 15 + publicznego regiony platformy Azure dostępna toochoose z klienci mogą tworzyć naprawdę wpływu na całym świecie hiperskali aplikacji.  Przykładowa aplikacja hello używany dla tego artykułu, aby uzyskać trzy środowiska usługi aplikacji zostały utworzone w pojedynczym regionie Azure (południowo-środkowe stany).
* **Konwencja nazewnictwa dla środowiska usługi aplikacji hello:** każdego środowiska usługi aplikacji wymaga unikatowej nazwy.  Poza jednego lub dwóch środowiska usługi App Service jest przydatne toohave konwencji nazewnictwa toohelp zidentyfikować każdego środowiska usługi aplikacji.  Dla aplikacji przykładowej hello użyto prostych konwencji nazewnictwa.  Witaj nazwy środowiska usługi aplikacji hello trzech są *fe1ase*, *fe2ase*, i *fe3ase*.
* **Konwencja nazewnictwa dla aplikacji hello:** ponieważ wiele wystąpień aplikacji hello zostanie wdrożony, nazwę jest wymagane dla każdego wystąpienia aplikacji hello wdrożone.  Jedną mało znanego, ale bardzo wygodny funkcji środowiska usługi App Service jest hello, tej samej nazwie aplikacji mogą być używane w wielu środowiskach usługi aplikacji.  Ponieważ każde środowisko usługi aplikacji ma sufiks domeny unikatowy, deweloperzy można Użyj toore hello dokładnie tego samego Nazwa aplikacji w każdym środowisku.  Na przykład deweloper może mieć następujące nazwy aplikacji: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net*itp.  Dla aplikacji przykładowej hello jednak każde wystąpienie aplikacji również ma unikatową nazwę.  Witaj nazwy wystąpienia aplikacji, używane są *webfrontend1*, *webfrontend2*, i *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Konfigurowanie hello profilu Menedżera ruchu
Po wielu wystąpień aplikacji są wdrażane na wielu środowiska usługi App Service, hello wystąpień poszczególnych aplikacji może być zarejestrowany z usługą Traffic Manager.  Dla aplikacji przykładowej hello Menedżera ruchu dla wymagany jest profil *skalowalne demo.trafficmanager.net ase* która może kierować klientów tooany z powitania po wdrożeniu aplikacji wystąpień:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** wystąpienia hello przykładowej aplikacji wdrożonych na hello pierwszy środowiska usługi aplikacji.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** wystąpienia hello przykładowej aplikacji wdrożonych na hello drugi środowiska usługi aplikacji.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** wystąpienia hello przykładowej aplikacji wdrożonych na hello trzeci środowiska usługi aplikacji.

Witaj Najprostszym sposobem tooregister wiele usłudze Azure App Service punktów końcowych, wszystkich uruchomionych w hello **tego samego** region platformy Azure jest hello Powershell [pomocy technicznej usługi Azure Resource Manager Traffic Manager] [ ARMTrafficManager].  

pierwszym krokiem Hello jest toocreate profilu Menedżera ruchu Azure.  Poniższy kod Hello pokazuje, jak hello profil został utworzony dla hello przykładową aplikację:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Zwróć uwagę, jak hello *RelativeDnsName* zbyt ustawiono parametr*skalowalne pokaz ase*.  Jak jest to hello nazwy domeny *skalowalne demo.trafficmanager.net ase* skojarzonego z profilem Menedżera ruchu.

Witaj *TrafficRoutingMethod* zasad Menedżera ruchu użyje toodetermine jak obciążenia klientów toospread we wszystkich dostępnych punktów końcowych hello równoważenia obciążenia hello definiuje parametru.  W tym hello przykład *ważone* wybrano metodę.  Spowoduje to żądania klientów są rozkładane wszystkie punkty końcowe aplikacji hello zarejestrowany oparte na powitania względnych wag skojarzone z każdym punkcie końcowym. 

Utworzony profil hello każde wystąpienie aplikacji jest dodawana toohello profilu jako natywny punktu końcowego platformy Azure.  Witaj poniższy kod pobiera odwołanie do aplikacji sieci web frontonu tooeach, a następnie dodanie każdej aplikacji jako punktu końcowego Menedżera ruchu na powitania *element TargetResourceId* parametru.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Zwróć uwagę, jak istnieje jedno wywołanie za*AzureTrafficManagerEndpointConfig Dodaj* dla każdego wystąpienia poszczególnych aplikacji.  Witaj *element TargetResourceId* parametr w każdej polecenia programu Powershell odwołuje się do jednego z trzech przypadkach wdrożonej aplikacji hello.  Hello profilu Menedżera ruchu zostaną rozkładu obciążenia we wszystkich trzech punktów końcowych w zarejestrowany w profilu hello.

Wszystkie trzy punkty końcowe używać hello hello tę samą wartość (10) hello *wagi* parametru.  W efekcie żądania klientów rozmieszczania Menedżer ruchu we wszystkich wystąpieniach aplikacji trzy równomierne. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Domeny niestandardowe wskazujące aplikacji hello na powitania domeny usługi Traffic Manager
Witaj w ostatnim kroku niezbędne jest toopoint hello domeny niestandardowej aplikacji hello na powitania domeny usługi Traffic Manager.  Hello przykładowej aplikacji to oznacza wskazanie *www.scalableasedemo.com* w *skalowalne demo.trafficmanager.net ase*.  Ten krok wymaga toobe zostało ukończone z Rejestratora domen hello zarządzanego hello domeny niestandardowej.  

Przy użyciu narzędzia do zarządzania rejestratora domen, toobe potrzeb rekordów CNAME utworzono których punkty domenę niestandardową hello na powitania domeny usługi Traffic Manager.  Obraz powitania poniżej przedstawiono przykład tej konfiguracji CNAME wygląda następująco:

![CNAME dla domeny niestandardowej][CNAMEforCustomDomain] 

Mimo że nie omówione w tym temacie, należy pamiętać, że każde wystąpienie poszczególnych aplikacji wymaga domeny niestandardowej hello toohave również zarejestrowany z nim.  W przeciwnym razie jeśli żądanie ułatwia tooan wystąpienia aplikacji, a aplikacja hello nie ma hello domeny niestandardowej w zarejestrowany aplikacji hello, hello żądanie zakończy się niepowodzeniem.  

W tym hello przykład domena niestandardowa jest *www.scalableasedemo.com*, a każde wystąpienie aplikacji ma niestandardową domenę hello skojarzonych z nim.

![Domena niestandardowa][CustomDomain] 

Aby drużyn z rejestrowania domeny niestandardowej z aplikacjami Azure App Service, zobacz hello poniższego artykułu [rejestracji domen niestandardowych][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Testuje hello Topologia rozproszona
Hello wynik końcowy konfiguracji Menedżera ruchu i DNS hello jest która zażąda *www.scalableasedemo.com* będzie przechodził przez hello w następującej kolejności:

1. Przeglądarki lub urządzenia spowoduje wyszukiwania DNS *www.scalableasedemo.com*
2. Witaj wpis CNAME u rejestratora domen hello powoduje, że hello DNS wyszukiwania toobe przekierowanie tooAzure Menedżera ruchu.
3. Wyszukiwania DNS jest przewidzieć *skalowalne demo.trafficmanager.net ase* na jednym z serwerów DNS Menedżera ruchu Azure hello.
4. Oparte na zasada równoważenia obciążenia hello (hello *TrafficRoutingMethod* parametru użytego wcześniej podczas tworzenia profilu usługi Traffic Manager hello), zostanie Menedżera ruchu, wybierz jeden hello punkty końcowe skonfigurowane i zwracać hello FQDN tego punkt końcowy toohello przeglądarki lub urządzenia.
5. Ponieważ hello FQDN punktu końcowego hello jest adres Url wystąpienia aplikacji uruchomionych na środowisku usługi aplikacji hello, hello przeglądarki lub urządzenie zapyta, serwer DNS firmy Microsoft Azure hello tooresolve adres IP tooan nazwy FQDN. 
6. Przeglądarka Hello lub urządzenie będzie wysyłać hello — adres IP toohello żądania HTTP/S.  
7. Żądanie hello pojawią się w jednym z wystąpień aplikacji hello uruchomiona na powitania środowiska usługi App Service.

Witaj konsoli obraz poniżej przedstawia wyszukiwania DNS dla hello Przykładowa aplikacja domeny niestandardowej pomyślnie rozpoznawania tooan aplikacji wystąpienia uruchomiona na powitania trzech przykładu środowiska usługi App Service (w tym przypadku hello sekundę środowiska usługi aplikacji hello trzech):

![Wyszukiwania DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Linki do dodatkowych i informacji
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Dokumentacja hello Powershell [pomocy technicznej usługi Azure Resource Manager Traffic Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
