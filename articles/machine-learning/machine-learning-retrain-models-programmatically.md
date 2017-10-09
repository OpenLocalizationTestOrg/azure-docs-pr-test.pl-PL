---
title: modeli aaaRetrain Machine Learning | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooprogrammatically retrain modelu i aktualizacji hello web toouse hello nowo uczonego modelu usług w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="96b7e-103">Programowe ponowne trenowanie modeli usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="96b7e-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="96b7e-104">W tym przewodniku dowiesz się, jak tooprogrammatically retrain Azure Machine Learning usługi sieci Web przy użyciu języka C# i hello usługi wykonywania wsadowego usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="96b7e-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="96b7e-105">Po ma retrained hello modelu, hello następujące wskazówki pokazują, jak tooupdate hello modelu w usłudze sieci web predykcyjnej:</span><span class="sxs-lookup"><span data-stu-id="96b7e-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="96b7e-106">Jeśli wdrożono klasycznym usługi sieci web w portalu usługi sieci Web usługi Machine Learning hello, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="96b7e-107">Jeśli wdrożono nową usługę sieci web, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="96b7e-108">Omówienie hello ponownego trenowania procesu, zobacz [Retrain modelu uczenia maszynowego](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="96b7e-109">Jeśli chcesz toostart z istniejącą nowej usługi Azure Resource Manager na podstawie usługi sieci web, zobacz [Retrain istniejącej usługi sieci web predykcyjnej](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="96b7e-110">Tworzenie eksperymentu szkolenia</span><span class="sxs-lookup"><span data-stu-id="96b7e-110">Create a training experiment</span></span>
<span data-ttu-id="96b7e-111">Na przykład użyjesz "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" hello Microsoft Azure Machine Learning próbek.</span><span class="sxs-lookup"><span data-stu-id="96b7e-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="96b7e-112">toocreate eksperymentu hello:</span><span class="sxs-lookup"><span data-stu-id="96b7e-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="96b7e-113">Zaloguj się do tooMicrosoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="96b7e-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="96b7e-114">Na powitania prawym dolnym rogu hello pulpitu nawigacyjnego, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="96b7e-115">Wybierz przykład 5 z hello Samples firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="96b7e-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="96b7e-116">toorename hello eksperymentu, u góry hello hello kanwy eksperymentu, wybierz nazwę eksperymentu hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych".</span><span class="sxs-lookup"><span data-stu-id="96b7e-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="96b7e-117">Typ modelu spisu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-117">Type Census Model.</span></span>
6. <span data-ttu-id="96b7e-118">U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="96b7e-119">Kliknij przycisk **Konfiguruj usługę sieci web** i wybierz **ponownego trenowania usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="96b7e-120">Oto Hello hello początkowej eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-120">hello following shows hello initial experiment.</span></span>
   
   ![Początkowa eksperymentu.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="96b7e-122">Utworzyć eksperyment predykcyjny i Opublikuj jako usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="96b7e-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="96b7e-123">Następnie należy utworzyć eksperyment Predicative.</span><span class="sxs-lookup"><span data-stu-id="96b7e-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="96b7e-124">U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="96b7e-125">Ten hello model jest zapisywany jako Uczonego modelu i dodaje modułów wejścia i wyjścia usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="96b7e-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="96b7e-126">Kliknij pozycję **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="96b7e-126">Click **Run**.</span></span> 
3. <span data-ttu-id="96b7e-127">Po eksperymentu hello zakończył działanie, kliknij przycisk **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="96b7e-128">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="96b7e-129">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="96b7e-130">Wdrażanie eksperyment uczenia hello jako usługę sieci web szkolenia</span><span class="sxs-lookup"><span data-stu-id="96b7e-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="96b7e-131">tooretrain hello trenowanego modelu, należy wdrożyć eksperyment uczenia hello utworzony jako usługę sieci web Retraining.</span><span class="sxs-lookup"><span data-stu-id="96b7e-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="96b7e-132">Ta usługa sieci web musi *wyjście usługi sieci Web* modułu połączone toohello  *[Train Model] [ train-model]*  modułu, toobe stanie tooproduce nowy modele przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="96b7e-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="96b7e-133">eksperyment uczenia toohello tooreturn, kliknij ikonę eksperymenty hello w okienku po lewej stronie powitania, a następnie kliknij eksperyment hello o nazwie modelu spisu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="96b7e-134">W polu wyszukiwania elementów eksperymentu wyszukiwania hello wpisz usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="96b7e-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="96b7e-135">Przeciągnij *wprowadzania usługi sieci Web* modułu na powitania obszaru roboczego eksperymentu i połącz toohello jego dane wyjściowe *Clean Missing Data* modułu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="96b7e-136">Dzięki temu, że dane ponownego trenowania jest przetwarzany hello takie same jak oryginalne dane szkolenia.</span><span class="sxs-lookup"><span data-stu-id="96b7e-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="96b7e-137">Przeciągnij dwa *wyjście usługi sieci web* modułów na powitania eksperymentu kanwy.</span><span class="sxs-lookup"><span data-stu-id="96b7e-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="96b7e-138">Połącz dane wyjściowe hello hello *Train Model* modułu tooone i hello dane wyjściowe hello *Evaluate Model* modułu toohello innych.</span><span class="sxs-lookup"><span data-stu-id="96b7e-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="96b7e-139">Witaj wyjście usługi sieci web dla **Train Model** daje hello nowe trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="96b7e-140">Hello dane wyjściowe dołączony zbyt**Evaluate Model** zwraca wyjściowy ten moduł, który jest hello wyniki.</span><span class="sxs-lookup"><span data-stu-id="96b7e-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="96b7e-141">Kliknij pozycję **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="96b7e-141">Click **Run**.</span></span> 

<span data-ttu-id="96b7e-142">Następnie należy wdrożyć eksperyment uczenia hello jako usługę sieci web, który spowoduje utworzenie uczonego modelu i wyniki oceny modelu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="96b7e-143">tooaccomplish to dalej zestawu działań są zależne od tego, czy użytkownik pracuje z usługą sieci web klasycznego lub nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="96b7e-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="96b7e-144">**Usługa sieci web klasycznego**</span><span class="sxs-lookup"><span data-stu-id="96b7e-144">**Classic web service**</span></span>

<span data-ttu-id="96b7e-145">U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="96b7e-146">Usługi sieci Web Hello **pulpitu nawigacyjnego** zostanie wyświetlony z strona pomocy hello klucz interfejsu API i hello interfejsu API dla wykonywania wsadowego usługi.</span><span class="sxs-lookup"><span data-stu-id="96b7e-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="96b7e-147">Witaj metody wykonywania wsadowego usługi może służyć do tworzenia modeli przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="96b7e-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="96b7e-148">**Nowa usługa sieci web**</span><span class="sxs-lookup"><span data-stu-id="96b7e-148">**New web service**</span></span>

<span data-ttu-id="96b7e-149">U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="96b7e-150">portal usługi sieci Web sieci Web usługi Azure Machine Learning Hello otwiera stronę usługi sieci web Deploy toohello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="96b7e-151">Wpisz nazwę usługi sieci web i wybierz plan płatności, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="96b7e-152">Hello metody wsadowe mogą służyć do tworzenia modeli przeszkolone</span><span class="sxs-lookup"><span data-stu-id="96b7e-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="96b7e-153">W obu przypadkach po obejmuje działania ukończone hello wynikowy przepływu pracy powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="96b7e-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Wynikowa przepływu pracy, po uruchomieniu.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="96b7e-155">Ponownie ucz modelu hello nowymi danymi za pomocą usługi BES</span><span class="sxs-lookup"><span data-stu-id="96b7e-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="96b7e-156">Na przykład używasz C# hello toocreate ponownego trenowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96b7e-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="96b7e-157">Umożliwia także hello Python lub R przykładowy kod tooaccomplish to zadanie.</span><span class="sxs-lookup"><span data-stu-id="96b7e-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="96b7e-158">toocall hello ponownego trenowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="96b7e-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="96b7e-159">Tworzenie aplikacji konsolowej C# w programie Visual Studio: **nowy** > **projektu** > **Visual C#** > **Windows Desktop klasycznego** > **aplikacji konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="96b7e-160">Zaloguj się toohello portalu Usługa sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="96b7e-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="96b7e-161">Podczas pracy z usługą sieci web klasycznego, kliknij przycisk **klasycznym usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="96b7e-162">Kliknij przycisk hello usługi sieci web, którą użytkownik pracuje z.</span><span class="sxs-lookup"><span data-stu-id="96b7e-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="96b7e-163">Kliknij przycisk hello domyślnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="96b7e-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="96b7e-164">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="96b7e-165">U dołu hello hello **Consume** strony w hello **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="96b7e-166">Nadal toostep 5 tej procedury.</span><span class="sxs-lookup"><span data-stu-id="96b7e-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="96b7e-167">Jeśli pracujesz z nową usługę sieci web, kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="96b7e-168">Kliknij przycisk hello usługi sieci web, którą użytkownik pracuje z.</span><span class="sxs-lookup"><span data-stu-id="96b7e-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="96b7e-169">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="96b7e-170">U dołu strony Consume hello w hello hello **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="96b7e-171">Skopiuj hello próbki kodu C# dla wykonywania wsadowego i wklej go do pliku Program.cs hello, upewniając się, że przestrzeń nazw hello pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="96b7e-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="96b7e-172">Dodaj hello pakiet Nuget Microsoft.AspNet.WebApi.Client określonych w hello komentarze.</span><span class="sxs-lookup"><span data-stu-id="96b7e-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="96b7e-173">tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania hello, być może konieczne tooinstall powitania klienta biblioteki dla usług magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96b7e-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="96b7e-174">Aby uzyskać więcej informacji, zobacz [usługi magazynu systemu Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="96b7e-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="96b7e-175">Zaktualizuj hello apikey deklaracji</span><span class="sxs-lookup"><span data-stu-id="96b7e-175">Update hello apikey declaration</span></span>
<span data-ttu-id="96b7e-176">Zlokalizuj hello **apikey** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="96b7e-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="96b7e-177">W hello **zużycie podstawowe informacje o** sekcji hello **Consume** strony Znajdź klucz podstawowy hello i skopiuj go toohello **apikey** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="96b7e-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="96b7e-178">Zaktualizuj informacje magazynie Azure hello</span><span class="sxs-lookup"><span data-stu-id="96b7e-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="96b7e-179">Hello BES przykładowy kod operacji przekazywania plików z dysku (na przykład "C:\temp\CensusIpnput.csv") tooAzure magazynu, procesy i zapisuje hello wyników wstecz tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="96b7e-180">tooaccomplish to zadanie, należy pobrać hello nazwę, klucz oraz kontenera informacji o koncie magazynu dla konta magazynu z hello klasycznego portalu Azure i zaktualizuj hello odpowiednie wartości w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="96b7e-181">Zaloguj się toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="96b7e-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="96b7e-182">W kolumnie nawigacji po lewej stronie powitania kliknij **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="96b7e-183">Z listy hello kont magazynu wybierz jeden toostore hello retrained modelu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="96b7e-184">U dołu hello hello strony, kliknij przycisk **Zarządzaj kluczami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="96b7e-185">Skopiuj i Zapisz hello **podstawowy klucz dostępu** hello Zamknij okno dialogowe i.</span><span class="sxs-lookup"><span data-stu-id="96b7e-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="96b7e-186">U góry hello hello strony, kliknij przycisk **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="96b7e-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="96b7e-187">Wybierz istniejącego kontenera lub Utwórz nową i Zapisz nazwę hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="96b7e-188">Zlokalizuj hello *StorageAccountName*, *StorageAccountKey*, i *StorageContainerName* deklaracje i zapisany w wartości hello aktualizacji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="96b7e-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="96b7e-189">Ponadto musisz zapewnić, że plik wejściowy hello jest dostępna w lokalizacji hello, które określisz w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="96b7e-190">Określ lokalizację danych wyjściowych hello</span><span class="sxs-lookup"><span data-stu-id="96b7e-190">Specify hello output location</span></span>
<span data-ttu-id="96b7e-191">Podczas określania lokalizacji wyjściowej hello na powitania ładunku żądania, hello rozszerzenie określone w pliku hello *RelativeLocation* muszą być określone jako ilearner.</span><span class="sxs-lookup"><span data-stu-id="96b7e-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="96b7e-192">Zobacz poniższy przykład hello:</span><span class="sxs-lookup"><span data-stu-id="96b7e-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="96b7e-193">Witaj nazwy lokalizacji danych wyjściowych mogą być inne niż te, w tym przewodniku oparte na powitania kolejności, w której są dodawane modułów wyjście usługi sieci web hello hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="96b7e-194">Ponieważ skonfigurowaniu tego eksperymentu uczenia z danych wyjściowych dwóch hello wyniki obejmują informacje o lokalizacji magazynu dla obu z nich.</span><span class="sxs-lookup"><span data-stu-id="96b7e-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Ponownego trenowania danych wyjściowych][6]

<span data-ttu-id="96b7e-196">Diagram 4: Ponownego trenowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="96b7e-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="96b7e-197">Ocena wyników ponownego trenowania hello</span><span class="sxs-lookup"><span data-stu-id="96b7e-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="96b7e-198">Po uruchomieniu aplikacji hello hello danych wyjściowych zawiera adres URL hello i tooaccess niezbędne tokenu sygnatury dostępu Współdzielonego hello wyniki oceny.</span><span class="sxs-lookup"><span data-stu-id="96b7e-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="96b7e-199">Można wyświetlić wyniki wydajności hello modelu hello retrained łącząc hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik Aby uzyskać *output2* (jak pokazano w poprzednim ponownego trenowania obrazu wyjściowego hello) i wklejanie hello pełny adres URL na pasku adresu przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="96b7e-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="96b7e-200">Witaj toodetermine wyników należy sprawdzić, czy nowo uczonego modelu hello wykonuje również za mało hello tooreplace jedną istniejącą.</span><span class="sxs-lookup"><span data-stu-id="96b7e-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="96b7e-201">Kopiuj hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z hello wynik użyjesz ich podczas hello ponownego trenowania procesu.</span><span class="sxs-lookup"><span data-stu-id="96b7e-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96b7e-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96b7e-202">Next steps</span></span>
<span data-ttu-id="96b7e-203">Jeśli wdrożono usługę sieci web predykcyjnej hello, klikając **wdrażanie usługi sieci Web [klasyczny]**, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="96b7e-204">Jeśli wdrożono usługę sieci web predykcyjnej hello, klikając **wdrażanie usługi sieci Web [New]**, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="96b7e-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
