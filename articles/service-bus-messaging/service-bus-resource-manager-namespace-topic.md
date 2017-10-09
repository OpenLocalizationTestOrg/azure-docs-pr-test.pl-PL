---
title: "aaaCreate Azure Service Bus przestrzeni nazw subskrypcję tematu przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji przy użyciu szablonu Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="c03fc-103">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c03fc-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="c03fc-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw usługi Service Bus i tematu i subskrypcji w ramach tego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="c03fc-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="c03fc-105">Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="c03fc-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="c03fc-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań</span><span class="sxs-lookup"><span data-stu-id="c03fc-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="c03fc-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="c03fc-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c03fc-108">Hello pełną szablonu, zobacz hello [przestrzeni nazw usługi Service Bus z tematów i subskrypcji] [ Service Bus namespace with topic and subscription] szablonu.</span><span class="sxs-lookup"><span data-stu-id="c03fc-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="c03fc-109">Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c03fc-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="c03fc-110">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="c03fc-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="c03fc-111">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="c03fc-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="c03fc-112">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="c03fc-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c03fc-113">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="c03fc-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="c03fc-114">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="c03fc-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c03fc-115">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="c03fc-115">What will you deploy?</span></span>

<span data-ttu-id="c03fc-116">W przypadku tego szablonu zostanie wdrożona przestrzeni nazw usługi Service Bus z tematów i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c03fc-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="c03fc-117">[Tematy usługi Service Bus i subskrypcje](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) Podaj jeden do wielu formę komunikacji w *publikowania/subskrypcji* wzorca.</span><span class="sxs-lookup"><span data-stu-id="c03fc-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="c03fc-118">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="c03fc-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="c03fc-119">[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c03fc-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c03fc-120">Parametry</span><span class="sxs-lookup"><span data-stu-id="c03fc-120">Parameters</span></span>

<span data-ttu-id="c03fc-121">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c03fc-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="c03fc-122">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="c03fc-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="c03fc-123">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="c03fc-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="c03fc-124">Definiuje parametry dla wartości, które będą zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="c03fc-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="c03fc-125">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="c03fc-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="c03fc-126">Szablon Hello definiuje hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="c03fc-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c03fc-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c03fc-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="c03fc-128">Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="c03fc-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="c03fc-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="c03fc-129">serviceBusTopicName</span></span>
<span data-ttu-id="c03fc-130">Nazwa Hello tematu hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="c03fc-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="c03fc-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="c03fc-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="c03fc-132">Nazwa Hello subskrypcji hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="c03fc-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="c03fc-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c03fc-133">serviceBusApiVersion</span></span>
<span data-ttu-id="c03fc-134">wersja interfejsu API usługi Service Bus Hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c03fc-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="c03fc-135">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="c03fc-135">Resources toodeploy</span></span>
<span data-ttu-id="c03fc-136">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**, tematu i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c03fc-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="c03fc-137">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c03fc-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="c03fc-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c03fc-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="c03fc-139">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c03fc-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="c03fc-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c03fc-140">Next steps</span></span>
<span data-ttu-id="c03fc-141">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="c03fc-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="c03fc-142">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c03fc-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c03fc-143">Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="c03fc-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
