---
title: "aaaCreate Azure Event Hubs przestrzeni nazw i konsumentów grupy przy użyciu szablonu | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Event Hubs przy użyciu Centrum zdarzeń i grupy odbiorców za pomocą szablonów usługi Azure Resource Manager"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="6da4a-103">Tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6da4a-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="6da4a-104">W tym artykule opisano, jak toouse szablonu usługi Azure Resource Manager tworzącą przestrzeni nazw typu centra zdarzeń z Centrum zdarzeń jednego i grupie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6da4a-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="6da4a-105">Witaj artykuł przedstawia sposób toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="6da4a-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="6da4a-106">Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań</span><span class="sxs-lookup"><span data-stu-id="6da4a-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="6da4a-107">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="6da4a-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="6da4a-108">Hello pełną szablonu, zobacz hello [szablonu zdarzenia koncentratora i konsumentów grupy] [ Event Hub and consumer group template] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6da4a-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="6da4a-109">toocheck hello najnowsze szablonów, odwiedź stronę hello [szablonów Szybki Start Azure] [ Azure Quickstart Templates] galerii i wyszukaj usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="6da4a-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="6da4a-110">Co chcesz wdrożyć?</span><span class="sxs-lookup"><span data-stu-id="6da4a-110">What will you deploy?</span></span>
<span data-ttu-id="6da4a-111">W przypadku tego szablonu zostanie wdrożona do przestrzeni nazw usługi Event Hubs z Centrum zdarzeń i grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="6da4a-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="6da4a-112">[Centra zdarzeń](event-hubs-what-is-event-hubs.md) jest zdarzeniem przetwarzania używanej tooprovide zdarzenia i dane telemetryczne wejściowych tooAzure w bardzo dużej skali, z małymi opóźnieniami i wysoką niezawodnością.</span><span class="sxs-lookup"><span data-stu-id="6da4a-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="6da4a-113">toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="6da4a-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="6da4a-114">[![Wdrażanie tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6da4a-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="6da4a-115">Parametry</span><span class="sxs-lookup"><span data-stu-id="6da4a-115">Parameters</span></span>
<span data-ttu-id="6da4a-116">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6da4a-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="6da4a-117">Szablon Hello obejmuje sekcję o nazwie `Parameters` zawiera wszystkie wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="6da4a-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="6da4a-118">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub oparte na powitania toowhich środowiska, które wdrażasz.</span><span class="sxs-lookup"><span data-stu-id="6da4a-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="6da4a-119">Definiuje parametry dla wartości, które zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="6da4a-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="6da4a-120">Każda wartość parametru szablonu hello definiuje hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6da4a-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="6da4a-121">Szablon Hello definiuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6da4a-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="6da4a-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="6da4a-122">eventHubNamespaceName</span></span>
<span data-ttu-id="6da4a-123">Nazwa Hello hello centra zdarzeń w przestrzeni nazw toocreate.</span><span class="sxs-lookup"><span data-stu-id="6da4a-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="6da4a-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="6da4a-124">eventHubName</span></span>
<span data-ttu-id="6da4a-125">Nazwa Hello hello Centrum zdarzeń utworzonych w hello centra zdarzeń w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="6da4a-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="6da4a-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="6da4a-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="6da4a-127">Nazwa Hello grupy konsumentów hello utworzone dla hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="6da4a-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="6da4a-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6da4a-128">apiVersion</span></span>
<span data-ttu-id="6da4a-129">Wersja Hello interfejsu API hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6da4a-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="6da4a-130">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="6da4a-130">Resources toodeploy</span></span>
<span data-ttu-id="6da4a-131">Tworzy nazw typu **EventHubs**, z Centrum zdarzeń i grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="6da4a-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="6da4a-132">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6da4a-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="6da4a-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6da4a-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="6da4a-134">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6da4a-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="6da4a-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6da4a-135">Next steps</span></span>
<span data-ttu-id="6da4a-136">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="6da4a-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="6da4a-137">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6da4a-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6da4a-138">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="6da4a-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="6da4a-139">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="6da4a-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
