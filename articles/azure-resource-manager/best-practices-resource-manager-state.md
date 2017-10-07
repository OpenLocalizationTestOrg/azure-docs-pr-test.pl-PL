---
title: "złożone wartości aaaPass między szablonami platformy Azure | Dokumentacja firmy Microsoft"
description: "Przedstawia zalecane podejścia do korzystania z usługi Azure Resource Manager szablony i połączone przy użyciu danych o stanie tooshare obiektów złożonych."
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="dcb88-103">Udostępnianie tooand stanu z szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dcb88-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="dcb88-104">W tym temacie przedstawiono najlepsze rozwiązania dotyczące zarządzania i udostępniania stanu w szablonach.</span><span class="sxs-lookup"><span data-stu-id="dcb88-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="dcb88-105">Witaj parametry i zmienne, które przedstawiono w tym temacie przedstawiono przykłady typu hello obiektów można zdefiniować tooconveniently organizowanie wymagań dotyczących wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="dcb88-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="dcb88-106">W tych przykładach można zaimplementować obiekty z wartości właściwości odpowiednich dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="dcb88-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="dcb88-107">Ten temat jest częścią większej oficjalny dokument.</span><span class="sxs-lookup"><span data-stu-id="dcb88-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="dcb88-108">Pobierz hello tooread pełnej papier [światowej klasy zasobu menedżera szablony zagadnienia i sprawdzonych rozwiązań](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="dcb88-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="dcb88-109">Określ ustawienia konfiguracji standardowej</span><span class="sxs-lookup"><span data-stu-id="dcb88-109">Provide standard configuration settings</span></span>
<span data-ttu-id="dcb88-110">Zamiast oferują szablon, który zapewnia elastyczność całkowitej i niezliczonych zmian, wspólnego wzorca jest tooprovide wybór znanych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dcb88-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="dcb88-111">W efekcie, użytkownicy mogą wybrać standardowe rozmiary obrazów na koszulki, takich jak piaskownicy, małych, średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="dcb88-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="dcb88-112">Inne przykłady rozmiary obrazów na koszulki są ofert produktów, takich jak community edition lub enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="dcb88-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="dcb88-113">W innych przypadkach może być konfiguracje specyficznego dla obciążenia technologii — takie jak ograniczyć mapy lub nie sql.</span><span class="sxs-lookup"><span data-stu-id="dcb88-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="dcb88-114">Złożone obiekty możesz tworzyć zmiennych, które zawierają zbiory danych, czasami znana jako "zbiory właściwości" i użyj deklaracja zasobów hello toodrive danych w szablonie.</span><span class="sxs-lookup"><span data-stu-id="dcb88-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="dcb88-115">Takie podejście zapewnia dobre, znanej konfiguracji o różnych rozmiarach, które są wstępnie skonfigurowane dla klientów.</span><span class="sxs-lookup"><span data-stu-id="dcb88-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="dcb88-116">Bez znanych konfiguracji użytkowników hello szablonu musi określić rozmiaru klastra na ich własnych, współczynnik w powiązanych zasobów platformy i czy matematyczne tooidentify hello wynikowa partycjonowanie konta magazynu i innych zasobów (ze względu na rozmiar toocluster i ograniczenia zasobów).</span><span class="sxs-lookup"><span data-stu-id="dcb88-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="dcb88-117">Ponadto toomaking lepsze środowisko dla powitania klienta kilka znanych konfiguracji są łatwiejsze toosupport i ułatwiają dostarczanie wyższego poziomu gęstości.</span><span class="sxs-lookup"><span data-stu-id="dcb88-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="dcb88-118">powitania po przykładzie pokazano, jak toodefine zmiennych, które zawierają złożone obiekty odpowiadające kolekcji danych.</span><span class="sxs-lookup"><span data-stu-id="dcb88-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="dcb88-119">kolekcje Hello zdefiniuj wartości, które są używane dla rozmiaru maszyny wirtualnej, ustawienia sieciowe, ustawień systemu operacyjnego i ustawienia dostępności.</span><span class="sxs-lookup"><span data-stu-id="dcb88-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="dcb88-120">Zwróć uwagę, że hello **tshirtSize** zmiennej łączy Rozmiar koszulki hello udostępnianej parametr (**małych**, **średni**, **duży**) tekst toohello **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="dcb88-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="dcb88-121">Ten rozmiar koszulki używany tej zmiennej tooretrieve hello skojarzony obiekt złożony zmiennej.</span><span class="sxs-lookup"><span data-stu-id="dcb88-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="dcb88-122">Następnie można odwoływać się tych zmiennych w dalszej części hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="dcb88-123">Witaj możliwości tooreference o nazwie — zmienne i ich właściwości upraszcza składni szablonu hello i umożliwia łatwe toounderstand kontekstu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="dcb88-124">Poniższy przykład Hello definiuje toodeploy zasobów za pomocą obiektów hello przedstawione wcześniej tooset wartości.</span><span class="sxs-lookup"><span data-stu-id="dcb88-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="dcb88-125">Na przykład hello rozmiar maszyny Wirtualnej jest ustawiana przez pobierania wartości hello `variables('tshirtSize').vmSize` podczas hello wartość na rozmiar dysku hello są pobierane z `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="dcb88-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="dcb88-126">Ponadto hello identyfikatora URI dla połączonych szablonu jest ustawiony z wartością hello `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="dcb88-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="dcb88-127">Przekaż szablon tooa stanu</span><span class="sxs-lookup"><span data-stu-id="dcb88-127">Pass state tooa template</span></span>
<span data-ttu-id="dcb88-128">Możesz udostępniać stanu do szablonu za pomocą parametrów, które zapewniają bezpośrednio podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="dcb88-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="dcb88-129">Witaj następujące parametry tabeli listy najczęściej używanych w szablonach.</span><span class="sxs-lookup"><span data-stu-id="dcb88-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="dcb88-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dcb88-130">Name</span></span> | <span data-ttu-id="dcb88-131">Wartość</span><span class="sxs-lookup"><span data-stu-id="dcb88-131">Value</span></span> | <span data-ttu-id="dcb88-132">Opis</span><span class="sxs-lookup"><span data-stu-id="dcb88-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dcb88-133">location</span><span class="sxs-lookup"><span data-stu-id="dcb88-133">location</span></span> |<span data-ttu-id="dcb88-134">Ciąg z listy ograniczone regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dcb88-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="dcb88-135">Lokalizacja Hello wdrożonym hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="dcb88-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="dcb88-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="dcb88-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="dcb88-137">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dcb88-137">String</span></span> |<span data-ttu-id="dcb88-138">Unikatową nazwę DNS hello rozmieszczenia dysków hello wirtualna konta magazynu</span><span class="sxs-lookup"><span data-stu-id="dcb88-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="dcb88-139">domainName</span><span class="sxs-lookup"><span data-stu-id="dcb88-139">domainName</span></span> |<span data-ttu-id="dcb88-140">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dcb88-140">String</span></span> |<span data-ttu-id="dcb88-141">Nazwa domeny hello publicznie jumpbox maszyny Wirtualnej w formacie hello: **{domainName}. { Lokalizacja}.cloudapp.com** na przykład: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="dcb88-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="dcb88-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="dcb88-142">adminUsername</span></span> |<span data-ttu-id="dcb88-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dcb88-143">String</span></span> |<span data-ttu-id="dcb88-144">Nazwa użytkownika dla hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="dcb88-144">Username for hello VMs</span></span> |
| <span data-ttu-id="dcb88-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="dcb88-145">adminPassword</span></span> |<span data-ttu-id="dcb88-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dcb88-146">String</span></span> |<span data-ttu-id="dcb88-147">Hasło dla hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="dcb88-147">Password for hello VMs</span></span> |
| <span data-ttu-id="dcb88-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="dcb88-148">tshirtSize</span></span> |<span data-ttu-id="dcb88-149">Rozmiary obrazów na koszulki oferowane ciąg z listy ograniczone</span><span class="sxs-lookup"><span data-stu-id="dcb88-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="dcb88-150">Witaj o nazwie tooprovision rozmiar jednostki skalowania.</span><span class="sxs-lookup"><span data-stu-id="dcb88-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="dcb88-151">Na przykład "Małe", "Medium", "Duże"</span><span class="sxs-lookup"><span data-stu-id="dcb88-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="dcb88-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="dcb88-152">virtualNetworkName</span></span> |<span data-ttu-id="dcb88-153">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dcb88-153">String</span></span> |<span data-ttu-id="dcb88-154">Nazwa hello sieci wirtualnej hello konsumenta chce toouse.</span><span class="sxs-lookup"><span data-stu-id="dcb88-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="dcb88-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="dcb88-155">enableJumpbox</span></span> |<span data-ttu-id="dcb88-156">Ciąg z listą ograniczone (włączone/wyłączone)</span><span class="sxs-lookup"><span data-stu-id="dcb88-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="dcb88-157">Parametr, który identyfikuje czy tooenable jumpbox hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="dcb88-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="dcb88-158">Wartości: "enabled", "wyłączone"</span><span class="sxs-lookup"><span data-stu-id="dcb88-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="dcb88-159">Witaj **tshirtSize** parametru użytego w poprzedniej sekcji hello jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="dcb88-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="dcb88-160">Przekaż szablony toolinked stanu</span><span class="sxs-lookup"><span data-stu-id="dcb88-160">Pass state toolinked templates</span></span>
<span data-ttu-id="dcb88-161">Podczas łączenia z toolinked szablony, można często używać różnych statyczne i wygenerować zmienne.</span><span class="sxs-lookup"><span data-stu-id="dcb88-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="dcb88-162">Zmienne statyczne</span><span class="sxs-lookup"><span data-stu-id="dcb88-162">Static variables</span></span>
<span data-ttu-id="dcb88-163">Zmienne statyczne są często wartości podstawowe tooprovide używane, takie jak adresy URL, które są używane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="dcb88-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="dcb88-164">W hello następującego fragmentu szablonu `templateBaseUrl` Określa lokalizację głównego hello hello szablonu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="dcb88-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="dcb88-165">Witaj w następnym wierszu tworzy nową zmienną `sharedTemplateUrl` który łączy hello podstawowego adresu URL hello znanej nazwy szablonu zasobów udostępnionych hello.</span><span class="sxs-lookup"><span data-stu-id="dcb88-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="dcb88-166">Poniżej tego wiersza, zmienną obiekt złożony jest używane toostore Rozmiar koszulki, który hello podstawowego adresu URL toohello połączonych znane lokalizacji szablonu konfiguracji i przechowywane w hello `vmTemplate` właściwości.</span><span class="sxs-lookup"><span data-stu-id="dcb88-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="dcb88-167">Witaj zaletą tej metody jest zmiana lokalizacji szablonu hello tylko potrzeby toochange hello statyczna zmienna w jednym miejscu, która przechodzi on w całym szablony hello połączone.</span><span class="sxs-lookup"><span data-stu-id="dcb88-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="dcb88-168">Wygenerowany zmiennych</span><span class="sxs-lookup"><span data-stu-id="dcb88-168">Generated variables</span></span>
<span data-ttu-id="dcb88-169">Dodanie toostatic zmienne kilku zmiennych są generowane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="dcb88-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="dcb88-170">W tej sekcji wymieniono niektóre typy typowe hello wygenerowanego zmiennych.</span><span class="sxs-lookup"><span data-stu-id="dcb88-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="dcb88-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="dcb88-171">tshirtSize</span></span>
<span data-ttu-id="dcb88-172">Znasz tej zmiennej wygenerowanych w powyższych przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="dcb88-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="dcb88-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="dcb88-173">networkSettings</span></span>
<span data-ttu-id="dcb88-174">W hello wydajność, możliwości lub szablon rozwiązania zakresami end-to-end, połączone szablony zwykle Utwórz zasoby, które istnieją w sieci.</span><span class="sxs-lookup"><span data-stu-id="dcb88-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="dcb88-175">Jednym z podejść prostego jest toouse ustawień sieciowych toostore obiekt złożony i przekazać je toolinked szablonów.</span><span class="sxs-lookup"><span data-stu-id="dcb88-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="dcb88-176">Przykład komunikacji ustawienia sieciowe są widoczne poniżej.</span><span class="sxs-lookup"><span data-stu-id="dcb88-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="dcb88-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="dcb88-177">availabilitySettings</span></span>
<span data-ttu-id="dcb88-178">Zasoby utworzone w szablonach połączonego często są umieszczane w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="dcb88-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="dcb88-179">W hello poniższy przykład nazwa zbioru dostępności hello określono również hello domeny błędów i toouse liczby domen aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dcb88-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="dcb88-180">Jeśli potrzebujesz wiele zestawów dostępności (na przykład, jeden dla węzłów głównych) i drugi dla węzłów danych, można użyć jako prefiksu nazwy, określ wiele zestawów dostępności lub wykonaj modelu hello przedstawiona wcześniej do utworzenia zmiennej w określonym Rozmiar koszulki.</span><span class="sxs-lookup"><span data-stu-id="dcb88-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="dcb88-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="dcb88-181">storageSettings</span></span>
<span data-ttu-id="dcb88-182">Szczegóły magazynu często są współużytkowane z szablonami połączony.</span><span class="sxs-lookup"><span data-stu-id="dcb88-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="dcb88-183">W poniższym przykładzie hello *storageSettings* obiektu zawiera szczegółowe informacje o hello nazwy konta i kontener magazynu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="dcb88-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="dcb88-184">osSettings</span></span>
<span data-ttu-id="dcb88-185">Z szablonami połączonego toopass systemu operacyjnego ustawienia toovarious węzłów typów może być konieczne w innej konfiguracji znanych typów.</span><span class="sxs-lookup"><span data-stu-id="dcb88-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="dcb88-186">Obiekt złożony jest łatwy sposób toostore i udziału informacje dotyczące systemu operacyjnego i umożliwia łatwiejsze toosupport wiele wyborów systemu operacyjnego dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="dcb88-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="dcb88-187">Witaj poniższy przykład przedstawia dla obiekt *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="dcb88-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="dcb88-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="dcb88-188">machineSettings</span></span>
<span data-ttu-id="dcb88-189">Generowana zmienna, *machineSettings* jest obiekt złożony, zawierające kombinację zmiennych core dla tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dcb88-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="dcb88-190">zmienne Hello obejmują nazwa użytkownika administratora i hasła, prefiks dla nazw maszyn wirtualnych hello i odwołanie do obrazu systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="dcb88-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="dcb88-191">Należy pamiętać, że *osImageReference* pobiera hello wartości z hello *osSettings* zmiennej zdefiniowanej w szablonie głównym hello.</span><span class="sxs-lookup"><span data-stu-id="dcb88-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="dcb88-192">Oznacza to, że można łatwo zmienić hello systemu operacyjnego dla maszyny Wirtualnej — całkowicie lub, w zależności od preferencji powitania klienta szablonu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="dcb88-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="dcb88-193">vmScripts</span></span>
<span data-ttu-id="dcb88-194">Witaj *vmScripts* obiektu zawiera szczegółowe informacje o hello toodownload skrypty i wykonywanie w wystąpieniu maszyny Wirtualnej, w tym odniesienia i wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="dcb88-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="dcb88-195">Poza odwołaniami obejmują hello infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="dcb88-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="dcb88-196">Wewnątrz odwołania zawierać hello zainstalowane oprogramowanie i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dcb88-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="dcb88-197">Użyj hello *scriptsToDownload* właściwości toolist hello skrypty toohello toodownload maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dcb88-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="dcb88-198">Ten obiekt zawiera również argumenty wiersza toocommand odwołania dla różnego rodzaju akcje.</span><span class="sxs-lookup"><span data-stu-id="dcb88-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="dcb88-199">Dostępne są akcje wykonywane hello domyślnej instalacji dla każdego indywidualnego węzła, instalacja wykonywana po wdrożeniu wszystkich węzłów i dodatkowych skryptów, które mogą być określone tooa danego szablonu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="dcb88-200">W tym przykładzie jest używany szablon toodeploy bazy danych MongoDB, co wymaga kryterium toodeliver wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="dcb88-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="dcb88-201">Witaj *arbiterNodeInstallCommand* został dodany za*vmScripts* tooinstall hello kryterium.</span><span class="sxs-lookup"><span data-stu-id="dcb88-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="dcb88-202">sekcja zmienne Hello jest, gdzie znaleźć zmiennych hello, definiujące hello określony tekst tooexecute hello skryptu hello odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="dcb88-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="dcb88-203">Zwraca stan z szablonu</span><span class="sxs-lookup"><span data-stu-id="dcb88-203">Return state from a template</span></span>
<span data-ttu-id="dcb88-204">Nie tylko można przekazywania danych do szablonu, możesz również udostępnianie danych wstecz toohello wywoływania szablonu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="dcb88-205">W hello **generuje** sekcji połączonych szablonu, możesz podać pary klucz wartość, które mogą być używane w szablonie źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="dcb88-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="dcb88-206">Witaj poniższy przykład przedstawia sposób toopass hello generowane w szablonie połączonego prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="dcb88-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="dcb88-207">W szablonie głównym hello można użyć danych z hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="dcb88-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="dcb88-208">Można użyć tego wyrażenia w sekcji danych wyjściowych hello lub sekcja zasobów hello hello głównym szablonu.</span><span class="sxs-lookup"><span data-stu-id="dcb88-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="dcb88-209">Nie można użyć wyrażenia hello w sekcji zmiennych hello, ponieważ zależy od hello stan czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dcb88-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="dcb88-210">tooreturn wartość tego parametru szablonu głównego hello, użyj:</span><span class="sxs-lookup"><span data-stu-id="dcb88-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="dcb88-211">Na przykład za pomocą hello generuje części szablonu połączonego tooreturn dysków z danymi dla maszyny wirtualnej, zobacz [tworzenie wielu dysków danych maszyny wirtualnej](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="dcb88-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="dcb88-212">Zdefiniuj ustawienia uwierzytelniania dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dcb88-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="dcb88-213">Witaj można użyć tego samego wzorca wcześniej ustawień uwierzytelniania hello toospecify ustawienia konfiguracji dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dcb88-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="dcb88-214">Parametr do przekazania do tworzenia hello typu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="dcb88-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="dcb88-215">Należy dodać zmienne dla hello różnymi typami uwierzytelniania i zmiennej toostore, jaki typ jest używany dla tego wdrożenia na podstawie wartości hello hello parametru.</span><span class="sxs-lookup"><span data-stu-id="dcb88-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="dcb88-216">Podczas definiowania hello maszyny wirtualnej, ustaw hello **osProfile** toohello zmiennej został utworzony.</span><span class="sxs-lookup"><span data-stu-id="dcb88-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="dcb88-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dcb88-217">Next steps</span></span>
* <span data-ttu-id="dcb88-218">Zobacz toolearn o hello części szablonu hello [Authoring Azure Resource Manager szablonów](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="dcb88-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="dcb88-219">toosee hello funkcje, które są dostępne w ramach szablonu, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="dcb88-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
