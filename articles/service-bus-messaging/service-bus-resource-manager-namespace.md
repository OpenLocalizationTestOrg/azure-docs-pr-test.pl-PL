---
title: "przestrzeń nazw magistrali usług aaaCreate przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Użyj toocreate szablonu usługi Azure Resource Manager przestrzeni nazw usługi Service Bus"
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
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="0b31a-103">Tworzenie przestrzeni nazw usługi Service Bus przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b31a-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="0b31a-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager, który tworzy przestrzeń nazw magistrali usług typu **wiadomości** z wersji Standard/Basic.</span><span class="sxs-lookup"><span data-stu-id="0b31a-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="0b31a-105">Artykuł Hello określa również hello parametrów, które są określone dla wykonywania hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b31a-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="0b31a-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="0b31a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="0b31a-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="0b31a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="0b31a-108">Hello pełną szablonu, zobacz hello [szablonu przestrzeni nazw usługi Service Bus] [ Service Bus namespace template] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b31a-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="0b31a-109">Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b31a-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="0b31a-110">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="0b31a-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="0b31a-111">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0b31a-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="0b31a-112">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="0b31a-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="0b31a-113">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="0b31a-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="0b31a-114">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukiwania dla usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0b31a-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="0b31a-115">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="0b31a-115">What will you deploy?</span></span>
<span data-ttu-id="0b31a-116">W przypadku tego szablonu wdroży przestrzeni nazw usługi Service Bus z [podstawowa, standardowa lub Premium](https://azure.microsoft.com/pricing/details/service-bus/) jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="0b31a-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="0b31a-117">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="0b31a-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="0b31a-118">[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0b31a-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="0b31a-119">Parametry</span><span class="sxs-lookup"><span data-stu-id="0b31a-119">Parameters</span></span>
<span data-ttu-id="0b31a-120">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="0b31a-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="0b31a-121">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="0b31a-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="0b31a-122">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="0b31a-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="0b31a-123">Definiuje parametry dla wartości, które będą zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="0b31a-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="0b31a-124">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0b31a-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="0b31a-125">Ten szablon definiuje hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="0b31a-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="0b31a-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="0b31a-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="0b31a-127">Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="0b31a-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="0b31a-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="0b31a-128">serviceBusSKU</span></span>
<span data-ttu-id="0b31a-129">Nazwa Hello hello usługi Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="0b31a-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

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
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="0b31a-130">Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (podstawowa, standardowa lub Premium) i przypisuje wartość domyślną (Standard), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="0b31a-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="0b31a-131">Aby uzyskać więcej informacji na temat cen usługi Service Bus, zobacz [usługi Service Bus cennik i rozliczenia][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="0b31a-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="0b31a-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="0b31a-132">serviceBusApiVersion</span></span>
<span data-ttu-id="0b31a-133">wersja interfejsu API usługi Service Bus Hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="0b31a-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="0b31a-134">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="0b31a-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="0b31a-135">Przestrzeń nazw magistrali usług</span><span class="sxs-lookup"><span data-stu-id="0b31a-135">Service Bus namespace</span></span>
<span data-ttu-id="0b31a-136">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**.</span><span class="sxs-lookup"><span data-stu-id="0b31a-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="0b31a-137">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="0b31a-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="0b31a-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b31a-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="0b31a-139">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0b31a-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="0b31a-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b31a-140">Next steps</span></span>
<span data-ttu-id="0b31a-141">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeczytaj następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0b31a-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="0b31a-142">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b31a-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="0b31a-143">Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="0b31a-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
