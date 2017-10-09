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
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="be1cf-103">Maszyny wirtualne w szablonie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be1cf-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="be1cf-104">W tym artykule opisano aspekty szablonu usługi Azure Resource Manager stosowane toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="be1cf-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="be1cf-105">W tym artykule nie opisano pełną szablonu do utworzenia maszyny wirtualnej; w tym należy definicji zasobu dla kont magazynu, interfejsy sieciowe publicznych adresów IP i sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="be1cf-106">Aby uzyskać więcej informacji o sposobie tych zasobów można definiować razem, zobacz hello [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="be1cf-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="be1cf-107">Istnieje wiele [szablony w galerii hello](https://azure.microsoft.com/documentation/templates/?term=VM) zawierające hello zasobu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="be1cf-108">Nie wszystkie elementy, które można uwzględnić w szablonie są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="be1cf-109">W tym przykładzie pokazano sekcję typowe zasobu szablon umożliwiający tworzenie określonej liczby maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="be1cf-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="be1cf-110">W tym przykładzie opiera się na konto magazynu, który został wcześniej utworzony.</span><span class="sxs-lookup"><span data-stu-id="be1cf-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="be1cf-111">Konto magazynu hello można utworzyć przez wdrożenie jej z hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="be1cf-112">przykład Witaj również zależy od interfejsu sieciowego i jego zasoby zależne, zdefiniowane w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="be1cf-113">Te zasoby nie są wyświetlane w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="be1cf-114">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="be1cf-114">API Version</span></span>

<span data-ttu-id="be1cf-115">Podczas wdrażania zasobów przy użyciu szablonu, masz toospecify wersję hello toouse interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="be1cf-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="be1cf-116">przykład Witaj przedstawia hello zasobu maszyny wirtualnej za pomocą tego elementu apiVersion:</span><span class="sxs-lookup"><span data-stu-id="be1cf-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="be1cf-117">Wersja Hello hello interfejsu API określonej w szablonie dotyczy właściwości, które można zdefiniować w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="be1cf-118">Ogólnie rzecz biorąc należy zaznaczyć hello najnowszą wersję interfejsu API, podczas tworzenia szablonów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="be1cf-119">Istniejących szablonów można zdecydować, czy mają toocontinue przy użyciu starszej wersji interfejsu API, lub zaktualizować szablon dla hello najnowszej wersji tootake korzystać z nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="be1cf-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="be1cf-120">Użyj tych możliwości pobierania najnowszej wersji interfejsu API hello:</span><span class="sxs-lookup"><span data-stu-id="be1cf-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="be1cf-121">Interfejs API REST - [listy wszystkich dostawców zasobów](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="be1cf-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="be1cf-122">PowerShell — [Get AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="be1cf-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="be1cf-123">Azure CLI 2.0 — [az Pokaż dostawcy](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="be1cf-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="be1cf-124">Parametry i zmienne</span><span class="sxs-lookup"><span data-stu-id="be1cf-124">Parameters and variables</span></span>

<span data-ttu-id="be1cf-125">[Parametry](../../resource-group-authoring-templates.md) ułatwiają możesz toospecify wartości dla szablonu powitania po jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="be1cf-126">W tej sekcji parametrów jest używana w przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="be1cf-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="be1cf-127">Podczas wdrażania szablonu przykład hello można wprowadzić wartości hello nazwę i hasło konta administratora hello na każdą maszynę Wirtualną i hello liczbę toocreate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="be1cf-128">Dostępna jest opcja hello określania wartości parametrów w osobnym pliku, który jest zarządzany za pomocą szablonu hello lub podawanie wartości po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="be1cf-129">[Zmienne](../../resource-group-authoring-templates.md) ułatwić Ci tooset wartości w szablonie hello często używane w całej go lub które mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="be1cf-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="be1cf-130">W tej sekcji zmiennych jest używana w przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="be1cf-130">This variables section is used in hello example:</span></span>

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

<span data-ttu-id="be1cf-131">Podczas wdrażania szablonu przykład hello wartości zmiennych są używane nazwy hello i identyfikator hello utworzone wcześniej konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="be1cf-132">Zmienne są również używane tooprovide hello ustawienia dla rozszerzenia diagnostycznych hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="be1cf-133">Użyj hello [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp można zdecydować, jak toostructure hello parametry i zmienne w szablonie.</span><span class="sxs-lookup"><span data-stu-id="be1cf-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="be1cf-134">Pętle zasobów</span><span class="sxs-lookup"><span data-stu-id="be1cf-134">Resource loops</span></span>

<span data-ttu-id="be1cf-135">Jeśli potrzebujesz więcej niż jednej maszyny wirtualnej dla aplikacji, można użyć elementu kopiowania w szablonie.</span><span class="sxs-lookup"><span data-stu-id="be1cf-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="be1cf-136">Ten opcjonalny element w pętli tworzenie hello liczbę maszyn wirtualnych, które określono jako parametr:</span><span class="sxs-lookup"><span data-stu-id="be1cf-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="be1cf-137">Ponadto w przykładzie hello, który indeks pętli hello jest używany podczas niektórych hello określania wartości dla zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="be1cf-138">Na przykład jeśli wprowadzono liczby wystąpień trzy, nazwy hello hello dysków systemu operacyjnego są myOSDisk1, myOSDisk2 i myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="be1cf-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="be1cf-139">W tym przykładzie użyto dysków zarządzanych hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="be1cf-140">Należy pamiętać o tym, które tworzenia pętli dla jednego zasobu w szablonie hello mogą wymagać możesz toouse hello pętli podczas tworzenia lub uzyskiwania dostępu do innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="be1cf-141">Na przykład wiele maszyn wirtualnych nie można użyć hello sam interfejs, sieci, jeśli szablon w pętli tworzenia trzech maszyn wirtualnych, również musi pętli przez proces tworzenia trzech interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="be1cf-142">Przypisując tooa interfejsu sieciowego maszyny Wirtualnej, indeks pętli hello jest używany tooidentify go:</span><span class="sxs-lookup"><span data-stu-id="be1cf-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="be1cf-143">Zależności</span><span class="sxs-lookup"><span data-stu-id="be1cf-143">Dependencies</span></span>

<span data-ttu-id="be1cf-144">Najwięcej zasobów są zależne od innych zasobów toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="be1cf-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="be1cf-145">Maszyny wirtualne muszą być skojarzone z sieci wirtualnej i toodo wymaga karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="be1cf-146">Witaj [dependsOn](../../resource-group-define-dependencies.md) element jest używany toomake się, że ten interfejs sieciowy hello jest gotowy toobe używane przed utworzeniem hello maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="be1cf-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="be1cf-147">Menedżer zasobów wdraża równolegle wszystkie zasoby, które nie są zależne od innego zasobu wdrażany.</span><span class="sxs-lookup"><span data-stu-id="be1cf-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="be1cf-148">Należy zachować ostrożność podczas ustawiania zależności, ponieważ przypadkowo spowalniają wdrożenia przez określenie niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="be1cf-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="be1cf-149">Zależności mogą być powiązane za pomocą wielu zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="be1cf-150">Na przykład hello interfejsu sieciowego jest zależna od hello publicznego adresu IP i zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="be1cf-151">Jak sprawdzić, czy zależność jest wymagane?</span><span class="sxs-lookup"><span data-stu-id="be1cf-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="be1cf-152">Sprawdź wartości hello ustawiona w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="be1cf-153">Jeśli element w definicji zasobu maszyny wirtualnej hello wskazuje tooanother zasobów, które zostało wdrożone w hello tego samego szablonu, potrzebujesz zależności.</span><span class="sxs-lookup"><span data-stu-id="be1cf-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="be1cf-154">Na przykład na komputerze wirtualnym przykład definiuje profilu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="be1cf-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="be1cf-155">tooset ta właściwość musi istnieć hello interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="be1cf-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="be1cf-156">W związku z tym należy zależności.</span><span class="sxs-lookup"><span data-stu-id="be1cf-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="be1cf-157">Należy również tooset zależność gdy jeden zasób (podrzędny) zdefiniowano w ramach innego zasobu (nadrzędnego).</span><span class="sxs-lookup"><span data-stu-id="be1cf-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="be1cf-158">Na przykład ustawienia diagnostyki hello i rozszerzenia niestandardowego skryptu są oba zdefiniowane jako zasoby podrzędne hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="be1cf-159">Nie można utworzyć dopóki hello maszyna wirtualna istnieje.</span><span class="sxs-lookup"><span data-stu-id="be1cf-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="be1cf-160">W związku z tym oba zasoby są oznaczone jako zależne hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="be1cf-161">Profile</span><span class="sxs-lookup"><span data-stu-id="be1cf-161">Profiles</span></span>

<span data-ttu-id="be1cf-162">Niektóre elementy profilu są używane podczas definiowania zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="be1cf-163">Niektóre są wymagane, a inne opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="be1cf-163">Some are required and some are optional.</span></span> <span data-ttu-id="be1cf-164">Na przykład hello hardwareProfile, osProfile storageProfile i networkProfile elementy są wymagane, ale hello diagnosticsProfile jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="be1cf-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="be1cf-165">Te profile zdefiniować ustawienia, takie jak:</span><span class="sxs-lookup"><span data-stu-id="be1cf-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="be1cf-166">rozmiar</span><span class="sxs-lookup"><span data-stu-id="be1cf-166">size</span></span>](sizes.md)
- <span data-ttu-id="be1cf-167">[Nazwa](/architecture/best-practices/naming-conventions) i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="be1cf-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="be1cf-168">dysk i [ustawień systemu operacyjnego](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="be1cf-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="be1cf-169">Interfejs sieciowy</span><span class="sxs-lookup"><span data-stu-id="be1cf-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="be1cf-170">Diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="be1cf-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="be1cf-171">Dyski i obrazów</span><span class="sxs-lookup"><span data-stu-id="be1cf-171">Disks and images</span></span>
   
<span data-ttu-id="be1cf-172">Na platformie Azure, pliki wirtualnego dysku twardego może reprezentować [dysków lub obrazów](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be1cf-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="be1cf-173">Gdy hello systemu operacyjnego w pliku vhd jest specjalne toobe określonej maszyny Wirtualnej, jest tooas określonego dysku.</span><span class="sxs-lookup"><span data-stu-id="be1cf-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="be1cf-174">Gdy uogólniony hello systemu operacyjnego w pliku vhd toobe używane toocreate wiele maszyn wirtualnych, tooas określonego obrazu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="be1cf-175">Tworzenie nowych maszyn wirtualnych i nowych dysków z obrazu platformy</span><span class="sxs-lookup"><span data-stu-id="be1cf-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="be1cf-176">Podczas tworzenia maszyny Wirtualnej należy zdecydować, jakiego toouse systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="be1cf-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="be1cf-177">element elementu imageReference Hello jest system operacyjny hello używane toodefine nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="be1cf-178">przykład Witaj zawiera definicję dla systemu operacyjnego Windows Server:</span><span class="sxs-lookup"><span data-stu-id="be1cf-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="be1cf-179">Może użyć tej definicji, jeśli chcesz toocreate systemu operacyjnego Linux:</span><span class="sxs-lookup"><span data-stu-id="be1cf-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="be1cf-180">Ustawienia konfiguracji dla dysku systemu operacyjnego hello są przypisywane z elementem osDisk hello.</span><span class="sxs-lookup"><span data-stu-id="be1cf-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="be1cf-181">Hello przykładzie zdefiniowano nowego dysku zarządzanego z hello buforowania zestawu trybu zbyt**ReadWrite** i dysku hello jest tworzony z [obrazu platformy](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="be1cf-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="be1cf-182">Tworzenie nowych maszyn wirtualnych z istniejących dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="be1cf-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="be1cf-183">Jeśli chcesz toocreate maszyny wirtualne z istniejącej dysków, Usuń elementu imageReference hello i hello osProfile elementy, a następnie Definiuj następujące ustawienia dysku:</span><span class="sxs-lookup"><span data-stu-id="be1cf-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="be1cf-184">Tworzenie nowych maszyn wirtualnych z zarządzanego obrazu</span><span class="sxs-lookup"><span data-stu-id="be1cf-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="be1cf-185">Jeśli chcesz toocreate maszynę wirtualną z zarządzanego obrazu, zmień element elementu imageReference hello i Definiuj następujące ustawienia dysku:</span><span class="sxs-lookup"><span data-stu-id="be1cf-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="be1cf-186">Dołącz dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="be1cf-186">Attach data disks</span></span>

<span data-ttu-id="be1cf-187">Można opcjonalnie dodawać toohello dysków danych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="be1cf-188">Witaj [liczba dysków](sizes.md) zależy od rozmiaru hello dysku systemu operacyjnego, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="be1cf-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="be1cf-189">Rozmiar maszyn wirtualnych hello hello ustawienie tooStandard_DS1_v2, hello maksymalna liczba dysków z danymi, które mogą zostać dodane toohello ich wynosi dwa.</span><span class="sxs-lookup"><span data-stu-id="be1cf-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="be1cf-190">Przykład Witaj jeden dysk danych zarządzanych jest dodawany tooeach maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="be1cf-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="be1cf-191">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="be1cf-191">Extensions</span></span>

<span data-ttu-id="be1cf-192">Mimo że [rozszerzenia](extensions-features.md) są osobne zasobu, są ściśle związany tooVMs.</span><span class="sxs-lookup"><span data-stu-id="be1cf-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="be1cf-193">Rozszerzenia mogą być dodawane jako zasoby podrzędne hello maszyny Wirtualnej lub jako osobne zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="be1cf-194">przykład Witaj pokazuje hello [rozszerzenia diagnostyki](extensions-diagnostics-template.md) dodawany toohello maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="be1cf-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

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

<span data-ttu-id="be1cf-195">Tego rozszerzenia zasobu używa zmiennej storageName hello i hello diagnostycznych zmienne tooprovide wartości.</span><span class="sxs-lookup"><span data-stu-id="be1cf-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="be1cf-196">Jeśli chcesz toochange hello dane zbierane przez to rozszerzenie, możesz dodać więcej zmiennej wadperfcounters toohello liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="be1cf-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="be1cf-197">Możesz również wybrać tooput hello diagnostyki danych do konta magazynu innego niż przechowywania hello dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="be1cf-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="be1cf-198">Istnieje wiele rozszerzeń, które można zainstalować na maszynie Wirtualnej, ale hello najbardziej przydatne jest prawdopodobnie hello [niestandardowe rozszerzenie skryptu](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="be1cf-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="be1cf-199">Przykład Witaj skrypt programu PowerShell o nazwie start.ps1 działa na każdej maszynie Wirtualnej po pierwszym uruchomieniu:</span><span class="sxs-lookup"><span data-stu-id="be1cf-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="be1cf-200">Witaj start.ps1 skryptu można wykonywać wiele zadań konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="be1cf-201">Na przykład nie są inicjowane dyski danych hello dodanych toohello maszyn wirtualnych w przykładzie hello; można użyć tooinitialize skryptu niestandardowego je.</span><span class="sxs-lookup"><span data-stu-id="be1cf-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="be1cf-202">Jeśli masz wiele toodo zadania uruchamiania, można użyć hello start.ps1 pliku toocall inne skrypty programu PowerShell w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="be1cf-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="be1cf-203">przykład Witaj używa programu PowerShell, ale można użyć dowolnej metody skryptów, która jest dostępna w systemie operacyjnym hello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="be1cf-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="be1cf-204">Można wyświetlić stan hello hello zainstalowanych rozszerzeń hello ustawień rozszerzenia w portalu hello:</span><span class="sxs-lookup"><span data-stu-id="be1cf-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Pobierz stan rozszerzenia](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="be1cf-206">Można również uzyskać informacji o rozszerzeniu za pomocą hello **Get-AzureRmVMExtension** PowerShell polecenia hello **get rozszerzenia maszyny wirtualnej** polecenia Azure CLI 2.0 lub hello **uzyskiwanie informacji o rozszerzeniu**  Interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="be1cf-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="be1cf-207">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="be1cf-207">Deployments</span></span>

<span data-ttu-id="be1cf-208">Podczas wdrażania szablonu Azure śledzi hello zasobów, które wdrożone w grupie i automatycznie przypisuje grupę toothis wdrożone nazwy.</span><span class="sxs-lookup"><span data-stu-id="be1cf-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="be1cf-209">Nazwa Hello wdrożenia hello jest hello taka sama jak nazwa hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="be1cf-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="be1cf-210">Jeśli zastanawiasz się, jak hello stan zasobów we wdrożeniu hello, można użyć hello bloku grupy zasobów w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="be1cf-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Uzyskaj informacje na temat wdrażania](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="be1cf-212">Nie jest problem toouse hello tyle samo zasobów toocreate szablon lub tooupdate istniejących zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="be1cf-213">Korzystając z polecenia toodeploy szablony, masz toosay możliwości hello którego [tryb](../../resource-group-template-deploy.md) ma toouse.</span><span class="sxs-lookup"><span data-stu-id="be1cf-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="be1cf-214">można ustawić trybu Hello tooeither **Complete** lub **przyrostowe**.</span><span class="sxs-lookup"><span data-stu-id="be1cf-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="be1cf-215">Domyślnie Hello jest toodo aktualizacji przyrostowych.</span><span class="sxs-lookup"><span data-stu-id="be1cf-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="be1cf-216">Należy zachować ostrożność przy użyciu hello **Complete** tryb ponieważ przypadkowo usuniesz zasobami.</span><span class="sxs-lookup"><span data-stu-id="be1cf-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="be1cf-217">Po ustawieniu trybu hello zbyt**Complete**, wszystkie zasoby w grupie zasobów hello, które nie znajdują się w szablonie hello usuwa Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="be1cf-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be1cf-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be1cf-218">Next Steps</span></span>

- <span data-ttu-id="be1cf-219">Tworzenie własnych przy użyciu szablonu [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="be1cf-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="be1cf-220">Wdrażanie szablonu hello, które zostały utworzone za pomocą [Utwórz maszynę wirtualną z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="be1cf-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="be1cf-221">Dowiedz się, jak toomanage hello maszyn wirtualnych, które zostały utworzone, przeglądając [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be1cf-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
