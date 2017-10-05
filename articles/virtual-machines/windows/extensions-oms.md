---
title: Rozszerzenie maszyny wirtualnej OMS Azure dla systemu Windows | Dokumentacja firmy Microsoft
description: "Wdróż agenta pakietu OMS na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej."
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
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="c269d-103">Rozszerzenie maszyny wirtualnej OMS dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c269d-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="c269d-104">Operations Management Suite (OMS) zapewnia możliwości korygowania monitorowania, alertów i alertów w chmurze i lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c269d-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="c269d-105">Agent pakietu OMS rozszerzenie maszyny wirtualnej dla systemu Windows publikowana i obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c269d-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="c269d-106">Rozszerzenie instaluje agenta pakietu OMS na maszynach wirtualnych platformy Azure i rejestrowania maszyn wirtualnych w istniejącym obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c269d-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="c269d-107">Ten dokument zawiera szczegóły dotyczące obsługiwanych platform, konfiguracji i opcje wdrażania dla rozszerzenia maszyny wirtualnej OMS dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c269d-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c269d-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c269d-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="c269d-109">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="c269d-109">Operating system</span></span>
<span data-ttu-id="c269d-110">Rozszerzenie Agent pakietu OMS dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.</span><span class="sxs-lookup"><span data-stu-id="c269d-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="c269d-111">Łączność z Internetem</span><span class="sxs-lookup"><span data-stu-id="c269d-111">Internet connectivity</span></span>
<span data-ttu-id="c269d-112">Rozszerzenia Agent pakietu OMS dla systemu Windows wymaga, aby docelowa maszyna wirtualna jest połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="c269d-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="c269d-113">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="c269d-113">Extension schema</span></span>

<span data-ttu-id="c269d-114">Następujące JSON zawiera schemat rozszerzenia Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c269d-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="c269d-115">Rozszerzenie wymaga obszaru roboczego identyfikator i klucz obszaru roboczego z docelowy obszar roboczy OMS, te można znaleźć w portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="c269d-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="c269d-116">Ponieważ klucz obszaru roboczego powinien być traktowany jako dane poufne, powinny być przechowywane w chronionej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c269d-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="c269d-117">Dane Azure ustawienia rozszerzenia chronione maszyny Wirtualnej jest szyfrowany i odszyfrowane tylko na docelowej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c269d-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="c269d-118">Należy pamiętać, że **workspaceId** i **workspaceKey** jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="c269d-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="c269d-119">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="c269d-119">Property values</span></span>

| <span data-ttu-id="c269d-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c269d-120">Name</span></span> | <span data-ttu-id="c269d-121">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="c269d-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="c269d-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c269d-122">apiVersion</span></span> | <span data-ttu-id="c269d-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="c269d-123">2015-06-15</span></span> |
| <span data-ttu-id="c269d-124">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="c269d-124">publisher</span></span> | <span data-ttu-id="c269d-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="c269d-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="c269d-126">type</span><span class="sxs-lookup"><span data-stu-id="c269d-126">type</span></span> | <span data-ttu-id="c269d-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="c269d-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="c269d-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="c269d-128">typeHandlerVersion</span></span> | <span data-ttu-id="c269d-129">1.0</span><span class="sxs-lookup"><span data-stu-id="c269d-129">1.0</span></span> |
| <span data-ttu-id="c269d-130">workspaceId (np.)</span><span class="sxs-lookup"><span data-stu-id="c269d-130">workspaceId (e.g)</span></span> | <span data-ttu-id="c269d-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="c269d-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="c269d-132">workspaceKey (np.)</span><span class="sxs-lookup"><span data-stu-id="c269d-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="c269d-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="c269d-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="c269d-134">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="c269d-134">Template deployment</span></span>

<span data-ttu-id="c269d-135">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c269d-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="c269d-136">Schematu JSON szczegółowo opisane w poprzedniej sekcji można w szablonie usługi Azure Resource Manager rozszerzenia Agent pakietu OMS są uruchamiane podczas wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c269d-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="c269d-137">Przykładowy szablon, który uwzględnia również rozszerzenie maszyny Wirtualnej agenta pakietu OMS można znaleźć w [Azure Szybki Start galerii](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c269d-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="c269d-138">JSON dla rozszerzenia maszyny wirtualnej mogą być zagnieżdżone wewnątrz zasobu maszyny wirtualnej lub umieszczony w katalogu głównego lub najwyższego poziomu szablonu usługi Resource Manager JSON.</span><span class="sxs-lookup"><span data-stu-id="c269d-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="c269d-139">Umieszczanie JSON ma wpływ na wartość nazwy zasobów i typu.</span><span class="sxs-lookup"><span data-stu-id="c269d-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="c269d-140">Aby uzyskać więcej informacji, zobacz [Ustaw nazwę i typ zasoby podrzędne](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c269d-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="c269d-141">Poniższy przykład przyjęto założenie, że rozszerzenie OMS jest zagnieżdżona zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c269d-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="c269d-142">Podczas zagnieżdżania rozszerzenia zasobu, JSON jest umieszczany w `"resources": []` obiektu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c269d-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


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

<span data-ttu-id="c269d-143">Podczas umieszczania rozszerzenia JSON w elemencie głównym szablonu, nazwy zasobu zawiera odwołanie do nadrzędnego maszyny wirtualnej, a typ odzwierciedla zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="c269d-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="c269d-144">Wdrożenie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c269d-144">PowerShell deployment</span></span>

<span data-ttu-id="c269d-145">`Set-AzureRmVMExtension` Polecenia można wdrożyć agenta pakietu OMS rozszerzenie maszyny wirtualnej na istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c269d-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="c269d-146">Przed uruchomieniem polecenia, konfiguracje publicznymi i prywatnymi muszą być przechowywane w tablicy skrótów programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c269d-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="c269d-147">Rozwiązywanie problemów i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="c269d-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="c269d-148">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c269d-148">Troubleshoot</span></span>

<span data-ttu-id="c269d-149">Dane dotyczące stanu wdrożenia rozszerzenia może zostać pobrany z portalu Azure i przy użyciu modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c269d-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="c269d-150">Aby wyświetlić stan wdrożenia rozszerzeń dla danej maszyny Wirtualnej, uruchom następujące polecenie przy użyciu modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c269d-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="c269d-151">Dane wyjściowe wykonania rozszerzenia jest rejestrowany pliki znajdujące się w następującym katalogu:</span><span class="sxs-lookup"><span data-stu-id="c269d-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="c269d-152">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="c269d-152">Support</span></span>

<span data-ttu-id="c269d-153">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ekspertów platformy Azure na [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="c269d-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="c269d-154">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c269d-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="c269d-155">Przejdź do [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="c269d-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="c269d-156">Aby uzyskać informacje o korzystaniu z platformy Azure obsługuje, przeczytaj [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="c269d-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
