---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Azure: klasyczny | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute (klasyczne)
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-routing-cli.md)
> * [Video - prywatnej komunikacji równorzędnej](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - publicznej komunikacji równorzędnej](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - komunikacji równorzędnej firmy Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-routing-classic.md)
> 

W tym artykule przedstawiono hello kroki toocreate i zarządzaj nimi konfiguracji routingu dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell i hello klasycznego modelu wdrażania. Poniższe kroki Hello wyświetli również, jak toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji
* Konieczne będzie hello najnowszą wersję hello poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko). Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).  
* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie toobe toorun stanie hello poleceń cmdlet opisane poniżej.

> [!IMPORTANT]
> Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2. Jeśli korzystasz z usług dostawcy oferującego zarządzane usługi warstwy 3 (zwykle IPVPN, np. MPLS), dostawca połączenia skonfiguruje routing i będzie nim zarządzać.
> 
> 

Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute. Możesz skonfigurować komunikację równorzędną w dowolnej kolejności. Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Zaloguj się za tooyour konto platformy Azure i wybierz subskrypcję
1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

        Login-AzureRmAccount

2. Sprawdź subskrypcje hello hello konta.

        Get-AzureRmSubscription

3. Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Następnie należy użyć następującego polecenia cmdlet tooadd hello tooPowerShell Twojej subskrypcji platformy Azure dla hello klasycznego modelu wdrażania.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Prywatna komunikacja równorzędna Azure
Ta sekcja zawiera instrukcje jak toocreate, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate Azure prywatnej komunikacji równorzędnej
1. **Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**
   
    Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Utworzyć obwodu usługi ExpressRoute.**
   
    Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello. Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello. 
3. **Sprawdź hello tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana.**
   
    Jeśli hello obwodu ExpressRoute jest udostępniane i również włączone, należy najpierw zaznaczyć toosee. Zobacz poniższy przykład hello.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone. W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu.**
   
    Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:
   
   * / 30 podsieci dla linku podstawowego hello. Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.
   * / 30 podsieci hello dodatkowej łącza. Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.
   * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
   * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS. Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej. Pamiętaj, aby nie używać numeru 65515.
   * Skrót MD5 po wybraniu toouse jeden. **Jest to opcjonalne**.
     
    Można uruchomić następujące polecenie cmdlet tooconfigure prywatnej komunikacji równorzędnej platformy Azure dla obwodu hello.
     
        Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100
     
    Można zastosować poniższe polecenie cmdlet hello, jeśli wybierzesz toouse skrótu MD5.
     
        Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure prywatnej komunikacji równorzędnej szczegóły
Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure
Można aktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello. W poniższym przykładzie hello hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete Azure prywatnej komunikacji równorzędnej
Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello.

> [!WARNING]
> Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu usługi expressroute, przed uruchomieniem tego polecenia cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Publiczna komunikacja równorzędna Azure
Ta sekcja zawiera instrukcje jak toocreate, get, aktualizować i usuwać hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate Azure publicznej komunikacji równorzędnej
1. **Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**
   
    Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Tworzenie obwodu usługi ExpressRoute**
   
    Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello. Jeśli dostawca połączenia oferuje zarządzanych usług warstwy 3, możesz poprosić użytkownika tooenable dostawcy łączności publicznej komunikacji równorzędnej dla Ciebie Azure. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello.
3. **Sprawdź tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana**
   
    Jeśli hello obwodu ExpressRoute jest udostępniane i również włączone, należy najpierw zaznaczyć toosee. Zobacz poniższy przykład hello.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone. W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla obwodu hello**
   
    Upewnij się, że masz hello następujących informacji przed przejściem dalej.
   
   * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4.
   * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4.
   * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
   * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
   * Skrót MD5 po wybraniu toouse jeden. **Jest to opcjonalne**.
     
    Możesz uruchomić następujące polecenie cmdlet tooconfigure publicznej komunikacji równorzędnej platformy Azure dla obwodu hello
     
        Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200
     
    Jeśli wybierzesz toouse skrótu MD5 służy hello poniższe polecenie cmdlet
     
        Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure publicznej komunikacji równorzędnej szczegóły
Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure publicznej konfiguracji komunikacji równorzędnej
Można zaktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Identyfikator sieci VLAN obwodu hello Hello jest aktualizowana z 200 too600 w hello powyżej przykładzie.

### <a name="toodelete-azure-public-peering"></a>toodelete Azure publicznej komunikacji równorzędnej
Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft
Ta sekcja zawiera instrukcje jak toocreate, get, aktualizować i usuwać hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>toocreate komunikacji równorzędnej firmy Microsoft
1. **Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**
   
    Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Tworzenie obwodu usługi ExpressRoute**
   
    Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello. Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello.
3. **Sprawdź tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana**
   
    Jeśli hello obwodu usługi expressroute, jest w stanie obsługiwane administracyjnie i włączone, należy najpierw zaznaczyć toosee.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone. W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft**
   
    Upewnij się, że masz hello następujących informacji, aby kontynuować.
   
   * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
   * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
   * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
   * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
   * Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP. Akceptowane są tylko prefiksy publicznych adresów IP. Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listy rozdzielanej przecinkami. Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.
   * Odbiorca ASN: Jeśli są anonsowania prefiksów, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer, można określić hello jako numer toowhich, które są zarejestrowane. **Jest to opcjonalne**.
   * Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.
   * Skrót MD5, jeśli wybierzesz toouse jeden. **Jest to opcjonalne.**
     
    Możesz uruchomić następujące polecenie cmdlet tooconfigure Microsoft pering dla obwodu hello
     
        Nowe AzureBGPPeering - AccessType Microsoft - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - VlanId 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes " 123.0.0.0/30 "- RoutingRegistryName"ARIN"- SharedKey"A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>Szczegóły komunikacji równorzędnej tooview firmy Microsoft
Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft
Można aktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete komunikacji równorzędnej firmy Microsoft
Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Następne kroki
Następnie [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-classic.md).

* Aby uzyskać więcej informacji o przepływach pracy, zobacz [przepływy pracy usługi ExpressRoute](expressroute-workflows.md).
* Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).

