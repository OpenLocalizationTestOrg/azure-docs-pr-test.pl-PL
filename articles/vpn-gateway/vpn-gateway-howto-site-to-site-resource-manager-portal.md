---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: Portal | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Te kroki pomoże utworzyć przy użyciu portalu hello połączenie bramy sieci VPN typu lokacja-lokacja między lokalizacjami."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Utwórz połączenie lokacja-lokacja w hello portalu Azure

W tym artykule opisano, jak toouse hello Azure toocreate portalu połączenie bramy sieci VPN lokacja-lokacja z toohello sieci Twojej lokalnej sieci wirtualnej. Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Interfejs wiersza polecenia](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP. Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:

* Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go. Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).
* Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.
* Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy. Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej. Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do. 

### <a name="values"></a>Przykładowe wartości

Przykłady Hello w tym artykule Użyj hello następujące wartości. Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.

* **Nazwa sieci wirtualnej:** TestVNet1
* **Przestrzeń adresowa:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcjonalnie na potrzeby tego ćwiczenia)
* **Podsieci:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcjonalnie na potrzeby tego ćwiczenia)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupa zasobów:** TestRG1
* **Lokalizacja:** Wschodnie stany USA
* **Serwer DNS:** opcjonalnie. Witaj adres IP serwera DNS.
* **Nazwa bramy sieci wirtualnej:** VNet1GW
* **Publiczny adres IP:** VNet1GWIP
* **Typ sieci VPN:** oparta na trasach
* **Typ połączenia:** lokacja-lokacja (IPsec)
* **Typ bramy:** VPN
* **Nazwa bramy sieci lokalnej:** Site2
* **Nazwa połączenia:** VNet1toSite2

## <a name="CreatVNet"></a>1. Tworzenie sieci wirtualnej

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Określanie serwera DNS

DNS nie jest wymagane toocreate Site-to-Site połączenia. Jednak jeśli chcesz toohave rozpoznawania nazw zasobów, które są wdrożone tooyour sieci wirtualnej, należy określić serwer DNS. To ustawienie umożliwia określenie serwera DNS hello mają toouse do rozpoznawania nazw dla tej sieci wirtualnej. Nie powoduje ono jednak utworzenia serwera DNS. Aby uzyskać więcej informacji na temat rozpoznawania nazw, zobacz artykuł [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Rozpoznawanie nazw dla maszyn wirtualnych i wystąpień roli)

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Utwórz podsieć bramy hello

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Tworzenie bramy sieci VPN hello

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Utwórz bramę sieci lokalnej hello

Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej. Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie. Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy. Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej. Jeśli zmiany sieci lokalnej lub publicznego adresu IP toochange hello hello urządzenia sieci VPN, należy można łatwo aktualizować wartości hello później.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Konfiguracja urządzenia sieci VPN

Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN. W tym kroku konfigurowane jest urządzenie sieci VPN. Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:

- Klucz współużytkowany. Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy podstawowego klucza współużytkowanego. Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.
- Witaj publiczny adres IP bramy sieci wirtualnej. Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia. toofind hello publiczny adres IP bramy sieci VPN przy użyciu hello portalu Azure Przejdź zbyt**bramy sieci wirtualnej**, następnie kliknij nazwę hello bramy.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Utwórz połączenie sieci VPN hello

Utwórz połączenie sieci VPN hello lokacja-lokacja między bramą sieci wirtualnej i lokalnego urządzenia sieci VPN.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Sprawdź hello połączenia sieci VPN

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>Maszyna wirtualna tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Jak tooreset bramy sieci VPN

Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja. W takiej sytuacji lokalnego urządzenia sieci VPN są wszystkie działa poprawnie, ale są nie jest w stanie tooestablish tuneli protokołu IPsec o hello bram sieci VPN platformy Azure. Aby uzyskać instrukcje, zobacz [Resetowanie bramy VPN Gateway](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Jak toochange bramy jednostki SKU (zmiany rozmiaru bramy)

Aby hello kroki toochange jednostka SKU bramy, zobacz [jednostki SKU bramy](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Następne kroki

* Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-forced-tunneling-rm.md).
* Aby uzyskać informacje o połączeniach o wysokiej dostępności typu aktywne-aktywne, zobacz [Połączenia obejmujące wiele lokalizacji i połączenia między sieciami wirtualnymi o wysokiej dostępności](vpn-gateway-highlyavailable.md).
