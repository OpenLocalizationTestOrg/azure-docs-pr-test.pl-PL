---
title: Pobierz szablon maszyny wirtualnej Azure | Dokumentacja firmy Microsoft
description: "Pobierz templatefor maszyny Wirtualnej, aby ułatwić Automatyzowanie wdrożeń w modelu wdrażania usługi Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="68a21-103">Pobieranie szablonu dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="68a21-103">Download the template for a VM</span></span>
<span data-ttu-id="68a21-104">Po utworzeniu maszyny Wirtualnej na platformie Azure za pomocą portalu lub programu PowerShell szablonu usługi Resource Manager jest tworzony automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="68a21-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="68a21-105">Ten szablon umożliwia szybkie duplikowanie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68a21-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="68a21-106">Szablon zawiera informacje na temat wszystkich zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="68a21-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="68a21-107">Dla maszyny wirtualnej oznacza to, że szablon zawiera wszystko, co jest tworzony w związku z maszyny Wirtualnej w ramach grupy zasobów, włącznie z zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="68a21-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="68a21-108">Pobieranie szablonu przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="68a21-108">Download the template using the portal</span></span>
1. <span data-ttu-id="68a21-109">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68a21-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68a21-110">Jeden menu Centrum wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="68a21-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="68a21-111">Wybierz maszynę wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="68a21-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="68a21-112">Wybierz **skryptu automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="68a21-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="68a21-113">Wybierz **Pobierz** i Zapisz plik zip na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68a21-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="68a21-114">Otwórz plik zip i Wyodrębnij pliki do folderu.</span><span class="sxs-lookup"><span data-stu-id="68a21-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="68a21-115">Plik zip będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="68a21-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="68a21-116">Deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="68a21-116">deploy.ps1</span></span>
   * <span data-ttu-id="68a21-117">Deploy.sh</span><span class="sxs-lookup"><span data-stu-id="68a21-117">deploy.sh</span></span> 
   * <span data-ttu-id="68a21-118">deployer.RB</span><span class="sxs-lookup"><span data-stu-id="68a21-118">deployer.rb</span></span>
   * <span data-ttu-id="68a21-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="68a21-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="68a21-120">parameters.JSON następującym kodem</span><span class="sxs-lookup"><span data-stu-id="68a21-120">parameters.json</span></span>
   * <span data-ttu-id="68a21-121">Template.JSON</span><span class="sxs-lookup"><span data-stu-id="68a21-121">template.json</span></span>

<span data-ttu-id="68a21-122">Plik template.json jest szablon.</span><span class="sxs-lookup"><span data-stu-id="68a21-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="68a21-123">Pobieranie szablonu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a21-123">Download the template using PowerShell</span></span>
<span data-ttu-id="68a21-124">Możesz również pobrać JSON szablonu plików przy użyciu [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68a21-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="68a21-125">Można użyć `-path` parametr, aby podać nazwę pliku i ścieżkę do pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="68a21-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="68a21-126">W tym przykładzie pokazano, jak pobrać szablonu dla grupy zasobów o nazwie **myResourceGroup** do **C:\users\public\downloads** folderu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="68a21-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="68a21-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68a21-127">Next steps</span></span>
<span data-ttu-id="68a21-128">Aby dowiedzieć się więcej o wdrażaniu zasobów przy użyciu szablonów, zobacz [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="68a21-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

