---
title: aaaUse Azure Stream Analytics Tools for Visual Studio | Dokumentacja firmy Microsoft
description: "Pierwsze kroki samouczka dotyczącego hello Azure Stream Analytics Tools for Visual Studio"
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="272ef-104">Użyj narzędzia Azure Stream Analytics Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="272ef-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="272ef-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="272ef-105">Introduction</span></span>
<span data-ttu-id="272ef-106">Z tego samouczka dowiesz się, jak toouse Azure Stream Analytics Tools for toocreate programu Visual Studio tworzenie, testowanie lokalnie, zarządzanie i debugowania z zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="272ef-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="272ef-107">Po ukończeniu tego samouczka, będą mieć możliwość:</span><span class="sxs-lookup"><span data-stu-id="272ef-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="272ef-108">Zapoznaj się z narzędzia do analizy strumienia dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="272ef-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="272ef-109">Konfigurowanie i wdrażanie zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272ef-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="272ef-110">Przetestuj zadania lokalnie z lokalnym przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="272ef-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="272ef-111">Użycie, monitorowanie tootroubleshoot problemów.</span><span class="sxs-lookup"><span data-stu-id="272ef-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="272ef-112">Wyeksportuj istniejących tooprojects zadania.</span><span class="sxs-lookup"><span data-stu-id="272ef-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="272ef-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="272ef-113">Prerequisites</span></span>
<span data-ttu-id="272ef-114">toocomplete tego samouczka należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="272ef-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="272ef-115">Zakończ hello kroki, które należy poprzedzić "Utwórz zadanie usługi analiza strumienia" w hello [tworzenia rozwiązania IoT przy użyciu usługi Stream Analytics samouczek](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="272ef-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="272ef-116">Użyj programu Visual Studio 2015, Visual Studio 2013 update 4 lub Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="272ef-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="272ef-117">Enterprise (Ultimate/Premium), Professional i społeczności wersje są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="272ef-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="272ef-118">Express edition nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="272ef-118">Express edition is not supported.</span></span> <span data-ttu-id="272ef-119">Visual Studio 2017 nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="272ef-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="272ef-120">Użyj hello zestawu Azure SDK dla platformy .NET w wersji 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="272ef-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="272ef-121">Zainstalować go za pomocą hello [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="272ef-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="272ef-122">Zainstaluj hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="272ef-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="272ef-123">Tworzenie projektu usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="272ef-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="272ef-124">W programie Visual Studio, kliknij przycisk hello **pliku** menu i wybierz **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="272ef-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="272ef-125">Z listy szablonów hello powitania po lewej stronie wybierz **Stream Analytics** , a następnie kliknij przycisk **Azure Stream Analytics aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="272ef-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="272ef-126">Wprowadź projektu hello **nazwa**, **lokalizacji**, i **Nazwa rozwiązania** podobnie jak w przypadku innych projektów.</span><span class="sxs-lookup"><span data-stu-id="272ef-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Nowe okno projektu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="272ef-128">A **przez** projektu jest generowany w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="272ef-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Numer projektu generowane w Eksploratorze rozwiązań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="272ef-130">Wybierz poprawną subskrypcję hello</span><span class="sxs-lookup"><span data-stu-id="272ef-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="272ef-131">W programie Visual Studio, kliknij przycisk hello **widoku** i otwórz menu **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="272ef-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="272ef-132">Zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="272ef-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="272ef-133">Definiowanie źródeł dla wejścia hello</span><span class="sxs-lookup"><span data-stu-id="272ef-133">Define hello input sources</span></span>
1.  <span data-ttu-id="272ef-134">W **Eksploratora rozwiązań**, rozwiń węzeł hello **dane wejściowe** węzła i Zmień nazwę **Input.json** za**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="272ef-135">Kliknij dwukrotnie **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="272ef-136">Witaj **Alias wejściowy** jest teraz **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="272ef-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="272ef-137">alias wejściowy Hello jest używany w skrypcie zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="272ef-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="272ef-138">W **typ źródła**, wybierz pozycję **strumienia danych**.</span><span class="sxs-lookup"><span data-stu-id="272ef-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="272ef-139">W **źródła**, wybierz pozycję **Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="272ef-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="272ef-140">W **Namespace magistrali usługi**, wybierz pozycję hello **TollData** opcji.</span><span class="sxs-lookup"><span data-stu-id="272ef-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="272ef-141">W **nazwy Centrum zdarzeń**, wybierz pozycję **wpis**.</span><span class="sxs-lookup"><span data-stu-id="272ef-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="272ef-142">W **nazwy zasad Centrum zdarzeń**, wybierz pozycję **RootManageSharedAccessKey** (hello wartość domyślna).</span><span class="sxs-lookup"><span data-stu-id="272ef-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="272ef-143">W **Format serializacji zdarzeń**, wybierz pozycję **Json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="272ef-144">W **kodowanie**, wybierz pozycję **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="272ef-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="272ef-145">Ustawienia powinna wyglądać powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="272ef-145">Your settings should look like hello following screenshot:</span></span>

    ![Okna wejściowego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="272ef-147">toofinish hello kreatora, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="272ef-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="272ef-148">Teraz można dodać innego źródła danych wejściowych toocreate hello zakończenia strumienia.</span><span class="sxs-lookup"><span data-stu-id="272ef-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="272ef-149">Kliknij prawym przyciskiem myszy hello **dane wejściowe** , a następnie wybierz węzeł **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="272ef-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Nowy element](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="272ef-151">W oknie hello wybierz **Azure Stream Analytics wprowadzania**i zmień hello **nazwa** za**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="272ef-152">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="272ef-152">Click **Add**.</span></span>

    ![Dodaj nowy element okna](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="272ef-154">Kliknij dwukrotnie **ExitStream.json** w projekcie hello i hello wykonaj kroki takie same jak hello wejścia strumienia.</span><span class="sxs-lookup"><span data-stu-id="272ef-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="272ef-155">Należy się tooenter **zakończyć** dla hello **nazwy Centrum zdarzeń** pokazane na powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="272ef-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Okno ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="272ef-157">Teraz zdefiniowane dwóch strumieni wejściowych:</span><span class="sxs-lookup"><span data-stu-id="272ef-157">Now you have defined two input streams:</span></span>

    ![Wejście i wyjście z strumienie wejściowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="272ef-159">Następnie dodaj odwołanie do danych wejściowych hello pliku blob, który zawiera samochodu danych rejestracji.</span><span class="sxs-lookup"><span data-stu-id="272ef-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="272ef-160">Kliknij prawym przyciskiem myszy hello **dane wejściowe** węzła w hello projektu, a następnie hello wykonaj kroki takie same jak dane wejściowe strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="272ef-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="272ef-161">W **Alias wejściowy**, wprowadź **rejestracji**, a następnie w **typ źródła**, wybierz pozycję **danych referencyjnych**.</span><span class="sxs-lookup"><span data-stu-id="272ef-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Okno rejestracji](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="272ef-163">W **konta magazynu**, wybierz pozycję hello **tolldata** opcji.</span><span class="sxs-lookup"><span data-stu-id="272ef-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="272ef-164">W **kontenera**, wybierz pozycję **tolldata**, a następnie w **wzorzec ścieżki**, wprowadź **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="272ef-165">Nazwa pliku jest rozróżniana wielkość liter i powinna być małymi literami.</span><span class="sxs-lookup"><span data-stu-id="272ef-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="272ef-166">toofinish hello kreatora, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="272ef-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="272ef-167">Teraz wszystkie dane wejściowe hello są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="272ef-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="272ef-168">Zdefiniuj hello danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="272ef-168">Define hello output</span></span>
1.  <span data-ttu-id="272ef-169">W **Eksploratora rozwiązań**, rozwiń węzeł hello **dane wejściowe** węzeł i kliknij dwukrotnie **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="272ef-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="272ef-170">W **Alias wyjściowy**, wprowadź **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="272ef-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="272ef-171">W **Sink**, wybierz pozycję **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="272ef-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="272ef-172">W **bazy danych**, wybierz pozycję **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="272ef-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="272ef-173">W **nazwy użytkownika**, wprowadź **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="272ef-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="272ef-174">W **hasło**, wprowadź **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="272ef-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="272ef-175">W **tabeli**, wprowadź **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="272ef-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="272ef-176">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="272ef-176">Click **Save**.</span></span>

    ![Okno danych wyjściowych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="272ef-178">Utwórz kwerendę usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="272ef-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="272ef-179">W tym samouczku prób tooanswer kilka pytania biznesowe, które są powiązane tootoll danych.</span><span class="sxs-lookup"><span data-stu-id="272ef-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="272ef-180">Tworzy zapytań usługi Stream Analytics, które mogą być używane w odpowiedzi odpowiednich tooprovide Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272ef-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="272ef-181">Przed rozpoczęciem pierwszego zadania Stream Analytics, Przyjrzyjmy się prostego scenariusza i hello składnia zapytania.</span><span class="sxs-lookup"><span data-stu-id="272ef-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="272ef-182">Wprowadzenie toohello język zapytań usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272ef-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="272ef-183">Załóżmy, że należy toocount hello liczba pojazdów, które wprowadź stoisku przez.</span><span class="sxs-lookup"><span data-stu-id="272ef-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="272ef-184">Ponieważ w tym przykładzie jest stały strumień zdarzeń, masz toodefine okres czasu.</span><span class="sxs-lookup"><span data-stu-id="272ef-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="272ef-185">Modyfikowanie toobe pytanie hello "ilu pojazdów wprowadź stoisku przez co trzy minuty?"</span><span class="sxs-lookup"><span data-stu-id="272ef-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="272ef-186">Ten sposób toocount, którego dane są często określane tooas hello wirowania liczba.</span><span class="sxs-lookup"><span data-stu-id="272ef-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="272ef-187">Obejrzyj hello Stream Analytics kwerendę, która zawiera odpowiedzi na to pytanie:</span><span class="sxs-lookup"><span data-stu-id="272ef-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="272ef-188">Analiza strumienia używa języka kwerend, takiego jak SQL i dodaje kilka rozszerzeń toospecify związanych z czasem aspektów hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="272ef-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="272ef-189">Aby uzyskać więcej informacji, zobacz [zarządzanie czasem](https://msdn.microsoft.com/library/azure/mt582045.aspx) i [Okienkową](https://msdn.microsoft.com/library/azure/dn835019.aspx) konstrukcji używanych w zapytaniu hello w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="272ef-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="272ef-190">Obecnie napisano pierwszego zapytania Stream Analytics, jest czas tootest go.</span><span class="sxs-lookup"><span data-stu-id="272ef-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="272ef-191">Użyj pliki danych przykładowych hello znajduje się w folderze TollApp w hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="272ef-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="272ef-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="272ef-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="272ef-193">Ten folder zawiera hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="272ef-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="272ef-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="272ef-194">Entry.json</span></span>
*   <span data-ttu-id="272ef-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="272ef-195">Exit.json</span></span>
*   <span data-ttu-id="272ef-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="272ef-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="272ef-197">Liczbę hello pojazdów stoisku przez</span><span class="sxs-lookup"><span data-stu-id="272ef-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="272ef-198">W projekcie powitania kliknij dwukrotnie **Script.asaql** tooopen hello skryptu w hello **edytora zapytań**.</span><span class="sxs-lookup"><span data-stu-id="272ef-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="272ef-199">Skopiuj i Wklej hello skryptu w poprzedniej sekcji hello w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="272ef-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="272ef-200">Witaj edytora zapytań obsługuje IntelliSense, kolorowanie składni i hello błąd znacznika.</span><span class="sxs-lookup"><span data-stu-id="272ef-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Edytor zapytań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="272ef-202">Testowanie zapytań usługi Stream Analytics lokalnie</span><span class="sxs-lookup"><span data-stu-id="272ef-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="272ef-203">toocompile hello zapytania toosee Jeśli występuje błąd składni, kliknij prawym przyciskiem myszy projekt hello i wybierz **kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="272ef-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="272ef-204">toovalidate to zapytanie względem przykładowe dane, można użyć lokalnego przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="272ef-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="272ef-205">Kliknij prawym przyciskiem myszy hello danych wejściowych, a następnie wybierz **dodać lokalne dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="272ef-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Dodaj lokalne dane wejściowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="272ef-207">W oknie podręcznym hello wybierz hello przykładowych danych z ścieżki lokalnej.</span><span class="sxs-lookup"><span data-stu-id="272ef-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="272ef-208">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="272ef-208">Click **Save**.</span></span>

    ![Dodaj lokalne okna wejściowego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="272ef-210">Plik o nazwie **local_EntryStream.json** jest automatycznie dodawany tooyour folderu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="272ef-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Dodano tooinputs folder pliku](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="272ef-212">W hello **edytora zapytań**, kliknij przycisk **uruchom lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="272ef-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="272ef-213">Lub naciśnięcie klawisza F5 hello.</span><span class="sxs-lookup"><span data-stu-id="272ef-213">Or you can press hello F5 key.</span></span>

    ![Uruchom lokalnie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Dane wyjściowe uruchamiania lokalnego](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="272ef-216">Naciśnij klawisz żadnych danych wyjściowych hello tooview klucza w hello **ASA lokalnego uruchamiania wynik** okna w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="272ef-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Okna ASA lokalnego uruchomienia wyniku](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="272ef-218">Kliknij przycisk **Otwórz Folder wyników** pliki wyjściowe hello toocheck, zarówno w formacie CSV i JSON.</span><span class="sxs-lookup"><span data-stu-id="272ef-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Otwórz Folder wyników w danych wyjściowych](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="272ef-220">Przykładowe dane wejściowe hello</span><span class="sxs-lookup"><span data-stu-id="272ef-220">Sample hello input data</span></span>
<span data-ttu-id="272ef-221">Można również przykładowych danych wejściowych z pliku lokalnego tooa źródeł danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="272ef-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="272ef-222">Kliknij prawym przyciskiem myszy plik wejściowy konfiguracji hello, a następnie wybierz **przykładowych danych**.</span><span class="sxs-lookup"><span data-stu-id="272ef-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Dane przykładowe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="272ef-224">Teraz można przykładowe tylko Centrum zdarzeń lub Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="272ef-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="272ef-225">Innych źródeł danych wejściowych nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="272ef-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="272ef-226">W oknie podręcznym hello wprowadź hello ścieżka lokalna używana toosave hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="272ef-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="272ef-227">Kliknij przycisk **próbki**.</span><span class="sxs-lookup"><span data-stu-id="272ef-227">Click **Sample**.</span></span>

    ![Przykładowe okno danych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="272ef-229">Wyświetlany postęp hello w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="272ef-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Okno danych wyjściowych](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="272ef-231">Przedstawia tooAzure zapytań usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272ef-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="272ef-232">W hello **edytora zapytań**, kliknij przycisk **przesłać tooAzure** w Edytorze skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="272ef-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Prześlij tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="272ef-234">Wybierz **utworzyć nowego zadania usługi analiza strumienia Azure**.</span><span class="sxs-lookup"><span data-stu-id="272ef-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="272ef-235">Wprowadź hello **Nazwa zadania**i wybierz hello poprawne **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="272ef-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="272ef-236">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="272ef-236">Click **Submit**.</span></span>

    ![Przedstawia okno zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="272ef-238">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="272ef-238">Start a job</span></span>
<span data-ttu-id="272ef-239">Teraz, kiedy zadanie tworzenia widoku zadania hello automatycznie jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="272ef-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="272ef-240">Witaj toostart zadania, kliknij przycisk hello **zieloną strzałkę** przycisku.</span><span class="sxs-lookup"><span data-stu-id="272ef-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Uruchom zadanie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="272ef-242">Wybierz ustawienie domyślne hello, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="272ef-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Uruchom okno zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="272ef-244">zadania Hello **stan** zmiany zbyt**systemem**, i **zdarzeń wprowadzania** i **zdarzeniach wyjściowych** są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="272ef-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Bieżący stan zadania Podsumowanie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="272ef-246">Sprawdzanie wyników hello w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="272ef-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="272ef-247">W programie Visual Studio Otwórz **Eksploratora serwera** i powitania kliknij prawym przyciskiem myszy **TollDataRefJoin** tabeli.</span><span class="sxs-lookup"><span data-stu-id="272ef-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="272ef-248">Wybierz **Pokaż dane tabeli** toosee hello dane wyjściowe z zadania.</span><span class="sxs-lookup"><span data-stu-id="272ef-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Wybór danych tabeli Pokaż w Eksploratorze serwera](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="272ef-250">Wyświetlaj hello zadania metryki</span><span class="sxs-lookup"><span data-stu-id="272ef-250">View hello job metrics</span></span>
<span data-ttu-id="272ef-251">Niektóre statystyki podstawowe zadania znajdują się w **metryki zadania**.</span><span class="sxs-lookup"><span data-stu-id="272ef-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Okno metryk zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="272ef-253">Lista zadań hello w Eksploratorze serwera</span><span class="sxs-lookup"><span data-stu-id="272ef-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="272ef-254">W **Eksploratora serwera**, kliknij przycisk **zadania usługi analiza strumienia** , a następnie kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="272ef-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="272ef-255">zadanie Hello jest wyświetlany w obszarze **zadania usługi analiza strumienia**.</span><span class="sxs-lookup"><span data-stu-id="272ef-255">hello job appears under **Stream Analytics jobs**.</span></span>

![W Eksploratorze serwera na liście zadania usługi analiza strumienia](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="272ef-257">Otwórz hello widoku zadania</span><span class="sxs-lookup"><span data-stu-id="272ef-257">Open hello job view</span></span>
<span data-ttu-id="272ef-258">tooopen hello widoku zadania, rozwiń węzeł zadanie i kliknij dwukrotnie hello **widoku zadania** węzła.</span><span class="sxs-lookup"><span data-stu-id="272ef-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Węzeł w widoku zadania](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="272ef-260">Eksportuj istniejącego projektu tooa zadania</span><span class="sxs-lookup"><span data-stu-id="272ef-260">Export an existing job tooa project</span></span>
<span data-ttu-id="272ef-261">Istnieją dwa sposoby można wyeksportować istniejący projekt tooa zadania.</span><span class="sxs-lookup"><span data-stu-id="272ef-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="272ef-262">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello zadania węzła w hello **zadania usługi analiza strumienia** a następnie wybierz węzeł **wyeksportować tooNew Stream Analytics projektu**.</span><span class="sxs-lookup"><span data-stu-id="272ef-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Eksportuj tooNew projektu usługi analiza strumienia](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="272ef-264">Projekt Hello jest generowana w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="272ef-264">hello project is generated in **Solution Explorer**.</span></span>

![Projekt generowane w Eksploratorze rozwiązań](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="272ef-266">Możesz również użyć widoku zadania hello i kliknij przycisk **Generowanie projektu**.</span><span class="sxs-lookup"><span data-stu-id="272ef-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Generowanie projektu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="272ef-268">Znane problemy i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="272ef-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="272ef-269">Nie jest obsługiwane dla danych wyjściowych usługi Power BI i wyjścia usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="272ef-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="272ef-270">Brak obsługi edytora w celu dodawania lub zmiana JavaScript funkcje zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="272ef-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="272ef-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="272ef-271">Next steps</span></span>
* [<span data-ttu-id="272ef-272">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="272ef-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="272ef-273">Rozpoczynanie pracy przy użyciu usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272ef-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="272ef-274">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="272ef-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="272ef-275">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="272ef-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="272ef-276">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="272ef-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
