---
title: "Utwórz subskrypcję tematu Azure Service Bus i reguł, przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="02079-103">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02079-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="02079-104">W tym artykule pokazano, jak użyć szablonu usługi Azure Resource Manager, który tworzy przestrzeń nazw usługi Service Bus z tematu, subskrypcji i reguły (filtru).</span><span class="sxs-lookup"><span data-stu-id="02079-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="02079-105">Dowiesz się, jak do definiowania zasobów, do których są wdrażane i sposób definiowania parametrów, które są określone, gdy wdrożenie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="02079-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="02079-106">Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="02079-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="02079-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="02079-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="02079-108">Aby uzyskać więcej informacji dotyczących rozwiązań i wzorców w konwencji nazewnictwa zasobów platformy Azure, zobacz [konwencje nazewnictwa dla zasobów platformy Azure zalecane][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="02079-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="02079-109">Zakończenie szablonu, zobacz [przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły] [ Service Bus namespace with topic, subscription, and rule] szablonu.</span><span class="sxs-lookup"><span data-stu-id="02079-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="02079-110">Następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="02079-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="02079-111">Tworzenie przestrzeni nazw usługi Service Bus z regułą kolejki i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="02079-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="02079-112">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="02079-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="02079-113">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="02079-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="02079-114">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="02079-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="02079-115">Aby sprawdzić najnowsze szablony, odwiedź stronę [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukiwania dla usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="02079-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="02079-116">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="02079-116">What will you deploy?</span></span>

<span data-ttu-id="02079-117">W przypadku tego szablonu można wdrożyć przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły (filtru).</span><span class="sxs-lookup"><span data-stu-id="02079-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="02079-118">[Tematy usługi Service Bus i subskrypcje](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) Podaj jeden do wielu formę komunikacji w *publikowania/subskrypcji* wzorca.</span><span class="sxs-lookup"><span data-stu-id="02079-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="02079-119">Korzystając z tematów i subskrypcji, składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem temat, który działa jako pośrednik. Subskrypcja tematu przypomina wirtualną kolejkę, która odbiera kopie komunikatów wysłanych do tematu.</span><span class="sxs-lookup"><span data-stu-id="02079-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="02079-120">Filtr subskrypcji umożliwia określenie, które komunikaty wysyłane do tematu są wyświetlane w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="02079-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="02079-121">Co to są reguły (filtry)?</span><span class="sxs-lookup"><span data-stu-id="02079-121">What are rules (filters)?</span></span>

<span data-ttu-id="02079-122">W wielu scenariuszach wiadomości, które mają określone parametry muszą być przetwarzane na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="02079-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="02079-123">Aby je włączyć, można skonfigurować subskrypcje, aby znaleźć wiadomości, które zostały określone właściwości, a następnie wykonaj zmiany w tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="02079-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="02079-124">Mimo że subskrypcje usługi Service Bus, zobacz wszystkich wiadomości wysłanych do tematu, można kopiować tylko podzbiór tych wiadomości do kolejki subskrypcji wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="02079-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="02079-125">Jest to realizowane przy użyciu filtrów subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="02079-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="02079-126">Aby dowiedzieć się więcej na temat reguł (filtry), zobacz [reguł i akcje](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="02079-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="02079-127">Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:</span><span class="sxs-lookup"><span data-stu-id="02079-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="02079-128">[![Wdrażanie na platformie Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="02079-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="02079-129">Parametry</span><span class="sxs-lookup"><span data-stu-id="02079-129">Parameters</span></span>

<span data-ttu-id="02079-130">Z usługi Azure Resource Manager, należy zdefiniować parametrów dla wartości, które chcesz określić podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="02079-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="02079-131">Szablon zawiera sekcję o nazwie `Parameters` obejmującą wszystkie wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="02079-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="02079-132">Parametr powinien obejmować wartości, które różnią się w zależności od wdrażanego projektu lub środowiska, w którym odbywa się wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="02079-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="02079-133">Nie należy definiować parametrów dla wartości, które pozostają niezmienione.</span><span class="sxs-lookup"><span data-stu-id="02079-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="02079-134">Każda wartość parametru używana w szablonie definiuje wdrażane zasoby.</span><span class="sxs-lookup"><span data-stu-id="02079-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="02079-135">Szablon definiuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="02079-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="02079-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="02079-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="02079-137">Nazwa przestrzeni nazw usługi Service Bus do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="02079-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="02079-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="02079-138">serviceBusTopicName</span></span>
<span data-ttu-id="02079-139">Nazwa tematu utworzone w przestrzeni nazw usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="02079-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="02079-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="02079-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="02079-141">Nazwa subskrypcji utworzone w przestrzeni nazw usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="02079-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="02079-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="02079-142">serviceBusRuleName</span></span>
<span data-ttu-id="02079-143">Nazwa rule(filter) utworzone w przestrzeni nazw usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="02079-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="02079-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="02079-144">serviceBusApiVersion</span></span>
<span data-ttu-id="02079-145">Wersja interfejsu API usługi Service Bus szablonu.</span><span class="sxs-lookup"><span data-stu-id="02079-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="02079-146">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="02079-146">Resources to deploy</span></span>
<span data-ttu-id="02079-147">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**, z tematów i subskrypcji i zasadami.</span><span class="sxs-lookup"><span data-stu-id="02079-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="02079-148">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="02079-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="02079-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02079-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="02079-150">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="02079-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="02079-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02079-151">Next steps</span></span>
<span data-ttu-id="02079-152">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak nimi zarządzać, przeglądając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="02079-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="02079-153">Zarządzanie usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="02079-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="02079-154">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="02079-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="02079-155">Zarządzanie zasobami usługi Service Bus za pomocą Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="02079-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

