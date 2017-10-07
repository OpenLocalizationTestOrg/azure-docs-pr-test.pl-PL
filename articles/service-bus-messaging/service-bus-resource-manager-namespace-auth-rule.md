---
title: "reguły autoryzacji usługi Service Bus aaaCreate przy użyciu szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Utworzyć regułę autoryzacji usługi Service Bus dla przestrzeni nazw i kolejki przy użyciu szablonu usługi Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="0b87f-103">Utworzyć regułę autoryzacji usługi Service Bus dla przestrzeni nazw i kolejki przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b87f-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="0b87f-104">W tym artykule przedstawiono sposób toouse szablonu usługi Azure Resource Manager, który tworzy [reguły autoryzacji](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) dla przestrzeni nazw usługi Service Bus i kolejki.</span><span class="sxs-lookup"><span data-stu-id="0b87f-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="0b87f-105">Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="0b87f-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="0b87f-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="0b87f-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="0b87f-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="0b87f-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="0b87f-108">Hello pełną szablonu, zobacz hello [szablonu reguły autoryzacji usługi Service Bus] [ Service Bus auth rule template] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b87f-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="0b87f-109">Hello następujące szablony usługi Azure Resource Manager są dostępne do pobrania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b87f-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="0b87f-110">Tworzenie przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="0b87f-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="0b87f-111">Tworzenie przestrzeni nazw usługi Service Bus z kolejki</span><span class="sxs-lookup"><span data-stu-id="0b87f-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="0b87f-112">Tworzenie przestrzeni nazw usługi Service Bus z tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0b87f-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="0b87f-113">Tworzenie przestrzeni nazw usługi Service Bus z tematu, subskrypcji i reguły</span><span class="sxs-lookup"><span data-stu-id="0b87f-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="0b87f-114">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="0b87f-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="0b87f-115">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="0b87f-115">What will you deploy?</span></span>
<span data-ttu-id="0b87f-116">W przypadku tego szablonu zostanie wdrożona regułę autoryzacji usługi Service Bus dla przestrzeni nazw i jednostki obsługi komunikatów (w tym przypadku kolejki).</span><span class="sxs-lookup"><span data-stu-id="0b87f-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="0b87f-117">Ten szablon używa [dostępu sygnatury dostępu Współdzielonego](service-bus-sas.md) do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0b87f-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="0b87f-118">Sygnatury dostępu Współdzielonego umożliwia aplikacji tooauthenticate tooService magistrali przy użyciu klawisza dostępu skonfigurowane na powitania przestrzeni nazw lub na powitania wiadomości jednostki (kolejka lub temat) określone prawa, które są skojarzone.</span><span class="sxs-lookup"><span data-stu-id="0b87f-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="0b87f-119">Następnie można użyć tego klucza toogenerate tokenu sygnatury dostępu Współdzielonego, którego klienci mogą z kolei używać tooService tooauthenticate magistrali.</span><span class="sxs-lookup"><span data-stu-id="0b87f-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="0b87f-120">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="0b87f-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="0b87f-121">[![Wdrażanie tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0b87f-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="0b87f-122">Parametry</span><span class="sxs-lookup"><span data-stu-id="0b87f-122">Parameters</span></span>

<span data-ttu-id="0b87f-123">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="0b87f-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="0b87f-124">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="0b87f-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="0b87f-125">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="0b87f-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="0b87f-126">Definiuje parametry dla wartości, które będą zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="0b87f-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="0b87f-127">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0b87f-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="0b87f-128">Szablon Hello definiuje hello następujące parametry.</span><span class="sxs-lookup"><span data-stu-id="0b87f-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="0b87f-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="0b87f-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="0b87f-130">Nazwa Hello toocreate przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="0b87f-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="0b87f-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="0b87f-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="0b87f-132">Witaj Nazwa reguły autoryzacji hello hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0b87f-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="0b87f-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="0b87f-133">serviceBusQueueName</span></span>
<span data-ttu-id="0b87f-134">Nazwa Hello kolejki hello w przestrzeni nazw usługi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="0b87f-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="0b87f-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="0b87f-135">serviceBusApiVersion</span></span>
<span data-ttu-id="0b87f-136">wersja interfejsu API usługi Service Bus Hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="0b87f-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="0b87f-137">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="0b87f-137">Resources toodeploy</span></span>
<span data-ttu-id="0b87f-138">Tworzy standardowe przestrzeni nazw usługi Service Bus typu **wiadomości**i reguły autoryzacji usługi Service Bus dla przestrzeni nazw i jednostek.</span><span class="sxs-lookup"><span data-stu-id="0b87f-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="0b87f-139">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="0b87f-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="0b87f-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b87f-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="0b87f-141">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0b87f-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="0b87f-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b87f-142">Next steps</span></span>
<span data-ttu-id="0b87f-143">Po utworzeniu i wdrożeniu zasobów przy użyciu usługi Azure Resource Manager, Dowiedz się, jak toomanage tych zasobów, przeglądając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0b87f-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="0b87f-144">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b87f-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="0b87f-145">Zarządzanie zasobami usługi Service Bus za pomocą hello Eksploratora magistrali usług</span><span class="sxs-lookup"><span data-stu-id="0b87f-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="0b87f-146">Magistrala usług uwierzytelniania i autoryzacji</span><span class="sxs-lookup"><span data-stu-id="0b87f-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
