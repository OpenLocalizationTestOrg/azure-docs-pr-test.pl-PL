---
title: "Zmodyfikuj prefiksy adresów IP bramy sieci lokalnej hello i adres IP bramy sieci VPN hello | Azure | INTERFEJS WIERSZA POLECENIA | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zmiana prefiksów adresów IP dla bramy sieci lokalnej za pomocą hello wiersza polecenia platformy Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a>Zmodyfikuj ustawienia bramy sieci lokalnej za pomocą hello wiersza polecenia platformy Azure

Czasami zmienić ustawienia hello prefiks adresu bramy sieci lokalnej lub adres IP bramy. W tym artykule opisano sposób toomodify ustawienia bramy sieci lokalnej. Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Przed rozpoczęciem

Zainstaluj najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej). Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <a name="gwip"></a>Zmodyfikuj adres IP bramy hello

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a>Następne kroki

Można sprawdzić połączenie bramy. Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).

