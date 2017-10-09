---
title: "aaaConsume usługi sieci web uczenie maszynowe za pomocą szablonu aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Szablon aplikacji sieci web w portalu Azure Marketplace tooconsume usługi sieci web predykcyjnej w usłudze Azure Machine Learning."
keywords: "Usługa sieci Web, operationalization, interfejsu API REST, uczenia maszynowego"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="21c59-104">Korzystanie z usługi sieci Web Azure Machine Learning za pomocą szablonu aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="21c59-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="21c59-105">Po opracowany model predykcyjny i wdrożyć go jako usługi sieci web platformy Azure przy użyciu usługi Machine Learning Studio lub za pomocą narzędzi, takich jak R lub Python, są dostępne hello operationalized modelu, używając interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="21c59-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="21c59-106">Istnieją różne sposoby tooconsume hello dostępu i interfejsu API REST hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="21c59-107">Na przykład można napisać aplikację w języku C#, R lub Python za pomocą hello przykładowy kod wygenerowany przez po wdrożeniu usługi sieci web hello (dostępne w hello [usługi Machine Learning portalu](https://services.azureml.net/quickstart) lub na pulpicie nawigacyjnym usługi sieci web hello w Usługa Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="21c59-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="21c59-108">Lub użyć hello przykładowy program Microsoft Excel skoroszyt utworzony na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="21c59-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="21c59-109">Ale hello tooaccess najszybszym i Najprostszym sposobem usługi sieci web jest dostępna w hello szablonów aplikacji sieci Web hello [Azure Marketplace aplikacji sieci Web](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="21c59-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="21c59-110">Witaj szablonów aplikacji sieci Web uczenie maszyny Azure</span><span class="sxs-lookup"><span data-stu-id="21c59-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="21c59-111">Szablony aplikacji sieci web Hello dostępne w hello Azure Marketplace można utworzyć aplikacji sieci web niestandardowego, który zna usługi sieci web dane wejściowe i oczekiwanych rezultatów.</span><span class="sxs-lookup"><span data-stu-id="21c59-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="21c59-112">Toodo wystarczy podać hello aplikacji dostępu tooyour Usługa sieci web i danych, a szablon hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="21c59-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="21c59-113">Dostępne są dwa szablony:</span><span class="sxs-lookup"><span data-stu-id="21c59-113">Two templates are available:</span></span>

* [<span data-ttu-id="21c59-114">Szablon aplikacji sieci Web usługi Azure ML żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="21c59-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="21c59-115">Szablon aplikacji partii zadań Azure ML wykonywania usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="21c59-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="21c59-116">Każdy szablon tworzy przykładowej aplikacji platformy ASP.NET, za pomocą hello URI interfejsu API i klucz dla usługi sieci web i wdraża go jako tooAzure witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="21c59-117">Szablon usługi żądań i odpowiedzi (RR) Hello służy do tworzenia aplikacji sieci web, która pozwala toosend pojedynczy wiersz danych toohello sieci web usługi tooget pojedynczego wyniku.</span><span class="sxs-lookup"><span data-stu-id="21c59-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="21c59-118">Szablon usługi wykonywania wsadowego (BES) Hello tworzenia aplikacji sieci web, która pozwala toosend wiele wierszy danych tooget wiele wyników.</span><span class="sxs-lookup"><span data-stu-id="21c59-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="21c59-119">Kodowanie nie jest wymagane toouse tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="21c59-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="21c59-120">Wystarczy podać hello klucz interfejsu API i identyfikator URI, a hello szablon tworzy aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="21c59-121">klucz interfejsu API hello tooget i identyfikator URI żądania usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="21c59-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="21c59-122">W hello [Portal usługi sieci Web](https://services.azureml.net/quickstart), nowej usługi sieci web, kliknij przycisk **usług sieci Web** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="21c59-123">Lub kliknij usługi sieci web klasycznego **klasycznym usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="21c59-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="21c59-124">Kliknij usługę sieci web hello ma tooaccess.</span><span class="sxs-lookup"><span data-stu-id="21c59-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="21c59-125">Usługi sieci web klasycznego kliknij punkt końcowy hello ma tooaccess.</span><span class="sxs-lookup"><span data-stu-id="21c59-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="21c59-126">Kliknij przycisk **Consume** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="21c59-127">Kopiuj hello **głównej** lub **klucza pomocniczego** i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="21c59-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="21c59-128">Jeśli tworzysz szablon żądania i odpowiedzi usługi (RR), skopiuj hello **żądań i odpowiedzi** identyfikatora URI i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="21c59-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="21c59-129">Jeśli tworzysz szablon usługi wykonywania wsadowego (BES), skopiuj hello **żądań wsadowych** identyfikatora URI i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="21c59-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="21c59-130">Jak toouse hello szablonu żądań i odpowiedzi usługi (RR)</span><span class="sxs-lookup"><span data-stu-id="21c59-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="21c59-131">Wykonaj te kroki toouse hello rekordy zasobów szablonu sieci web app, pokazane na powitania po diagramu.</span><span class="sxs-lookup"><span data-stu-id="21c59-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Proces toouse rekordy zasobów sieci web szablonu][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="21c59-133">Przejdź toohello [portalu Azure](https://portal.azure.com), **logowania**, kliknij przycisk **nowy**, wyszukaj i wybierz **aplikacji sieci Web usługi Azure ML żądanie-odpowiedź**, następnie kliknij przycisk **Utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="21c59-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="21c59-134">Nadaj unikatową nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-134">Give your web app a unique name.</span></span> <span data-ttu-id="21c59-135">adres URL aplikacji sieci web hello Hello będzie tej nazwy, a następnie `.azurewebsites.net.` na przykład`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="21c59-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="21c59-136">Wybierz hello subskrypcji platformy Azure i usługi, w których jest uruchomiona usługa sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="21c59-137">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="21c59-137">Click **Create**.</span></span>
     
     ![Tworzenie aplikacji sieci Web][image5]

4. <span data-ttu-id="21c59-139">Po zakończeniu Azure wdrażanie aplikacji sieci web powitania kliknij hello **adres URL** na hello strony ustawień aplikacji sieci web na platformie Azure, lub wprowadź adres URL hello w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="21c59-140">Na przykład: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="21c59-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="21c59-141">Gdy hello uruchamia pierwszej aplikacji sieci web go pojawi się prośba o hello **adresu URL przesyłania interfejsu API** i **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="21c59-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="21c59-142">Wprowadź wartości hello został wcześniej zapisany (**przez identyfikator URI żądania** i **klucz interfejsu API**odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="21c59-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="21c59-143">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="21c59-143">Click **Submit**.</span></span>
     
     ![Wprowadź Post identyfikator URI i klucz interfejsu API][image6]

6. <span data-ttu-id="21c59-145">Witaj aplikacja sieci web jest wyświetlana jego **konfiguracji aplikacji sieci Web** strony z hello bieżące ustawienia usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="21c59-146">Tutaj można wprowadzić zmiany toohello ustawienia używane przez hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="21c59-147">Zmiana ustawień hello tutaj tylko zmiany ich tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="21c59-148">Ustawienia domyślne hello usługi sieci web nie go zmienić.</span><span class="sxs-lookup"><span data-stu-id="21c59-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="21c59-149">Na przykład, jeśli zmienisz hello **opis** w tym miejscu nie zmienia hello opis wyświetlany na powitania pulpit nawigacyjny usługi sieci web w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="21c59-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="21c59-150">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać zmiany**, a następnie kliknij przycisk **Przejdź tooHome strony**.</span><span class="sxs-lookup"><span data-stu-id="21c59-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="21c59-151">Z hello stronę główną, którą można wprowadzić wartości usługi sieci web tooyour toosend.</span><span class="sxs-lookup"><span data-stu-id="21c59-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="21c59-152">Kliknij przycisk **przesyłania** gdy wszystko będzie gotowe, i zostanie zwrócony wynik hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="21c59-153">Jeśli chcesz, aby tooreturn toohello **konfiguracji** pozycję Przejdź toohello `setting.aspx` strony hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="21c59-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="21c59-154">Na przykład: `http://carprediction.azurewebsites.net/setting.aspx.` klucz interfejsu API hello tooenter zostanie wyświetlony monit o będzie można ponownie — należy czy tooaccess hello strony i zaktualizuj ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="21c59-155">Można zatrzymać, ponownie uruchomić lub usunąć hello aplikacji sieci web w portalu Azure, takich jak każda inna aplikacja sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="21c59-156">Tak długo, jak działa można wybrać adres sieci web macierzystego toohello i wprowadź nowe wartości.</span><span class="sxs-lookup"><span data-stu-id="21c59-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="21c59-157">Jak toouse hello szablonu usługi wykonywania wsadowego (BES)</span><span class="sxs-lookup"><span data-stu-id="21c59-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="21c59-158">Można użyć hello BES szablonu aplikacji sieci web w hello sam sposób jako szablon RR hello, z wyjątkiem tego hello aplikacji sieci web, która jest tworzona umożliwi toosubmit wiele wierszy danych i odbierania wiele wyników.</span><span class="sxs-lookup"><span data-stu-id="21c59-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="21c59-159">Witaj wartości wejściowe dla usługi sieci web wykonywania wsadowego mogą pochodzić z magazynu Azure lub plikiem lokalnym; wyniki Hello są przechowywane w kontenerze magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="21c59-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="21c59-160">Tak, będzie konieczne toohold kontenera magazynu Azure hello wyników zwróconych przez hello aplikacji sieci web, i będzie trzeba tooget danych wejściowych gotowe.</span><span class="sxs-lookup"><span data-stu-id="21c59-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Przetwarzanie toouse BES szablonu sieci web][image2]

1. <span data-ttu-id="21c59-162">Wykonaj hello same procedury toocreate hello BES zbyt sieci web aplikacji, jak w przypadku hello rekordy zasobów szablonu, z wyjątkiem go[szablonu aplikacji sieci Web Azure ML partii wykonywania usługi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello szablonu usługi BES w portalu Azure Marketplace i kliknij przycisk **tworzenie aplikacji sieci Web** .</span><span class="sxs-lookup"><span data-stu-id="21c59-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="21c59-163">toospecify miejscu wyniki hello przechowywane, wprowadź informacje o kontenerze docelowego hello na stronie głównej aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="21c59-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="21c59-164">Również określić, gdzie hello aplikacji sieci web można uzyskać wartości wejściowe hello, w pliku lokalnym lub kontener magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="21c59-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="21c59-165">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="21c59-165">Click **Submit**.</span></span>
   
    ![Informacje o magazynu][image7]

<span data-ttu-id="21c59-167">Hello aplikacji sieci web zostanie wyświetlona strona o stanie zadania.</span><span class="sxs-lookup"><span data-stu-id="21c59-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="21c59-168">Po ukończeniu zadania hello będziesz mieć lokalizacji hello hello wyników w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="21c59-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="21c59-169">Istnieje również opcja hello pobierania pliku lokalne powitania wyników tooa.</span><span class="sxs-lookup"><span data-stu-id="21c59-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="21c59-170">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="21c59-170">For more information</span></span>
<span data-ttu-id="21c59-171">więcej informacji na temat toolearn...</span><span class="sxs-lookup"><span data-stu-id="21c59-171">toolearn more about...</span></span>

* <span data-ttu-id="21c59-172">Tworzenie eksperymentu uczenia maszynowego o usłudze Machine Learning Studio, zobacz [Tworzenie pierwszego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="21c59-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="21c59-173">toodeploy Twojego uczenia maszynowego eksperymentu jako usługi sieci web, zobacz temat [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="21c59-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="21c59-174">inne sposoby tooaccess usługi sieci web, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="21c59-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
