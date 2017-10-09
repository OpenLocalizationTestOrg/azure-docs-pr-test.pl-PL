---
title: "tooa aaaConnect Usługa sieci Web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Za pomocą języka C# lub języka Python należy połączyć tooan usługi Azure Machine Learning w sieci Web przy użyciu klucza autoryzacji."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="8c7ce-103">Połącz tooan Usługa sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c7ce-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="8c7ce-104">Witaj środowisko dewelopera usługi Azure Machine Learning jest sieci Web interfejsu API toomake operacje przewidywania dla usługi w danych wejściowych w czasie rzeczywistym lub w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="8c7ce-105">Operacje przewidywania dla usługi Azure Machine Learning Studio toocreate użycia i wdrażania usługi Azure Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="8c7ce-106">toolearn temat toocreate i wdrażanie usługi Machine Learning w sieci Web przy użyciu usługi Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="8c7ce-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="8c7ce-107">Samouczek dotyczący toocreate eksperymentu w usłudze Machine Learning Studio, zobacz temat [Tworzenie pierwszego eksperymentu](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="8c7ce-108">Aby uzyskać więcej informacji na temat toodeploy usługi sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="8c7ce-109">Aby uzyskać więcej informacji na temat usługi Machine Learning, odwiedź hello [Centrum dokumentacji uczenia maszynowego](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="8c7ce-110">Usługa Azure Machine Learning w sieci Web</span><span class="sxs-lookup"><span data-stu-id="8c7ce-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="8c7ce-111">Z hello usługi sieci Web Azure Machine Learning zewnętrznej aplikacji komunikuje się z modelem oceniania uczenia maszynowego przepływu pracy w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="8c7ce-112">Wywołanie usługi Machine Learning Web zwraca wyniki prognozowania tooan aplikacji zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="8c7ce-113">toomake wywołania usługi Machine Learning w sieci Web, należy przekazać klucz interfejsu API, który jest tworzony podczas wdrażania prognozowania.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="8c7ce-114">Witaj Machine Learning Web service jest oparta na REST, wybór popularnych Architektura programowania projektów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="8c7ce-115">Usługa Azure Machine Learning udostępnia dwa typy usług:</span><span class="sxs-lookup"><span data-stu-id="8c7ce-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="8c7ce-116">Odpowiedź na żądania usługi (RR) — krótki czas oczekiwania, wysoce skalowalna usługa, która zapewnia interfejs modeli bezstanowych toohello tworzone i wdrażane ze hello Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="8c7ce-117">Usługa partia zadań wykonywania (BES) — asynchronicznego usługi tego wyniki w partii rekordów danych.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="8c7ce-118">Aby uzyskać więcej informacji na temat usługi Machine Learning w sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="8c7ce-119">Pobierz klucz autoryzacji usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c7ce-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="8c7ce-120">Podczas wdrażania eksperymentu klucze interfejsu API są generowane dla hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="8c7ce-121">Można pobrać kluczy hello z kilku lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="8c7ce-122">W portalu usługi sieci Web Microsoft Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="8c7ce-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="8c7ce-123">Zaloguj się toohello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) portalu.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="8c7ce-124">tooretrieve klucz hello interfejsu API usługi sieci Web uczenie nowe maszyny:</span><span class="sxs-lookup"><span data-stu-id="8c7ce-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="8c7ce-125">W portalu usługi sieci Web systemu Azure Machine Learning powitania kliknij **usług sieci Web** hello menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="8c7ce-126">Kliknij przycisk hello usługi sieci Web, dla której ma zostać tooretrieve hello klucza.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="8c7ce-127">W menu u góry hello, kliknij polecenie **Consume**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="8c7ce-128">Skopiuj i Zapisz hello **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="8c7ce-129">tooretrieve klucz hello interfejsu API usługi klasycznego Machine Learning w sieci Web:</span><span class="sxs-lookup"><span data-stu-id="8c7ce-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="8c7ce-130">W portalu usługi sieci Web systemu Azure Machine Learning powitania kliknij **usług sieci Web klasycznego** hello menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="8c7ce-131">Kliknij przycisk hello usługi sieci Web, z którym pracujesz.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="8c7ce-132">Kliknij punkt końcowy hello, dla którego ma zostać tooretrieve hello klucza.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="8c7ce-133">W menu u góry hello, kliknij polecenie **Consume**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="8c7ce-134">Skopiuj i Zapisz hello **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="8c7ce-135">Klasycznym usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="8c7ce-135">Classic Web service</span></span>
 <span data-ttu-id="8c7ce-136">Można również pobierać klucza dla usługi sieci Web klasycznego z usługi Machine Learning Studio lub hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="8c7ce-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8c7ce-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="8c7ce-138">W usłudze Machine Learning Studio, kliknij przycisk **usług sieci WEB** powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="8c7ce-139">Kliknij usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-139">Click a Web service.</span></span> <span data-ttu-id="8c7ce-140">Witaj **klucz interfejsu API** znajduje się na powitania **pulpitu NAWIGACYJNEGO** kartę.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="8c7ce-141">klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="8c7ce-141">Azure classic portal</span></span>
1. <span data-ttu-id="8c7ce-142">Kliknij przycisk **UCZENIA MASZYNOWEGO** powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="8c7ce-143">Kliknij obszar roboczy hello, w którym znajduje się usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="8c7ce-144">Kliknij przycisk **usług sieci WEB**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="8c7ce-145">Kliknij usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-145">Click a Web service.</span></span>
5. <span data-ttu-id="8c7ce-146">Kliknij punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-146">Click an endpoint.</span></span> <span data-ttu-id="8c7ce-147">Witaj "Klucz interfejsu API" jest wyłączony w prawym dolnym hello.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="8c7ce-148"><a id="connect"></a>Usługa Machine Learning Web tooa Connect</span><span class="sxs-lookup"><span data-stu-id="8c7ce-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="8c7ce-149">Możesz połączyć tooa usługi Machine Learning w sieci Web przy użyciu dowolnego języka programowania, która obsługuje żądania HTTP i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="8c7ce-150">Przykłady można wyświetlić w języku C#, Python i R ze strony pomocy usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="8c7ce-151">**Maszyny pomocy Learning API** Machine Learning API pomocy jest tworzona podczas wdrażania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="8c7ce-152">Zobacz [uczenie maszynowe Azure wskazówki — wdrażanie usługi sieci Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="8c7ce-153">Hello Machine Learning API Pomocy zawiera szczegółowe informacje o prognozowania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="8c7ce-154">Kliknij przycisk hello usługi sieci Web, z którym pracujesz.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="8c7ce-155">Kliknij punkt końcowy hello, dla której ma zostać hello tooview strona pomocy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="8c7ce-156">W menu u góry hello, kliknij polecenie **Consume**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="8c7ce-157">Kliknij przycisk **strona pomocy interfejsu API** hello żądanie-odpowiedź lub wykonywania wsadowego usługi punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="8c7ce-158">**tooview Machine Learning API Pomoc dla usługi sieci Web nowy**</span><span class="sxs-lookup"><span data-stu-id="8c7ce-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="8c7ce-159">W portalu usługi sieci Web Azure Machine Learning hello:</span><span class="sxs-lookup"><span data-stu-id="8c7ce-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="8c7ce-160">Kliknij przycisk **usług sieci WEB** na powitania menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="8c7ce-161">Kliknij przycisk hello usługi sieci Web, dla której ma zostać tooretrieve hello klucza.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="8c7ce-162">Kliknij przycisk **Consume** tooget hello identyfikatorów URI dla hello Reposonse żądania i usługi wykonywania wsadowego i przykładowy kod w języku C#, R i Python.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="8c7ce-163">Kliknij przycisk **interfejsu API programu Swagger** tooget Swagger opartych na dokumentacji hello interfejsów API wywoływane z hello dostarczony identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="8c7ce-164">Przykład C#</span><span class="sxs-lookup"><span data-stu-id="8c7ce-164">C# Sample</span></span>
<span data-ttu-id="8c7ce-165">Użyj tooa tooconnect usługi Machine Learning Web **HttpClient** przekazywanie ScoreData.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="8c7ce-166">ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="8c7ce-167">Usługa Machine Learning toohello uwierzytelniania przy użyciu klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="8c7ce-168">Witaj tooa tooconnect usługi Machine Learning Web **Microsoft.AspNet.WebApi.Client** musi być zainstalowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="8c7ce-169">**Instalowania Microsoft.AspNet.WebApi.Client NuGet w programie Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="8c7ce-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="8c7ce-170">Publikowanie hello pobierania danych z UCI: 2 dla dorosłych klasy dataset usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="8c7ce-171">Kliknij pozycję **Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="8c7ce-172">Wybierz **Microsoft.AspNet.WebApi.Client Install-Package**.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="8c7ce-173">**Przykładowy kod hello toorun**</span><span class="sxs-lookup"><span data-stu-id="8c7ce-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="8c7ce-174">Publikowanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część hello pobieranie próbek uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="8c7ce-175">Przypisz apiKey kluczem hello z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="8c7ce-176">Zobacz **Pobierz klucz autoryzacji usługi Azure Machine Learning** powyżej.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="8c7ce-177">Przypisz serviceUri z hello przez identyfikator URI żądania.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="8c7ce-178">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="8c7ce-178">Python Sample</span></span>
<span data-ttu-id="8c7ce-179">tooa tooconnect usługi Machine Learning w sieci Web, użyj hello **urllib2** przekazywanie ScoreData biblioteki.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="8c7ce-180">ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="8c7ce-181">Usługa Machine Learning toohello uwierzytelniania przy użyciu klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="8c7ce-182">**Przykładowy kod hello toorun**</span><span class="sxs-lookup"><span data-stu-id="8c7ce-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="8c7ce-183">Wdrażanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część hello pobieranie próbek uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="8c7ce-184">Przypisz apiKey kluczem hello z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="8c7ce-185">Zobacz hello **Pobierz klucz autoryzacji usługi Azure Machine Learning** hello początku części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="8c7ce-186">Przypisz serviceUri z hello przez identyfikator URI żądania.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-186">Assign serviceUri with hello Request URI.</span></span>

