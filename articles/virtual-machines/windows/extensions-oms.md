---
title: aaaOMS rozszerzenia maszyny wirtualnej platformy Azure dla systemu Windows | Dokumentacja firmy Microsoft
description: "Wdróż agenta pakietu OMS hello na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="d99ca-103">Rozszerzenie maszyny wirtualnej OMS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d99ca-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="d99ca-104">Operations Management Suite (OMS) zapewnia możliwości korygowania monitorowania, alertów i alertów w chmurze i lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d99ca-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="d99ca-105">Witaj Agent pakietu OMS rozszerzenie maszyny wirtualnej dla systemu Windows publikowana i obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d99ca-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="d99ca-106">rozszerzenie Hello instaluje agenta pakietu OMS hello na maszynach wirtualnych platformy Azure i rejestrowania maszyn wirtualnych w istniejącym obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="d99ca-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="d99ca-107">Hello szczegóły tego dokumentu obsługiwanych platform, konfiguracji i opcji wdrażania dla hello OMS rozszerzenie maszyny wirtualnej dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d99ca-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d99ca-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d99ca-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="d99ca-109">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="d99ca-109">Operating system</span></span>
<span data-ttu-id="d99ca-110">Witaj Agent pakietu OMS rozszerzenia dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.</span><span class="sxs-lookup"><span data-stu-id="d99ca-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="d99ca-111">Łączność z Internetem</span><span class="sxs-lookup"><span data-stu-id="d99ca-111">Internet connectivity</span></span>
<span data-ttu-id="d99ca-112">Hello Agent pakietu OMS rozszerzenia dla systemu Windows wymaga tego hello docelowej maszyny wirtualnej jest połączonych toohello internet.</span><span class="sxs-lookup"><span data-stu-id="d99ca-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="d99ca-113">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="d99ca-113">Extension schema</span></span>

<span data-ttu-id="d99ca-114">Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="d99ca-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="d99ca-115">rozszerzenie Hello wymaga hello klucz identyfikator i obszaru roboczego obszaru roboczego z obszarem roboczym pakietu OMS docelowej hello, te można znaleźć w portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="d99ca-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="d99ca-116">Ponieważ klucz obszaru roboczego hello powinny być traktowane jako poufne dane, powinny być przechowywane w chronionej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d99ca-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="d99ca-117">Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d99ca-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="d99ca-118">Należy pamiętać, że **workspaceId** i **workspaceKey** jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d99ca-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="d99ca-119">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="d99ca-119">Property values</span></span>

| <span data-ttu-id="d99ca-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d99ca-120">Name</span></span> | <span data-ttu-id="d99ca-121">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="d99ca-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="d99ca-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d99ca-122">apiVersion</span></span> | <span data-ttu-id="d99ca-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="d99ca-123">2015-06-15</span></span> |
| <span data-ttu-id="d99ca-124">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="d99ca-124">publisher</span></span> | <span data-ttu-id="d99ca-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="d99ca-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="d99ca-126">type</span><span class="sxs-lookup"><span data-stu-id="d99ca-126">type</span></span> | <span data-ttu-id="d99ca-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="d99ca-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="d99ca-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="d99ca-128">typeHandlerVersion</span></span> | <span data-ttu-id="d99ca-129">1.0</span><span class="sxs-lookup"><span data-stu-id="d99ca-129">1.0</span></span> |
| <span data-ttu-id="d99ca-130">workspaceId (np.)</span><span class="sxs-lookup"><span data-stu-id="d99ca-130">workspaceId (e.g)</span></span> | <span data-ttu-id="d99ca-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="d99ca-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="d99ca-132">workspaceKey (np.)</span><span class="sxs-lookup"><span data-stu-id="d99ca-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="d99ca-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="d99ca-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="d99ca-134">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="d99ca-134">Template deployment</span></span>

<span data-ttu-id="d99ca-135">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d99ca-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="d99ca-136">Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent pakietu OMS rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można.</span><span class="sxs-lookup"><span data-stu-id="d99ca-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="d99ca-137">Przykładowy szablon, która zawiera rozszerzenia maszyny Wirtualnej agenta pakietu OMS hello znajduje się na powitania [Azure Szybki Start galerii](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="d99ca-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="d99ca-138">Hello JSON dla rozszerzenia maszyny wirtualnej mogą być zagnieżdżone wewnątrz hello zasobu maszyny wirtualnej lub umieszczane na główny hello lub najwyższego poziomu szablonu usługi Resource Manager JSON.</span><span class="sxs-lookup"><span data-stu-id="d99ca-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="d99ca-139">rozmieszczenie Hello hello JSON dotyczy wartości hello hello nazwy zasobów i typu.</span><span class="sxs-lookup"><span data-stu-id="d99ca-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="d99ca-140">Aby uzyskać więcej informacji, zobacz [Ustaw nazwę i typ zasoby podrzędne](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d99ca-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="d99ca-141">Witaj poniższym przykładzie przyjęto założenie, że rozszerzenie OMS hello jest zagnieżdżona hello zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d99ca-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="d99ca-142">Podczas zagnieżdżania hello rozszerzenia zasobu, hello JSON jest umieszczany w hello `"resources": []` obiektu hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d99ca-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="d99ca-143">Podczas umieszczania hello rozszerzenia JSON w głównym hello hello szablonu, hello Nazwa zasobu zawiera maszynę wirtualną nadrzędnej toohello odwołania, a typ hello odzwierciedla hello zagnieżdżonych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d99ca-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="d99ca-144">Wdrożenie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d99ca-144">PowerShell deployment</span></span>

<span data-ttu-id="d99ca-145">Witaj `Set-AzureRmVMExtension` polecenie może być używane toodeploy hello Agent pakietu OMS maszyny wirtualnej rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d99ca-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="d99ca-146">Przed uruchomieniem polecenia hello, konfiguracje hello publicznymi i prywatnymi muszą toobe przechowywane w tablicy skrótów programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d99ca-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="d99ca-147">Rozwiązywanie problemów i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="d99ca-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="d99ca-148">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d99ca-148">Troubleshoot</span></span>

<span data-ttu-id="d99ca-149">Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="d99ca-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="d99ca-150">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej hello uruchom następujące polecenia przy użyciu hello modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d99ca-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="d99ca-151">Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:</span><span class="sxs-lookup"><span data-stu-id="d99ca-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="d99ca-152">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="d99ca-152">Support</span></span>

<span data-ttu-id="d99ca-153">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="d99ca-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="d99ca-154">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d99ca-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="d99ca-155">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="d99ca-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="d99ca-156">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="d99ca-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
