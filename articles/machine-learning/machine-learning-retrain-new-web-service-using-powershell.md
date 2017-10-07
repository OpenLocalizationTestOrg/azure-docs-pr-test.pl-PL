---
title: "aaaRetrain nowej usługi Azure Machine Learning usługi sieci web przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprogrammatically ponownie ucz i aktualizacji hello sieci web usługi toouse hello nowo uczonego modelu w usłudze Azure Machine Learning przy użyciu poleceń cmdlet programu PowerShell do zarządzania Machine Learning hello."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Usługi sieci web na podstawie nowego Menedżera zasobów za pomocą poleceń cmdlet programu PowerShell do zarządzania Machine Learning hello retrain
Gdy retrain nową usługę sieci web, należy zaktualizować hello predykcyjnego modelu usług sieci web definicji tooreference hello nowe przeszkolone.  

## <a name="prerequisites"></a>Wymagania wstępne
Należy zdefiniować eksperyment uczenia i eksperyment predykcyjny pokazane [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> eksperyment predykcyjny Hello musi być wdrożony jako maszyna usługi Azure Resource Manager (nowy) na podstawie szkoleniowe dotyczące usługi sieci web. toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Ten proces wymaga, że zainstalowano hello polecenia cmdlet usługi Azure Machine Learning. Instalowanie poleceń cmdlet usługi Machine Learning hello informacji, zobacz hello [polecenia cmdlet usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN.

Witaj skopiowanych następujących informacji z hello ponownego trenowania danych wyjściowych:

* BaseLocation
* RelativeLocation

Witaj czynności, które możesz wykonać są:

1. Zaloguj się tooyour konta usługi Azure Resource Manager.
2. Pobierz definicję usługi sieci web hello
3. Eksportuj hello definicji usługi sieci Web w formacie JSON
4. Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.
5. Importowanie hello JSON do definicji usługi sieci Web
6. Usługi sieci web hello aktualizacji z nowej definicji usługi sieci Web

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Zaloguj się tooyour konta usługi Azure Resource Manager
Musisz najpierw zalogować się tooyour konto platformy Azure z środowisku PowerShell hello przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.

## <a name="get-hello-web-service-definition"></a>Pobierz hello definicji usługi sieci Web
Następnie Pobierz hello usługi sieci Web przez wywołanie hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet. Hello definicji usługi sieci Web jest wewnętrznej reprezentacji hello uczonego modelu hello usługi sieci web, a nie można bezpośrednio modyfikować. Upewnij się, że są pobierane hello definicji usługi sieci Web dla Twojego eksperyment predykcyjny i nie eksperyment uczenia.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, uruchom polecenie cmdlet Get-AzureRmMlWebService hello bez żadnych parametrów toodisplay hello sieci web usług w Twojej subskrypcji. Zlokalizuj hello usługi sieci web, a następnie sprawdź jej identyfikatora usługi sieci web Witaj Nazwa grupy zasobów hello jest czwartym elementem hello w identyfikatorze hello zaraz po hello *resourceGroups* elementu. W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Alternatywnie toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, logowanie w portalu usługi sieci Web Microsoft Azure Machine Learning toohello. Wybierz usługę sieci web hello. Nazwa grupy zasobów Hello jest hello elementu piątym powitania adres URL usługi sieci web hello, zaraz po hello *resourceGroups* elementu. W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Eksportuj hello definicji usługi sieci Web w formacie JSON
toomodify hello definicji toohello uczony model toouse nowo hello Trenowanego modelu, należy najpierw użyć hello [AzureRmMlWebService eksportu](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport polecenia cmdlet go tooa plik w formacie JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.
Zasoby hello odszukaj hello [uczonego modelu] hello aktualizacji *uri* wartość hello *locationInfo* węzeł z identyfikatora URI obiektu hello ilearner blob hello. Witaj identyfikatora URI jest generowany przez połączenie hello *BaseLocation* i hello *RelativeLocation* z wyników hello hello BES Wywołanie ponownego trenowania. Spowoduje to zaktualizowanie hello ścieżki tooreference hello nowe trenowanego modelu.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>Importowanie hello JSON do definicji usługi sieci Web
Należy użyć hello [AzureRmMlWebService importu](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert polecenia cmdlet zmodyfikowany plik JSON do definicji usługi sieci Web, których można używać hello tooupdate definicji usługi sieci Web.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Usługi sieci web hello aktualizacji z nowej definicji usługi sieci Web
Na koniec użyj [AzureRmMlWebService aktualizacji](https://msdn.microsoft.com/library/azure/mt767922.aspx) polecenia cmdlet tooupdate hello definicji usługi sieci Web.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Podsumowanie
Przy użyciu poleceń cmdlet do zarządzania hello Machine Learning PowerShell, można zaktualizować hello uczonego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:

* Model okresowego ponownego trenowania nowymi danymi.
* Dystrybucja toocustomers modelu hello celem jest umożliwienie je ponownie ucz hello modelu, używając własnych danych.

