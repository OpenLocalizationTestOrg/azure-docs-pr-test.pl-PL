---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: środowiska PowerShell: usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-circuit-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-circuit-classic.md)
>

W tym artykule opisano sposób toocreate Azure ExpressRoute obwodu przy użyciu programu PowerShell hello i polecenia cmdlet usługi Azure Resource Manager modelu wdrażania. Ten artykuł zawiera także jak toocheck hello stanu obwodu hello, zaktualizuj lub usuń i anulowanie zastrzeżenia go.

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview).
* Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.


## <a name="create-and-provision-an-expressroute-circuit"></a>Tworzenie i przydzielanie obwodu usługi ExpressRoute
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji
toobegin konfigurację logowania tooyour konto platformy Azure. Użyj hello następujące przykłady toohelp, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
```

Sprawdź subskrypcje hello hello konta:

```powershell
Get-AzureRmSubscription
```

Wybierz subskrypcję hello, która ma toocreate obwodu usługi expressroute dla:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości
Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.

polecenia cmdlet programu PowerShell Hello **Get AzureRmExpressRouteServiceProvider** zwraca informację, która będzie używana w dalszych krokach:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Określ, czy toosee podane jest dostawcą połączenia. Zanotuj hello następujących informacji. Należy go później podczas tworzenia obwodu.

* Nazwa
* PeeringLocations
* BandwidthsOffered

Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)
Jeśli nie masz już grupę zasobów, należy go utworzyć przed utworzeniem obwodu usługi ExpressRoute. Można to zrobić, uruchamiając następujące polecenie hello:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej. Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania. Hello poniżej przedstawiono przykładowe żądanie dla nowego klucza usługi.

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Upewnij się, że określono hello prawidłowe jednostki SKU warstwy i rodzina jednostek SKU:

* Jednostka SKU warstwy określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium. Można określić *standardowe* tooget hello standardowy SKU lub *Premium* dla hello premium dodatku.
* Rodzina jednostek SKU Określa typ rozliczeń hello. Można określić *Metereddata* planu dane naliczane i *Unlimiteddata* planu nieograniczone danych. Można zmienić typu rozliczeń hello z *Metereddata* za*Unlimiteddata*, ale nie można zmienić typu hello z *Unlimiteddata* zbyt*Metereddata* .

> [!IMPORTANT]
> Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute. Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.
> 
> 

odpowiedź Hello zawiera hello klucza usługi. Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Wyświetl listę wszystkich obwody usługi ExpressRoute
tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone, uruchom hello **Get-AzureRmExpressRouteCircuit** polecenia:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureRmExpressRouteCircuit` polecenia cmdlet. Tworzenie hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello. Klucz usługi będzie wyświetlane w hello *bindingTemplate* pola:

```powershell
Get-AzureRmExpressRouteCircuit
```


odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi
*ServiceProviderProvisioningState* zawiera informacje o hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello. Stan zawiera stan hello na powitania po stronie firmy Microsoft. Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.

Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



obwodu Hello ulegnie zmianie po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza
Sprawdzanie stanu hello i stan hello hello obwodu klucza informuje o tym, gdy dostawca jest włączony obwodu. Po skonfigurowaniu obwodu hello *ServiceProviderProvisioningState* pojawia się jako *obsługiwane administracyjnie*, jak pokazano w hello poniższy przykład:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:

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

### <a name="7-create-your-routing-configuration"></a>7. Tworzenie konfiguracji routingu
Aby uzyskać instrukcje krok po kroku, zobacz hello [obwodu ExpressRoute konfiguracji routingu](expressroute-howto-routing-arm.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.

> [!IMPORTANT]
> Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Link sieci wirtualnej tooan obwodu usługi expressroute
Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute. Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](expressroute-howto-linkvnet-arm.md) artykuł podczas pracy z modelu wdrażania usługi Resource Manager hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Pobieranie stanu hello obwodu usługi ExpressRoute
Te informacje w dowolnym momencie można pobrać za pomocą hello **Get-AzureRmExpressRouteCircuit** polecenia cmdlet. Tworzenie hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.

```powershell
Get-AzureRmExpressRouteCircuit
```


odpowiedź Hello będzie toohello podobnie poniższy przykład:

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


Wyświetlane są informacje dotyczące określonego obwodu ExpressRoute, przekazując nazwy grupy zasobów hello i nazwy obwodu jako parametr toohello wywołanie:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


odpowiedź Hello będzie wyglądać podobnie toohello poniższy przykład:

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


Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące polecenie hello:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Modyfikowanie obwodu usługi ExpressRoute
Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.

Możesz zrobić hello po bez przestojów:

* Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.
* Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność. Zmiana wersji na starszą hello przepustowości obwodu nie jest obsługiwane. 
* Zmień hello planu z danych naliczane tooUnlimited danych pomiaru. Zmiana hello pomiaru planu z tooMetered nieograniczone danych, danych nie jest obsługiwane.
* Można włączyć lub wyłączyć *operacje klasycznego*.

Aby uzyskać więcej informacji na limity i ograniczenia, można znaleźć toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>Dodatek tooenable ExpressRoute hello w warstwie premium
Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu, używając powitania po fragment środowiska PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

obwód Hello będzie teraz hello ExpressRoute premium dodatkowe funkcje są włączone. Rozpocznie się rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>Dodatek toodisable ExpressRoute hello w warstwie premium
> [!IMPORTANT]
> Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.
> 
> 

Należy uwzględnić następujące hello:

* Przed zmienią premium toostandard upewnij się, że hello liczba sieci wirtualnych, które są połączone toohello obwód jest mniejsza niż 10. Jeśli tego nie zrobisz, żądanie aktualizacji nie powiedzie się i firma Microsoft będzie naliczać opłaty możesz stawkami premium.
* Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi. Jeśli nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a firma Microsoft będzie naliczać opłaty możesz stawkami premium.
* Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej. Jeśli rozmiar tabeli tras jest większa niż 4000 tras, sesji BGP hello porzuca i nie będzie reenabled, aż przejdzie hello liczby prefiksów anonsowanych poniżej 4000.

Dodatek premium ExpressRoute hello dla istniejącego obwodu hello można wyłączyć za pomocą następującego polecenia cmdlet programu PowerShell hello:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>przepustowości obwodu ExpressRoute hello tooupdate
Dla opcji obsługiwanych przepustowości dla dostawcy, sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md). Można wybrać żadnych rozmiar większy niż rozmiar hello z istniejącym obwodem.

> [!IMPORTANT]
> Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności. Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.
>
> Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń. Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.
> 

Po wybraniu, jaki rozmiar, należy użyć następującego polecenia tooresize hello obwodu:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Obwodu będzie ustalany po stronie firmy Microsoft hello. Następnie należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany. Po wprowadzeniu tego powiadomienia, rozpocznie się możesz rozliczeń dla opcji przepustowości hello zaktualizowane.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Witaj toomove SKU z naliczane toounlimited
Witaj SKU obwodu ExpressRoute można zmienić za pomocą powitania po fragment programu PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>klasycznym toohello dostępu toocontrol i środowisk usługi Resource Manager
Przejrzyj instrukcjami hello [Przenieś obwody usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Anulowania obsługi i usuwania obwodu usługi ExpressRoute
Należy uwzględnić następujące hello:

* Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute. Jeśli ta operacja nie powiedzie się, sprawdź, czy toosee, jeśli wszystkie sieci wirtualne są połączone toohello obwodu.
* Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok. Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.
* Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello. Spowoduje to zatrzymanie rozliczeń dla obwodu hello

Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Następne kroki

Po utworzeniu obwodu, upewnij się, że hello następujące:

* [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute](expressroute-howto-routing-arm.md)
* [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)
