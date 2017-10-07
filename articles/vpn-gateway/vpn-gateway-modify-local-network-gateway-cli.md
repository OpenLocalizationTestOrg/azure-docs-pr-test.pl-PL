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
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="bd1a0-103">Zmodyfikuj ustawienia bramy sieci lokalnej za pomocą hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bd1a0-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="bd1a0-104">Czasami zmienić ustawienia hello prefiks adresu bramy sieci lokalnej lub adres IP bramy.</span><span class="sxs-lookup"><span data-stu-id="bd1a0-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="bd1a0-105">W tym artykule opisano sposób toomodify ustawienia bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="bd1a0-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="bd1a0-106">Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="bd1a0-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd1a0-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd1a0-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="bd1a0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd1a0-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="bd1a0-109">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bd1a0-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="bd1a0-110"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="bd1a0-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="bd1a0-111">Zainstaluj najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="bd1a0-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="bd1a0-112">Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd1a0-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="bd1a0-113"><a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP</span><span class="sxs-lookup"><span data-stu-id="bd1a0-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="bd1a0-114"><a name="gwip"></a>Zmodyfikuj adres IP bramy hello</span><span class="sxs-lookup"><span data-stu-id="bd1a0-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bd1a0-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd1a0-115">Next steps</span></span>

<span data-ttu-id="bd1a0-116">Można sprawdzić połączenie bramy.</span><span class="sxs-lookup"><span data-stu-id="bd1a0-116">You can verify your gateway connection.</span></span> <span data-ttu-id="bd1a0-117">Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bd1a0-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

