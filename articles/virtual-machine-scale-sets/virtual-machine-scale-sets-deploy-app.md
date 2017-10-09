---
title: Ustawia aaaDeploy aplikacji w skali maszyny wirtualnej
description: "Użyj rozszerzenia toodepoy aplikację na zestawy skalowania maszyny wirtualnej Azure."
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="f8411-103">Wdrażanie aplikacji na zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f8411-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="f8411-104">W tym artykule opisano różne sposoby konfiguracji oprogramowania tooinstall na dużą skalę hello czasu hello są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f8411-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="f8411-105">Może być tooreview hello [Omówienie projektowania zestaw skali](virtual-machine-scale-sets-design-overview.md) artykułu, który opisano niektóre hello ograniczeń narzuconych przez zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8411-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="f8411-106">Użyć obrazu</span><span class="sxs-lookup"><span data-stu-id="f8411-106">Capture and reuse an image</span></span>

<span data-ttu-id="f8411-107">Można użyć ustawionych w Azure tooprepare obraz podstawowy dla Twojego skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8411-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="f8411-108">Ten proces tworzy dysków zarządzanych na Twoim koncie magazynu, który może odwoływać się jako obrazu podstawowego hello zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="f8411-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="f8411-109">Witaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f8411-109">Do hello following steps:</span></span>

1. <span data-ttu-id="f8411-110">Utwórz maszynę wirtualną platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f8411-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="f8411-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="f8411-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="f8411-112">[Systemu Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="f8411-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="f8411-113">Zdalne hello maszyny wirtualnej i dostosować hello systemu tooyour potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f8411-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="f8411-114">Jeśli chcesz, należy zainstalować aplikację teraz.</span><span class="sxs-lookup"><span data-stu-id="f8411-114">If you want, you can install your application now.</span></span> <span data-ttu-id="f8411-115">Jednak wiedzieć, że instalując swoją aplikację już teraz, użytkownik może utworzyć uaktualniania aplikacji bardziej skomplikowane, ponieważ może być konieczne tooremove jej pierwszym.</span><span class="sxs-lookup"><span data-stu-id="f8411-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="f8411-116">Zamiast tego można użyć tego kroku tooinstall wszystkie wymagania wstępne, które mogą być potrzebne aplikacji, takich jak określonej funkcji środowiska uruchomieniowego lub systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f8411-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="f8411-117">Czynności opisane w samouczku "Przechwytywanie maszyny" hello, w obu [Linux] [ linux-vm-capture] lub [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="f8411-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="f8411-118">Utwórz [zestawu skalowania maszyn wirtualnych] [ vmss-create] z hello obrazu przechwycone w poprzednim kroku hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="f8411-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="f8411-119">Aby uzyskać więcej informacji dotyczących dysków, zobacz [omówienie dysków zarządzanych](../virtual-machines/windows/managed-disks-overview.md) i [używać dołączonych dysków danych](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f8411-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="f8411-120">Zainstaluj po udostępnieniu hello zestaw skali</span><span class="sxs-lookup"><span data-stu-id="f8411-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="f8411-121">Rozszerzenia maszyn wirtualnych może być stosowane zestaw skali maszyny wirtualnej tooa.</span><span class="sxs-lookup"><span data-stu-id="f8411-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="f8411-122">Za pomocą rozszerzenia maszyny wirtualnej można dostosowywać hello maszyn wirtualnych w skali Ustaw jako całej grupy.</span><span class="sxs-lookup"><span data-stu-id="f8411-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="f8411-123">Aby uzyskać więcej informacji na temat rozszerzeń, zobacz [rozszerzenia maszyny wirtualnej](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8411-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f8411-124">Istnieją trzy główne rozszerzeń, których można używać, w zależności od Jeśli system operacyjny jest oparty na systemie Linux lub z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="f8411-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="f8411-125">Windows</span><span class="sxs-lookup"><span data-stu-id="f8411-125">Windows</span></span>

<span data-ttu-id="f8411-126">Dla systemu operacyjnego z systemem Windows, należy użyć albo hello **v1.8 niestandardowego skryptu** rozszerzenia lub hello **DSC środowiska PowerShell** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f8411-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="f8411-127">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="f8411-127">Custom Script</span></span>

<span data-ttu-id="f8411-128">Witaj rozszerzenia niestandardowego skryptu uruchamia skrypt w każdym wystąpieniu maszyny wirtualnej w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="f8411-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="f8411-129">Pliku konfiguracji lub zmienna wskazuje, które pliki są pobierane toohello maszyny wirtualnej, a następnie jakie polecenia uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="f8411-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="f8411-130">Na przykład można użyć tego Instalatora toorun, skrypt, pliku wsadowego lub każdego pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="f8411-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="f8411-131">PowerShell korzysta z ustawień hello obiektu hashtable.</span><span class="sxs-lookup"><span data-stu-id="f8411-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="f8411-132">Ten przykład konfiguruje hello skryptu niestandardowego rozszerzenia toorun skrypt programu PowerShell, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="f8411-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="f8411-133">Użyj hello `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="f8411-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="f8411-134">Azure CLI używa pliku json hello ustawień.</span><span class="sxs-lookup"><span data-stu-id="f8411-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="f8411-135">Ten przykład konfiguruje hello skryptu niestandardowego rozszerzenia toorun skrypt programu PowerShell, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="f8411-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="f8411-136">Zapisz hello następującego pliku json jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="f8411-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="f8411-137">Następnie uruchom to polecenie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8411-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="f8411-138">Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="f8411-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="f8411-139">DSC środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8411-139">PowerShell DSC</span></span>

<span data-ttu-id="f8411-140">Możesz użyć wystąpień maszyny wirtualnej zestawu skali hello toocustomize DSC środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8411-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="f8411-141">Witaj **DSC** rozszerzenia opublikowanych przez **Microsoft.Powershell** wdraża i uruchamia konfiguracji DSC hello podane w każdym wystąpieniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8411-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="f8411-142">Pliku konfiguracji lub zmienna Określa, że rozszerzenie hello gdzie *zip* jest pakietu i które _funkcji skryptu_ toorun kombinacji.</span><span class="sxs-lookup"><span data-stu-id="f8411-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="f8411-143">PowerShell korzysta z ustawień hello obiektu hashtable.</span><span class="sxs-lookup"><span data-stu-id="f8411-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="f8411-144">W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="f8411-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="f8411-145">Użyj hello `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="f8411-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="f8411-146">Azure CLI używa ustawienia hello json.</span><span class="sxs-lookup"><span data-stu-id="f8411-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="f8411-147">W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="f8411-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="f8411-148">Zapisz hello następującego pliku json jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="f8411-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="f8411-149">Następnie uruchom to polecenie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8411-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="f8411-150">Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="f8411-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="f8411-151">Linux</span><span class="sxs-lookup"><span data-stu-id="f8411-151">Linux</span></span>

<span data-ttu-id="f8411-152">Linux można użyć albo hello **v2.0 niestandardowego skryptu** rozszerzenia lub użyj **init chmury** podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="f8411-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="f8411-153">Niestandardowego skryptu jest proste rozszerzenia, które pobiera wystąpień maszyn wirtualnych toohello plików i wykonuje polecenie.</span><span class="sxs-lookup"><span data-stu-id="f8411-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="f8411-154">Niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="f8411-154">Custom Script</span></span>

<span data-ttu-id="f8411-155">Zapisz hello następującego pliku json jako _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="f8411-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="f8411-156">Użyj hello Azure CLI tooadd tego tooan rozszerzenia istniejący zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8411-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="f8411-157">Każda maszyna wirtualna w skali hello ustawić automatycznie uruchamia hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f8411-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="f8411-158">Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="f8411-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="f8411-159">Init chmury</span><span class="sxs-lookup"><span data-stu-id="f8411-159">Cloud-Init</span></span>

<span data-ttu-id="f8411-160">Init chmury jest używany podczas tworzenia zestawu skali hello.</span><span class="sxs-lookup"><span data-stu-id="f8411-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="f8411-161">Najpierw należy utworzyć lokalnego pliku o nazwie _init.txt chmury_ i dodać Twojego tooit konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f8411-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="f8411-162">Na przykład, zobacz [tego gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="f8411-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="f8411-163">Ustaw hello Użyj interfejsu wiersza polecenia Azure toocreate skali.</span><span class="sxs-lookup"><span data-stu-id="f8411-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="f8411-164">Witaj `--custom-data` pole akceptuje hello nazwa pliku skryptu init chmury.</span><span class="sxs-lookup"><span data-stu-id="f8411-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="f8411-165">Jak zarządzać aktualizacji aplikacji?</span><span class="sxs-lookup"><span data-stu-id="f8411-165">How do I manage application updates?</span></span>

<span data-ttu-id="f8411-166">Jeśli wdrożono aplikację za pomocą rozszerzenia zmiany definicji rozszerzenia hello w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="f8411-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="f8411-167">Ta zmiana powoduje, że wystąpień maszyn wirtualnych tooall hello rozszerzenia toobe ponownego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f8411-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="f8411-168">Coś **musi** można zmienić o rozszerzeniu hello, takie jak zmiana nazwy pliku do którego istnieje odwołanie, w przeciwnym razie ma Azure nie można znaleźć, który hello rozszerzenia została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="f8411-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="f8411-169">Jeśli aplikacja hello rozszerzania się do obrazu systemu operacyjnego, należy użyć potoku automatycznego wdrażania aktualizacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f8411-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="f8411-170">Projektowanie sieci toofacilitate architektura szybkiej wymiany przemieszczanego skali, ustaw w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f8411-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="f8411-171">Dobrym przykładem tego podejścia jest hello [Azure Spinnaker sterownik pracy](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="f8411-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="f8411-172">[Pakujący](https://www.packer.io/) i [Terraform](https://www.terraform.io/) pomocy technicznej usługi Azure Resource Manager, można również zdefiniować obrazów "jako kod" i je kompilować na platformie Azure, następnie użyć hello wirtualnego dysku twardego w zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="f8411-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="f8411-173">Jednak to tak staje się powodować problemy dla obrazów witryny marketplace, kiedy rozszerzenia/niestandardowe skrypty stać się ważniejsze od usługi bits z witryny marketplace nie zmieniać bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f8411-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="f8411-174">Co się stanie po zestawu skalowania skaluje się?</span><span class="sxs-lookup"><span data-stu-id="f8411-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="f8411-175">Aplikacja hello jest instalowana automatycznie podczas dodawania co najmniej jeden zestaw skalowania tooa maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f8411-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="f8411-176">Przykład, jeśli zestaw skalowania hello ma rozszerzenia zdefiniowane, są uruchamiane na nowej maszynie wirtualnej każdym razem, gdy jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="f8411-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="f8411-177">Jeśli zestaw skali hello jest oparta na obraz niestandardowy, wszelkie nowej maszyny wirtualnej jest kopią hello źródła niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="f8411-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="f8411-178">Jeśli maszyn wirtualnych zestawu skalowania hello hostów kontenera, może być uruchamiania kodu tooload hello kontenery w niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="f8411-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="f8411-179">Lub rozszerzenie może zainstalować agenta, który rejestruje z programem orchestrator klastra, takie jak usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8411-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="f8411-180">Jak wdrożeniem aktualizacji systemu operacyjnego między domenami aktualizacji?</span><span class="sxs-lookup"><span data-stu-id="f8411-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="f8411-181">Załóżmy, że chcesz tooupdate obrazu systemu operacyjnego przy zachowaniu hello skalowania maszyny wirtualnej ustawić uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f8411-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="f8411-182">PowerShell i hello wiersza polecenia platformy Azure można zaktualizować obrazy maszyny wirtualnej hello, jednej maszyny wirtualnej w czasie.</span><span class="sxs-lookup"><span data-stu-id="f8411-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="f8411-183">Witaj [uaktualnienia zestawu skalowania maszyn wirtualnych](./virtual-machine-scale-sets-upgrade-scale-set.md) artykuł zawiera również dodatkowe informacje na jakie opcje są dostępne tooperform uaktualnienia systemu operacyjnego przez zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8411-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8411-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8411-184">Next steps</span></span>

* [<span data-ttu-id="f8411-185">Użyj programu PowerShell toomanage zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="f8411-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="f8411-186">Utwórz szablon zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="f8411-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

