---
title: aaaCustom rozszerzenia skryptu na maszynie Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft
description: "Automatyzowanie zadań konfiguracji maszyny Wirtualnej platformy Azure za pomocą skryptów programu PowerShell toorun rozszerzenia niestandardowego skryptu hello na zdalnej maszynie Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="f146b-103">Niestandardowych skryptów rozszerzenia dla systemu Windows za pomocą hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="f146b-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f146b-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f146b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f146b-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="f146b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f146b-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f146b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f146b-107">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f146b-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f146b-108">Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="f146b-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="f146b-109">To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f146b-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f146b-110">Skryptów można pobrać z magazynu Azure lub usługi GitHub lub podane toohello portalu Azure w rozszerzeniu czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f146b-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="f146b-111">Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f146b-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f146b-112">Ten dokument zawiera szczegóły, jak za pomocą niestandardowego rozszerzenia skryptu hello toouse hello modułu Azure PowerShell, szablony usługi Azure Resource Manager i szczegóły dotyczące rozwiązywania problemów z systemów Windows.</span><span class="sxs-lookup"><span data-stu-id="f146b-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f146b-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f146b-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f146b-114">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="f146b-114">Operating System</span></span>

<span data-ttu-id="f146b-115">Witaj niestandardowe rozszerzenie skryptu dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.</span><span class="sxs-lookup"><span data-stu-id="f146b-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="f146b-116">Lokalizacja skryptu</span><span class="sxs-lookup"><span data-stu-id="f146b-116">Script Location</span></span>

<span data-ttu-id="f146b-117">skrypt Hello musi toobe przechowywanych w magazynu Azure lub innej lokalizacji dostępny za pośrednictwem prawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="f146b-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f146b-118">Połączenie z Internetem</span><span class="sxs-lookup"><span data-stu-id="f146b-118">Internet Connectivity</span></span>

<span data-ttu-id="f146b-119">Hello niestandardowe rozszerzenie skryptu systemu Windows wymaga tego hello docelowej maszyny wirtualnej jest toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="f146b-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="f146b-120">Rozszerzenie schematu</span><span class="sxs-lookup"><span data-stu-id="f146b-120">Extension schema</span></span>

<span data-ttu-id="f146b-121">Witaj JSON następujące zawiera schemat hello hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="f146b-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="f146b-122">rozszerzenie Hello wymaga lokalizacji skryptu (magazynu Azure lub innej lokalizacji z prawidłowym adresem URL) i tooexecute polecenia.</span><span class="sxs-lookup"><span data-stu-id="f146b-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="f146b-123">Jeśli jako źródło skryptu hello przy użyciu usługi Azure Storage, usługa Azure storage konta nazwy i klucza konta jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="f146b-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="f146b-124">Te elementy powinny traktowane jako poufne dane i określony w konfiguracji chronionych ustawień rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="f146b-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="f146b-125">Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f146b-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="f146b-126">Wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="f146b-126">Property values</span></span>

| <span data-ttu-id="f146b-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f146b-127">Name</span></span> | <span data-ttu-id="f146b-128">Wartość / przykład</span><span class="sxs-lookup"><span data-stu-id="f146b-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f146b-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f146b-129">apiVersion</span></span> | <span data-ttu-id="f146b-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f146b-130">2015-06-15</span></span> |
| <span data-ttu-id="f146b-131">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="f146b-131">publisher</span></span> | <span data-ttu-id="f146b-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="f146b-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="f146b-133">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f146b-133">extension</span></span> | <span data-ttu-id="f146b-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="f146b-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="f146b-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f146b-135">typeHandlerVersion</span></span> | <span data-ttu-id="f146b-136">1.8</span><span class="sxs-lookup"><span data-stu-id="f146b-136">1.8</span></span> |
| <span data-ttu-id="f146b-137">fileUris (np.)</span><span class="sxs-lookup"><span data-stu-id="f146b-137">fileUris (e.g)</span></span> | <span data-ttu-id="f146b-138">https://RAW.githubusercontent.com/Microsoft/DotNet-Core-Sample-Templates/Master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1</span><span class="sxs-lookup"><span data-stu-id="f146b-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="f146b-139">commandToExecute (np.)</span><span class="sxs-lookup"><span data-stu-id="f146b-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="f146b-140">PowerShell - ExecutionPolicy Unrestricted - pliku skonfigurować muzyka app.ps1</span><span class="sxs-lookup"><span data-stu-id="f146b-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="f146b-141">Wdrażanie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="f146b-141">Template deployment</span></span>

<span data-ttu-id="f146b-142">Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f146b-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f146b-143">można schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w hello toorun szablonu usługi Azure Resource Manager niestandardowe rozszerzenie skryptu podczas wdrażania szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f146b-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="f146b-144">Przykładowy szablon, który obejmuje hello niestandardowe rozszerzenie skryptu można znaleźć tutaj, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="f146b-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="f146b-145">Wdrożenie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f146b-145">PowerShell deployment</span></span>

<span data-ttu-id="f146b-146">Witaj `Set-AzureVMCustomScriptExtension` polecenie może być używane tooadd hello niestandardowego skryptu rozszerzenia tooan istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f146b-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="f146b-147">Aby uzyskać więcej informacji, zobacz [AzureRmVMCustomScriptExtension zestawu ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="f146b-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="f146b-148">Rozwiązywanie problemów i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="f146b-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="f146b-149">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f146b-149">Troubleshoot</span></span>

<span data-ttu-id="f146b-150">Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f146b-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="f146b-151">Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="f146b-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="f146b-152">Wykonanie rozszerzenia output nam toofiles zarejestrowane w hello następującego katalogu na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f146b-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="f146b-153">sam skrypt Hello jest pobierany na powitania po katalogu na powitania docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f146b-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="f146b-154">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="f146b-154">Support</span></span>

<span data-ttu-id="f146b-155">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f146b-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f146b-156">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f146b-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f146b-157">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="f146b-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f146b-158">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f146b-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
