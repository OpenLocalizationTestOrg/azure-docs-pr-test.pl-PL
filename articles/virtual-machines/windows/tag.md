---
title: tootag aaaHow zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o znakowanie utworzona na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello maszynę wirtualną systemu Windows"
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
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="71af3-103">Jak tootag maszynę wirtualną systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="71af3-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="71af3-104">W tym artykule opisano różne sposoby tootag maszynę wirtualną systemu Windows na platformie Azure za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="71af3-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="71af3-105">Tagi to pary klucz wartość zdefiniowana przez użytkownika, które mogą być umieszczone bezpośrednio na zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="71af3-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="71af3-106">Obecnie Azure obsługuje tagi too15 według zasobu i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="71af3-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="71af3-107">Tagi mogą być umieszczane w zasobie na powitania godzina utworzenia lub dodać tooan istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="71af3-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="71af3-108">Należy pamiętać, że tagi są obsługiwane dla zasobów utworzone za pośrednictwem modelu wdrażania usługi Resource Manager hello tylko.</span><span class="sxs-lookup"><span data-stu-id="71af3-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="71af3-109">Jeśli chcesz tootag maszyny wirtualnej systemu Linux, zobacz [jak tootag maszyny wirtualnej systemu Linux na platformie Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71af3-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="71af3-110">Znakowanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71af3-110">Tagging with PowerShell</span></span>
<span data-ttu-id="71af3-111">toocreate, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw tooset się z [środowiska PowerShell z usługą Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="71af3-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="71af3-112">Po zakończeniu instalacji hello można umieścić znaczniki zasobów obliczeniowych, sieci i magazynu podczas tworzenia lub hello zasób został utworzony za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71af3-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="71af3-113">W tym artykule będzie skoncentrować się na wyświetlanie/edytowanie tagów umieszczone na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="71af3-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="71af3-114">Przejdź najpierw tooa maszyny wirtualnej za pośrednictwem hello `Get-AzureRmVM` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71af3-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="71af3-115">Maszyna wirtualna zawiera już znaczników, zostanie wtedy wyświetlone wszystkie tagi hello na zasobu:</span><span class="sxs-lookup"><span data-stu-id="71af3-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="71af3-116">Jeśli chcesz tooadd tagów za pomocą programu PowerShell, możesz użyć hello `Set-AzureRmResource` polecenia.</span><span class="sxs-lookup"><span data-stu-id="71af3-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="71af3-117">Należy zwrócić uwagę podczas aktualizowania tagów za pomocą programu PowerShell, tagi są aktualizowane jako całość.</span><span class="sxs-lookup"><span data-stu-id="71af3-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="71af3-118">Dlatego w przypadku dodawania jeden tag tooa zasób, który ma już tagi, konieczne będzie tooinclude wszystkie tagi hello, które mają toobe dotyczącymi zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="71af3-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="71af3-119">Poniżej przedstawiono przykładowy sposób tooadd dodatkowe znaczniki tooa zasobów za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71af3-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="71af3-120">To pierwsze polecenie cmdlet ustawia wszystkich znaczników hello dotyczącymi *MyTestVM* toohello *$tags* zmiennej przy użyciu hello `Get-AzureRmResource` i `Tags` właściwości.</span><span class="sxs-lookup"><span data-stu-id="71af3-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="71af3-121">drugie polecenie Hello Wyświetla hello tagów hello podane zmiennej.</span><span class="sxs-lookup"><span data-stu-id="71af3-121">hello second command displays hello tags for hello given variable.</span></span>

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

<span data-ttu-id="71af3-122">trzecie polecenie Hello dodaje toohello dodatkowe tag *$tags* zmiennej.</span><span class="sxs-lookup"><span data-stu-id="71af3-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="71af3-123">Należy zwrócić uwagę użycie hello hello  **+=**  tooappend hello nowe toohello pary klucz wartość *$tags* listy.</span><span class="sxs-lookup"><span data-stu-id="71af3-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="71af3-124">polecenie czwarty Hello ustawia wszystkich znaczników hello zdefiniowane w hello *$tags* zmiennej toohello danego zasobu.</span><span class="sxs-lookup"><span data-stu-id="71af3-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="71af3-125">W takim przypadku jest MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="71af3-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="71af3-126">polecenie piątym powitania Wyświetla wszystkie znaczniki hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="71af3-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="71af3-127">Jak widać, *lokalizacji* jest teraz zdefiniowany jako tag *MyLocation* jako wartość hello.</span><span class="sxs-lookup"><span data-stu-id="71af3-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

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

<span data-ttu-id="71af3-128">więcej informacji o toolearn znakowanie za pomocą programu PowerShell, zapoznaj się z hello [polecenia cmdlet usługi Azure Resource][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="71af3-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="71af3-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71af3-129">Next steps</span></span>
* <span data-ttu-id="71af3-130">toolearn więcej informacji na temat znakowanie zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager] [ Azure Resource Manager Overview] i [tooorganize przy użyciu tagów zasobów platformy Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="71af3-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="71af3-131">toosee tagi ułatwia zarządzanie korzystanie z zasobów platformy Azure, zobacz [Opis rachunku Azure] [ Understanding your Azure Bill] i [uzyskać wgląd w Microsoft Azure użycia zasobów] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="71af3-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
