---
title: "Zmodyfikuj prefiksy adresów IP bramy sieci lokalnej hello i adres IP bramy sieci VPN hello | Azure | PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zmiana prefiksów adresów IP dla bramy sieci lokalnej za pomocą programu PowerShell"
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
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="32028-103">Modyfikowanie ustawień lokalnej bramy sieci przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="32028-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="32028-104">Czasami zmienić ustawienia hello prefiks adresu lub GatewayIPAddress bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="32028-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="32028-105">W tym artykule opisano sposób toomodify ustawienia bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="32028-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="32028-106">Można również zmodyfikować te ustawienia przy użyciu innej metody, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="32028-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="32028-107">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="32028-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="32028-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32028-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="32028-109">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="32028-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="32028-110"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="32028-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="32028-111">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32028-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="32028-112">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32028-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="32028-113"><a name="ipaddprefix"></a>Zmodyfikuj prefiksy adresów IP</span><span class="sxs-lookup"><span data-stu-id="32028-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="32028-114"><a name="gwip"></a>Zmodyfikuj adres IP bramy hello</span><span class="sxs-lookup"><span data-stu-id="32028-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="32028-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32028-115">Next steps</span></span>

<span data-ttu-id="32028-116">Można sprawdzić połączenie bramy.</span><span class="sxs-lookup"><span data-stu-id="32028-116">You can verify your gateway connection.</span></span> <span data-ttu-id="32028-117">Zobacz [sprawdzić połączenie bramy](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="32028-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>