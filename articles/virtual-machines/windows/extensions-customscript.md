---
title: aaaAzure niestandardowe rozszerzenie skryptu systemu Windows | Dokumentacja firmy Microsoft
description: "Automatyzowanie zadań konfiguracji maszyny Wirtualnej systemu Windows przy użyciu rozszerzenia niestandardowego skryptu hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="f9d37-103">Niestandardowe rozszerzenie skryptu dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f9d37-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="f9d37-104">Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d37-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="f9d37-105">To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f9d37-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f9d37-106">Skryptów można pobrać z magazynu Azure lub usługi GitHub lub podane toohello portalu Azure w rozszerzeniu czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f9d37-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="f9d37-107">Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d37-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f9d37-108">Ten dokument zawiera szczegóły, jak za pomocą niestandardowego rozszerzenia skryptu hello toouse hello modułu Azure PowerShell, szablony usługi Azure Resource Manager i szczegóły dotyczące rozwiązywania problemów z systemów Windows.</span><span class="sxs-lookup"><span data-stu-id="f9d37-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9d37-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9d37-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f9d37-110">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="f9d37-110">Operating System</span></span>

<span data-ttu-id="f9d37-111">Witaj niestandardowe rozszerzenie skryptu dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.</span><span class="sxs-lookup"><span data-stu-id="f9d37-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="f9d37-112">Lokalizacja skryptu</span><span class="sxs-lookup"><span data-stu-id="f9d37-112">Script Location</span></span>

<span data-ttu-id="f9d37-113">skrypt Hello musi toobe przechowywane w magazynie obiektów Blob Azure lub w innej lokalizacji dostępny za pośrednictwem prawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="f9d37-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f9d37-114">Połączenie z Internetem</span><span class="sxs-lookup"><span data-stu-id="f9d37-114">Internet Connectivity</span></span>

<span data-ttu-id="f9d37-115">Hello niestandardowe rozszerzenie skryptu systemu Windows wymaga tego hello docelowej maszyny wirtualnej jest toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="f9d37-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="f9d37-116">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="f9d37-116">Extension schema</span></span>

<span data-ttu-id="f9d37-117">Witaj JSON następujące zawiera schemat hello hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="f9d37-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="f9d37-118">rozszerzenie Hello wymaga lokalizacji skryptu (magazynu Azure lub innej lokalizacji z prawidłowym adresem URL) i tooexecute polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9d37-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="f9d37-119">Jeśli jako źródło skryptu hello przy użyciu usługi Azure Storage, usługa Azure storage konta nazwy i klucza konta jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="f9d37-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="f9d37-120">Te elementy powinny traktowane jako poufne dane i określony w konfiguracji chronionych ustawień rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="f9d37-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="f9d37-121">Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9d37-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="f9d37-122">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="f9d37-122">Property values</span></span>

| <span data-ttu-id="f9d37-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f9d37-123">Name</span></span> | <span data-ttu-id="f9d37-124">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="f9d37-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f9d37-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f9d37-125">apiVersion</span></span> | <span data-ttu-id="f9d37-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f9d37-126">2015-06-15</span></span> |
| <span data-ttu-id="f9d37-127">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="f9d37-127">publisher</span></span> | <span data-ttu-id="f9d37-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="f9d37-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="f9d37-129">type</span><span class="sxs-lookup"><span data-stu-id="f9d37-129">type</span></span> | <span data-ttu-id="f9d37-130">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f9d37-130">extensions</span></span> |
| <span data-ttu-id="f9d37-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f9d37-131">typeHandlerVersion</span></span> | <span data-ttu-id="f9d37-132">1.9</span><span class="sxs-lookup"><span data-stu-id="f9d37-132">1.9</span></span> |
| <span data-ttu-id="f9d37-133">fileUris (np.)</span><span class="sxs-lookup"><span data-stu-id="f9d37-133">fileUris (e.g)</span></span> | <span data-ttu-id="f9d37-134">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-Sample-Templates/Master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="f9d37-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="f9d37-135">commandToExecute (np.)</span><span class="sxs-lookup"><span data-stu-id="f9d37-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="f9d37-136">PowerShell - ExecutionPolicy Unrestricted - pliku skonfigurować muzyka app.ps1</span><span class="sxs-lookup"><span data-stu-id="f9d37-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="f9d37-137">storageAccountName (np.)</span><span class="sxs-lookup"><span data-stu-id="f9d37-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="f9d37-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="f9d37-138">examplestorageacct</span></span> |
| <span data-ttu-id="f9d37-139">storageAccountKey (np.)</span><span class="sxs-lookup"><span data-stu-id="f9d37-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="f9d37-140">TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg ==</span><span class="sxs-lookup"><span data-stu-id="f9d37-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="f9d37-141">**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f9d37-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="f9d37-142">Użyj nazwy hello, jak pokazano powyżej problemy z wdrażaniem tooavoid.</span><span class="sxs-lookup"><span data-stu-id="f9d37-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="f9d37-143">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="f9d37-143">Template deployment</span></span>

<span data-ttu-id="f9d37-144">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f9d37-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f9d37-145">można schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w hello toorun szablonu usługi Azure Resource Manager niestandardowe rozszerzenie skryptu podczas wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f9d37-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="f9d37-146">Przykładowy szablon, który obejmuje hello niestandardowe rozszerzenie skryptu można znaleźć tutaj, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="f9d37-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="f9d37-147">Wdrożenie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9d37-147">PowerShell deployment</span></span>

<span data-ttu-id="f9d37-148">Witaj `Set-AzureRmVMCustomScriptExtension` polecenie może być używane tooadd hello niestandardowego skryptu rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9d37-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="f9d37-149">Aby uzyskać więcej informacji, zobacz [AzureRmVMCustomScriptExtension zestawu ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="f9d37-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="f9d37-150">Rozwiązywanie problemów i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="f9d37-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="f9d37-151">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f9d37-151">Troubleshoot</span></span>

<span data-ttu-id="f9d37-152">Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f9d37-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="f9d37-153">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="f9d37-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="f9d37-154">Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles omówionych w artykule hello następującego katalogu na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9d37-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="f9d37-155">Witaj określony na powitania po katalog na docelowej maszynie wirtualnej hello są pobierane pliki.</span><span class="sxs-lookup"><span data-stu-id="f9d37-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="f9d37-156">gdzie `<n>` jest dziesiętną liczbą całkowitą, która może zmienić pomiędzy wykonaniami hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f9d37-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="f9d37-157">Witaj `1.*` wartość odpowiada bieżącej rzeczywiste hello `typeHandlerVersion` wartość hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f9d37-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="f9d37-158">Na przykład może być katalogowych hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="f9d37-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="f9d37-159">Podczas wykonywania hello `commandToExecute` polecenia rozszerzenia hello spowoduje ustawienie tego katalogu (np. `...\Downloads\2`) jako bieżący katalog roboczy hello.</span><span class="sxs-lookup"><span data-stu-id="f9d37-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="f9d37-160">Umożliwia zastosowanie hello ścieżek względnych toolocate hello pliki pobrane za pośrednictwem hello `fileURIs` właściwości.</span><span class="sxs-lookup"><span data-stu-id="f9d37-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="f9d37-161">Zobacz poniższą tabelę hello do przykłady.</span><span class="sxs-lookup"><span data-stu-id="f9d37-161">See hello table below for examples.</span></span>

<span data-ttu-id="f9d37-162">Ponieważ ścieżka bezwzględna pobierania hello mogą się zmieniać wraz z upływem czasu jest lepsze tooopt ścieżek względnych skryptów i plików w hello `commandToExecute` string, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="f9d37-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="f9d37-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f9d37-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="f9d37-164">Informacje o ścieżce po hello pierwszy segment identyfikatora URI są przechowywane pliki pobrane za pośrednictwem hello `fileUris` listy właściwości.</span><span class="sxs-lookup"><span data-stu-id="f9d37-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="f9d37-165">Jak pokazano w poniższej tabeli hello, pobierane pliki są mapowane do pobierania podkatalogów tooreflect hello struktury hello `fileUris` wartości.</span><span class="sxs-lookup"><span data-stu-id="f9d37-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="f9d37-166">Przykłady pobrane pliki</span><span class="sxs-lookup"><span data-stu-id="f9d37-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="f9d37-167">Identyfikator URI w fileUris</span><span class="sxs-lookup"><span data-stu-id="f9d37-167">URI in fileUris</span></span> | <span data-ttu-id="f9d37-168">Względne położenie pobrany</span><span class="sxs-lookup"><span data-stu-id="f9d37-168">Relative downloaded location</span></span> | <span data-ttu-id="f9d37-169">Bezwzględna pobrać lokalizację *</span><span class="sxs-lookup"><span data-stu-id="f9d37-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="f9d37-170">\*Jako powyżej, hello bezwzględne ścieżki katalogów zmieni hello okresu istnienia, hello maszyny Wirtualnej, ale nie w ramach pojedynczego uruchomienia rozszerzenia CustomScript hello.</span><span class="sxs-lookup"><span data-stu-id="f9d37-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="f9d37-171">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="f9d37-171">Support</span></span>

<span data-ttu-id="f9d37-172">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f9d37-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f9d37-173">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d37-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f9d37-174">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="f9d37-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f9d37-175">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f9d37-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
