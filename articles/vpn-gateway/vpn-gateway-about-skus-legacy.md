---
title: Brama sieci wirtualnej platformy Azure aaaLegacy jednostki SKU | Dokumentacja firmy Microsoft
description: Stary wirtualnych sieci jednostki SKU bramy.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Praca z bramy sieci wirtualnej jednostki SKU (starszej wersji jednostki SKU)

Ten artykuł zawiera informacje o hello starszej wersji (stare) bramy sieci wirtualnej jednostki SKU. starsza wersja Hello jednostki SKU nadal działa w obu modelach wdrażania dla bram sieci VPN, które zostały już utworzone. Klasycznego bramy sieci VPN kontynuować toouse hello starszej wersji jednostki SKU, zarówno dla bramy istniejących i nowych bram. Podczas tworzenia nowego Menedżera zasobów sieci VPN bramy, użyj nowej bramy hello jednostki SKU. Informacji o hello nowej wersji produktu, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Szacowany łącznej przepływności przez jednostki SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Obsługiwane konfiguracje według typu jednostki SKU i sieci VPN

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Zmień rozmiar bramy (zmienianie jednostka SKU bramy)

Możesz zmienić rozmiar jednostka SKU bramy w ramach hello tej samej rodziny SKU. Na przykład jeśli masz wersji Standard, można zmienić rozmiar tooa wysokowydajnej jednostki SKU. Nie można zmienić rozmiaru sieć VPN bramy między hello starego jednostki SKU i hello nowe rodziny SKU. Na przykład nie można przejść z wersji Standard tooa VpnGw2 jednostki SKU. 

tooresize brama jednostki SKU dla hello klasycznego modelu wdrażania, hello Użyj następującego polecenia:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize brama jednostki SKU dla hello modelu wdrażania usługi Resource Manager, użyj hello następujące polecenie:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Migrowanie toohello nową bramę jednostki SKU

Jeśli pracujesz z modelu wdrażania usługi Resource Manager hello, można migrować toohello nową bramę jednostki SKU. Jeśli pracujesz z hello klasycznego modelu wdrażania, nie można migrować toohello nowe jednostki SKU i zamiast tego należy kontynuować toouse hello starszej wersji jednostki SKU.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat hello nowe jednostki SKU bramy, zobacz [jednostki SKU bramy](vpn-gateway-about-vpngateways.md#gwsku).

Aby uzyskać więcej informacji na temat ustawień konfiguracji, zobacz [o bramy sieci VPN, ustawienia konfiguracji](vpn-gateway-about-vpn-gateway-settings.md).