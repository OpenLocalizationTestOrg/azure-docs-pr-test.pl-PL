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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="3ef18-103">Zmodyfikuj ustawienia bramy sieci lokalnej za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3ef18-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="3ef18-104">Czasami zmienić ustawienia hello prefiks adresu lub GatewayIPAddress bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3ef18-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="3ef18-105">W tym artykule opisano sposób toomodify ustawienia bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3ef18-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="3ef18-106">Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="3ef18-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ef18-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ef18-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="3ef18-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ef18-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="3ef18-109">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3ef18-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="3ef18-110"><a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP</span><span class="sxs-lookup"><span data-stu-id="3ef18-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="3ef18-111">Po zmodyfikowaniu prefiksów adresów IP hello kroki, które należy wykonać są zależne od tego, czy brama sieci lokalnej ma połączenie.</span><span class="sxs-lookup"><span data-stu-id="3ef18-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="3ef18-112"><a name="gwip"></a>Zmodyfikuj adres IP bramy hello</span><span class="sxs-lookup"><span data-stu-id="3ef18-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="3ef18-113">Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia.</span><span class="sxs-lookup"><span data-stu-id="3ef18-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="3ef18-114">Po zmianie hello publicznego adresu IP hello kroki, które należy wykonać są zależne od tego, czy brama sieci lokalnej ma połączenie.</span><span class="sxs-lookup"><span data-stu-id="3ef18-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3ef18-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ef18-115">Next steps</span></span>

<span data-ttu-id="3ef18-116">Można sprawdzić połączenie bramy.</span><span class="sxs-lookup"><span data-stu-id="3ef18-116">You can verify your gateway connection.</span></span> <span data-ttu-id="3ef18-117">Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3ef18-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>