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
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="83a4e-103">Usługi sieci web na podstawie nowego Menedżera zasobów za pomocą poleceń cmdlet programu PowerShell do zarządzania Machine Learning hello retrain</span><span class="sxs-lookup"><span data-stu-id="83a4e-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="83a4e-104">Gdy retrain nową usługę sieci web, należy zaktualizować hello predykcyjnego modelu usług sieci web definicji tooreference hello nowe przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="83a4e-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="83a4e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83a4e-105">Prerequisites</span></span>
<span data-ttu-id="83a4e-106">Należy zdefiniować eksperyment uczenia i eksperyment predykcyjny pokazane [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="83a4e-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="83a4e-107">eksperyment predykcyjny Hello musi być wdrożony jako maszyna usługi Azure Resource Manager (nowy) na podstawie szkoleniowe dotyczące usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="83a4e-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="83a4e-108">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="83a4e-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="83a4e-109">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="83a4e-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="83a4e-110">Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="83a4e-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="83a4e-111">Ten proces wymaga, że zainstalowano hello polecenia cmdlet usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="83a4e-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="83a4e-112">Instalowanie poleceń cmdlet usługi Machine Learning hello informacji, zobacz hello [polecenia cmdlet usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="83a4e-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="83a4e-113">Witaj skopiowanych następujących informacji z hello ponownego trenowania danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="83a4e-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="83a4e-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="83a4e-114">BaseLocation</span></span>
* <span data-ttu-id="83a4e-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="83a4e-115">RelativeLocation</span></span>

<span data-ttu-id="83a4e-116">Witaj czynności, które możesz wykonać są:</span><span class="sxs-lookup"><span data-stu-id="83a4e-116">hello steps you take are:</span></span>

1. <span data-ttu-id="83a4e-117">Zaloguj się tooyour konta usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="83a4e-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="83a4e-118">Pobierz definicję usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="83a4e-118">Get hello web service definition</span></span>
3. <span data-ttu-id="83a4e-119">Eksportuj hello definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="83a4e-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="83a4e-120">Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="83a4e-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="83a4e-121">Importowanie hello JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="83a4e-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="83a4e-122">Usługi sieci web hello aktualizacji z nowej definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="83a4e-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="83a4e-123">Zaloguj się tooyour konta usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="83a4e-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="83a4e-124">Musisz najpierw zalogować się tooyour konto platformy Azure z środowisku PowerShell hello przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83a4e-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="83a4e-125">Pobierz hello definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="83a4e-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="83a4e-126">Następnie Pobierz hello usługi sieci Web przez wywołanie hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="83a4e-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="83a4e-127">Hello definicji usługi sieci Web jest wewnętrznej reprezentacji hello uczonego modelu hello usługi sieci web, a nie można bezpośrednio modyfikować.</span><span class="sxs-lookup"><span data-stu-id="83a4e-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="83a4e-128">Upewnij się, że są pobierane hello definicji usługi sieci Web dla Twojego eksperyment predykcyjny i nie eksperyment uczenia.</span><span class="sxs-lookup"><span data-stu-id="83a4e-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="83a4e-129">toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, uruchom polecenie cmdlet Get-AzureRmMlWebService hello bez żadnych parametrów toodisplay hello sieci web usług w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83a4e-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="83a4e-130">Zlokalizuj hello usługi sieci web, a następnie sprawdź jej identyfikatora usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="83a4e-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="83a4e-131">Witaj Nazwa grupy zasobów hello jest czwartym elementem hello w identyfikatorze hello zaraz po hello *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="83a4e-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="83a4e-132">W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="83a4e-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="83a4e-133">Alternatywnie toodetermine hello Nazwa grupy zasobów z istniejącej usługi sieci web, logowanie w portalu usługi sieci Web Microsoft Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="83a4e-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="83a4e-134">Wybierz usługę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="83a4e-134">Select hello web service.</span></span> <span data-ttu-id="83a4e-135">Nazwa grupy zasobów Hello jest hello elementu piątym powitania adres URL usługi sieci web hello, zaraz po hello *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="83a4e-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="83a4e-136">W hello poniższy przykład nazwa grupy zasobów hello jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="83a4e-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="83a4e-137">Eksportuj hello definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="83a4e-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="83a4e-138">toomodify hello definicji toohello uczony model toouse nowo hello Trenowanego modelu, należy najpierw użyć hello [AzureRmMlWebService eksportu](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport polecenia cmdlet go tooa plik w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="83a4e-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="83a4e-139">Aktualizacja hello toohello ilearner obiekt blob odwołania w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="83a4e-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="83a4e-140">Zasoby hello odszukaj hello [uczonego modelu] hello aktualizacji *uri* wartość hello *locationInfo* węzeł z identyfikatora URI obiektu hello ilearner blob hello.</span><span class="sxs-lookup"><span data-stu-id="83a4e-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="83a4e-141">Witaj identyfikatora URI jest generowany przez połączenie hello *BaseLocation* i hello *RelativeLocation* z wyników hello hello BES Wywołanie ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="83a4e-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="83a4e-142">Spowoduje to zaktualizowanie hello ścieżki tooreference hello nowe trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="83a4e-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="83a4e-143">Importowanie hello JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="83a4e-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="83a4e-144">Należy użyć hello [AzureRmMlWebService importu](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert polecenia cmdlet zmodyfikowany plik JSON do definicji usługi sieci Web, których można używać hello tooupdate definicji usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="83a4e-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="83a4e-145">Usługi sieci web hello aktualizacji z nowej definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="83a4e-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="83a4e-146">Na koniec użyj [AzureRmMlWebService aktualizacji](https://msdn.microsoft.com/library/azure/mt767922.aspx) polecenia cmdlet tooupdate hello definicji usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="83a4e-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="83a4e-147">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="83a4e-147">Summary</span></span>
<span data-ttu-id="83a4e-148">Przy użyciu poleceń cmdlet do zarządzania hello Machine Learning PowerShell, można zaktualizować hello uczonego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:</span><span class="sxs-lookup"><span data-stu-id="83a4e-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="83a4e-149">Model okresowego ponownego trenowania nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="83a4e-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="83a4e-150">Dystrybucja toocustomers modelu hello celem jest umożliwienie je ponownie ucz hello modelu, używając własnych danych.</span><span class="sxs-lookup"><span data-stu-id="83a4e-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

