---
title: "Przegląd dostawcy zasobów aaaNetwork | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello nowego dostawcy zasobów sieciowych w systemie Azure Resource Manager"
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
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="d90df-103">Dostawca zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="d90df-103">Network Resource Provider</span></span>
<span data-ttu-id="d90df-104">Podstawa w bieżącej sukcesu firmy, jest hello toobuild możliwości zarządzania aplikacjami pamiętać sieci dużą skalę w sposób agile, elastyczne, bezpieczne i repeatable.</span><span class="sxs-lookup"><span data-stu-id="d90df-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="d90df-105">Usługa Azure Resource Manager umożliwia toocreate można takich aplikacji, jako pojedynczą kolekcję zasobów w grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="d90df-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="d90df-106">Takie zasoby są zarządzane przez różnych dostawców zasobów w obszarze usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d90df-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="d90df-107">Usługa Azure Resource Manager zależy od zasobu różnych dostawców tooprovide dostęp do tooyour zasobów.</span><span class="sxs-lookup"><span data-stu-id="d90df-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="d90df-108">Istnieją trzy dostawców zasobów głównego: sieci, magazynu i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d90df-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="d90df-109">W tym dokumencie omówiono hello właściwości i zalet hello dostawcy zasobów sieciowych, w tym:</span><span class="sxs-lookup"><span data-stu-id="d90df-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="d90df-110">**Metadane** — można dodać tooresources informacji przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="d90df-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="d90df-111">Znaczniki mogą być używane tootrack wykorzystania zasobów między grupami zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="d90df-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="d90df-112">**Większą kontrolę nad siecią** — są luźno powiązane z zasobów sieciowych i sterować nimi w sposób bardziej szczegółowego.</span><span class="sxs-lookup"><span data-stu-id="d90df-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="d90df-113">Oznacza to, że masz większą elastyczność w zarządzaniu hello zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="d90df-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="d90df-114">**Szybsze konfiguracji** — ponieważ są luźno powiązane z zasobów sieciowych, można tworzyć i organizowania zasobów sieciowych równolegle.</span><span class="sxs-lookup"><span data-stu-id="d90df-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="d90df-115">Ma to znaczne zmniejszoną ilość czasu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d90df-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="d90df-116">**Kontroli dostępu opartej na rolach** -RBAC zawiera domyślne role, z określonego zakresu zabezpieczeń, w przypadku tworzenia hello tooallowing dodanie ról niestandardowych do bezpiecznego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d90df-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="d90df-117">**Łatwiejsze zarządzanie i wdrażanie** — jest łatwiejsze toodeploy i zarządzania aplikacjami, ponieważ można całego stosu aplikacji można utworzyć jako pojedynczą kolekcję zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d90df-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="d90df-118">I szybsze toodeploy, ponieważ po prostu zapewniając ładunek JSON szablonu można wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="d90df-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="d90df-119">**Dostosowywanie szybkie** — można użyć szablonów deklaratywne stylu tooenable powtarzalnych i szybkiego dostosowywania wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="d90df-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="d90df-120">**Dostosowywanie powtarzalne** — można użyć szablonów deklaratywne stylu tooenable powtarzalnych i szybkiego dostosowywania wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="d90df-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="d90df-121">**Interfejsy zarządzania** — można użyć dowolnego z następujących interfejsów toomanage hello zasobów:</span><span class="sxs-lookup"><span data-stu-id="d90df-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="d90df-122">REST API oparty na</span><span class="sxs-lookup"><span data-stu-id="d90df-122">REST based API</span></span>
  * <span data-ttu-id="d90df-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d90df-123">PowerShell</span></span>
  * <span data-ttu-id="d90df-124">Zestaw SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d90df-124">.NET SDK</span></span>
  * <span data-ttu-id="d90df-125">Zestaw Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="d90df-125">Node.JS SDK</span></span>
  * <span data-ttu-id="d90df-126">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="d90df-126">Java SDK</span></span>
  * <span data-ttu-id="d90df-127">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d90df-127">Azure CLI</span></span>
  * <span data-ttu-id="d90df-128">Portal w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="d90df-128">Preview Portal</span></span>
  * <span data-ttu-id="d90df-129">Język szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d90df-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="d90df-130">Zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="d90df-130">Network resources</span></span>
<span data-ttu-id="d90df-131">Możesz teraz zarządzać zasobów sieciowych niezależnie, zamiast je zarządzanych za pomocą obliczeń jednego zasobu (maszyny wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="d90df-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="d90df-132">Dzięki temu wyższego poziomu bezpieczeństwa i elastyczność oraz elastyczność w tworzenie infrastruktury złożone i dużej skali, w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d90df-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="d90df-133">Widok koncepcyjny Przykładowe wdrożenie obejmujące wielowarstwowych aplikacji znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="d90df-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="d90df-134">Każdy zasób, który zostanie wyświetlony, takie jak karty sieciowe, publicznych adresów IP i maszyn wirtualnych, można zarządzać niezależnie.</span><span class="sxs-lookup"><span data-stu-id="d90df-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Model zasobów sieciowych](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="d90df-136">Każdy zasób zawiera zbiór wspólnych właściwości i ich indywidualnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="d90df-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="d90df-137">wspólne właściwości Hello są:</span><span class="sxs-lookup"><span data-stu-id="d90df-137">hello common properties are:</span></span>

| <span data-ttu-id="d90df-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d90df-138">Property</span></span> | <span data-ttu-id="d90df-139">Opis</span><span class="sxs-lookup"><span data-stu-id="d90df-139">Description</span></span> | <span data-ttu-id="d90df-140">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="d90df-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d90df-141">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="d90df-141">**name**</span></span> |<span data-ttu-id="d90df-142">Nazwa zasobu unikatowy.</span><span class="sxs-lookup"><span data-stu-id="d90df-142">Unique resource name.</span></span> <span data-ttu-id="d90df-143">Każdy typ zasobu ma własną ograniczenia nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="d90df-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="d90df-144">NIC01 PIP01, VM01,</span><span class="sxs-lookup"><span data-stu-id="d90df-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="d90df-145">**location**</span><span class="sxs-lookup"><span data-stu-id="d90df-145">**location**</span></span> |<span data-ttu-id="d90df-146">Region platformy Azure, w których hello zasób znajduje się</span><span class="sxs-lookup"><span data-stu-id="d90df-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="d90df-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="d90df-147">westus, eastus</span></span> |
| <span data-ttu-id="d90df-148">**Identyfikator**</span><span class="sxs-lookup"><span data-stu-id="d90df-148">**id**</span></span> |<span data-ttu-id="d90df-149">Unikatowy identyfikator URI na podstawie</span><span class="sxs-lookup"><span data-stu-id="d90df-149">Unique URI based identification</span></span> |<span data-ttu-id="d90df-150">/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="d90df-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="d90df-151">Możesz sprawdzić hello poszczególnych właściwości zasobów w poniższych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="d90df-151">You can check hello individual properties of resources in hello sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="d90df-152">Interfejsy zarządzania</span><span class="sxs-lookup"><span data-stu-id="d90df-152">Management interfaces</span></span>
<span data-ttu-id="d90df-153">Możesz zarządzać zasobami sieci Azure przy użyciu różnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="d90df-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="d90df-154">W tym dokumencie firma Microsoft będzie skupić się na tow te interfejsy: interfejs API REST i szablony.</span><span class="sxs-lookup"><span data-stu-id="d90df-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="d90df-155">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d90df-155">REST API</span></span>
<span data-ttu-id="d90df-156">Jak wspomniano wcześniej, można zarządzać za pośrednictwem różnych interfejsy, w tym interfejsu API REST, zestawu SDK programu .NET, Node.JS SDK, zestaw SDK Java, programu PowerShell, interfejsu wiersza polecenia, portalu Azure i szablony zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="d90df-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="d90df-157">Witaj interfejsu API Rest jest zgodna z toohello Specyfikacja protokołu HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="d90df-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="d90df-158">Hello ogólną strukturę URI hello interfejsu API jest przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="d90df-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="d90df-159">I reprezentują parametry hello w nawiasach klamrowych hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d90df-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="d90df-160">**Identyfikator subskrypcji** — identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d90df-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="d90df-161">**przestrzeń nazw dostawcy zasobów** — przestrzeń nazw dla dostawca hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="d90df-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="d90df-162">wartość Hello dostawcy zasobów sieciowych hello jest *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="d90df-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="d90df-163">**Nazwa regionu** — nazwa regionu Azure hello</span><span class="sxs-lookup"><span data-stu-id="d90df-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="d90df-164">Witaj następujących metod HTTP obsługiwanych podczas wprowadzania toohello wywołania interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="d90df-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="d90df-165">**Umieść** — używane toocreate zasobów danego typu, modyfikować właściwości zasobu lub zmień skojarzenia między zasobami.</span><span class="sxs-lookup"><span data-stu-id="d90df-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="d90df-166">**Pobierz** — używane informacje tooretrieve elastycznie zasobu.</span><span class="sxs-lookup"><span data-stu-id="d90df-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="d90df-167">**Usuń** — używane toodelete istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d90df-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="d90df-168">Zarówno hello żądania i odpowiedzi jest zgodna z format ładunku JSON tooa.</span><span class="sxs-lookup"><span data-stu-id="d90df-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="d90df-169">Aby uzyskać więcej informacji, zobacz [interfejsów API usługi Azure Resource Management](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="d90df-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="d90df-170">Język szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d90df-170">Resource Manager template language</span></span>
<span data-ttu-id="d90df-171">Dodanie toomanaging zasobów imperatively (za pośrednictwem interfejsów API lub zestawu SDK) można również użyć deklaratywne programowania toobuild styl i zarządzania zasobami sieci przy użyciu hello język szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d90df-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="d90df-172">Poniższe przykładowe reprezentację szablonu —</span><span class="sxs-lookup"><span data-stu-id="d90df-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="d90df-173">Szablon Hello jest głównie opisu JSON zasobów hello i wartości wystąpienia hello wprowadzonym za pomocą parametrów.</span><span class="sxs-lookup"><span data-stu-id="d90df-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="d90df-174">w poniższym przykładzie Hello mogą być używane toocreate sieć wirtualną przy użyciu podsieci 2.</span><span class="sxs-lookup"><span data-stu-id="d90df-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="d90df-175">Masz hello opcja podania wartości parametrów hello ręcznie, przy użyciu szablonu, lub można użyć pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="d90df-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="d90df-176">Witaj w poniższym przykładzie przedstawiono możliwe zestaw używany z szablonem hello powyżej toobe wartości parametru:</span><span class="sxs-lookup"><span data-stu-id="d90df-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

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


<span data-ttu-id="d90df-177">główne zalety Hello za pomocą szablonów są następujące:</span><span class="sxs-lookup"><span data-stu-id="d90df-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="d90df-178">Można tworzyć złożone infrastruktury w grupie zasobów w stylu deklaratywne.</span><span class="sxs-lookup"><span data-stu-id="d90df-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="d90df-179">Witaj aranżacji tworzenia zasobów hello, w tym zarządzania zależności jest obsługiwany przez Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="d90df-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="d90df-180">Witaj infrastruktury można tworzyć w sposób powtarzalny w różnych regionach i w obrębie regionu, zmieniając po prostu parametrów.</span><span class="sxs-lookup"><span data-stu-id="d90df-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="d90df-181">Styl deklaratywne Hello prowadzi tooshorter czas realizacji w tworzeniu szablonów hello i wdrażania infrastruktury hello.</span><span class="sxs-lookup"><span data-stu-id="d90df-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="d90df-182">Przykładowe szablonów, zobacz [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d90df-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="d90df-183">Aby uzyskać więcej informacji na powitania język szablonu usługi Resource Manager, zobacz [język szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d90df-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d90df-184">Przykładowy szablon Hello powyżej używa hello sieci wirtualnej i zasoby podsieci.</span><span class="sxs-lookup"><span data-stu-id="d90df-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="d90df-185">Brak innych zasobów sieciowych, których można używać wymienione poniżej:</span><span class="sxs-lookup"><span data-stu-id="d90df-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="d90df-186">Przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="d90df-186">Using a template</span></span>
<span data-ttu-id="d90df-187">TooAzure usługi z szablonu można wdrożyć przy użyciu programu PowerShell, AzureCLI, lub wykonując toodeploy kliknij pozycję z witryny GitHub.</span><span class="sxs-lookup"><span data-stu-id="d90df-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="d90df-188">toodeploy usługi z szablonu w witrynie GitHub, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d90df-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="d90df-189">Otwórz plik template3 hello z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d90df-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="d90df-190">Na przykład otwórz [sieci wirtualnej z dwoma podsieciami](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="d90df-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="d90df-191">Polecenie **wdrażanie tooAzure**, a następnie zaloguj się na toohello portalu Azure przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d90df-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="d90df-192">Sprawdź hello szablonu, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d90df-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="d90df-193">Kliknij przycisk **Edytuj parametry** i wybierz lokalizację, takich jak *zachodnie stany USA*, hello sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="d90df-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="d90df-194">W razie potrzeby zmień hello **prefiks adresu** i **SUBNETPREFIX** parametry, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d90df-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="d90df-195">Kliknij przycisk **wybierz grupę zasobów** a następnie kliknij polecenie hello grupa zasobów ma tooadd hello w sieci wirtualnej i podsieci z.</span><span class="sxs-lookup"><span data-stu-id="d90df-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="d90df-196">Alternatywnie można utworzyć nową grupę zasobów, klikając **lub utworzyć nowy**.</span><span class="sxs-lookup"><span data-stu-id="d90df-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="d90df-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d90df-197">Click **Create**.</span></span> <span data-ttu-id="d90df-198">Zwróć uwagę, hello wyświetlanie kafelka **wdrażania szablonu inicjowania obsługi administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="d90df-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="d90df-199">Po ukończeniu wdrażania hello, zobaczysz ekran podobny tooone poniżej.</span><span class="sxs-lookup"><span data-stu-id="d90df-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Przykładowe wdrożenie szablonu](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="d90df-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d90df-201">Next steps</span></span>
[<span data-ttu-id="d90df-202">Język szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d90df-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="d90df-203">Sieć platformy Azure — często używane szablony</span><span class="sxs-lookup"><span data-stu-id="d90df-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="d90df-204">Usługa Azure Resource Manager, a wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="d90df-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="d90df-205">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d90df-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

