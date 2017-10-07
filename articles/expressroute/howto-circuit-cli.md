---
title: "Tworzenie i modyfikowanie obwodu usługi Azure ExpressRoute: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia


W tym artykule opisano, jak toocreate obwodu Azure ExpressRoute przy użyciu hello interfejsu wiersza polecenia (CLI). Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu. Jeśli chcesz toouse toowork inną metodę z obwody usługi ExpressRoute, można wybrać artykuł hello z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-circuit-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Przed rozpoczęciem

* Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej). Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli) i [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.

## <a name="create-and-provision-an-expressroute-circuit"></a>Tworzenie i przydzielanie obwodu usługi ExpressRoute

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji

toobegin konfigurację logowania tooyour konto platformy Azure. Użyj hello następujące przykłady toohelp, gdy nawiązujesz połączenie:

```azurecli
az login
```

Sprawdź subskrypcje hello hello konta.

```azurecli
az account list
```

Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu usługi ExpressRoute.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości

Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości. Hello interfejsu wiersza polecenia polecenie "az sieci express route listy--usługodawców" zwraca informację, która będzie używana w dalszych krokach:

```azurecli
az network express-route list-service-providers
```

odpowiedź Hello jest toohello podobnie poniższy przykład:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Sprawdź hello toosee odpowiedzi, jeśli znajduje się dostawcą połączenia. Zanotuj następujące informacje, które należy podczas tworzenia obwód hello:

* Nazwa
* PeeringLocations
* BandwidthsOffered

Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.

### <a name="3-create-an-expressroute-circuit"></a>3. Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)

> [!IMPORTANT]
> Jest on rozliczany od momentu hello wygenerowaniu klucza usługi obwodu usługi ExpressRoute. Tę operację należy wykonać, gdy dostawca łączności hello jest gotowy tooprovision hello obwodu.
> 
> 

Jeśli nie masz już grupę zasobów, należy go utworzyć przed utworzeniem obwodu usługi ExpressRoute. Można utworzyć grupę zasobów, uruchamiając następujące polecenie hello:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej. Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania. 

Upewnij się, że określono hello prawidłowe jednostki SKU warstwy i rodzina jednostek SKU:

* Jednostka SKU warstwy określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium. Można określić "Standardowy" hello tooget standardowy SKU lub "Premium" dla hello premium dodatku.
* Rodzina jednostek SKU Określa typ rozliczeń hello. "Metereddata" można określić dla planu dane naliczane i "Unlimiteddata" planu dane nieograniczone. Można zmienić typu rozliczeń hello z "Metereddata"too'Unlimiteddata", ale nie można zmienić typu hello z too'Metereddata"Unlimiteddata"".


Jest on rozliczany od momentu hello wygenerowaniu klucza usługi obwodu usługi ExpressRoute. Poniższy przykład Hello jest żądaniem klucza usługi:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

odpowiedź Hello zawiera hello klucza usługi.

### <a name="4-list-all-expressroute-circuits"></a>4. Wyświetl listę wszystkich obwody usługi ExpressRoute

tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone, uruchom polecenie "Lista express route sieci az" hello. Te informacje w dowolnym momencie można pobrać za pomocą tego polecenia. toolist wszystkich obwodów należy hello wywołania bez parametrów.

```azurecli
az network express-route list
```

Klucz usługi ma na liście hello *bindingTemplate* pole hello odpowiedzi.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Aby uzyskać szczegółowy opis wszystkich parametrów hello, uruchomione polecenie hello przy użyciu hello "-h" parametru.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi

"ServiceProviderProvisioningState" zawiera informacje o hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello. Stan Hello zawiera stan hello na powitania po stronie firmy Microsoft. Aby uzyskać więcej informacji, zobacz hello [artykułu przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Podczas tworzenia nowego obwodu ExpressRoute obwodu hello jest powitania po stanu:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

następujące stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello zmiany obwodu Hello:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza

Sprawdzanie stanu hello i stan hello hello obwodu klucza informuje o tym, gdy dostawca jest włączony obwodu. Po skonfigurowaniu obwodu hello "ServiceProviderProvisioningState" pojawia się jako "Obsługiwane administracyjnie", jak pokazano w hello poniższy przykład:

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

odpowiedź Hello jest toohello podobnie poniższy przykład:

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Tworzenie konfiguracji routingu

Aby uzyskać instrukcje krok po kroku, zobacz hello [obwodu ExpressRoute konfiguracji routingu](howto-routing-cli.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.

> [!IMPORTANT]
> Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia konfiguruje i zarządza nimi routingu dla Ciebie.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Link sieci wirtualnej tooan obwodu usługi expressroute

Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute. Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](howto-linkvnet-cli.md) artykułu.

## <a name="modify"></a>Modyfikowanie obwodu usługi ExpressRoute

Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność. Możesz wprowadzić następujące zmiany bez przestojów hello:

* Można włączyć lub wyłączyć dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.
* Można zwiększyć hello przepustowości obwodu ExpressRoute, pod warunkiem na porcie hello jest dostępna pojemność. Jednak hello przepustowości obwodu zmiana wersji na starszą nie jest obsługiwane. 
* Można zmienić planu zliczania hello naliczane danych tooUnlimited danych. Jednak zmiana hello pomiaru planu z tooMetered nieograniczone danych, danych nie jest obsługiwane.
* Można włączyć lub wyłączyć *operacje klasycznego*.

Aby uzyskać więcej informacji na limity i ograniczenia, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>Dodatek tooenable ExpressRoute hello w warstwie premium

Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu za pomocą następującego polecenia hello:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

obwód Hello ma teraz włączone hello ExpressRoute premium dodatkowe funkcje. Zaczniemy rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>Dodatek toodisable ExpressRoute hello w warstwie premium

> [!IMPORTANT]
> Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.
> 
> 

Przed wyłączeniem hello dodatek usługi ExpressRoute w warstwie premium, zrozumieć hello następujące kryteria:

* Przed zmienią premium toostandard użytkownik musi upewnić się, że masz mniej niż 10 obwodu toohello połączone sieci wirtualne. Jeśli masz więcej niż 10 żądania aktualizacji zakończy się niepowodzeniem, a nas rachunku stawkami premium.
* Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi. Jeśli nie można odłączyć wszystkie sieci wirtualne, żądanie aktualizacji nie powiedzie się i NAS rachunku stawkami premium.
* Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej. Jeśli rozmiar tabeli tras jest większa niż 4000 tras, porzuca hello sesji BGP. Hello sesji nie reenabled, dopóki nie zostanie hello liczby prefiksów anonsowanych poniżej 4000.

Dodatek premium ExpressRoute hello dla istniejącego obwodu hello można wyłączyć za pomocą hello poniższy przykład:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>przepustowości obwodu ExpressRoute hello tooupdate

Dla opcji przepustowości hello obsługiwane dla dostawcy, sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md). Można wybrać żadnych rozmiar większy niż rozmiar hello z istniejącym obwodem.

> [!IMPORTANT]
> Jeśli na powitania istniejącego portu jest nieodpowiedni pojemności, może być obwodu ExpressRoute hello toorecreate. Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.
>
> Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń. Zmiany na starszą wersję przepustowości wymaga możesz toodeprovision hello obwodu usługi expressroute, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.
>

Po wybraniu rozmiar hello, należy użyć następującego polecenia tooresize hello obwodu:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Obwodu jest o rozmiarze po stronie firmy Microsoft hello. Następnie należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany. Po wprowadzeniu tego powiadomienia, możemy rozpocząć rozliczeń można opcji przepustowości hello zaktualizowane.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Witaj toomove SKU z naliczane toounlimited

Witaj SKU obwodu ExpressRoute można zmienić za pomocą hello poniższy przykład:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>klasycznym toohello dostępu toocontrol i środowisk usługi Resource Manager

Przejrzyj instrukcjami hello [Przenieś obwody usługi ExpressRoute z modelu wdrażania Menedżera zasobów klasycznych toohello hello](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Anulowania obsługi i usuwania obwodu usługi ExpressRoute

toodeprovision i delete obwodu usługi ExpressRoute, upewnij się, że rozumiesz hello następujące kryteria:

* Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute. Jeśli ta operacja nie powiedzie się, sprawdź, czy toosee, jeśli wszystkie sieci wirtualne są połączone toohello obwodu.
* Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie**, należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok. Firma Microsoft może nadal tooreserve zasobów, a następnie obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.
* Dostawcy usług hello została anulowana obwodu hello można usunąć obwodu hello. Gdy obwód jest anulowana, dostawcy usług hello stan inicjowania obsługi jest ustawiany za**nieudostępniane**. Powoduje to zatrzymanie rozliczeń dla hello obwodu.

Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Następne kroki

Po utworzeniu obwodu, upewnij się, że hello następujących zadań:

* [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute](howto-routing-cli.md)
* [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute](howto-linkvnet-cli.md)
