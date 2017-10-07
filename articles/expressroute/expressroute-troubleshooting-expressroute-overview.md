---
title: "Weryfikowanie łączności: ExpressRoute Azure przewodnik rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące rozwiązywania problemów i weryfikowanie łączności tooend zakończenia obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Sprawdzanie połączenia ExpressRoute
ExpressRoute, który rozciąga się sieci lokalnej na powitania firmy Microsoft w chmurze prywatnej połączenie, które umożliwiają to dostawca połączenia, obejmuje następujące trzy różne sieci strefy hello:

-   Sieci klienta
-   Dostawcy sieci
-   Centrum danych firmy Microsoft

Witaj celem niniejszego dokumentu jest tooidentify użytkownika toohelp gdzie (lub nawet wtedy, gdy) istnieje problem z łącznością, w której strefy, co tooseek pomoże od zespołu odpowiednie tooresolve hello problemu. Jeśli pomocy technicznej firmy Microsoft jest wymagana tooresolve problem, otwórz bilet pomocy technicznej z [Microsoft Support][Support].

> [!IMPORTANT]
> Ten dokument jest zamierzone toohelp diagnozowania i rozwiązywania problemów proste. Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft. Otwórz bilet pomocy technicznej z [Microsoft Support] [ Support] przypadku toosolve hello problem przy użyciu hello wskazówki.
>
>

## <a name="overview"></a>Omówienie
Witaj Poniższy diagram przedstawia hello logicznej łączność sieci tooMicrosoft sieci klienta, za pomocą usługi ExpressRoute.
[![1]][1]

W hello poprzedzających diagramu liczby hello wskazują punkty klucza sieci. punkty sieci Hello odwołuje się często za pośrednictwem tego artykułu numeru skojarzone.

W zależności od połączenia ExpressRoute hello modelu (chmury Exchange wspólnej lokalizacji, bezpośrednie połączenie sieci Ethernet lub dowolny z każdym (IPVPN)) hello sieci punkty 3 i 4 mogą być przełączniki (warstwy 2 urządzenia). punkty klucza sieciowego Hello przedstawione są następujące:

1.  Urządzenie obliczeniowe klienta (na przykład serwera lub komputera)
2.  CEs: Routery brzegowe klienta uzyskują 
3.  PEs (skierowane do CE): Dostawca krawędzi routery czy przełączniki które stoją routery brzegowe klienta uzyskują. Określony tooas PE CEs w niniejszym dokumencie.
4.  PEs (MSEE połączonej): Dostawca krawędzi routery czy przełączniki które stoją MSEEs. Określony tooas PE MSEEs w niniejszym dokumencie.
5.  MSEEs: Routery Microsoft Edge przedsiębiorstwa (MSEE) ExpressRoute
6.  Brama sieci wirtualnej (VNet)
7.  Obliczenia bazy danych urządzenia na powitania sieci wirtualnej Azure

Jeśli modele łączności chmury Exchange wspólnej lokalizacji lub połączenia Ethernet Point-to-Point hello są używane, router brzegowy klienta hello (2) czy ustanowić komunikację równorzędną za MSEEs (5) Protokół BGP. Sieci punkty 3 i 4 będzie nadal istnieje, ale nieco przejrzyste jako urządzenia warstwy 2.

Jeśli model usługi łączności dowolny z każdym (IPVPN) hello jest używany, hello PEs (skierowane do MSEE) (4) czy nawiązania komunikacji równorzędnej z MSEEs (5) Protokół BGP. Tras czy rozpropagowane wstecz toohello sieci klienta za pośrednictwem sieci dostawcy usług IPVPN hello.

>[!NOTE]
>Wysoką dostępność usługi ExpressRoute firma Microsoft wymaga parę nadmiarowych sesje BGP między MSEEs (5) i PE-MSEEs (4). Parę nadmiarowych ścieżek sieciowych zaleca się między sieci klienta i serwera CEs PE. Jednak w model połączenia dowolny z każdym (IPVPN), pojedyncze urządzenie CE (2) może być połączone tooone lub więcej PEs (3).
>
>

(punktowi hello sieci określona przez liczbę hello skojarzone) obejmuje toovalidate obwodu usługi ExpressRoute, hello następujące kroki:
1. [Sprawdź poprawność aprowizacji obwodów i stan (5)](#validate-circuit-provisioning-and-state)
2. [Sprawdzanie poprawności co najmniej jeden ExpressRoute komunikacji równorzędnej jest skonfigurowany (5)](#validate-peering-configuration)
3. [Sprawdź poprawność ARP od dostawcy usług firmy Microsoft i hello (łącze od 4 do 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Sprawdź poprawność protokołu BGP oraz tras na powitania MSEE (BGP między 4 too5 i 5 too6 Jeśli sieci wirtualnej jest podłączona)](#validate-bgp-and-routes-on-the-msee)
5. [Sprawdź hello statystyki ruchu (ruchu przechodzącego przez 5)](#check-the-traffic-statistics)

Więcej operacji sprawdzania poprawności i kontroli zostaną dodane w hello o przyszłych, zajrzyj tu co miesiąc!

##<a name="validate-circuit-provisioning-and-state"></a>Sprawdź poprawność aprowizacji obwodów i stanu
Niezależnie od tego modelu łączności hello obwodu usługi ExpressRoute ma toobe utworzone, dlatego usługa klucz wygenerowany dla aprowizacji obwodów. Inicjowanie obsługi administracyjnej obwodu usługi ExpressRoute ustanawia nadmiarowych połączeń warstwy 2 między PE-MSEEs (4) i MSEEs (5). Aby uzyskać więcej informacji dotyczących sposobu toocreate, modyfikowanie, udostępnić i sprawdzić obwodu usługi ExpressRoute, zobacz artykuł hello [tworzenia i modyfikowania obwodu usługi expressroute][CreateCircuit].

>[!TIP]
>Klucz usługi unikatowo identyfikuje obwodu usługi ExpressRoute. Ten klucz jest wymagany dla większości poleceń programu powershell hello wymienione w niniejszym dokumencie. Ponadto, jeśli będzie potrzebna pomoc przez firmę Microsoft lub tootroubleshoot partner usługi ExpressRoute problemu ExpressRoute, dostarcza hello usługi klucza tooreadily zidentyfikować hello obwodu.
>
>

###<a name="verification-via-hello-azure-portal"></a>Weryfikacja za pomocą hello portalu Azure
W portalu Azure hello, można sprawdzić stan hello obwodu usługi ExpressRoute, wybierając ![2][2] na powitania po lewej stronie paska menu, a następnie wybierając hello obwodu usługi expressroute. Wybranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" zostanie otwarty blok obwodu ExpressRoute hello. W hello ![3][3] części bloku hello hello ExpressRoute essentials są wyświetlane, jak pokazano w powitania po zrzut ekranu:

![4][4]    

W hello ExpressRoute Essentials *obwodu stan* wskazuje stan hello obwodu hello na powitania po stronie firmy Microsoft. *Dostawca stanu* wskazuje, czy został obwodu hello *obsługiwane administracyjnie nie zainicjowano obsługę administracyjną* po stronie dostawcy usług hello. 

Dla usługi ExpressRoute obwodu toobe operacyjne, hello *obwodu stan* musi być *włączone* i hello *stan dostawcy* musi być *obsługiwane administracyjnie*.

>[!NOTE]
>Jeśli hello *obwodu stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support]. Jeśli hello *stan dostawcy* jest nieudostępniane, skontaktuj się z dostawcą usług.
>
>

###<a name="verification-via-powershell"></a>Weryfikacja za pomocą programu PowerShell
toolist wszystkie hello obwody usługi ExpressRoute w grupie zasobów, użyj następującego polecenia hello:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Nazwę grupy zasobów można uzyskać za pośrednictwem hello portalu Azure. Zobacz poprzednie podsekcji hello tego dokumentu i należy pamiętać, że hello nazwę grupy zasobów jest wymieniona w zrzut ekranu przedstawiający przykładowy hello.
>
>

tooselect danego obwodu usługi expressroute w grupie zasobów, hello Użyj następującego polecenia:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Przykładowa odpowiedź jest:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm, jeśli działa obwodu usługi ExpressRoute, należy zwrócić szczególną uwagę toohello następujące pola:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Jeśli hello *CircuitProvisioningState* jest wyłączona, skontaktuj się z [Microsoft Support][Support]. Jeśli hello *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.
>
>

###<a name="verification-via-powershell-classic"></a>Weryfikacja za pomocą programu PowerShell (klasyczne)
toolist wszystkie hello obwody usługi ExpressRoute w ramach subskrypcji, użyj następującego polecenia hello:

    Get-AzureDedicatedCircuit

tooselect danego obwodu ExpressRoute, hello Użyj następującego polecenia:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Przykładowa odpowiedź jest:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm jeśli działa obwodu usługi ExpressRoute, należy zwrócić szczególną uwagę toohello następujące pola: ServiceProviderProvisioningState: stan elastycznie: włączone

>[!NOTE]
>Jeśli hello *stan* jest wyłączona, skontaktuj się z [Microsoft Support][Support]. Jeśli hello *ServiceProviderProvisioningState* jest nieudostępniane, skontaktuj się z dostawcą usług.
>
>

##<a name="validate-peering-configuration"></a>Sprawdź poprawność konfiguracji komunikacji równorzędnej
Dostawcy usług powitania po hello ukończono aprowizacji obwodu ExpressRoute hello konfigurację routingu mogą być tworzone przez hello obwodu ExpressRoute między MSEE-PRs (4) i MSEEs (5). Każdy obwód usługi ExpressRoute może mieć jedną, dwie lub trzy konteksty routingu włączona: prywatnej komunikacji równorzędnej platformy Azure (ruchu tooprivate sieci wirtualne na platformie Azure), publicznej komunikacji równorzędnej platformy Azure (ruchu toopublic adresy IP na platformie Azure) i (ruchu tooOffice 365 komunikacji równorzędnej firmy Microsoft i Dynamics 365). Aby uzyskać więcej informacji na temat toocreate i modyfikować konfigurację routingu, zobacz artykuł hello [tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Weryfikacja za pomocą hello portalu Azure
>[!IMPORTANT]
>Brak znaną usterką w portalu Azure, w którym są komunikacji równorzędnych ExpressRoute hello *nie* wyświetlana w portalu hello skonfigurowanie hello usługodawcy. Dodawanie komunikacji równorzędnych ExpressRoute za pośrednictwem portalu hello lub programu PowerShell *zastąpienie ustawień dostawcy usługi hello*. Ta akcja dzieli hello routingu na powitania obwodu ExpressRoute i wymaga obsługi hello hello usługi dostawcy toorestore hello ustawień i ponownie ustanowić normalna routingu. Komunikacji równorzędnych ExpressRoute hello należy modyfikować tylko wtedy, jeśli jest pewność, że tego dostawcę usługi hello zapewnia tylko warstwy 2 usługi!
>
>

<p/>
>[!NOTE]
>W przypadku warstwy 3 dostarczane przez hello komunikacji równorzędnych dostawcy i hello usługi są puste w portalu hello, programu PowerShell może być ustawienia skonfigurowanego dostawcy usługi hello toosee używane.
>
>

W portalu Azure hello, można sprawdzić stan obwodu usługi ExpressRoute, wybierając ![2][2] na powitania po lewej stronie paska menu, a następnie wybierając hello obwodu usługi expressroute. Wybieranie ExpressRoute obwodu wymienione w obszarze "Wszystkie zasoby" zostaną otwarte bloku obwodu ExpressRoute hello. W hello ![3][3] części bloku hello hello ExpressRoute otrzyma essentials, jak pokazano w powitania po zrzut ekranu:

![5][5]

W hello poprzedzających przykładzie jako dostrzeżone Azure prywatnej komunikacji równorzędnej kontekstu routingu jest włączone, natomiast Azure publicznego i konteksty routingu komunikacji równorzędnej firmy Microsoft nie są włączone. Pomyślnie włączono kontekstu komunikacji równorzędnej musi również hello podsieci podstawowego i pomocniczego point-to-point (wymagane dla protokołu BGP) na liście. Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs. 

>[!NOTE]
>Jeśli nie włączono komunikacji równorzędnej, sprawdź, jeśli hello podstawowych i pomocniczych podsieci przypisane zgodne konfiguracji hello na PE MSEEs. Jeśli nie, toochange hello konfiguracji na routerach MSEE, zapoznaj się zbyt[Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Weryfikacja za pomocą programu PowerShell
tooget hello Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej, jest:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Pomyślnie włączono kontekstu komunikacji równorzędnej musi prefiksy adresów podstawowych i pomocniczych hello na liście. Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs.

tooget hello Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Jeśli nie skonfigurowano komunikacji równorzędnej, może to być komunikat o błędzie. Przykładowa odpowiedź, gdy hello wyrażony w komunikacji równorzędnej (Azure publicznej komunikacji równorzędnej, w tym przykładzie) nie jest skonfigurowany w ramach obwodu hello:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Jeśli komunikacji równorzędnej nie jest włączona, upewnij się, hello przypisanych podsieci podstawowego i pomocniczego dopasowania hello konfiguracji na powitania połączony PE MSEE. Również poprawić Sprawdź, czy hello *VlanId*, *AzureASN*, i *PeerASN* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE. Jeśli wybrano opcję tworzenia skrótu MD5, klucz udostępniony hello powinny być takie same na pary MSEE i PE MSEE. Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Weryfikacja za pomocą programu PowerShell (klasyczne)
tooget hello Azure prywatnej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następujące polecenie:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Przykładowa odpowiedź dla pomyślnie skonfigurowano prywatnej komunikacji równorzędnej jest:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Pomyślnie włączono A komunikacji równorzędnej kontekstu musi podsieci podstawowego i pomocniczego elementu równorzędnego hello wymienione. Witaj /30 podsieci służą do adresu IP interfejsu hello hello MSEEs i PE MSEEs.

tooget hello Azure publicznej komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft komunikacji równorzędnej szczegółów konfiguracji, użyj hello następującego polecenia:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Jeśli komunikacji równorzędnych warstwy 3 zostały określone przez usługodawcę hello, ustawienie komunikacji równorzędnych ExpressRoute hello za pośrednictwem portalu hello lub programu PowerShell zastępuje ustawienia dostawcy usługi hello. Resetowanie ustawień komunikacji równorzędnej hello dostawcy po stronie wymaga obsługi hello hello dostawcy usług. Komunikacji równorzędnych ExpressRoute hello należy modyfikować tylko wtedy, jeśli jest pewność, że tego dostawcę usługi hello zapewnia tylko warstwy 2 usługi!
>
>

<p/>
>[!NOTE]
>Jeśli komunikacji równorzędnej nie jest włączona, upewnij się, hello podstawowego i pomocniczego elementu równorzędnego przypisanych podsieci dopasowania hello konfiguracji na powitania połączony PE MSEE. Również poprawić Sprawdź, czy hello *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE. Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za [Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Sprawdź poprawność ARP od dostawcy usług firmy Microsoft i hello
Ta sekcja używa poleceń programu PowerShell (klasyczny). Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora subskrypcji toohello za pośrednictwem [klasycznego portalu Azure][OldPortal]. Rozwiązywanie problemów przy użyciu usługi Azure Resource Manager polecenia można znaleźć w artykule toohello [pobierania ARP tabele w modelu wdrażania usługi Resource Manager hello] [ ARP] dokumentu.

>[!NOTE]
>można tooget ARP, zarówno hello portalu Azure, jak i poleceń programu PowerShell usługi Azure Resource Manager. Jeśli za pomocą polecenia programu PowerShell usługi Azure Resource Manager hello zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.
>
>

tooget hello tabeli protokołu ARP z hello głównej MSEE routera hello prywatnej komunikacji równorzędnej, użyj następującego polecenia hello:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Przykład odpowiedzi dla polecenia hello, w scenariuszu pomyślne hello:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Analogicznie, można sprawdzić hello tabeli protokołu ARP z hello MSEE w hello *głównej*/*dodatkowej* ścieżki dla *prywatnej* /  *Publiczny*/*Microsoft* komunikacji równorzędnych.

Witaj poniższy przykład, że pokazuje hello odpowiedzi polecenia powitania dla komunikacji równorzędnej nie istnieje.

    ARP Info:
       
>[!NOTE]
>Jeśli nie ma tabeli protokołu ARP hello adresy IP interfejsów hello zamapowane tooMAC adresy, hello Przejrzyj następujące informacje:
>1. Jeśli hello pierwszy adres IP podsieci hello /30 hello łącza między hello MSEE PR a MSEE jest używana w hello interfejsu MSEE PR. Azure zawsze używa hello drugiego adresu IP dla MSEEs.
>2. Upewnij się, jeśli powitania klienta (C-znacznik) i znaczniki sieci VLAN usługi (S-Tag) odpowiadają na pary MSEE PR i MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Sprawdź poprawność protokołu BGP oraz tras na powitania MSEE
Ta sekcja używa poleceń programu PowerShell (klasyczny). Jeśli z polecenia programu PowerShell usługi Azure Resource Manager, upewnij się, że masz dostęp administratora/współadministratora subskrypcji toohello za pośrednictwem [klasycznego portalu Azure][OldPortal]

>[!NOTE]
>tooget BGP informacje, oba hello portalu Azure i poleceń programu PowerShell usługi Azure Resource Manager może zostać użyty. Jeśli za pomocą polecenia programu PowerShell usługi Azure Resource Manager hello zostaną napotkane błędy, klasycznym poleceń programu PowerShell powinna działać jako klasycznego środowiska PowerShell poleceń również współpracować z obwody usługi ExpressRoute Menedżera zasobów Azure.
>
>

tooget hello tabeli routingu (BGP sąsiada) podsumowania dla określonego kontekstu routingu, użyj następującego polecenia hello:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Oto przykład odpowiedzi jest:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Jak przedstawiono hello poprzedzających przykład, polecenie hello jest przydatne toodetermine na jak długo została ustanowiona hello kontekstu routingu. Wskazuje ona także liczby prefiksów trasy anonsowane przez router hello w komunikacji równorzędnej.

>[!NOTE]
>Jeśli hello stan jest aktywny lub bezczynności, sprawdź hello podstawowego i pomocniczego elementu równorzędnego przypisanych podsieci dopasowania hello konfiguracji na powitania połączony PE MSEE. Również poprawić Sprawdź, czy hello *VlanId*, *AzureAsn*, i *PeerAsn* są używane na MSEEs i jeśli te wartości mapuje toohello używane na powitania połączone PE MSEE. Jeśli wybrano opcję tworzenia skrótu MD5, klucz udostępniony hello powinny być takie same na pary MSEE i PE MSEE. Konfiguracja hello toochange na routerach MSEE hello, można znaleźć za[Utwórz i zmodyfikuj routingu dla obwodu usługi ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Jeśli niektóre miejsca docelowe są niedostępne w szczególności komunikacji równorzędnej, sprawdź hello tabeli tras MSEEs hello należących toohello określonego kontekstu komunikacji równorzędnej. Jeśli zgodny prefiks (może być NATed IP) znajduje się w tabeli routingu hello, następnie sprawdź, czy istnieją zapór / / listy ACL grupy NSG na ścieżce hello i jeżeli pozwalają hello ruchu.
>
>

tooget hello pełne tabeli routingu z MSEE na powitania *głównej* ścieżki dla konkretnego hello *prywatnej* kontekstu routingu hello Użyj następującego polecenia:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Przykład pomyślnego wyniku dla polecenia hello jest:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Analogicznie, można sprawdzić hello tabeli routingu z hello MSEE w hello *głównej*/*dodatkowej* ścieżki dla *prywatnej* / *Publicznych*/*Microsoft* komunikacji równorzędnej kontekstu.

Witaj poniższy przykład, że pokazuje hello odpowiedzi polecenia powitania dla komunikacji równorzędnej nie istnieje:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Sprawdź hello statystyki ruchu
tooget hello łączyć statystyki ruchu ścieżki podstawowego i pomocniczego — bajtów i wylogowywanie — kontekstu komunikacji równorzędnej, hello Użyj następującego polecenia:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Przykładowe dane wyjściowe polecenia hello jest:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Przykładowe dane wyjściowe polecenia powitania dla nieistniejącego komunikacji równorzędnej jest:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji lub uzyskać pomoc zapoznaj się hello następującego łącza:

- [Pomoc techniczna firmy Microsoft][Support]
- [Tworzenie i modyfikowanie obwodu usługi ExpressRoute][CreateCircuit]
- [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Połączenie logiczne Express Route"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Wszystkie zasoby ikony"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Ikona — omówienie"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Zrzut ekranu przykładu ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Zrzut ekranu przykładu ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






