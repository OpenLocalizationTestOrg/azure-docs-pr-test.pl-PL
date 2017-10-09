---
title: "pulpit nawigacyjny usługi BI aaaPower na platformie Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Użyj w czasie rzeczywistym przesyłania strumieniowego usługi Power BI pulpitu nawigacyjnego toogather analizy biznesowej i analizować dane dużych zadania usługi analiza strumienia."
keywords: pulpitu nawigacyjnego Analytics, pulpit nawigacyjny w czasie rzeczywistym
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="581a7-104">Strumienia analizy i usługi Power BI: pulpitu nawigacyjnego analytics w czasie rzeczywistym do strumieniowego przesyłania danych</span><span class="sxs-lookup"><span data-stu-id="581a7-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="581a7-105">Usługa Azure Stream Analytics umożliwia tootake zaletą jedną hello wiodące narzędzia do analizy biznesowej, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="581a7-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="581a7-106">W tym artykule dowiesz się, jak utworzyć przy użyciu usługi Power BI jako dane wyjściowe dla Twojego zadania usługi analiza strumienia Azure narzędzia do analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="581a7-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="581a7-107">Możesz także dowiedzieć się, jak toocreate i pulpit nawigacyjny w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="581a7-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="581a7-108">Ten artykuł stanowi kontynuację hello Stream Analytics [wykrywanie oszustw w czasie rzeczywistym](stream-analytics-real-time-fraud-detection.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="581a7-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="581a7-109">Jego oparty na powitania przepływu pracy utworzone w tym samouczku i dodaje dane wyjściowe, dzięki czemu można zwizualizować fałszywych połączeń telefonicznych, które są wykrywane przez zadanie analizy przesyłania strumieniowego usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="581a7-110">Możesz obserwować [wideo](https://www.youtube.com/watch?v=SGUpT-a99MA) przedstawiający tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="581a7-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="581a7-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="581a7-111">Prerequisites</span></span>

<span data-ttu-id="581a7-112">Przed rozpoczęciem upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="581a7-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="581a7-113">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="581a7-113">An Azure account.</span></span>
* <span data-ttu-id="581a7-114">Konto usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-114">An account for Power BI.</span></span> <span data-ttu-id="581a7-115">Można użyć konta służbowego lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="581a7-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="581a7-116">Ukończoną wersję hello [wykrywanie oszustw w czasie rzeczywistym](stream-analytics-real-time-fraud-detection.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="581a7-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="581a7-117">Samouczek Hello zawiera aplikację, która generuje metadanych fikcyjne połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="581a7-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="581a7-118">W samouczku hello tworzenia Centrum zdarzeń i wysłać hello przesyłania strumieniowego Centrum zdarzeń toohello danych połączenia telefonicznego.</span><span class="sxs-lookup"><span data-stu-id="581a7-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="581a7-119">Możesz napisać zapytanie wykrywające fałszywych wywołania (wywołania z hello tę samą liczbę na powitania sam czas w różnych lokalizacjach).</span><span class="sxs-lookup"><span data-stu-id="581a7-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="581a7-120">Dodawanie danych wyjściowych usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="581a7-120">Add Power BI output</span></span>
<span data-ttu-id="581a7-121">W samouczku wykrywanie oszustw w czasie rzeczywistym hello hello wyjściowe są wysyłane tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="581a7-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="581a7-122">W tej sekcji możesz dodać dane wyjściowe, które wysyła informacje tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="581a7-123">Hello portalu Azure Otwórz hello zadanie analizy przesyłania strumieniowego, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="581a7-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="581a7-124">Jeśli używasz hello sugerowana nazwa zadania hello nosi nazwę `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="581a7-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="581a7-125">Wybierz hello **dane wyjściowe** polu w środku hello hello zadania w pulpicie nawigacyjnym, a następnie wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="581a7-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="581a7-126">Aby uzyskać **Alias wyjściowy**, wprowadź `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="581a7-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="581a7-127">Można użyć innej nazwy.</span><span class="sxs-lookup"><span data-stu-id="581a7-127">You can use a different name.</span></span> <span data-ttu-id="581a7-128">Jeśli to zrobisz, zanotuj, ponieważ potrzebna nazwa hello później.</span><span class="sxs-lookup"><span data-stu-id="581a7-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="581a7-129">W obszarze **Sink**, wybierz pozycję **usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="581a7-129">Under **Sink**, select **Power BI**.</span></span>

   ![Utworzenie danych wyjściowych dla usługi Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="581a7-131">Kliknij przycisk **autoryzować**.</span><span class="sxs-lookup"><span data-stu-id="581a7-131">Click **Authorize**.</span></span>

    <span data-ttu-id="581a7-132">Otwiera okno, w którym można podać poświadczenia platformy Azure dla konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="581a7-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Wprowadź poświadczenia dla dostępu tooPower analizy Biznesowej](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="581a7-134">Wprowadź swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="581a7-134">Enter your credentials.</span></span> <span data-ttu-id="581a7-135">Należy pamiętać, a następnie wprowadź swoje poświadczenia, użytkownik jest również nadanie tooaccess zadanie analizy przesyłania strumieniowego toohello uprawnień obszaru usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="581a7-136">Gdy nastąpi powrót toohello **nowe dane wyjściowe** bloku, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="581a7-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="581a7-137">**Obszar roboczy grupy**: Wybierz obszar roboczy w dzierżawie usługi Power BI miejscu toocreate hello dataset.</span><span class="sxs-lookup"><span data-stu-id="581a7-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="581a7-138">**Nazwa zestawu danych**: wprowadź `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="581a7-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="581a7-139">Można użyć innej nazwy.</span><span class="sxs-lookup"><span data-stu-id="581a7-139">You can use a different name.</span></span> <span data-ttu-id="581a7-140">Jeśli to zrobisz, zanotuj jej na później.</span><span class="sxs-lookup"><span data-stu-id="581a7-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="581a7-141">**Nazwa tabeli**: wprowadź `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="581a7-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="581a7-142">Obecnie usługa Power BI dane wyjściowe zadania usługi analiza strumienia może mieć tylko jedną tabelę w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="581a7-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Obszar roboczy PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="581a7-144">Usługa Power BI udostępnia zestaw danych hello tabeli, które mają takie same nazwy jako hello te, które określisz w zadaniu Stream Analytics hello, zostaną zastąpione hello istniejące grupy.</span><span class="sxs-lookup"><span data-stu-id="581a7-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="581a7-145">Zaleca się, że nie jawnie utworzysz ten zestaw danych i tabeli na koncie usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="581a7-146">Są one tworzone automatycznie podczas uruchamiania zadania usługi analiza strumienia i hello zadanie uruchamia pompującego dane wyjściowe do usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="581a7-147">Jeśli zadania kwerenda nie zwróciła żadnych wyników, hello zestawu danych i tabeli nie są tworzone.</span><span class="sxs-lookup"><span data-stu-id="581a7-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="581a7-148">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="581a7-148">Click **Create**.</span></span>

<span data-ttu-id="581a7-149">zestaw danych Hello jest utworzona z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="581a7-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="581a7-150">**defaultRetentionPolicy: BasicFIFO**: dane są FIFO, używając maksymalnie 200 000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="581a7-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="581a7-151">**właściwości defaultMode: pushStreaming**: hello zestawu danych obsługuje przesyłania strumieniowego Kafelki i tradycyjnych elementy wizualne na podstawie raportu ()</span><span class="sxs-lookup"><span data-stu-id="581a7-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="581a7-152">Push).</span><span class="sxs-lookup"><span data-stu-id="581a7-152">push).</span></span>

<span data-ttu-id="581a7-153">Obecnie nie można utworzyć zestawy danych z innych flagi.</span><span class="sxs-lookup"><span data-stu-id="581a7-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="581a7-154">Aby uzyskać więcej informacji na temat zestawów danych usługi Power BI, zobacz hello [API REST usługi Power BI](https://msdn.microsoft.com/library/mt203562.aspx) odwołania.</span><span class="sxs-lookup"><span data-stu-id="581a7-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="581a7-155">Pisanie zapytań hello</span><span class="sxs-lookup"><span data-stu-id="581a7-155">Write hello query</span></span>

1. <span data-ttu-id="581a7-156">Zamknij hello **dane wyjściowe** bloku i zwracany toohello bloku zadania.</span><span class="sxs-lookup"><span data-stu-id="581a7-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="581a7-157">Kliknij przycisk hello **zapytania** pole.</span><span class="sxs-lookup"><span data-stu-id="581a7-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="581a7-158">Wprowadź hello następującego zapytania.</span><span class="sxs-lookup"><span data-stu-id="581a7-158">Enter hello following query.</span></span> <span data-ttu-id="581a7-159">To zapytanie jest podobne toohello samosprzężenie utworzona kwerenda hello wykrywanie oszustw samouczka.</span><span class="sxs-lookup"><span data-stu-id="581a7-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="581a7-160">Hello różnicą jest to zapytanie i wysyła wyniki toohello nowe dane wyjściowe utworzonego (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="581a7-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="581a7-161">Jeśli hello dane wejściowe nie nazwy `CallStream` w samouczku wykrywanie oszustw hello, należy zastąpić nazwę `CallStream` w hello **FROM** i **JOIN** klauzule hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="581a7-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="581a7-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="581a7-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="581a7-163">Zapytanie hello testu</span><span class="sxs-lookup"><span data-stu-id="581a7-163">Test hello query</span></span>
<span data-ttu-id="581a7-164">Ta sekcja jest opcjonalna, ale zalecana.</span><span class="sxs-lookup"><span data-stu-id="581a7-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="581a7-165">Jeżeli hello TelcoStreaming aplikacji nie jest obecnie uruchomiona, należy ją uruchomić, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="581a7-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="581a7-166">Otwórz okno poleceń.</span><span class="sxs-lookup"><span data-stu-id="581a7-166">Open a command window.</span></span>
    * <span data-ttu-id="581a7-167">Przejdź toohello folder zawierający hello telcogenerator.exe i telcodatagen.exe.config zmodyfikowane pliki.</span><span class="sxs-lookup"><span data-stu-id="581a7-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="581a7-168">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="581a7-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="581a7-169">W hello **zapytania** bloku, kliknij przycisk Dalej toohello punktów hello `CallStream` danych wejściowych, a następnie wybierz **przykładowe dane z danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="581a7-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="581a7-170">Określ wartość trzy minuty danych i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="581a7-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="581a7-171">Poczekaj, aż zostanie wyświetlone powiadomienie, że hello dane uzyskane podczas próbkowania.</span><span class="sxs-lookup"><span data-stu-id="581a7-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="581a7-172">Kliknij przycisk **testu** i upewnij się, że otrzymywanie wyników.</span><span class="sxs-lookup"><span data-stu-id="581a7-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="581a7-173">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="581a7-173">Run hello job</span></span>

1. <span data-ttu-id="581a7-174">Upewnij się, że jest uruchomiona, aplikacja TelcoStreaming hello.</span><span class="sxs-lookup"><span data-stu-id="581a7-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="581a7-175">Zamknij hello **zapytania** bloku.</span><span class="sxs-lookup"><span data-stu-id="581a7-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="581a7-176">W bloku zadania powitania kliknij **Start**.</span><span class="sxs-lookup"><span data-stu-id="581a7-176">In hello job blade, click **Start**.</span></span>

    ![Uruchom zadanie usługi Stream Analytics hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="581a7-178">Zadanie analizy przesyłania strumieniowego uruchamia wyszukiwanie fałszywych wywołań hello strumienia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="581a7-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="581a7-179">zadanie Hello również tworzy hello zestawu danych i tabeli w usłudze Power BI i rozpoczyna wysyłanie danych dotyczących hello toothem fałszywych wywołania.</span><span class="sxs-lookup"><span data-stu-id="581a7-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="581a7-180">Utwórz pulpit nawigacyjny hello w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="581a7-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="581a7-181">Przejdź za[witryny Powerbi.com](https://powerbi.com) i zaloguj się przy użyciu konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="581a7-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="581a7-182">Jeśli zapytanie zadania usługi analiza strumienia hello zapisuje wyniki, zobacz zestawu danych jest już utworzony:</span><span class="sxs-lookup"><span data-stu-id="581a7-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Zestawu danych przesyłania strumieniowego w usłudze Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="581a7-184">W obszarze roboczym, kliknij przycisk  **+ &nbsp;Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="581a7-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![przycisk Utwórz Hello w obszarze roboczym usługi Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="581a7-186">Utwórz nowy pulpit nawigacyjny i nadaj mu nazwę `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="581a7-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Utwórz pulpit nawigacyjny i nadaj mu nazwę w obszarze roboczym usługi Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="581a7-188">U góry okna hello hello, kliknij przycisk **kafelka Dodaj**, wybierz pozycję **danych przesyłania STRUMIENIOWEGO NIESTANDARDOWYCH**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="581a7-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Niestandardowe przesyłania strumieniowego zestawu danych](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="581a7-190">W obszarze **YOUR DATSETS**, wybierz zestaw danych, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="581a7-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Zestaw danych przesyłania strumieniowego](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="581a7-192">W obszarze **typ wizualizacji**, wybierz pozycję **karty**, a następnie w hello **pola** listy, wybierz **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="581a7-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Wizualizacja szczegółów dotyczących nowego kafelka](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="581a7-194">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="581a7-194">Click **Next**.</span></span>

8. <span data-ttu-id="581a7-195">Wprowadź szczegóły kafelka, takie jak tytuł i pomocniczą.</span><span class="sxs-lookup"><span data-stu-id="581a7-195">Fill in tile details like a title and subtitle.</span></span>

    ![Tytuł i podtytuł dotyczących nowego kafelka](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="581a7-197">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="581a7-197">Click **Apply**.</span></span>

    <span data-ttu-id="581a7-198">Teraz masz licznika oszustw.</span><span class="sxs-lookup"><span data-stu-id="581a7-198">Now you have a fraud counter!</span></span>

    ![Licznik oszustwa](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="581a7-200">Witaj wykonaj kroki ponownie tooadd kafelka (począwszy od krok 4).</span><span class="sxs-lookup"><span data-stu-id="581a7-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="581a7-201">Tym razem hello następujące:</span><span class="sxs-lookup"><span data-stu-id="581a7-201">This time, do hello following:</span></span>

    * <span data-ttu-id="581a7-202">Gdy pojawi się zbyt**typ wizualizacji**, wybierz pozycję **wykres liniowy**.</span><span class="sxs-lookup"><span data-stu-id="581a7-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="581a7-203">Dodawanie osi i wybierz **windowend**.</span><span class="sxs-lookup"><span data-stu-id="581a7-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="581a7-204">Dodaj wartość i wybrać **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="581a7-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="581a7-205">Aby uzyskać **toodisplay okno czasu**, wybierz pozycję hello ostatnich 10 minut.</span><span class="sxs-lookup"><span data-stu-id="581a7-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Utwórz Kafelek wykres liniowy](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="581a7-207">Kliknij przycisk **dalej**, Dodaj tytuł i podtytuł i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="581a7-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="581a7-208">pulpit nawigacyjny usługi Power BI Hello teraz oferuje dwa widoki danych o wywołaniach fałszywych wykryciu hello strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="581a7-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Zakończono pulpit nawigacyjny usługi Power BI przedstawiający dwa Kafelki dla fałszywych wywołań](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="581a7-210">Dowiedz się więcej o usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="581a7-210">Learn more about Power BI</span></span>

<span data-ttu-id="581a7-211">W tym samouczku przedstawiono sposób toocreate tylko kilka rodzajów wizualizacji dla zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="581a7-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="581a7-212">Usługa Power BI może pomóc tworzyć inne narzędzia analizy biznesowej odbiorcy w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="581a7-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="581a7-213">Aby uzyskać więcej informacji zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="581a7-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="581a7-214">Na przykład innego pulpitu nawigacyjnego usługi Power BI Obejrzyj hello [wprowadzenie do korzystania z usługi Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) wideo.</span><span class="sxs-lookup"><span data-stu-id="581a7-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="581a7-215">Aby uzyskać więcej informacji o konfigurowaniu analizy strumienia zadania tooPower dane wyjściowe BI i przy użyciu usługi Power BI grup, przejrzyj hello [usługi Power BI](stream-analytics-define-outputs.md#power-bi) sekcji hello [analiza strumienia danych wyjściowych](stream-analytics-define-outputs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="581a7-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="581a7-216">Aby dowiedzieć się, jak przy użyciu usługi Power BI, ogólnie rzecz biorąc, zobacz [pulpitów nawigacyjnych w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="581a7-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="581a7-217">Dowiedz się więcej o ograniczeniach oraz najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="581a7-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="581a7-218">Obecnie usługa Power BI można wywołać około raz na sekundę.</span><span class="sxs-lookup"><span data-stu-id="581a7-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="581a7-219">Elementy wizualne przesyłania strumieniowego obsługuje pakietów 15 KB.</span><span class="sxs-lookup"><span data-stu-id="581a7-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="581a7-220">Ponadto niepowodzeniem przesyłania strumieniowego elementy wizualne (ale wypychania nadal toowork).</span><span class="sxs-lookup"><span data-stu-id="581a7-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="581a7-221">Ze względu na ograniczenia te usługi Power BI pozwalają najbardziej naturalnie toocases gdzie Azure Stream Analytics jest zmniejszenie obciążenia dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="581a7-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="581a7-222">Zalecamy używanie okno wirowania lub Hopping okna tooensure czy wypychanie danych jest co najwyżej jeden wypychania na sekundę i czy zapytanie wyładowuje w hello przepływności wymagania.</span><span class="sxs-lookup"><span data-stu-id="581a7-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="581a7-223">Program hello po równości toocompute hello wartość toogive okna w sekundach:</span><span class="sxs-lookup"><span data-stu-id="581a7-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="581a7-225">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="581a7-225">For example:</span></span>

* <span data-ttu-id="581a7-226">Masz 1000 urządzeń wysyłanie danych na sekundę.</span><span class="sxs-lookup"><span data-stu-id="581a7-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="581a7-227">Używasz hello Power BI Pro SKU obsługującego 1 000 000 wierszy na godzinę.</span><span class="sxs-lookup"><span data-stu-id="581a7-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="581a7-228">Ma toopublish hello ilość uśrednianie danych na urządzeniu tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="581a7-229">W związku z tym staje się równania hello:</span><span class="sxs-lookup"><span data-stu-id="581a7-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="581a7-231">W takiej konfiguracji można zmienić hello oryginalnego zapytania toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="581a7-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="581a7-232">Odnów autoryzacji</span><span class="sxs-lookup"><span data-stu-id="581a7-232">Renew authorization</span></span>
<span data-ttu-id="581a7-233">Jeśli hasło hello uległ zmianie od czasu utworzenia lub ostatniej uwierzytelniony zadania, należy tooreauthenticate Twojego konta usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="581a7-234">Jeśli uwierzytelnianie wieloskładnikowe Azure został skonfigurowany w dzierżawie usługi Azure Active Directory (Azure AD), należy również autoryzacji usługi Power BI toorenew co dwa tygodnie.</span><span class="sxs-lookup"><span data-stu-id="581a7-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="581a7-235">Jeśli nie odnowisz, można zauważyć objawy, takich jak brakujące dane wyjściowe zadania lub `Authenticate user error` w hello dzienników operacji.</span><span class="sxs-lookup"><span data-stu-id="581a7-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="581a7-236">Podobnie jeśli zadanie rozpoczyna się po wygaśnięciu tokenu hello, występuje błąd, a zadanie hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="581a7-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="581a7-237">tooresolve ten problem, Zatrzymaj zadanie hello, którym jest uruchomiony i przejdź tooyour, które dane wyjściowe usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="581a7-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="581a7-238">tooavoid utraty danych, wybierz opcję hello **odnowić autoryzacji** połączyć, a następnie uruchom ponownie zadanie z hello **czas ostatniego zatrzymania**.</span><span class="sxs-lookup"><span data-stu-id="581a7-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="581a7-239">Po odświeżeniu hello autoryzacji przy użyciu usługi Power BI, zielony alertu pojawi się w tooreflect obszar autoryzacji hello hello problem został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="581a7-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="581a7-240">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="581a7-240">Get help</span></span>
<span data-ttu-id="581a7-241">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="581a7-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="581a7-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="581a7-242">Next steps</span></span>
* [<span data-ttu-id="581a7-243">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="581a7-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="581a7-244">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="581a7-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="581a7-245">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="581a7-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="581a7-246">Dokumentacja języka zapytań usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="581a7-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="581a7-247">Odwołania API REST zarządzania usługi analiza strumienia Azure</span><span class="sxs-lookup"><span data-stu-id="581a7-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
