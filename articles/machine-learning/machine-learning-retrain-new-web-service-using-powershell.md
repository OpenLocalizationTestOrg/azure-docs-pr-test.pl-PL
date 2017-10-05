---
title: "Ponownie ucz nowej usługi Azure Machine Learning usługi sieci web przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak programowo retrain modelu i usługi sieci web do korzystania z nowo uczonego modelu w usłudze Azure Machine Learning przy użyciu poleceń cmdlet programu PowerShell do zarządzania Machine Learning aktualizacji."
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
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="4126f-103">Ponownie ucz usługi sieci web na podstawie nowego Menedżera zasobów za pomocą poleceń cmdlet programu PowerShell do zarządzania Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4126f-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="4126f-104">Gdy retrain nową usługę sieci web, należy zaktualizować definicji usługi predykcyjnej sieci web do odwołania do nowego uczonego modelu.</span><span class="sxs-lookup"><span data-stu-id="4126f-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4126f-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4126f-105">Prerequisites</span></span>
<span data-ttu-id="4126f-106">Należy zdefiniować eksperyment uczenia i eksperyment predykcyjny pokazane [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="4126f-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4126f-107">Eksperyment predykcyjny musi być wdrożony jako maszyna usługi Azure Resource Manager (nowy) na podstawie szkoleniowe dotyczące usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="4126f-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="4126f-108">Aby wdrożyć nową usługę sieci web musi masz wystarczające uprawnienia do subskrypcji, do którego należy wdrożyć usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="4126f-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="4126f-109">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="4126f-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="4126f-110">Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4126f-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="4126f-111">Ten proces wymaga zainstalowanego polecenia cmdlet programu Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4126f-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="4126f-112">Instalowanie poleceń cmdlet usługi Machine Learning informacji, zobacz [polecenia cmdlet usługi Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="4126f-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="4126f-113">Z ponownego trenowania danych wyjściowych, należy skopiować następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="4126f-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="4126f-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="4126f-114">BaseLocation</span></span>
* <span data-ttu-id="4126f-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="4126f-115">RelativeLocation</span></span>

<span data-ttu-id="4126f-116">Dostępne są następujące czynności, które należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="4126f-116">The steps you take are:</span></span>

1. <span data-ttu-id="4126f-117">Zaloguj się do swojego konta usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4126f-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="4126f-118">Pobierz definicję usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="4126f-118">Get the web service definition</span></span>
3. <span data-ttu-id="4126f-119">Eksportowanie definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="4126f-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="4126f-120">Aktualizacja odwołania do obiektu blob ilearner w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4126f-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="4126f-121">Zaimportuj dane JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4126f-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="4126f-122">Aktualizacja usługi sieci web z nowego definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4126f-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="4126f-123">Zaloguj się do konta usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4126f-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="4126f-124">Musisz najpierw zalogować się do konta z platformy Azure w ramach przy użyciu środowiska PowerShell [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4126f-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="4126f-125">Pobierz definicję usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4126f-125">Get the Web Service Definition</span></span>
<span data-ttu-id="4126f-126">Następnie Pobierz usługę sieci Web przez wywołanie metody [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4126f-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="4126f-127">Definicja usługi sieci Web jest reprezentacji wewnętrznej trenowanego modelu usługi sieci web, a nie można bezpośrednio modyfikować.</span><span class="sxs-lookup"><span data-stu-id="4126f-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="4126f-128">Upewnij się, że są pobierania definicji usługi sieci Web dla predykcyjnej eksperymentu, a nie eksperyment uczenia.</span><span class="sxs-lookup"><span data-stu-id="4126f-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="4126f-129">Aby określić nazwę grupy zasobów z istniejącej usługi sieci web, uruchom polecenie cmdlet Get-AzureRmMlWebService bez żadnych parametrów do wyświetlenia w ramach subskrypcji usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="4126f-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="4126f-130">Znajdź usługę sieci web, a następnie sprawdź jej identyfikatora usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="4126f-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="4126f-131">Nazwa grupy zasobów jest czwartym elementem w identyfikatorze, zaraz po *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="4126f-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="4126f-132">W poniższym przykładzie nazwa grupy zasobów jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="4126f-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="4126f-133">Alternatywnie można określić nazwę grupy zasobów istniejącej usługi sieci web, zaloguj się do portalu usługi sieci Web Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4126f-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="4126f-134">Wybierz usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="4126f-134">Select the web service.</span></span> <span data-ttu-id="4126f-135">Nazwa grupy zasobów jest piąty elementu adres URL usługi sieci web zaraz po *resourceGroups* elementu.</span><span class="sxs-lookup"><span data-stu-id="4126f-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="4126f-136">W poniższym przykładzie nazwa grupy zasobów jest domyślna-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="4126f-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="4126f-137">Eksportowanie definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="4126f-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="4126f-138">Aby zmodyfikować definicję do uczonego modelu w celu wykorzystania nowo Trenowanego modelu, należy najpierw użyć [AzureRmMlWebService eksportu](https://msdn.microsoft.com/library/azure/mt767935.aspx) polecenia cmdlet można wyeksportować go do pliku formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="4126f-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="4126f-139">Aktualizacja odwołania do obiektu blob ilearner w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4126f-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="4126f-140">Zasoby, odszukaj [nauczony model], zaktualizuj *uri* wartość w *locationInfo* węzła o identyfikatorze URI obiektu ilearner blob.</span><span class="sxs-lookup"><span data-stu-id="4126f-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="4126f-141">Identyfikator URI jest generowany przez łączenie *BaseLocation* i *RelativeLocation* z danych wyjściowych BES ponownego trenowania wywołania.</span><span class="sxs-lookup"><span data-stu-id="4126f-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="4126f-142">Spowoduje to zaktualizowanie ścieżkę do odwołania do nowego trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="4126f-142">This updates the path to reference the new trained model.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="4126f-143">Zaimportuj dane JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4126f-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="4126f-144">Należy użyć [AzureRmMlWebService importu](https://msdn.microsoft.com/library/azure/mt767925.aspx) polecenia cmdlet, aby przekonwertować zmodyfikowany plik JSON do definicji usługi sieci Web, który służy do aktualizacji definicji usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4126f-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="4126f-145">Aktualizacja usługi sieci web z nowego definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4126f-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="4126f-146">Na koniec użyj [AzureRmMlWebService aktualizacji](https://msdn.microsoft.com/library/azure/mt767922.aspx) polecenia cmdlet można zaktualizować definicji usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4126f-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="4126f-147">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4126f-147">Summary</span></span>
<span data-ttu-id="4126f-148">Polecenia cmdlet programu PowerShell Learning maszyny do zarządzania można aktualizować trenowanego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:</span><span class="sxs-lookup"><span data-stu-id="4126f-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="4126f-149">Model okresowego ponownego trenowania nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="4126f-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="4126f-150">Dystrybucja klientów przy użyciu modelu w celu umożliwienie je ponownie ucz modelu, używając własnych danych.</span><span class="sxs-lookup"><span data-stu-id="4126f-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

