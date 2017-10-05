---
title: "Wdrażanie aplikacji na zestawy skalowania maszyny wirtualnej"
description: "Użyj rozszerzenia depoy aplikację na zestawy skalowania maszyny wirtualnej Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="ad9d1-103">Wdrażanie aplikacji na zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ad9d1-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="ad9d1-104">W tym artykule opisano różne sposoby jak zainstalować oprogramowanie, w tym czasie są obsługiwane przez zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="ad9d1-105">Warto przejrzeć [Omówienie projektowania zestaw skali](virtual-machine-scale-sets-design-overview.md) artykułu, który opisano niektóre ograniczenia narzucone przez zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="ad9d1-106">Użyć obrazu</span><span class="sxs-lookup"><span data-stu-id="ad9d1-106">Capture and reuse an image</span></span>

<span data-ttu-id="ad9d1-107">Można użyć maszyny wirtualnej, zdefiniowanych na platformie Azure, aby przygotować obraz podstawowy na skalę.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="ad9d1-108">Ten proces tworzy dysków zarządzanych na Twoim koncie magazynu, który może odwoływać się jako obrazu podstawowego zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="ad9d1-109">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ad9d1-109">Do the following steps:</span></span>

1. <span data-ttu-id="ad9d1-110">Utwórz maszynę wirtualną platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ad9d1-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="ad9d1-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="ad9d1-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="ad9d1-112">[Systemu Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="ad9d1-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="ad9d1-113">Zdalnego do maszyny wirtualnej i Dostosuj system do potrzeb użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="ad9d1-114">Jeśli chcesz, należy zainstalować aplikację teraz.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-114">If you want, you can install your application now.</span></span> <span data-ttu-id="ad9d1-115">Jednak pamiętać, że instalując swoją aplikację już teraz, może wprowadzić uaktualniania aplikacji bardziej skomplikowane, ponieważ trzeba najpierw usuń.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="ad9d1-116">Zamiast tego można użyć tego kroku można zainstalować wszystkie wymagania wstępne, które mogą być potrzebne aplikacji, takich jak określonej funkcji środowiska uruchomieniowego lub systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="ad9d1-117">Czynności opisane w samouczku "Przechwytywanie maszyny" dla dowolnego [Linux] [ linux-vm-capture] lub [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="ad9d1-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="ad9d1-118">Utwórz [zestawu skalowania maszyn wirtualnych] [ vmss-create] z obrazem URI przechwycone w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="ad9d1-119">Aby uzyskać więcej informacji dotyczących dysków, zobacz [omówienie dysków zarządzanych](../virtual-machines/windows/managed-disks-overview.md) i [używać dołączonych dysków danych](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="ad9d1-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="ad9d1-120">Zainstaluj po udostępnieniu zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="ad9d1-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="ad9d1-121">Rozszerzenia maszyn wirtualnych może odnosić się do zestawu skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="ad9d1-122">Za pomocą rozszerzenia maszyny wirtualnej można dostosowywać maszyn wirtualnych w skali Ustaw jako całej grupy.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="ad9d1-123">Aby uzyskać więcej informacji na temat rozszerzeń, zobacz [rozszerzenia maszyny wirtualnej](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad9d1-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ad9d1-124">Istnieją trzy główne rozszerzeń, których można używać, w zależności od Jeśli system operacyjny jest oparty na systemie Linux lub z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="ad9d1-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ad9d1-125">Windows</span></span>

<span data-ttu-id="ad9d1-126">Dla systemu operacyjnego z systemem Windows, użyj **v1.8 niestandardowego skryptu** rozszerzenia, lub **DSC środowiska PowerShell** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="ad9d1-127">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="ad9d1-127">Custom Script</span></span>

<span data-ttu-id="ad9d1-128">Rozszerzenie skryptu niestandardowego uruchamia skrypt w każdym wystąpieniu maszyny wirtualnej w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="ad9d1-129">Pliku konfiguracji lub zmienna wskazuje, które pliki są pobierane do maszyny wirtualnej, a następnie jakie polecenia uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="ad9d1-130">Aby uruchomić Instalatora, skrypt, plik wsadowy każdego pliku wykonywalnego, na przykład może wykorzystać tę.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="ad9d1-131">PowerShell korzysta z tablicy skrótów dla ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="ad9d1-132">Ten przykład Konfiguruje rozszerzenia niestandardowego skryptu, aby uruchomić skrypt programu PowerShell, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="ad9d1-133">Użyj `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="ad9d1-134">Azure CLI używa pliku json dla ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="ad9d1-135">Ten przykład Konfiguruje rozszerzenia niestandardowego skryptu, aby uruchomić skrypt programu PowerShell, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="ad9d1-136">Zapisz plik json następujące jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="ad9d1-137">Następnie uruchom to polecenie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ad9d1-138">Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="ad9d1-139">DSC środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad9d1-139">PowerShell DSC</span></span>

<span data-ttu-id="ad9d1-140">DSC środowiska PowerShell umożliwia dostosowywanie wystąpień maszyny wirtualnej zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="ad9d1-141">**DSC** rozszerzenia opublikowanych przez **Microsoft.Powershell** wdraża i uruchamia Podana konfiguracja DSC w każdym wystąpieniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="ad9d1-142">Pliku konfiguracji lub zmienna Określa, że rozszerzenie gdzie *zip* jest pakietu i które _funkcji skryptu_ kombinacja do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="ad9d1-143">PowerShell korzysta z tablicy skrótów dla ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="ad9d1-144">W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="ad9d1-145">Użyj `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="ad9d1-146">Azure CLI używa json dla ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="ad9d1-147">W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="ad9d1-148">Zapisz plik json następujące jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="ad9d1-149">Następnie uruchom to polecenie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ad9d1-150">Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="ad9d1-151">Linux</span><span class="sxs-lookup"><span data-stu-id="ad9d1-151">Linux</span></span>

<span data-ttu-id="ad9d1-152">Linux można użyć dowolnego **v2.0 niestandardowego skryptu** rozszerzenia lub użyj **init chmury** podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="ad9d1-153">Niestandardowego skryptu jest proste rozszerzenia, które pobiera pliki do wystąpień maszyny wirtualnej i wykonuje polecenie.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="ad9d1-154">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="ad9d1-154">Custom Script</span></span>

<span data-ttu-id="ad9d1-155">Zapisz plik json następujące jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="ad9d1-156">Użyj interfejsu wiersza polecenia Azure, aby dodać to rozszerzenie do istniejącego zestawu skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="ad9d1-157">Każda maszyna wirtualna w skali ustawiane automatycznie uruchamia rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ad9d1-158">Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="ad9d1-159">Init chmury</span><span class="sxs-lookup"><span data-stu-id="ad9d1-159">Cloud-Init</span></span>

<span data-ttu-id="ad9d1-160">Init chmury jest używany podczas tworzenia zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="ad9d1-161">Najpierw należy utworzyć lokalnego pliku o nazwie _init.txt chmury_ i Dodaj do niej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="ad9d1-162">Na przykład, zobacz [tego gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="ad9d1-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="ad9d1-163">Użyj interfejsu wiersza polecenia Azure, aby utworzyć zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="ad9d1-164">`--custom-data` Polu można wprowadzić nazwę pliku skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="ad9d1-165">Jak zarządzać aktualizacji aplikacji?</span><span class="sxs-lookup"><span data-stu-id="ad9d1-165">How do I manage application updates?</span></span>

<span data-ttu-id="ad9d1-166">Jeśli wdrożono aplikację za pomocą rozszerzenia, należy zmienić definicji rozszerzenia w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="ad9d1-167">Ta zmiana powoduje, że rozszerzenie ponownego wdrożenia dla wszystkich wystąpień maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="ad9d1-168">Coś **musi** można zmienić o rozszerzeniu, takie jak zmiana nazwy pliku do którego istnieje odwołanie, w przeciwnym razie ma Azure nie można znaleźć rozszerzenia o zmianie.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="ad9d1-169">Jeśli aplikacja jest rozszerzania do obrazu systemu operacyjnego, należy użyć potoku automatycznego wdrażania aktualizacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="ad9d1-170">Projekt architektury ułatwia szybkie wymiany przemieszczanego skali, ustaw w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="ad9d1-171">Dobrym przykładem tego podejścia jest [Azure Spinnaker sterownik pracy](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="ad9d1-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="ad9d1-172">[Pakujący](https://www.packer.io/) i [Terraform](https://www.terraform.io/) pomocy technicznej usługi Azure Resource Manager, można również zdefiniować obrazów "jako kod" i je kompilować na platformie Azure, następnie użyć wirtualnego dysku twardego w zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="ad9d1-173">Jednak to tak staje się powodować problemy dla obrazów witryny marketplace, kiedy rozszerzenia/niestandardowe skrypty stać się ważniejsze od usługi bits z witryny marketplace nie zmieniać bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="ad9d1-174">Co się stanie po zestawu skalowania skaluje się?</span><span class="sxs-lookup"><span data-stu-id="ad9d1-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="ad9d1-175">Aplikacja jest instalowana automatycznie po dodaniu co najmniej jednej maszyny wirtualnej do zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="ad9d1-176">Przykład, jeśli wartość skali ma rozszerzenia zdefiniowane, są uruchamiane na nowej maszynie wirtualnej każdym razem, gdy jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="ad9d1-177">Jeśli zestaw skalowania jest oparta na obraz niestandardowy, wszelkie nowej maszyny wirtualnej jest kopią niestandardowego obrazu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="ad9d1-178">Jeśli kontener hosty maszyn wirtualnych zestawu skalowania, może być uruchamianie kodu w celu załadowania kontenerów w niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="ad9d1-179">Lub rozszerzenie może zainstalować agenta, który rejestruje z programem orchestrator klastra, takie jak usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="ad9d1-180">Jak wdrożeniem aktualizacji systemu operacyjnego między domenami aktualizacji?</span><span class="sxs-lookup"><span data-stu-id="ad9d1-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="ad9d1-181">Załóżmy, że chcesz zaktualizować obraz systemu operacyjnego przy zachowaniu zestaw systemem skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="ad9d1-182">PowerShell i interfejsu wiersza polecenia Azure można zaktualizować obrazy maszyny wirtualnej, maszyn wirtualnych jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="ad9d1-183">[Uaktualnienia zestawu skalowania maszyn wirtualnych](./virtual-machine-scale-sets-upgrade-scale-set.md) artykuł zawiera również dodatkowe informacje na jakie opcje są dostępne do uaktualnienia systemu operacyjnego przez zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad9d1-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad9d1-184">Next steps</span></span>

* [<span data-ttu-id="ad9d1-185">Użyj programu PowerShell do zarządzania zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="ad9d1-186">Utwórz szablon zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="ad9d1-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

