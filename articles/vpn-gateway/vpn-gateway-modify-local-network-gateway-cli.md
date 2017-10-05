---
title: "Zmodyfikuj prefiksy adresów IP bramy sieci lokalnej i adres IP bramy sieci VPN | Azure | INTERFEJS WIERSZA POLECENIA | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zmiana prefiksów adresów IP dla bramy sieci lokalnej przy użyciu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="b47ff-103">Zmodyfikuj ustawienia bramy sieci lokalnej przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b47ff-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="b47ff-104">Czasami zmienić ustawienia dla bramy sieci lokalnej prefiks adresu lub adres IP bramy.</span><span class="sxs-lookup"><span data-stu-id="b47ff-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="b47ff-105">W tym artykule przedstawiono sposób zmodyfikować ustawienia bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b47ff-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="b47ff-106">Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z poniższej listy:</span><span class="sxs-lookup"><span data-stu-id="b47ff-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b47ff-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b47ff-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="b47ff-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b47ff-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="b47ff-109">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b47ff-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="b47ff-110"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b47ff-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="b47ff-111">Zainstaluj najnowszą wersję polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="b47ff-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="b47ff-112">Aby uzyskać informacje o instalowaniu poleceń interfejsu wiersza polecenia, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b47ff-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="b47ff-113"><a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP</span><span class="sxs-lookup"><span data-stu-id="b47ff-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="b47ff-114"><a name="gwip"></a>Zmodyfikuj adres IP bramy</span><span class="sxs-lookup"><span data-stu-id="b47ff-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b47ff-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b47ff-115">Next steps</span></span>

<span data-ttu-id="b47ff-116">Można sprawdzić połączenie bramy.</span><span class="sxs-lookup"><span data-stu-id="b47ff-116">You can verify your gateway connection.</span></span> <span data-ttu-id="b47ff-117">Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b47ff-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

