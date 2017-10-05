---
title: "Wdrażanie aplikacji sieci web, przy użyciu MSDeploy z certyfikatów ssl i nazwy hosta"
description: "Szablon usługi Azure Resource Manager umożliwia wdrażanie aplikacji sieci web, przy użyciu MSDeploy i konfigurowanie niestandardowej nazwy hosta i certyfikatem SSL"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Wdrażanie aplikacji sieci web z MSDeploy, niestandardową nazwę hosta i certyfikat protokołu SSL
Ten przewodnik przeprowadzi Cię przez tworzenie end-to-end wdrożenia dla aplikacji sieci Web platformy Azure, wykorzystując MSDeploy, a także Dodawanie niestandardowej nazwy hosta i certyfikat SSL do szablonu ARM.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Tworzenie przykładowej aplikacji
Wdrażania aplikacji sieci web ASP.NET. Pierwszym krokiem jest utworzenie prostą aplikację sieci web (lub można użyć istniejącego — w takim przypadku możesz pominąć ten krok).

Otwórz program Visual Studio 2015 i wybrać plik > Nowy projekt. W wyświetlonym oknie dialogowym Wybierz sieci Web > Aplikacja sieci Web ASP.NET. W obszarze szablonów wybierz sieci Web, a następnie wybierz szablon MVC. Wybierz *Zmień typ uwierzytelniania* do *bez uwierzytelniania*. To jest tylko tworzenie przykładowej aplikacji, wystarczy.

W tym momencie będziesz mieć podstawowe aplikacji sieci web ASP.Net gotowe do użycia w ramach procesu wdrażania.

### <a name="create-msdeploy-package"></a>Utwórz pakiet MSDeploy
Następnym krokiem jest, aby utworzyć pakiet do wdrożenia aplikacji sieci web na platformie Azure. W tym celu należy zapisać projekt, a następnie uruchom następujące polecenie w wierszu polecenia:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Spowoduje to utworzenie pakietu ZIP w folderze tabelę PackageLocation. Aplikacja jest teraz gotowa do wdrożenia, które można teraz utworzyć limit szablonu usługi Azure Resource Manager w tym.

### <a name="create-arm-template"></a>Utwórz szablon ARM
Po pierwsze Zacznijmy podstawowy szablon ARM, który spowoduje utworzenie aplikacji sieci web i plan hostingu (należy pamiętać, że parametry i zmienne nie są pokazywane w celu jego skrócenia).

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

Następnie należy zmodyfikować zasobów aplikacji sieci web do podjęcia zagnieżdżonych zasobów MSDeploy. Dzięki temu będzie można odwołania do pakietu utworzonego wcześniej i poinformuj usługi Azure Resource Manager umożliwia MSDeploy można wdrożyć pakietu dla aplikacji sieci Web platformy Azure. Poniżej przedstawiono zasób Microsoft.Web/sites o zagnieżdżonych zasobów MSDeploy:

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

Teraz można zauważyć, że zasób MSDeploy przyjmuje **packageUri** właściwość, która jest zdefiniowana w następujący sposób:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

To **packageUri** pobiera identyfikator uri konta magazynu, która wskazuje na konto magazynu, gdzie możesz przekazać pocztowy do pakietu. Będzie korzystać z usługi Azure Resource Manager [sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) do Rozwiń pakiet lokalnie z konta magazynu podczas wdrażania szablonu. Ten proces będzie można zautomatyzować za pomocą skryptu programu PowerShell, przekaż pakiet i wywołania interfejsu API zarządzania platformy Azure do tworzenia kluczy, wymaganych i przekazania ich na szablon jako parametry (*_artifactsLocation* i *_artifactsLocationSasToken*). Należy określić parametry w folderze i nazwa pliku pakietu zostanie przesłany w ramach kontenera magazynu.

Następnie należy dodać w inny zasób zagnieżdżonych konfiguracja powiązań z nazwami hostów wykorzystać domeny niestandardowej. Najpierw należy zapewnić własnej nazwy hosta i ustaw go do weryfikacji przez platformę Azure własne jej — zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md). Po zakończeniu tej operacji można dodać do szablonu w sekcji zasobów Microsoft.Web/sites następujące:

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

Na koniec należy dodać najwyższego poziomu zasób Microsoft.Web/certificates. Ten zasób będzie zawierać certyfikatu SSL i będzie istnieć na tym samym poziomie jako aplikacji sieci web i plan hostingu.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

Musisz mieć ważny certyfikat SSL w celu skonfigurowania tego zasobu. Po określeniu, że prawidłowy certyfikat należy wyodrębnić bajtów pfx jako ciąg base64. Użyj następującego polecenia programu PowerShell jest jedną opcję, aby wyodrębnić to:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Użytkownik może następnie przekazać jako parametru, do wdrożenia szablonu ARM.

Na tym etapie szablon ARM jest gotowy.

### <a name="deploy-template"></a>Wdrażanie szablonu
Końcowe czynności mają element to wszystkich elementów do wdrażania pełnej end-to-end. Aby wdrożenie łatwiej można wykorzystać **AzureResourceGroup.ps1 Wdróż** skrypt PowerShell, który jest dodawany po utworzeniu projektu grupy zasobów platformy Azure w Visual Studio, aby ułatwić przekazywanie wszelkie artefakty wymagane w szablonie. Wymaga utworzono konto magazynu, którego chcesz użyć wcześniejsze. Na przykład utworzono konto magazynu udostępnionego dla pakiet.zip do załadowania. Skrypt będzie korzystać z narzędzia AzCopy, aby przekazać pakiet do konta magazynu. Przekazać w lokalizacji folderu artefaktów i skrypt automatycznie przekazać do kontenera magazynu o nazwie wszystkie pliki w tym katalogu. Po wywołaniu metody wdrażania AzureResourceGroup.ps1 należy zaktualizować powiązania SSL, aby zamapować niestandardową nazwę hosta przy użyciu certyfikatu SSL.

Następujące PowerShell Wyświetla pełne wdrożenie wywoływania Wdróż-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

W tym momencie aplikacja powinna zostały wdrożone, oraz powinny być możliwe przeglądanie za pomocą https://www.yourcustomdomain.com

