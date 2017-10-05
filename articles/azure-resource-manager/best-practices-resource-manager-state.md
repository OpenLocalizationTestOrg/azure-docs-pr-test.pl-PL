---
title: "Złożone wartości przekazywane między szablonami platformy Azure | Dokumentacja firmy Microsoft"
description: "Przedstawia zalecane podejście do danych o stanie udostępniać szablony usługi Azure Resource Manager i połączone przy użyciu obiektów złożonych."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="63a40-103">Stan udziału do i z szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63a40-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="63a40-104">W tym temacie przedstawiono najlepsze rozwiązania dotyczące zarządzania i udostępniania stanu w szablonach.</span><span class="sxs-lookup"><span data-stu-id="63a40-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="63a40-105">Parametry i zmienne, które przedstawiono w tym temacie przedstawiono przykładowe typy obiektów, które można zdefiniować wygodny sposób organizowania wymagań dotyczących wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="63a40-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="63a40-106">W tych przykładach można zaimplementować obiekty z wartości właściwości odpowiednich dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="63a40-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="63a40-107">Ten temat jest częścią większej oficjalny dokument.</span><span class="sxs-lookup"><span data-stu-id="63a40-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="63a40-108">Aby uzyskać pełne papieru, Pobierz [światowej klasy zasobu menedżera szablony zagadnienia i sprawdzonych rozwiązań](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="63a40-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="63a40-109">Określ ustawienia konfiguracji standardowej</span><span class="sxs-lookup"><span data-stu-id="63a40-109">Provide standard configuration settings</span></span>
<span data-ttu-id="63a40-110">Zamiast oferują szablon, który zapewnia elastyczność całkowitej i niezliczonych zmian, wspólnego wzorca ma na celu dostarczenie wybór znanych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="63a40-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="63a40-111">W efekcie, użytkownicy mogą wybrać standardowe rozmiary obrazów na koszulki, takich jak piaskownicy, małych, średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="63a40-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="63a40-112">Inne przykłady rozmiary obrazów na koszulki są ofert produktów, takich jak community edition lub enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="63a40-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="63a40-113">W innych przypadkach może być konfiguracje specyficznego dla obciążenia technologii — takie jak ograniczyć mapy lub nie sql.</span><span class="sxs-lookup"><span data-stu-id="63a40-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="63a40-114">Z obiektów złożonych mogą tworzyć zmiennych, które zawierają zbiory danych, czasami znana jako "zbiory właściwości" i użyć tych danych do deklaracji zasobów na dysku w szablonie.</span><span class="sxs-lookup"><span data-stu-id="63a40-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="63a40-115">Takie podejście zapewnia dobre, znanej konfiguracji o różnych rozmiarach, które są wstępnie skonfigurowane dla klientów.</span><span class="sxs-lookup"><span data-stu-id="63a40-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="63a40-116">Bez znanych konfiguracji użytkowników szablonu musi ustalić klastra zmiany rozmiaru na ich własnych, uwzględnieniu ograniczenia zasobów platformy i wykonywanie obliczeń do identyfikowania wynikowy partycjonowanie konta magazynu i innych zasobów (ze względu na rozmiar klastra i zasoby ograniczenia).</span><span class="sxs-lookup"><span data-stu-id="63a40-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="63a40-117">Oprócz tworzenia lepsze środowisko dla odbiorcy, kilka konfiguracji znane są łatwiejsze do obsługi i ułatwiają dostarczanie wyższego poziomu gęstości.</span><span class="sxs-lookup"><span data-stu-id="63a40-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="63a40-118">Poniższy przykład przedstawia sposób definiowania zmiennych, które zawierają złożone obiekty odpowiadające kolekcji danych.</span><span class="sxs-lookup"><span data-stu-id="63a40-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="63a40-119">Kolekcje zdefiniuj wartości, które są używane dla rozmiaru maszyny wirtualnej, ustawienia sieciowe, ustawień systemu operacyjnego i ustawienia dostępności.</span><span class="sxs-lookup"><span data-stu-id="63a40-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="63a40-120">Zwróć uwagę, że **tshirtSize** zmiennej łączy Rozmiar koszulki udostępnianej parametr (**małych**, **średni**, **duży** ) w tekście **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="63a40-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="63a40-121">Ta zmienna służy do pobierania zmiennej skojarzony obiekt złożony dla tego rozmiar koszulki.</span><span class="sxs-lookup"><span data-stu-id="63a40-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="63a40-122">Następnie można odwoływać się tych zmiennych w dalszej części szablonu.</span><span class="sxs-lookup"><span data-stu-id="63a40-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="63a40-123">Możliwość odwołania o nazwie zmienne i ich właściwości upraszcza składni szablonu i ułatwia zrozumienie kontekstu.</span><span class="sxs-lookup"><span data-stu-id="63a40-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="63a40-124">W poniższym przykładzie zdefiniowano zasobów do wdrożenia przy użyciu obiektów pokazana wcześniej, aby ustawić wartości.</span><span class="sxs-lookup"><span data-stu-id="63a40-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="63a40-125">Na przykład rozmiar maszyny Wirtualnej jest ustawiony przez pobranie wartość `variables('tshirtSize').vmSize` podczas wartość na rozmiar dysku jest pobierana z `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="63a40-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="63a40-126">Ponadto identyfikator URI dla połączonych szablonu jest ustawiony na wartość dla `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="63a40-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="63a40-127">Stan powodzenia do szablonu</span><span class="sxs-lookup"><span data-stu-id="63a40-127">Pass state to a template</span></span>
<span data-ttu-id="63a40-128">Możesz udostępniać stanu do szablonu za pomocą parametrów, które zapewniają bezpośrednio podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="63a40-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="63a40-129">W poniższej tabeli wymieniono typowe parametry w szablonach.</span><span class="sxs-lookup"><span data-stu-id="63a40-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="63a40-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="63a40-130">Name</span></span> | <span data-ttu-id="63a40-131">Wartość</span><span class="sxs-lookup"><span data-stu-id="63a40-131">Value</span></span> | <span data-ttu-id="63a40-132">Opis</span><span class="sxs-lookup"><span data-stu-id="63a40-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="63a40-133">location</span><span class="sxs-lookup"><span data-stu-id="63a40-133">location</span></span> |<span data-ttu-id="63a40-134">Ciąg z listy ograniczone regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="63a40-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="63a40-135">Lokalizacja, w których są wdrożone zasoby.</span><span class="sxs-lookup"><span data-stu-id="63a40-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="63a40-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="63a40-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="63a40-137">Ciąg</span><span class="sxs-lookup"><span data-stu-id="63a40-137">String</span></span> |<span data-ttu-id="63a40-138">Unikatowa nazwa DNS dla konta magazynu rozmieszczenia dysków maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="63a40-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="63a40-139">domainName</span><span class="sxs-lookup"><span data-stu-id="63a40-139">domainName</span></span> |<span data-ttu-id="63a40-140">Ciąg</span><span class="sxs-lookup"><span data-stu-id="63a40-140">String</span></span> |<span data-ttu-id="63a40-141">Nazwa domeny jumpbox publicznie maszyny Wirtualnej w formacie: **{domainName}. { Lokalizacja}.cloudapp.com** na przykład: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="63a40-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="63a40-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="63a40-142">adminUsername</span></span> |<span data-ttu-id="63a40-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="63a40-143">String</span></span> |<span data-ttu-id="63a40-144">Nazwa użytkownika dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="63a40-144">Username for the VMs</span></span> |
| <span data-ttu-id="63a40-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="63a40-145">adminPassword</span></span> |<span data-ttu-id="63a40-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="63a40-146">String</span></span> |<span data-ttu-id="63a40-147">Hasło dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="63a40-147">Password for the VMs</span></span> |
| <span data-ttu-id="63a40-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="63a40-148">tshirtSize</span></span> |<span data-ttu-id="63a40-149">Rozmiary obrazów na koszulki oferowane ciąg z listy ograniczone</span><span class="sxs-lookup"><span data-stu-id="63a40-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="63a40-150">Rozmiar jednostki skalowania o nazwie do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="63a40-150">The named scale unit size to provision.</span></span> <span data-ttu-id="63a40-151">Na przykład "Małe", "Medium", "Duże"</span><span class="sxs-lookup"><span data-stu-id="63a40-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="63a40-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="63a40-152">virtualNetworkName</span></span> |<span data-ttu-id="63a40-153">Ciąg</span><span class="sxs-lookup"><span data-stu-id="63a40-153">String</span></span> |<span data-ttu-id="63a40-154">Nazwa sieci wirtualnej, które użytkownik chce używać.</span><span class="sxs-lookup"><span data-stu-id="63a40-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="63a40-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="63a40-155">enableJumpbox</span></span> |<span data-ttu-id="63a40-156">Ciąg z listą ograniczone (włączone/wyłączone)</span><span class="sxs-lookup"><span data-stu-id="63a40-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="63a40-157">Parametr, który określa, czy włączyć jumpbox dla środowiska.</span><span class="sxs-lookup"><span data-stu-id="63a40-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="63a40-158">Wartości: "enabled", "wyłączone"</span><span class="sxs-lookup"><span data-stu-id="63a40-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="63a40-159">**TshirtSize** parametru użytego w poprzedniej sekcji jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="63a40-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="63a40-160">Przekaż stan połączonego szablonów</span><span class="sxs-lookup"><span data-stu-id="63a40-160">Pass state to linked templates</span></span>
<span data-ttu-id="63a40-161">Podczas nawiązywania połączenia połączonej szablony, można często używać różnych statyczne i wygenerować zmienne.</span><span class="sxs-lookup"><span data-stu-id="63a40-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="63a40-162">Zmienne statyczne</span><span class="sxs-lookup"><span data-stu-id="63a40-162">Static variables</span></span>
<span data-ttu-id="63a40-163">Zmienne statyczne są często używane w celu zapewnienia podstawowej wartości, takie jak adresy URL, które są używane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="63a40-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="63a40-164">W poniższym fragmencie szablonu `templateBaseUrl` Określa katalog główny dla szablonu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="63a40-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="63a40-165">Następnego wiersza tworzy nową zmienną `sharedTemplateUrl` który łączy podstawowy adres URL ze znanej nazwy szablonu zasobów udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="63a40-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="63a40-166">Poniżej tego wiersza, zmienna obiekt złożony jest używany do przechowywania Rozmiar koszulki, gdy podstawowy adres URL jest połączony do lokalizacji szablonu znanej konfiguracji i przechowywane w `vmTemplate` właściwości.</span><span class="sxs-lookup"><span data-stu-id="63a40-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="63a40-167">Zaletą tej metody jest, że zmiana lokalizacji szablonu wystarczy zmienić zmienna statyczna w jednym miejscu, która przechodzi on w całym szablonów połączonych.</span><span class="sxs-lookup"><span data-stu-id="63a40-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="63a40-168">Wygenerowany zmiennych</span><span class="sxs-lookup"><span data-stu-id="63a40-168">Generated variables</span></span>
<span data-ttu-id="63a40-169">Oprócz zmienne statyczne kilku zmiennych są generowane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="63a40-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="63a40-170">W tej sekcji wymieniono niektórych typowych wygenerowanego zmiennych.</span><span class="sxs-lookup"><span data-stu-id="63a40-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="63a40-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="63a40-171">tshirtSize</span></span>
<span data-ttu-id="63a40-172">Znasz tej zmiennej wygenerowanych w powyższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="63a40-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="63a40-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="63a40-173">networkSettings</span></span>
<span data-ttu-id="63a40-174">W wydajność, możliwości lub szablon rozwiązania zakresami end-to-end połączone szablony zwykle Utwórz zasoby, które istnieją w sieci.</span><span class="sxs-lookup"><span data-stu-id="63a40-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="63a40-175">Jednym z podejść prostego jest złożone obiekt używany do przechowywania ustawień sieci i przekazują je do połączonego szablonów.</span><span class="sxs-lookup"><span data-stu-id="63a40-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="63a40-176">Przykład komunikacji ustawienia sieciowe są widoczne poniżej.</span><span class="sxs-lookup"><span data-stu-id="63a40-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="63a40-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="63a40-177">availabilitySettings</span></span>
<span data-ttu-id="63a40-178">Zasoby utworzone w szablonach połączonego często są umieszczane w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="63a40-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="63a40-179">W poniższym przykładzie jest określona nazwa zbioru dostępności, a także liczba domeny błędów i Aktualizacja domeny do użycia.</span><span class="sxs-lookup"><span data-stu-id="63a40-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="63a40-180">Jeśli potrzebujesz wiele zestawów dostępności (na przykład, jeden dla węzłów głównych) i drugi dla węzłów danych, można użyć jako prefiksu nazwy, określ wiele zestawów dostępności lub postępuj zgodnie z modelem przedstawiona wcześniej do utworzenia zmiennej w określonym Rozmiar koszulki.</span><span class="sxs-lookup"><span data-stu-id="63a40-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="63a40-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="63a40-181">storageSettings</span></span>
<span data-ttu-id="63a40-182">Szczegóły magazynu często są współużytkowane z szablonami połączony.</span><span class="sxs-lookup"><span data-stu-id="63a40-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="63a40-183">W poniższym przykładzie *storageSettings* obiektu zawiera szczegółowe informacje dotyczące nazwy konta i kontener magazynu.</span><span class="sxs-lookup"><span data-stu-id="63a40-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="63a40-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="63a40-184">osSettings</span></span>
<span data-ttu-id="63a40-185">Z szablonami połączone konieczne może być przekazać ustawień systemu operacyjnego do różnych typów węzłów w innej konfiguracji znanych typów.</span><span class="sxs-lookup"><span data-stu-id="63a40-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="63a40-186">Obiekt złożony jest łatwo przechowywać i udostępniać informacje dotyczące systemu operacyjnego i również ułatwia obsługują wiele wyborów systemu operacyjnego dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="63a40-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="63a40-187">W poniższym przykładzie przedstawiono dla obiekt *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="63a40-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="63a40-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="63a40-188">machineSettings</span></span>
<span data-ttu-id="63a40-189">Generowana zmienna, *machineSettings* jest obiekt złożony, zawierające kombinację zmiennych core dla tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="63a40-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="63a40-190">Zmienne to nazwa użytkownika administratora i hasła, prefiks dla nazw maszyn wirtualnych i odwołanie do obrazu systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="63a40-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="63a40-191">Należy pamiętać, że *osImageReference* pobiera wartości z *osSettings* zmiennej zdefiniowanej w szablonie głównym.</span><span class="sxs-lookup"><span data-stu-id="63a40-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="63a40-192">Oznacza to, że można łatwo zmienić system operacyjny dla maszyny Wirtualnej — całkowicie lub, w zależności od preferencji konsumenta szablonu.</span><span class="sxs-lookup"><span data-stu-id="63a40-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="63a40-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="63a40-193">vmScripts</span></span>
<span data-ttu-id="63a40-194">*VmScripts* obiekt zawiera szczegółowe informacje o skrypty w celu pobierania i wykonywania w wystąpieniu maszyny Wirtualnej, w tym odniesienia i wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="63a40-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="63a40-195">Poza odwołaniami obejmują infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="63a40-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="63a40-196">Wewnątrz odwołania zawierać zainstalowanego oprogramowania zainstalowanego i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="63a40-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="63a40-197">Możesz użyć *scriptsToDownload* właściwość, aby wyświetlić skryptów do pobrania z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="63a40-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="63a40-198">Ten obiekt zawiera również odwołania do argumentów wiersza polecenia dla różnego rodzaju akcje.</span><span class="sxs-lookup"><span data-stu-id="63a40-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="63a40-199">Czynności te obejmują wykonywanie domyślnej instalacji dla każdego indywidualnego węzła, instalacja wykonywana po wdrożeniu wszystkich węzłów i dodatkowych skryptów, które mogą być specyficzne dla danego szablonu.</span><span class="sxs-lookup"><span data-stu-id="63a40-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="63a40-200">W tym przykładzie jest używany do wdrażania bazy danych MongoDB, co wymaga kryterium zapewniających wysoką dostępność szablonu.</span><span class="sxs-lookup"><span data-stu-id="63a40-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="63a40-201">*ArbiterNodeInstallCommand* został dodany do *vmScripts* zainstalować kryterium.</span><span class="sxs-lookup"><span data-stu-id="63a40-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="63a40-202">W sekcji zmiennych jest, gdzie znaleźć definiujące określony tekst można wykonać skryptu za pomocą odpowiednich wartości zmiennych.</span><span class="sxs-lookup"><span data-stu-id="63a40-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="63a40-203">Zwraca stan z szablonu</span><span class="sxs-lookup"><span data-stu-id="63a40-203">Return state from a template</span></span>
<span data-ttu-id="63a40-204">Nie tylko możesz przekazać dane do szablonu, możesz również udostępniać danych powrót do wywoływania szablonu.</span><span class="sxs-lookup"><span data-stu-id="63a40-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="63a40-205">W **generuje** sekcji połączonych szablonu, możesz podać pary klucz wartość, które mogą być używane w szablonie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="63a40-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="63a40-206">Poniższy przykład przedstawia sposób przekazywania prywatnego adresu IP generowane w szablonie połączony.</span><span class="sxs-lookup"><span data-stu-id="63a40-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="63a40-207">W szablonie głównym można użyć tych danych przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="63a40-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="63a40-208">Można użyć tego wyrażenia w sekcji danych wyjściowych lub sekcji zasobów w szablonie głównym.</span><span class="sxs-lookup"><span data-stu-id="63a40-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="63a40-209">W sekcji zmiennych nie można użyć wyrażenia, ponieważ zależy od stanu czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="63a40-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="63a40-210">Aby przywrócić tę wartość w szablonie głównym, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="63a40-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="63a40-211">Przykład zgodnie z sekcją danych wyjściowych szablonu połączony do zwrócenia dysków z danymi dla maszyny wirtualnej, zobacz [tworzenie wielu dysków danych maszyny wirtualnej](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="63a40-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="63a40-212">Zdefiniuj ustawienia uwierzytelniania dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="63a40-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="63a40-213">Aby określić ustawienia uwierzytelniania dla maszyny wirtualnej, można użyć z tego samego wzorca wcześniej ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="63a40-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="63a40-214">Parametr do przekazania do tworzenia typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="63a40-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="63a40-215">Dodaj zmienne dla typów uwierzytelniania inny i zmienną do przechowywania typ jest używany dla tego wdrożenia na podstawie wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="63a40-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="63a40-216">Podczas definiowania maszyny wirtualnej, należy ustawić **osProfile** do zmiennej został utworzony.</span><span class="sxs-lookup"><span data-stu-id="63a40-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="63a40-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63a40-217">Next steps</span></span>
* <span data-ttu-id="63a40-218">Informacje na temat części szablonu, zobacz [Authoring Azure Resource Manager szablonów](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="63a40-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="63a40-219">Aby poznać funkcje, które są dostępne w ramach szablonu, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="63a40-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
