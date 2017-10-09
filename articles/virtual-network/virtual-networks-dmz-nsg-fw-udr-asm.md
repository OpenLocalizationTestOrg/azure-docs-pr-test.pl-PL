---
title: "Przykład — aaaDMZ kompilacji DMZ tooProtect sieci z zapory, przez i NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ za pomocą zapory, zdefiniowane przez użytkownika routingu (przez) i grupy zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Przykład 3 — Tworzenie DMZ tooProtect sieci z zapory, przez i grupy NSG
[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]

W tym przykładzie utworzy strefą DMZ z zapory, cztery serwery z systemem windows, użytkownik zdefiniowane routingu, przesyłania dalej protokołu IP i grup zabezpieczeń sieci. On również przeprowadzi każdego tooprovide odpowiednich poleceń hello głębsze zrozumienie każdego kroku. Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ. Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy. 

![Dwukierunkowe DMZ NVA, NSG i przez][1]

## <a name="environment-setup"></a>Konfigurowanie środowiska
W tym przykładzie jest subskrypcji, która zawiera następujące hello:

* Trzy usługi w chmurze: "SecSvc001", "FrontEnd001" i "BackEnd001"
* "CorpNetwork" przy użyciu trzech podsieci sieci wirtualnej: "SecNet", "Fronton" i "Wewnętrzna"
* Urządzenie wirtualne sieci, w tym przykładzie zaporą, podłączone podsieci SecNet toohello
* Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwa okna serwerów, które reprezentują aplikacji z powrotem kończyć serwery ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")

W sekcji odwołań hello poniżej jest skrypt programu PowerShell, który zostanie skompilowany większość środowiska hello opisane powyżej. Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie.

toobuild hello środowiska:

1. Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)
2. Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi itp.)
3. Uruchom skrypt hello w programie PowerShell

**Uwaga**: region hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.

Po pomyślnym uruchomieniu skryptu hello można podjąć następujące kroki po skryptu hello:

1. Konfigurowanie reguł zapory hello, to jest objęte hello sekcji poniżej: opis reguły zapory.
2. Opcjonalnie w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.

Po pomyślnym uruchomieniu skryptu hello hello reguły zapory, należy ukończyć toobe, ten temat znajdują się w sekcji hello: reguł zapory.

## <a name="user-defined-routing-udr"></a>Zdefiniowane przez użytkownika routingu (przez)
Domyślnie program hello następujące trasy systemowe są zdefiniowane jako:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Witaj VNETLocal jest zawsze prefiksy adresów hello zdefiniowane z hello sieci wirtualnej dla tej sieci określonych (ie go ulegnie zmianie z tooVNet sieci wirtualnej, w zależności od tego, jak zdefiniowano każdej określonej sieci wirtualnej). trasy systemowe pozostałych Hello są statyczne i domyślne jako powyżej.

Podobnie jak w przypadku priorytet trasy są przetwarzane przy użyciu metody najdłuższym prefiksu dopasowania (LPM) Wybierane hello, w związku z tym hello specyficzny trasy w tabeli hello powinna zostać zastosowana tooa podany adres docelowy.

W związku z tym ruchu (na przykład serwer toohello DNS01, 10.0.2.4) przeznaczone na powitania w sieci lokalnej (10.0.0.0/16) zostanie przekierowane na docelowym tooits sieci wirtualnej hello powodu toohello 10.0.0.0/16 trasy. Innymi słowy 10.0.2.4, trasy 10.0.0.0/16 hello jest najbardziej określoną trasę hello, mimo że hello 10.0.0.0/8 i 0.0.0.0/0 również można zastosować, ale ponieważ są one szerszym nie wpływają one na ten ruch. W związku z tym too10.0.2.4 ruchu hello musi następnego przeskoku hello lokalnej sieci wirtualnej i po prostu trasy toohello docelowego.

Jeśli ruch jest przeznaczona do 10.1.1.1, na przykład, hello 10.0.0.0/16 trasy nie zastosować, ale hello 10.0.0.0/8 byłoby hello specyficzny i będzie ruch hello pomijane ("czarna holed"), ponieważ hello następnego przeskoku jest Null. 

Jeśli hello docelowy nie miał zastosowania tooany prefiksy Null hello lub hello VNETLocal prefiksy, a następnie należy wykonać hello najmniej określonej trasy, 0.0.0.0/0 oraz być kierowane toohello Internet jako hello następnego przeskoku i w związku z tym limit krawędzi internet platformy Azure.

Jeśli istnieją dwie identyczne prefiksów w tabeli tras hello, hello Oto hello według priorytetu na podstawie atrybutu "source" tras hello:

1. "VirtualAppliance" = tabeli dodane ręcznie toohello trasy zdefiniowane przez użytkownika
2. "Właściwość VPNGateway" = dynamiczny trasy protokołu BGP (gdy jest używany z sieci hybrydowe), dodane przez protokół dynamicznej sieci, te trasy może ulec zmianie jako protokół dynamicznej hello automatycznie uwzględnia zmiany w połączyć za pomocą sieci
3. "Default" = hello tras systemowych, hello lokalnej sieci wirtualnej i hello statyczne, jak pokazano w powyższej tabeli tras hello.

> [!NOTE]
> Użytkownika zdefiniowane routingu przez mogą teraz używać z bramy sieci VPN i ExpressRoute tooforce wychodzący i przychodzący między lokalizacjami ruchu toobe routingiem tooa sieci urządzenie wirtualne (NVA).
> 
> 

#### <a name="creating-hello-local-routes"></a>Tworzenie hello tras lokalnych
W tym przykładzie są potrzebne dwie tabele routingu, jeden dla każdej podsieci hello frontonu i wewnętrznej bazy danych. Każda tabela tras statycznych, które są odpowiednie dla podanej podsieci hello jest załadowana. W celu hello w tym przykładzie każda tabela zawiera trzy tras:

1. Ruchu w podsieci lokalnej z następnego przeskoku zdefiniowane tooallow podsieci lokalnej ruchu toobypass hello zapory
2. Ruchu w sieci wirtualnej z przeskoku dalej zdefiniowany jako zapory, przesłania hello domyślna reguła, która umożliwia bezpośrednio lokalnego tooroute ruchu w sieci wirtualnej
3. Wszystkie pozostałe ruchu (0/0) z następnego przeskoku zdefiniowany jako hello zapory

Po utworzeniu tabele routingu hello są one powiązane tootheir podsieci. Na frontonie hello podsieci tabeli routingu po utworzeniu i powiązane podsieci toohello powinien wyglądać następująco:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


W tym przykładzie polecenia tabeli tras hello toobuild używane są następujące hello Dodaj trasy zdefiniowane przez użytkownika, a następnie powiązać podsieci tooa tabeli tras hello (Uwaga; wszystkie elementy poniżej rozpoczynający się od znaku dolara (np.: $BESubnet) są zmiennych zdefiniowanych przez użytkownika ze skryptu hello w Witaj odwołanie sekcji tego dokumentu):

1. Można utworzyć pierwszy hello podstawowej tabeli routingu. Ta Wstawka kodu pokazano tworzenie hello tabeli hello hello podsieci wewnętrznej bazy danych. W skrypcie hello tworzona jest również odpowiedniego tabeli hello podsieci frontonu.
   
     Nowe AzureRouteTable-Name $BERouteTableName "
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Po utworzeniu tabeli tras hello można dodać trasy zdefiniowane przez określonego użytkownika. W tym przedstawiono cały ruch (0.0.0.0/0), zostaną przesłane za pośrednictwem hello urządzenie wirtualne (używane toopass hello adres IP przypisany, gdy urządzenie wirtualne hello został utworzony we wcześniejszej części skryptu hello jest zmienną $VMIP [0]). W skrypcie hello tworzona jest również odpowiednią regułę hello tabeli frontonu.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Witaj powyżej wejście dla trasy spowoduje zastąpienie hello domyślną trasę "0.0.0.0/0", ale reguła 10.0.0.0/16 domyślnej hello nadal istniejące, które umożliwiałyby ruch w ramach tooroute sieci wirtualnej hello bezpośrednio toohello docelowego i toohello urządzenie wirtualne sieci. toocorrect, należy dodać tę regułę wykonaj hello zachowanie.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. W tym momencie jest toobe wyborów dokonanych. Z hello powyżej na dwa sposoby cały ruch będzie przekierowywać toohello zapory w celu oceny, nawet ruch w ramach pojedynczej podsieci. Może to konieczne, jednak tooallow ruchu w podsieci tooroute lokalnie bez udziału hello zapory, trzeci, bardzo określonej reguły mogą zostać dodane. Ta trasa stanów, które dowolnego adresu destine dla podsieci lokalne powitania można po prostu kierować bezpośrednio (Typ następnego przeskoku = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Na koniec z tabeli routingu hello tworzone i wypełniane przy użyciu trasy zdefiniowane przez użytkownika, tabela hello teraz musi być powiązane tooa podsieci. W skrypcie hello tabeli tras frontonu hello jest także powiązane toohello podsieci frontonu. W tym miejscu to skrypt powiązanie hello hello podsieci wewnętrznej.
   
     Zestaw AzureSubnetRouteTable - VirtualNetworkName $VNetName "
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>Przesyłanie dalej IP
TooUDR funkcji Pomocnik jest przekazywanie adresów IP. To jest ustawienie na urządzenie wirtualne, umożliwiającą ruch tooreceive nie specjalnie kierowane toohello urządzenia i następnie przesyła ten ruch tooits ostatecznym miejscem przeznaczenia.

Na przykład jeśli ruch z AppVM01 sprawia, że serwer DNS01 toohello żądania przez może kierować Zapora toohello. Z przesyłania dalej protokołu IP włączone hello ruchu dla miejsca docelowego DNS01 hello (10.0.2.4) zostanie zaakceptowane przez urządzenia hello (10.0.0.4) i przesyłane dalej ostatecznym miejscem przeznaczenia tooits (10.0.2.4). Bez przesyłania dalej protokołu IP włączone na powitania zapory ruch może nie zostać zaakceptowane przez hello urządzenia nawet hello tabeli tras ma zapory hello jako hello następnego przeskoku. 

> [!IMPORTANT]
> Jest krytyczne tooremember tooenable przesyłania dalej protokołu IP w połączeniu z routingiem zdefiniowane użytkownika.
> 
> 

Konfigurowanie przekazywania adresów IP jest jednego polecenia i może odbywać się w czasie tworzenia maszyny Wirtualnej. Dla hello przepływu fragment kodu hello ten przykład jest końcowej hello hello skryptu i zgrupowana za pomocą polecenia przez hello:

1. Wywołania hello wystąpienia maszyny Wirtualnej, które jest urządzenia wirtualnego, w takim przypadku hello zapory i włączenia funkcji przesyłania dalej IP (Uwaga; dowolny element w czerwonym rozpoczynający się od znaku dolara (np.: $VMName[0]) jest zmienną zdefiniowanych przez użytkownika ze skryptu hello hello odwołanie sekcji tego dokumentu. Witaj zero w nawiasach [0], reprezentuje hello pierwsza maszyna wirtualna w tablicy hello maszyn wirtualnych, dla hello przykładowy skrypt toowork bez żadnych modyfikacji, powitalne pierwsza maszyna wirtualna (VM 0) musi być hello zapory):
   
     Get-AzureVM-Name $VMName [0] - ServiceName $ServiceName [0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Sieciowe grupy zabezpieczeń (NSG)
W tym przykładzie grupa NSG jest wbudowana i następnie ładowane przy użyciu jednej reguły. Ta grupa jest następnie powiązany tylko toohello frontonu i zaplecza podsieci (nie hello SecNet). Deklaratywnie budowanego hello następujące reguły:

1. Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (wszystkie podsieci)

Mimo że grupy NSG są używane w tym przykładzie, jego głównym celem jest jako dodatkowej warstwy obrony przed ręcznej konfiguracji. Chcemy tooblock wszystkie przychodzący ruch z hello internet tooeither hello frontonu, lub podsieci wewnętrznej bazy danych, ruch powinny przepływać tylko za pośrednictwem zapory toohello podsieci SecNet hello (i następnie jeśli odpowiednią na toohello frontonu lub wewnętrznej bazy danych podsieci). Plus przy użyciu reguł przez hello w miejscu, dowolnego ruchu, który przekształcić go hello podsieci frontonu lub wewnętrznej bazy danych spowoduje przekierowanie limit toohello zapory (Dziękujemy tooUDR). Zapora Hello będzie traktować jako asymetrycznego przepływu i spowoduje pominięcie hello ruchu wychodzącego. W związku z tym istnieją trzy warstwy zabezpieczeń Ochrona powitalnych frontonu i wewnętrznej bazy danych podsieci; 1) nie Otwórz punkty końcowe na powitania FrontEnd001 i usługi w chmurze BackEnd001, 2) grupy NSG zezwalających na ruch z Internetu, 3) hello Zapora porzucenie asymetrycznego ruchu hello.

Jeden punkt interesujące dotyczące hello sieciowej grupy zabezpieczeń w tym przykładzie jest, że zawiera on tylko jedną regułę, pokazano poniżej, czyli toodeny internet ruchu toohello całej sieci wirtualnej, która obejmuje hello zabezpieczeń podsieci. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

Jednak ponieważ hello grupa NSG jest tylko powiązana toohello frontonu i wewnętrznej bazy danych podsieci, reguła hello nie jest przetwarzana ruchu przychodzącego toohello zabezpieczeń podsieci. W związku z tym mimo że reguły NSG hello jest wyświetlany komunikat nie adres internetowy ruch tooany na powitania sieci wirtualnej, ponieważ powitalne NSG nigdy nie został powiązany podsieci zabezpieczeń toohello ruch będzie przepływać toohello zabezpieczeń podsieci.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Reguły zapory
W zaporze hello przekazywania zasady należy toobe utworzony. Ponieważ Zapora hello jest blokowanie lub funkcji przekazywania wszystkich przychodzące, wychodzące, sieć wirtualną wewnątrz ruchu wiele reguł zapory są wymagane. Ponadto cały ruch przychodzący nastąpi trafienie hello usługi zabezpieczeń publicznego adresu IP (różne porty), toobe przetworzony przez zaporę Windows hello. Najlepszym rozwiązaniem jest toodiagram hello logicznej przepływów przed rozpoczęciem konfigurowania później hello podsieci i przeróbek tooavoid reguł zapory. Witaj poniższej ilustracji jest widok logiczny hello reguły zapory w tym przykładzie:

![Widok logiczny hello reguły zapory][2]

> [!NOTE]
> Oparte na powitania używanych przez urządzenie wirtualne sieci, porty zarządzania hello będą się różnić. W tym przykładzie, który odwołuje się do zapory NextGen Barracuda, który używa portów 22, 801 i 807. Przejrzyj hello urządzenia dostawcy dokumentacji toofind hello porty używane do zarządzania hello urządzenie używane.
> 
> 

### <a name="logical-rule-description"></a>Opis reguły logiczne
W hello logicznej powyższym diagramie hello zabezpieczeń podsieci nie jest wyświetlane, ponieważ zapory hello hello tylko zasobów tej podsieci, a ten diagram jest wyświetlany hello reguły zapory i sposób ich logicznie akceptować lub odrzucać przepływów ruchu sieciowego i nie hello routingiem ścieżkę. Ponadto zewnętrzne porty hello wybrany na potrzeby hello na ruch RDP są wyższe ranged portów (8014 — 8026) i zostały wybrane toosomewhat są wyrównane z hello ostatni dwa oktety hello lokalny adres IP dla czytelności łatwiejsze (np. adres serwera lokalnego 10.0.1.4 jest skojarzony z portu zewnętrznego 8014), jednak można użyć żadnych wyższej niekolidujących portów.

Na przykład potrzebujemy 7 typów reguł, te typy reguł są opisane w następujący sposób:

* Reguły zewnętrzne (dla ruchu przychodzącego):
  1. Zarządzanie reguła: Ta zasada przekierowania aplikacji umożliwia ruch toopass toohello zarządzania porty urządzenie wirtualne hello sieci.
  2. Zasady protokołu RDP (na każdym serwerze z systemem windows): następujące cztery reguły (po jednym dla każdego serwera) umożliwi Zarządzanie hello poszczególnych serwerów za pomocą protokołu RDP. Może to być również połączone w jedną regułę w zależności od możliwości hello hello urządzenie wirtualne sieci używane.
  3. Reguły ruchu aplikacji: Istnieją dwie reguły ruchu aplikacji hello najpierw dla ruchu w sieci web frontonu hello i hello drugi transmisji hello zaplecza (np warstwa sieci web serwera toodata). Konfiguracja Hello tych zasad będzie zależeć od architektury sieci hello (w którym są umieszczane serwerów) oraz ruch (które ruchu hello kierunek przepływu i które porty są używane).
     * Pierwsza reguła Hello umożliwi serwera aplikacji hello tooreach ruch rzeczywisty aplikacji hello. Hello inne zasady Zezwalaj na zabezpieczenia, zarządzanie, itp., reguły aplikacji są co Zezwalaj zewnętrznych tooaccess użytkowników lub usług aplikacji hello. Na przykład jest jednym serwerze sieci web na porcie 80, w związku z tym regułę zapory jednej aplikacji przekieruje ruch przychodzący toohello IP zewnętrznego, toohello serwerów wewnętrzny adres IP sieci web. Witaj przekierowanie ruchu sesji ma NAT może być toohello wewnętrznego serwera.
     * Hello jest drugą regułę ruchu aplikacji hello wewnętrzna reguła tooallow powitania serwera sieci Web tootalk toohello AppVM01 serwera (ale nie AppVM02) za pomocą dowolnego portu.
* Wewnętrzne zasady (dla ruchu w sieci wirtualnej wewnątrz)
  1. TooInternet wychodzących reguł: Ta reguła będzie zezwalać na ruch z dowolnej sieci toopass toohello wybrane sieci. Ta reguła jest zwykle domyślna reguła już na powitania zapory, ale w stanie wyłączenia. Ta reguła powinna być włączona w tym przykładzie.
  2. Reguła DNS: Ta zasada umożliwia tylko DNS (port 53) ruchu toopass toohello serwera DNS. Dla tego środowiska, większość ruchu z toohello frontonu hello wewnętrznej bazy danych jest zablokowany ta zasada umożliwia DNS w szczególności z żadnych podsieci lokalnej.
  3. Podsieci tooSubnet reguły: Ta reguła jest tooallow dowolnego serwera na powitania wstecz kończyć podsieci tooconnect tooany serwera na powitania podsieci frontonu (ale nie hello odwrotnej).
* Reguła awaryjnego (dla ruchu, który nie spełnia żadnego z hello powyżej):
  1. Odmów wszystkie reguły ruchu: To zawsze powinna być hello reguły końcowego (w zakresie priorytet), a jako takie Jeśli przepływa ruch nie toomatch żadnego hello poprzedzających reguł, które zostaną usunięte przez tę regułę. Jest to domyślna reguła i zwykle jest aktywna, żadnych modyfikacji nie są zwykle wymagane.

> [!TIP]
> Na powitania drugą regułę ruchu aplikacji każdy port jest dozwolony dla łatwy w tym przykładzie, hello rzeczywistym scenariuszu najbardziej określonych zakresów port i adres powinien być używany tooreduce hello ataku tej reguły.
> 
> 

<br />

> [!IMPORTANT]
> Po utworzeniu wszystkich hello powyżej reguły, ważne jest tooreview hello priorytetu ruchu tooensure każdej reguły, które ma być dozwolony lub zabroniony zgodnie z potrzebami. W tym przykładzie są reguły hello w kolejności priorytetu. Jest łatwy toobe zablokowane zapory hello powodu uporządkowane toomis reguły. Co najmniej upewnij się, że hello zarządzania samą zaporę hello jest zawsze hello bezwzględną najwyższy priorytet reguły.
> 
> 

### <a name="rule-prerequisites"></a>Reguły wymagań wstępnych
Jeden wymagań wstępnych dla zapory hello uruchomionej maszyny wirtualnej hello są publiczne punkty końcowe. Dla ruchu tooprocess zapory hello hello odpowiednie publiczne punkty końcowe musi być otwarty. Istnieją trzy typy ruchu w tym przykładzie; 1) zarządzania ruchu toocontrol hello zapory i reguły zapory, serwerów windows hello toocontrol ruch RDP 2) i ruchu 3) aplikacji. Są trzy kolumny hello typów ruchu w górnym hello połowy widok logiczny reguł zapory hello powyżej.

> [!IMPORTANT]
> W tym miejscu klucza takeway jest tooremember który **wszystkie** ruchu rozpocznie się przez zaporę Windows hello. Tak pulpitu tooremote toohello IIS01 serwera, nawet jeśli komputer jest w hello Front End chmury usługi i podsieci frontonu hello, tooaccess tego serwera, potrzebne będą tooRDP toohello zapory na porcie 8014, a następnie wewnętrznie Pozwól hello zapory tooroute hello RDP żądania toohello IIS01 portem RDP. Witaj portalu Azure "Połącz" przycisku nie będzie działać, ponieważ nie istnieje żadne bezpośrednie tooIIS01 ścieżkę protokołu RDP (o ile hello portalu można zobaczyć). Oznacza to, że wszystkie połączenia z hello internet będzie toohello usługi zabezpieczeń i Port, np. secscv001.cloudapp.net:xxxx (odwołanie hello powyżej diagram mapowania hello portu zewnętrznego i wewnętrznym adresem IP i Port).
> 
> 

Punkt końcowy można otworzyć w momencie hello tworzenia maszyny Wirtualnej lub po kompilacji jest przeprowadzane w hello przykładowy skrypt i przedstawionym poniżej na następujący fragment kodu (Uwaga; dowolnego elementu, począwszy od znak dolara (np.: $VMName[$i]) jest zmienną zdefiniowanych przez użytkownika ze skryptu hello w hello referen CE sekcji tego dokumentu. Witaj "$i" w nawiasach [$i] reprezentuje hello tablicy liczbę określonej maszyny Wirtualnej w tablicy maszyn wirtualnych):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Mimo że nie wyraźnie przedstawiony tutaj powodu toohello użycie zmiennych, ale punkty końcowe są **tylko** otwarte na powitania zabezpieczeń usługi w chmurze. Jest to tooensure obsługi cały ruch przychodzący (kierowane, translatora adresów Sieciowych porzucone) przez zaporę Windows hello.

Klienta zarządzania należy toobe zainstalowany w zaporze hello toomanage komputera, a następnie utwórz wymagane konfiguracje hello. Zobacz hello dostawcy dokumentacji zapory (lub inne NVA) w sposób toomanage hello urządzenia. Hello pozostałej części tej sekcji i hello następnej sekcji, tworzenie reguł zapory, opisano konfigurację hello hello zapory, za pośrednictwem powitania klienta zarządzania dostawców (tj. hello portalu Azure lub programu PowerShell).

Instrukcje dotyczące pobierania klienta i łączenia toohello Barracuda używana w tym przykładzie można znaleźć tutaj: [Barracuda NG administratora](https://techlib.barracuda.com/NG61/NGAdmin)

Po zalogowaniu się na powitania zapory, ale przed utworzeniem reguły zapory, istnieją dwie klasy obiektu wymagań wstępnych, które ułatwia tworzenie reguł hello; Obiekty sieci i usługi.

W tym przykładzie trzy obiekty nazwanej sieci powinien być zdefiniowany (jeden dla podsieci Frontend hello i hello podsieci wewnętrznej bazy danych, również obiekt sieci hello adres IP serwera DNS hello). toocreate nazwanej sieci; począwszy od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello, w hello sekcji konfiguracji operacyjnych kliknij zestaw reguł, kliknij przycisk "Sieci" w menu obiekty zapory hello, a następnie kliknij przycisk Nowa, w menu Edycja sieci hello. Hello sieci można teraz można utworzyć obiektu, dodając nazwy hello i prefiksu hello:

![Utwórz obiekt sieci frontonu][3]

Spowoduje to utworzenie nazwanej sieci dla podsieci FrontEnd hello, należy utworzyć obiekt podobny hello również podsieci wewnętrznej bazy danych. Teraz hello podsieci można łatwiej odwoływać się do nazwy w regułach zapory hello.

Dla hello obiektu serwera DNS:

![Utwórz obiekt serwera DNS][4]

Ten jedno odwołanie adres IP zostanie wykorzystana w regule DNS w dalszej części dokumentu hello.

drugi obiekty wymagań wstępnych Hello są obiektami usługi. Te będą stanowiły hello portów połączeń protokołu RDP dla każdego serwera. Ponieważ hello istniejący obiekt usługi protokołu RDP jest powiązane toohello domyślnym portem RDP, 3389, nowych usług mogą być tworzone tooallow ruchu z portów zewnętrznych hello (8014 8026). Hello nowych portów można również dodać toohello istniejącej usługi protokołu RDP, ale w celu ułatwienia demonstracyjnych, można utworzyć regułę dla każdego serwera. toocreate nowej reguły protokołu RDP dla serwera; począwszy od hello Barracuda NG administratora klient pulpitu nawigacyjnego, przejdź na kartę Konfiguracja toohello, w hello konfigurację operacyjną kliknij zestaw reguł, sekcji, a następnie kliknij przycisk "Usługi" w obszarze hello menu obiekty zapory, przewiń w dół listę hello usług i wybierz hello Usługa "RDP". Kliknij prawym przyciskiem myszy i wybierz Kopiuj, a następnie kliknij prawym przyciskiem myszy i wybierz Wklej. Teraz jest obiektem usługi RDP Copy1, które mogą być edytowane. Kliknij prawym przyciskiem myszy RDP Copy1 i wybrać edycji, hello Edytuj obiekt usługi oknie wyskakującym zostanie w sposób pokazany poniżej:

![Kopiowanie reguły domyślnej protokołu RDP][5]

wartości Hello następnie może być edytowany toorepresent hello usługi protokołu RDP dla określonego serwera. W przypadku hello AppVM01 powyżej domyślnej reguły protokołu RDP powinien być zmodyfikowane tooreflect nową nazwę usługi, opis, i portu zewnętrznego RDP używane w hello diagram rysunek 8 (Uwaga: hello portów nie zostaną zmienione hello RDP domyślną 3389 portu zewnętrznego toohello używany dla tego określonego serwera w przypadku hello portu zewnętrznego AppVM01 hello jest 8025) hello zmodyfikowane usługi przedstawiono poniżej:

![Reguła AppVM01][6]

Ten proces musi być powtarzane toocreate usługi protokołu RDP dla hello pozostałych serwerów; AppVM02 DNS01 i IIS01. Tworzenie Hello tych usług będzie tworzenia reguły hello prostszy i bardziej oczywistymi w następnej sekcji hello.

> [!NOTE]
> Usługa protokołu RDP dla hello zapory nie jest wymagana dwóch powodów; 1) pierwsze zapory hello maszyny Wirtualnej jest obrazem opartymi na systemie Linux SSH będzie używany port 22 dla maszyny Wirtualnej zarządzania zamiast protokołu RDP, a port 22 2) i dwa porty zarządzania są dozwolone w hello pierwszej reguły zarządzania opisane poniżej tooallow zarządzania łączności.
> 
> 

### <a name="firewall-rules-creation"></a>Tworzenie reguły zapory
Istnieją trzy typy reguł zapory, w tym przykładzie, wszystkie mają różne ikony:

Reguła przekierowania aplikacji Hello: ![przekierowania ikona aplikacji][7]

Reguła NAT docelowego Hello: ![docelowym translacji adresów Sieciowych ikony][8]

Reguła przebiegu Hello: ![Przekaż ikonę][9]

Więcej informacji na temat tych zasad można znaleźć w witrynie sieci web Barracuda hello.

toocreate hello następujące zasady (lub sprawdź istniejących reguł domyślnych), zaczynając od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello w hello konfigurację operacyjną sekcji kliknij pozycję zestaw reguł. Wywołuje siatkę, "Main reguły" wyświetli hello istniejących reguł active i zdezaktywowane tej zapory. W hello prawego górnego rogu tej siatki jest mały, zielony "+", kliknij ten toocreate nową regułę (Uwaga: Zapora może być "zablokowana" zmian, jeśli przycisk oznaczony jako "Lock" i są toocreate lub Edytuj reguły, kliknij ten przycisk, zbyt "Odblokuj" hello se reguły t i Zezwól na edytowanie). Jeśli chcesz, aby tooedit istniejącą regułę, wybierz tej reguły, kliknij prawym przyciskiem myszy i wybierz edytowanie reguły.

Gdy reguły są tworzone i/lub zmodyfikowane, musi być przypisany toohello zapory, a następnie aktywowany, jeśli nie zostanie to zrobione reguły hello zmiany nie zostaną wprowadzone. opisano sposób wypychania i aktywacji Hello poniżej hello szczegóły reguły opisy.

Szczegóły Hello każdej reguły wymagane toocomplete w tym przykładzie są opisane w następujący sposób:

* **Zarządzanie reguły zapory**: ten przekierowania aplikacji reguła zezwala na ruch portów zarządzania toohello toopass hello sieci urządzenie wirtualne, w tym przykładzie zapory NextGen Barracuda. porty zarządzania Hello są 801, 807 i opcjonalnie 22. Witaj zewnętrznych i wewnętrznych portów są hello takie same (tzn. bez translacji port). Reguły i ustawienia dostępu do danych, reguła domyślna i domyślnie włączona (w wersji zapory NextGen Barracuda 6.1).
  
    ![Reguły zapory zarządzania][10]

> [!TIP]
> Hello przestrzeni adresowej źródła w tej regule jest dowolne, jeśli hello zakresów adresów IP zarządzania są znane, zmniejszając ten zakres będzie również zmniejszyć porty zarządzania powierzchni toohello atak powitania.
> 
> 

* **Zasady protokołu RDP**: reguł NAT przeznaczenia tych umożliwi Zarządzanie hello poszczególnych serwerów za pomocą protokołu RDP.
  Istnieją cztery toocreate wymagane pola krytyczne tej reguły:
  
  1. Źródło — tooallow protokołu RDP z dowolnego miejsca, odwołanie hello "Dowolne" jest używany w polu źródła hello.
  2. Usługi — używają powitalne odpowiedniego obiektu usługi utworzony wcześniej, w tym przypadku "AppVM01 RDP", zewnętrzne porty hello przekierowania toohello serwerów lokalny adres IP i tooport 3386 (hello domyślny port protokołu RDP). Ta reguła określonych ma tooAppVM01 dostępu RDP.
  3. Miejsce docelowe — powinno być hello *portów lokalnych na zaporze hello*, "DCHP 1 lokalny adres IP" lub eth0 używania statycznych adresów IP. numer porządkowy Hello (eth0, eth1 itp.) może się różnić, jeśli urządzenia sieciowe ma wiele interfejsów lokalnych. Jest to hello port zapory hello wysyła z (może to być hello takie same jak hello odbieranie portu), pole listy docelowej hello jest hello rzeczywistego przeznaczenia routingiem.
  4. Przekierowanie — w tej sekcji opisano urządzenie wirtualne hello gdzie tooultimately przekierować ruch. Najprostsza przekierowania Hello jest tooplace hello IP i Port (opcjonalnie) w polu listy docelowej hello. Jeśli nie jest używane hello port docelowy na żądanie przychodzące hello będzie używany (ie nie tłumaczenie), jeśli port jest wybrany hello port będzie również NAT oraz hello IP zajmie się.
     
     ![Reguły zapory protokołu RDP][11]
     
     Łącznie cztery reguły protokołu RDP, należy utworzyć toobe: 
     
     | Nazwa reguły | Serwer | Usługa | Listy docelowej |
     | --- | --- | --- | --- |
     | RDP-IIS01 |IIS01 |IIS01 PROTOKOŁU RDP |10.0.1.4:3389 |
     | RDP-DNS01 |DNS01 |DNS01 PROTOKOŁU RDP |10.0.2.4:3389 |
     | RDP-AppVM01 |AppVM01 |AppVM01 protokołu RDP |10.0.2.5:3389 |
     | RDP-AppVM02 |AppVM02 |AppVm02 protokołu RDP |10.0.2.6:3389 |

> [!TIP]
> Zawęzić zakres hello hello źródła i pola usługi zmniejsza możliwości ataku hello. zakres Hello najbardziej ograniczone, który umożliwi funkcji powinny być używane.
> 
> 

* **Reguły ruchu aplikacji**: istnieją dwie reguły ruchu aplikacji hello najpierw dla ruchu w sieci web frontonu hello i hello drugi transmisji hello zaplecza (np warstwa sieci web serwera toodata). Te reguły będzie zależeć od architektury sieci hello (w którym są umieszczane serwerów) oraz ruch (które ruchu hello kierunek przepływu i które porty są używane).
  
    Najpierw omówiona jest hello frontonu reguły dla ruchu w sieci web:
  
    ![Reguła zapory w sieci Web][12]
  
    Ta reguła NAT docelowym zezwala serwerowi aplikacji hello tooreach hello rzeczywistej aplikacji ruchu. Hello inne zasady Zezwalaj na zabezpieczenia, zarządzanie, itp., reguły aplikacji są co Zezwalaj zewnętrznych tooaccess użytkowników lub usług aplikacji hello. Na przykład jest jednym serwerze sieci web na porcie 80, w związku z tym hello pojedynczą aplikacji regułę zapory przekieruje ruch przychodzący toohello IP zewnętrznego, toohello serwerów wewnętrzny adres IP sieci web.
  
    **Uwaga**: czy istnieje nie portu przypisane w polu listy docelowej hello, w związku z tym hello przychodzący port 80 (lub 443 dla wybranej usługi hello) będzie używany w przekierowania hello powitania serwera sieci web. Jeśli serwer sieci web hello nasłuchuje na innym porcie, na przykład portu 8080, pole listy docelowej hello może być tooallow too10.0.1.4:8080 Zaktualizowano również przekierowania portu hello.
  
    Hello jest dalej reguły ruchu aplikacji hello wewnętrzna reguła tooallow powitania serwera sieci Web tootalk toohello AppVM01 serwera (ale nie AppVM02) za pośrednictwem usługi:
  
    ![Reguły zapory AppVM01][13]
  
    Ta zasada przebiegu umożliwia dowolnego serwera IIS na powitania serwera sieci Web podsieci tooreach hello AppVM01 (adres IP 10.0.2.5) na dowolnym porcie przy użyciu protokołu danych tooaccess wymagane przez aplikację sieci web hello.
  
    W tym zrzucie ekranu "\<jawne dest\>" jest używany w toosignify pola docelowego hello 10.0.2.5 jako miejsce docelowe hello. Może to być albo jawne pokazany lub a o nazwie obiektu Network (jak to zostało zrobione wymagań wstępnych hello powitania serwera DNS). Jest to się administrator toohello zapory hello zostanie użyta metoda toowhich. Kliknij dwukrotnie hello pierwszy pusty wiersz pod tooadd 10.0.2.5 jako Explict Desitnation \<jawne dest\> , a następnie wprowadź adres hello w oknie wyskakującym hello.
  
    Z tą regułą przekazać odłączenia translatora adresów Sieciowych jest niezbędne, ponieważ jest to wewnętrzny ruchu, hello metodę połączenia można ustawić za "Nie SNAT".
  
    **Uwaga**: hello sieć źródłową w tej regule jest dowolnego zasobu w podsieci frontonu hello, jeśli będą istnieć tylko jedna lub znanych określoną liczbę serwerów sieci web, obiekt sieci, zasoby mogą być tworzone toobe dokładniej toothose dokładne adresów IP zamiast Witaj całej podsieci frontonu.

> [!TIP]
> Ta zasada używa usługi hello toomake "Wszystkie" hello toosetup łatwiejsze przykładowej aplikacji i użyć, to będzie również umożliwiać ICMPv4 (ping) w jednej reguły. Jednak to nie jest zalecanym rozwiązaniem. Witaj portów i protokołów ("usługi") powinna być zwężającym toohello minimalne możliwe, że umożliwia aplikacji operacji tooreduce hello ataku tej granicy.
> 
> 

<br />

> [!TIP]
> Mimo że ta zasada zawiera odwołania do jawnego dest używany, spójnego podejścia powinny być używane w konfiguracji zapory hello. Zaleca się, że hello o nazwie obiektu sieci używanego w łatwiejsze czytelności i obsługi. jawne dest Hello jest używany tutaj tooshow tylko alternatywnych reference — metoda i zwykle nie jest zalecane (szczególnie w przypadku złożonych konfiguracji).
> 
> 

* **TooInternet wychodzące reguły**: przekazać ta reguła będzie zezwalać na ruch z dowolnego źródła sieci toopass toohello wybrane miejsce docelowe sieci. Ta reguła jest domyślna reguła zwykle już hello Barracuda NextGen zapory, ale jest w stanie wyłączenia. Kliknięcie prawym przyciskiem myszy tę regułę można uzyskać dostęp hello uaktywnić reguły polecenia. Reguła Hello pokazane został zmodyfikowany tooadd hello dwie podsieci lokalne utworzonych jako odwołania w sekcji wymagań wstępnych hello tego dokumentu toohello źródła atrybutu tej reguły.
  
    ![Reguła ruchu wychodzącego][14]
* **Reguła DNS**: przekazać ta reguła zezwala tylko DNS (port 53) ruchu toopass toohello serwera DNS. Dla tego środowiska, większość ruchu z toohello frontonu hello wewnętrznej bazy danych jest zablokowany ta zasada umożliwia w szczególności DNS.
  
    ![Reguły zapory DNS][15]
  
    **Uwaga**: na tym ekranie jest dołączony zrzut hello metodę połączenia. Ponieważ ta reguła dotyczy ruchu adres IP wewnętrznego adresu IP toointernal, NATing nie jest wymagane, to hello metodę połączenia jest ustawiany za "Nie SNAT" dla tej reguły przebiegu.
* **Podsieci tooSubnet reguły**: przekazania tej reguły jest domyślna reguła, która została uaktywniona i modyfikacji tooallow dowolnego serwera na powitania wstecz kończyć podsieci tooconnect tooany serwera na hello podsieci frontonu. Ta reguła jest ruchu wszystkie wewnętrznej, hello metodę połączenia można ustawić tooNo SNAT.
  
    ![Reguła sieci wirtualnej wewnątrz zapory][16]
  
    **Uwaga**: hello dwukierunkowe wyboru nie jest zaznaczone (ani nie jest zaznaczone w większości reguł), to ma znaczenie dla tej reguły, ponieważ ułatwia to reguły "w jedną stronę", można zainicjować połączenia z toohello sieć frontonu hello wewnętrzna podsieć, jednak nie hello odwrotnie. Jeśli pole wyboru zostało zaznaczone, ta zasada umożliwiłyby ruch dwukierunkowy, który z naszych diagram logiczny nie jest wymagana.
* **Odmów wszystkie reguły ruchu**: to zawsze powinna być hello reguły końcowego (w zakresie priorytet), i w związku Jeśli przepływa ruch toomatch kończy się niepowodzeniem żadnego hello poprzedzających reguły go zostanie usunięte przez tę regułę. Jest to domyślna reguła i zwykle jest aktywna, żadnych modyfikacji nie są zwykle wymagane. 
  
    ![Zapora regułę Odmów][17]

> [!IMPORTANT]
> Po utworzeniu wszystkich hello powyżej reguły, ważne jest tooreview hello priorytetu ruchu tooensure każdej reguły, które ma być dozwolony lub zabroniony zgodnie z potrzebami. W tym przykładzie hello reguły są w kolejności hello powinien pojawią się one w hello siatki Main przesyłania reguły w powitania klienta zarządzania Barracuda.
> 
> 

## <a name="rule-activation"></a>Reguły aktywacji
Specyfikacja toohello ruleset zmodyfikowane hello diagramu logiki hello, hello ruleset musi być przekazany toohello zapory, a następnie aktywowany.

![Aktywacja reguły zapory][18]

W prawym górnym narożniku hello powitania klienta zarządzania są klastra przycisków. Kliknij przycisk hello "Wyślij zmiany" przycisk toosend hello zmodyfikowane zasady toohello zapory, a następnie kliknij przycisk "Uaktywnij" hello.

Z aktywacji hello zestaw reguł zapory hello tej kompilacji w środowisku przykładzie zostanie zakończona.

## <a name="traffic-scenarios"></a>Scenariusze ruchu
> [!IMPORTANT]
> Takeway klucza jest tooremember który **wszystkie** ruchu rozpocznie się przez zaporę Windows hello. Tak pulpitu tooremote toohello IIS01 serwera, nawet jeśli komputer jest w hello Front End chmury usługi i podsieci frontonu hello, tooaccess tego serwera, potrzebne będą tooRDP toohello zapory na porcie 8014, a następnie wewnętrznie Pozwól hello zapory tooroute hello RDP żądania toohello IIS01 portem RDP. Witaj portalu Azure "Połącz" przycisku nie będzie działać, ponieważ nie istnieje żadne bezpośrednie tooIIS01 ścieżkę protokołu RDP (o ile hello portalu można zobaczyć). Oznacza to, że wszystkie połączenia z hello internet będzie toohello usługi zabezpieczeń i Port, np. secscv001.cloudapp.net:xxxx.
> 
> 

W tych sytuacjach hello następujące reguły zapory powinny być stosowane:

1. Zarządzanie zaporą
2. TooIIS01 protokołu RDP
3. TooDNS01 protokołu RDP
4. TooAppVM01 protokołu RDP
5. TooAppVM02 protokołu RDP
6. Toohello ruchu aplikacji sieci Web
7. TooAppVM01 ruchu aplikacji
8. Wychodzące toohello Internet
9. TooDNS01 frontonu
10. Wewnątrz podsieci ruchu (tylko koniec toofront wewnętrzna)
11. Odmów wszystkich

zestaw reguł zapory rzeczywiste hello najprawdopodobniej będzie miał wiele innych reguł w toothese dodanie, reguły hello na dowolnym danym zapory będą także mieć różne numery niż hello te wymienione w tym miejscu. Tej listy i skojarzone z nimi numery są istotność tooprovide między tylko te reguły 11 i hello względny priorytet jeden z nich. Innymi słowy; zaporę rzeczywiste hello hello "RDP tooIIS01" może być numer reguły 5, ale tak długo, jak jest poniżej reguły "Zarządzanie zaporą" hello lub nowszym regułę "RDP tooDNS01" hello, którą będzie ona zgodna z zamiarem hello tej listy. Lista Hello także pomoże w hello poniżej scenariusze umożliwiające skrócenia; np. "Reguła Zapory 9 (DNS)". Jednak hello cztery reguły protokołu RDP będzie zbiorczo skrót, "tekst hello reguły protokołu RDP" gdy scenariusz ruchu hello jest tooRDP niepowiązanych.

Odwołaj również, czy grupy zabezpieczeń sieci w miejscu dla ruchu przychodzącego internet na powitania serwera sieci Web i podsieci wewnętrznej bazy danych.

#### <a name="allowed-internet-tooweb-server"></a>(Dozwolone) Internet tooWeb serwera
1. Strony internetowe użytkownika żądania HTTP z SecSvc001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. Chmury usługi przekazuje ruch przez otwarty punkt końcowy interfejsu toofirewall port 80 na 10.0.0.4:80
3. Nie NSG przypisane tooSecurity podsieci, więc reguły NSG systemu zezwalają na ruch toofirewall
4. Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)
5. Zapora rozpoczyna przetwarzanie reguł:
   1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
   2. Reguły Zapory 2-5 (zasad protokołu RDP) nie zastosować, przenieść toonext regułę
   3. PD zasady 6 (aplikacji: sieci Web) zastosować, ruch jest dozwolony, zapory NAT go too10.0.1.4 (IIS01)
6. podsieci frontonu Hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. 1 reguły NSG (Zablokuj Internet) nie ma zastosowania (ruch został NAT czy przez zaporę Windows hello, w związku z tym adresu źródłowego hello jest teraz hello zaporą, który znajduje się w podsieci zabezpieczeń hello i widoczne dla podsieci Frontend hello NSG toobe "lokalnie" ruchu, w związku z tym jest dozwolone), przenieść toonext regułę
   2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
7. IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello
8. IIS01 prób tooinitiates tooAppVM01 sesji FTP w podsieci wewnętrznej bazy danych
9. Witaj przez trasy podsieci frontonu sprawia, że hello zapory hello następnego skoku
10. Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony
11. Zapora rozpoczyna przetwarzanie reguł:
    1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
    2. Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę
    3. PD zasady 6 (aplikacji: sieci Web) nie są spełnione, przenieść toonext regułę
    4. PD zasady 7 (aplikacji: wewnętrznej bazy danych) jest stosowana, ruch jest dozwolony, zapora przekazuje ruch too10.0.2.5 (AppVM01)
12. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
    1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
    2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
13. AppVM01 odbiera żądanie hello i inicjuje hello sesji i odpowiada
14. trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku
15. Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone
16. Ponieważ to zwraca ruchu na zapory hello ustanowienie sesji przekazuje hello odpowiedzi serwera sieci web wstecz toohello (IIS01)
17. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
    1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
    2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
18. powitania serwera IIS otrzyma odpowiedź hello, zakończeniu transakcji hello z AppVM01 i następnie kończy tworzenie hello odpowiedzi HTTP, odpowiedź HTTP zostanie wysłany toohello obiektu żądającego
19. Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci frontonu jest dozwolona
20. Witaj zapory hello trafień odpowiedzi HTTP, a ponieważ jest to tooan odpowiedzi hello ustanowić sesji translatora adresów Sieciowych jest akceptowany przez zaporę Windows hello
21. Witaj zapory, a następnie przekierowuje hello toohello wstecz odpowiedzi użytkownika Internet
22. Ponieważ nie ma żadnych reguł NSG dla ruchu wychodzącego ani przeskoków przez podsieci frontonu hello odpowiedź hello jest dozwolone, a hello Internet użytkownik otrzymuje hello strona sieci web.

#### <a name="allowed-internet-rdp-toobackend"></a>(Dozwolone) TooBackend protokołu RDP z Internetu
1. Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP za pośrednictwem SecSvc001.CloudApp.Net:8025, gdzie 8025 jest numer portu przypisany użytkownik hello reguły zapory "RDP tooAppVM01" hello
2. usługi w chmurze Hello przekazuje ruch za pośrednictwem punktu końcowego Otwórz hello interfejsu toofirewall 8025 portu na 10.0.0.4:8025
3. Nie NSG przypisane tooSecurity podsieci, więc reguły NSG systemu zezwalają na ruch toofirewall
4. Zapora rozpoczyna przetwarzanie reguł:
   1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
   2. 2 reguły Zapory (RDP IIS) nie ma zastosowania, przenieść toonext regułę
   3. PD zasady 3 (RDP DNS01) nie ma zastosowania, przenieść toonext regułę
   4. Zastosować PD zasady 4 (RDP AppVM01), ruch jest dozwolony, zapory NAT go too10.0.2.5:3386 (portem RDP na AppVM01)
5. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. 1 reguły NSG (Zablokuj Internet) nie ma zastosowania (ruch został NAT czy przez zaporę Windows hello, w związku z tym adresu źródłowego hello jest teraz hello zaporą, który znajduje się w podsieci zabezpieczeń hello i widoczne dla podsieci wewnętrznej bazy danych hello NSG toobe "lokalnie" ruchu, w związku z tym jest dozwolone), przenieść toonext regułę
   2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
6. AppVM01 nasłuchuje ruchu protokołu RDP i odpowiada
7. Z wychodzących reguł NSG Zastosuj reguły domyślne, a zwracany ruch jest dozwolony
8. PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku
9. Ponieważ to zwraca ruchu na zapory hello ustanowienie sesji przekazuje hello odpowiedzi wstecz toohello internet użytkownika
10. Włączono sesji protokołu RDP
11. AppVM01 wyświetli monit o hasło nazwy użytkownika

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Dozwolone) Wyszukiwania DNS serwera sieci Web na serwerze DNS
1. Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.
2. Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello
3. PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku
4. Brak wychodzących reguł NSG są powiązane toohello podsieci frontonu, ruch jest dozwolony.
5. Zapora rozpoczyna przetwarzanie reguł:
   1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
   2. Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę
   3. Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę
   4. 8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę
   5. Zastosuj reguły Zapory 9 DNS (Domain Name System), ruch jest dozwolony, zapora przekazuje ruch too10.0.2.4 (DNS01)
6. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
   1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
   2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
7. Serwer DNS odbiera żądanie hello
8. Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet
9. PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku
10. Nie wychodzące reguły NSG podsieci wewnętrznej bazy danych, ruch jest dozwolony
11. Zapora rozpoczyna przetwarzanie reguł:
    1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
    2. Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę
    3. Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę
    4. Zastosuj 8 reguły Zapory (tooInternet), ruch jest dozwolony, sesja jest SNAT limit tooroot DNS serwera na powitania Internet
12. Serwer DNS w Internecie odpowiada, ponieważ w tej sesji zostało zainicjowane w zaporze hello, odpowiedź hello jest akceptowany przez zaporę Windows hello
13. Jak jest to ustanowienie sesji, zapory hello przekazuje toohello odpowiedzi hello inicjowania serwera, DNS01
14. podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:
    1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
    2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
15. Hello serwer DNS odbiera i buforuje odpowiedź hello i następnie odpowiada tooIIS01 wstecz toohello żądania początkowego
16. trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku
17. Wychodzące NSG nie istnieją żadne reguły podsieci wewnętrznej bazy danych hello ruch jest dozwolony.
18. Jest to ustanowienie sesji na zaporze hello, odpowiedź hello jest przesyłany dalej przez serwer IIS wstecz toohello zapory hello
19. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
    1. Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG
    2. Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony
20. IIS01 odbiera odpowiedź hello z DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Dozwolone) TooFrontend serwera wewnętrznej bazy danych
1. Administrator zalogowany tooAppVM02 za pomocą protokołu RDP zażąda pliku bezpośrednio z serwerem IIS01 hello za pomocą Eksploratora plików systemu windows
2. trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku
3. Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone
4. Zapora rozpoczyna przetwarzanie reguł:
   1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
   2. Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę
   3. Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę
   4. 8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę
   5. 9 reguły Zapory (DNS, Domain Name System) nie ma zastosowania, przenieść toonext regułę
   6. Zastosuj 10 reguły Zapory (Intra-podsieć), ruch jest dozwolony, zapora przekazuje ruch too10.0.1.4 (IIS01)
5. Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:
   1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
   2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
6. Zakładając, że odpowiednie uwierzytelniania i autoryzacji, IIS01 akceptuje Żądanie hello i odpowiada
7. Witaj przez trasy podsieci frontonu sprawia, że hello zapory hello następnego skoku
8. Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci frontonu jest dozwolona
9. Jak jest to istniejącej sesji na zaporze hello ta odpowiedź jest dozwolone i zapory hello zwraca hello tooAppVM02 odpowiedzi
10. Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:
    1. Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę
    2. Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG
11. AppVM02 odbiera odpowiedź hello

#### <a name="denied-internet-direct-tooweb-server"></a>(Odmowa) Bezpośrednie tooWeb internetowego serwera
1. Internet użytkownik spróbuje tooaccess powitania serwera sieci web, IIS01, za pośrednictwem hello FrontEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla ruchu HTTP, to nie będzie przekazywać hello usługi w chmurze i nie osiągnięcia powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, hello NSG (Zablokuj Internet) w podsieci frontonu hello uniemożliwiają ten ruch
4. Na koniec trasy przez podsieci frontonu hello wyśle cały ruch wychodzący z zapory toohello IIS01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym istnieją przynajmniej trzy warstwy niezależne sposobem ochrony między hello internet i IIS01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.

#### <a name="denied-internet-toobackend-server"></a>(Odmowa) Internet tooBackend serwera
1. Internet użytkownik spróbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi
2. Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, hello NSG (Zablokuj Internet) umożliwia zablokowanie tego ruchu
4. Na koniec trasy przez hello wyśle cały ruch wychodzący z zapory toohello AppVM01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym są co najmniej trzy warstwy niezależne obrony między Witaj internet i AppVM01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.

#### <a name="denied-frontend-server-toobackend-server"></a>(Odmowa) TooBackend serwera frontonu serwera
1. Przykładowa IIS01 zostało naruszone i działa złośliwego kodu w trakcie serwerów podsieci wewnętrznej bazy danych hello tooscan.
2. trasy przez podsieci frontonu Hello czy Wyślij cały ruch wychodzący z zapory toohello IIS01 jako hello następnego przeskoku. Nie jest to coś, który może być modyfikowany przez hello naruszenia zabezpieczeń maszyny Wirtualnej.
3. zapory Hello może przetwarzać ruchu hello, jeśli Żądanie hello zostało tooAppVM01 lub toohello serwera DNS podczas wyszukiwania DNS, które potencjalnie być dozwolony ruch przez zaporę Windows hello (powodu tooFW zasady 7 i 9). Wszelki inny ruch zostałby zablokowany przez PD zasady 11 (Odmów wszystko).
4. Jeśli zaawansowane wykrywanie zagrożeń włączono zaporę hello (nieuwzględnionego w tym dokumencie, zobacz hello dokumentacji dostawcy dla urządzenia określoną sieć zaawansowane funkcje zagrożenia), nawet ruch będzie dozwolony przez hello podstawowe zasady przekazywania omówione w tym dokumencie można zapobiegać Jeśli ruch hello zawarte podpisów znanych lub wzorce, które Flaga regułę advanced threat.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Odmowa) Wyszukiwania DNS w Internecie na serwerze DNS
1. Internet użytkownik spróbuje toolookup wewnętrzny rekord DNS na DNS01 za pośrednictwem usługi BackEnd001.CloudApp.Net 
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla ruchu DNS, to nie przejdzie za pośrednictwem hello usługi w chmurze i nie osiągnięcia powitania serwera
3. Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG hello (Zablokuj Internet) w podsieci frontonu hello uniemożliwiają ten ruch
4. Na koniec tras przez podsieci wewnętrznej bazy danych hello wyśle cały ruch wychodzący z zapory toohello DNS01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym istnieją przynajmniej trzy warstwy niezależne sposobem ochrony między hello internet i DNS01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Odmowa) Dostęp do tooSQL Internetu przez zaporę
1. Internet użytkownik żąda danych SQL z SecSvc001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)
2. Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, to nie przejdzie hello usługi w chmurze i nie osiągnąć hello zapory
3. Jeśli punkty końcowe SQL były otwarte jakiegoś powodu, zapory hello może rozpocząć przetwarzania zasad:
   1. PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę
   2. Reguły Zapory 2-5 (zasad protokołu RDP) nie zastosować, przenieść toonext regułę
   3. Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę
   4. 8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę
   5. 9 reguły Zapory (DNS, Domain Name System) nie ma zastosowania, przenieść toonext regułę
   6. 10 reguły Zapory (Intra-podsieci) nie ma zastosowania, przenieść toonext regułę
   7. Zastosować PD zasady 11 (Odmów wszystko), ruch jest przetwarzania zasad zablokowane, stop

## <a name="references"></a>Dokumentacja
### <a name="main-script-and-network-config"></a>Skrypt głównego i konfiguracji sieci
Zapisz hello pełne skryptu w pliku skryptu programu PowerShell. Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf2.xml".
Modyfikuj zmienne zdefiniowane przez użytkownika hello, zgodnie z potrzebami. Uruchom skrypt hello, a następnie postępuj zgodnie z powyższych instrukcji instalacji reguły zapory hello.

#### <a name="full-script"></a>Pełna skryptu
Ten skrypt zostanie, na podstawie hello zmiennych zdefiniowanych przez użytkownika:

1. Połącz tooan subskrypcji platformy Azure
2. Utwórz nowe konto magazynu
3. Utwórz nową sieć wirtualną i trzy podsieci zgodnie z definicją w pliku konfiguracji sieci hello
4. Tworzenie maszyn wirtualnych pięć; zapory 1 i 4 systemu windows server maszyny wirtualne
5. Skonfiguruj przez w tym:
   1. Utworzenie dwóch nowych tabel tras
   2. Dodawanie tras toohello tabel
   3. Powiąż podsieci tooappropriate tabel
6. Włączanie funkcji przesyłania dalej IP na powitania NVA
7. Skonfiguruj grupy NSG w tym:
   1. Tworzenie grupy NSG
   2. Dodanie reguły
   3. Powiązanie hello NSG toohello odpowiednie podsieci

Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.

> [!IMPORTANT]
> Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell. Tylko komunikaty o błędach na czerwono są przyczyną problemu.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Plik konfiguracji sieci
Zapisz ten plik xml z lokalizacji zaktualizowane i Dodaj hello łącze toothis pliku toohello $NetworkConfigFile zmiennej w skrypcie hello powyżej.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Przykładowe skrypty aplikacji
Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Dwukierunkowe DMZ NVA, NSG i przez"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Widok logiczny hello reguły zapory"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Utwórz obiekt sieci frontonu"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Utwórz obiekt serwera DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Kopiowanie reguły domyślnej protokołu RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Reguła AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Ikona przekierowania aplikacji"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Ikona NAT docelowego"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Ikona — dostęp próbny"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Reguły zapory zarządzania"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Reguły zapory protokołu RDP"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Reguła zapory w sieci Web"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Reguły zapory AppVM01"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Reguła ruchu wychodzącego"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Reguły zapory DNS"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Reguła sieci wirtualnej wewnątrz zapory"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Zapora regułę Odmów"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Aktywacja reguły zapory"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
