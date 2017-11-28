---
title: obrazy aaaSelect maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodetermine programu Azure PowerSHell toouse hello wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="5e54c-103">Jak obrazy toofind maszyny Wirtualnej systemu Windows w programie hello Azure Marketplace przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e54c-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="5e54c-104">W tym temacie opisano, jak obrazy toouse programu Azure PowerShell toofind maszyny Wirtualnej w programie hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5e54c-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="5e54c-105">Podczas tworzenia maszyny Wirtualnej systemu Windows za pomocą tej informacji toospecify obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5e54c-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="5e54c-106">Upewnij się, że zainstalowane i skonfigurowane hello najnowszych [modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5e54c-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="5e54c-107">Tabela często używane obrazów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5e54c-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="5e54c-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="5e54c-108">PublisherName</span></span> | <span data-ttu-id="5e54c-109">Oferta</span><span class="sxs-lookup"><span data-stu-id="5e54c-109">Offer</span></span> | <span data-ttu-id="5e54c-110">SKU</span><span class="sxs-lookup"><span data-stu-id="5e54c-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5e54c-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-112">WindowsServer</span></span> |<span data-ttu-id="5e54c-113">Centrum danych 2016</span><span class="sxs-lookup"><span data-stu-id="5e54c-113">2016-Datacenter</span></span> |
| <span data-ttu-id="5e54c-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-115">WindowsServer</span></span> |<span data-ttu-id="5e54c-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="5e54c-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="5e54c-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-118">WindowsServer</span></span> |<span data-ttu-id="5e54c-119">2016 centrum danych z kontenerów</span><span class="sxs-lookup"><span data-stu-id="5e54c-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="5e54c-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-121">WindowsServer</span></span> |<span data-ttu-id="5e54c-122">2016-Nano serwer</span><span class="sxs-lookup"><span data-stu-id="5e54c-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="5e54c-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-124">WindowsServer</span></span> |<span data-ttu-id="5e54c-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="5e54c-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="5e54c-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="5e54c-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-127">WindowsServer</span></span> |<span data-ttu-id="5e54c-128">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="5e54c-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="5e54c-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="5e54c-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="5e54c-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="5e54c-130">DynamicsNAV</span></span> |<span data-ttu-id="5e54c-131">2017</span><span class="sxs-lookup"><span data-stu-id="5e54c-131">2017</span></span> |
| <span data-ttu-id="5e54c-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="5e54c-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="5e54c-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="5e54c-134">2016</span><span class="sxs-lookup"><span data-stu-id="5e54c-134">2016</span></span> |
| <span data-ttu-id="5e54c-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="5e54c-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="5e54c-136">SQL2016-WS2016</span></span> |<span data-ttu-id="5e54c-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="5e54c-137">Enterprise</span></span> |
| <span data-ttu-id="5e54c-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="5e54c-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="5e54c-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="5e54c-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="5e54c-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="5e54c-140">Enterprise</span></span> |
| <span data-ttu-id="5e54c-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="5e54c-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="5e54c-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="5e54c-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="5e54c-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="5e54c-143">2012R2</span></span> |
| <span data-ttu-id="5e54c-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="5e54c-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="5e54c-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="5e54c-145">WindowsServerEssentials</span></span> |<span data-ttu-id="5e54c-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="5e54c-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="5e54c-147">Znajdowanie określonych obrazów</span><span class="sxs-lookup"><span data-stu-id="5e54c-147">Find specific images</span></span>


<span data-ttu-id="5e54c-148">Podczas tworzenia nowej maszyny wirtualnej za pomocą Menedżera zasobów Azure, w niektórych przypadkach należy toospecify obrazu z kombinacją hello hello następujące właściwości obrazu:</span><span class="sxs-lookup"><span data-stu-id="5e54c-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="5e54c-149">Wydawca</span><span class="sxs-lookup"><span data-stu-id="5e54c-149">Publisher</span></span>
* <span data-ttu-id="5e54c-150">Oferta</span><span class="sxs-lookup"><span data-stu-id="5e54c-150">Offer</span></span>
* <span data-ttu-id="5e54c-151">SKU</span><span class="sxs-lookup"><span data-stu-id="5e54c-151">SKU</span></span>

<span data-ttu-id="5e54c-152">Na przykład użyć tych wartości z hello [AzureRMVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) polecenia cmdlet programu PowerShell lub przy użyciu szablonu grupy zasobów, w którym należy określić typ hello toobe maszyny Wirtualnej utworzone.</span><span class="sxs-lookup"><span data-stu-id="5e54c-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="5e54c-153">Toodetermine tych wartości, należy wykonać hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), i [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) poleceń cmdlet toonavigate hello obrazów.</span><span class="sxs-lookup"><span data-stu-id="5e54c-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="5e54c-154">Należy określić te wartości:</span><span class="sxs-lookup"><span data-stu-id="5e54c-154">You determine these values:</span></span>

1. <span data-ttu-id="5e54c-155">Lista wydawców obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="5e54c-155">List hello image publishers.</span></span>
2. <span data-ttu-id="5e54c-156">Dla danego wydawcy wyświetl listę ofert.</span><span class="sxs-lookup"><span data-stu-id="5e54c-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="5e54c-157">Dla danej oferty wyświetl listę wersji SKU.</span><span class="sxs-lookup"><span data-stu-id="5e54c-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="5e54c-158">Po pierwsze lista wydawców hello z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5e54c-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="5e54c-159">Wypełnij nazwę wybranego wydawcy, a następnie uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="5e54c-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="5e54c-160">Wypełnij nazwę wybranego oferty, a następnie uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="5e54c-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="5e54c-161">Z danych wyjściowych hello hello `Get-AzureRMVMImageSku` polecenie ma wszystkie informacje hello potrzebne toospecify hello obrazu dla nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e54c-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="5e54c-162">Oto Hello pełny przykład:</span><span class="sxs-lookup"><span data-stu-id="5e54c-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="5e54c-163">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5e54c-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="5e54c-164">Dla wydawcy "MicrosoftWindowsServer" hello:</span><span class="sxs-lookup"><span data-stu-id="5e54c-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="5e54c-165">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5e54c-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="5e54c-166">Oferta "Windows Server" hello:</span><span class="sxs-lookup"><span data-stu-id="5e54c-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="5e54c-167">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5e54c-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="5e54c-168">Z tej listy, skopiuj hello wybrana nazwa jednostki SKU i mieć wszystkie informacje hello hello `Set-AzureRMVMSourceImage` polecenia cmdlet programu PowerShell lub szablonu grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5e54c-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e54c-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e54c-169">Next steps</span></span>
<span data-ttu-id="5e54c-170">Teraz można wybrać dokładnie hello obraz ma toouse.</span><span class="sxs-lookup"><span data-stu-id="5e54c-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="5e54c-171">Zobacz maszynę wirtualną, używając szybko hello obrazu informacje, które właśnie znaleziony, toocreate [Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5e54c-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
