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
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Wdrażanie aplikacji na zestawy skalowania maszyny wirtualnej

W tym artykule opisano różne sposoby konfiguracji oprogramowania tooinstall na dużą skalę hello czasu hello są obsługiwane.

Może być tooreview hello [Omówienie projektowania zestaw skali](virtual-machine-scale-sets-design-overview.md) artykułu, który opisano niektóre hello ograniczeń narzuconych przez zestawy skalowania maszyny wirtualnej.

## <a name="capture-and-reuse-an-image"></a>Użyć obrazu

Można użyć ustawionych w Azure tooprepare obraz podstawowy dla Twojego skali maszyny wirtualnej. Ten proces tworzy dysków zarządzanych na Twoim koncie magazynu, który może odwoływać się jako obrazu podstawowego hello zestawu skali. 

Witaj następujące kroki:

1. Utwórz maszynę wirtualną platformy Azure
   * [Linux][linux-vm-create]
   * [Systemu Windows][windows-vm-create]

2. Zdalne hello maszyny wirtualnej i dostosować hello systemu tooyour potrzeb.

   Jeśli chcesz, należy zainstalować aplikację teraz. Jednak wiedzieć, że instalując swoją aplikację już teraz, użytkownik może utworzyć uaktualniania aplikacji bardziej skomplikowane, ponieważ może być konieczne tooremove jej pierwszym. Zamiast tego można użyć tego kroku tooinstall wszystkie wymagania wstępne, które mogą być potrzebne aplikacji, takich jak określonej funkcji środowiska uruchomieniowego lub systemu operacyjnego.

3. Czynności opisane w samouczku "Przechwytywanie maszyny" hello, w obu [Linux] [ linux-vm-capture] lub [Windows][windows-vm-capture].

4. Utwórz [zestawu skalowania maszyn wirtualnych] [ vmss-create] z hello obrazu przechwycone w poprzednim kroku hello identyfikatora URI.

Aby uzyskać więcej informacji dotyczących dysków, zobacz [omówienie dysków zarządzanych](../virtual-machines/windows/managed-disks-overview.md) i [używać dołączonych dysków danych](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Zainstaluj po udostępnieniu hello zestaw skali

Rozszerzenia maszyn wirtualnych może być stosowane zestaw skali maszyny wirtualnej tooa. Za pomocą rozszerzenia maszyny wirtualnej można dostosowywać hello maszyn wirtualnych w skali Ustaw jako całej grupy. Aby uzyskać więcej informacji na temat rozszerzeń, zobacz [rozszerzenia maszyny wirtualnej](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Istnieją trzy główne rozszerzeń, których można używać, w zależności od Jeśli system operacyjny jest oparty na systemie Linux lub z systemem Windows.

### <a name="windows"></a>Windows

Dla systemu operacyjnego z systemem Windows, należy użyć albo hello **v1.8 niestandardowego skryptu** rozszerzenia lub hello **DSC środowiska PowerShell** rozszerzenia.

#### <a name="custom-script"></a>Niestandardowego skryptu

Witaj rozszerzenia niestandardowego skryptu uruchamia skrypt w każdym wystąpieniu maszyny wirtualnej w zestawie skalowania hello. Pliku konfiguracji lub zmienna wskazuje, które pliki są pobierane toohello maszyny wirtualnej, a następnie jakie polecenia uruchamiane. Na przykład można użyć tego Instalatora toorun, skrypt, pliku wsadowego lub każdego pliku wykonywalnego.

PowerShell korzysta z ustawień hello obiektu hashtable. Ten przykład konfiguruje hello skryptu niestandardowego rozszerzenia toorun skrypt programu PowerShell, który instaluje usługi IIS.

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
>Użyj hello `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

---------


Azure CLI używa pliku json hello ustawień. Ten przykład konfiguruje hello skryptu niestandardowego rozszerzenia toorun skrypt programu PowerShell, który instaluje usługi IIS. Zapisz hello następującego pliku json jako _settings.json_.

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
>Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

### <a name="powershell-dsc"></a>DSC środowiska PowerShell

Możesz użyć wystąpień maszyny wirtualnej zestawu skali hello toocustomize DSC środowiska PowerShell. Witaj **DSC** rozszerzenia opublikowanych przez **Microsoft.Powershell** wdraża i uruchamia konfiguracji DSC hello podane w każdym wystąpieniu maszyny wirtualnej. Pliku konfiguracji lub zmienna Określa, że rozszerzenie hello gdzie *zip* jest pakietu i które _funkcji skryptu_ toorun kombinacji.

PowerShell korzysta z ustawień hello obiektu hashtable. W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS.

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
>Użyj hello `-ProtectedSetting` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

-----------

Azure CLI używa ustawienia hello json. W tym przykładzie wdraża DSC pakietu, który instaluje usługi IIS. Zapisz hello następującego pliku json jako _settings.json_.

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
>Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

### <a name="linux"></a>Linux

Linux można użyć albo hello **v2.0 niestandardowego skryptu** rozszerzenia lub użyj **init chmury** podczas tworzenia.

Niestandardowego skryptu jest proste rozszerzenia, które pobiera wystąpień maszyn wirtualnych toohello plików i wykonuje polecenie.

#### <a name="custom-script"></a>Niestandardowego skryptu

Zapisz hello następującego pliku json jako _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Użyj hello Azure CLI tooadd tego tooan rozszerzenia istniejący zestaw skali maszyny wirtualnej. Każda maszyna wirtualna w skali hello ustawić automatycznie uruchamia hello rozszerzenia.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Użyj hello `--protected-settings` Przełącz wszystkie ustawienia, które mogą zawierać poufne informacje.

#### <a name="cloud-init"></a>Init chmury

Init chmury jest używany podczas tworzenia zestawu skali hello. Najpierw należy utworzyć lokalnego pliku o nazwie _init.txt chmury_ i dodać Twojego tooit konfiguracji. Na przykład, zobacz [tego gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Ustaw hello Użyj interfejsu wiersza polecenia Azure toocreate skali. Witaj `--custom-data` pole akceptuje hello nazwa pliku skryptu init chmury.

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

Jeśli wdrożono aplikację za pomocą rozszerzenia zmiany definicji rozszerzenia hello w określony sposób. Ta zmiana powoduje, że wystąpień maszyn wirtualnych tooall hello rozszerzenia toobe ponownego wdrożenia. Coś **musi** można zmienić o rozszerzeniu hello, takie jak zmiana nazwy pliku do którego istnieje odwołanie, w przeciwnym razie ma Azure nie można znaleźć, który hello rozszerzenia została zmieniona.

Jeśli aplikacja hello rozszerzania się do obrazu systemu operacyjnego, należy użyć potoku automatycznego wdrażania aktualizacji aplikacji. Projektowanie sieci toofacilitate architektura szybkiej wymiany przemieszczanego skali, ustaw w środowisku produkcyjnym. Dobrym przykładem tego podejścia jest hello [Azure Spinnaker sterownik pracy](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Pakujący](https://www.packer.io/) i [Terraform](https://www.terraform.io/) pomocy technicznej usługi Azure Resource Manager, można również zdefiniować obrazów "jako kod" i je kompilować na platformie Azure, następnie użyć hello wirtualnego dysku twardego w zestawie skali. Jednak to tak staje się powodować problemy dla obrazów witryny marketplace, kiedy rozszerzenia/niestandardowe skrypty stać się ważniejsze od usługi bits z witryny marketplace nie zmieniać bezpośrednio.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Co się stanie po zestawu skalowania skaluje się?
Aplikacja hello jest instalowana automatycznie podczas dodawania co najmniej jeden zestaw skalowania tooa maszyn wirtualnych. Przykład, jeśli zestaw skalowania hello ma rozszerzenia zdefiniowane, są uruchamiane na nowej maszynie wirtualnej każdym razem, gdy jest tworzona. Jeśli zestaw skali hello jest oparta na obraz niestandardowy, wszelkie nowej maszyny wirtualnej jest kopią hello źródła niestandardowego obrazu. Jeśli maszyn wirtualnych zestawu skalowania hello hostów kontenera, może być uruchamiania kodu tooload hello kontenery w niestandardowe rozszerzenie skryptu. Lub rozszerzenie może zainstalować agenta, który rejestruje z programem orchestrator klastra, takie jak usługi kontenera platformy Azure.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Jak wdrożeniem aktualizacji systemu operacyjnego między domenami aktualizacji?
Załóżmy, że chcesz tooupdate obrazu systemu operacyjnego przy zachowaniu hello skalowania maszyny wirtualnej ustawić uruchomiona. PowerShell i hello wiersza polecenia platformy Azure można zaktualizować obrazy maszyny wirtualnej hello, jednej maszyny wirtualnej w czasie. Witaj [uaktualnienia zestawu skalowania maszyn wirtualnych](./virtual-machine-scale-sets-upgrade-scale-set.md) artykuł zawiera również dodatkowe informacje na jakie opcje są dostępne tooperform uaktualnienia systemu operacyjnego przez zestaw skali maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki

* [Użyj programu PowerShell toomanage zestawie skali.](virtual-machine-scale-sets-windows-manage.md)
* [Utwórz szablon zestaw skali.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

