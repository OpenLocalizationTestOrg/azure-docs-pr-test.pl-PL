---
title: "Zmodyfikuj prefiksy adresów IP bramy sieci lokalnej hello i adres IP bramy sieci VPN hello | Azure | Portal | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zmiana prefiksów adresów IP dla bramy sieci lokalnej za pomocą hello portalu Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Zmodyfikuj ustawienia bramy sieci lokalnej za pomocą hello portalu Azure

Czasami zmienić ustawienia hello prefiks adresu lub GatewayIPAddress bramy sieci lokalnej. W tym artykule opisano sposób toomodify ustawienia bramy sieci lokalnej. Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP

Po zmodyfikowaniu prefiksów adresów IP hello kroki, które należy wykonać są zależne od tego, czy brama sieci lokalnej ma połączenie.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Zmodyfikuj adres IP bramy hello

Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia. Po zmianie hello publicznego adresu IP hello kroki, które należy wykonać są zależne od tego, czy brama sieci lokalnej ma połączenie.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Następne kroki

Można sprawdzić połączenie bramy. Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).