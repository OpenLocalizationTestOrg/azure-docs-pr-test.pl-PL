---
title: "aaaDeploy aplikacji sieci web przy użyciu narzędzia MSDeploy z certyfikatów ssl i nazwy hosta"
description: "Użycie toodeploy szablonu usługi Azure Resource Manager aplikacji sieci web przy użyciu MSDeploy i konfigurowanie niestandardowej nazwy hosta i certyfikatem SSL"
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Wdrażanie aplikacji sieci web z MSDeploy, niestandardową nazwę hosta i certyfikat protokołu SSL
Ten przewodnik przeprowadzi Cię przez tworzenie end-to-end wdrożenia dla aplikacji sieci Web platformy Azure, wykorzystaniu MSDeploy, a także Dodawanie niestandardowej nazwy hosta i szablon ARM toohello certyfikatu SSL.

Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [Authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Tworzenie przykładowej aplikacji
Wdrażania aplikacji sieci web ASP.NET. pierwszym krokiem Hello toocreate prostą aplikację sieci web (lub toouse można wybrać istniejący — w takim przypadku możesz pominąć ten krok).

Otwórz program Visual Studio 2015 i wybrać plik > Nowy projekt. W oknie dialogowym hello, który pojawia się wybrać sieci Web > Aplikacja sieci Web ASP.NET. W obszarze szablonów wybierz sieci Web, a następnie wybierz szablon MVC hello. Wybierz *Zmień typ uwierzytelniania* za*bez uwierzytelniania*. Jest to po prostu toomake hello przykładowej aplikacji, wystarczy.

W tym momencie będziesz mieć podstawowe ASP.Net web app gotowe toouse w ramach procesu wdrażania.

### <a name="create-msdeploy-package"></a>Utwórz pakiet MSDeploy
Następnym krokiem jest tooAzure aplikacji sieci web hello toodeploy toocreate hello pakietu. toodo, Zapisz projekt, a następnie uruchom następujące hello z wiersza polecenia hello:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Spowoduje to utworzenie pakietu ZIP w folderze tabelę PackageLocation hello. Witaj aplikacji jest teraz gotowa toobe wdrożeniu, które można teraz utworzyć limit toodo szablonu usługi Azure Resource Manager który.

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

Następnie należy toomodify hello sieci web aplikacji zasobów tootake zagnieżdżonych zasobów MSDeploy. To spowoduje Zezwól możesz tooreference hello pakietu utworzonego wcześniej i poinformuj usługi Azure Resource Manager toouse MSDeploy toodeploy hello pakietu toohello aplikacji sieci Web platformy Azure. Oto Hello hello Microsoft.Web/sites zasobów z zasobem MSDeploy hello zagnieżdżone:

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

Teraz można zauważyć przyjmuje tego hello zasobów MSDeploy **packageUri** właściwość, która jest zdefiniowana w następujący sposób:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

To **packageUri** przyjmuje hello identyfikator uri konta magazynu, którego konto magazynu toohello, gdzie możesz przekazać pocztowy pakietu do punktu. Witaj usługi Azure Resource Manager będzie korzystać z [sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pakietu hello toopull dół lokalnie z konta magazynu hello podczas wdrażania szablonu hello. Ten proces będzie można zautomatyzować za pomocą skryptu programu PowerShell, przekaż pakiet hello i wywołać hello Azure Management API toocreate hello klucze są wymagane i przekazania ich na powitania szablonu jako parametry (*_artifactsLocation* i *_artifactsLocationSasToken*). Musisz mieć parametry toodefine folderu hello oraz filename hello pakiet jest kontenera magazynu hello toounder przekazane.

Następnie należy tooadd w innym zagnieżdżonych zasobów toosetup hello hostname powiązania tooleverage domeny niestandardowej. Będzie pierwszy tooensure potrzeby właścicielem hello nazwy hosta, a następnie skonfigurować toobe zweryfikowane przez usługę Azure jego właścicielem — zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md). Po zakończeniu tej operacji można dodać następującego szablonu tooyour w sekcji zasobów Microsoft.Web/sites hello hello:

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

Na koniec należy tooadd inny zasób najwyższego poziomu, Microsoft.Web/certificates. Ten zasób będzie zawierać certyfikatu SSL i będzie istniał w momencie powitalne sam poziom jako aplikacji sieci web i hostingu plan.

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

Konieczne będzie toohave ważnego certyfikatu SSL w kolejności tooset się tego zasobu. Po określeniu, że prawidłowy certyfikat należy tooextract hello pfx bajtów jako ciąg base64. Jedną z opcji tooextract to hello toouse następującego polecenia programu PowerShell:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Można następnie przekazać to jako parametr tooyour ARM wdrażania szablonu.

Na tym etapie szablon ARM hello jest gotowy.

### <a name="deploy-template"></a>Wdrażanie szablonu
Witaj ostatnie kroki są toopiece to wszystkich elementów do wdrażania pełnej end-to-end. łatwiejsze, można wykorzystać hello wdrożenia toomake **AzureResourceGroup.ps1 Wdróż** skrypt PowerShell, który jest dodawany po utworzeniu projektu grupy zasobów platformy Azure w Visual Studio toohelp z przekazywanie wszelkie artefakty wymagane w Szablon Hello. Wymaga to toohave utworzone konto magazynu, które chcesz toouse wcześniejsze. Na przykład utworzono konto magazynu udostępnionego dla toobe pakiet.zip hello przekazany. skrypt Hello będzie korzystać z konta magazynu toohello AzCopy tooupload hello pakietu. Przekaż w lokalizacji folderu artefaktów i hello skryptu spowoduje automatyczne przekazywanie wszystkich plików w tym toohello katalog o nazwie kontenera magazynu. Po wywołaniu metody wdrażania AzureResourceGroup.ps1 masz toothen aktualizacji hello SSL powiązania toomap hello niestandardową nazwę hosta przy użyciu certyfikatu SSL.

powitania po programu PowerShell pokazuje hello hello wywoływania ukończenia wdrożenia Wdróż-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

W tym momencie aplikacja powinna zostały wdrożone, oraz powinno być możliwe toobrowse tooit za pośrednictwem https://www.yourcustomdomain.com

