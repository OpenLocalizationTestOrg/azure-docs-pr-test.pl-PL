---
title: "aaaAzure integracji usługi analiza strumienia i Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toouse funkcja zdefiniowana przez użytkownika i uczenia maszynowego w zadaniu Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="ee2d5-103">Wykonywanie analiz wskaźniki nastrojów klientów przy użyciu usługi Azure Stream Analytics i usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ee2d5-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="ee2d5-104">W tym artykule opisano sposób konfigurowania proste zadanie usługi analiza strumienia Azure, której zintegrowano usługi Azure Machine Learning tooquickly.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="ee2d5-105">Korzystają z modelu uczenia maszynowego wskaźniki nastrojów klientów analytics z hello dane przesyłane strumieniowo tekst tooanalyze Cortana Intelligence Gallery i określić hello wynik wskaźniki nastrojów klientów w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="ee2d5-106">Przy użyciu pakietu Cortana Intelligence Suite hello pozwala wykonać to zadanie, nie martwiąc się o hello mogli dokładnie zapoznać tworzenia modelu analizy wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="ee2d5-107">Należy zastosować, Dowiedz się od tooscenarios tego artykułu, takich jak te:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="ee2d5-108">Analizowanie w czasie rzeczywistym wskaźniki nastrojów klientów na przesyłanie strumieniowe danych Twitter.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="ee2d5-109">Analizowanie rekordy klienta rozmowy z pracownikami działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="ee2d5-110">Ocena komentarze dotyczące fora, blogi i wideo.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="ee2d5-111">Wiele innych w czasie rzeczywistym, predykcyjnej oceniania scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="ee2d5-112">W przypadku rzeczywistych jak hello danych bezpośrednio z serwisem Twitter strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="ee2d5-113">Samouczek hello toosimplify, możemy napisanych go tak, aby hello zadanie analizy przesyłania strumieniowego pobiera tweetów z pliku CSV w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="ee2d5-114">Można utworzyć pliku CSV, lub można użyć przykładowy plik CSV, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![Przykładowe tweetów w pliku CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="ee2d5-116">utworzonego zadania przesyłania strumieniowego Analytics Hello stosuje modelu analizy wskaźniki nastrojów klientów hello w funkcji zdefiniowanej przez użytkownika (UDF) na powitania tekst danych z magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="ee2d5-117">dane wyjściowe Hello (hello wynik analizy wskaźniki nastrojów klientów hello) są zapisywane toohello tego samego magazynu obiektów blob w innym pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="ee2d5-118">Witaj poniższym rysunku pokazano tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="ee2d5-119">Jak wspomniano, dla scenariusza bardziej realistyczne można zastąpić strumienia danych Twitter z wejściem Azure Event Hubs magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="ee2d5-120">Ponadto można zbudować [Microsoft Power BI](https://powerbi.microsoft.com/) w czasie rzeczywistym wizualizację hello agregacji wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Omówienie integracji uczenia maszynowego usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="ee2d5-122">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee2d5-122">Prerequisites</span></span>
<span data-ttu-id="ee2d5-123">Przed rozpoczęciem upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="ee2d5-124">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-124">An active Azure subscription.</span></span>
* <span data-ttu-id="ee2d5-125">Plik CSV z niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-125">A CSV file with some data in it.</span></span> <span data-ttu-id="ee2d5-126">Możesz pobrać plik hello przedstawiona wcześniej z [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), lub można utworzyć własny plik.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="ee2d5-127">W tym artykule przyjęto założenie, że używasz hello pliku z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="ee2d5-128">Na wysokim poziomie toocomplete hello zadania zostało to pokazane w tym artykule należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="ee2d5-129">Tworzenie konta magazynu platformy Azure i kontener magazynu obiektów blob i przekaż kontenera toohello wejściowego pliku w formacie CSV.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="ee2d5-130">Dodawanie modelu analizy wskaźniki nastrojów klientów z roboczym usługi Azure Machine Learning tooyour Cortana Intelligence Gallery hello i wdrożyć ten model jako usługę sieci web w hello obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="ee2d5-131">Utwórz zadanie usługi Stream Analytics, które wymaga tej usługi sieci web jako funkcję w kolejności toodetermine wskaźniki nastrojów klientów hello wprowadzania tekstu.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="ee2d5-132">Uruchom zadanie usługi Stream Analytics hello i sprawdź hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="ee2d5-133">Tworzenie kontenera magazynu i przekazywanie pliku wejściowego hello CSV</span><span class="sxs-lookup"><span data-stu-id="ee2d5-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="ee2d5-134">W tym kroku można użyć dowolnego pliku CSV, takich jak hello dostępna z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="ee2d5-135">W portalu Azure hello, kliknij przycisk **nowy** &gt; **magazynu** &gt; **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![Utwórz nowe konto magazynu](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="ee2d5-137">Podaj nazwę (`samldemo` w przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="ee2d5-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="ee2d5-138">Nazwa Hello można użyć tylko małe litery i cyfry, i między Azure musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="ee2d5-139">Wybierz istniejącą grupę zasobów i określ lokalizację.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="ee2d5-140">Dla lokalizacji, zaleca się wszystkie zasoby hello utworzone w tym samouczku hello sam lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![Podaj szczegóły konta magazynu](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="ee2d5-142">W portalu Azure hello wybierz konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="ee2d5-143">W bloku konto magazynu hello, kliknij przycisk **kontenery** , a następnie kliknij przycisk  **+ &nbsp;kontenera** toocreate magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![Tworzenie kontenera obiektów blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="ee2d5-145">Podaj nazwę kontenera hello (`azuresamldemoblob` w przykładzie hello) i sprawdź, czy **dostęp typu** ustawiono zbyt**obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="ee2d5-146">Gdy skończysz, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-146">When you're done, click **OK**.</span></span>

    ![Określ szczegóły kontenera obiektów blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="ee2d5-148">W hello **kontenery** bloku, nowy kontener select hello, która otwiera blok powitania dla tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="ee2d5-149">Kliknij pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-149">Click **Upload**.</span></span>

    ![Przekaż przycisk kontenera](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="ee2d5-151">W hello **przekazywanie obiektu blob** bloku, określ plik CSV hello mają toouse w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="ee2d5-152">Dla **typu obiektu Blob**, wybierz pozycję **blokowych obiektów blob** i zestaw hello bloku rozmiar too4 MB, co jest wystarczająca dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![Przekaż plik obiektu blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="ee2d5-154">Kliknij przycisk hello **przekazać** przycisk u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="ee2d5-155">Dodawanie modelu analizy hello wskaźniki nastrojów klientów z hello Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="ee2d5-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="ee2d5-156">Teraz, hello przykładowe dane są w obiekcie blob, można włączyć model analizy wskaźniki nastrojów klientów hello w Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="ee2d5-157">Przejdź toohello [modelu analizy predykcyjnej wskaźniki nastrojów klientów](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) strony w hello Cortana Intelligence Gallery.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="ee2d5-158">Kliknij przycisk **Otwórz w Studio**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-158">Click **Open in Studio**.</span></span>  
   
   ![Strumienia uczenia maszynowego analizy, otwórz Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="ee2d5-160">Zaloguj się w obszarze roboczym toohello toogo.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="ee2d5-161">Wybierz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-161">Select a location.</span></span>

4. <span data-ttu-id="ee2d5-162">Kliknij przycisk **Uruchom** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="ee2d5-163">Uruchamia proces Hello, co trwa około minuty.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-163">hello process runs, which takes about a minute.</span></span>

   ![Uruchom eksperyment w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="ee2d5-165">Po hello proces został uruchomiony pomyślnie, wybierz **wdrażanie usługi sieci Web** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![Wdrażanie eksperymentu w usłudze Machine Learning Studio jako usługę sieci web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="ee2d5-167">toovalidate, który hello wskaźniki nastrojów klientów modelu analytics jest gotowy toouse kliknij hello **testu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="ee2d5-168">Przekaż dane wejściowe, takie jak "Świetnie Microsoft".</span><span class="sxs-lookup"><span data-stu-id="ee2d5-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Test eksperymentu w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="ee2d5-170">Jeśli hello test działa, zostanie wyświetlony wynik toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![wyniki testu w usłudze Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="ee2d5-172">W hello **aplikacji** kolumny, kliknij przycisk hello **programu Excel 2010 lub skoroszyt w starszej** toodownload łącze skoroszytu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="ee2d5-173">Witaj skoroszyt zawiera klucz hello interfejsu API i hello adres URL należy nowsze tooset hello zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, szybkiego dostępu](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="ee2d5-175">Utwórz zadanie usługi Stream Analytics, który używa modelu uczenia maszynowego hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="ee2d5-176">Można teraz utworzyć zadanie usługi Stream Analytics odczytujący hello tweetów przykładowe z pliku CSV hello w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="ee2d5-177">Utwórz zadanie hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-177">Create hello job</span></span>

1. <span data-ttu-id="ee2d5-178">Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee2d5-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="ee2d5-179">Kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Azure portalu ścieżkę pobierania tooa nowego zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="ee2d5-181">Nazwa zadania hello `azure-sa-ml-demo`, określ subskrypcję, określ istniejącą grupę zasobów lub Utwórz nową i wybierz lokalizację hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![Określ ustawienia nowego zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="ee2d5-183">Skonfiguruj zadania hello w danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="ee2d5-183">Configure hello job input</span></span>
<span data-ttu-id="ee2d5-184">zadanie Hello pobiera jej danych wejściowych z pliku CSV hello czy przesłany wcześniejszych tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="ee2d5-185">Po hello zadania został utworzony, w obszarze **topologii zadania** w bloku zadania powitania kliknij hello **dane wejściowe** pole.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Pole "Dane wejściowe" w bloku zadania usługi analiza strumienia](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="ee2d5-187">W hello **dane wejściowe** bloku, kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![Dodawanie przycisku do dodawania zadania usługi analiza strumienia wejściowego toohello](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="ee2d5-189">Wypełnianie hello **wprowadzania nowych** bloku następującymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="ee2d5-190">**Alias wejściowy**: Użyj nazwy hello `datainput`.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="ee2d5-191">**Typ źródła**: Wybierz **strumienia danych**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="ee2d5-192">**Źródło**: Wybierz **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="ee2d5-193">**Opcji importowania**: Wybierz **Użyj magazynu obiektów blob z bieżącej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="ee2d5-194">**Konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-194">**Storage account**.</span></span> <span data-ttu-id="ee2d5-195">Wybierz utworzone wcześniej konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="ee2d5-196">**Kontener**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-196">**Container**.</span></span> <span data-ttu-id="ee2d5-197">Kontener hello wybierz wcześniej utworzony (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="ee2d5-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="ee2d5-198">**Format serializacji zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-198">**Event serialization format**.</span></span> <span data-ttu-id="ee2d5-199">Wybierz **CSV**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-199">Select **CSV**.</span></span>

    ![Ustawienia dla nowego zadania danych wejściowych.](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="ee2d5-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="ee2d5-202">Skonfiguruj hello dane wyjściowe zadania</span><span class="sxs-lookup"><span data-stu-id="ee2d5-202">Configure hello job output</span></span>
<span data-ttu-id="ee2d5-203">Witaj zadania wysyła wyników toohello sam obiektu blob magazynu, w którym pobiera dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="ee2d5-204">W obszarze **topologii zadania** w bloku zadania powitania kliknij hello **dane wyjściowe** pole.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Utwórz nowe dane wyjściowe zadania przesyłania strumieniowego usługi analiza](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="ee2d5-206">W hello **dane wyjściowe** bloku, kliknij przycisk **+ Dodaj**, a następnie dodaj wyjście z aliasem hello `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="ee2d5-207">Aby uzyskać **Sink**, wybierz pozycję **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="ee2d5-208">Następnie wypełnij hello reszty hello output ustawień za pomocą hello takie same wartości, używane do magazynu obiektów blob powitania dla danych wejściowych:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="ee2d5-209">**Konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-209">**Storage account**.</span></span> <span data-ttu-id="ee2d5-210">Wybierz utworzone wcześniej konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="ee2d5-211">**Kontener**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-211">**Container**.</span></span> <span data-ttu-id="ee2d5-212">Kontener hello wybierz wcześniej utworzony (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="ee2d5-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="ee2d5-213">**Format serializacji zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-213">**Event serialization format**.</span></span> <span data-ttu-id="ee2d5-214">Wybierz **CSV**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-214">Select **CSV**.</span></span>

   ![Ustawienia dla nowego dane wyjściowe zadania](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="ee2d5-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="ee2d5-217">Dodawanie funkcji Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="ee2d5-218">Wcześniej opublikowaniu usługi sieci web tooa modelu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="ee2d5-219">W naszym scenariuszu po uruchomieniu zadanie analizy strumienia hello wysyła każdego tweet próbki z hello usługi sieci web toohello wejściowy do analizy wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="ee2d5-220">usługi sieci web uczenie maszynowe Hello zwraca wskaźniki nastrojów klientów (`positive`, `neutral`, lub `negative`) i prawdopodobieństwo tweet hello jest dodatnia.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="ee2d5-221">W tej części samouczka hello można zdefiniować funkcję hello zadanie analizy strumienia.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="ee2d5-222">Funkcja Hello można wywołanej toosend tweet toohello usługi sieci web i wrócić hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="ee2d5-223">Upewnij się, że masz hello klucza usługi sieci web adres URL i interfejsu API pobranego wcześniej hello skoroszytu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="ee2d5-224">Zwraca toohello zadania omówienie bloku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="ee2d5-225">W obszarze **ustawienia**, wybierz pozycję **funkcje** , a następnie kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Dodaj zadanie usługi Stream Analytics toohello — funkcja](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="ee2d5-227">Wprowadź `sentiment` jako hello alias funkcji i wypełnianie hello reszty bloku hello przy użyciu następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="ee2d5-228">**Typ funkcji**: Wybierz **uczenie Maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="ee2d5-229">**Opcji importowania**: Wybierz **importu z innej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="ee2d5-230">Dzięki temu można szansy tooenter hello URL i klucza.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="ee2d5-231">**Adres URL**: Wklej adres URL usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="ee2d5-232">**Klucz**: Wklej w kluczu hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-232">**Key**: Paste in hello API key.</span></span>
  
    ![Ustawienia dotyczące dodawania zadania usługi analiza strumienia toohello funkcji Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="ee2d5-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="ee2d5-235">Utwórz zapytanie tootransform hello danych</span><span class="sxs-lookup"><span data-stu-id="ee2d5-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="ee2d5-236">Analiza strumienia używa danych wejściowych deklaratywne kwerendy SQL na podstawie tooexamine hello i go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="ee2d5-237">W tej sekcji utworzysz kwerendę, która odczytuje tweet każdej z danych wejściowych, a następnie wywołuje hello uczenia maszynowego funkcja tooperform wskaźniki nastrojów klientów analizy.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="ee2d5-238">Zapytanie Hello wysyła następnie toohello wynik hello output zdefiniowania (magazynu obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="ee2d5-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="ee2d5-239">Zwraca toohello zadania omówienie bloku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="ee2d5-240">W obszarze **topologii zadania**, kliknij przycisk hello **zapytania** pole.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Utwórz zapytanie dotyczące zadanie analizy przesyłania strumieniowego](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="ee2d5-242">Wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="ee2d5-243">zapytania Hello wywołuje funkcję hello utworzonym wcześniej (`sentiment`) w kolejności tooperform wskaźniki nastrojów klientów analizy w każdym tweet w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="ee2d5-244">Kliknij przycisk **zapisać** toosave hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="ee2d5-245">Uruchom zadanie usługi Stream Analytics hello i sprawdź dane wyjściowe hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="ee2d5-246">Można teraz uruchomić zadania Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="ee2d5-247">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-247">Start hello job</span></span>
1. <span data-ttu-id="ee2d5-248">Zwraca toohello zadania omówienie bloku.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="ee2d5-249">Kliknij przycisk **Start** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-249">Click **Start** at hello top of hello blade.</span></span>

    ![Utwórz zapytanie dotyczące zadanie analizy przesyłania strumieniowego](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="ee2d5-251">W hello **rozpoczęcia zadania**, wybierz pozycję **niestandardowe**, a następnie wybierz jeden dzień toowhen poprzednich przesłanych magazynu tooblob pliku CSV hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="ee2d5-252">Gdy wszystko będzie gotowe, kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="ee2d5-253">Sprawdź dane wyjściowe hello</span><span class="sxs-lookup"><span data-stu-id="ee2d5-253">Check hello output</span></span>
1. <span data-ttu-id="ee2d5-254">Let hello zadanie było uruchamiane kilka minut, aż zostanie wyświetlony działania w hello **monitorowanie** pole.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="ee2d5-255">Jeśli masz narzędzie normalnie korzystać tooexamine hello zawartość magazynu obiektów blob, użyj tego narzędzia tooexamine hello `azuresamldemoblob` kontenera.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="ee2d5-256">Alternatywnie hello następujące kroki w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="ee2d5-257">W portalu hello Znajdź hello `samldemo` magazynu konta, a w ramach konta hello Znajdź hello `azuresamldemoblob` kontenera.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="ee2d5-258">Zobacz dwa pliki w kontenerze hello: hello plik zawierający hello próbki tweetów i plik CSV wygenerowany przez zadanie usługi Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="ee2d5-259">Kliknij prawym przyciskiem myszy hello wygenerowany plik, a następnie wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Pobierz dane wyjściowe zadania CSV z magazynu obiektów Blob](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="ee2d5-261">Otwórz hello wygenerowany plik CSV.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-261">Open hello generated CSV file.</span></span> <span data-ttu-id="ee2d5-262">Zostanie wyświetlony ekran podobny do hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-262">You see something like hello following example:</span></span>  
   
   ![Wyświetl Stream Analytics Machine Learning, CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="ee2d5-264">Wyświetlaj metryki</span><span class="sxs-lookup"><span data-stu-id="ee2d5-264">View metrics</span></span>
<span data-ttu-id="ee2d5-265">Można również wyświetlić metryk powiązanych funkcji usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="ee2d5-266">Witaj następujących metryk powiązanych funkcji są wyświetlane w hello **monitorowanie** pole w bloku zadania hello:</span><span class="sxs-lookup"><span data-stu-id="ee2d5-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="ee2d5-267">**Funkcja żądania** wskazuje hello liczbę żądań wysłanych tooa usługi sieci web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="ee2d5-268">**Działania zdarzenia** wskazuje hello liczby zdarzeń w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="ee2d5-269">Domyślnie tooa każdego żądania usługi sieci web Machine Learning zawiera zapasową too1, 000 zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ee2d5-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="ee2d5-270">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee2d5-270">Next steps</span></span>

* [<span data-ttu-id="ee2d5-271">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="ee2d5-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ee2d5-272">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ee2d5-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ee2d5-273">Integracja interfejsu API REST i uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="ee2d5-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="ee2d5-274">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ee2d5-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



