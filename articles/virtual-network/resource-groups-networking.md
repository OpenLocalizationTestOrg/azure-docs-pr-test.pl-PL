---
title: "Omówienie dostawcy zasobów sieci | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat nowego dostawcy zasobów sieciowych w systemie Azure Resource Manager"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="a8e34-103">Dostawca zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="a8e34-103">Network Resource Provider</span></span>
<span data-ttu-id="a8e34-104">Podstawa w bieżącej sukcesu firmy, jest możliwość tworzenia i zarządzania aplikacjami pamiętać sieci dużą skalę w sposób agile, elastyczne, bezpieczne i repeatable.</span><span class="sxs-lookup"><span data-stu-id="a8e34-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="a8e34-105">Usługa Azure Resource Manager umożliwia tworzenie takich aplikacji, jako pojedynczą kolekcję zasobów w grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="a8e34-106">Takie zasoby są zarządzane przez różnych dostawców zasobów w obszarze usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8e34-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="a8e34-107">Usługa Azure Resource Manager zależy od dostawców zasobów różnych w celu zapewnienia dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="a8e34-108">Istnieją trzy dostawców zasobów głównego: sieci, magazynu i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="a8e34-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="a8e34-109">W tym dokumencie omówiono charakterystyki i korzyści wynikające z dostawcy zasobów sieciowych, w tym:</span><span class="sxs-lookup"><span data-stu-id="a8e34-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="a8e34-110">**Metadane** — informacje można dodać do zasobów przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="a8e34-111">Znaczniki mogą służyć do śledzenia wykorzystania zasobów między grupami zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="a8e34-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="a8e34-112">**Większą kontrolę nad siecią** — są luźno powiązane z zasobów sieciowych i sterować nimi w sposób bardziej szczegółowego.</span><span class="sxs-lookup"><span data-stu-id="a8e34-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="a8e34-113">Oznacza to, że masz większą elastyczność w zarządzaniu zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="a8e34-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="a8e34-114">**Szybsze konfiguracji** — ponieważ są luźno powiązane z zasobów sieciowych, można tworzyć i organizowania zasobów sieciowych równolegle.</span><span class="sxs-lookup"><span data-stu-id="a8e34-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="a8e34-115">Ma to znaczne zmniejszoną ilość czasu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a8e34-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="a8e34-116">**Kontroli dostępu opartej na rolach** -RBAC zawiera domyślne role, z określonego zakresu zabezpieczeń, oprócz umożliwienia Tworzenie niestandardowych ról dla bezpiecznego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a8e34-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="a8e34-117">**Łatwiejsze zarządzanie i wdrażanie** — ułatwia wdrażanie i zarządzanie aplikacjami, ponieważ można całego stosu aplikacji można utworzyć jako pojedynczą kolekcję zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="a8e34-118">I szybsze do wdrożenia, ponieważ po prostu zapewniając ładunek JSON szablonu można wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="a8e34-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="a8e34-119">**Dostosowywanie szybkie** — szablony deklaratywne stylu można użyć do włączenia powtarzalnych i szybkiego dostosowywania wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="a8e34-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="a8e34-120">**Dostosowywanie powtarzalne** — szablony deklaratywne stylu można użyć do włączenia powtarzalnych i szybkiego dostosowywania wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="a8e34-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="a8e34-121">**Interfejsy zarządzania** — można użyć dowolnego z poniższych interfejsów do zarządzania zasobami:</span><span class="sxs-lookup"><span data-stu-id="a8e34-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="a8e34-122">REST API oparty na</span><span class="sxs-lookup"><span data-stu-id="a8e34-122">REST based API</span></span>
  * <span data-ttu-id="a8e34-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8e34-123">PowerShell</span></span>
  * <span data-ttu-id="a8e34-124">Zestaw SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a8e34-124">.NET SDK</span></span>
  * <span data-ttu-id="a8e34-125">Zestaw Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="a8e34-125">Node.JS SDK</span></span>
  * <span data-ttu-id="a8e34-126">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="a8e34-126">Java SDK</span></span>
  * <span data-ttu-id="a8e34-127">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a8e34-127">Azure CLI</span></span>
  * <span data-ttu-id="a8e34-128">Portal w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="a8e34-128">Preview Portal</span></span>
  * <span data-ttu-id="a8e34-129">Język szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e34-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="a8e34-130">Zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="a8e34-130">Network resources</span></span>
<span data-ttu-id="a8e34-131">Możesz teraz zarządzać zasobów sieciowych niezależnie, zamiast je zarządzanych za pomocą obliczeń jednego zasobu (maszyny wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="a8e34-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="a8e34-132">Dzięki temu wyższego poziomu bezpieczeństwa i elastyczność oraz elastyczność w tworzenie infrastruktury złożone i dużej skali, w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="a8e34-133">Widok koncepcyjny Przykładowe wdrożenie obejmujące wielowarstwowych aplikacji znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="a8e34-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="a8e34-134">Każdy zasób, który zostanie wyświetlony, takie jak karty sieciowe, publicznych adresów IP i maszyn wirtualnych, można zarządzać niezależnie.</span><span class="sxs-lookup"><span data-stu-id="a8e34-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Model zasobów sieciowych](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="a8e34-136">Każdy zasób zawiera zbiór wspólnych właściwości i ich indywidualnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="a8e34-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="a8e34-137">Wspólne właściwości są:</span><span class="sxs-lookup"><span data-stu-id="a8e34-137">The common properties are:</span></span>

| <span data-ttu-id="a8e34-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a8e34-138">Property</span></span> | <span data-ttu-id="a8e34-139">Opis</span><span class="sxs-lookup"><span data-stu-id="a8e34-139">Description</span></span> | <span data-ttu-id="a8e34-140">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="a8e34-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8e34-141">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="a8e34-141">**name**</span></span> |<span data-ttu-id="a8e34-142">Nazwa zasobu unikatowy.</span><span class="sxs-lookup"><span data-stu-id="a8e34-142">Unique resource name.</span></span> <span data-ttu-id="a8e34-143">Każdy typ zasobu ma własną ograniczenia nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="a8e34-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="a8e34-144">NIC01 PIP01, VM01,</span><span class="sxs-lookup"><span data-stu-id="a8e34-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="a8e34-145">**location**</span><span class="sxs-lookup"><span data-stu-id="a8e34-145">**location**</span></span> |<span data-ttu-id="a8e34-146">Region platformy Azure, w której znajduje się zasób</span><span class="sxs-lookup"><span data-stu-id="a8e34-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="a8e34-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="a8e34-147">westus, eastus</span></span> |
| <span data-ttu-id="a8e34-148">**Identyfikator**</span><span class="sxs-lookup"><span data-stu-id="a8e34-148">**id**</span></span> |<span data-ttu-id="a8e34-149">Unikatowy identyfikator URI na podstawie</span><span class="sxs-lookup"><span data-stu-id="a8e34-149">Unique URI based identification</span></span> |<span data-ttu-id="a8e34-150">/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="a8e34-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="a8e34-151">Możesz sprawdzić poszczególnych właściwości zasobów w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="a8e34-151">You can check the individual properties of resources in the sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="a8e34-152">Interfejsy zarządzania</span><span class="sxs-lookup"><span data-stu-id="a8e34-152">Management interfaces</span></span>
<span data-ttu-id="a8e34-153">Możesz zarządzać zasobami sieci Azure przy użyciu różnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="a8e34-154">W tym dokumencie firma Microsoft będzie skupić się na tow te interfejsy: interfejs API REST i szablony.</span><span class="sxs-lookup"><span data-stu-id="a8e34-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="a8e34-155">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a8e34-155">REST API</span></span>
<span data-ttu-id="a8e34-156">Jak wspomniano wcześniej, można zarządzać za pośrednictwem różnych interfejsy, w tym interfejsu API REST, zestawu SDK programu .NET, Node.JS SDK, zestaw SDK Java, programu PowerShell, interfejsu wiersza polecenia, portalu Azure i szablony zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="a8e34-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="a8e34-157">Interfejs API Rest jest zgodny ze specyfikacją protokołu HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="a8e34-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="a8e34-158">Identyfikator URI ogólną strukturę interfejsu API znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="a8e34-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="a8e34-159">I parametrów w nawiasach klamrowych reprezentują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a8e34-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="a8e34-160">**Identyfikator subskrypcji** — identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e34-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="a8e34-161">**przestrzeń nazw dostawcy zasobów** — przestrzeń nazw dla używanego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="a8e34-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="a8e34-162">Wartość dostawcy zasobów sieciowych jest *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="a8e34-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="a8e34-163">**Nazwa regionu** — nazwa regionu Azure</span><span class="sxs-lookup"><span data-stu-id="a8e34-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="a8e34-164">W wywołaniach interfejsu API REST, obsługiwane są następujące metody HTTP:</span><span class="sxs-lookup"><span data-stu-id="a8e34-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="a8e34-165">**Umieść** — umożliwia tworzenie zasobu danego typu, modyfikować właściwości zasobu lub zmiana skojarzenia między zasobami.</span><span class="sxs-lookup"><span data-stu-id="a8e34-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="a8e34-166">**Pobierz** — używane do pobierania informacji o elastycznie zasobu.</span><span class="sxs-lookup"><span data-stu-id="a8e34-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="a8e34-167">**Usuń** — używane do usuwania istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a8e34-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="a8e34-168">Żądanie i odpowiedź jest zgodna z formatem ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="a8e34-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="a8e34-169">Aby uzyskać więcej informacji, zobacz [interfejsów API usługi Azure Resource Management](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8e34-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="a8e34-170">Język szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e34-170">Resource Manager template language</span></span>
<span data-ttu-id="a8e34-171">Oprócz zarządzania zasobami imperatively (za pośrednictwem interfejsów API lub zestawu SDK), można również używać deklaratywne stylu programowania do tworzenia i zarządzania zasobami sieci przy użyciu języka szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8e34-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="a8e34-172">Poniższe przykładowe reprezentację szablonu —</span><span class="sxs-lookup"><span data-stu-id="a8e34-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="a8e34-173">Szablon jest głównie opisu JSON zasobów i wartości wystąpienia wprowadzonym za pomocą parametrów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="a8e34-174">W poniższym przykładzie może służyć do tworzenia sieci wirtualnej 2 podsieci.</span><span class="sxs-lookup"><span data-stu-id="a8e34-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="a8e34-175">Masz ręcznie podać wartości parametrów przy użyciu szablonu, lub można użyć pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="a8e34-176">W poniższym przykładzie pokazano zestaw możliwych wartości parametrów do użycia na podstawie tego szablonu:</span><span class="sxs-lookup"><span data-stu-id="a8e34-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="a8e34-177">Główne zalety za pomocą szablonów są następujące:</span><span class="sxs-lookup"><span data-stu-id="a8e34-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="a8e34-178">Można tworzyć złożone infrastruktury w grupie zasobów w stylu deklaratywne.</span><span class="sxs-lookup"><span data-stu-id="a8e34-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="a8e34-179">Orchestration tworzenia zasobów, w tym zarządzanie zależności jest obsługiwany przez Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="a8e34-180">Infrastruktura można tworzyć w sposób powtarzalny w różnych regionach i w obrębie regionu, zmieniając po prostu parametrów.</span><span class="sxs-lookup"><span data-stu-id="a8e34-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="a8e34-181">Styl deklaratywne prowadzi do krótszy czas realizacji w tworzeniu szablonów i wdrażania infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="a8e34-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="a8e34-182">Przykładowe szablonów, zobacz [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a8e34-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="a8e34-183">Aby uzyskać więcej informacji o języku szablonu usługi Resource Manager, zobacz [język szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a8e34-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a8e34-184">Przykładowy szablon powyżej korzysta z sieci wirtualnej i zasoby podsieci.</span><span class="sxs-lookup"><span data-stu-id="a8e34-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="a8e34-185">Brak innych zasobów sieciowych, których można używać wymienione poniżej:</span><span class="sxs-lookup"><span data-stu-id="a8e34-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="a8e34-186">Przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="a8e34-186">Using a template</span></span>
<span data-ttu-id="a8e34-187">Można wdrożyć usługi Azure z szablonu, za pomocą programu PowerShell, AzureCLI, lub wykonując kliknij, aby wdrożyć z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8e34-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="a8e34-188">Do wdrożenia usług z szablonu w usłudze GitHub, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8e34-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="a8e34-189">Otwórz plik template3 z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8e34-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="a8e34-190">Na przykład otwórz [sieci wirtualnej z dwoma podsieciami](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="a8e34-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="a8e34-191">Polecenie **wdrażanie na platformie Azure**, a następnie zaloguj się portalu Azure przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a8e34-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="a8e34-192">Sprawdź szablon, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a8e34-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="a8e34-193">Kliknij przycisk **Edytuj parametry** i wybierz lokalizację, takich jak *zachodnie stany USA*dla sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="a8e34-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="a8e34-194">W razie potrzeby zmień **prefiks adresu** i **SUBNETPREFIX** parametry, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8e34-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="a8e34-195">Kliknij przycisk **wybierz grupę zasobów** a następnie kliknij polecenie grupy zasobów, aby dodać sieć wirtualną i podsieci z.</span><span class="sxs-lookup"><span data-stu-id="a8e34-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="a8e34-196">Alternatywnie można utworzyć nową grupę zasobów, klikając **lub utworzyć nowy**.</span><span class="sxs-lookup"><span data-stu-id="a8e34-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="a8e34-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a8e34-197">Click **Create**.</span></span> <span data-ttu-id="a8e34-198">Zwróć uwagę, wyświetlanie kafelka **wdrażania szablonu inicjowania obsługi administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="a8e34-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="a8e34-199">Po zakończeniu wdrożenia zostanie wyświetlony ekran podobny do poniżej.</span><span class="sxs-lookup"><span data-stu-id="a8e34-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![Przykładowe wdrożenie szablonu](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="a8e34-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8e34-201">Next steps</span></span>
[<span data-ttu-id="a8e34-202">Język szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e34-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="a8e34-203">Sieć platformy Azure — często używane szablony</span><span class="sxs-lookup"><span data-stu-id="a8e34-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="a8e34-204">Usługa Azure Resource Manager, a wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="a8e34-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="a8e34-205">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e34-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

