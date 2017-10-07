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
# <a name="create-a-logic-app-using-a-template"></a>Tworzenie aplikacji logiki przy użyciu szablonu
Szablony zapewniają toouse szybko różnych łączników w aplikacji logiki. Usługa Logic apps udostępnia szablony usługi Azure Resource Manager toocreate aplikacji logiki, które mogą być używane toodefine przepływów pracy firmowych. Można zdefiniować zasobów, do których zostały wdrożone, jak i toodefine parametrów podczas wdrażania aplikacji logiki. Ten szablon służy do scenariuszy biznesowych lub dostosować go toomeet wymagań.

Więcej szczegółów na właściwości aplikacji hello logiki, zobacz [API zarządzania przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Przykłady samą powitalnych definicję można znaleźć [definicjami aplikacji logiki autora](logic-apps-author-definitions.md). 

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

Hello pełną szablonu, zobacz [szablon aplikacji logiki](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Możesz wdrożyć
W przypadku tego szablonu wdrażania aplikacji logiki.

wdrożenia hello toorun automatycznie, wybierz powitania po przycisku:  

[![Wdrażanie tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Toodeploy zasobów
### <a name="logic-app"></a>Aplikacji logiki
Tworzy hello aplikacji logiki.

Szablony Hello używa wartości parametru Nazwa aplikacji hello logiki. Ustawia lokalizację hello toohello aplikacji logiki hello tej samej lokalizacji co hello grupy zasobów. 

Tej konkretnej definicji jest uruchamiana raz na godzinę, a polecenia ping hello lokalizacji określonej w hello **testUri** parametru. 

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


## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



