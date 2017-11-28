---
title: "Maszyny wirtualne w szablonie usługi Azure Resource Manager | Microsoft Azure"
description: "Dowiedz się więcej na temat sposobu zasobu maszyny wirtualnej jest zdefiniowany w szablonie usługi Azure Resource Manager."
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
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="86732-103">Maszyny wirtualne w szablonie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="86732-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="86732-104">W tym artykule opisano aspekty szablonu usługi Azure Resource Manager, które są stosowane do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="86732-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="86732-105">W tym artykule nie opisano pełną szablonu do utworzenia maszyny wirtualnej; w tym należy definicji zasobu dla kont magazynu, interfejsy sieciowe publicznych adresów IP i sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="86732-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="86732-106">Aby uzyskać więcej informacji o sposobie tych zasobów można definiować razem, zobacz [Przewodnik po szablonie usługi Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="86732-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="86732-107">Istnieje wiele [szablony w galerii](https://azure.microsoft.com/documentation/templates/?term=VM) zawierające zasobu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="86732-108">Nie wszystkie elementy, które można uwzględnić w szablonie są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="86732-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="86732-109">W tym przykładzie pokazano sekcję typowe zasobu szablon umożliwiający tworzenie określonej liczby maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="86732-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="86732-110">W tym przykładzie opiera się na konto magazynu, który został wcześniej utworzony.</span><span class="sxs-lookup"><span data-stu-id="86732-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="86732-111">Konta magazynu można utworzyć przez wdrożenie jej z szablonu.</span><span class="sxs-lookup"><span data-stu-id="86732-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="86732-112">Przykład również zależy od interfejsu sieciowego i jego zasoby zależne, zdefiniowane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="86732-113">Te zasoby nie są wyświetlane w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="86732-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="86732-114">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="86732-114">API Version</span></span>

<span data-ttu-id="86732-115">Podczas wdrażania zasobów przy użyciu szablonu, należy określić wersję interfejsu API do użycia.</span><span class="sxs-lookup"><span data-stu-id="86732-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="86732-116">W przykładzie pokazano zasobu maszyny wirtualnej za pomocą tego elementu apiVersion:</span><span class="sxs-lookup"><span data-stu-id="86732-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="86732-117">Wersja interfejsu API, określ w szablonie dotyczy właściwości, które można zdefiniować w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="86732-118">Ogólnie rzecz biorąc należy zaznaczyć najnowszą wersję interfejsu API, podczas tworzenia szablonów.</span><span class="sxs-lookup"><span data-stu-id="86732-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="86732-119">Istniejących szablonów można zdecydować, czy chcesz nadal używać starszej wersji interfejsu API, lub zaktualizować szablon do najnowszej wersji móc korzystać z nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="86732-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="86732-120">Użyj tych możliwości pobierania najnowszej wersji interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="86732-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="86732-121">Interfejs API REST - [listy wszystkich dostawców zasobów](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="86732-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="86732-122">PowerShell — [Get AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="86732-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="86732-123">Azure CLI 2.0 — [az Pokaż dostawcy](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="86732-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="86732-124">Parametry i zmienne</span><span class="sxs-lookup"><span data-stu-id="86732-124">Parameters and variables</span></span>

<span data-ttu-id="86732-125">[Parametry](../../resource-group-authoring-templates.md) ułatwiają określenie wartości dla szablonu po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="86732-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="86732-126">W tej sekcji parametrów jest używana w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="86732-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="86732-127">Podczas wdrażania szablonu przykład wprowadzenie wartości dla nazwy i hasła konta administratora na każdej maszyny Wirtualnej i liczbę maszyn wirtualnych, aby utworzyć.</span><span class="sxs-lookup"><span data-stu-id="86732-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="86732-128">Istnieje możliwość określenia wartości parametrów w osobnym pliku, który jest zarządzany przy użyciu szablonu lub podanie wartości po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="86732-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="86732-129">[Zmienne](../../resource-group-authoring-templates.md) ułatwiają konfigurowanie wartości w szablonie często używane w całej go lub które mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="86732-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="86732-130">W tej sekcji zmiennych jest używana w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="86732-130">This variables section is used in the example:</span></span>

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

<span data-ttu-id="86732-131">Podczas wdrażania szablonu przykładowe wartości zmiennych są używane nazwy i identyfikatora wcześniej utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="86732-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="86732-132">Zmienne są również używane w celu zapewnienia ustawień diagnostycznych rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="86732-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="86732-133">Użyj [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](../../resource-manager-template-best-practices.md) Aby określić sposób strukturę parametrów i zmiennych w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="86732-134">Pętle zasobów</span><span class="sxs-lookup"><span data-stu-id="86732-134">Resource loops</span></span>

<span data-ttu-id="86732-135">Jeśli potrzebujesz więcej niż jednej maszyny wirtualnej dla aplikacji, można użyć elementu kopiowania w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="86732-136">Ten opcjonalny element w pętli tworzenie liczby maszyn wirtualnych, które określono jako parametr:</span><span class="sxs-lookup"><span data-stu-id="86732-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="86732-137">Zauważ również, w tym przykładzie użytą indeks pętli, określając niektóre wartości dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="86732-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="86732-138">Na przykład jeśli wprowadzono liczby wystąpień trzy nazwy dysków systemu operacyjnego są myOSDisk1, myOSDisk2 i myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="86732-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="86732-139">W tym przykładzie użyto zarządzanych dyski dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="86732-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="86732-140">Należy pamiętać, że tworzenie pętli dla jednego zasobu w szablonie może wymagać używania pętli podczas tworzenia lub uzyskiwania dostępu do innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="86732-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="86732-141">Na przykład wiele maszyn wirtualnych nie mogą używać tego samego interfejsu sieciowego, dlatego jeśli szablonu w pętli tworzenia trzech maszyn wirtualnych należy również pętli przez proces tworzenia trzech interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="86732-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="86732-142">Podczas przypisywania do interfejsu sieciowego z maszyną wirtualną, indeks pętli jest używany do identyfikowania go:</span><span class="sxs-lookup"><span data-stu-id="86732-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="86732-143">Zależności</span><span class="sxs-lookup"><span data-stu-id="86732-143">Dependencies</span></span>

<span data-ttu-id="86732-144">Najwięcej zasobów są zależne od innych zasobów potrzebnych do prawidłowego działania.</span><span class="sxs-lookup"><span data-stu-id="86732-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="86732-145">Maszyny wirtualne muszą być skojarzone z siecią wirtualną i zrobić, że wymaga ona interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="86732-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="86732-146">[DependsOn](../../resource-group-define-dependencies.md) element służy do upewnij się, że interfejs sieciowy jest gotowa do użycia, przed utworzeniem maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="86732-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="86732-147">Menedżer zasobów wdraża równolegle wszystkie zasoby, które nie są zależne od innego zasobu wdrażany.</span><span class="sxs-lookup"><span data-stu-id="86732-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="86732-148">Należy zachować ostrożność podczas ustawiania zależności, ponieważ przypadkowo spowalniają wdrożenia przez określenie niepotrzebnych zależności.</span><span class="sxs-lookup"><span data-stu-id="86732-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="86732-149">Zależności mogą być powiązane za pomocą wielu zasobów.</span><span class="sxs-lookup"><span data-stu-id="86732-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="86732-150">Na przykład interfejsu sieciowego jest zależna od publicznego adresu IP i zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="86732-151">Jak sprawdzić, czy zależność jest wymagane?</span><span class="sxs-lookup"><span data-stu-id="86732-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="86732-152">Sprawdź wartości ustawionej w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-152">Look at the values you set in the template.</span></span> <span data-ttu-id="86732-153">Element punktów definicji zasobu maszyny wirtualnej do innego zasobu, które zostało wdrożone w tym samym szablonie, należy najpierw zależności.</span><span class="sxs-lookup"><span data-stu-id="86732-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="86732-154">Na przykład na komputerze wirtualnym przykład definiuje profilu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="86732-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="86732-155">Aby ustawić tę właściwość, musi istnieć interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="86732-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="86732-156">W związku z tym należy zależności.</span><span class="sxs-lookup"><span data-stu-id="86732-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="86732-157">Należy również ustawić zależność, gdy jeden zasób (podrzędny) zdefiniowano w ramach innego zasobu (nadrzędnego).</span><span class="sxs-lookup"><span data-stu-id="86732-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="86732-158">Na przykład ustawienia diagnostyki i rozszerzenia niestandardowego skryptu są oba zdefiniowane jako zasoby podrzędne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="86732-159">Nie można utworzyć dopóki maszyna wirtualna istnieje.</span><span class="sxs-lookup"><span data-stu-id="86732-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="86732-160">W związku z tym oba zasoby są oznaczone jako zależne od maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="86732-161">Profile</span><span class="sxs-lookup"><span data-stu-id="86732-161">Profiles</span></span>

<span data-ttu-id="86732-162">Niektóre elementy profilu są używane podczas definiowania zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="86732-163">Niektóre są wymagane, a inne opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="86732-163">Some are required and some are optional.</span></span> <span data-ttu-id="86732-164">Na przykład hardwareProfile, osProfile storageProfile i networkProfile elementy są wymagane, ale diagnosticsProfile jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="86732-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="86732-165">Te profile zdefiniować ustawienia, takie jak:</span><span class="sxs-lookup"><span data-stu-id="86732-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="86732-166">rozmiar</span><span class="sxs-lookup"><span data-stu-id="86732-166">size</span></span>](sizes.md)
- <span data-ttu-id="86732-167">[Nazwa](/architecture/best-practices/naming-conventions) i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="86732-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="86732-168">dysk i [ustawień systemu operacyjnego](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="86732-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="86732-169">Interfejs sieciowy</span><span class="sxs-lookup"><span data-stu-id="86732-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="86732-170">Diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="86732-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="86732-171">Dyski i obrazów</span><span class="sxs-lookup"><span data-stu-id="86732-171">Disks and images</span></span>
   
<span data-ttu-id="86732-172">Na platformie Azure, pliki wirtualnego dysku twardego może reprezentować [dysków lub obrazów](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86732-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="86732-173">W przypadku systemu operacyjnego w pliku vhd jest przeznaczone do można określonej maszyny Wirtualnej, jest określana na jako dysk.</span><span class="sxs-lookup"><span data-stu-id="86732-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="86732-174">Gdy systemu operacyjnego w pliku vhd jest uogólnione w celu można utworzyć wiele maszyn wirtualnych, jego jest określany jako obraz.</span><span class="sxs-lookup"><span data-stu-id="86732-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="86732-175">Tworzenie nowych maszyn wirtualnych i nowych dysków z obrazu platformy</span><span class="sxs-lookup"><span data-stu-id="86732-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="86732-176">Podczas tworzenia maszyny Wirtualnej należy zdecydować, jakiego systemu operacyjnego do użycia.</span><span class="sxs-lookup"><span data-stu-id="86732-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="86732-177">Element elementu imageReference służy do definiowania nowej maszyny Wirtualnej systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="86732-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="86732-178">W przykładzie pokazano definicję dla systemu operacyjnego Windows Server:</span><span class="sxs-lookup"><span data-stu-id="86732-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="86732-179">Może użyć tej definicji, jeśli chcesz utworzyć systemu operacyjnego Linux:</span><span class="sxs-lookup"><span data-stu-id="86732-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="86732-180">Ustawienia konfiguracji dla dysku systemu operacyjnego są przypisywane z elementem osDisk.</span><span class="sxs-lookup"><span data-stu-id="86732-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="86732-181">W przykładzie zdefiniowano nowych dysków zarządzanych w trybie buforowania, wartość **ReadWrite** i że dysk jest tworzony z [obrazu platformy](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="86732-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="86732-182">Tworzenie nowych maszyn wirtualnych z istniejących dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="86732-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="86732-183">Jeśli chcesz tworzyć maszyny wirtualne z istniejącej dysków, Usuń elementu imageReference i elementy osProfile i Definiuj następujące ustawienia dysku:</span><span class="sxs-lookup"><span data-stu-id="86732-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="86732-184">Tworzenie nowych maszyn wirtualnych z zarządzanego obrazu</span><span class="sxs-lookup"><span data-stu-id="86732-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="86732-185">Jeśli chcesz utworzyć maszynę wirtualną z do zarządzanego obrazu, zmień element elementu imageReference i Definiuj następujące ustawienia dysku:</span><span class="sxs-lookup"><span data-stu-id="86732-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="86732-186">Dołącz dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="86732-186">Attach data disks</span></span>

<span data-ttu-id="86732-187">Można opcjonalnie dodawać dysków z danymi z maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="86732-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="86732-188">[Liczba dysków](sizes.md) zależy od rozmiaru dysku systemu operacyjnego, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="86732-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="86732-189">Maksymalna liczba dysków danych, które można dodać do nich o rozmiarze maszyn wirtualnych ustawioną Standard_DS1_v2 wynosi dwa.</span><span class="sxs-lookup"><span data-stu-id="86732-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="86732-190">W tym przykładzie jeden dysk danych zarządzanych jest dodawany do każdej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="86732-190">In the example, one managed data disk is being added to each VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="86732-191">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="86732-191">Extensions</span></span>

<span data-ttu-id="86732-192">Mimo że [rozszerzenia](extensions-features.md) są osobne zasobu, są ściśle powiązane maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="86732-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="86732-193">Rozszerzenia mogą być dodawane jako zasób podrzędnych maszyny wirtualnej lub jako osobne zasób.</span><span class="sxs-lookup"><span data-stu-id="86732-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="86732-194">W przykładzie [rozszerzenia diagnostyki](extensions-diagnostics-template.md) dodawany do maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="86732-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

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

<span data-ttu-id="86732-195">Tego rozszerzenia zasobu używa zmiennej storageName i zmienne diagnostycznych, aby zapewnić wartości.</span><span class="sxs-lookup"><span data-stu-id="86732-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="86732-196">Jeśli chcesz zmienić dane, które są zbierane przez to rozszerzenie, możesz dodać więcej liczników wydajności do zmiennej wadperfcounters.</span><span class="sxs-lookup"><span data-stu-id="86732-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="86732-197">Można również wybrać umieszczanie danych diagnostycznych do konta magazynu innego niż przechowywania dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="86732-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="86732-198">Istnieje wiele rozszerzeń, które można zainstalować na maszynie Wirtualnej, ale najbardziej przydatne jest prawdopodobnie [niestandardowe rozszerzenie skryptu](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="86732-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="86732-199">W tym przykładzie skrypt programu PowerShell o nazwie start.ps1 działa na każdej maszynie Wirtualnej po pierwszym uruchomieniu:</span><span class="sxs-lookup"><span data-stu-id="86732-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="86732-200">Skrypt start.ps1 można wykonywać wiele zadań konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="86732-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="86732-201">Na przykład dysków z danymi, które są dodawane do maszyn wirtualnych w tym przykładzie nie jest inicjowany; niestandardowego skryptu służy do ich inicjowania.</span><span class="sxs-lookup"><span data-stu-id="86732-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="86732-202">Jeśli masz wiele zadań uruchamiania zrobić, można użyć pliku start.ps1 do wywołania inne skrypty programu PowerShell w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="86732-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="86732-203">W przykładzie użyto programu PowerShell, ale można użyć dowolnej metody skryptów, która jest dostępna w systemie operacyjnym, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="86732-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="86732-204">Można wyświetlić stan zainstalowanych rozszerzeń z ustawień rozszerzenia w portalu:</span><span class="sxs-lookup"><span data-stu-id="86732-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Pobierz stan rozszerzenia](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="86732-206">Można także uzyskać informacji o rozszerzeniu przy użyciu **Get-AzureRmVMExtension** polecenia programu PowerShell **get rozszerzenia maszyny wirtualnej** polecenia Azure CLI 2.0 lub **uzyskiwanie informacji o rozszerzeniu** INTERFEJS API REST.</span><span class="sxs-lookup"><span data-stu-id="86732-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="86732-207">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="86732-207">Deployments</span></span>

<span data-ttu-id="86732-208">Podczas wdrażania szablonu Azure śledzi zasoby wdrożone w grupie, a następnie automatycznie przypisuje nazwę do wdrożonej grupy.</span><span class="sxs-lookup"><span data-stu-id="86732-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="86732-209">Nazwa wdrożenia jest taka sama jak nazwa szablonu.</span><span class="sxs-lookup"><span data-stu-id="86732-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="86732-210">Jeśli zastanawiasz się, jak stan zasobów we wdrożeniu, można użyć bloku grupy zasobów w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="86732-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Uzyskaj informacje na temat wdrażania](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="86732-212">Nie jest problem do używania tego samego szablonu, aby utworzyć zasobów lub zaktualizować istniejące zasoby.</span><span class="sxs-lookup"><span data-stu-id="86732-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="86732-213">Korzystając z polecenia do wdrażania szablonów, masz możliwość powiedzieć, które [tryb](../../resource-group-template-deploy.md) chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="86732-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="86732-214">Tryb może być ustawiona jako **Complete** lub **przyrostowe**.</span><span class="sxs-lookup"><span data-stu-id="86732-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="86732-215">Wartość domyślna to robić aktualizacji przyrostowych.</span><span class="sxs-lookup"><span data-stu-id="86732-215">The default is to do incremental updates.</span></span> <span data-ttu-id="86732-216">Należy zachować ostrożność przy użyciu **Complete** tryb ponieważ przypadkowo usuniesz zasobami.</span><span class="sxs-lookup"><span data-stu-id="86732-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="86732-217">Po ustawieniu trybu **Complete**, Menedżer zasobów usuwa wszystkie zasoby w grupie zasobów, które nie znajdują się w szablonie.</span><span class="sxs-lookup"><span data-stu-id="86732-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86732-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86732-218">Next Steps</span></span>

- <span data-ttu-id="86732-219">Tworzenie własnych przy użyciu szablonu [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="86732-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="86732-220">Wdrażanie szablonu, który został utworzony przy użyciu [Utwórz maszynę wirtualną z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="86732-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="86732-221">Dowiedz się, jak zarządzać maszynami wirtualnymi, które zostały utworzone, przeglądając [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86732-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
