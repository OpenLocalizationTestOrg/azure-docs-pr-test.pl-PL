---
title: Szablon hello aaaDownload dla maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Pobierz templatefor hello toohelp maszyny Wirtualnej, automatyzacji wdrażania modelu wdrażania usługi Resource Manager hello"
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="19770-103">Pobierz hello szablon maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="19770-103">Download hello template for a VM</span></span>
<span data-ttu-id="19770-104">Podczas tworzenia maszyny Wirtualnej na platformie Azure za pomocą portalu hello lub programu PowerShell, Menedżer zasobów szablonu jest utworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="19770-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="19770-105">Można użyć tego duplikat tooquickly szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="19770-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="19770-106">Szablon Hello zawiera informacje na temat wszystkich zasobów hello w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="19770-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="19770-107">Dla maszyny wirtualnej oznacza to, że szablon hello zawiera wszystko, co jest tworzony w związku z hello maszyny Wirtualnej w tej grupie zasobów, w tym hello zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="19770-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="19770-108">Pobierz szablon hello przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="19770-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="19770-109">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="19770-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="19770-110">Hello jednego koncentratora menu, wybierz opcję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="19770-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="19770-111">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="19770-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="19770-112">Wybierz **skryptu automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="19770-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="19770-113">Wybierz **Pobierz** i Zapisz komputer lokalny plik tooyour hello zip.</span><span class="sxs-lookup"><span data-stu-id="19770-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="19770-114">Otwórz plik zip hello i wyodrębnienia hello pliki tooa folder.</span><span class="sxs-lookup"><span data-stu-id="19770-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="19770-115">plik zip Hello będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="19770-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="19770-116">Deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="19770-116">deploy.ps1</span></span>
   * <span data-ttu-id="19770-117">Deploy.sh</span><span class="sxs-lookup"><span data-stu-id="19770-117">deploy.sh</span></span> 
   * <span data-ttu-id="19770-118">deployer.RB</span><span class="sxs-lookup"><span data-stu-id="19770-118">deployer.rb</span></span>
   * <span data-ttu-id="19770-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="19770-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="19770-120">parameters.JSON następującym kodem</span><span class="sxs-lookup"><span data-stu-id="19770-120">parameters.json</span></span>
   * <span data-ttu-id="19770-121">Template.JSON</span><span class="sxs-lookup"><span data-stu-id="19770-121">template.json</span></span>

<span data-ttu-id="19770-122">Plik template.json Hello jest hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="19770-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="19770-123">Pobierz szablon hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="19770-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="19770-124">Możesz również pobrać plik szablonu JSON hello przy użyciu hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="19770-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="19770-125">Można użyć hello `-path` parametru tooprovide hello nazwę i ścieżkę do pliku JSON hello.</span><span class="sxs-lookup"><span data-stu-id="19770-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="19770-126">W tym przykładzie pokazano, jak szablon hello toodownload hello grupy zasobów o nazwie **myResourceGroup** toohello **C:\users\public\downloads** folderu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="19770-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="19770-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19770-127">Next steps</span></span>
<span data-ttu-id="19770-128">toolearn więcej informacji na temat wdrażania zasobów przy użyciu szablonów, zobacz [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="19770-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

