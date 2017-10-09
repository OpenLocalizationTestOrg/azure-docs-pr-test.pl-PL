---
title: bramy sieci wirtualnej ExpressRoute aaaAbout | Dokumentacja firmy Microsoft
description: "Informacje na temat bram sieci wirtualnej dla usługi ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a>Informacje o bramach sieci wirtualnej dla usługi ExpressRoute
Brama sieci wirtualnej służy toosend ruchu sieciowego między sieciami wirtualnymi platformy Azure i lokalizacji lokalnej. Po skonfigurowaniu połączenia ExpressRoute, należy utworzyć i skonfigurować bramę sieci wirtualnej i połączenia bramy sieci wirtualnej.

Podczas tworzenia bramy sieci wirtualnej należy określić kilka ustawień. Jedno z ustawień wymaganych hello Określa, czy brama hello będzie używana dla ruchu ExpressRoute i sieci VPN typu lokacja-lokacja. W modelu wdrażania usługi Resource Manager hello jest hello ustawienie "-elementu GatewayType".

Po ruch sieciowy będzie przesyłany w połączeniu sieci prywatnej, należy użyć typu bramy hello "ExpressRoute". Dotyczy to również określonego tooas bramę usługi ExpressRoute. Gdy ruch sieciowy będzie przesyłany zaszyfrowanych przez hello publicznej sieci Internet, użyj typu bramy hello "Vpn". Jest to tooas określonej bramy sieci VPN. Wszystkie połączenia typu lokacja-lokacja, punkt-lokacja i połączenia między sieciami wirtualnymi używają bramy sieci VPN.

Każda sieć wirtualna może mieć tylko jedną bramę sieci wirtualnej na typ bramy. Na przykład można mieć jedną bramę sieci wirtualnej, która używa klasy -GatewayType Vpn, oraz jednej, która używa klasy -GatewayType ExpressRoute. Ten artykuł skupia się na bramę sieci wirtualnej hello ExpressRoute.

## <a name="gwsku"></a>Jednostki SKU bramy
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Jeśli chcesz tooupgrade Twojego tooa bramy bardziej zaawansowanych bramy jednostka SKU, w większości przypadków, w których można używać hello polecenia cmdlet programu PowerShell "Zmiany rozmiaru AzureRmVirtualNetworkGateway". To będzie działać dla uaktualnienia tooStandard i wysokowydajnej jednostki SKU. Jednak toohello tooupgrade UltraPerformance SKU, konieczne będzie toorecreate hello bramy.

### <a name="aggthroughput"></a>Szacowany łącznej przepływności według jednostka SKU bramy
Witaj poniższej tabeli przedstawiono typy bramy hello i hello szacowany łącznej przepływności. Ta tabela odnosi się hello tooboth Resource Manager i klasycznych modeli wdrażania.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Przepływność aplikacji zależy od wielu czynników, takich jak czas oczekiwania na trasie hello, i hello liczba ruch przepływa zostanie otwarta aplikacja hello. numery Hello hello tabeli reprezentują hello górny limit aplikacji hello mogących theorectically osiągnięcia w środowisku idealne. 
> 
>

## <a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST
Aby uzyskać dodatkowe zasoby techniczne i wymagania określonej składni, korzystając z polecenia cmdlet programu PowerShell i interfejsów API REST konfiguracji bramy sieci wirtualnej Zobacz hello następujące strony:

| **Wdrożenie klasyczne** | **Resource Manager** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [Interfejs API REST](https://msdn.microsoft.com/library/jj154113.aspx) |[Interfejs API REST](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Następne kroki
Zobacz [omówienie ExpressRoute](expressroute-introduction.md) Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń. 

