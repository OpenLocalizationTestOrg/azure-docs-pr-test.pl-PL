---
title: "aaaVirtual maszyny w szablonie usługi Azure Resource Manager | Microsoft Azure"
description: "Dowiedz się więcej na temat sposobu hello zasobu maszyny wirtualnej jest zdefiniowany w szablonie usługi Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Maszyny wirtualne w szablonie usługi Azure Resource Manager

W tym artykule opisano aspekty szablonu usługi Azure Resource Manager stosowane toovirtual maszyny. W tym artykule nie opisano pełną szablonu do utworzenia maszyny wirtualnej; w tym należy definicji zasobu dla kont magazynu, interfejsy sieciowe publicznych adresów IP i sieci wirtualnych. Aby uzyskać więcej informacji o sposobie tych zasobów można definiować razem, zobacz hello [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Istnieje wiele [szablony w galerii hello](https://azure.microsoft.com/documentation/templates/?term=VM) zawierające hello zasobu maszyny Wirtualnej. Nie wszystkie elementy, które można uwzględnić w szablonie są opisane poniżej.

W tym przykładzie pokazano sekcję typowe zasobu szablon umożliwiający tworzenie określonej liczby maszyn wirtualnych:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>W tym przykładzie opiera się na konto magazynu, który został wcześniej utworzony. Konto magazynu hello można utworzyć przez wdrożenie jej z hello szablonu. przykład Witaj również zależy od interfejsu sieciowego i jego zasoby zależne, zdefiniowane w szablonie hello. Te zasoby nie są wyświetlane w przykładzie hello.
>
>

## <a name="api-version"></a>Wersja interfejsu API

Podczas wdrażania zasobów przy użyciu szablonu, masz toospecify wersję hello toouse interfejsu API. przykład Witaj przedstawia hello zasobu maszyny wirtualnej za pomocą tego elementu apiVersion:

```
"apiVersion": "2016-04-30-preview",
```

Wersja Hello hello interfejsu API określonej w szablonie dotyczy właściwości, które można zdefiniować w szablonie hello. Ogólnie rzecz biorąc należy zaznaczyć hello najnowszą wersję interfejsu API, podczas tworzenia szablonów. Istniejących szablonów można zdecydować, czy mają toocontinue przy użyciu starszej wersji interfejsu API, lub zaktualizować szablon dla hello najnowszej wersji tootake korzystać z nowych funkcji.

Użyj tych możliwości pobierania najnowszej wersji interfejsu API hello:

- Interfejs API REST - [listy wszystkich dostawców zasobów](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell — [Get AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Azure CLI 2.0 — [az Pokaż dostawcy](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parametry i zmienne

[Parametry](../../resource-group-authoring-templates.md) ułatwiają możesz toospecify wartości dla szablonu powitania po jej uruchomieniu. W tej sekcji parametrów jest używana w przykładzie hello:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Podczas wdrażania szablonu przykład hello można wprowadzić wartości hello nazwę i hasło konta administratora hello na każdą maszynę Wirtualną i hello liczbę toocreate maszyn wirtualnych. Dostępna jest opcja hello określania wartości parametrów w osobnym pliku, który jest zarządzany za pomocą szablonu hello lub podawanie wartości po wyświetleniu monitu.

[Zmienne](../../resource-group-authoring-templates.md) ułatwić Ci tooset wartości w szablonie hello często używane w całej go lub które mogą ulec zmianie. W tej sekcji zmiennych jest używana w przykładzie hello:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Podczas wdrażania szablonu przykład hello wartości zmiennych są używane nazwy hello i identyfikator hello utworzone wcześniej konto magazynu. Zmienne są również używane tooprovide hello ustawienia dla rozszerzenia diagnostycznych hello. Użyj hello [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp można zdecydować, jak toostructure hello parametry i zmienne w szablonie.

## <a name="resource-loops"></a>Pętle zasobów

Jeśli potrzebujesz więcej niż jednej maszyny wirtualnej dla aplikacji, można użyć elementu kopiowania w szablonie. Ten opcjonalny element w pętli tworzenie hello liczbę maszyn wirtualnych, które określono jako parametr:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Ponadto w przykładzie hello, który indeks pętli hello jest używany podczas niektórych hello określania wartości dla zasobu hello. Na przykład jeśli wprowadzono liczby wystąpień trzy, nazwy hello hello dysków systemu operacyjnego są myOSDisk1, myOSDisk2 i myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>W tym przykładzie użyto dysków zarządzanych hello maszyn wirtualnych.
>
>

Należy pamiętać o tym, które tworzenia pętli dla jednego zasobu w szablonie hello mogą wymagać możesz toouse hello pętli podczas tworzenia lub uzyskiwania dostępu do innych zasobów. Na przykład wiele maszyn wirtualnych nie można użyć hello sam interfejs, sieci, jeśli szablon w pętli tworzenia trzech maszyn wirtualnych, również musi pętli przez proces tworzenia trzech interfejsów sieciowych. Przypisując tooa interfejsu sieciowego maszyny Wirtualnej, indeks pętli hello jest używany tooidentify go:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Zależności

Najwięcej zasobów są zależne od innych zasobów toowork poprawnie. Maszyny wirtualne muszą być skojarzone z sieci wirtualnej i toodo wymaga karty sieciowej. Witaj [dependsOn](../../resource-group-define-dependencies.md) element jest używany toomake się, że ten interfejs sieciowy hello jest gotowy toobe używane przed utworzeniem hello maszyn wirtualnych:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Menedżer zasobów wdraża równolegle wszystkie zasoby, które nie są zależne od innego zasobu wdrażany. Należy zachować ostrożność podczas ustawiania zależności, ponieważ przypadkowo spowalniają wdrożenia przez określenie niepotrzebnych zależności. Zależności mogą być powiązane za pomocą wielu zasobów. Na przykład hello interfejsu sieciowego jest zależna od hello publicznego adresu IP i zasoby sieci wirtualnej.

Jak sprawdzić, czy zależność jest wymagane? Sprawdź wartości hello ustawiona w szablonie hello. Jeśli element w definicji zasobu maszyny wirtualnej hello wskazuje tooanother zasobów, które zostało wdrożone w hello tego samego szablonu, potrzebujesz zależności. Na przykład na komputerze wirtualnym przykład definiuje profilu sieciowego:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset ta właściwość musi istnieć hello interfejsu sieciowego. W związku z tym należy zależności. Należy również tooset zależność gdy jeden zasób (podrzędny) zdefiniowano w ramach innego zasobu (nadrzędnego). Na przykład ustawienia diagnostyki hello i rozszerzenia niestandardowego skryptu są oba zdefiniowane jako zasoby podrzędne hello maszyny wirtualnej. Nie można utworzyć dopóki hello maszyna wirtualna istnieje. W związku z tym oba zasoby są oznaczone jako zależne hello maszyny wirtualnej.

## <a name="profiles"></a>Profile

Niektóre elementy profilu są używane podczas definiowania zasobu maszyny wirtualnej. Niektóre są wymagane, a inne opcjonalne. Na przykład hello hardwareProfile, osProfile storageProfile i networkProfile elementy są wymagane, ale hello diagnosticsProfile jest opcjonalna. Te profile zdefiniować ustawienia, takie jak:
   
- [rozmiar](sizes.md)
- [Nazwa](/architecture/best-practices/naming-conventions) i poświadczenia
- dysk i [ustawień systemu operacyjnego](cli-ps-findimage.md)
- [Interfejs sieciowy](../../virtual-network/virtual-networks-multiple-nics.md) 
- Diagnostyki rozruchu

## <a name="disks-and-images"></a>Dyski i obrazów
   
Na platformie Azure, pliki wirtualnego dysku twardego może reprezentować [dysków lub obrazów](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Gdy hello systemu operacyjnego w pliku vhd jest specjalne toobe określonej maszyny Wirtualnej, jest tooas określonego dysku. Gdy uogólniony hello systemu operacyjnego w pliku vhd toobe używane toocreate wiele maszyn wirtualnych, tooas określonego obrazu.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Tworzenie nowych maszyn wirtualnych i nowych dysków z obrazu platformy

Podczas tworzenia maszyny Wirtualnej należy zdecydować, jakiego toouse systemu operacyjnego. element elementu imageReference Hello jest system operacyjny hello używane toodefine nowej maszyny Wirtualnej. przykład Witaj zawiera definicję dla systemu operacyjnego Windows Server:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Może użyć tej definicji, jeśli chcesz toocreate systemu operacyjnego Linux:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Ustawienia konfiguracji dla dysku systemu operacyjnego hello są przypisywane z elementem osDisk hello. Hello przykładzie zdefiniowano nowego dysku zarządzanego z hello buforowania zestawu trybu zbyt**ReadWrite** i dysku hello jest tworzony z [obrazu platformy](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Tworzenie nowych maszyn wirtualnych z istniejących dysków zarządzanych

Jeśli chcesz toocreate maszyny wirtualne z istniejącej dysków, Usuń elementu imageReference hello i hello osProfile elementy, a następnie Definiuj następujące ustawienia dysku:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Tworzenie nowych maszyn wirtualnych z zarządzanego obrazu

Jeśli chcesz toocreate maszynę wirtualną z zarządzanego obrazu, zmień element elementu imageReference hello i Definiuj następujące ustawienia dysku:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Dołącz dysków z danymi

Można opcjonalnie dodawać toohello dysków danych maszyn wirtualnych. Witaj [liczba dysków](sizes.md) zależy od rozmiaru hello dysku systemu operacyjnego, którego używasz. Rozmiar maszyn wirtualnych hello hello ustawienie tooStandard_DS1_v2, hello maksymalna liczba dysków z danymi, które mogą zostać dodane toohello ich wynosi dwa. Przykład Witaj jeden dysk danych zarządzanych jest dodawany tooeach maszyny Wirtualnej:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Rozszerzenia

Mimo że [rozszerzenia](extensions-features.md) są osobne zasobu, są ściśle związany tooVMs. Rozszerzenia mogą być dodawane jako zasoby podrzędne hello maszyny Wirtualnej lub jako osobne zasobów. przykład Witaj pokazuje hello [rozszerzenia diagnostyki](extensions-diagnostics-template.md) dodawany toohello maszyn wirtualnych:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Tego rozszerzenia zasobu używa zmiennej storageName hello i hello diagnostycznych zmienne tooprovide wartości. Jeśli chcesz toochange hello dane zbierane przez to rozszerzenie, możesz dodać więcej zmiennej wadperfcounters toohello liczników wydajności. Możesz również wybrać tooput hello diagnostyki danych do konta magazynu innego niż przechowywania hello dysków maszyny Wirtualnej.

Istnieje wiele rozszerzeń, które można zainstalować na maszynie Wirtualnej, ale hello najbardziej przydatne jest prawdopodobnie hello [niestandardowe rozszerzenie skryptu](extensions-customscript.md). Przykład Witaj skrypt programu PowerShell o nazwie start.ps1 działa na każdej maszynie Wirtualnej po pierwszym uruchomieniu:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

Witaj start.ps1 skryptu można wykonywać wiele zadań konfiguracyjnych. Na przykład nie są inicjowane dyski danych hello dodanych toohello maszyn wirtualnych w przykładzie hello; można użyć tooinitialize skryptu niestandardowego je. Jeśli masz wiele toodo zadania uruchamiania, można użyć hello start.ps1 pliku toocall inne skrypty programu PowerShell w magazynie Azure. przykład Witaj używa programu PowerShell, ale można użyć dowolnej metody skryptów, która jest dostępna w systemie operacyjnym hello, którego używasz.

Można wyświetlić stan hello hello zainstalowanych rozszerzeń hello ustawień rozszerzenia w portalu hello:

![Pobierz stan rozszerzenia](./media/template-description/virtual-machines-show-extensions.png)

Można również uzyskać informacji o rozszerzeniu za pomocą hello **Get-AzureRmVMExtension** PowerShell polecenia hello **get rozszerzenia maszyny wirtualnej** polecenia Azure CLI 2.0 lub hello **uzyskiwanie informacji o rozszerzeniu**  Interfejsu API REST.

## <a name="deployments"></a>Wdrożenia

Podczas wdrażania szablonu Azure śledzi hello zasobów, które wdrożone w grupie i automatycznie przypisuje grupę toothis wdrożone nazwy. Nazwa Hello wdrożenia hello jest hello taka sama jak nazwa hello hello szablonu.

Jeśli zastanawiasz się, jak hello stan zasobów we wdrożeniu hello, można użyć hello bloku grupy zasobów w portalu Azure hello:

![Uzyskaj informacje na temat wdrażania](./media/template-description/virtual-machines-deployment-info.png)
    
Nie jest problem toouse hello tyle samo zasobów toocreate szablon lub tooupdate istniejących zasobów. Korzystając z polecenia toodeploy szablony, masz toosay możliwości hello którego [tryb](../../resource-group-template-deploy.md) ma toouse. można ustawić trybu Hello tooeither **Complete** lub **przyrostowe**. Domyślnie Hello jest toodo aktualizacji przyrostowych. Należy zachować ostrożność przy użyciu hello **Complete** tryb ponieważ przypadkowo usuniesz zasobami. Po ustawieniu trybu hello zbyt**Complete**, wszystkie zasoby w grupie zasobów hello, które nie znajdują się w szablonie hello usuwa Menedżera zasobów.

## <a name="next-steps"></a>Następne kroki

- Tworzenie własnych przy użyciu szablonu [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).
- Wdrażanie szablonu hello, które zostały utworzone za pomocą [Utwórz maszynę wirtualną z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md).
- Dowiedz się, jak toomanage hello maszyn wirtualnych, które zostały utworzone, przeglądając [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
