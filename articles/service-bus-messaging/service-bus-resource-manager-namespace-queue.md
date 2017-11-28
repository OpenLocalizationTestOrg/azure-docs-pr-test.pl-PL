---
title: "przestrzeń nazw magistrali usług Azure aaaCreate i kolejki przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Service Bus i kolejki przy użyciu szablonu usługi Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="095bb-103">Tworzenie przestrzeni nazw usługi Service Bus i kolejki przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="095bb-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="095bb-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw usługi Service Bus i kolejką w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="095bb-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="095bb-105">Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="095bb-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="095bb-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="095bb-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="095bb-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="095bb-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="095bb-108">Hello pełną szablonu, zobacz hello [szablonu przestrzeni nazw i kolejki usługi Service Bus] [ Service Bus namespace and queue template] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="095bb-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="095bb-109">Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="095bb-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="095bb-110">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="095bb-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="095bb-111">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="095bb-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="095bb-112">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="095bb-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="095bb-113">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="095bb-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="095bb-114">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="095bb-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="095bb-115">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="095bb-115">What will you deploy?</span></span>

<span data-ttu-id="095bb-116">W przypadku tego szablonu zostanie wdrożona przestrzeni nazw usługi Service Bus z kolejką.</span><span class="sxs-lookup"><span data-stu-id="095bb-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="095bb-117">[Kolejki usługi Service Bus](service-bus-queues-topics-subscriptions.md#queues) oferują pierwszy na wejściu — tooone dostarczania komunikatów pierwszy na wyjściu (FIFO) lub więcej konkurujących konsumentów.</span><span class="sxs-lookup"><span data-stu-id="095bb-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="095bb-118">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="095bb-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="095bb-119">[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="095bb-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="095bb-120">Parametry</span><span class="sxs-lookup"><span data-stu-id="095bb-120">Parameters</span></span>

<span data-ttu-id="095bb-121">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="095bb-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="095bb-122">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="095bb-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="095bb-123">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="095bb-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="095bb-124">Definiuje parametry dla wartości, które będą zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="095bb-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="095bb-125">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="095bb-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="095bb-126">Szablon Hello definiuje hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="095bb-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="095bb-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="095bb-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="095bb-128">Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="095bb-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="095bb-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="095bb-129">serviceBusQueueName</span></span>
<span data-ttu-id="095bb-130">Nazwa Hello kolejki hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="095bb-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="095bb-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="095bb-131">serviceBusApiVersion</span></span>
<span data-ttu-id="095bb-132">wersja interfejsu API usługi Service Bus Hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="095bb-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="095bb-133">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="095bb-133">Resources toodeploy</span></span>
<span data-ttu-id="095bb-134">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**, z kolejką.</span><span class="sxs-lookup"><span data-stu-id="095bb-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="095bb-135">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="095bb-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="095bb-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="095bb-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="095bb-137">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="095bb-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="095bb-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="095bb-138">Next steps</span></span>
<span data-ttu-id="095bb-139">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="095bb-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="095bb-140">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="095bb-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="095bb-141">Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="095bb-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
