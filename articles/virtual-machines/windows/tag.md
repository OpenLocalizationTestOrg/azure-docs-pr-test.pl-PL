---
title: Jak tag zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o znakowanie utworzona na platformie Azure przy użyciu modelu wdrażania Menedżera zasobów systemu Windows maszyny wirtualnej"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 5f00c4265cea3db02dbb09a7f81be636a3fdd3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="e03a2-103">Jak tagu maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e03a2-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="e03a2-104">W tym artykule opisano różne sposoby tagu maszyny wirtualnej systemu Windows na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e03a2-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="e03a2-105">Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="e03a2-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="e03a2-106">Azure obecnie obsługuje maksymalnie 15 znaczników dla zasobu i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e03a2-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="e03a2-107">Tagi mogą dotyczącymi zasobów w czasie tworzenia lub dodać do istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="e03a2-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="e03a2-108">Należy pamiętać, że tagi są obsługiwane dla zasobów utworzone za pośrednictwem tylko modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="e03a2-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="e03a2-109">Jeśli chcesz oznaczyć maszyny wirtualnej systemu Linux, zobacz [jak tagu maszyny wirtualnej systemu Linux na platformie Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03a2-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="e03a2-110">Znakowanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e03a2-110">Tagging with PowerShell</span></span>
<span data-ttu-id="e03a2-111">Aby utworzyć, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw skonfigurować Twoje [środowiska PowerShell z usługą Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="e03a2-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="e03a2-112">Po zakończeniu instalacji można umieścić znaczniki zasobów obliczeniowych, sieci i magazynu podczas tworzenia lub zasób jest tworzony za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e03a2-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="e03a2-113">W tym artykule będzie skoncentrować się na wyświetlanie/edytowanie tagów umieszczone na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e03a2-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="e03a2-114">Po pierwsze, przejdź do maszyny wirtualnej za pomocą `Get-AzureRmVM` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e03a2-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="e03a2-115">Maszyna wirtualna zawiera już znaczników, zostanie wtedy wyświetlone wszystkie tagi na zasobu:</span><span class="sxs-lookup"><span data-stu-id="e03a2-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="e03a2-116">Jeśli chcesz dodać tagów za pomocą programu PowerShell, możesz użyć `Set-AzureRmResource` polecenia.</span><span class="sxs-lookup"><span data-stu-id="e03a2-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="e03a2-117">Należy zwrócić uwagę podczas aktualizowania tagów za pomocą programu PowerShell, tagi są aktualizowane jako całość.</span><span class="sxs-lookup"><span data-stu-id="e03a2-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="e03a2-118">Więc jeden tag jest dodawane do zasobu, który ma już tagi, należy uwzględnić wszystkie tagi, które mają zostać umieszczone w zasobie.</span><span class="sxs-lookup"><span data-stu-id="e03a2-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="e03a2-119">Poniżej przedstawiono przykładowy sposób dodawania dodatkowych tagów do zasobów za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e03a2-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="e03a2-120">To pierwsze polecenie cmdlet Ustawia wszystkie tagi dotyczącymi *MyTestVM* do *$tags* przy użyciu zmiennej `Get-AzureRmResource` i `Tags` właściwości.</span><span class="sxs-lookup"><span data-stu-id="e03a2-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="e03a2-121">Drugie polecenie wyświetla tagi dla danego zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e03a2-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="e03a2-122">Trzecie polecenie dodaje tag dodatkowe do *$tags* zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e03a2-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="e03a2-123">Zwróć uwagę na użycie  **+=**  do dołączenia nową parę klucz wartość do *$tags* listy.</span><span class="sxs-lookup"><span data-stu-id="e03a2-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="e03a2-124">Czwarte polecenie ustawia wszystkie tagi zdefiniowane w *$tags* zmienną do określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e03a2-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="e03a2-125">W takim przypadku jest MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="e03a2-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="e03a2-126">Polecenie piątego Wyświetla wszystkie tagi zasobu.</span><span class="sxs-lookup"><span data-stu-id="e03a2-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="e03a2-127">Jak widać, *lokalizacji* jest teraz zdefiniowany jako tag *MyLocation* jako wartość.</span><span class="sxs-lookup"><span data-stu-id="e03a2-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="e03a2-128">Aby dowiedzieć się więcej na temat znakowanie za pomocą programu PowerShell, zapoznaj się [polecenia cmdlet usługi Azure Resource][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="e03a2-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="e03a2-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e03a2-129">Next steps</span></span>
* <span data-ttu-id="e03a2-130">Aby dowiedzieć się więcej na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [przy użyciu tagów do organizowania zasobów platformy Azure][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="e03a2-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="e03a2-131">Aby dowiedzieć się, jak tagów można zarządzać korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="e03a2-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
