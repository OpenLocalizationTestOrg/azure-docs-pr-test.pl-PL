---
title: "Eksportowanie grupy zasobów Azure, która zawiera rozszerzenia maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Wyeksportować szablony Menedżera zasobów, które obejmują rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cc3c705f1c9123de75ced016a5b39eb1a86b0f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="5bd1f-103">Eksportowanie grupy zasobów, która zawiera rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5bd1f-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="5bd1f-104">Grupy zasobów platformy Azure mogą być eksportowane do nowego szablonu usługi Resource Manager, które mogą być następnie wdrażane.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="5bd1f-105">Proces eksportu interpretuje istniejących zasobów i tworzy szablon usługi Resource Manager która po wdrożeniu powoduje podobne grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="5bd1f-106">Korzystając z opcji eksportu grupy zasobów przed grupę zasobów zawierającą rozszerzenia maszyny wirtualnej, kilka elementów należy rozważyć, takich jak zgodność rozszerzenia i chronionych ustawień.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="5bd1f-107">Szczegóły tego dokumentu działania procesu eksportowania grupy zasobów dotyczących rozszerzenia maszyny wirtualnej, łącznie z listą obsługiwanych rozszerzeń, a szczegóły dotyczące obsługi zabezpieczonych danych.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="5bd1f-108">Rozszerzenia obsługiwanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="5bd1f-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="5bd1f-109">Dostępnych jest wiele rozszerzeń maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="5bd1f-110">Nie wszystkie rozszerzenia mogą być eksportowane do szablonu usługi Resource Manager za pomocą funkcji "Skrypt automatyzacji".</span><span class="sxs-lookup"><span data-stu-id="5bd1f-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="5bd1f-111">Jeśli rozszerzenie maszyny wirtualnej nie jest obsługiwana, należy ręcznie można umieścić do wyeksportowanego szablonu.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="5bd1f-112">Następujące rozszerzenia można wyeksportować za pomocą funkcji skryptów automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="5bd1f-113">Wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="5bd1f-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="5bd1f-114">Kopia zapasowa Acronis</span><span class="sxs-lookup"><span data-stu-id="5bd1f-114">Acronis Backup</span></span> | <span data-ttu-id="5bd1f-115">Agent Datadog Windows</span><span class="sxs-lookup"><span data-stu-id="5bd1f-115">Datadog Windows Agent</span></span> | <span data-ttu-id="5bd1f-116">Stosowanie poprawek dla systemu Linux systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5bd1f-116">OS Patching For Linux</span></span> | <span data-ttu-id="5bd1f-117">Migawki maszyny Wirtualnej w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="5bd1f-118">Kopia zapasowa Acronis systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-118">Acronis Backup Linux</span></span> | <span data-ttu-id="5bd1f-119">Rozszerzenie docker</span><span class="sxs-lookup"><span data-stu-id="5bd1f-119">Docker Extension</span></span> | <span data-ttu-id="5bd1f-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="5bd1f-120">Puppet Agent</span></span> |
| <span data-ttu-id="5bd1f-121">Informacje o BG</span><span class="sxs-lookup"><span data-stu-id="5bd1f-121">Bg Info</span></span> | <span data-ttu-id="5bd1f-122">Rozszerzenie DSC</span><span class="sxs-lookup"><span data-stu-id="5bd1f-122">DSC Extension</span></span> | <span data-ttu-id="5bd1f-123">Szczegółowe informacje o lokacji 24 x 7 Apm</span><span class="sxs-lookup"><span data-stu-id="5bd1f-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="5bd1f-124">Linux Agent BMC CTM</span><span class="sxs-lookup"><span data-stu-id="5bd1f-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="5bd1f-125">Dynatrace systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-125">Dynatrace Linux</span></span> | <span data-ttu-id="5bd1f-126">24 x 7 Linux serwera lokacji</span><span class="sxs-lookup"><span data-stu-id="5bd1f-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="5bd1f-127">BMC CTM agenta w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="5bd1f-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="5bd1f-128">Dynatrace systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5bd1f-128">Dynatrace Windows</span></span> | <span data-ttu-id="5bd1f-129">Lokacja 24 x 7 systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="5bd1f-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="5bd1f-130">Chef klienta</span><span class="sxs-lookup"><span data-stu-id="5bd1f-130">Chef Client</span></span> | <span data-ttu-id="5bd1f-131">HPE zabezpieczeń aplikacji Defender</span><span class="sxs-lookup"><span data-stu-id="5bd1f-131">HPE Security Application Defender</span></span> | <span data-ttu-id="5bd1f-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="5bd1f-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="5bd1f-133">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="5bd1f-133">Custom Script</span></span> | <span data-ttu-id="5bd1f-134">IaaS ochrony przed złośliwym oprogramowaniem</span><span class="sxs-lookup"><span data-stu-id="5bd1f-134">IaaS Antimalware</span></span> | <span data-ttu-id="5bd1f-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="5bd1f-136">Rozszerzenie niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="5bd1f-136">Custom Script Extension</span></span> | <span data-ttu-id="5bd1f-137">Diagnostyka IaaS</span><span class="sxs-lookup"><span data-stu-id="5bd1f-137">IaaS Diagnostics</span></span> | <span data-ttu-id="5bd1f-138">Dostęp do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-138">VM Access For Linux</span></span> |
| <span data-ttu-id="5bd1f-139">Skryptu niestandardowego dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-139">Custom Script for Linux</span></span> | <span data-ttu-id="5bd1f-140">Linux Chef klienta</span><span class="sxs-lookup"><span data-stu-id="5bd1f-140">Linux Chef Client</span></span> | <span data-ttu-id="5bd1f-141">Dostęp do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-141">VM Access For Linux</span></span> |
| <span data-ttu-id="5bd1f-142">Datadog agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-142">Datadog Linux Agent</span></span> | <span data-ttu-id="5bd1f-143">Diagnostyka systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5bd1f-143">Linux Diagnostic</span></span> | <span data-ttu-id="5bd1f-144">Migawki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5bd1f-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="5bd1f-145">Eksportowanie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5bd1f-145">Export the Resource Group</span></span>

<span data-ttu-id="5bd1f-146">Aby wyeksportować grupy zasobów do szablonów wielokrotnego użytku, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bd1f-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="5bd1f-147">Logowanie się do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5bd1f-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="5bd1f-148">W Menu centralnym kliknij grup zasobów</span><span class="sxs-lookup"><span data-stu-id="5bd1f-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="5bd1f-149">Wybierz z listy docelowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5bd1f-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="5bd1f-150">W bloku grupy zasobów kliknij skryptu automatyzacji</span><span class="sxs-lookup"><span data-stu-id="5bd1f-150">In the Resource Group blade, click Automation Script</span></span>

![Eksportowanie szablonu](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="5bd1f-152">Skrypt automatyzacji Azure Resource Manager tworzy szablon usługi Resource Manager, pliku parametrów i skrypty wdrażania przykładowe, takie jak środowiska PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="5bd1f-153">W tym momencie wyeksportowanego szablonu można pobrać za pomocą przycisku pobierania, dodać jako nowy szablon Biblioteka szablonów lub wdrożone za pomocą przycisku Wdróż.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="5bd1f-154">Skonfiguruj ustawienia chronionego</span><span class="sxs-lookup"><span data-stu-id="5bd1f-154">Configure protected settings</span></span>

<span data-ttu-id="5bd1f-155">Wiele rozszerzeń maszyny wirtualnej platformy Azure obejmują konfiguracji chronionych ustawień, który szyfruje dane poufne, na przykład poświadczenia i parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="5bd1f-156">Ustawienia chronionych nie są eksportowane z skryptów automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="5bd1f-157">Jeśli konieczne, chronionych ustawień należy ponownie do wyeksportowanego szablonu.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="5bd1f-158">Krok 1 — Usuń parametr szablonu</span><span class="sxs-lookup"><span data-stu-id="5bd1f-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="5bd1f-159">Po wyeksportowaniu grupy zasobów, tworzona jest parametrem jednego szablonu podawanie wartości do wyeksportowanych ustawieniach chronionych.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="5bd1f-160">Ten parametr może zostać usunięta.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-160">This parameter can be removed.</span></span> <span data-ttu-id="5bd1f-161">Aby usunąć parametr, Przejrzyj listy parametrów i Usuń parametr, który wygląda podobnie jak w tym przykładzie JSON.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="5bd1f-162">Krok 2 - Get chronione ustawienia właściwości</span><span class="sxs-lookup"><span data-stu-id="5bd1f-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="5bd1f-163">Ponieważ każdy chroniony ustawienie ma zestaw właściwości wymagane, należy zebrać listę tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="5bd1f-164">Każdy parametr chronionych ustawień konfiguracji można znaleźć w [schematu usługi Azure Resource Manager w witrynie GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="5bd1f-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="5bd1f-165">Ten schemat zawiera tylko zestawy parametrów dla rozszerzeń wymienionych w sekcji Przegląd tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="5bd1f-166">Od w ramach schematu repozytorium, wyszukaj żądane rozszerzenie, w tym przykładzie `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="5bd1f-167">Raz rozszerzenia `protectedSettings` obiektu została znaleziona, zanotuj każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="5bd1f-168">W przykładzie `IaasDiagnostic` rozszerzenia, wymagają parametry są `storageAccountName`, `storageAccountKey`, i `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="5bd1f-169">Krok 3 — ponownie utworzyć konfigurację chronionych</span><span class="sxs-lookup"><span data-stu-id="5bd1f-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="5bd1f-170">W wyeksportowanego szablonu, wyszukaj `protectedSettings` i Zastąp wyeksportowanego ustawiania chronionego obiektu nową zawierający parametry wymagane rozszerzenie i wartość dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="5bd1f-171">W przykładzie `IaasDiagnostic` rozszerzenia, nowej konfiguracji chronionych ustawienie będzie wyglądać jak w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="5bd1f-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="5bd1f-172">Zasób rozszerzeniem końcowym wygląda podobnie do poniższego przykładu JSON:</span><span class="sxs-lookup"><span data-stu-id="5bd1f-172">The final extension resource looks similar to the following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="5bd1f-173">Aby zapewnić wartości właściwości przy użyciu parametrów szablonu, te muszą zostać utworzone.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="5bd1f-174">Podczas tworzenia parametrów szablonu dla chronionych ustawiania wartości, upewnij się, że użyj `SecureString` typ parametru, tak aby poufnych wartości są chronione.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="5bd1f-175">Aby uzyskać więcej informacji na temat używania parametrów, zobacz [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5bd1f-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5bd1f-176">W przykładzie `IaasDiagnostic` rozszerzenia, następujące parametry zostałyby utworzone w sekcji parametrów szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="5bd1f-177">W tym momencie szablonu można wdrożyć przy użyciu dowolnej metody wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="5bd1f-177">At this point, the template can be deployed using any template deployment method.</span></span>
