---
title: "Strumienia danych z usługi Stream Analytics do usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Stream Analytics strumienia danych do usługi Azure Data Lake Store"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="782cf-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics (Strumieniowe przesyłanie danych z obiektu blob usługi Azure Storage do usługi Data Lake Store za pomocą usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="782cf-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="782cf-104">W tym artykule dowiesz się, jak używać usługi Azure Data Lake Store jako dane wyjściowe zadania usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="782cf-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="782cf-105">W tym artykule przedstawiono prosty scenariusz, który będzie odczytywać dane z obiektu blob magazynu Azure (dane wejściowe) i zapisuje dane do usługi Data Lake Store (dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="782cf-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="782cf-106">W tej chwili tworzenia i konfigurowania usługi Data Lake Store generuje Stream Analytics jest obsługiwane tylko w [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="782cf-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="782cf-107">W związku z tym niektórych części tego samouczka zostanie Użyj klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="782cf-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="782cf-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="782cf-108">Prerequisites</span></span>
<span data-ttu-id="782cf-109">Przed przystąpieniem do wykonania kroków opisanych w tym samouczku należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="782cf-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="782cf-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="782cf-110">**An Azure subscription**.</span></span> <span data-ttu-id="782cf-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="782cf-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="782cf-112">**Konto usługi Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="782cf-112">**Azure Storage account**.</span></span> <span data-ttu-id="782cf-113">Kontener obiektów blob z tego konta zostaną użyte do wprowadzania danych w przypadku zadania Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="782cf-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="782cf-114">W tym samouczku założono, że masz konto magazynu o nazwie **storageforasa** i kontener w ramach konta o nazwie **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="782cf-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="782cf-115">Po utworzeniu kontenera, Przekaż przykładowy plik danych do niego.</span><span class="sxs-lookup"><span data-stu-id="782cf-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="782cf-116">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="782cf-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="782cf-117">Postępuj zgodnie z instrukcjami w temacie [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="782cf-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="782cf-118">Załóżmy, że masz konto usługi Data Lake Store o nazwie **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="782cf-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="782cf-119">Tworzenie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="782cf-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="782cf-120">Rozpoczyna się od utworzenia zadanie usługi Stream Analytics, która zawiera źródło danych wejściowych i miejsce docelowe danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="782cf-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="782cf-121">W tym samouczku źródło jest kontenera obiektów blob platformy Azure i miejsce docelowe jest Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="782cf-122">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="782cf-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="782cf-123">W okienku po lewej stronie kliknij **zadania usługi analiza strumienia**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="782cf-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="782cf-124">![Tworzenie zadania usługi analiza strumienia](./media/data-lake-store-stream-analytics/create.job.png "utworzyć zadania usługi analiza strumienia")</span><span class="sxs-lookup"><span data-stu-id="782cf-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="782cf-125">Upewnij się, możesz utworzyć zadania w tym samym regionie co konto magazynu lub spowoduje naliczenie dodatkowych kosztów przenoszenia danych między regionami.</span><span class="sxs-lookup"><span data-stu-id="782cf-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="782cf-126">Tworzenie obiektu Blob danych wejściowych dla zadania</span><span class="sxs-lookup"><span data-stu-id="782cf-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="782cf-127">Otwórz stronę do zadania usługi analiza strumienia, w lewym okienku kliknij **dane wejściowe** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="782cf-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="782cf-128">![Dodawanie danych wejściowych do zadania](./media/data-lake-store-stream-analytics/create.input.1.png "dodać danych wejściowych do zadania")</span><span class="sxs-lookup"><span data-stu-id="782cf-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="782cf-129">Na **wprowadzania nowych** bloku, podaj następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="782cf-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="782cf-130">![Dodawanie danych wejściowych do zadania](./media/data-lake-store-stream-analytics/create.input.2.png "dodać danych wejściowych do zadania")</span><span class="sxs-lookup"><span data-stu-id="782cf-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="782cf-131">Dla **alias wejściowy**, wprowadź unikatową nazwę dla zadania danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="782cf-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="782cf-132">Aby uzyskać **typ źródła**, wybierz pozycję **strumienia danych**.</span><span class="sxs-lookup"><span data-stu-id="782cf-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="782cf-133">Aby uzyskać **źródła**, wybierz pozycję **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="782cf-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="782cf-134">Aby uzyskać **subskrypcji**, wybierz pozycję **Użyj magazynu obiektów blob z bieżącej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="782cf-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="782cf-135">Aby uzyskać **konta magazynu**, wybierz konto magazynu, który został utworzony jako część wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="782cf-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="782cf-136">Aby uzyskać **kontenera**, wybierz kontener, który został utworzony w wybranego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="782cf-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="782cf-137">Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.</span><span class="sxs-lookup"><span data-stu-id="782cf-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="782cf-138">Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.</span><span class="sxs-lookup"><span data-stu-id="782cf-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="782cf-139">Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="782cf-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="782cf-140">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="782cf-140">Click **Create**.</span></span> <span data-ttu-id="782cf-141">Portal teraz dodaje dane wejściowe i testuje połączenie do niego.</span><span class="sxs-lookup"><span data-stu-id="782cf-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="782cf-142">Utwórz dane wyjściowe zadania usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="782cf-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="782cf-143">Otwórz stronę do zadania usługi analiza strumienia, kliknij przycisk **dane wyjściowe** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="782cf-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="782cf-144">![Dodawanie danych wyjściowych do zadania](./media/data-lake-store-stream-analytics/create.output.1.png "dodać danych wyjściowych do zadania")</span><span class="sxs-lookup"><span data-stu-id="782cf-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="782cf-145">Na **nowe dane wyjściowe** bloku, podaj następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="782cf-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="782cf-146">![Dodawanie danych wyjściowych do zadania](./media/data-lake-store-stream-analytics/create.output.2.png "dodać danych wyjściowych do zadania")</span><span class="sxs-lookup"><span data-stu-id="782cf-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="782cf-147">Aby uzyskać **alias wyjściowy**, wprowadź unikatową nazwę dla danych wyjściowych zadania.</span><span class="sxs-lookup"><span data-stu-id="782cf-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="782cf-148">Jest to przyjazna nazwa używana w zapytaniach do kierowania wyników zapytania do tej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="782cf-149">Aby uzyskać **Sink**, wybierz pozycję **usługi Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="782cf-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="782cf-150">Pojawi się autoryzacja dostępu do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="782cf-151">Kliknij przycisk **autoryzować**.</span><span class="sxs-lookup"><span data-stu-id="782cf-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="782cf-152">Na **nowe dane wyjściowe** bloku, podaj następujące wartości w dalszym ciągu.</span><span class="sxs-lookup"><span data-stu-id="782cf-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="782cf-153">![Dodawanie danych wyjściowych do zadania](./media/data-lake-store-stream-analytics/create.output.3.png "dodać danych wyjściowych do zadania")</span><span class="sxs-lookup"><span data-stu-id="782cf-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="782cf-154">Aby uzyskać **nazwa konta**, wybierz utworzone miejsce zadania dane wyjściowe do wysłania do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="782cf-155">Aby uzyskać **wzorzec prefiksu ścieżki**, wprowadź ścieżkę pliku używany do zapisywania plików w ramach określonego konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="782cf-156">Aby uzyskać **format daty**, jeśli token daty jest używany w ścieżce prefiksu, można wybrać format daty, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="782cf-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="782cf-157">Dla **format czasu**, jeśli token czasu używany w ścieżce prefiks określić format czasu, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="782cf-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="782cf-158">Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.</span><span class="sxs-lookup"><span data-stu-id="782cf-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="782cf-159">Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.</span><span class="sxs-lookup"><span data-stu-id="782cf-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="782cf-160">Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="782cf-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="782cf-161">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="782cf-161">Click **Create**.</span></span> <span data-ttu-id="782cf-162">Portal teraz dodaje dane wyjściowe i testuje połączenie do niego.</span><span class="sxs-lookup"><span data-stu-id="782cf-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="782cf-163">Uruchom zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="782cf-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="782cf-164">Aby uruchomić zadanie usługi Stream Analytics, należy uruchomić kwerendę, **zapytania** kartę.</span><span class="sxs-lookup"><span data-stu-id="782cf-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="782cf-165">W tym samouczku, można uruchomić przykładowe zapytanie, zastępując symbole zastępcze zadania danych wejściowych i wyjściowych aliasy, jak pokazano w poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="782cf-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="782cf-166">![Uruchom zapytanie](./media/data-lake-store-stream-analytics/run.query.png ", uruchom zapytanie")</span><span class="sxs-lookup"><span data-stu-id="782cf-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="782cf-167">Kliknij przycisk **zapisać** od góry ekranu, a następnie z **omówienie** , kliknij pozycję **Start**.</span><span class="sxs-lookup"><span data-stu-id="782cf-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="782cf-168">W oknie dialogowym wybierz **czasu niestandardowe**, a następnie ustaw bieżącą datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="782cf-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="782cf-169">![Ustawianie czasu zadania](./media/data-lake-store-stream-analytics/run.query.2.png "ustawić czas pracy")</span><span class="sxs-lookup"><span data-stu-id="782cf-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="782cf-170">Kliknij przycisk **Start** można uruchomić zadania.</span><span class="sxs-lookup"><span data-stu-id="782cf-170">Click **Start** to start the job.</span></span> <span data-ttu-id="782cf-171">Może potrwać kilka minut, aby uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="782cf-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="782cf-172">Aby uruchomić zadanie do pobrania danych z obiektu blob, skopiuj przykładowy plik danych do kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="782cf-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="782cf-173">Można pobrać przykładowy plik danych z [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="782cf-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="782cf-174">W tym samouczku, skopiuj plik **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="782cf-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="782cf-175">Można użyć różnych klientów, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/), aby przekazać dane do kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="782cf-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="782cf-176">Z **omówienie** , w obszarze **monitorowanie**, zobacz przetwarzaniu danych.</span><span class="sxs-lookup"><span data-stu-id="782cf-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="782cf-177">![Zadanie monitora](./media/data-lake-store-stream-analytics/run.query.3.png "zadania monitora")</span><span class="sxs-lookup"><span data-stu-id="782cf-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="782cf-178">Na koniec można sprawdzić, czy dane dane wyjściowe zadania są dostępne w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="782cf-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="782cf-179">![Sprawdź dane wyjściowe](./media/data-lake-store-stream-analytics/run.query.4.png "Sprawdź dane wyjściowe")</span><span class="sxs-lookup"><span data-stu-id="782cf-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="782cf-180">W okienku Eksplorator danych ustawienia w danych wyjściowych Zwróć uwagę, że dane wyjściowe są zapisywane w ścieżce folderu określone w usłudze Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="782cf-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="782cf-181">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="782cf-181">See also</span></span>
* [<span data-ttu-id="782cf-182">Tworzenie klastra usługi HDInsight do użycia usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="782cf-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
