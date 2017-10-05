---
title: "Sprawdź połączenie bramy sieci VPN | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób sprawdzania, połączenie sieci VPN bramy sieci wirtualnej."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="a92ab-103">Sprawdź połączenie bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="a92ab-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="a92ab-104">W tym artykule przedstawiono sposób sprawdzić połączenie bramy sieci VPN dla modeli wdrażania usługi Resource Manager i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="a92ab-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="a92ab-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a92ab-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="a92ab-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a92ab-106">PowerShell</span></span>

<span data-ttu-id="a92ab-107">Aby sprawdzić połączenie bramy sieci VPN dla modelu wdrażania usługi Resource Manager przy użyciu programu PowerShell, należy zainstalować najnowszą wersję [poleceń cmdlet programu PowerShell usługi Azure Resource Manager](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a92ab-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="a92ab-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a92ab-108">Azure CLI</span></span>

<span data-ttu-id="a92ab-109">Aby sprawdzić połączenie bramy sieci VPN dla modelu wdrażania usługi Resource Manager przy użyciu wiersza polecenia platformy Azure, zainstaluj najnowszą wersję [polecenia interfejsu wiersza polecenia](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="a92ab-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="a92ab-110">Portalu Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="a92ab-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="a92ab-111">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="a92ab-111">PowerShell (classic)</span></span>

<span data-ttu-id="a92ab-112">Aby sprawdzić połączenie bramy sieci VPN dla klasycznym modelu wdrażania przy użyciu programu PowerShell, należy zainstalować najnowsze wersje poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a92ab-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="a92ab-113">Pamiętaj pobrać i zainstalować [zarządzania usługami](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) modułu.</span><span class="sxs-lookup"><span data-stu-id="a92ab-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="a92ab-114">Użyj "Add-AzureAccount", aby zalogować się w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a92ab-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a92ab-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a92ab-115">Next steps</span></span>

* <span data-ttu-id="a92ab-116">Do sieci wirtualnych można dodać maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="a92ab-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="a92ab-117">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a92ab-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>