---
title: Ponownie ucz modele uczenia maszynowego programowo | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak programowo retrain modelu i usługi sieci web, aby użyć nowo uczonego modelu w usłudze Azure Machine Learning aktualizacji."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="0891c-103">Programowe ponowne trenowanie modeli usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0891c-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="0891c-104">W tym przewodniku dowiesz się, jak programowo ponownie ucz Azure Machine Learning usługi sieci Web przy użyciu języka C# i usługę wykonywania wsadowego usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0891c-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="0891c-105">Po ma retrained modelu, następujące wskazówki pokazują, jak zaktualizować model w usłudze sieci web predykcyjnej:</span><span class="sxs-lookup"><span data-stu-id="0891c-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="0891c-106">Jeśli wdrożono klasycznym usługi sieci web w portalu usługi sieci Web usługi Machine Learning, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="0891c-107">Jeśli wdrożono nową usługę sieci web, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="0891c-108">Omówienie procesu ponownego trenowania, zobacz [Retrain modelu uczenia maszynowego](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="0891c-109">Jeśli chcesz uruchomić z usługą sieci web nowej usługi Azure Resource Manager na podstawie istniejących, zobacz [Retrain istniejącej usługi sieci web predykcyjnej](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="0891c-110">Tworzenie eksperymentu szkolenia</span><span class="sxs-lookup"><span data-stu-id="0891c-110">Create a training experiment</span></span>
<span data-ttu-id="0891c-111">Na przykład użyjesz "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" z próbek Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0891c-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="0891c-112">Aby utworzyć eksperyment:</span><span class="sxs-lookup"><span data-stu-id="0891c-112">To create the experiment:</span></span>

1. <span data-ttu-id="0891c-113">Studio uczenia maszynowego za pomocą Zaloguj się do platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0891c-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="0891c-114">W prawym dolnym rogu pulpitu nawigacyjnego, kliknij polecenie **nowy**.</span><span class="sxs-lookup"><span data-stu-id="0891c-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="0891c-115">Wybierz przykład 5 z Samples firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0891c-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="0891c-116">Aby zmienić nazwę eksperymentu w górnej części obszaru roboczego eksperymentu, wybierz nazwę eksperymentu "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych".</span><span class="sxs-lookup"><span data-stu-id="0891c-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="0891c-117">Typ modelu spisu.</span><span class="sxs-lookup"><span data-stu-id="0891c-117">Type Census Model.</span></span>
6. <span data-ttu-id="0891c-118">W dolnej części obszaru roboczego eksperymentu, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="0891c-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="0891c-119">Kliknij przycisk **Konfiguruj usługę sieci web** i wybierz **ponownego trenowania usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="0891c-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="0891c-120">Poniżej przedstawiono początkowej eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="0891c-120">The following shows the initial experiment.</span></span>
   
   ![Początkowa eksperymentu.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="0891c-122">Utworzyć eksperyment predykcyjny i Opublikuj jako usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="0891c-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="0891c-123">Następnie należy utworzyć eksperyment Predicative.</span><span class="sxs-lookup"><span data-stu-id="0891c-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="0891c-124">W dolnej części obszaru roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="0891c-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="0891c-125">Ten model jest zapisywany jako Uczonego modelu i dodaje modułów wejścia i wyjścia usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="0891c-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="0891c-126">Kliknij pozycję **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="0891c-126">Click **Run**.</span></span> 
3. <span data-ttu-id="0891c-127">Po zakończeniu pracy eksperyment, kliknij przycisk **wdrażanie usługi sieci Web [klasyczny]** lub **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="0891c-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="0891c-128">Aby wdrożyć nową usługę sieci web musi masz wystarczające uprawnienia do subskrypcji, do którego należy wdrożyć usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="0891c-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="0891c-129">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="0891c-130">Wdrażanie eksperyment uczenia jako usługę sieci web szkolenia</span><span class="sxs-lookup"><span data-stu-id="0891c-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="0891c-131">Aby ponownie ucz trenowanego modelu, należy wdrożyć eksperyment uczenia, utworzony jako usługę sieci web Retraining.</span><span class="sxs-lookup"><span data-stu-id="0891c-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="0891c-132">Ta usługa sieci web musi *wyjście usługi sieci Web* modułu połączony  *[Train Model] [ train-model]*  modułu, aby można było tworzyć nowe modele przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="0891c-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="0891c-133">Aby powrócić do eksperyment uczenia, kliknij ikonę eksperymenty w okienku po lewej stronie, a następnie kliknij eksperyment o nazwie modelu spisu.</span><span class="sxs-lookup"><span data-stu-id="0891c-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="0891c-134">W polu wyszukiwania elementów eksperymentu wyszukiwania wpisz usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="0891c-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="0891c-135">Przeciągnij *wprowadzania usługi sieci Web* modułu na eksperyment roboczego i połącz dane wyjściowe do *Clean Missing Data* modułu.</span><span class="sxs-lookup"><span data-stu-id="0891c-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="0891c-136">Dzięki temu, że ponownego trenowania danych jest przetwarzany taki sam sposób jak oryginalne dane szkolenia.</span><span class="sxs-lookup"><span data-stu-id="0891c-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="0891c-137">Przeciągnij dwa *wyjście usługi sieci web* modułów do kanwy eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="0891c-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="0891c-138">Połącz dane wyjściowe *Train Model* na jednym i dane wyjściowe z modułu *Evaluate Model* modułu do drugiego.</span><span class="sxs-lookup"><span data-stu-id="0891c-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="0891c-139">Wyjście usługi sieci web dla **Train Model** daje nowe trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="0891c-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="0891c-140">Dane wyjściowe dołączony do **Evaluate Model** zwraca wyjściowy ten moduł, który jest wyniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="0891c-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="0891c-141">Kliknij pozycję **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="0891c-141">Click **Run**.</span></span> 

<span data-ttu-id="0891c-142">Następnie należy wdrożyć eksperyment uczenia jako usługę sieci web, który spowoduje utworzenie uczonego modelu i wyniki oceny modelu.</span><span class="sxs-lookup"><span data-stu-id="0891c-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="0891c-143">W tym celu dalej zestawu działań są zależne od tego, czy działają z usługą sieci web klasycznego lub nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="0891c-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="0891c-144">**Usługa sieci web klasycznego**</span><span class="sxs-lookup"><span data-stu-id="0891c-144">**Classic web service**</span></span>

<span data-ttu-id="0891c-145">W dolnej części obszaru roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**.</span><span class="sxs-lookup"><span data-stu-id="0891c-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="0891c-146">Usługa sieci Web **pulpitu nawigacyjnego** jest wyświetlana strona pomocy interfejsu API i klucz interfejsu API dla wykonywania wsadowego usługi.</span><span class="sxs-lookup"><span data-stu-id="0891c-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="0891c-147">Metody wykonywania wsadowego usługi może służyć do tworzenia modeli przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="0891c-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="0891c-148">**Nowa usługa sieci web**</span><span class="sxs-lookup"><span data-stu-id="0891c-148">**New web service**</span></span>

<span data-ttu-id="0891c-149">W dolnej części obszaru roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="0891c-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="0891c-150">Portal usługi sieci Web sieci Web usługi Azure Machine Learning otwiera się do strony usługi sieci web Deploy.</span><span class="sxs-lookup"><span data-stu-id="0891c-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="0891c-151">Wpisz nazwę usługi sieci web i wybierz plan płatności, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="0891c-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="0891c-152">Metody wykonywania wsadowego usługi może służyć do tworzenia modeli przeszkolone</span><span class="sxs-lookup"><span data-stu-id="0891c-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="0891c-153">W obu przypadkach po eksperymentu zakończy działanie, wynikowy przepływu pracy powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="0891c-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Wynikowa przepływu pracy, po uruchomieniu.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="0891c-155">Ponownie ucz modelu nowymi danymi za pomocą usługi BES</span><span class="sxs-lookup"><span data-stu-id="0891c-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="0891c-156">Na przykład używasz C# do tworzenia aplikacji ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="0891c-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="0891c-157">Aby wykonać to zadanie umożliwia także przykładowy kod języka Python lub R.</span><span class="sxs-lookup"><span data-stu-id="0891c-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="0891c-158">Wywoływanie interfejsów API ponownego trenowania:</span><span class="sxs-lookup"><span data-stu-id="0891c-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="0891c-159">Tworzenie aplikacji konsolowej C# w programie Visual Studio: **nowy** > **projektu** > **Visual C#** > **Windows Desktop klasycznego** > **aplikacji konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="0891c-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="0891c-160">Zaloguj się do portalu usługi sieci Web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0891c-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="0891c-161">Podczas pracy z usługą sieci web klasycznego, kliknij przycisk **klasycznym usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="0891c-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="0891c-162">Kliknij usługę sieci web, w którym pracujesz z.</span><span class="sxs-lookup"><span data-stu-id="0891c-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="0891c-163">Kliknij domyślny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="0891c-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="0891c-164">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="0891c-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="0891c-165">W dolnej części **Consume** strony w **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="0891c-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="0891c-166">Przejdź do kroku 5 tej procedury.</span><span class="sxs-lookup"><span data-stu-id="0891c-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="0891c-167">Jeśli pracujesz z nową usługę sieci web, kliknij przycisk **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="0891c-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="0891c-168">Kliknij usługę sieci web, w którym pracujesz z.</span><span class="sxs-lookup"><span data-stu-id="0891c-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="0891c-169">Kliknij przycisk **korzystać**.</span><span class="sxs-lookup"><span data-stu-id="0891c-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="0891c-170">W dolnej części Consume strony, **przykładowy kod** kliknij **partii**.</span><span class="sxs-lookup"><span data-stu-id="0891c-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="0891c-171">Skopiuj przykładowy kod C# dla wykonywania wsadowego i wklej go do pliku Program.cs, upewniając się, że przestrzeń nazw pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="0891c-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="0891c-172">Dodaj pakiet Nuget Microsoft.AspNet.WebApi.Client określonych w komentarzach.</span><span class="sxs-lookup"><span data-stu-id="0891c-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="0891c-173">Można dodać odwołania do Microsoft.WindowsAzure.Storage.dll, należy najpierw zainstalować bibliotekę klienta usługi magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0891c-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="0891c-174">Aby uzyskać więcej informacji, zobacz [usługi magazynu systemu Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="0891c-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="0891c-175">Deklaracja apikey aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0891c-175">Update the apikey declaration</span></span>
<span data-ttu-id="0891c-176">Zlokalizuj **apikey** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="0891c-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="0891c-177">W **zużycie podstawowe informacje o** sekcji **Consume** strony Znajdź klucz podstawowy i skopiuj go do **apikey** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="0891c-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="0891c-178">Zaktualizuj informacje o usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0891c-178">Update the Azure Storage information</span></span>
<span data-ttu-id="0891c-179">BES przykładowy kod operacji przekazywania plików z dysku lokalnego (na przykład "C:\temp\CensusIpnput.csv") do usługi Azure Storage, procesy i zapisuje wyniki wstecz do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="0891c-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="0891c-180">Aby wykonać to zadanie, należy pobrać nazwę, klucz oraz kontenera informacji o koncie magazynu dla konta magazynu z klasycznego portalu Azure i wartości odpowiednich aktualizacji w kodzie.</span><span class="sxs-lookup"><span data-stu-id="0891c-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="0891c-181">Zaloguj się do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0891c-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="0891c-182">W kolumnie nawigacji po lewej stronie kliknij **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="0891c-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="0891c-183">Z listy kont magazynu wybierz jeden do przechowywania retrained modelu.</span><span class="sxs-lookup"><span data-stu-id="0891c-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="0891c-184">W dolnej części strony kliknij **Zarządzaj kluczami dostępu**.</span><span class="sxs-lookup"><span data-stu-id="0891c-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="0891c-185">Skopiuj i Zapisz **podstawowy klucz dostępu** i zamknij okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0891c-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="0891c-186">W górnej części strony kliknij **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="0891c-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="0891c-187">Wybierz kontener istniejącą lub Utwórz nową i Zapisz nazwę.</span><span class="sxs-lookup"><span data-stu-id="0891c-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="0891c-188">Zlokalizuj *StorageAccountName*, *StorageAccountKey*, i *StorageContainerName* deklaracje i zaktualizuj wartości zapisane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0891c-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="0891c-189">Ponadto musisz zapewnić, że plik wejściowy jest dostępny w lokalizacji, które określisz w kodzie.</span><span class="sxs-lookup"><span data-stu-id="0891c-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="0891c-190">Określ lokalizację danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="0891c-190">Specify the output location</span></span>
<span data-ttu-id="0891c-191">Podczas określania lokalizacji danych wyjściowych w ładunku żądania, rozszerzenie pliku określona w *RelativeLocation* muszą być określone jako ilearner.</span><span class="sxs-lookup"><span data-stu-id="0891c-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="0891c-192">Zobacz poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0891c-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="0891c-193">Nazwy lokalizacji danych wyjściowych może być inne niż w podane w tym przewodniku, na podstawie kolejności, w której są dodawane modułów wyjście usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="0891c-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="0891c-194">Ponieważ skonfigurowaniu tego eksperymentu uczenia z danych wyjściowych dwóch wyniki obejmują informacje o lokalizacji magazynu dla obu z nich.</span><span class="sxs-lookup"><span data-stu-id="0891c-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Ponownego trenowania danych wyjściowych][6]

<span data-ttu-id="0891c-196">Diagram 4: Ponownego trenowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0891c-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="0891c-197">Ocena ponownego trenowania wyników</span><span class="sxs-lookup"><span data-stu-id="0891c-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="0891c-198">Po uruchomieniu aplikacji, danych wyjściowych zawiera token adresu URL i skojarzenia zabezpieczeń niezbędnych do uzyskania dostępu wyniki oceny.</span><span class="sxs-lookup"><span data-stu-id="0891c-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="0891c-199">Można wyświetlić wyniki wydajności retrained modelu, łącząc *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z wyników danych wyjściowych dla *output2* (jak pokazano w poprzednim ponownego trenowania obrazu wyjściowego) i wklejanie pełny adres URL na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="0891c-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="0891c-200">Przeanalizuj wyniki do ustalenia, czy nowo trenowanego modelu pełni wystarczająco również zastąpić istniejący.</span><span class="sxs-lookup"><span data-stu-id="0891c-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="0891c-201">Kopiuj *BaseLocation*, *RelativeLocation*, i *SasBlobToken* z wyników dane wyjściowe będą używały ich podczas procesu ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="0891c-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0891c-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0891c-202">Next steps</span></span>
<span data-ttu-id="0891c-203">Jeśli wdrożono usługę sieci web predykcyjnych, klikając **wdrażanie usługi sieci Web [klasyczny]**, zobacz [Retrain usługi sieci web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="0891c-204">Jeśli wdrożono usługę sieci web predykcyjnych, klikając **wdrażanie usługi sieci Web [New]**, zobacz [Retrain nową usługę sieci web za pomocą poleceń cmdlet Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0891c-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
