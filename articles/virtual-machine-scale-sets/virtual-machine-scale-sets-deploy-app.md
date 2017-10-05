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
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Wdrażanie aplikacji na zestawy skalowania maszyny wirtualnej

W tym artykule opisano różne sposoby jak zainstalować oprogramowanie, w tym czasie są obsługiwane przez zestaw skali.

Warto przejrzeć [Omówienie projektowania zestaw skali](virtual-machine-scale-sets-design-overview.md) artykułu, który opisano niektóre ograniczenia narzucone przez zestawy skalowania maszyny wirtualnej.

## <a name="capture-and-reuse-an-image"></a>Użyć obrazu

Można użyć maszyny wirtualnej, zdefiniowanych na platformie Azure, aby przygotować obraz podstawowy na skalę. Ten proces tworzy dysków zarządzanych na Twoim koncie magazynu, który może odwoływać się jako obrazu podstawowego zestawu skali. 

Wykonaj następujące czynności:

1. Utwórz maszynę wirtualną platformy Azure
   * [Linux][linux-vm-create]
   * [Systemu Windows][windows-vm-create]

2. Zdalnego do maszyny wirtualnej i Dostosuj system do potrzeb użytkownika.

   Jeśli chcesz, należy zainstalować aplikację teraz. Jednak pamiętać, że instalując swoją aplikację już teraz, może wprowadzić uaktualniania aplikacji bardziej skomplikowane, ponieważ trzeba najpierw usuń. Zamiast tego można użyć tego kroku można zainstalować wszystkie wymagania wstępne, które mogą być potrzebne aplikacji, takich jak określonej funkcji środowiska uruchomieniowego lub systemu operacyjnego.

3. Czynności opisane w samouczku "Przechwytywanie maszyny" dla dowolnego [Linux] [ linux-vm-capture] lub [Windows][windows-vm-capture].

4. Utwórz [zestawu skalowania maszyn wirtualnych] [ vmss-create] z obrazem URI przechwycone w poprzednim kroku.

Aby uzyskać więcej informacji dotyczących dysków, zobacz [omówienie dysków zarządzanych](../virtual-machines/windows/managed-disks-overview.md) i [używać dołączonych dysków danych](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-the-scale-set-is-provisioned"></a>Zainstaluj po udostępnieniu zestawu skalowania

Rozszerzenia maszyn wirtualnych może odnosić się do zestawu skalowania maszyn wirtualnych. Za pomocą rozszerzenia maszyny wirtualnej można dostosowywać maszyn wirtualnych w skali Ustaw jako całej grupy. Aby uzyskać więcej informacji na temat rozszerzeń, zobacz [rozszerzenia maszyny wirtualnej](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Istnieją trzy główne rozszerzeń, których można używać, w zależności od Jeśli system operacyjny jest oparty na systemie Linux lub z systemem Windows.

### <a name="windows"></a>Windows

Dla systemu operacyjnego z systemem Windows, użyj **v1.8 niestandardowego skryptu** rozszerzenia, lub **DSC środowiska PowerShell** rozszerzenia.

#### <a name="custom-script"></a>Niestandardowego skryptu

Rozszerzenie skryptu niestandardowego uruchamia skrypt w każdym wystąpieniu maszyny wirtualnej w zestawie skalowania. Pliku konfiguracji lub zmienna wskazuje, które pliki są pobierane do maszyny wirtualnej, a następnie jakie polecenia uruchamiane. Aby uruchomić Instalatora, skrypt, plik wsadowy każdego pliku wykonywalnego, na przykład może wykorzystać tę.

PowerShell korzysta z tablicy skrótów dla ustawień. Ten przykład Konfiguruje rozszerzenia niestandardowego skryptu, aby uruchomić skrypt programu PowerShell, który instaluje usługi IIS.

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
>Użyj `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

---------


Azure CLI używa pliku json dla ustawień. Ten przykład Konfiguruje rozszerzenia niestandardowego skryptu, aby uruchomić skrypt programu PowerShell, który instaluje usługi IIS. Zapisz plik json następujące jako _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Następnie uruchom to polecenie wiersza polecenia platformy Azure.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

### <a name="powershell-dsc"></a>DSC środowiska PowerShell

DSC środowiska PowerShell umożliwia dostosowywanie wystąpień maszyny wirtualnej zestawu skali. **DSC** rozszerzenia opublikowanych przez **Microsoft.Powershell** wdraża i uruchamia Podana konfiguracja DSC w każdym wystąpieniu maszyny wirtualnej. Pliku konfiguracji lub zmienna Określa, że rozszerzenie gdzie *zip* jest pakietu i które _funkcji skryptu_ kombinacja do uruchomienia.

PowerShell korzysta z tablicy skrótów dla ustawień. W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.

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
>Użyj `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

-----------

Azure CLI używa json dla ustawień. W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS. Zapisz plik json następujące jako _settings.json_.

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

Następnie uruchom to polecenie wiersza polecenia platformy Azure.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

### <a name="linux"></a>Linux

Linux można użyć dowolnego **v2.0 niestandardowego skryptu** rozszerzenia lub użyj **init chmury** podczas tworzenia.

Niestandardowego skryptu jest proste rozszerzenia, które pobiera pliki do wystąpień maszyny wirtualnej i wykonuje polecenie.

#### <a name="custom-script"></a>Niestandardowego skryptu

Zapisz plik json następujące jako _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Użyj interfejsu wiersza polecenia Azure, aby dodać to rozszerzenie do istniejącego zestawu skalowania maszyny wirtualnej. Każda maszyna wirtualna w skali ustawiane automatycznie uruchamia rozszerzenia.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Użyj `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

#### <a name="cloud-init"></a>Init chmury

Init chmury jest używany podczas tworzenia zestawu skalowania. Najpierw należy utworzyć lokalnego pliku o nazwie _init.txt chmury_ i Dodaj do niej konfiguracji. Na przykład, zobacz [tego gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Użyj interfejsu wiersza polecenia Azure, aby utworzyć zestaw skali. `--custom-data` Polu można wprowadzić nazwę pliku skryptu init chmury.

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

## <a name="how-do-i-manage-application-updates"></a>Jak zarządzać aktualizacji aplikacji?

Jeśli wdrożono aplikację za pomocą rozszerzenia, należy zmienić definicji rozszerzenia w określony sposób. Ta zmiana powoduje, że rozszerzenie ponownego wdrożenia dla wszystkich wystąpień maszyny wirtualnej. Coś **musi** można zmienić o rozszerzeniu, takie jak zmiana nazwy pliku do którego istnieje odwołanie, w przeciwnym razie ma Azure nie można znaleźć rozszerzenia o zmianie.

Jeśli aplikacja jest rozszerzania do obrazu systemu operacyjnego, należy użyć potoku automatycznego wdrażania aktualizacji aplikacji. Projekt architektury ułatwia szybkie wymiany przemieszczanego skali, ustaw w środowisku produkcyjnym. Dobrym przykładem tego podejścia jest [Azure Spinnaker sterownik pracy](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Pakujący](https://www.packer.io/) i [Terraform](https://www.terraform.io/) pomocy technicznej usługi Azure Resource Manager, można również zdefiniować obrazów "jako kod" i je kompilować na platformie Azure, następnie użyć wirtualnego dysku twardego w zestawie skali. Jednak to tak staje się powodować problemy dla obrazów witryny marketplace, kiedy rozszerzenia/niestandardowe skrypty stać się ważniejsze od usługi bits z witryny marketplace nie zmieniać bezpośrednio.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Co się stanie po zestawu skalowania skaluje się?
Aplikacja jest instalowana automatycznie po dodaniu co najmniej jednej maszyny wirtualnej do zestawu skalowania. Przykład, jeśli wartość skali ma rozszerzenia zdefiniowane, są uruchamiane na nowej maszynie wirtualnej każdym razem, gdy jest tworzona. Jeśli zestaw skalowania jest oparta na obraz niestandardowy, wszelkie nowej maszyny wirtualnej jest kopią niestandardowego obrazu źródłowego. Jeśli kontener hosty maszyn wirtualnych zestawu skalowania, może być uruchamianie kodu w celu załadowania kontenerów w niestandardowe rozszerzenie skryptu. Lub rozszerzenie może zainstalować agenta, który rejestruje z programem orchestrator klastra, takie jak usługi kontenera platformy Azure.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Jak wdrożeniem aktualizacji systemu operacyjnego między domenami aktualizacji?
Załóżmy, że chcesz zaktualizować obraz systemu operacyjnego przy zachowaniu zestaw systemem skalowania maszyny wirtualnej. PowerShell i interfejsu wiersza polecenia Azure można zaktualizować obrazy maszyny wirtualnej, maszyn wirtualnych jednocześnie. [Uaktualnienia zestawu skalowania maszyn wirtualnych](./virtual-machine-scale-sets-upgrade-scale-set.md) artykuł zawiera również dodatkowe informacje na jakie opcje są dostępne do uaktualnienia systemu operacyjnego przez zestaw skali maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki

* [Użyj programu PowerShell do zarządzania zestawie skali.](virtual-machine-scale-sets-windows-manage.md)
* [Utwórz szablon zestaw skali.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

