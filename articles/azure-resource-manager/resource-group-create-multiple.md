---
title: "aaaDeploy wiele wystąpień zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj operacji kopiowania i tablic w tooiterate szablonu usługi Azure Resource Manager wielokrotnie podczas wdrażania zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="6d6b6-103">Wdrażanie wielu wystąpień zasobów lub właściwości w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d6b6-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="6d6b6-104">W tym temacie opisano sposób tooiterate w Twojej toocreate szablonu usługi Azure Resource Manager wiele wystąpień zasobu lub wiele wystąpień właściwości w zasobie.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="6d6b6-105">Jeśli potrzebujesz tooadd logiki tooyour szablon, który pozwala toospecify Określa, czy zasób jest wdrażana, zobacz [warunkowo wdrażanie zasobów](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="6d6b6-106">Iteracja zasobów</span><span class="sxs-lookup"><span data-stu-id="6d6b6-106">Resource iteration</span></span>
<span data-ttu-id="6d6b6-107">Dodawanie wielu wystąpień typu zasobu toocreate `copy` typ zasobu toohello elementu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="6d6b6-108">W elemencie kopiowania hello można określić numer hello iteracji i nazwę tej pętli.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="6d6b6-109">wartość licznika Hello musi być dodatnią liczbą całkowitą i nie może przekraczać 800.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="6d6b6-110">Menedżer zasobów tworzy zasobów hello równolegle.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="6d6b6-111">W związku z tym nie jest gwarantowana hello kolejności, w której zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="6d6b6-112">zasoby toocreate iterowane w sekwencji, zobacz [Serial kopiowania](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="6d6b6-113">toocreate zasobów Hello wielokrotnie przyjmuje hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-113">hello resource toocreate multiple times takes hello following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="6d6b6-114">Zwróć uwagę, że hello nazwa każdego zasobu zawiera hello `copyIndex()` funkcji, która zwraca bieżącą iterację hello w pętli hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="6d6b6-115">`copyIndex()`jest liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="6d6b6-116">Poniższy przykład tak, hello:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="6d6b6-117">Tworzy następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-117">Creates these names:</span></span>

* <span data-ttu-id="6d6b6-118">storage0</span><span class="sxs-lookup"><span data-stu-id="6d6b6-118">storage0</span></span>
* <span data-ttu-id="6d6b6-119">storage1</span><span class="sxs-lookup"><span data-stu-id="6d6b6-119">storage1</span></span>
* <span data-ttu-id="6d6b6-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-120">storage2.</span></span>

<span data-ttu-id="6d6b6-121">wartość indeksu hello toooffset, można przekazać wartość w funkcji copyIndex() hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="6d6b6-122">Hello liczby iteracji tooperform jest nadal określona w elemencie kopiowania hello, ale jest zwracana wartość hello copyIndex w hello określona wartość.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="6d6b6-123">Poniższy przykład tak, hello:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="6d6b6-124">Tworzy następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-124">Creates these names:</span></span>

* <span data-ttu-id="6d6b6-125">storage1</span><span class="sxs-lookup"><span data-stu-id="6d6b6-125">storage1</span></span>
* <span data-ttu-id="6d6b6-126">storage2</span><span class="sxs-lookup"><span data-stu-id="6d6b6-126">storage2</span></span>
* <span data-ttu-id="6d6b6-127">storage3</span><span class="sxs-lookup"><span data-stu-id="6d6b6-127">storage3</span></span>

<span data-ttu-id="6d6b6-128">Operacja kopiowania Hello jest przydatne podczas pracy z tablicami, ponieważ można wykonać iterację każdego elementu w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="6d6b6-129">Użyj hello `length` funkcja na powitania tablicy toospecify hello liczba iteracji, i `copyIndex` tooretrieve hello bieżący indeks w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="6d6b6-130">Poniższy przykład tak, hello:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-130">So, hello following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="6d6b6-131">Tworzy następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-131">Creates these names:</span></span>

* <span data-ttu-id="6d6b6-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="6d6b6-132">storagecontoso</span></span>
* <span data-ttu-id="6d6b6-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="6d6b6-133">storagefabrikam</span></span>
* <span data-ttu-id="6d6b6-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="6d6b6-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="6d6b6-135">Kopiuj szeregowe</span><span class="sxs-lookup"><span data-stu-id="6d6b6-135">Serial copy</span></span>

<span data-ttu-id="6d6b6-136">Gdy używasz hello kopiowania elementu toocreate wiele wystąpień typu zasobu, Menedżer zasobów domyślnie wdroży je równolegle.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="6d6b6-137">Jednak możesz toospecify hello, że zasoby są wdrażane w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="6d6b6-138">Na przykład podczas aktualizacji do środowiska produkcyjnego, może zaistnieć toostagger hello aktualizacji, tylko pewne są aktualizowane w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="6d6b6-139">Usługa Resource Manager zapewnia, że właściwości w elemencie kopiowania hello umożliwiających tooserially można wdrożyć wiele wystąpień.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="6d6b6-140">W zestawie elementów kopiowania hello, `mode` za**serial** i `batchSize` toohello liczbę wystąpień toodeploy naraz.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="6d6b6-141">Serial w trybie Menedżera zasobów tworzy zależność w wystąpieniach wcześniej w pętli hello, więc nie zostanie uruchomiony serii do chwili zakończenia poprzedniej wsadowym hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="6d6b6-142">Witaj właściwości tryb również akceptuje **równoległych**, która jest wartością domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="6d6b6-143">tootest serial kopiowania bez tworzenia rzeczywistych zasobów hello Użyj następującego szablonu, który wdraża pusty zagnieżdżone szablony:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="6d6b6-144">W historii wdrożenia hello Zwróć uwagę, że hello zagnieżdżonych wdrożenia są przetwarzane w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![Serial wdrożenia](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="6d6b6-146">Dla scenariusza bardziej realistyczne hello poniższy przykład wdraża dwóch wystąpień w czasie z zagnieżdżonych szablonu maszyny wirtualnej systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="6d6b6-147">Właściwość iteracji</span><span class="sxs-lookup"><span data-stu-id="6d6b6-147">Property iteration</span></span>

<span data-ttu-id="6d6b6-148">Dodaj wiele wartości dla właściwości w zasobie toocreate `copy` tablicy w elemencie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="6d6b6-149">Ta tablica zawiera obiekty, a każdy obiekt ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="6d6b6-150">Nazwa hello z toocreate właściwości hello wielu wartości</span><span class="sxs-lookup"><span data-stu-id="6d6b6-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="6d6b6-151">Liczba — liczba hello toocreate wartości</span><span class="sxs-lookup"><span data-stu-id="6d6b6-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="6d6b6-152">dane wejściowe - obiekt, który zawiera właściwości toohello tooassign wartości hello</span><span class="sxs-lookup"><span data-stu-id="6d6b6-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="6d6b6-153">powitania po przykładzie pokazano, jak tooapply `copy` toohello dataDisks właściwości na maszynie wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="6d6b6-154">Zwróć uwagę, że przy użyciu `copyIndex` wewnątrz iteracji właściwości, należy podać nazwę hello hello iteracji.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="6d6b6-155">Nie masz nazwy hello tooprovide, gdy jest używany z zasobów iteracji.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="6d6b6-156">Menedżer zasobów rozszerza hello `copy` tablicy podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="6d6b6-157">Nazwa Hello tablicy hello staje się nazwa hello hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="6d6b6-158">wartości wejściowe Hello stają się hello właściwości obiektu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-158">hello input values become hello object properties.</span></span> <span data-ttu-id="6d6b6-159">Witaj wdrożyć szablon staje się:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-159">hello deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="6d6b6-160">Iteracja zasobów i właściwości można użyć razem.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="6d6b6-161">Odwołanie hello iteracji właściwości według nazwy.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-161">Reference hello property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="6d6b6-162">Może zawierać tylko jeden element kopiowania hello właściwości dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="6d6b6-163">toospecify iteracji pętli dla więcej niż jedną właściwość, należy zdefiniować wiele obiektów w hello kopiowania tablicy.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="6d6b6-164">Każdy obiekt jest iterowane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-164">Each object is iterated separately.</span></span> <span data-ttu-id="6d6b6-165">Na przykład toocreate wiele wystąpień zarówno hello `frontendIPConfigurations` właściwości i hello `loadBalancingRules` właściwości modułu równoważenia obciążenia, zdefiniuj zarówno do obiektów w elemencie pojedynczej kopii:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="6d6b6-166">Są zależne od zasobów w pętli</span><span class="sxs-lookup"><span data-stu-id="6d6b6-166">Depend on resources in a loop</span></span>
<span data-ttu-id="6d6b6-167">Określ, czy zasób jest wdrażane po innego zasobu za pomocą hello `dependsOn` elementu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="6d6b6-168">toodeploy z zasobem, który jest zależny od hello kolekcji zasobów w pętli, podaj nazwę hello pętlę kopiowania hello w elemencie dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="6d6b6-169">Witaj poniższy przykład pokazuje, jak toodeploy trzy konta magazynu przed wdrożeniem hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="6d6b6-170">Witaj pełnej definicji maszyny wirtualnej nie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="6d6b6-171">Powiadomienia elementu kopiowania hello ma nazwę ustawić także`storagecopy` i elementu dependsOn hello hello maszyn wirtualnych jest również ustawiona zbyt`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="6d6b6-172">Tworzenie wielu wystąpień zasobu podrzędnego</span><span class="sxs-lookup"><span data-stu-id="6d6b6-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="6d6b6-173">Nie można używać pętli kopii zasobu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="6d6b6-174">toocreate wiele wystąpień z zasobem, który zazwyczaj zdefiniowane jako zagnieżdżony w innym zasobem, należy zamiast tego utworzyć tego zasobu jako zasób najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="6d6b6-175">Można zdefiniować relacji hello z zasobu nadrzędnego hello za pośrednictwem hello typem i nazwą właściwości.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="6d6b6-176">Na przykład załóżmy, że zazwyczaj Definiowanie zestawu danych jako zasób podrzędnych w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="6d6b6-177">toocreate instancje zestawów danych, przenieś go poza hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="6d6b6-178">Hello zestawu danych musi znajdować się na powitania sam poziom jako hello fabryki danych, ale nadal jest zasobem podrzędnych hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="6d6b6-179">Możesz zachować hello relacja między zestawu danych i fabryki danych za pośrednictwem hello typem i nazwą właściwości.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="6d6b6-180">Ponieważ nie można wywnioskować typu z pozycji w szablonie hello, musisz podać typ hello w pełni kwalifikowana w formacie hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="6d6b6-181">tooestablish relacji nadrzędny/podrzędny z wystąpienia fabryki danych hello, podaj nazwę dla zestawu danych hello, która zawiera nazwę zasobu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="6d6b6-182">Użyj formatu hello: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="6d6b6-183">Witaj poniższy przykład przedstawia implementację hello:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-183">hello following example shows hello implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="6d6b6-184">Warunkowo wdrażanie zasobów</span><span class="sxs-lookup"><span data-stu-id="6d6b6-184">Conditionally deploy resource</span></span>

<span data-ttu-id="6d6b6-185">toospecify, czy zasób jest wdrażana, użyj hello `condition` elementu.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="6d6b6-186">Witaj wartość dla tego elementu rozpoznaje tootrue, lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="6d6b6-187">Jeśli wartość hello ma wartość true, zasobów hello jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="6d6b6-188">Gdy wartość hello ma wartość false, hello zasobów nie są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="6d6b6-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="6d6b6-189">Na przykład toospecify czy nowe konto magazynu jest wdrożony lub istniejącego konta magazynu jest używany, użyj:</span><span class="sxs-lookup"><span data-stu-id="6d6b6-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="6d6b6-190">Na przykład za pomocą nowego lub istniejącego zasobu, zobacz [nowy lub istniejący szablon warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="6d6b6-191">Na przykład przy użyciu hasła lub maszyny wirtualnej toodeploy klucza SSH, zobacz [nazwa użytkownika lub SSH szablonu warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d6b6-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d6b6-192">Next steps</span></span>
* <span data-ttu-id="6d6b6-193">Jeśli toolearn sekcje hello szablonu informacje, zobacz [Authoring Azure Resource Manager szablony](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6d6b6-194">toolearn jak toodeploy szablonu, zobacz [wdrażanie aplikacji przy użyciu szablonu usługi Resource Manager Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6d6b6-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

