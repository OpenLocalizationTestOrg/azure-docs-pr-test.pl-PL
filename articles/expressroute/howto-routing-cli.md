---
title: "Jak tooconfigure routingu dla obwodu usługi Azure ExpressRoute: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Ten artykuł ułatwia tworzenie i przydzielanie hello prywatne, publiczna i obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute, przy użyciu interfejsu wiersza polecenia

W tym artykule opisano tworzenie i zarządzanie nimi konfiguracji routingu dla obwodu usługi ExpressRoute w modelu wdrażania usługi Resource Manager hello przy użyciu interfejsu wiersza polecenia. Można również sprawdzić stan hello, update lub delete i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute. Jeśli chcesz toouse toowork inną metodę z obwodu wybierz artykułu z hello następującej listy:

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

* Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej). Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).
* Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływu pracy](expressroute-workflows.md) strony przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](howto-circuit-cli.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować. Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie toobe toorun stanie hello poleceń w tym artykule.

Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IPVPN, takich jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.

Można skonfigurować jedną, dwie lub wszystkich trzech komunikacji równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) dla obwodu usługi ExpressRoute. Możesz skonfigurować komunikację równorzędną w dowolnej kolejności. Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.

## <a name="azure-private-peering"></a>Prywatna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate Azure prywatnej komunikacji równorzędnej

1. Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure. Należy użyć najnowszej wersji hello hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.

  ```azurecli
  az login
  ```

  Wybierz hello subskrypcję toocreate obwodu ExpressRoute

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute. Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.
3. Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona. Poniższy przykład hello użycia:

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:

  * / 30 podsieci dla linku podstawowego hello. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * / 30 podsieci hello dodatkowej łącza. Hello podsieci nie może być częścią żadnych przestrzeni adresowej zarezerwowane dla sieci wirtualnych.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS. Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej. Pamiętaj, aby nie używać numeru 65515.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.

  Użyj powitania po tooconfigure przykład prywatnej komunikacji równorzędnej dla obwodu usługi Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure prywatnej komunikacji równorzędnej szczegóły

Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure

Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład. W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete Azure prywatnej komunikacji równorzędnej

Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:

> [!WARNING]
> Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu ExpressRoute przed uruchomieniem w tym przykładzie. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Publiczna komunikacja równorzędna Azure

Ta sekcja pomoże Ci tworzenie, pobrać, aktualizowanie i usuwanie hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate Azure publicznej komunikacji równorzędnej

1. Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure. Należy użyć najnowszej wersji hello hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.

  ```azurecli
  az login
  ```

  Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute.  Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, mogą żądać, czy dostawca połączenia umożliwia prywatnej komunikacji równorzędnej platformy Azure dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.
3. Sprawdź tooensure obwodu ExpressRoute hello jest udostępniane i włączona. Poniższy przykład hello użycia:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla hello obwodu. Upewnij się, że masz hello następujących informacji przed przejściem dalej.

  * / 30 podsieci dla linku podstawowego hello. Musi to być prawidłowy publiczny prefiks IPv4.
  * / 30 podsieci hello dodatkowej łącza. Musi to być prawidłowy publiczny prefiks IPv4.
  * Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej. Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.
  * Numer AS do komunikacji równorzędnej. Możesz używać 2-bajtowych i 4-bajtowych numerów AS.
  * **Opcjonalne -** skrótu MD5 po wybraniu toouse jeden.

  Uruchom powitania po tooconfigure przykład publicznej komunikacji równorzędnej dla obwodu usługi Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Jeśli wybierzesz toouse skrótu MD5, użyj hello poniższy przykład:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.

### <a name="tooview-azure-public-peering-details"></a>tooview Azure publicznej komunikacji równorzędnej szczegóły

Można pobrać szczegółów konfiguracji przy użyciu hello poniższy przykład:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure publicznej konfiguracji komunikacji równorzędnej

Można aktualizować dowolną część konfiguracji hello przy użyciu hello poniższy przykład. W tym przykładzie hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 200 too600.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete Azure publicznej komunikacji równorzędnej

Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft

Ta sekcja pomoże Ci tworzenie, get, aktualizowanie i usuwanie hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.

> [!IMPORTANT]
> Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane przez hello komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy. Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu. Aby uzyskać więcej informacji, zobacz [skonfigurować filtr trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate komunikacji równorzędnej firmy Microsoft

1. Zainstaluj najnowszą wersję hello wiersza polecenia platformy Azure. Użyj hello najnowszą wersję hello Azure interfejsu wiersza polecenia (CLI). * hello przeglądu [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.

  ```azurecli
  az login
  ```

  Wybierz subskrypcję hello, dla której ma zostać toocreate obwodu ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Utwórz obwód usługi ExpressRoute. Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](howto-circuit-cli.md) i udostępniane przez dostawcę łączności hello.

  Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie. W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello. Dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, nadal konfigurację za pomocą hello następnych kroków.

3. Sprawdź toomake obwodu ExpressRoute hello się, że jest udostępniane i włączona. Poniższy przykład hello użycia:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
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

   Uruchom powitania po komunikacji równorzędnej firmy Microsoft tooconfigure przykład dla obwodu:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>Szczegóły komunikacji równorzędnej tooget firmy Microsoft

Szczegóły konfiguracji można uzyskać za pomocą hello poniższy przykład:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft

Można aktualizować dowolną część konfiguracji hello. Witaj anonsowany prefiksy obwodu hello są aktualizowane z too124.1.0.0/24 123.1.0.0/24 w hello poniższy przykład:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete komunikacji równorzędnej firmy Microsoft

Należy usunąć konfigurację komunikacji równorzędnej, uruchamiając hello poniższy przykład:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Następne kroki

Następny krok [połączyć sieć wirtualną tooan obwodu ExpressRoute](howto-linkvnet-cli.md).

* Więcej informacji na temat przepływów pracy usługi ExpressRoute znajduje się w artykule [ExpressRoute workflows](expressroute-workflows.md) (Przepływy pracy usługi ExpressRoute).
* Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).
* Więcej informacji na temat pracy z sieciami wirtualnymi znajduje się w artykule [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Omówienie sieci wirtualnych).