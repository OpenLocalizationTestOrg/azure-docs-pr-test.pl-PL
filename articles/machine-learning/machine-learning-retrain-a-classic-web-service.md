---
title: "Usługi sieci web klasycznego retrain | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak programowo retrain modelu i usługi sieci web, aby użyć nowo uczonego modelu w usłudze Azure Machine Learning aktualizacji."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="5886c-103">Ponowne szkolenie klasycznej usługi internetowej</span><span class="sxs-lookup"><span data-stu-id="5886c-103">Retrain a Classic web service</span></span>
<span data-ttu-id="5886c-104">Usługa sieci Web predykcyjnych, wdrożone jest domyślnego punktu końcowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="5886c-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="5886c-105">Domyślne punkty końcowe są utrzymywane w synchronizacji z oryginalnego szkolenia i oceniania eksperymentów, a w związku z tym nie można zamienić trenowanego modelu dla domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5886c-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="5886c-106">Aby ponownie ucz usługi sieci web, należy dodać nowy punkt końcowy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="5886c-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5886c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5886c-107">Prerequisites</span></span>
<span data-ttu-id="5886c-108">Musi mieć skonfigurowaniu eksperyment uczenia i eksperyment predykcyjny jak pokazano w [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="5886c-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5886c-109">Należy wdrożyć eksperyment predykcyjny jako usługę sieci web uczenia maszynowego klasycznego.</span><span class="sxs-lookup"><span data-stu-id="5886c-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="5886c-110">Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5886c-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="5886c-111">Dodaj nowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="5886c-111">Add a new Endpoint</span></span>
<span data-ttu-id="5886c-112">Predykcyjnej wdrożonej usługi sieci Web zawiera domyślne oceniania punktu końcowego, który jest synchronizowana z oryginalnym szkolenia i oceniania eksperymenty trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="5886c-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="5886c-113">Aby zaktualizować usługi sieci web do nowego trenowanego modelu, należy utworzyć nowy punkt końcowy oceniania.</span><span class="sxs-lookup"><span data-stu-id="5886c-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="5886c-114">Aby utworzyć nowy punkt końcowy oceniania, od predykcyjnej usługi sieci Web, która może zostać zaktualizowana przy użyciu trenowanego modelu:</span><span class="sxs-lookup"><span data-stu-id="5886c-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="5886c-115">Upewnij się, że punkt końcowy jest dodawany do predykcyjnej usługi sieci Web nie usługę sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="5886c-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="5886c-116">Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwie usługi WWW, na liście.</span><span class="sxs-lookup"><span data-stu-id="5886c-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="5886c-117">Predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".</span><span class="sxs-lookup"><span data-stu-id="5886c-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="5886c-118">Istnieją trzy sposoby, w których można dodać nowy punkt końcowy usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="5886c-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="5886c-119">Programistycznie</span><span class="sxs-lookup"><span data-stu-id="5886c-119">Programmatically</span></span>
2. <span data-ttu-id="5886c-120">Za pomocą portalu usługi sieci Web platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5886c-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="5886c-121">Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5886c-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="5886c-122">Programowe Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="5886c-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="5886c-123">Możesz dodać oceniania punktów końcowych przy użyciu przykładowy kod podany w tym [repozytorium github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="5886c-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="5886c-124">Dodawanie punktu końcowego za pomocą portalu usługi sieci Web platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5886c-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="5886c-125">W usłudze Machine Learning Studio w kolumnie nawigacji po lewej stronie kliknij usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5886c-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="5886c-126">W dolnej części pulpitu nawigacyjnego usługi sieci web, kliknij przycisk **Zarządzaj punktami końcowymi Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="5886c-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="5886c-127">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5886c-127">Click **Add**.</span></span>
4. <span data-ttu-id="5886c-128">Wpisz nazwę i opis dla nowego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5886c-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="5886c-129">Wybierz poziom rejestrowania i czy jest włączone przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="5886c-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="5886c-130">Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi sieci web uczenie maszynowe](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="5886c-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="5886c-131">Użyj klasycznego portalu Azure, aby dodać punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="5886c-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="5886c-132">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5886c-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5886c-133">W menu po lewej stronie kliknij **uczenia maszynowego**.</span><span class="sxs-lookup"><span data-stu-id="5886c-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="5886c-134">W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="5886c-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="5886c-135">W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .</span><span class="sxs-lookup"><span data-stu-id="5886c-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="5886c-136">W dolnej części strony kliknij **Dodawanie punktu końcowego**.</span><span class="sxs-lookup"><span data-stu-id="5886c-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="5886c-137">Aby uzyskać więcej informacji dotyczących dodawania punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5886c-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="5886c-138">Zaktualizuj Uczonego modelu dodano punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="5886c-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="5886c-139">Aby ukończyć proces ponownego trenowania, należy zaktualizować trenowanego modelu nowy punkt końcowy, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="5886c-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="5886c-140">Jeśli dodano nowy punkt końcowy, przy użyciu klasycznego portalu Azure, możesz kliknąć nazwę nowego punktu końcowego w portalu, a następnie **operacja UpdateResource** łącze, aby uzyskać adres URL, musisz zaktualizować punktu końcowego modelu.</span><span class="sxs-lookup"><span data-stu-id="5886c-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="5886c-141">Jeśli dodano punkt końcowy, za pomocą przykładowy kod, w tym lokalizacji identyfikowana na podstawie adresu URL pomocy *HelpLocationURL* wartość w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5886c-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="5886c-142">Aby pobrać ścieżki adresu URL:</span><span class="sxs-lookup"><span data-stu-id="5886c-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="5886c-143">Skopiuj i wklej adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="5886c-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="5886c-144">Kliknij łącze aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="5886c-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="5886c-145">Skopiuj adres URL żądania PATCH POST.</span><span class="sxs-lookup"><span data-stu-id="5886c-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="5886c-146">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5886c-146">For example:</span></span>
   
     <span data-ttu-id="5886c-147">ADRES URL POPRAWKI: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2</span><span class="sxs-lookup"><span data-stu-id="5886c-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="5886c-148">Można teraz używać trenowanego modelu można zaktualizować punktu końcowego oceniania utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5886c-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="5886c-149">Następujący przykładowy kod przedstawia sposób użycia *BaseLocation*, *RelativeLocation*, *SasBlobToken*i poprawka adres URL, aby zaktualizować punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5886c-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="5886c-150">*ApiKey* i *endpointUrl* dla wywołania można uzyskać z poziomu pulpitu nawigacyjnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5886c-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="5886c-151">Wartość *nazwa* parametru w *zasobów* powinna odpowiadać nazwie zasobu zapisane Uczonego modelu w eksperyment predykcyjny.</span><span class="sxs-lookup"><span data-stu-id="5886c-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="5886c-152">Aby uzyskać nazwę zasobu:</span><span class="sxs-lookup"><span data-stu-id="5886c-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="5886c-153">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5886c-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5886c-154">W menu po lewej stronie kliknij **uczenia maszynowego**.</span><span class="sxs-lookup"><span data-stu-id="5886c-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="5886c-155">W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="5886c-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="5886c-156">W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .</span><span class="sxs-lookup"><span data-stu-id="5886c-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="5886c-157">Kliknij nowy punkt końcowy, dodane.</span><span class="sxs-lookup"><span data-stu-id="5886c-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="5886c-158">Na pulpicie nawigacyjnym punktu końcowego kliknij **aktualizacji zasobów**.</span><span class="sxs-lookup"><span data-stu-id="5886c-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="5886c-159">Na stronie dokumentacji interfejsu API aktualizacji zasobów dla usługi sieci web można znaleźć **Nazwa zasobu** w obszarze **nadaje się do aktualizacji zasobów**.</span><span class="sxs-lookup"><span data-stu-id="5886c-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="5886c-160">Jeśli token sygnatury dostępu Współdzielonego wygasa przed zakończeniem aktualizowanie punktu końcowego, należy wykonać pobierania identyfikatorem zadania do uzyskania tokenu świeże.</span><span class="sxs-lookup"><span data-stu-id="5886c-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="5886c-161">Jeśli kod został uruchomiony pomyślnie, nowy punkt końcowy należy rozpocząć używanie retrained modelu w około 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="5886c-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="5886c-162">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5886c-162">Summary</span></span>
<span data-ttu-id="5886c-163">Interfejsy API ponownego trenowania można aktualizować trenowanego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:</span><span class="sxs-lookup"><span data-stu-id="5886c-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="5886c-164">Model okresowego ponownego trenowania nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="5886c-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="5886c-165">Dystrybucja klientów przy użyciu modelu w celu umożliwienie je ponownie ucz modelu, używając własnych danych.</span><span class="sxs-lookup"><span data-stu-id="5886c-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5886c-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5886c-166">Next steps</span></span>
[<span data-ttu-id="5886c-167">Rozwiązywanie problemów z ponownego trenowania usługi sieci web klasycznego Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5886c-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

