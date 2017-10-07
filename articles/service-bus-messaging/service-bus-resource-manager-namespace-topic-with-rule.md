---
title: "aaaCreate subskrypcję tematu Azure Service Bus i reguł, przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły przy użyciu szablonu usługi Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="49a91-103">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49a91-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="49a91-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły (filtru).</span><span class="sxs-lookup"><span data-stu-id="49a91-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="49a91-105">Dowiesz się, jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="49a91-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="49a91-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań</span><span class="sxs-lookup"><span data-stu-id="49a91-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="49a91-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="49a91-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="49a91-108">Aby uzyskać więcej informacji dotyczących rozwiązań i wzorców w konwencji nazewnictwa zasobów platformy Azure, zobacz [konwencje nazewnictwa dla zasobów platformy Azure zalecane][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="49a91-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="49a91-109">Hello pełną szablonu, zobacz hello [przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły] [ Service Bus namespace with topic, subscription, and rule] szablonu.</span><span class="sxs-lookup"><span data-stu-id="49a91-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="49a91-110">Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="49a91-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="49a91-111">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="49a91-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="49a91-112">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="49a91-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="49a91-113">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="49a91-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="49a91-114">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="49a91-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="49a91-115">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukiwania dla usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="49a91-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="49a91-116">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="49a91-116">What will you deploy?</span></span>

<span data-ttu-id="49a91-117">W przypadku tego szablonu można wdrożyć przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły (filtru).</span><span class="sxs-lookup"><span data-stu-id="49a91-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="49a91-118">[Tematy usługi Service Bus i subskrypcje](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) Podaj jeden do wielu formę komunikacji w *publikowania/subskrypcji* wzorca.</span><span class="sxs-lookup"><span data-stu-id="49a91-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="49a91-119">Korzystając z tematów i subskrypcji, składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem temat, który działa jako pośrednik. Tooa subskrypcja tematu przypomina wirtualną kolejkę, która odbiera kopie komunikatów wysłanych toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="49a91-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="49a91-120">Filtr subskrypcji umożliwia toospecify wysyłane wiadomości, które tooa tematu powinny pojawić się w ramach subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="49a91-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="49a91-121">Co to są reguły (filtry)?</span><span class="sxs-lookup"><span data-stu-id="49a91-121">What are rules (filters)?</span></span>

<span data-ttu-id="49a91-122">W wielu scenariuszach wiadomości, które mają określone parametry muszą być przetwarzane na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="49a91-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="49a91-123">tooenable, można skonfigurować subskrypcje toofind wiadomości, które zostały określone właściwości, a następnie wykonaj modyfikacje toothose właściwości.</span><span class="sxs-lookup"><span data-stu-id="49a91-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="49a91-124">Mimo że subskrypcje usługi Service Bus, zobacz wszystkich wiadomości wysłanych toohello temacie, można kopiować tylko podzbiór tych kolejki subskrypcji wirtualnego toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="49a91-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="49a91-125">Jest to realizowane przy użyciu filtrów subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="49a91-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="49a91-126">toolearn więcej informacji na temat reguł (filtry), zobacz [reguł i akcje](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="49a91-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="49a91-127">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="49a91-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="49a91-128">[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="49a91-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="49a91-129">Parametry</span><span class="sxs-lookup"><span data-stu-id="49a91-129">Parameters</span></span>

<span data-ttu-id="49a91-130">Z usługi Azure Resource Manager, należy zdefiniować parametrów dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="49a91-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="49a91-131">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="49a91-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="49a91-132">Należy zdefiniować parametr dla tych wartości, które różnią się na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="49a91-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="49a91-133">Definiuje parametry dla wartości, które zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="49a91-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="49a91-134">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="49a91-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="49a91-135">Szablon Hello definiuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="49a91-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="49a91-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="49a91-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="49a91-137">Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="49a91-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="49a91-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="49a91-138">serviceBusTopicName</span></span>
<span data-ttu-id="49a91-139">Nazwa Hello tematu hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="49a91-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="49a91-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="49a91-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="49a91-141">Nazwa Hello subskrypcji hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="49a91-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="49a91-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="49a91-142">serviceBusRuleName</span></span>
<span data-ttu-id="49a91-143">Nazwa Hello rule(filter) hello utworzone w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="49a91-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="49a91-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="49a91-144">serviceBusApiVersion</span></span>
<span data-ttu-id="49a91-145">wersja interfejsu API usługi Service Bus Hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="49a91-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="49a91-146">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="49a91-146">Resources toodeploy</span></span>
<span data-ttu-id="49a91-147">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**, z tematów i subskrypcji i zasadami.</span><span class="sxs-lookup"><span data-stu-id="49a91-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="49a91-148">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="49a91-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="49a91-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49a91-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="49a91-150">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="49a91-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="49a91-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49a91-151">Next steps</span></span>
<span data-ttu-id="49a91-152">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="49a91-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="49a91-153">Zarządzanie usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="49a91-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="49a91-154">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="49a91-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="49a91-155">Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="49a91-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

