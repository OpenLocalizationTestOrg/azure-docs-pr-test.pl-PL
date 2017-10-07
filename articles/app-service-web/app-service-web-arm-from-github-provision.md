---
title: "aaaDeploy aplikacji sieci web, która jest połączona z repozytorium GitHub tooa | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager toodeploy szablonu aplikacji sieci web, który zawiera projekt z repozytorium GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Wdrażanie repozytorium GitHub tooa połączonych aplikacji sieci web
W tym temacie dowiesz się, jak toocreate szablonu usługi Azure Resource Manager, która wdraża aplikację sieci web, która jest połączona tooa projektu w repozytorium GitHub. Dowiesz się jak toodefine zasobów, do których są wdrażane i jak parametry toodefine, które są określone, podczas wdrażania hello jest wykonywana. Można użyć tego szablonu własnych wdrożeniach lub dostosować go toomeet wymagań.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

Hello pełną szablonu, zobacz [połączonej aplikacji sieci Web szablonu tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Zostanie wdrożona
W przypadku tego szablonu zostanie wdrożona w aplikacji sieci web zawierający kod hello z projektu w witrynie GitHub.

toorun automatycznie hello wdrożenia, kliknij powitania po przycisku:

[![Wdrażanie tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
adres URL Hello repozytorium GitHub, zawierający hello toodeploy projektu. Ten parametr zawiera wartość domyślną, ale ta wartość jest tylko zamierzonego tooshow należy jak tooprovide hello adres URL dla repozytorium. Tej wartości można użyć podczas testowania hello szablonu, ale będzie tooprovide hello URL własnych repozytorium podczas pracy z hello szablonu.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Gałęzi
Rozgałęzienie Hello hello repozytorium toouse podczas wdrażania aplikacji hello. Wartość domyślna Hello jest baza danych master, ale można podać nazwę hello żadnych gałęzi w repozytorium hello że chcesz toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Toodeploy zasobów
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Aplikacja internetowa
Tworzy hello aplikacji sieci web, który jest połączony toohello projektu w witrynie GitHub. 

Należy określić nazwę hello hello aplikacji sieci web za pośrednictwem hello **siteName** parametru i lokalizację hello hello aplikacji sieci web za pośrednictwem hello **siteLocation** parametru. W hello **dependsOn** elementu hello szablon definiuje hello aplikacji sieci web jako zależne od usługi hello plan hostingu. Ponieważ jest on zależny od hello plan hostingu, hello aplikacji sieci web nie zostanie utworzony, do momentu zakończenia hello plan hostingu tworzona. Witaj **dependsOn** element jest tylko używane toospecify kolejności wdrażania. Jeśli nie zostanie zaznaczone hello aplikacji sieci web jako zależne hello plan hostingu, Mananger zasobów platformy Azure będzie podejmować toocreate oba zasoby na powitania tym samym czasie i może zostać wyświetlony błąd hello aplikacji sieci web zostanie utworzony przed hello plan hostingu.

Aplikacja sieci web Hello ma również zasobu podrzędnego, który jest zdefiniowany w **zasobów** poniższej sekcji. Ten zasób podrzędnych definiuje kontroli źródła dla projektu hello wdrażane hello aplikacji sieci web. W tym szablonie hello kontroli źródła jest połączony tooa określonego repozytorium GitHub. repozytorium GitHub Hello jest zdefiniowana z kodem hello **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** może adres URL repozytorium hello kodowane należy toocreate szablon, który wdraża wielokrotnie pojedynczego projektu podczas wymagające hello minimalną liczbę parametrów.
Zamiast kodować hello adres URL repozytorium, możesz dodać parametr adresu URL repozytorium hello i użycie tej wartości na powitania **RepoUrl** właściwości.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Polecenia toorun wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Dla zawartości pliku JSON hello parametrów, zobacz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

