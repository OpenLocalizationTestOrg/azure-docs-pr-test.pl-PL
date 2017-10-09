---
title: "usługi sieci web klasycznego aaaRetrain | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprogrammatically retrain modelu i aktualizacji hello web toouse hello nowo uczonego modelu usług w usłudze Azure Machine Learning."
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="32083-103">Ponowne szkolenie klasycznej usługi internetowej</span><span class="sxs-lookup"><span data-stu-id="32083-103">Retrain a Classic web service</span></span>
<span data-ttu-id="32083-104">Hello wdrożono predykcyjnej usługi sieci Web jest domyślnym hello punktu końcowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="32083-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="32083-105">Domyślne punkty końcowe są synchronizowana z hello oryginalnego celów szkoleniowych i oceniania eksperymentów, a w związku z tym hello uczonego modelu do hello domyślny punkt końcowy nie można zastąpić.</span><span class="sxs-lookup"><span data-stu-id="32083-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="32083-106">Usługa sieci web hello tooretrain, należy dodać nową usługę sieci web toohello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="32083-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="32083-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="32083-107">Prerequisites</span></span>
<span data-ttu-id="32083-108">Musi mieć skonfigurowaniu eksperyment uczenia i eksperyment predykcyjny jak pokazano w [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="32083-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="32083-109">eksperyment predykcyjny Hello należy wdrożyć jako usługę sieci web uczenia maszynowego klasycznego.</span><span class="sxs-lookup"><span data-stu-id="32083-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="32083-110">Aby uzyskać dodatkowe informacje na temat usługi sieci web wdrażanie, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="32083-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="32083-111">Dodaj nowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="32083-111">Add a new Endpoint</span></span>
<span data-ttu-id="32083-112">Witaj predykcyjnej usługi sieci Web, która została wdrożona zawiera domyślne oceniania punktu końcowego, który jest synchronizowana z hello oryginalnego szkolenia i oceniania eksperymenty trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="32083-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="32083-113">tooupdate Twojego toowith nowy nauczony model usługi sieci web należy utworzyć nowy punkt końcowy oceniania.</span><span class="sxs-lookup"><span data-stu-id="32083-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="32083-114">toocreate nowy oceniania punkt końcowy, na powitania predykcyjnej usługi sieci Web, który może zostać zaktualizowana przy użyciu hello uczonego modelu:</span><span class="sxs-lookup"><span data-stu-id="32083-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="32083-115">Upewnij się, że w przypadku dodawania hello toohello punkt końcowy usługi sieci Web predykcyjnych, hello usługi sieci Web szkolenia.</span><span class="sxs-lookup"><span data-stu-id="32083-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="32083-116">Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwie usługi WWW, na liście.</span><span class="sxs-lookup"><span data-stu-id="32083-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="32083-117">Hello predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".</span><span class="sxs-lookup"><span data-stu-id="32083-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="32083-118">Istnieją trzy sposoby, w których można dodać nową usługę sieci web tooa punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="32083-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="32083-119">Programistycznie</span><span class="sxs-lookup"><span data-stu-id="32083-119">Programmatically</span></span>
2. <span data-ttu-id="32083-120">Za pomocą portalu usługi sieci Web platformy Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="32083-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="32083-121">Witaj Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="32083-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="32083-122">Programowe Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="32083-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="32083-123">Możesz dodać oceniania punktów końcowych przy użyciu hello przykładowy kod podany w tym [repozytorium github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="32083-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="32083-124">Użyj portalu tooadd usługi sieci Web platformy Microsoft Azure hello punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="32083-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="32083-125">W usłudze Machine Learning Studio kolumny nawigacji po lewej stronie powitania kliknij usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="32083-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="32083-126">U dołu hello hello pulpit nawigacyjny z usługi sieci web, kliknij przycisk **Zarządzaj punktami końcowymi Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="32083-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="32083-127">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="32083-127">Click **Add**.</span></span>
4. <span data-ttu-id="32083-128">Wpisz nazwę i opis dla nowego punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="32083-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="32083-129">Wybierz poziom rejestrowania hello i czy jest włączone przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="32083-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="32083-130">Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi sieci web uczenie maszynowe](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="32083-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="32083-131">Witaj Użyj klasycznego portalu Azure tooadd punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="32083-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="32083-132">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="32083-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="32083-133">W menu po lewej stronie powitania kliknij **uczenia maszynowego**.</span><span class="sxs-lookup"><span data-stu-id="32083-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="32083-134">W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="32083-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="32083-135">W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .</span><span class="sxs-lookup"><span data-stu-id="32083-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="32083-136">U dołu hello hello strony, kliknij przycisk **Dodawanie punktu końcowego**.</span><span class="sxs-lookup"><span data-stu-id="32083-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="32083-137">Aby uzyskać więcej informacji dotyczących dodawania punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="32083-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="32083-138">Aktualizacja hello dodać punktu końcowego Uczonego modelu</span><span class="sxs-lookup"><span data-stu-id="32083-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="32083-139">proces ponownego trenowania hello toocomplete, należy zaktualizować hello nauczony model hello nowy punkt końcowy, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="32083-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="32083-140">Jeśli dodano nowy punkt końcowy hello przy użyciu klasycznego portalu Azure hello, możesz kliknąć nazwę hello nowego punktu końcowego w portalu hello, a następnie hello **operacja UpdateResource** adres URL hello tooget będzie potrzebny modelu tooupdate hello punktu końcowego łącza.</span><span class="sxs-lookup"><span data-stu-id="32083-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="32083-141">Jeśli dodano hello punktu końcowego za pomocą hello przykładowy kod, w tym lokalizacji adres URL pomocy hello identyfikowane przez hello *HelpLocationURL* wartość w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="32083-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="32083-142">adres URL ścieżki hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="32083-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="32083-143">Skopiuj i wklej adres URL hello w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="32083-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="32083-144">Kliknij łącze aktualizacji zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="32083-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="32083-145">Skopiuj hello adresu URL przesyłania żądania PATCH hello.</span><span class="sxs-lookup"><span data-stu-id="32083-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="32083-146">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="32083-146">For example:</span></span>
   
     <span data-ttu-id="32083-147">ADRES URL POPRAWKI: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2</span><span class="sxs-lookup"><span data-stu-id="32083-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="32083-148">Można teraz używać hello tooupdate uczonego modelu hello oceniania punktu końcowego, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="32083-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="32083-149">Witaj następującego przykładowego kodu pokazuje sposób toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*i punktu końcowego hello tooupdate poprawka adresu URL.</span><span class="sxs-lookup"><span data-stu-id="32083-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="32083-150">Witaj *apiKey* i hello *endpointUrl* dla wywołania hello można uzyskać z poziomu pulpitu nawigacyjnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="32083-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="32083-151">Witaj wartość hello *nazwa* parametru w *zasobów* ma hello dopasowania nazwy zasobu hello zapisany Uczonego modelu w eksperyment predykcyjny hello.</span><span class="sxs-lookup"><span data-stu-id="32083-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="32083-152">Witaj tooget Nazwa zasobu:</span><span class="sxs-lookup"><span data-stu-id="32083-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="32083-153">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="32083-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="32083-154">W menu po lewej stronie powitania kliknij **uczenia maszynowego**.</span><span class="sxs-lookup"><span data-stu-id="32083-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="32083-155">W obszarze nazwy, kliknij obszar roboczy, a następnie kliknij **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="32083-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="32083-156">W obszarze nazwy, kliknij przycisk **modelu spisu [exp predykcyjnych.]** .</span><span class="sxs-lookup"><span data-stu-id="32083-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="32083-157">Kliknij przycisk hello nowy punkt końcowy, dodane.</span><span class="sxs-lookup"><span data-stu-id="32083-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="32083-158">Na powitania punktu końcowego pulpitu nawigacyjnego, kliknij przycisk **aktualizacji zasobów**.</span><span class="sxs-lookup"><span data-stu-id="32083-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="32083-159">Na stronie dokumentacji interfejsu API zasobów aktualizacji hello hello usługi sieci web, można znaleźć hello **Nazwa zasobu** w obszarze **nadaje się do aktualizacji zasobów**.</span><span class="sxs-lookup"><span data-stu-id="32083-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="32083-160">Jeśli token sygnatury dostępu Współdzielonego wygasa przed zakończeniem Trwa aktualizowanie punktu końcowego hello, należy wykonać GET z hello tooobtain zadania o identyfikatorze nowego tokenu.</span><span class="sxs-lookup"><span data-stu-id="32083-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="32083-161">Gdy kod hello został uruchomiony pomyślnie, hello nowy punkt końcowy należy zacząć przy użyciu modelu hello retrained około 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="32083-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="32083-162">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="32083-162">Summary</span></span>
<span data-ttu-id="32083-163">Przy użyciu hello ponownego trenowania interfejsów API, można zaktualizować hello uczonego modelu predykcyjnego usługi sieci Web, włączanie scenariuszy, takich jak:</span><span class="sxs-lookup"><span data-stu-id="32083-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="32083-164">Model okresowego ponownego trenowania nowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="32083-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="32083-165">Dystrybucja toocustomers modelu hello celem jest umożliwienie je ponownie ucz hello modelu, używając własnych danych.</span><span class="sxs-lookup"><span data-stu-id="32083-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32083-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32083-166">Next steps</span></span>
[<span data-ttu-id="32083-167">Rozwiązywanie problemów z hello ponownego trenowania usługi sieci web klasycznego Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32083-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

