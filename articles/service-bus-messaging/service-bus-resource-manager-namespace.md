---
title: "Tworzenie przestrzeni nazw usługi Service Bus przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Szablon usługi Azure Resource Manager umożliwia tworzenie przestrzeni nazw usługi Service Bus"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="d8732-103">Tworzenie przestrzeni nazw usługi Service Bus przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8732-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="d8732-104">W tym artykule opisano, jak szablon Menedżera zasobów Azure, która tworzy przestrzeń nazw magistrali usług typu **wiadomości** z wersji Standard/Basic.</span><span class="sxs-lookup"><span data-stu-id="d8732-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="d8732-105">Artykuł również definiuje parametry, które są określone, aby wykonać wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="d8732-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="d8732-106">Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d8732-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d8732-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="d8732-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="d8732-108">Zakończenie szablonu, zobacz [szablonu przestrzeni nazw usługi Service Bus] [ Service Bus namespace template] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8732-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="d8732-109">Następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d8732-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="d8732-110">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="d8732-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="d8732-111">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d8732-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="d8732-112">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="d8732-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="d8732-113">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="d8732-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="d8732-114">Aby sprawdzić najnowsze szablony, odwiedź stronę [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukiwania dla usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d8732-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="d8732-115">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="d8732-115">What will you deploy?</span></span>
<span data-ttu-id="d8732-116">W przypadku tego szablonu wdroży przestrzeni nazw usługi Service Bus z [podstawowa, standardowa lub Premium](https://azure.microsoft.com/pricing/details/service-bus/) jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="d8732-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="d8732-117">Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:</span><span class="sxs-lookup"><span data-stu-id="d8732-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="d8732-118">[![Wdrażanie na platformie Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d8732-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d8732-119">Parametry</span><span class="sxs-lookup"><span data-stu-id="d8732-119">Parameters</span></span>
<span data-ttu-id="d8732-120">Przy użyciu usługi Azure Resource Manager można zdefiniować parametry dla wartości, które mają zostać uwzględnione podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="d8732-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="d8732-121">Szablon zawiera sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="d8732-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="d8732-122">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie projektu, który jest wdrażany lub opartych na środowisku, które wdrażasz.</span><span class="sxs-lookup"><span data-stu-id="d8732-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="d8732-123">Definiuje parametry dla wartości, które będą zawsze taki sam.</span><span class="sxs-lookup"><span data-stu-id="d8732-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="d8732-124">Każda wartość parametru używana w szablonie definiuje wdrażane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d8732-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="d8732-125">Ten szablon definiuje następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="d8732-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="d8732-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="d8732-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="d8732-127">Nazwa przestrzeni nazw usługi Service Bus do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="d8732-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="d8732-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="d8732-128">serviceBusSKU</span></span>
<span data-ttu-id="d8732-129">Nazwa usługi Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="d8732-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="d8732-130">Szablon definiuje wartości, które są dozwolone dla tego parametru (podstawowa, standardowa lub Premium) i przypisuje wartość domyślną (Standard), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="d8732-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="d8732-131">Aby uzyskać więcej informacji na temat cen usługi Service Bus, zobacz [usługi Service Bus cennik i rozliczenia][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="d8732-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="d8732-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="d8732-132">serviceBusApiVersion</span></span>
<span data-ttu-id="d8732-133">Wersja interfejsu API usługi Service Bus szablonu.</span><span class="sxs-lookup"><span data-stu-id="d8732-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="d8732-134">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d8732-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="d8732-135">Przestrzeń nazw magistrali usług</span><span class="sxs-lookup"><span data-stu-id="d8732-135">Service Bus namespace</span></span>
<span data-ttu-id="d8732-136">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**.</span><span class="sxs-lookup"><span data-stu-id="d8732-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="d8732-137">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d8732-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d8732-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8732-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="d8732-139">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8732-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="d8732-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8732-140">Next steps</span></span>
<span data-ttu-id="d8732-141">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak nimi zarządzać przeczytaj następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="d8732-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="d8732-142">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8732-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="d8732-143">Zarządzanie zasobami usługi Service Bus za pomocą Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="d8732-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
