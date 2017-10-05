---
title: "Tworzenie aplikacji logiki na platformie Azure przy użyciu szablonu | Dokumentacja firmy Microsoft"
description: "Wdrażanie aplikacji logiki do definiowania przepływów pracy za pomocą szablonu usługi Azure Resource Manager."
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
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="ddab8-103">Tworzenie aplikacji logiki przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="ddab8-103">Create a Logic App using a template</span></span>
<span data-ttu-id="ddab8-104">Szablony umożliwiają szybkie użyć różnych łączników w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ddab8-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="ddab8-105">Aplikacje logiki zawiera szablony usługi Azure Resource Manager umożliwia tworzenie aplikacji logiki, który może służyć do definiowania przepływów pracy firmowych.</span><span class="sxs-lookup"><span data-stu-id="ddab8-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="ddab8-106">Można zdefiniować zasobów, do których są wdrażane, a także sposób definiowania parametrów podczas wdrażania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ddab8-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="ddab8-107">Możesz użyć tego szablonu dla scenariuszy biznesowych lub dostosować go do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="ddab8-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="ddab8-108">Więcej szczegółów na właściwości aplikacji logiki, zobacz [API zarządzania przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddab8-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="ddab8-109">Aby uzyskać przykłady samą definicję, zobacz [definicjami aplikacji logiki autora](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="ddab8-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="ddab8-110">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ddab8-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ddab8-111">Zakończenie szablonu, zobacz [szablon aplikacji logiki](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ddab8-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="ddab8-112">Możesz wdrożyć</span><span class="sxs-lookup"><span data-stu-id="ddab8-112">What you deploy</span></span>
<span data-ttu-id="ddab8-113">W przypadku tego szablonu wdrażania aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ddab8-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="ddab8-114">Aby automatycznie uruchamiać wdrożenie, przycisk:</span><span class="sxs-lookup"><span data-stu-id="ddab8-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="ddab8-115">[![Wdrażanie na platformie Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ddab8-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ddab8-116">Parametry</span><span class="sxs-lookup"><span data-stu-id="ddab8-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="ddab8-117">testUri</span><span class="sxs-lookup"><span data-stu-id="ddab8-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="ddab8-118">Zasoby wymagające wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ddab8-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="ddab8-119">Aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ddab8-119">Logic app</span></span>
<span data-ttu-id="ddab8-120">Tworzenie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ddab8-120">Creates the logic app.</span></span>

<span data-ttu-id="ddab8-121">Szablony używa wartości parametru Nazwa aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="ddab8-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="ddab8-122">Ustawia lokalizację aplikacji logiki do tej samej lokalizacji co grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ddab8-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="ddab8-123">Tej konkretnej definicji jest uruchamiana raz na godzinę, a następnie wysyła pakiet usługi ping do lokalizacji określonej w **testUri** parametru.</span><span class="sxs-lookup"><span data-stu-id="ddab8-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

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


## <a name="commands-to-run-deployment"></a><span data-ttu-id="ddab8-124">Polecenia umożliwiające uruchomienie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ddab8-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="ddab8-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddab8-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="ddab8-126">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ddab8-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



