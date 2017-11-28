---
title: "aaaDifferent sposobów toocreate maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla listę toocreate różne sposoby hello maszynę wirtualną za pomocą Menedżera zasobów systemu Windows."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="d3980-103">Różne sposoby toocreate maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d3980-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="d3980-104">System Azure oferuje różne sposoby toocreate maszyny wirtualnej, ponieważ maszyny wirtualne są odpowiednie dla różnych użytkowników i celów.</span><span class="sxs-lookup"><span data-stu-id="d3980-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="d3980-105">To oznacza, że konieczne toomake niektóre opcje dotyczące maszyny wirtualnej hello i w jaki sposób toocreate go.</span><span class="sxs-lookup"><span data-stu-id="d3980-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="d3980-106">Ten artykuł zawiera podsumowanie tych opcji oraz łączy tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="d3980-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="d3980-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d3980-107">Azure portal</span></span>
<span data-ttu-id="d3980-108">Przy użyciu portalu Azure hello jest tootry prosty sposób limit maszynę wirtualną, zwłaszcza, jeśli zaczynasz przy użyciu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d3980-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="d3980-109">Utwórz maszynę wirtualną z systemem Windows przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="d3980-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="d3980-110">Szablon</span><span class="sxs-lookup"><span data-stu-id="d3980-110">Template</span></span>
<span data-ttu-id="d3980-111">Maszyny wirtualne wymagają różnych zasobów (np. o dostępności zestawów i kont magazynu).</span><span class="sxs-lookup"><span data-stu-id="d3980-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="d3980-112">Zamiast wdrażanie i zarządzanie każdego zasobu oddzielnie, można utworzyć szablonu usługi Azure Resource Manager, który wdraża i udostępnia wszystkie zasoby hello w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="d3980-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="d3980-113">Tworzenie maszyny wirtualnej z systemem Windows przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3980-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="d3980-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3980-114">Azure PowerShell</span></span>
<span data-ttu-id="d3980-115">Jeśli wolisz Praca w powłoce poleceń, można użyć programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3980-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="d3980-116">Tworzenie maszyny wirtualnej z systemem Windows przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3980-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="d3980-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3980-117">Visual Studio</span></span>
<span data-ttu-id="d3980-118">Użyj toobuild programu Visual Studio, zarządzać i wdrażanie maszyn wirtualnych o hello Azure Tools dla programu Visual Studio oraz hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="d3980-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="d3980-119">Azure Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3980-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

