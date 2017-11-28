---
title: "aaaCreate wielu modeli z doświadczenia | Dokumentacja firmy Microsoft"
description: "Użyj programu PowerShell toocreate wielu modeli uczenia maszynowego i sieci web punktów końcowych usługi z hello samego algorytmu, ale szkolenia różnych zestawów danych."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="e3dd3-103">Tworzenie wielu modeli usługi Machine Learning i punktów końcowych usługi sieci Web na podstawie jednego eksperymentu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3dd3-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="e3dd3-104">W tym miejscu jest to powszechny problem learning maszyny: mają wiele modeli, które mają hello toocreate tego samego przepływu pracy szkolenia i użyj hello samego algorytmu, ale ma szkolenia różnych zestawów danych, jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="e3dd3-105">W tym artykule opisano sposób toodo to na dużą skalę w usłudze Azure Machine Learning Studio za pomocą tylko jednego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="e3dd3-106">Załóżmy na przykład, że właścicielem firmy franchisingowe roweru globalnego dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="e3dd3-107">Ma toobuild zażąda wynajem hello toopredict modelu regresji na podstawie historycznych danych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="e3dd3-108">Masz 1000 lokalizacje dzierżawa między Witaj świecie i zostały zebrane zestawu danych dla każdej lokalizacji, która zawiera ważne funkcje, takie jak dzień, godzina pogodą i ruchu, który jest tooeach określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="e3dd3-109">Można uczenia modelu raz we wszystkich lokalizacjach za pomocą scalonych wersji wszystkich hello zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="e3dd3-110">Jednak ponieważ każdy z lokalizacji ma unikatowy środowiska, lepszym rozwiązaniem może być tootrain modelu regresji oddzielnie dla każdej lokalizacji za pomocą hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="e3dd3-111">W ten sposób każdy uczonego modelu może potrwać do konta hello magazynu różne rozmiary, woluminu, geography, wypełniania, ruch roweru przyjaznego środowiska, *itp.*.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="e3dd3-112">Może to być hello najlepszym rozwiązaniem, ale nie chcesz, aby z każdą z nich reprezentujący unikatową lokalizację toocreate 1000 szkolenia eksperymentów w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="e3dd3-113">Oprócz jest utrudnione zadań, należy również wydaje się bardzo mało wydajne, ponieważ wszystkie hello tego samego składników z wyjątkiem hello szkolenia dataset musi każdego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="e3dd3-114">Na szczęście, firma Microsoft może to zrobić przy użyciu hello [ponownego trenowania interfejsu API uczenia maszynowego Azure](machine-learning-retrain-models-programmatically.md) i automatyzowanie zadań hello z [programu PowerShell usługi Azure Machine Learning](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="e3dd3-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e3dd3-115">toomake naszej próbki szybsze, firma Microsoft będzie zmniejszyć hello liczba lokalizacji z too10 1000.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="e3dd3-116">Ale hello tego samego zasadami i procedurami zastosować too1, lokalizacje 000.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="e3dd3-117">Hello jedyna różnica polega na tym, że jeśli tootrain z 1000 zestawów danych prawdopodobnie potrzebna będzie toothink uruchomionych hello następujące skrypty programu PowerShell równolegle.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="e3dd3-118">Jak toodo, która wykracza poza zakres tego artykułu, ale hello można znaleźć przykłady PowerShell wielowątkowości na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="e3dd3-119">Konfigurowanie eksperyment uczenia hello</span><span class="sxs-lookup"><span data-stu-id="e3dd3-119">Set up hello training experiment</span></span>
<span data-ttu-id="e3dd3-120">Zamierzamy toouse przykład [eksperyment uczenia](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) który mamy już utworzone w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="e3dd3-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e3dd3-121">Otwórz tego eksperymentu w Twojej [Azure Machine Learning Studio](https://studio.azureml.net) obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="e3dd3-122">W kolejności toofollow wraz z tego przykładu możesz toouse standardowe obszaru roboczego, a nie wolnego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="e3dd3-123">Możemy utworzyć jeden punkt końcowy dla każdego klienta — dla wszystkich punktów końcowych 10 - i standardowe obszaru roboczego będzie wymagają od wolnego obszaru roboczego jest ograniczona too3 punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="e3dd3-124">Jeśli masz tylko obszar roboczy wolne, po prostu Zmodyfikuj skrypty hello poniżej tooallow tylko 3 lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="e3dd3-125">używa eksperymentu Hello **i zaimportuj dane** modułu tooimport hello szkolenia w zestawie danych *customer001.csv* z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="e3dd3-126">Załóżmy, że firma Microsoft zbierane szkolenia zestawów danych z wszystkich lokalizacji wynajem roweru i zapisał je w hello sam lokalizacji magazynu obiektów blob z nazwami plików od *rentalloc001.csv* za*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="e3dd3-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="e3dd3-128">Należy pamiętać, że **wyjście usługi sieci Web** moduł został dodany toohello **Train Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="e3dd3-129">Po wdrożeniu tego eksperymentu jako usługę sieci web punktu końcowego hello skojarzone z tym produktem wyjściowym zwróci hello uczonego modelu w formacie hello pliku .ilearner.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="e3dd3-130">Należy również zauważyć, że skonfigurowanie parametr usługi sieci web dla adresu URL hello tego hello **i zaimportuj dane** korzysta z modułu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="e3dd3-131">Dzięki temu nam toouse hello parametru toospecify szkolenia poszczególnych zestawów danych tootrain hello modelu dla każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="e3dd3-132">Istnieją inne sposoby firma Microsoft może mieć zostało to zrobione, takich jak za pomocą zapytania SQL z danych tooget parametr usługi sieci web z bazy danych SQL Azure lub po prostu **wprowadzania usługi sieci Web** usługi sieci web toopass modułu w toohello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="e3dd3-134">Teraz umożliwia uruchamianie tego eksperymentu uczenia przy użyciu wartości domyślnej hello *rental001.csv* jako hello zestawu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="e3dd3-135">Podczas przeglądania danych wyjściowych hello hello **Evaluate** modułu (kliknij hello wyjściowy i wybierz **wizualizacja**), zostanie wyświetlony, uzyskujemy zadowalający wydajność *AUC* = 0,91.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="e3dd3-136">W tym momencie mamy toodeploy gotowe usługi sieci web poza tym eksperyment uczenia.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="e3dd3-137">Wdrażanie hello szkolenia i oceniania usług sieci web</span><span class="sxs-lookup"><span data-stu-id="e3dd3-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="e3dd3-138">toodeploy hello szkolenia usługi sieci web, kliknij przycisk hello **ustawić usługę sieci Web** poniżej hello roboczego eksperymentu i wybrać **wdrażanie usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="e3dd3-139">Wywołania tej usługi sieci web "" roweru wynajem szkolenia".</span><span class="sxs-lookup"><span data-stu-id="e3dd3-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="e3dd3-140">Teraz potrzebujemy toodeploy hello oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="e3dd3-141">toodo, możemy kliknąć **ustawić usługę sieci Web** poniżej hello obszar roboczy i wybierz **predykcyjnej usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="e3dd3-142">Spowoduje to utworzenie oceniania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="e3dd3-143">Potrzebujemy toomake kilka toomake niewielkich dostosowań pracy jako usługi sieci web, takie jak usunięcie kolumny etykiety hello "cnt" z hello dane wejściowe i ograniczanie identyfikator wystąpienia hello hello dane wyjściowe tooonly i hello odpowiadającego przewidzieć wartość.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="e3dd3-144">toosave, który działa, możesz po prostu otworzyć hello [eksperyment predykcyjny](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) w hello galerii, który jest już przygotowane.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="e3dd3-145">Usługa sieci web hello toodeploy uruchomić eksperyment predykcyjny hello, następnie kliknij przycisk hello **wdrażanie usługi sieci Web** znajdujący się poniżej hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="e3dd3-146">Nazwa hello oceniania usługi sieci web "Roweru wynajem oceniania" ".</span><span class="sxs-lookup"><span data-stu-id="e3dd3-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="e3dd3-147">Tworzenie punktów końcowych usługi sieci web identyczne 10 przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3dd3-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="e3dd3-148">Ta usługa sieci web jest dostarczany z domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="e3dd3-149">Ale nie jesteśmy jako zainteresowana hello domyślnego punktu końcowego, ponieważ nie można zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="e3dd3-150">Co należy toodo jest toocreate 10 dodatkowych punktów końcowych, po jednej dla każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="e3dd3-151">Firma Microsoft to zrobić przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="e3dd3-152">Po pierwsze skonfigurowanie naszego środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e3dd3-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="e3dd3-153">Następnie uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="e3dd3-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="e3dd3-154">Teraz utworzona 10 punktów końcowych i wszystkie zawierają hello ćwiczenie uczonego modelu w tym samym *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="e3dd3-155">Można je wyświetlić w portalu zarządzania Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-155">You can view them in hello Azure Management Portal.</span></span>

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="e3dd3-157">Zaktualizuj hello punkty końcowe toouse oddzielne szkolenia danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3dd3-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="e3dd3-158">Witaj następnym krokiem jest punkty końcowe hello tooupdate z modelami jednoznacznie ćwiczenie poszczególnych danych każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="e3dd3-159">Jednak najpierw musimy tooproduce tych modeli z hello **roweru wynajem szkolenia** usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="e3dd3-160">Przejdź wstecz toohello **roweru wynajem szkolenia** usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="e3dd3-161">Potrzebujemy toocall punktu końcowego usługi BES 10 razy z 10 szkolenia różnych zestawów danych w kolejności tooproduce 10 różne modele.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="e3dd3-162">Użyjemy hello **InovkeAmlWebServiceBESEndpoint** toodo polecenia cmdlet programu PowerShell to.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="e3dd3-163">Należy również tooprovide poświadczenia dla konta magazynu obiektów blob do `$configContent`, to znaczy, w polach hello `AccountName`, `AccountKey` i `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="e3dd3-164">Witaj `AccountName` może być jedną z nazwy konta, jak pokazano w hello **klasycznego portalu zarządzania Azure** (*magazynu* kartę).</span><span class="sxs-lookup"><span data-stu-id="e3dd3-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="e3dd3-165">Po kliknięciu na koncie magazynu, jego `AccountKey` można znaleźć, naciskając klawisz hello **Zarządzaj kluczami dostępu** u dołu hello i kopiowanie hello *podstawowy klucz dostępu*.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="e3dd3-166">Witaj `RelativeLocation` jest hello ścieżki względnej tooyour magazynu przechowywania nowego modelu.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="e3dd3-167">Na przykład ścieżka hello `hai/retrain/bike_rental/` w skrypcie hello poniżej punktów tooa kontener o nazwie `hai`, i `/retrain/bike_rental/` znajdują się podfoldery.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="e3dd3-168">Obecnie nie można utworzyć podfoldery za pośrednictwem portalu hello interfejsu użytkownika, ale istnieją [kilka eksploratory usługi Storage Azure](../storage/common/storage-explorers.md) umożliwiającą toodo tak.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="e3dd3-169">Zalecane jest utworzenie nowego kontenera w hello toostore Twojego magazynu nowe modele przeszkolone (.ilearner pliki) w następujący sposób: na stronie magazynu, kliknij hello **Dodaj** znajdujący się u dołu hello i nadaj mu nazwę `retrain`.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="e3dd3-170">Podsumowując, skrypt toohello niezbędne zmiany hello poniżej odnoszą się zbyt`AccountName`, `AccountKey` i `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="e3dd3-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="e3dd3-171">punkt końcowy usługi BES Hello jest hello obsługiwany tylko tryb dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="e3dd3-172">Rekordy zasobów nie może służyć do tworzenia modeli przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="e3dd3-173">Jak pokazano powyżej, zamiast tworzenia 10 różnych BES zadania konfiguracji json plików, firma Microsoft dynamicznie zamiast tego utwórz Ciąg konfiguracyjny hello i umieść go toohello *jobConfigString* parametru hello  **InvokeAmlWebServceBESEndpoint** polecenia cmdlet, ponieważ nie istnieje naprawdę tookeep nie potrzeby kopiowania na dysku.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="e3dd3-174">Jeśli wszystko odbędzie się poprawnie, po chwili powinno być widoczne 10 plików .ilearner, z *model001.ilearner* za*model010.ilearner*, na Twoim koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="e3dd3-175">Teraz jest gotowy tooupdate naszych 10 oceniania sieci web punkty końcowe usługi przy użyciu tych modeli przy użyciu hello **AmlWebServiceEndpoint poprawki** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="e3dd3-176">Ponownie należy pamiętać, że firma Microsoft tylko poprawki z systemem innym niż domyślne punkty końcowe hello, utworzonego programowo wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="e3dd3-177">To powinno być ono uruchomione stosunkowo szybko.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-177">This should run fairly quickly.</span></span> <span data-ttu-id="e3dd3-178">Po zakończeniu wykonywania hello, firma Microsoft będzie pomyślnie utworzono 10 punktów końcowych usługi sieci web predykcyjnych, każda z nich zawiera uczonego modelu jednoznacznie ćwiczenie hello zestawu danych tooa określonych wynajem lokalizacji, z eksperyment pojedynczego szkolenia.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="e3dd3-179">tooverify, możesz spróbować wywoływania tych punktów końcowych przy użyciu hello **InvokeAmlWebServiceRRSEndpoint** polecenia cmdlet, zapewnienie im z hello same dane wejściowe i wyniki prognozowania różnych toosee należy oczekiwać od modele hello są uczone z szkolenia różnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="e3dd3-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="e3dd3-180">Pełna skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3dd3-180">Full PowerShell script</span></span>
<span data-ttu-id="e3dd3-181">Oto lista hello hello pełny kod źródłowy:</span><span class="sxs-lookup"><span data-stu-id="e3dd3-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
