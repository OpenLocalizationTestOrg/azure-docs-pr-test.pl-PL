---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Menedżer zasobów: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell

W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu programu PowerShell. Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute. Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-routing-cli.md)
> * [Video - prywatnej komunikacji równorzędnej](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - publicznej komunikacji równorzędnej](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - komunikacji równorzędnej firmy Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji

* Konieczne będzie hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). 
* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie poleceń cmdlet hello stanie toorun toobe w tym artykule.

Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.

> [!IMPORTANT]
> Mamy obecnie nie anonsuje skonfigurowane przez dostawców usług za pośrednictwem portalu zarządzania usługami hello komunikacji równorzędnych. Pracujemy nad tym, by wkrótce włączyć tę funkcję. Skontaktuj się z dostawcą usług przed rozpoczęciem konfigurowania komunikacji równorzędnych protokołu BGP.
> 
> 

Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute. Możesz skonfigurować komunikację równorzędną w dowolnej kolejności. Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie. 

## <a name="azure-private-peering"></a>Prywatna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate Azure prywatnej komunikacji równorzędnej

1. Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.

  Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Należy toorun programu PowerShell jako Administrator.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.

  ```powershell
  Import-AzureRM
  ```

  Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Zaloguj się na koncie tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute.

  Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.
3. Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona. Poniższy przykład hello użycia:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  odpowiedź Hello jest toohello podobnie poniższy przykład:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:

  * / 30 podsieci dla linku podstawowego hello. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * / 30 podsieci hello dodatkowej łącza. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS. Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej. Pamiętaj, aby nie używać numeru 65515.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.

  Użyj powitania po tooconfigure przykład prywatnej komunikacji równorzędnej dla obwodu usługi Azure:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure prywatnej komunikacji równorzędnej szczegóły

Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure

Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład. W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete Azure prywatnej komunikacji równorzędnej

Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:

> [!WARNING]
> Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu ExpressRoute przed uruchomieniem w tym przykładzie. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Publiczna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate Azure publicznej komunikacji równorzędnej

1. Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.

  Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Należy toorun programu PowerShell jako Administrator.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.

  ```powershell
  Import-AzureRM
  ```

  Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.

  ```powershell
  Import-Module AzureRM.Network
```

  Zaloguj się na koncie tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute.

  Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.
3. Sprawdź tooensure obwodu ExpressRoute hello jest udostępniane i włączona. Poniższy przykład hello użycia:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  odpowiedź Hello jest toohello podobnie poniższy przykład:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz hello następujących informacji przed przejściem dalej.

  * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4.
  * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.

  Uruchom powitania po tooconfigure przykład Azure publicznej komunikacji równorzędnej dla obwodu

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure publicznej komunikacji równorzędnej szczegóły

Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure publicznej konfiguracji komunikacji równorzędnej

Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład. W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 200 too600.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete Azure publicznej komunikacji równorzędnej

Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft

Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.

> [!IMPORTANT]
> Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy. Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu. Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate komunikacji równorzędnej firmy Microsoft

1. Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.

  Należy zainstalować najnowszą wersję Instalatora programu PowerShell hello z [galerii programu PowerShell](http://www.powershellgallery.com/) i zaimportuj moduły usługi Azure Resource Manager hello do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello. Należy toorun programu PowerShell jako Administrator.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importuj wszystkie moduły AzureRM.* hello w hello znany zakres wersji semantycznej.

  ```powershell
  Import-AzureRM
  ```

  Można także po prostu zaimportować moduł select w obrębie hello znany zakres wersji semantycznej.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Zaloguj się na koncie tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

  Wybierz subskrypcję hello ma toocreate obwodu ExpressRoute.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute.

  Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-arm.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.
3. Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona. Poniższy przykład hello użycia:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  odpowiedź Hello jest toohello podobnie poniższy przykład:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft. Upewnij się, że masz hello następujących informacji, aby kontynuować.

  * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
  * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
  * Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP. Akceptowane są tylko prefiksy publicznych adresów IP. Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listę rozdzielaną przecinkami. Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.
  * **Opcjonalne -** klienta ASN: w przypadku prefiksów reklamy, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer hello można określić jako numer toowhich są zarejestrowani.
  * Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.

   Użyj powitania po komunikacji równorzędnej firmy Microsoft tooconfigure przykład dla obwodu:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>Szczegóły komunikacji równorzędnej tooget firmy Microsoft

Można pobrać szczegółów konfiguracji przy użyciu hello poniższy przykład:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft

Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete komunikacji równorzędnej firmy Microsoft

Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Następne kroki

Następny krok [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-arm.md).

* Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).
* Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).
* Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).
