---
title: "aaaCreate na platformie Azure przy użyciu szablonu aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager toodeploy szablon aplikacji logiki do definiowania przepływów pracy."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="bea5a-103">Tworzenie aplikacji logiki przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="bea5a-103">Create a Logic App using a template</span></span>
<span data-ttu-id="bea5a-104">Szablony zapewniają toouse szybko różnych łączników w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="bea5a-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="bea5a-105">Usługa Logic apps udostępnia szablony usługi Azure Resource Manager toocreate aplikacji logiki, które mogą być używane toodefine przepływów pracy firmowych.</span><span class="sxs-lookup"><span data-stu-id="bea5a-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="bea5a-106">Można zdefiniować zasobów, do których zostały wdrożone, jak i toodefine parametrów podczas wdrażania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="bea5a-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="bea5a-107">Ten szablon służy do scenariuszy biznesowych lub dostosować go toomeet wymagań.</span><span class="sxs-lookup"><span data-stu-id="bea5a-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="bea5a-108">Więcej szczegółów na właściwości aplikacji hello logiki, zobacz [API zarządzania przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="bea5a-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="bea5a-109">Przykłady samą powitalnych definicję można znaleźć [definicjami aplikacji logiki autora](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="bea5a-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="bea5a-110">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bea5a-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="bea5a-111">Hello pełną szablonu, zobacz [szablon aplikacji logiki](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bea5a-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="bea5a-112">Możesz wdrożyć</span><span class="sxs-lookup"><span data-stu-id="bea5a-112">What you deploy</span></span>
<span data-ttu-id="bea5a-113">W przypadku tego szablonu wdrażania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="bea5a-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="bea5a-114">wdrożenia hello toorun automatycznie, wybierz powitania po przycisku:</span><span class="sxs-lookup"><span data-stu-id="bea5a-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="bea5a-115">[![Wdrażanie tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bea5a-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bea5a-116">Parametry</span><span class="sxs-lookup"><span data-stu-id="bea5a-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="bea5a-117">testUri</span><span class="sxs-lookup"><span data-stu-id="bea5a-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="bea5a-118">Toodeploy zasobów</span><span class="sxs-lookup"><span data-stu-id="bea5a-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="bea5a-119">Aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="bea5a-119">Logic app</span></span>
<span data-ttu-id="bea5a-120">Tworzy hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="bea5a-120">Creates hello logic app.</span></span>

<span data-ttu-id="bea5a-121">Szablony Hello używa wartości parametru Nazwa aplikacji hello logiki.</span><span class="sxs-lookup"><span data-stu-id="bea5a-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="bea5a-122">Ustawia lokalizację hello toohello aplikacji logiki hello tej samej lokalizacji co hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bea5a-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="bea5a-123">Tej konkretnej definicji jest uruchamiana raz na godzinę, a polecenia ping hello lokalizacji określonej w hello **testUri** parametru.</span><span class="sxs-lookup"><span data-stu-id="bea5a-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a><span data-ttu-id="bea5a-124">Polecenia toorun wdrożenia</span><span class="sxs-lookup"><span data-stu-id="bea5a-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="bea5a-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bea5a-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="bea5a-126">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bea5a-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



