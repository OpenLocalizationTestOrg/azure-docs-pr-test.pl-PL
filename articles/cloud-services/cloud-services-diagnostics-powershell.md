---
title: "Diagnostyka aaaEnable w usług Azure Cloud Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable diagnostyki dla chmury usług przy użyciu programu PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell
Można zebrać danych diagnostycznych, takich jak dzienniki aplikacji, liczniki wydajności itp. z usługi w chmurze przy użyciu hello rozszerzenia diagnostycznych platformy Azure. W tym artykule opisano, jak tooenable hello rozszerzenia diagnostyki Azure dla usługi w chmurze przy użyciu programu PowerShell.  Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service
Ta metoda jest typ integracji toocontinuous odpowiednich scenariuszach, w którym można włączyć rozszerzenia w ramach wdrażania diagnostyki hello hello usługi w chmurze. Podczas tworzenia nowego wdrożenia usługi w chmurze można włączyć rozszerzenia diagnostyki hello przez przekazywanie hello *ExtensionConfiguration* toohello parametru [AzureDeployment nowy](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) polecenia cmdlet. Witaj *ExtensionConfiguration* parametr pobiera tablicę diagnostyki konfiguracje, które mogą być tworzone przy użyciu hello [AzureServiceDiagnosticsExtensionConfig nowy](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) polecenia cmdlet.

Witaj poniższy przykład przedstawia sposób można włączyć diagnostyki z sieć Web i proces roboczy, o konfiguracji diagnostyki innej usługi w chmurze.

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

Jeśli plik konfiguracji diagnostyki hello Określa `StorageAccount` element nazwy konta magazynu, następnie hello `New-AzureServiceDiagnosticsExtensionConfig` polecenia cmdlet będą automatycznie używać tego konta magazynu. Dla tego toowork hello konto magazynu na potrzeby toobe w hello tej samej subskrypcji, ponieważ hello wdrażania usługi w chmurze.

Z Azure SDK 2.6 publikowania plików konfiguracji rozszerzenia dalszego hello generowanych przez hello MSBuild danych wyjściowych będzie zawierać nazwy konta magazynu hello oparte na ciąg konfiguracji diagnostyki hello określony w pliku konfiguracji usługi hello (cscfg). skrypt Hello poniżej pokazano, jak pliki konfiguracji rozszerzenia hello tooparse z hello publikowanie danych wyjściowych i skonfigurować rozszerzenia diagnostyki dla każdej roli, podczas wdrażania usługi w chmurze hello.

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online używa podejście podobne zautomatyzowanych wdrożeń usług w chmurze z rozszerzeniem diagnostyki hello. Zobacz [AzureCloudDeployment.ps1 publikowania](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pełny przykład.

Jeśli nie `StorageAccount` została określona w konfiguracji diagnostyki hello, wówczas należy toopass w hello *StorageAccountName* polecenia cmdlet toohello parametru. Jeśli hello *StorageAccountName* określony parametr, a następnie hello cmdlet zawsze używać konta magazynu hello określonego w parametrze hello i nie Witaj, który jest określony w pliku konfiguracyjnym hello diagnostyki.

Jeśli konto magazynu jest w innej subskrypcji z hello usługi w chmurze, a następnie należy tooexplicitly diagnostyki hello przekazywanie hello *StorageAccountName* i *StorageAccountKey* parametrów polecenia cmdlet toohello. Witaj *StorageAccountKey* parametru nie jest wymagana, gdy diagnostyki hello konto magazynu znajduje się w tej samej subskrypcji, Witaj, hello polecenia cmdlet można automatycznie zapytania i ustaw wartość klucza hello podczas włączania rozszerzenia diagnostyki hello. Jednak jeśli hello konto magazynu diagnostyki jest w innej subskrypcji, polecenia cmdlet hello może nie być możliwe tooget hello klucza automatycznie i potrzebujesz tooexplicitly określ klucz hello za pośrednictwem hello *StorageAccountKey* parametr.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service
Można użyć hello [AzureServiceDiagnosticsExtension zestaw](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet tooenable lub aktualizacji konfiguracji diagnostyki na usługi w chmurze, która jest już uruchomiona.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki
Użyj hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet tooget hello bieżącej diagnostyki konfiguracji dla usługi w chmurze.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Usuwanie rozszerzenia diagnostyki
tooturn poza diagnostyki w chmurze usługi, należy użyć hello [AzureServiceDiagnosticsExtension Usuń](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Jeśli włączono rozszerzenie diagnostyki hello przy użyciu *AzureServiceDiagnosticsExtension zestawu* lub hello *AzureServiceDiagnosticsExtensionConfig nowy* bez hello *roli* parametr, a następnie można usunąć za pomocą rozszerzenia hello *AzureServiceDiagnosticsExtension Usuń* bez hello *roli* parametru. Jeśli hello *roli* parametr został użyty podczas włączania rozszerzenia hello to należy użyć podczas usuwania hello rozszerzenia.

rozszerzenie diagnostyki hello tooremove z poszczególnych poszczególnych ról:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać dodatkowe wskazówki na temat używania innych technik tootroubleshoot problemów i Diagnostyka Azure, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md).
* Witaj [schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/dn782207.aspx) opisano różne konfiguracje xml opcje rozszerzenia diagnostyki hello hello.
* toolearn tooenable hello diagnostyki rozszerzenia dla maszyn wirtualnych, zobacz temat [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md)
