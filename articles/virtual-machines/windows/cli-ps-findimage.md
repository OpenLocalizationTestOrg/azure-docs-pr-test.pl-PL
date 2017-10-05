---
title: Wybierz obrazy maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać programu Azure PowerSHell w celu określenia wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
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
ms.openlocfilehash: 814ae260123c045d4b6766bf4b312f874cd77068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-windows-vm-images-in-the-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="25bc7-103">Jak znaleźć obrazów maszyn wirtualnych systemu Windows w portalu Azure Marketplace przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="25bc7-103">How to find Windows VM images in the Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="25bc7-104">W tym temacie opisano sposób użycia programu Azure PowerShell można znaleźć obrazów maszyn wirtualnych w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="25bc7-104">This topic describes how to use Azure PowerShell to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="25bc7-105">Dzięki tym informacjom można określić obrazu z witryny Marketplace, podczas tworzenia maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="25bc7-105">Use this information to specify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="25bc7-106">Upewnij się, że zainstalowane i skonfigurowane najnowszej [modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="25bc7-106">Make sure that you installed and configured the latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="25bc7-107">Tabela często używane obrazów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="25bc7-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="25bc7-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="25bc7-108">PublisherName</span></span> | <span data-ttu-id="25bc7-109">Oferta</span><span class="sxs-lookup"><span data-stu-id="25bc7-109">Offer</span></span> | <span data-ttu-id="25bc7-110">SKU</span><span class="sxs-lookup"><span data-stu-id="25bc7-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="25bc7-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-112">WindowsServer</span></span> |<span data-ttu-id="25bc7-113">Centrum danych 2016</span><span class="sxs-lookup"><span data-stu-id="25bc7-113">2016-Datacenter</span></span> |
| <span data-ttu-id="25bc7-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-115">WindowsServer</span></span> |<span data-ttu-id="25bc7-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="25bc7-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="25bc7-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-118">WindowsServer</span></span> |<span data-ttu-id="25bc7-119">2016 centrum danych z kontenerów</span><span class="sxs-lookup"><span data-stu-id="25bc7-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="25bc7-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-121">WindowsServer</span></span> |<span data-ttu-id="25bc7-122">2016-Nano serwer</span><span class="sxs-lookup"><span data-stu-id="25bc7-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="25bc7-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-124">WindowsServer</span></span> |<span data-ttu-id="25bc7-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="25bc7-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="25bc7-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="25bc7-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-127">WindowsServer</span></span> |<span data-ttu-id="25bc7-128">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="25bc7-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="25bc7-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="25bc7-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="25bc7-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="25bc7-130">DynamicsNAV</span></span> |<span data-ttu-id="25bc7-131">2017</span><span class="sxs-lookup"><span data-stu-id="25bc7-131">2017</span></span> |
| <span data-ttu-id="25bc7-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="25bc7-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="25bc7-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="25bc7-134">2016</span><span class="sxs-lookup"><span data-stu-id="25bc7-134">2016</span></span> |
| <span data-ttu-id="25bc7-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="25bc7-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="25bc7-136">SQL2016-WS2016</span></span> |<span data-ttu-id="25bc7-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="25bc7-137">Enterprise</span></span> |
| <span data-ttu-id="25bc7-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="25bc7-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="25bc7-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="25bc7-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="25bc7-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="25bc7-140">Enterprise</span></span> |
| <span data-ttu-id="25bc7-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="25bc7-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="25bc7-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="25bc7-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="25bc7-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="25bc7-143">2012R2</span></span> |
| <span data-ttu-id="25bc7-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="25bc7-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="25bc7-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="25bc7-145">WindowsServerEssentials</span></span> |<span data-ttu-id="25bc7-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="25bc7-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="25bc7-147">Znajdowanie określonych obrazów</span><span class="sxs-lookup"><span data-stu-id="25bc7-147">Find specific images</span></span>


<span data-ttu-id="25bc7-148">Podczas tworzenia nowej maszyny wirtualnej przy użyciu usługi Azure Resource Manager w niektórych przypadkach należy określić obraz za pomocą kombinacji następujących właściwości obrazu:</span><span class="sxs-lookup"><span data-stu-id="25bc7-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="25bc7-149">Wydawca</span><span class="sxs-lookup"><span data-stu-id="25bc7-149">Publisher</span></span>
* <span data-ttu-id="25bc7-150">Oferta</span><span class="sxs-lookup"><span data-stu-id="25bc7-150">Offer</span></span>
* <span data-ttu-id="25bc7-151">SKU</span><span class="sxs-lookup"><span data-stu-id="25bc7-151">SKU</span></span>

<span data-ttu-id="25bc7-152">Na przykład użyć tych wartości za pomocą [AzureRMVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) polecenia cmdlet programu PowerShell, lub za pomocą szablonu grupy zasobów, w którym należy określić typ maszyna wirtualna ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="25bc7-152">For example, use these values with the [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify the type of VM to be created.</span></span>

<span data-ttu-id="25bc7-153">Jeśli trzeba określić te wartości, możesz uruchomić [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), i [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) poleceń cmdlet, aby przejść obrazów.</span><span class="sxs-lookup"><span data-stu-id="25bc7-153">If you need to determine these values, you can run the [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets to navigate the images.</span></span> <span data-ttu-id="25bc7-154">Należy określić te wartości:</span><span class="sxs-lookup"><span data-stu-id="25bc7-154">You determine these values:</span></span>

1. <span data-ttu-id="25bc7-155">Wyświetl listę wydawców obrazów.</span><span class="sxs-lookup"><span data-stu-id="25bc7-155">List the image publishers.</span></span>
2. <span data-ttu-id="25bc7-156">Dla danego wydawcy wyświetl listę ofert.</span><span class="sxs-lookup"><span data-stu-id="25bc7-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="25bc7-157">Dla danej oferty wyświetl listę wersji SKU.</span><span class="sxs-lookup"><span data-stu-id="25bc7-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="25bc7-158">Najpierw wyświetl listę wydawców za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="25bc7-158">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="25bc7-159">Wprowadź nazwę wybranego wydawcy i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="25bc7-159">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="25bc7-160">Wprowadź nazwę wybranej oferty i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="25bc7-160">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="25bc7-161">Z danych wyjściowych `Get-AzureRMVMImageSku` polecenie ma wszystkie informacje, należy określić obraz dla nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25bc7-161">From the output of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="25bc7-162">Poniżej przedstawiono pełny przykład:</span><span class="sxs-lookup"><span data-stu-id="25bc7-162">The following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="25bc7-163">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="25bc7-163">Output:</span></span>

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

<span data-ttu-id="25bc7-164">Dla wydawcy „MicrosoftWindowsServer”:</span><span class="sxs-lookup"><span data-stu-id="25bc7-164">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="25bc7-165">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="25bc7-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="25bc7-166">Dla oferty „WindowsServer”:</span><span class="sxs-lookup"><span data-stu-id="25bc7-166">For the "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="25bc7-167">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="25bc7-167">Output:</span></span>

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

<span data-ttu-id="25bc7-168">Skopiuj z tej listy nazwę wybranej wersji SKU — w ten sposób uzyskasz wszystkie informacje, jakie należy podać w poleceniu cmdlet programu PowerShell `Set-AzureRMVMSourceImage` lub szablonie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="25bc7-168">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25bc7-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25bc7-169">Next steps</span></span>
<span data-ttu-id="25bc7-170">Teraz można dokładnie wybrać obraz, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="25bc7-170">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="25bc7-171">Aby szybko utworzyć maszynę wirtualną, korzystając z informacji obrazu, który właśnie odnaleziony, zobacz [Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="25bc7-171">To create a virtual machine quickly by using the image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
