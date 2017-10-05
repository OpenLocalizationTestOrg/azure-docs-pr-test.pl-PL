---
title: "Różne sposoby tworzenia maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla listę różnych sposobów tworzenia maszyny wirtualnej systemu Windows za pomocą Menedżera zasobów."
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a><span data-ttu-id="b3fab-103">Różne sposoby tworzenia maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b3fab-103">Different ways to create a Windows virtual machine</span></span>

<span data-ttu-id="b3fab-104">System Azure oferuje różne sposoby tworzenia maszyny wirtualnej, ponieważ maszyny wirtualne są odpowiednie dla różnych użytkowników i celów.</span><span class="sxs-lookup"><span data-stu-id="b3fab-104">Azure offers different ways to create a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="b3fab-105">Oznacza to, należy wybrać niektóre opcje dotyczące maszyny wirtualnej i utwórz go.</span><span class="sxs-lookup"><span data-stu-id="b3fab-105">This means that you need to make some choices about the virtual machine and how to create it.</span></span> <span data-ttu-id="b3fab-106">Ten artykuł zawiera podsumowanie tych opcji i linki do instrukcji.</span><span class="sxs-lookup"><span data-stu-id="b3fab-106">This article gives you a summary of these choices and links to instructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b3fab-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3fab-107">Azure portal</span></span>
<span data-ttu-id="b3fab-108">Przy użyciu portalu Azure jest prosty sposób na wypróbowanie maszynę wirtualną, zwłaszcza jeśli zaczynasz przy użyciu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3fab-108">Using the Azure portal is a simple way to try out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="b3fab-109">Tworzenie maszyny wirtualnej z systemem Windows przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="b3fab-109">Create a virtual machine running Windows using the portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="b3fab-110">Szablon</span><span class="sxs-lookup"><span data-stu-id="b3fab-110">Template</span></span>
<span data-ttu-id="b3fab-111">Maszyny wirtualne wymagają różnych zasobów (np. o dostępności zestawów i kont magazynu).</span><span class="sxs-lookup"><span data-stu-id="b3fab-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="b3fab-112">Zamiast wdrażanie i zarządzanie każdego zasobu oddzielnie, można utworzyć szablonu usługi Azure Resource Manager, który wdraża i udostępnia wszystkie zasoby w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="b3fab-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of the resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="b3fab-113">Tworzenie maszyny wirtualnej z systemem Windows przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3fab-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="b3fab-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fab-114">Azure PowerShell</span></span>
<span data-ttu-id="b3fab-115">Jeśli wolisz Praca w powłoce poleceń, można użyć programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3fab-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="b3fab-116">Tworzenie maszyny wirtualnej z systemem Windows przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3fab-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="b3fab-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b3fab-117">Visual Studio</span></span>
<span data-ttu-id="b3fab-118">Do tworzenia, zarządzania i wdrażania maszyn wirtualnych przy użyciu narzędzi platformy Azure dla programu Visual Studio i zestawu Azure SDK, należy użyć programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3fab-118">Use Visual Studio to build, manage, and deploy VMs with the Azure Tools for Visual Studio and the Azure SDK.</span></span>

[<span data-ttu-id="b3fab-119">Azure Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b3fab-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

