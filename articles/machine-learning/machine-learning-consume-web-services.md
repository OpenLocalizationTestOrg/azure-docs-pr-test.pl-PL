---
title: "Jak korzystać z usługi sieci Web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Po wdrożeniu usługi uczenia maszynowego, usługę sieci Web RESTFul, który ma zostać udostępnione mogą być używane jako usługa w czasie rzeczywistym żądanie odpowiedź lub jako usługę wykonywania wsadowego."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a><span data-ttu-id="6b3de-103">Jak korzystać z usługi Azure Machine Learning w sieci Web</span><span class="sxs-lookup"><span data-stu-id="6b3de-103">How to consume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="6b3de-104">Po wdrożenia usługi Azure Machine Learning model predykcyjny jako usługę sieci Web, można użyć interfejsu API REST przesyła dane do pobrania prognoz.</span><span class="sxs-lookup"><span data-stu-id="6b3de-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API to send it data and get predictions.</span></span> <span data-ttu-id="6b3de-105">Możesz wysłać dane w czasie rzeczywistym lub w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="6b3de-105">You can send the data in real-time or in batch mode.</span></span>

<span data-ttu-id="6b3de-106">Można znaleźć więcej informacji na temat sposobu tworzenia i wdrażania usługi Machine Learning w sieci Web przy użyciu usługi Machine Learning Studio, w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="6b3de-106">You can find more information about how to create and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="6b3de-107">Samouczek dotyczący sposobu tworzenia eksperymentu w usłudze Machine Learning Studio, zobacz [Tworzenie pierwszego eksperymentu](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="6b3de-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="6b3de-108">Aby uzyskać więcej informacji na temat wdrażania usługi sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6b3de-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="6b3de-109">Aby uzyskać więcej informacji na temat usługi Machine Learning, odwiedź [Centrum dokumentacji uczenia maszynowego](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="6b3de-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="6b3de-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b3de-110">Overview</span></span>
<span data-ttu-id="6b3de-111">W usłudze Azure Machine Learning w sieci Web aplikacji zewnętrznej komunikuje się z modelem oceniania uczenia maszynowego przepływu pracy w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="6b3de-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="6b3de-112">Wywołanie usługi Machine Learning Web zwraca wyniki prognozowania do aplikacji zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="6b3de-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="6b3de-113">Aby wywołać usługi Machine Learning w sieci Web, należy przekazać klucz interfejsu API, który jest tworzony podczas wdrażania prognozowania.</span><span class="sxs-lookup"><span data-stu-id="6b3de-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="6b3de-114">Usługa Machine Learning w sieci Web jest oparta na REST, wybór popularnych Architektura programowania projektów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="6b3de-115">Usługa Azure Machine Learning udostępnia dwa typy usług:</span><span class="sxs-lookup"><span data-stu-id="6b3de-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="6b3de-116">Odpowiedź na żądania usługi (RR) — krótki czas oczekiwania, wysoce skalowalna usługa, która zapewnia interfejs do modeli bezstanowych, utworzeniu i wdrożeniu z Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="6b3de-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="6b3de-117">Usługa partia zadań wykonywania (BES) — asynchronicznego usługi tego wyniki w partii rekordów danych.</span><span class="sxs-lookup"><span data-stu-id="6b3de-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="6b3de-118">Aby uzyskać więcej informacji na temat usługi Machine Learning w sieci Web, zobacz [wdrażania usługi Machine Learning Web](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6b3de-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="6b3de-119">Pobierz klucz autoryzacji usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6b3de-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="6b3de-120">Podczas wdrażania eksperymentu klucze interfejsu API są generowane przez usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="6b3de-121">Klucze można pobrać z kilku lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="6b3de-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="6b3de-122">W portalu usługi sieci Web Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6b3de-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="6b3de-123">Zaloguj się do [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) portalu.</span><span class="sxs-lookup"><span data-stu-id="6b3de-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="6b3de-124">Aby pobrać klucz interfejsu API usługi sieci Web uczenie nowe maszyny:</span><span class="sxs-lookup"><span data-stu-id="6b3de-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="6b3de-125">W portalu usługi sieci Web systemu Azure Machine Learning kliknij **usług sieci Web** menu u góry.</span><span class="sxs-lookup"><span data-stu-id="6b3de-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="6b3de-126">Kliknij usługę sieci Web, dla których chcesz pobrać klucza.</span><span class="sxs-lookup"><span data-stu-id="6b3de-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="6b3de-127">W górnym menu, kliknij przycisk **Consume**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="6b3de-128">Skopiuj i Zapisz **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="6b3de-129">Aby pobrać klucz interfejsu API usługi klasycznego Machine Learning w sieci Web:</span><span class="sxs-lookup"><span data-stu-id="6b3de-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="6b3de-130">W portalu usługi sieci Web systemu Azure Machine Learning kliknij **usług sieci Web klasycznego** menu u góry.</span><span class="sxs-lookup"><span data-stu-id="6b3de-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="6b3de-131">Kliknij usługę sieci Web, z którym pracujesz.</span><span class="sxs-lookup"><span data-stu-id="6b3de-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="6b3de-132">Kliknij punkt końcowy, dla którego chcesz pobrać klucza.</span><span class="sxs-lookup"><span data-stu-id="6b3de-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="6b3de-133">W górnym menu, kliknij przycisk **Consume**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="6b3de-134">Skopiuj i Zapisz **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="6b3de-135">Klasycznym usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="6b3de-135">Classic Web service</span></span>
 <span data-ttu-id="6b3de-136">Można również pobierać klucza dla usługi sieci Web klasycznego z usługi Machine Learning Studio lub klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3de-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="6b3de-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="6b3de-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="6b3de-138">W usłudze Machine Learning Studio, kliknij przycisk **usług sieci WEB** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="6b3de-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="6b3de-139">Kliknij usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-139">Click a Web service.</span></span> <span data-ttu-id="6b3de-140">**Klucz interfejsu API** znajduje się na **pulpitu NAWIGACYJNEGO** kartę.</span><span class="sxs-lookup"><span data-stu-id="6b3de-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="6b3de-141">klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="6b3de-141">Azure classic portal</span></span>
1. <span data-ttu-id="6b3de-142">Kliknij przycisk **UCZENIA MASZYNOWEGO** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="6b3de-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="6b3de-143">Kliknij obszar roboczy, w którym znajduje się usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="6b3de-144">Kliknij przycisk **usług sieci WEB**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="6b3de-145">Kliknij usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-145">Click a Web service.</span></span>
5. <span data-ttu-id="6b3de-146">Kliknij punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="6b3de-146">Click an endpoint.</span></span> <span data-ttu-id="6b3de-147">"Klucz interfejsu API" jest wyłączony w prawej dolnej.</span><span class="sxs-lookup"><span data-stu-id="6b3de-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="6b3de-148"><a id="connect"></a>Połączyć się z usługą Machine Learning w sieci Web</span><span class="sxs-lookup"><span data-stu-id="6b3de-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="6b3de-149">Można nawiązać połączenia z usługą Machine Learning w sieci Web przy użyciu języka programowania, która obsługuje żądania HTTP i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6b3de-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="6b3de-150">Przykłady można wyświetlić w języku C#, Python i R ze strony pomocy usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="6b3de-151">**Maszyny pomocy Learning API** Machine Learning API pomocy jest tworzona podczas wdrażania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="6b3de-152">Zobacz [uczenie maszynowe Azure wskazówki — wdrażanie usługi sieci Web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6b3de-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="6b3de-153">Pomoc Machine Learning API zawiera szczegółowe informacje o prognozowania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="6b3de-154">Kliknij usługę sieci Web, z którym pracujesz.</span><span class="sxs-lookup"><span data-stu-id="6b3de-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="6b3de-155">Kliknij punkt końcowy, dla którego chcesz wyświetlić strona pomocy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b3de-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="6b3de-156">W górnym menu, kliknij przycisk **Consume**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="6b3de-157">Kliknij przycisk **strona pomocy interfejsu API** w obszarze żądanie-odpowiedź lub wykonywania wsadowego usługi punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="6b3de-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="6b3de-158">**Do widoku interfejsu API uczenia maszynowego Pomoc dla usługi sieci Web nowy**</span><span class="sxs-lookup"><span data-stu-id="6b3de-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="6b3de-159">W Azure Machine Learning Portal usługi sieci Web:</span><span class="sxs-lookup"><span data-stu-id="6b3de-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="6b3de-160">Kliknij przycisk **usług sieci WEB** w górnym menu.</span><span class="sxs-lookup"><span data-stu-id="6b3de-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="6b3de-161">Kliknij usługę sieci Web, dla których chcesz pobrać klucza.</span><span class="sxs-lookup"><span data-stu-id="6b3de-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="6b3de-162">Kliknij przycisk **Consume** można pobrać identyfikatorów URI dla żądania Reposonse i usługi wykonywania wsadowego i przykładowy kod w języku C#, R i Python.</span><span class="sxs-lookup"><span data-stu-id="6b3de-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="6b3de-163">Kliknij przycisk **interfejsu API programu Swagger** można pobrać struktury Swagger interfejsy API wywoływanych z podany identyfikator URI na podstawie dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6b3de-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="6b3de-164">Przykład C#</span><span class="sxs-lookup"><span data-stu-id="6b3de-164">C# Sample</span></span>
<span data-ttu-id="6b3de-165">Aby połączyć się z usługą Machine Learning w sieci Web, należy użyć **HttpClient** przekazywanie ScoreData.</span><span class="sxs-lookup"><span data-stu-id="6b3de-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="6b3de-166">ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje ScoreData.</span><span class="sxs-lookup"><span data-stu-id="6b3de-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="6b3de-167">Uwierzytelnianie usługi Machine Learning przy użyciu klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b3de-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="6b3de-168">Aby połączyć się z usługą Machine Learning w sieci Web, **Microsoft.AspNet.WebApi.Client** musi być zainstalowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b3de-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="6b3de-169">**Instalowania Microsoft.AspNet.WebApi.Client NuGet w programie Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="6b3de-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="6b3de-170">Publikowanie pobierania zestawu danych z UCI: 2 dla dorosłych klasy dataset usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="6b3de-171">Kliknij pozycję **Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="6b3de-172">Wybierz **Microsoft.AspNet.WebApi.Client Install-Package**.</span><span class="sxs-lookup"><span data-stu-id="6b3de-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="6b3de-173">**Aby uruchomić przykładowy kod**</span><span class="sxs-lookup"><span data-stu-id="6b3de-173">**To run the code sample**</span></span>

1. <span data-ttu-id="6b3de-174">Publikowanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część pobieranie próbek uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="6b3de-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="6b3de-175">Przypisz apiKey przy użyciu klucza z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="6b3de-176">Zobacz **Pobierz klucz autoryzacji usługi Azure Machine Learning** powyżej.</span><span class="sxs-lookup"><span data-stu-id="6b3de-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="6b3de-177">Przypisz serviceUri o identyfikatorze URI żądania.</span><span class="sxs-lookup"><span data-stu-id="6b3de-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="6b3de-178">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="6b3de-178">Python Sample</span></span>
<span data-ttu-id="6b3de-179">Aby połączyć się z usługą Machine Learning w sieci Web, należy użyć **urllib2** przekazywanie ScoreData biblioteki.</span><span class="sxs-lookup"><span data-stu-id="6b3de-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="6b3de-180">ScoreData zawiera FeatureVector, n wymiarowej wektor liczbowe funkcje reprezentuje ScoreData.</span><span class="sxs-lookup"><span data-stu-id="6b3de-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="6b3de-181">Uwierzytelnianie usługi Machine Learning przy użyciu klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b3de-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="6b3de-182">**Aby uruchomić przykładowy kod**</span><span class="sxs-lookup"><span data-stu-id="6b3de-182">**To run the code sample**</span></span>

1. <span data-ttu-id="6b3de-183">Wdrażanie "przykład 1: pobrać zestaw danych z UCI: osoba dorosła 2 klasy dataset" eksperymentu, część pobieranie próbek uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="6b3de-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="6b3de-184">Przypisz apiKey przy użyciu klucza z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6b3de-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="6b3de-185">Zobacz **Pobierz klucz autoryzacji usługi Azure Machine Learning** na początku części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="6b3de-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="6b3de-186">Przypisz serviceUri o identyfikatorze URI żądania.</span><span class="sxs-lookup"><span data-stu-id="6b3de-186">Assign serviceUri with the Request URI.</span></span>

