---
title: "aaaExporting grup zasobów Azure, która zawiera rozszerzenia maszyny Wirtualnej | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="627dc-103">Eksportowanie grupy zasobów, która zawiera rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="627dc-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="627dc-104">Grupy zasobów platformy Azure mogą być eksportowane do nowego szablonu usługi Resource Manager, które mogą być następnie wdrażane.</span><span class="sxs-lookup"><span data-stu-id="627dc-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="627dc-105">Witaj procesu eksportu interpretuje istniejących zasobów i tworzy szablonu usługi Resource Manager która po wdrożeniu powoduje podobne grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="627dc-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="627dc-106">Korzystając z opcji eksportu grupy zasobów hello przed grupę zasobów zawierającą rozszerzenia maszyny wirtualnej, kilka elementów potrzeby toobe uznawane za takich jak zgodność rozszerzenia i chronionych ustawień.</span><span class="sxs-lookup"><span data-stu-id="627dc-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="627dc-107">Szczegóły tego dokumentu, jak działa hello procesu eksportu grupy zasobów dotyczących rozszerzenia maszyny wirtualnej, łącznie z listą obsługiwanych rozszerzeń, a szczegóły dotyczące obsługi zabezpieczonych danych.</span><span class="sxs-lookup"><span data-stu-id="627dc-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="627dc-108">Rozszerzenia obsługiwanych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="627dc-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="627dc-109">Dostępnych jest wiele rozszerzeń maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="627dc-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="627dc-110">Nie wszystkie rozszerzenia mogą być eksportowane do szablonu usługi Resource Manager za pomocą funkcji "Skrypt automatyzacji" hello.</span><span class="sxs-lookup"><span data-stu-id="627dc-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="627dc-111">Jeśli rozszerzenie maszyny wirtualnej nie jest obsługiwana, musi on toobe ręcznie umieścić do wyeksportowanego szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="627dc-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="627dc-112">Witaj następujących rozszerzeń można eksportować z funkcją skryptów automatyzacji hello.</span><span class="sxs-lookup"><span data-stu-id="627dc-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="627dc-113">Wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="627dc-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="627dc-114">Kopia zapasowa Acronis</span><span class="sxs-lookup"><span data-stu-id="627dc-114">Acronis Backup</span></span> | <span data-ttu-id="627dc-115">Agent Datadog Windows</span><span class="sxs-lookup"><span data-stu-id="627dc-115">Datadog Windows Agent</span></span> | <span data-ttu-id="627dc-116">Stosowanie poprawek dla systemu Linux systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="627dc-116">OS Patching For Linux</span></span> | <span data-ttu-id="627dc-117">Migawki maszyny Wirtualnej w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="627dc-118">Kopia zapasowa Acronis systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-118">Acronis Backup Linux</span></span> | <span data-ttu-id="627dc-119">Rozszerzenie docker</span><span class="sxs-lookup"><span data-stu-id="627dc-119">Docker Extension</span></span> | <span data-ttu-id="627dc-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="627dc-120">Puppet Agent</span></span> |
| <span data-ttu-id="627dc-121">Informacje o BG</span><span class="sxs-lookup"><span data-stu-id="627dc-121">Bg Info</span></span> | <span data-ttu-id="627dc-122">Rozszerzenie DSC</span><span class="sxs-lookup"><span data-stu-id="627dc-122">DSC Extension</span></span> | <span data-ttu-id="627dc-123">Szczegółowe informacje o lokacji 24 x 7 Apm</span><span class="sxs-lookup"><span data-stu-id="627dc-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="627dc-124">Linux Agent BMC CTM</span><span class="sxs-lookup"><span data-stu-id="627dc-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="627dc-125">Dynatrace systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-125">Dynatrace Linux</span></span> | <span data-ttu-id="627dc-126">24 x 7 Linux serwera lokacji</span><span class="sxs-lookup"><span data-stu-id="627dc-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="627dc-127">BMC CTM agenta w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="627dc-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="627dc-128">Dynatrace systemu Windows</span><span class="sxs-lookup"><span data-stu-id="627dc-128">Dynatrace Windows</span></span> | <span data-ttu-id="627dc-129">Lokacja 24 x 7 systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="627dc-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="627dc-130">Chef klienta</span><span class="sxs-lookup"><span data-stu-id="627dc-130">Chef Client</span></span> | <span data-ttu-id="627dc-131">HPE zabezpieczeń aplikacji Defender</span><span class="sxs-lookup"><span data-stu-id="627dc-131">HPE Security Application Defender</span></span> | <span data-ttu-id="627dc-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="627dc-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="627dc-133">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="627dc-133">Custom Script</span></span> | <span data-ttu-id="627dc-134">IaaS ochrony przed złośliwym oprogramowaniem</span><span class="sxs-lookup"><span data-stu-id="627dc-134">IaaS Antimalware</span></span> | <span data-ttu-id="627dc-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="627dc-136">Rozszerzenie niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="627dc-136">Custom Script Extension</span></span> | <span data-ttu-id="627dc-137">Diagnostyka IaaS</span><span class="sxs-lookup"><span data-stu-id="627dc-137">IaaS Diagnostics</span></span> | <span data-ttu-id="627dc-138">Dostęp do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-138">VM Access For Linux</span></span> |
| <span data-ttu-id="627dc-139">Skryptu niestandardowego dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-139">Custom Script for Linux</span></span> | <span data-ttu-id="627dc-140">Linux Chef klienta</span><span class="sxs-lookup"><span data-stu-id="627dc-140">Linux Chef Client</span></span> | <span data-ttu-id="627dc-141">Dostęp do maszyny Wirtualnej dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-141">VM Access For Linux</span></span> |
| <span data-ttu-id="627dc-142">Datadog agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-142">Datadog Linux Agent</span></span> | <span data-ttu-id="627dc-143">Diagnostyka systemu Linux</span><span class="sxs-lookup"><span data-stu-id="627dc-143">Linux Diagnostic</span></span> | <span data-ttu-id="627dc-144">Migawki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="627dc-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="627dc-145">Eksportuj hello grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="627dc-145">Export hello Resource Group</span></span>

<span data-ttu-id="627dc-146">tooexport grupę zasobów do szablonu wielokrotnego użytku, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="627dc-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="627dc-147">Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="627dc-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="627dc-148">W Menu centralnym hello kliknij polecenie grup zasobów</span><span class="sxs-lookup"><span data-stu-id="627dc-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="627dc-149">Wybierz z listy hello hello docelowa grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="627dc-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="627dc-150">W bloku grupy zasobów powitania kliknij skryptu automatyzacji</span><span class="sxs-lookup"><span data-stu-id="627dc-150">In hello Resource Group blade, click Automation Script</span></span>

![Eksportowanie szablonu](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="627dc-152">Witaj skryptów automatyzacji Azure Resource Manager tworzy szablonu usługi Resource Manager, pliku parametrów i skrypty wdrażania przykładowe, takie jak środowiska PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="627dc-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="627dc-153">W tym momencie hello wyeksportowanego szablonu można pobrać za pomocą przycisku pobierania hello, dodany jako nowy szablon biblioteki toohello szablonu, lub ponownej instalacji przy użyciu hello wdrażanie przycisku.</span><span class="sxs-lookup"><span data-stu-id="627dc-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="627dc-154">Skonfiguruj ustawienia chronionego</span><span class="sxs-lookup"><span data-stu-id="627dc-154">Configure protected settings</span></span>

<span data-ttu-id="627dc-155">Wiele rozszerzeń maszyny wirtualnej platformy Azure obejmują konfiguracji chronionych ustawień, który szyfruje dane poufne, na przykład poświadczenia i parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="627dc-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="627dc-156">Ustawienia chronionych nie są eksportowane z hello skryptów automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="627dc-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="627dc-157">Jeśli konieczne, chronionych ustawienia należy ponownie wstawić do hello toobe eksportowane szablonem.</span><span class="sxs-lookup"><span data-stu-id="627dc-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="627dc-158">Krok 1 — Usuń parametr szablonu</span><span class="sxs-lookup"><span data-stu-id="627dc-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="627dc-159">Podczas tworzenia tooprovide powitalne grupy zasobów jest eksportowany, parametr jednego szablonu toohello wartość wyeksportowane ustawienia chronionych.</span><span class="sxs-lookup"><span data-stu-id="627dc-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="627dc-160">Ten parametr może zostać usunięta.</span><span class="sxs-lookup"><span data-stu-id="627dc-160">This parameter can be removed.</span></span> <span data-ttu-id="627dc-161">Parametr hello tooremove, przejrzyj listę parametrów hello i usunąć parametr hello, która wygląda podobnie przykład JSON toothis.</span><span class="sxs-lookup"><span data-stu-id="627dc-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="627dc-162">Krok 2 - Get chronione ustawienia właściwości</span><span class="sxs-lookup"><span data-stu-id="627dc-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="627dc-163">Ponieważ każdy chroniony ustawienie ma zestaw właściwości wymagane, listę tych właściwości muszą toobe zebrane.</span><span class="sxs-lookup"><span data-stu-id="627dc-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="627dc-164">Każdy parametr hello chronionych ustawień konfiguracji można znaleźć w hello [schematu usługi Azure Resource Manager w witrynie GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="627dc-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="627dc-165">Ten schemat zawiera tylko zestawy parametrów hello rozszerzeń hello wymienione w sekcji Przegląd hello tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="627dc-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="627dc-166">Z wewnątrz hello schematu repozytorium, wyszukaj rozszerzenie hello potrzebne, w tym przykładzie `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="627dc-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="627dc-167">Raz hello rozszerzenia `protectedSettings` obiektu została znaleziona, zanotuj każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="627dc-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="627dc-168">W przykładzie hello hello `IaasDiagnostic` hello rozszerzenia, wymagają parametry są `storageAccountName`, `storageAccountKey`, i `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="627dc-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="627dc-169">Krok 3 — odtworzyć konfiguracji hello chronione</span><span class="sxs-lookup"><span data-stu-id="627dc-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="627dc-170">Na hello wyeksportowanego szablonu, wyszukiwanie `protectedSettings` i Zastąp hello wyeksportowanego ustawiania chronionego obiektu nowy obejmującej hello wymagane rozszerzenie parametrów i wartości dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="627dc-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="627dc-171">W przykładzie hello hello `IaasDiagnostic` rozszerzenia, nowej konfiguracji chronionych ustawienie hello będzie wyglądała hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="627dc-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="627dc-172">Hello rozszerzeniem końcowym zasobów wygląda podobnie toohello poniższy przykład JSON:</span><span class="sxs-lookup"><span data-stu-id="627dc-172">hello final extension resource looks similar toohello following JSON example:</span></span>

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

<span data-ttu-id="627dc-173">Jeśli przy użyciu wartości właściwości tooprovide parametrów szablonu, te czynności toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="627dc-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="627dc-174">Podczas tworzenia parametrów szablonu dla chronionych ustawiania wartości, upewnij się, że hello toouse `SecureString` typ parametru, tak aby poufnych wartości są chronione.</span><span class="sxs-lookup"><span data-stu-id="627dc-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="627dc-175">Aby uzyskać więcej informacji na temat używania parametrów, zobacz [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="627dc-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="627dc-176">W przykładzie hello hello `IaasDiagnostic` rozszerzenia, hello następujące parametry zostałyby utworzone w sekcji parametrów hello hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="627dc-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

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

<span data-ttu-id="627dc-177">W tym momencie hello szablonu można wdrożyć przy użyciu dowolnej metody wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="627dc-177">At this point, hello template can be deployed using any template deployment method.</span></span>
