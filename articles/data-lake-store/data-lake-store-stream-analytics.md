---
title: "aaaStream danych z usługi Stream Analytics do usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Stream Analytics toostream danych do usługi Azure Data Lake Store"
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
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="0f9c0-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics (Strumieniowe przesyłanie danych z obiektu blob usługi Azure Storage do usługi Data Lake Store za pomocą usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="0f9c0-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="0f9c0-104">W tym artykule dowiesz się, jak toouse Azure Data Lake przechowywać jako dane wyjściowe zadania usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="0f9c0-105">W tym artykule przedstawiono prosty scenariusz służącą do odczytywania danych z obiektu blob magazynu Azure (dane wejściowe), a następnie zapisuje hello danych tooData Lake Store (dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="0f9c0-106">W tej chwili tworzenia i konfigurowania usługi Data Lake Store generuje Stream Analytics jest obsługiwane tylko w hello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="0f9c0-107">W związku z tym niektórych części tego samouczka zostanie użyty hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="0f9c0-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f9c0-108">Prerequisites</span></span>
<span data-ttu-id="0f9c0-109">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="0f9c0-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="0f9c0-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-110">**An Azure subscription**.</span></span> <span data-ttu-id="0f9c0-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0f9c0-112">**Konto usługi Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-112">**Azure Storage account**.</span></span> <span data-ttu-id="0f9c0-113">Zadanie Stream Analytics będzie używać kontenera obiektów blob z konta tooinput danych.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="0f9c0-114">W tym samouczku założono, że masz konto magazynu o nazwie **storageforasa** i wywołać kontenera w ramach konta hello **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="0f9c0-115">Po utworzeniu kontenera hello, Przekaż przykładowe dane pliku tooit.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="0f9c0-116">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="0f9c0-117">Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="0f9c0-118">Załóżmy, że masz konto usługi Data Lake Store o nazwie **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="0f9c0-119">Tworzenie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="0f9c0-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="0f9c0-120">Rozpoczyna się od utworzenia zadanie usługi Stream Analytics, która zawiera źródło danych wejściowych i miejsce docelowe danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="0f9c0-121">W tym samouczku hello źródła jest kontenera obiektów blob platformy Azure i miejsce docelowe hello jest Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="0f9c0-122">Zaloguj się na toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0f9c0-123">W okienku po lewej stronie powitania kliknij **zadania usługi analiza strumienia**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="0f9c0-124">![Tworzenie zadania usługi analiza strumienia](./media/data-lake-store-stream-analytics/create.job.png "utworzyć zadania usługi analiza strumienia")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f9c0-125">Upewnij się, że zadania tworzenia w hello tym samym regionie co konto magazynu hello lub spowoduje naliczenie dodatkowych kosztów przenoszenia danych między regionami.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="0f9c0-126">Tworzenie obiektu Blob danych wejściowych hello zadania</span><span class="sxs-lookup"><span data-stu-id="0f9c0-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="0f9c0-127">Otwórz hello hello zadania usługi analiza strumienia, w okienku po lewej stronie powitania kliknij hello **dane wejściowe** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="0f9c0-128">![Dodaj zadanie wejściowych tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "dodać zadania tooyour wejściowych")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="0f9c0-129">Na powitania **wprowadzania nowych** bloku, podaj następujące wartości hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="0f9c0-130">![Dodaj zadanie wejściowych tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "dodać zadania tooyour wejściowych")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="0f9c0-131">Dla **alias wejściowy**, wprowadź unikatową nazwę dla zadania hello w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="0f9c0-132">Aby uzyskać **typ źródła**, wybierz pozycję **strumienia danych**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="0f9c0-133">Aby uzyskać **źródła**, wybierz pozycję **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="0f9c0-134">Aby uzyskać **subskrypcji**, wybierz pozycję **Użyj magazynu obiektów blob z bieżącej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="0f9c0-135">Aby uzyskać **konta magazynu**, wybierz konto magazynu hello, utworzony jako część hello wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="0f9c0-136">Dla **kontenera**, wybierz kontener hello, który został utworzony w hello wybranego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="0f9c0-137">Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="0f9c0-138">Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="0f9c0-139">Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="0f9c0-140">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-140">Click **Create**.</span></span> <span data-ttu-id="0f9c0-141">Hello portal teraz dodaje dane wejściowe hello i testy hello tooit połączenia.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="0f9c0-142">Utwórz dane wyjściowe zadania hello usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0f9c0-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="0f9c0-143">Otwórz stronę hello zadania usługi analiza strumienia hello, kliknij przycisk hello **dane wyjściowe** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="0f9c0-144">![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "dodać zadania tooyour danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="0f9c0-145">Na powitania **nowe dane wyjściowe** bloku, podaj następujące wartości hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="0f9c0-146">![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "dodać zadania tooyour danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="0f9c0-147">Dla **alias wyjściowy**, wprowadź unikatową nazwę hello dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="0f9c0-148">Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="0f9c0-149">Aby uzyskać **Sink**, wybierz pozycję **usługi Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="0f9c0-150">Zostanie wyświetlony monit o tooauthorize będzie można uzyskać dostęp do konta tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="0f9c0-151">Kliknij przycisk **autoryzować**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="0f9c0-152">Na powitania **nowe dane wyjściowe** bloku kontynuować hello tooprovide następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="0f9c0-153">![Dodawanie danych wyjściowych zadania tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "dodać zadania tooyour danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="0f9c0-154">Aby uzyskać **nazwa konta**, wybierz konto usługi Data Lake Store hello utworzone miejsce toobe dane wyjściowe zadania hello wysyłane do.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="0f9c0-155">Dla **wzorzec prefiksu ścieżki**, wprowadź toowrite użyta ścieżka pliku pliki w obrębie hello określone konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="0f9c0-156">Aby uzyskać **format daty**, jeśli token daty jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="0f9c0-157">Dla **format czasu**, jeśli token czasu używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="0f9c0-158">Aby uzyskać **format serializacji zdarzeń**, wybierz pozycję **CSV**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="0f9c0-159">Aby uzyskać **ogranicznik**, wybierz pozycję **kartę**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="0f9c0-160">Aby uzyskać **kodowanie**, wybierz pozycję **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="0f9c0-161">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-161">Click **Create**.</span></span> <span data-ttu-id="0f9c0-162">Hello portal teraz dodaje dane wyjściowe hello i testy hello tooit połączenia.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="0f9c0-163">Uruchom zadanie usługi Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="0f9c0-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="0f9c0-164">toorun zadanie usługi Stream Analytics, należy uruchomić zapytania z hello **zapytania** kartę. W tym samouczku, można uruchomić hello przykładowe zapytanie, zastępując symbole zastępcze hello z hello zadania wejściowymi i wyjściowymi aliasy, jak pokazano w poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="0f9c0-165">![Uruchom zapytanie](./media/data-lake-store-stream-analytics/run.query.png ", uruchom zapytanie")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="0f9c0-166">Kliknij przycisk **zapisać** od góry hello hello ekranu, a następnie z hello **omówienie** , kliknij pozycję **Start**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="0f9c0-167">W oknie dialogowym hello, wybierz **czasu niestandardowe**, a następnie ustaw hello bieżącą datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="0f9c0-168">![Ustawianie czasu zadania](./media/data-lake-store-stream-analytics/run.query.2.png "ustawić czas pracy")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="0f9c0-169">Kliknij przycisk **Start** toostart hello zadania.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="0f9c0-170">Może potrwać tooa kilka minut toostart hello zadania.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="0f9c0-171">tootrigger hello zadania toopick hello danych z obiektu blob hello, skopiuj kontenera obiektów blob toohello plików przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="0f9c0-172">Możesz pobrać przykładowy plik danych ze hello [repozytorium Git programu Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="0f9c0-173">W tym samouczku, skopiuj plik hello **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="0f9c0-174">Można użyć różnych klientów, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/), tooupload danych tooa obiektów blob kontenera.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="0f9c0-175">Z hello **omówienie** , w obszarze **monitorowanie**, zobacz przetwarzaniu hello danych.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="0f9c0-176">![Zadanie monitora](./media/data-lake-store-stream-analytics/run.query.3.png "zadania monitora")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="0f9c0-177">Na koniec można sprawdzić, czy dane wyjściowe zadania hello jest dostępna w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0f9c0-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="0f9c0-178">![Sprawdź dane wyjściowe](./media/data-lake-store-stream-analytics/run.query.4.png "Sprawdź dane wyjściowe")</span><span class="sxs-lookup"><span data-stu-id="0f9c0-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="0f9c0-179">W okienku Eksplorator danych hello, zwróć uwagę, że hello output, ścieżka folderu tooa zapisywane jako określono w hello ustawienia danych wyjściowych usługi Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="0f9c0-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="0f9c0-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0f9c0-180">See also</span></span>
* [<span data-ttu-id="0f9c0-181">Utwórz toouse klastra usługi HDInsight usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0f9c0-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
