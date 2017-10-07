---
title: "Połącz lokacji toomultiple sieci wirtualnej przy użyciu bramy sieci VPN i programu PowerShell: klasycznym | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomoże łączenia wielu lokalnych witryn tooa wirtualnej sieci lokalnej dla hello klasycznego modelu wdrażania przy użyciu bramy sieci VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Dodaj tooa połączenia lokacja-lokacja sieci wirtualnej z istniejącego połączenia bramy sieci VPN (klasyczne)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klasyczny)](vpn-gateway-multi-site.md)
>
>

W tym artykule przedstawiono przy użyciu programu PowerShell tooadd lokacja-lokacja (S2S) połączeń tooa bramy sieci VPN z istniejącego połączenia. Ten typ połączenia jest często tooas określonej konfiguracji "obejmujący wiele lokacji". Hello czynności w tym artykule dotyczą sieci toovirtual utworzone za pomocą hello klasycznego modelu wdrażania (znanej także jako Service Management). Te kroki należy stosować konfiguracje połączenia ważnych tooExpressRoute/lokacja-lokacja.

### <a name="deployment-models-and-methods"></a>Modele i metody wdrażania

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Modyfikacjom w tej tabeli jako artykułów i dodatkowe narzędzia staną się dostępne dla tej konfiguracji. Artykuł jest dostępny, możemy połączyć bezpośrednio tooit z tej tabeli.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>O łączeniu

Można połączyć wiele lokalnej lokacji tooa jednej sieci wirtualnej. Jest to szczególnie atrakcyjne tworzenie hybrydowych rozwiązań w chmurze. Tworzenie bramy sieci wirtualnej platformy Azure tooyour połączenia z wieloma lokacjami jest podobne toocreating innych połączeń lokacja-lokacja. W rzeczywistości, można użyć istniejącej bramy sieci VPN platformy Azure, tak długo, jak bramy hello jest dynamiczny (opartej na trasach).

Jeśli masz już statycznych bramy sieci wirtualnej podłączonej tooyour, można zmienić bez konieczności w kolejności tooaccommodate obejmujący wiele lokacji sieci wirtualnej hello toorebuild toodynamic typu bramy hello. Przed zmianą typu routingu hello, upewnij się, że bramy sieci VPN, lokalnymi obsługuje konfiguracje sieci VPN opartej na trasach.

![diagram obejmujący wiele lokacji](./media/vpn-gateway-multi-site/multisite.png "obejmujący wiele lokacji")

## <a name="points-tooconsider"></a>Punkty tooconsider

**Nie będzie możliwe toouse hello portalu toomake zmiany toothis wirtualnej sieci.** Należy toomake pliku konfiguracji sieci toohello zmiany zamiast hello portalu. Jeśli wprowadzisz zmiany w portalu hello zastępują ustawienia odwołania obejmujący wiele lokacji w tej sieci wirtualnej.

Chcesz powinno ujawnić przy użyciu pliku konfiguracji sieci hello czasu hello przeprowadzisz hello procedury obejmujący wiele lokacji. Jednak jeśli masz wiele osób pracuje w konfiguracji sieci, należy toomake się, że wszyscy zna tego ograniczenia. To nie oznacza, że nie możesz użyć portalu hello na wszystkich. Można go dla wszystkich innych urządzeń, z wyjątkiem wprowadzania konfiguracji zmiany toothis konkretnej wirtualnej sieci.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem konfigurowania należy sprawdzić, czy następujące hello:

* Zgodny sprzęt sieci VPN dla każdej lokalizacji lokalnej. Sprawdź [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md) tooverify Jeśli hello urządzenia, które mają toouse czegoś znanego toobe zgodne.
* Zewnętrznie połączonej publiczny adres IPv4 dla każdego urządzenia sieci VPN. adres IP Hello nie może znajdować się za urządzeniem NAT To wymaganie.
* Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell. Upewnij się, że hello wersji usługi zarządzania (SM) w wersji Menedżera zasobów toohello dodanie. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.
* Osoby, która jest wykorzystać Konfigurowanie sprzętu sieci VPN. Będziesz mieć toohave silne znajomością działania tooconfigure urządzenia sieci VPN lub pracy z osobą, która jest.
* zakresy adresów IP Hello mają toouse dla sieci wirtualnej (jeśli jeszcze nie utworzono jeden).
* Witaj zakresów adresów IP dla każdej lokacji sieci lokalnej hello, które będą łączyć się z. Należy się upewnić, że hello zakresy adresów IP każdego hello lokacji sieci lokalnej, które mają toodo tooconnect nie nakładają się na siebie toomake. W przeciwnym razie konfiguracji hello przekazywanych spowoduje odrzucenie portalu hello lub hello interfejsu API REST.<br>Na przykład jeśli masz dwie lokacje sieci lokalnej, czy zawierają 10.2.3.0/24 zakres adresów IP hello i czy masz pakiet o docelowy adres 10.2.3.3 Azure nie wiedzieć lokacji, do której ma się zakresów adresów hello toobecause toosend hello pakietu nakładające się. problemy z routingu tooprevent Azure nie zezwala tooupload pliku konfiguracji, który ma nakładające się zakresy.

## <a name="1-create-a-site-to-site-vpn"></a>1. Tworzenie sieci VPN typu lokacja-lokacja
Jeśli masz już sieć VPN lokacja-lokacja z bramą routingu dynamicznego ponosić! Możesz przejść za[Eksportuj ustawienia konfiguracji sieci wirtualnej hello](#export). Jeśli nie, hello następujące:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Jeśli masz już sieć wirtualną do lokacji, ale nie statyczne bramy routingu (na podstawie zasad):
1. Zmień Twoje bramy typu toodynamic routingu. Obejmujący wiele lokacji sieci VPN wymaga dynamicznej bramy routingu (znanej także jako opartej na trasach). Typ bramy toochange, użytkownik będzie toofirst delete hello istniejącą bramę, a następnie utwórz nową. Aby uzyskać instrukcje, zobacz [jak toochange hello routingu typ sieci VPN dla bramy](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Konfigurowanie nowej bramy i utworzyć tunel sieci VPN. Aby uzyskać instrukcje, zobacz [Brama sieci VPN w hello klasycznego portalu Azure](vpn-gateway-configure-vpn-gateway-mp.md). Najpierw zmień Twoje bramy typu toodynamic routingu.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Jeśli nie masz lokacja-lokacja sieci wirtualnej:
1. Tworzenie sieci wirtualnej lokacja-lokacja, korzystając z tych instrukcji: [tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja-lokacja w hello klasycznego portalu Azure](vpn-gateway-site-to-site-create.md).  
2. Należy skonfigurować bramę routingu dynamicznego przy użyciu tych instrukcji: [Brama sieci VPN](vpn-gateway-configure-vpn-gateway-mp.md). Należy się tooselect **routingu dynamicznego** dla danego typu bramy.

## <a name="export"></a>2. Plik konfiguracji sieci hello eksportu
Wyeksportuj do pliku konfiguracji sieci platformy Azure, uruchamiając następujące polecenie hello. Możesz zmienić lokalizację hello hello pliku tooexport tooa różnych lokalizacji, w razie potrzeby.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Plik konfiguracji sieci Otwórz hello
Otwórz plik konfiguracji sieci hello, który został pobrany w ostatnim kroku hello. Użyj dowolnego edytora xml, który chcesz. Plik Hello powinien wyglądać podobnie toohello następujące:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Dodawanie odwołania do wielu lokacji
Po dodaniu lub usunięciu informacji o lokacji odniesienia, będzie wprowadzać zmian konfiguracji toohello ConnectionsToLocalNetwork/elementu LocalNetworkSiteRef. Dodawanie nowego odwołania do lokacji lokalnej wyzwala Azure toocreate nowe tunelu. W poniższym przykładzie hello konfiguracja sieci hello jest połączenia pojedynczej lokacji. Zapisz plik hello, po zakończeniu wprowadzania zmian.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd dodatkowe odsyłacze do witryn (Tworzenie konfiguracji wielu lokacji), po prostu dodaj dodatkowe "elementu LocalNetworkSiteRef" wierszy, jak pokazano w poniższym przykładzie hello:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Plik konfiguracji sieci hello importu
Importowanie pliku konfiguracji sieci hello. Podczas importowania tego pliku ze zmianami hello hello nowych tuneli zostaną dodane. tunele Hello użyje hello bramy dynamiczne utworzony wcześniej. Możesz użyć hello klasycznego portalu lub plik hello tooimport programu PowerShell.

## <a name="6-download-keys"></a>6. Pobierz kluczy
Po dodaniu Twoje nowe tuneli klawisze hello PowerShell polecenia cmdlet "Get-AzureVNetGatewayKey" tooget hello IPsec i IKE wstępnego dla każdego tunelu.

Na przykład:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Jeśli wolisz, możesz również użyć hello *uzyskać wirtualnych sieci bramy klucz wstępny* tooget interfejsu API REST hello kluczy wstępnych.

## <a name="7-verify-your-connections"></a>7. Sprawdź połączenia
Sprawdź stan tunelu obejmujący wiele lokacji hello. Po pobraniu hello kluczy dla każdego tunelu, należy tooverify połączenia. Użyj tooget "Get-AzureVnetConnection" tuneli listę sieci wirtualnej, jak pokazano w poniższym przykładzie hello. VNet1 jest nazwa hello hello sieci wirtualnej.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Przykład zwrotu:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat bram sieci VPN, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).
