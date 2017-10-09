---
title: "połączenie bramy sieci VPN aaaVerify | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooverify a wirtualnych sieci połączenie bramy sieci VPN."
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="27d56-103">Sprawdź połączenie bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="27d56-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="27d56-104">W tym artykule opisano sposób tooverify połączenie bramy sieci VPN dla hello klasycznego i modeli wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="27d56-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="27d56-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="27d56-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="27d56-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27d56-106">PowerShell</span></span>

<span data-ttu-id="27d56-107">tooverify połączenia bramy sieci VPN dla hello wdrożenie usługi Resource Manager modelu przy użyciu programu PowerShell, należy zainstalować najnowszą wersję hello hello [poleceń cmdlet programu PowerShell usługi Azure Resource Manager](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="27d56-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="27d56-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="27d56-108">Azure CLI</span></span>

<span data-ttu-id="27d56-109">tooverify połączenia bramy sieci VPN dla hello wdrożenie usługi Resource Manager modelu przy użyciu wiersza polecenia platformy Azure, zainstaluj najnowszą wersję hello hello [polecenia interfejsu wiersza polecenia](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="27d56-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="27d56-110">Portalu Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="27d56-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="27d56-111">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="27d56-111">PowerShell (classic)</span></span>

<span data-ttu-id="27d56-112">tooverify połączenia bramy sieci VPN dla hello wdrażania klasycznego modelu przy użyciu programu PowerShell, należy zainstalować najnowsze wersje hello hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27d56-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="27d56-113">Należy się hello toodownload i zainstaluj [zarządzania usługami](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) modułu.</span><span class="sxs-lookup"><span data-stu-id="27d56-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="27d56-114">Użyj "Add-AzureAccount" toolog w toohello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="27d56-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="27d56-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27d56-115">Next steps</span></span>

* <span data-ttu-id="27d56-116">Można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="27d56-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="27d56-117">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27d56-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
