---
title: "Wdrażanie aplikacji sieci web, która jest połączona z repozytorium GitHub | Dokumentacja firmy Microsoft"
description: "Szablon usługi Azure Resource Manager umożliwia wdrażanie aplikacji sieci web, który zawiera projekt z repozytorium GitHub."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a>Wdrażanie aplikacji sieci web, połączony z repozytorium GitHub
W tym temacie dowiesz się, jak utworzyć szablon usługi Azure Resource Manager, która wdraża aplikację sieci web, która jest połączona z projektem w repozytorium GitHub. Dowiesz się, jak do definiowania zasobów, do których są wdrażane i sposób definiowania parametrów, które są określone, gdy wdrożenie jest wykonywane. Można użyć tego szablonu na potrzeby własnych wdrożeń lub dostosować go do konkretnych potrzeb.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

Zakończenie szablonu, zobacz [sieci Web aplikacji połączonych do szablonu usługi GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Zostanie wdrożona
W przypadku tego szablonu zostanie wdrożona aplikacja sieci web, która zawiera kod z projektem w usłudze GitHub.

Aby automatycznie uruchomić wdrożenie, kliknij poniższy przycisk:

[![Wdrażanie na platformie Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parametry
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Adres URL repozytorium GitHub, zawierający projekt do wdrożenia. Ten parametr zawiera wartość domyślną, ale ta wartość jest przeznaczona tylko do opisano, jak wprowadzić adres URL repozytorium. Tej wartości można użyć podczas testowania szablonu, ale można podać adres URL własnych repozytorium podczas pracy z szablonem.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Gałęzi
Rozgałęzienie repozytorium do użycia podczas wdrażania aplikacji. Wartością domyślną jest baza danych master, ale można podać nazwę dowolnego gałęzi w repozytorium, który chcesz wdrożyć.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a>Zasoby wymagające wdrożenia
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Aplikacja internetowa
Tworzy aplikacji sieci web, z którym powiązany jest projekt w witrynie GitHub. 

Należy określić nazwę aplikacji sieci web za pośrednictwem **siteName** parametr i lokalizacja aplikacji sieci web za pomocą **siteLocation** parametru. W **dependsOn** element, szablon definiuje aplikacji sieci web jako zależne od usługi plan hostingu. Ponieważ jest on zależny od plan hostingu, aplikacji sieci web nie zostanie utworzony, do momentu zakończenia plan hostingu tworzona. **DependsOn** elementu tylko służy do określania kolejności wdrażania. Jeśli aplikacja sieci web jako zależne plan hostingu nie jest zaznaczone, Mananger zasobów Azure podejmie próbę utworzenia oba zasoby w tym samym czasie i może wystąpić błąd, jeśli aplikacja sieci web został utworzony przed plan hostingu.

Aplikacja sieci web ma również zasobu podrzędnego, który jest zdefiniowany w **zasobów** poniższej sekcji. Ten zasób podrzędnych definiuje kontroli źródła dla projektu z aplikacji sieci web. W tym szablonie kontroli źródła jest połączony z konkretnym repozytorium GitHub. Repozytorium GitHub jest zdefiniowany kod **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** możesz kodowane adres URL repozytorium, gdy chcesz utworzyć szablon, który wdraża wielokrotnie pojedynczy Projekt podczas wymagające minimalną liczbę parametrów.
Zamiast kodować adres URL repozytorium, możesz dodać parametr adresu URL repozytorium i użycie tej wartości dla **RepoUrl** właściwości.

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

## <a name="commands-to-run-deployment"></a>Polecenia umożliwiające uruchomienie wdrożenia
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Dla zawartości pliku JSON parametrów, zobacz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

