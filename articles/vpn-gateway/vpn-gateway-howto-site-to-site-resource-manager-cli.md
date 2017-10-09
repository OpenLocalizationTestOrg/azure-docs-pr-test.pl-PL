---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: interfejs wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Ta procedura jest pomocna podczas tworzenia połączenia bramy sieci VPN typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą interfejsu wiersza polecenia."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Tworzenie sieci wirtualnej z wykorzystaniem połączenia sieci VPN typu lokacja-lokacja przy użyciu interfejsu wiersza polecenia

W tym artykule opisano, jak toouse hello Azure CLI toocreate połączenie bramy sieci VPN lokacja-lokacja z toohello sieci Twojej lokalnej sieci wirtualnej. Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:<br>

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Interfejs wiersza polecenia](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP. Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:

* Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go. Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).
* Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.
* Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy. Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej. Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.
* Sprawdź, że zainstalowano najnowszą wersję hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej). Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli) i [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Przykładowe wartości

Można użyć hello następujące wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Połącz tooyour subskrypcji

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Tworzenie grupy zasobów

Witaj poniższy przykład tworzy grupę zasobów o nazwie "TestRG1" w lokalizacji "eastus" hello. Jeśli masz już grupę zasobów w regionie hello mają toocreate sieci wirtualnej, można użyć niż jeden.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Tworzenie sieci wirtualnej

Jeśli nie masz już sieć wirtualną, utwórz ją za pomocą hello [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) polecenia. Podczas tworzenia sieci wirtualnej, upewnij się, że przestrzenie adresowe hello, które określisz nie nakłada przestrzeni adresowych hello wyposażonych w sieci lokalnej.

Witaj poniższy przykład tworzy sieć wirtualną o nazwie "TestVNet1" i podsieć, "Podsieć1".

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Utwórz podsieć bramy hello

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Dla tej konfiguracji potrzebna jest również podsieć bramy. Brama sieci wirtualnej Hello używa podsieć bramy, która zawiera hello adresy IP, które są używane przez usługi bramy sieci VPN hello. Podczas tworzenia podsieci bramy musi ona otrzymać nazwę „GatewaySubnet”. Jeśli zostanie nadana inna nazwa, podsieć zostanie utworzona, ale platforma Azure nie będzie jej traktowała jako podsieci bramy.

rozmiar Hello hello podsieć bramy, który określisz jest zależna od konfiguracji bramy sieci VPN hello, które mają toocreate. Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając /27 lub /28. Przy użyciu większych podsieci bramy umożliwia za mało adresów tooaccommodate możliwe przyszłych konfiguracją IP.

Użyj hello [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create) podsieci bramy hello toocreate polecenia.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Utwórz bramę sieci lokalnej hello

Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej. Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie. Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy. Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej. W przypadku zmiany sieci lokalnej, można łatwo aktualizować hello prefiksy.

Użyj hello następujące wartości:

* Witaj *— adres ip bramy* hello adres IP urządzenia sieci VPN użytkownika lokalnego. Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.
* Witaj *--prefiksy w przypadku adresów lokalnych* są lokalnej przestrzeni adresowych.

Użyj hello [Tworzenie bramy lokalnej sieci az](/cli/azure/network/local-gateway#create) tooadd polecenia bramy sieci lokalnej przy użyciu wielu prefiksy adresów:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Żądanie publicznego adresu IP

Brama sieci VPN musi mieć publiczny adres IP. Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej. adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello. Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP. Nie można zażądać przypisania statycznego publicznego adresu IP. Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN. Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie. Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.

Użyj hello [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create) toorequest polecenia dynamicznego publicznego adresu IP.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Tworzenie bramy sieci VPN hello

Tworzenie bramy sieci VPN hello sieci wirtualnej. Tworzenie bramy sieci VPN może potrwać too45 minut lub więcej toocomplete.

Użyj hello następujące wartości:

* Witaj *— typ bramy* Site-to-Site konfiguracja jest *Vpn*. Typ bramy Hello jest zawsze toohello określonej konfiguracji w przypadku wdrażania. Aby uzyskać więcej informacji, zobacz [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype) (Typy bram).
* Witaj *— sieci vpn typu* może być *RouteBased* (określony tooas dynamiczne bramy w części dokumentacji), lub *PolicyBased* (określony tooas statycznych bramy w niektórych dokumentacja). Ustawienie Hello jest określonych toorequirements hello urządzenia, które są nawiązywane. Aby uzyskać więcej informacji o typach bram sieci VPN, zobacz [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype) (Informacje o ustawieniach konfiguracji bramy sieci VPN).
* Wybierz hello jednostka SKU bramy, które mają toouse. Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji. Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).

Tworzenie bramy sieci VPN hello przy użyciu hello [Tworzenie bramy sieci wirtualnej sieci az](/cli/azure/network/vnet-gateway#create) polecenia. Po uruchomieniu tego polecenia, używając hello parametr — nie - oczekiwania nie widać żadnych opinie i danych wyjściowych. Ten parametr umożliwia toocreate bramy hello w tle hello. Trwa około 45 minut toocreate bramy.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Konfiguracja urządzenia sieci VPN

Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN. W tym kroku konfigurowane jest urządzenie sieci VPN. Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:

- Klucz współużytkowany. Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy podstawowego klucza współużytkowanego. Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.
- Witaj publiczny adres IP bramy sieci wirtualnej. Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia. toofind hello publicznego adresu IP bramy sieci wirtualnej, użyj hello [az sieci ip publicznego listy](/cli/azure/network/public-ip#list) polecenia. Czytelnej, dane wyjściowe hello jest sformatowany toodisplay hello lista publicznych adresów IP w formacie tabeli.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Utwórz połączenie sieci VPN hello

Utwórz połączenie sieci VPN hello lokacja-lokacja między bramą sieci wirtualnej i lokalnego urządzenia sieci VPN. Płatności szczególną uwagę toohello udostępnionego klucza wartość, która musi być zgodna z hello skonfigurowane udostępnionych wartości klucza dla urządzenia sieci VPN.

Utwórz połączenie hello przy użyciu hello [Tworzenie połączenia sieci vpn az sieci](/cli/azure/network/vpn-connection#create) polecenia.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Automatycznie podczas hello zostanie nawiązane połączenie.

## <a name="toverify"></a>10. Sprawdź hello połączenia sieci VPN

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Jeśli chcesz toouse innego tooverify metody połączenia, zobacz [sprawdzić połączenie bramy sieci VPN](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>Maszyna wirtualna tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Typowe zadania

Ta sekcja zawiera typowe polecenia, które są przydatne przy pracy z konfiguracjami lokacja-lokacja. Witaj pełną listę poleceń interfejsu wiersza polecenia sieci, zobacz [wiersza polecenia platformy Azure — sieci](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Następne kroki

* Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).
* Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-forced-tunneling-rm.md).
* Aby uzyskać informacje o połączeniach o wysokiej dostępności typu aktywne-aktywne, zobacz [Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności](vpn-gateway-highlyavailable.md).
* Aby zapoznać się z listą poleceń interfejsu wiersza polecenia platformy Azure dotyczących sieci, zobacz [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/network).