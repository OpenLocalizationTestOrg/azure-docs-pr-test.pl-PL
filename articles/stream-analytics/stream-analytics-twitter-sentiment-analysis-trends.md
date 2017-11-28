---
title: "czas aaaReal Twitter wskaźniki nastrojów klientów analizy z usługą Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse analiza strumienia w czasie rzeczywistym analizy wskaźniki nastrojów klientów usługi Twitter. Wskazówki krok po kroku z toodata generowania zdarzeń na pulpicie nawigacyjnym na żywo."
keywords: "Analiza trendu w czasie rzeczywistym usługi twitter, analizy wskaźniki nastrojów klientów, analizy mediów społecznościowych, przykład analizy trendów"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="d56c1-105">W czasie rzeczywistym analizy usługi Azure Stream Analytics wskaźniki nastrojów klientów usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="d56c1-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="d56c1-106">Dowiedz się, jak toobuild wskaźniki nastrojów klientów rozwiązania analizy w celu wykonania analizy mediów społecznościowych przełączając w czasie rzeczywistym w usłudze Twitter zdarzeń w usłudze Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d56c1-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="d56c1-107">Następnie można zapisywać danych hello Azure Stream Analytics query tooanalyze i albo zapisać hello wyniki do późniejszego użycia i przy użyciu pulpitu nawigacyjnego i [usługi Power BI](https://powerbi.com/) tooprovide wgląd w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="d56c1-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="d56c1-108">Narzędzia do analizy mediów społecznościowych pomagające organizacjom Zrozumienie trendów tematów.</span><span class="sxs-lookup"><span data-stu-id="d56c1-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="d56c1-109">Tematy trendów są tematy i stanowisk, w których znajduje się duża liczba wpisów w mediów społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="d56c1-110">Wskaźniki nastrojów klientów analizy, która jest również nazywany *wyszukiwania opinii*, korzysta z mediami społecznościowymi analytics narzędzia toodetermine stanowisk kierunku produktu, pomysł i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d56c1-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="d56c1-111">W czasie rzeczywistym analizy trendów w serwisie Twitter jest doskonałym przykładem narzędzia analizy, ponieważ hello hasztagiem subskrypcji modelu pozwala słowa kluczowe toospecific toolisten (hashtagów) i utworzyć wskaźniki nastrojów klientów analizy hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="d56c1-112">Scenariusz: Mediów społecznościowych wskaźniki nastrojów klientów analizy w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d56c1-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="d56c1-113">Firma, która ma nośnika wiadomości witryny sieci Web jest zainteresowana uzyskanie korzyści wyprzedzenia konkurencji przez zawierających zawartość witryny, która jest natychmiast odpowiednich tooits czytników.</span><span class="sxs-lookup"><span data-stu-id="d56c1-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="d56c1-114">Witaj w firmie analizy mediów społecznościowych dotyczące kwestii, które są odpowiednie tooreaders wykonując wskaźniki nastrojów klientów w czasie rzeczywistym analizy danych Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="d56c1-115">tooidentify tematy trendów w czasie rzeczywistym w serwisie Twitter, hello analiz w czasie rzeczywistym potrzeb firmy dotyczących hello tweet woluminów i wskaźniki nastrojów klientów tematy klucza.</span><span class="sxs-lookup"><span data-stu-id="d56c1-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="d56c1-116">Innymi słowy hello jest aparat analizy analytics wskaźniki nastrojów klientów, oparty na tym nośniku społecznościowych źródła danych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d56c1-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d56c1-117">Prerequisites</span></span>
<span data-ttu-id="d56c1-118">W tym samouczku użyjesz aplikacji klienta, który jest podłączany tooTwitter i wyszukuje tweetów mających niektórych hashtagów (które można ustawić).</span><span class="sxs-lookup"><span data-stu-id="d56c1-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="d56c1-119">W kolejności toorun hello aplikacji i analizować hello tweetów przy użyciu usługi analiza strumienia Azure, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d56c1-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="d56c1-120">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d56c1-120">An Azure subscription</span></span>
* <span data-ttu-id="d56c1-121">Konto w serwisie Twitter</span><span class="sxs-lookup"><span data-stu-id="d56c1-121">A Twitter account</span></span> 
* <span data-ttu-id="d56c1-122">Aplikacja usługi Twitter i hello [token dostępu OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d56c1-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="d56c1-123">Firma Microsoft udostępnia ogólne instrukcje toocreate aplikacji Twitter, który jest później.</span><span class="sxs-lookup"><span data-stu-id="d56c1-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="d56c1-124">Witaj TwitterWPFClient aplikacji, która odczytuje hello Twitter źródła danych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="d56c1-125">tooget tej aplikacji, pobierania hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) plików z witryny GitHub i następnie Rozpakuj pakiet hello do folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d56c1-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="d56c1-126">Jeśli chcesz, aby kod źródłowy hello toosee i uruchomić aplikację hello w debugerze, możesz uzyskać hello kodu źródłowego z [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="d56c1-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="d56c1-127">Tworzenie Centrum zdarzeń dla analizy strumienia danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="d56c1-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="d56c1-128">Hello Przykładowa aplikacja generuje zdarzenia i umieszcza je tooan Centrum zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d56c1-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="d56c1-129">Usługa Azure event hubs są hello preferowana metoda wprowadzanie zdarzeń dla usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d56c1-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="d56c1-130">Aby uzyskać więcej informacji, zobacz hello [dokumentacji usługi Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="d56c1-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="d56c1-131">Tworzenie Centrum zdarzeń w przestrzeni nazw i Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d56c1-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="d56c1-132">W tej procedurze należy najpierw utworzyć przestrzeń nazw Centrum zdarzeń, a następnie dodaj do przestrzeni nazw toothat Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="d56c1-133">Przestrzenie nazw Centrum zdarzeń są używane grupy toologically związane z wystąpień magistrali zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="d56c1-134">Zaloguj się za toohello portalu Azure, a następnie kliknij przycisk **nowy** > **Internetu rzeczy** > **Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="d56c1-135">W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw, takich jak `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="d56c1-136">Można użyć dowolnej nazwy przestrzeni nazw hello, ale hello nazwa musi być prawidłowa dla danego adresu URL i między Azure musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="d56c1-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="d56c1-137">Wybierz subskrypcję i Utwórz lub wybierz grupę zasobów, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Tworzenie przestrzeni nazw Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="d56c1-139">Po zakończeniu przestrzeni nazw hello wdrażania można znaleźć przestrzeni nazw Centrum zdarzeń hello na liście zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d56c1-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="d56c1-140">Kliknij hello nowej przestrzeni nazw, a w bloku przestrzeni nazw powitania kliknij  **+ &nbsp;Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="d56c1-141">przycisk Dodaj Centrum zdarzeń Hello do tworzenia nowego Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d56c1-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="d56c1-142">Nazwa hello nowym Centrum zdarzeń `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="d56c1-143">Można użyć innej nazwy.</span><span class="sxs-lookup"><span data-stu-id="d56c1-143">You can use a different name.</span></span> <span data-ttu-id="d56c1-144">Jeśli to zrobisz, zanotuj, ponieważ potrzebna nazwa hello później.</span><span class="sxs-lookup"><span data-stu-id="d56c1-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="d56c1-145">Nie trzeba tooset inne opcje dla hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Blok do tworzenia nowego Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="d56c1-147">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="d56c1-148">Centrum zdarzeń toohello dostępu GRANT</span><span class="sxs-lookup"><span data-stu-id="d56c1-148">Grant access toohello event hub</span></span>

<span data-ttu-id="d56c1-149">Aby proces może wysłać Centrum zdarzeń tooan danych, Centrum zdarzeń hello musi mieć zasadę, która umożliwia uzyskanie odpowiedniego dostępu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="d56c1-150">zasady dostępu Hello generuje ciąg połączenia, który zawiera informacje o autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="d56c1-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="d56c1-151">W bloku przestrzeni nazw zdarzeń powitania kliknij **usługi Event Hubs** a następnie kliknij nazwę hello nowe Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="d56c1-152">W bloku Centrum zdarzeń hello, kliknij przycisk **zasady dostępu współużytkowanego** , a następnie kliknij przycisk  **+ &nbsp;Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="d56c1-153">Upewnij się, że pracujesz z Centrum zdarzeń hello, nie hello Centrum przestrzeni nazw zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="d56c1-154">Dodaj zasady o nazwie `socialtwitter-access` i **oświadczeń**, wybierz pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Blok do tworzenia nowych zasad dostępu do Centrum zdarzeń](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="d56c1-156">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-156">Click **Create**.</span></span>

5.  <span data-ttu-id="d56c1-157">Po wdrożeniu zasad powitania kliknij go hello liście zasady dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d56c1-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="d56c1-158">Znajdź pole hello **klucz podstawowy ciąg połączenia** i kliknij przycisk hello kopiowania przycisku Dalej toohello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Kopiowanie klucza ciąg połączenia głównej hello hello zasady dostępu](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="d56c1-160">Wklej parametry połączenia hello w edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="d56c1-161">Należy tego ciągu połączenia dla następnej sekcji hello, po wprowadzeniu niektórych tooit małych edycji.</span><span class="sxs-lookup"><span data-stu-id="d56c1-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="d56c1-162">Parametry połączenia Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d56c1-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="d56c1-163">Powiadomienie, że parametry połączenia hello zawiera wiele par klucz wartość, oddzielając je średnikami: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, i `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="d56c1-164">Dla bezpieczeństwa części hello parametry połączenia w przykładzie hello zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="d56c1-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="d56c1-165">W edytorze tekstu hello, Usuń hello `EntityPath` parę z parametrów połączenia hello (nie zapomnij tooremove hello średnika, przechwyceniem).</span><span class="sxs-lookup"><span data-stu-id="d56c1-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="d56c1-166">Gdy wszystko będzie gotowe, ciąg połączenia hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d56c1-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="d56c1-167">Skonfiguruj i uruchom aplikację klienta usługi Twitter hello</span><span class="sxs-lookup"><span data-stu-id="d56c1-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="d56c1-168">Aplikacja kliencka Hello pobiera zdarzenia tweet bezpośrednio z usługą Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="d56c1-169">W celu toodo tak, musi on hello toocall uprawnienia w usłudze Twitter interfejsów API przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="d56c1-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="d56c1-170">tooconfigure, że uprawnienia do tworzenia aplikacji w usłudze Twitter, generowany unikatowy poświadczeń (takich jak token OAuth).</span><span class="sxs-lookup"><span data-stu-id="d56c1-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="d56c1-171">Następnie można skonfigurować powitania klienta aplikacji toouse tych poświadczeń podczas wykonywania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d56c1-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="d56c1-172">Utwórz aplikację usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="d56c1-172">Create a Twitter application</span></span>
<span data-ttu-id="d56c1-173">Jeśli nie masz już aplikację usługi Twitter, która służy do celów tego samouczka, można go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="d56c1-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="d56c1-174">Musi już konta w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="d56c1-175">proces dokładnego Hello w Twitter do tworzenia aplikacji i uzyskiwanie hello kluczy, kluczy tajnych i token mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="d56c1-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="d56c1-176">Jeśli te instrukcje nie są zgodne, można znaleźć w witrynie Twitter hello, zapoznaj się z dokumentacją dewelopera Twitter toohello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="d56c1-177">Przejdź toohello [strony zarządzania aplikacji Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="d56c1-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="d56c1-178">Utwórz nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="d56c1-178">Create a new application.</span></span> 

    * <span data-ttu-id="d56c1-179">Witaj adresu URL witryny sieci Web Określ prawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="d56c1-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="d56c1-180">Toobe nie ma lokacji na żywo.</span><span class="sxs-lookup"><span data-stu-id="d56c1-180">It does not have toobe a live site.</span></span> <span data-ttu-id="d56c1-181">(Nie można określić tylko `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="d56c1-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="d56c1-182">Witaj wywołania zwrotnego pole puste.</span><span class="sxs-lookup"><span data-stu-id="d56c1-182">Leave hello callback field blank.</span></span> <span data-ttu-id="d56c1-183">Aplikacja kliencka Hello używanej w tym samouczku nie wymagają wywołań zwrotnych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Tworzenie aplikacji w usłudze Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="d56c1-185">Opcjonalnie można zmienić uprawnienia aplikacji hello tylko tooread.</span><span class="sxs-lookup"><span data-stu-id="d56c1-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="d56c1-186">Po utworzeniu aplikacji hello Przejdź toohello **kluczy i tokenów dostępu** strony.</span><span class="sxs-lookup"><span data-stu-id="d56c1-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="d56c1-187">Kliknij przycisk toogenerate przycisk hello token dostępu i klucz tajny tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="d56c1-188">Zachowaj te informacje przydatne, ponieważ będzie potrzebny w następnej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="d56c1-189">Hello kluczy i kluczy tajnych dla aplikacji Twitter hello zapewniają dostęp do konta w usłudze Twitter tooyour.</span><span class="sxs-lookup"><span data-stu-id="d56c1-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="d56c1-190">Traktować te informacje jako poufne, hello takie same, jak hasło usługi Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="d56c1-191">Na przykład nie osadzaj te informacje w aplikacji, że podajesz tooothers.</span><span class="sxs-lookup"><span data-stu-id="d56c1-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="d56c1-192">Konfigurowanie aplikacji klienta hello</span><span class="sxs-lookup"><span data-stu-id="d56c1-192">Configure hello client application</span></span>
<span data-ttu-id="d56c1-193">Utworzyliśmy aplikacji klienckiej, która łączy się przy użyciu danych tooTwitter [API przesyłania strumieniowego w serwisie Twitter](https://dev.twitter.com/streaming/overview) toocollect tweet zdarzenia o określony zbiór tematów.</span><span class="sxs-lookup"><span data-stu-id="d56c1-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="d56c1-194">Aplikacja Hello używa hello [Sentiment140](http://help.sentiment140.com/) narzędzie typu open source, który przypisuje powitania po tweet tooeach wartość wskaźniki nastrojów klientów:</span><span class="sxs-lookup"><span data-stu-id="d56c1-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="d56c1-195">0 = ujemna</span><span class="sxs-lookup"><span data-stu-id="d56c1-195">0 = negative</span></span>
* <span data-ttu-id="d56c1-196">2 = neutral</span><span class="sxs-lookup"><span data-stu-id="d56c1-196">2 = neutral</span></span>
* <span data-ttu-id="d56c1-197">4 = dodatnią</span><span class="sxs-lookup"><span data-stu-id="d56c1-197">4 = positive</span></span>

<span data-ttu-id="d56c1-198">Po przypisaniu zdarzenia tweet hello wartość wskaźniki nastrojów klientów, są one wypychana toohello Centrum zdarzeń, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d56c1-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="d56c1-199">Przed uruchomieniem aplikacji hello, wymaga pewne informacje, takie jak klucze Twitter hello i parametry połączenia Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="d56c1-200">Można podać informacje o konfiguracji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d56c1-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="d56c1-201">Uruchamianie aplikacji hello, a następnie użyj aplikacji hello interfejsu użytkownika tooenter hello kluczy, kluczy tajnych i parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="d56c1-202">Jeśli to zrobisz, informacje o konfiguracji hello jest używany dla bieżącej sesji, ale nie jest on zapisany.</span><span class="sxs-lookup"><span data-stu-id="d56c1-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="d56c1-203">Edytowanie pliku config aplikacji hello i wartości hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="d56c1-204">Takie podejście będzie nadal występował, informacje o konfiguracji hello, ale oznacza to również, że te potencjalnie wrażliwe informacje są przechowywane w postaci zwykłego tekstu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d56c1-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="d56c1-205">Witaj poniższej procedury dokumentów obu podejść.</span><span class="sxs-lookup"><span data-stu-id="d56c1-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="d56c1-206">Upewnij się, że zostały pobrane i rozpakowane hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplikacji, wymienione w hello wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="d56c1-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="d56c1-207">tooset hello wartości w czasie wykonywania (i tylko dla bieżącej sesji hello), uruchom hello `TwitterWPFClient.exe` aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d56c1-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="d56c1-208">Gdy aplikacja hello monit, wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="d56c1-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="d56c1-209">Witaj w usłudze Twitter konsumenta (klucz interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="d56c1-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="d56c1-210">Witaj w usłudze Twitter klucz tajny klienta (klucz tajny interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="d56c1-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="d56c1-211">Witaj w usłudze Twitter tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="d56c1-212">Witaj w usłudze Twitter klucz tajny tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="d56c1-213">Hello informacje ciągu połączenia, który został wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="d56c1-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="d56c1-214">Upewnij się, że użyto parametrów połączenia hello usunięcie hello `EntityPath` pary klucz wartość z.</span><span class="sxs-lookup"><span data-stu-id="d56c1-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="d56c1-215">Witaj Twitter słów kluczowych, które mają toodetermine wskaźniki nastrojów klientów dla.</span><span class="sxs-lookup"><span data-stu-id="d56c1-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Aplikacja TwitterWpfClient uruchomiony, pokazujący ustawienia pośrednie](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="d56c1-217">wartości hello tooset trwale, użyj pliku TwitterWpfClient.exe.config hello tooopen edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="d56c1-218">Następnie w hello `<appSettings>` element, w tym:</span><span class="sxs-lookup"><span data-stu-id="d56c1-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="d56c1-219">Ustaw `oauth_consumer_key` toohello klucz klienta usługi Twitter (klucz interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="d56c1-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="d56c1-220">Ustaw `oauth_consumer_secret` toohello Twitter klucz tajny klienta (klucz tajny interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="d56c1-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="d56c1-221">Ustaw `oauth_token` toohello Token dostępu w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="d56c1-222">Ustaw `oauth_token_secret` toohello Twitter klucz tajny tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d56c1-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="d56c1-223">Dalszej części hello `<appSettings>` element, wprowadź następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="d56c1-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="d56c1-224">Ustaw `EventHubName` nazwy Centrum zdarzeń toohello (to znaczy toohello wartość hello jednostki ścieżki).</span><span class="sxs-lookup"><span data-stu-id="d56c1-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="d56c1-225">Ustaw `EventHubNameConnectionString` toohello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="d56c1-226">Upewnij się, że użyto parametrów połączenia hello usunięcie hello `EntityPath` pary klucz wartość z.</span><span class="sxs-lookup"><span data-stu-id="d56c1-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="d56c1-227">Witaj `<appSettings>` sekcji wygląda hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="d56c1-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="d56c1-228">(Dla jasności i zabezpieczeń, możemy opakowana wiersze i usunąć niektóre znaki.)</span><span class="sxs-lookup"><span data-stu-id="d56c1-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![TwitterWpfClient pliku konfiguracji aplikacji w edytorze tekstów, przedstawiający hello Twitter kluczy i kluczy tajnych i informacje o parametrach połączenia Centrum zdarzeń hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="d56c1-230">Jeśli nie został już uruchomiony aplikacji hello, uruchom teraz TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="d56c1-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="d56c1-231">Kliknij przycisk hello start zielony przycisk toocollect społecznościowych wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="d56c1-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="d56c1-232">Zobacz Tweet zdarzeń o hello **CreatedAt**, **tematu**, i **SentimentScore** wartości wysyłane tooyour Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Uruchomiona jest aplikacja TwitterWpfClient, przedstawiający listę tweetów](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="d56c1-234">Jeśli występuje błąd, a strumień tweetów wyświetlane w dolnej części okna hello hello jest niewidoczny, należy dokładnie sprawdzić hello kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="d56c1-235">Sprawdź również parametry połączenia hello (Upewnij się, że nie ma hello `EntityPath` kluczy i wartości.)</span><span class="sxs-lookup"><span data-stu-id="d56c1-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="d56c1-236">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d56c1-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="d56c1-237">Teraz, gdy zdarzenia tweet strumieniowe w czasie rzeczywistym z serwisem Twitter, skonfigurowaniem tooanalyze zadania usługi analiza strumienia tych zdarzeń w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="d56c1-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="d56c1-238">W portalu Azure hello, kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="d56c1-239">Nazwa zadania hello `socialtwitter-sa-job` i określ subskrypcję, lokalizacji i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d56c1-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="d56c1-240">Z dobrze tooplace hello zadania i hello Centrum zdarzeń w hello jest tym samym regionie, aby uzyskać najlepszą wydajność i dlatego nie zwracania tootransfer danych między regionami.</span><span class="sxs-lookup"><span data-stu-id="d56c1-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Tworzenie nowego zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="d56c1-242">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-242">Click **Create**.</span></span>

    <span data-ttu-id="d56c1-243">Utworzono zadanie Hello i hello portal Wyświetla szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="d56c1-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="d56c1-244">Określ dane wejściowe zadania hello</span><span class="sxs-lookup"><span data-stu-id="d56c1-244">Specify hello job input</span></span>

1. <span data-ttu-id="d56c1-245">W przypadku zadania Stream Analytics w obszarze **topologii zadania** w środku hello hello zadania bloku, kliknij przycisk **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="d56c1-246">W hello **dane wejściowe** bloku, kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="d56c1-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="d56c1-247">**Alias wejściowy**: Użyj nazwy hello `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="d56c1-248">Użyj innej nazwy, aby je zapisać, ponieważ będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="d56c1-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="d56c1-249">**Typ źródła**: Wybierz **strumienia danych**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="d56c1-250">**Źródło**: Wybierz **Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="d56c1-251">**Opcji importowania**: Wybierz **Użyj Centrum zdarzeń z bieżącej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="d56c1-252">**Przestrzeń nazw magistrali usług**: Wybierz hello Centrum przestrzeni nazw zdarzenia utworzonego wcześniej (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="d56c1-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="d56c1-253">**Centrum zdarzeń**: Centrum zdarzeń hello wybierz utworzony wcześniej (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="d56c1-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="d56c1-254">**Nazwa zasad Centrum zdarzeń**: Wybierz zasady dostępu hello utworzonego wcześniej (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="d56c1-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Utwórz nowe dane wejściowe zadania przesyłania strumieniowego usługi analiza](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="d56c1-256">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="d56c1-257">Określ zapytanie dotyczące zadań hello</span><span class="sxs-lookup"><span data-stu-id="d56c1-257">Specify hello job query</span></span>

<span data-ttu-id="d56c1-258">Analiza strumienia obsługuje prosty, deklaratywny model zapytań opisujący przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="d56c1-259">toolearn więcej informacji na temat języka hello, zobacz hello [Azure Stream Analytics zapytania Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="d56c1-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="d56c1-260">Ten samouczek ułatwia tworzenie i testowanie kilka zapytań za pośrednictwem danych Twitter.</span><span class="sxs-lookup"><span data-stu-id="d56c1-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="d56c1-261">toocompare hello liczby uwagi między tematami, można użyć [okno wirowania](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello liczba uwagi w temacie co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="d56c1-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="d56c1-262">Zamknij hello **dane wejściowe** bloku, jeśli nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d56c1-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="d56c1-263">W bloku zadania powitania kliknij hello **zapytania** pole.</span><span class="sxs-lookup"><span data-stu-id="d56c1-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="d56c1-264">Azure zawiera dane wejściowe hello i dane wyjściowe, które są skonfigurowane dla zadania hello i pozwala utworzyć kwerendę, która umożliwia przekształcenie strumienia wejściowego hello podczas przesyłania danych wyjściowych toohello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="d56c1-265">Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d56c1-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="d56c1-266">W hello **zapytania** bloku, kliknij przycisk Dalej toohello punktów hello `TwitterStream` danych wejściowych, a następnie wybierz **przykładowe dane z danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Menu Opcje toouse przykładowych danych do hello wpis "Przykładowych danych z danych wejściowych" wybrane zadania przesyłania strumieniowego Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="d56c1-268">Spowoduje to otwarcie bloku, który pozwala określić, ile tooget dane przykładowe, zdefiniowanych pod względem jak długo tooread hello wejściowych strumienia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="d56c1-269">Ustaw **minut** too3, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Próbkowanie hello strumienia wejściowego, z "3 minuty" wybrane opcje.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="d56c1-271">Azure przykłady 3 minut, przez które danych ze strumienia wejściowego hello i powiadamia użytkownika, gdy będzie gotowy hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="d56c1-272">(Trwa to krótki czas).</span><span class="sxs-lookup"><span data-stu-id="d56c1-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="d56c1-273">Hello przykładowe dane są tymczasowo przechowywane i jest dostępny, gdy masz hello okna kwerendy.</span><span class="sxs-lookup"><span data-stu-id="d56c1-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="d56c1-274">Jeśli zamkniesz okno kwerendy hello hello przykładowe dane są usuwane, a masz toocreate nowy zestaw przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="d56c1-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="d56c1-275">Zmień zapytanie hello w następujących toohello edytora kodu hello:</span><span class="sxs-lookup"><span data-stu-id="d56c1-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="d56c1-276">Jeśli nie użyto `TwitterStream` jako hello aliasu dla danych wejściowych hello, Zastąp aliasu dla `TwitterStream` w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="d56c1-277">To zapytanie używa hello **TIMESTAMP BY** toospecify — słowo kluczowe w toobe ładunku hello używany w obliczeniach danych czasowych hello pola sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="d56c1-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="d56c1-278">Jeśli to pole nie zostanie określona, hello okien operacja została wykonana za pomocą czas hello każdego zdarzenia dotarły hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d56c1-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="d56c1-279">Dowiedz się więcej w sekcji hello "Godzina nadejścia vs czas aplikacji" [Stream Analytics kwerendy odwołania](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="d56c1-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="d56c1-280">To zapytanie również uzyskuje dostęp do sygnatury czasowej do hello koniec każdego okna przy użyciu hello **System.Timestamp** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d56c1-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="d56c1-281">Kliknij przycisk **testu**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-281">Click **Test**.</span></span> <span data-ttu-id="d56c1-282">Zapytanie Hello jest uruchamiana dla danych hello pobrano.</span><span class="sxs-lookup"><span data-stu-id="d56c1-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="d56c1-283">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-283">Click **Save**.</span></span> <span data-ttu-id="d56c1-284">Spowoduje to zapisanie hello zapytania jako część zadania przesyłania strumieniowego Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="d56c1-285">(Nie zostanie on zapisany hello przykładowe dane).</span><span class="sxs-lookup"><span data-stu-id="d56c1-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="d56c1-286">Przy użyciu różnych pól ze strumienia hello eksperymentu</span><span class="sxs-lookup"><span data-stu-id="d56c1-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="d56c1-287">Witaj poniższej tabeli wymieniono hello pola, które są częścią hello dane przesyłane strumieniowo JSON.</span><span class="sxs-lookup"><span data-stu-id="d56c1-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="d56c1-288">Możesz wolnego tooexperiment w edytorze zapytań hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="d56c1-289">Właściwość JSON</span><span class="sxs-lookup"><span data-stu-id="d56c1-289">JSON property</span></span> | <span data-ttu-id="d56c1-290">Definicja</span><span class="sxs-lookup"><span data-stu-id="d56c1-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="d56c1-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="d56c1-291">CreatedAt</span></span> | <span data-ttu-id="d56c1-292">czas Hello tego tweet hello został utworzony</span><span class="sxs-lookup"><span data-stu-id="d56c1-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="d56c1-293">Temat</span><span class="sxs-lookup"><span data-stu-id="d56c1-293">Topic</span></span> | <span data-ttu-id="d56c1-294">temat Hello, który odpowiada hello określone słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="d56c1-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="d56c1-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="d56c1-295">SentimentScore</span></span> | <span data-ttu-id="d56c1-296">wskaźniki nastrojów klientów Hello wyniku Sentiment140</span><span class="sxs-lookup"><span data-stu-id="d56c1-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="d56c1-297">Autor</span><span class="sxs-lookup"><span data-stu-id="d56c1-297">Author</span></span> | <span data-ttu-id="d56c1-298">dojście Twitter Hello wysyłane hello tweet</span><span class="sxs-lookup"><span data-stu-id="d56c1-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="d56c1-299">Tekst</span><span class="sxs-lookup"><span data-stu-id="d56c1-299">Text</span></span> | <span data-ttu-id="d56c1-300">Pełna treść Hello hello tweet</span><span class="sxs-lookup"><span data-stu-id="d56c1-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="d56c1-301">Utwórz ujście danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="d56c1-301">Create an output sink</span></span>

<span data-ttu-id="d56c1-302">Teraz zdefiniowano strumienia zdarzeń, zdarzenia wejściowe tooingest Centrum zdarzeń i tooperform zapytania transformację za pośrednictwem hello strumienia.</span><span class="sxs-lookup"><span data-stu-id="d56c1-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="d56c1-303">ostatni krok Hello jest toodefine ujście danych wyjściowych zadania hello.</span><span class="sxs-lookup"><span data-stu-id="d56c1-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="d56c1-304">W tym samouczku pisania hello zagregowane tweet zdarzenia z hello zadania kwerendy tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="d56c1-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="d56c1-305">Możesz również wypchnąć z wyników tooAzure bazy danych SQL, magazynem tabel Azure Event Hubs lub usługa Power BI, w zależności od aplikacji wymaga.</span><span class="sxs-lookup"><span data-stu-id="d56c1-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="d56c1-306">Określ hello dane wyjściowe zadania</span><span class="sxs-lookup"><span data-stu-id="d56c1-306">Specify hello job output</span></span>

1. <span data-ttu-id="d56c1-307">W hello **topologii zadania** kliknij hello **dane wyjściowe** pole.</span><span class="sxs-lookup"><span data-stu-id="d56c1-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="d56c1-308">W hello **dane wyjściowe** bloku, kliknij przycisk  **+ &nbsp;Dodaj** , a następnie wypełnij bloku hello z tymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="d56c1-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="d56c1-309">**Alias wyjściowy**: Użyj nazwy hello `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="d56c1-310">**Obiekt sink**: Wybierz **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="d56c1-311">**Opcje importowania**: Wybierz **Użyj magazynu obiektów blob z bieżącej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="d56c1-312">**Konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-312">**Storage account**.</span></span> <span data-ttu-id="d56c1-313">Wybierz **Utwórz nowe konto magazynu.**</span><span class="sxs-lookup"><span data-stu-id="d56c1-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="d56c1-314">**Konto magazynu** (drugie pole).</span><span class="sxs-lookup"><span data-stu-id="d56c1-314">**Storage account** (second box).</span></span> <span data-ttu-id="d56c1-315">Wprowadź `YOURNAMEsa`, gdzie `YOURNAME` jest nazwa użytkownika lub inny unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="d56c1-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="d56c1-316">Nazwa Hello można użyć tylko małe litery i cyfry, i między Azure musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="d56c1-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="d56c1-317">**Kontener**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-317">**Container**.</span></span> <span data-ttu-id="d56c1-318">Wprowadź `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="d56c1-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="d56c1-319">Nazwa konta magazynu Hello i nazwa kontenera są używane razem tooprovide identyfikator URI dla magazynu obiektów blob hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d56c1-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Blok "Nowe dane wyjściowe" zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="d56c1-321">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-321">Click **Create**.</span></span> 

    <span data-ttu-id="d56c1-322">Azure tworzy konto magazynu hello i automatycznie generuje klucz.</span><span class="sxs-lookup"><span data-stu-id="d56c1-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="d56c1-323">Zamknij hello **dane wyjściowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="d56c1-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="d56c1-324">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="d56c1-324">Start hello job</span></span>

<span data-ttu-id="d56c1-325">Dane wejściowe zadania, zapytań i dane wyjściowe zostały określone.</span><span class="sxs-lookup"><span data-stu-id="d56c1-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="d56c1-326">To zadanie usługi Stream Analytics hello toostart gotowe.</span><span class="sxs-lookup"><span data-stu-id="d56c1-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="d56c1-327">Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d56c1-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="d56c1-328">W bloku zadania powitania kliknij **Start**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-328">In hello job blade, click **Start**.</span></span>

    ![Uruchom zadanie usługi Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="d56c1-330">W hello **rozpoczęcia zadania** bloku dla **dane wyjściowe zadania godzina rozpoczęcia**, wybierz pozycję **teraz** , a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Blok "Uruchomić zadanie" hello zadania usługi analiza strumienia](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="d56c1-332">Azure sygnalizuje hello zadań została uruchomiona, a następnie w bloku zadania hello, zostanie wyświetlony stan hello **systemem**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Uruchomione zadanie](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="d56c1-334">Widok danych wyjściowych analizy wskaźniki nastrojów klientów</span><span class="sxs-lookup"><span data-stu-id="d56c1-334">View output for sentiment analysis</span></span>

<span data-ttu-id="d56c1-335">Po uruchomieniu zadania przetwarza hello strumienia w czasie rzeczywistym w serwisie Twitter, można wyświetlić dane wyjściowe hello analizy wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="d56c1-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="d56c1-336">Można użyć narzędzia, takiego jak [Eksploratora usługi Storage Azure](https://http://storageexplorer.com/) lub [Eksploratora Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview w czasie rzeczywistym danych wyjściowych zadania.</span><span class="sxs-lookup"><span data-stu-id="d56c1-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="d56c1-337">W tym miejscu, można użyć [usługi Power BI](https://powerbi.com/) tooextend Twojego tooinclude aplikacji dostosowany pulpit nawigacyjny, takich jak Witaj, co pokazano na powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="d56c1-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="d56c1-339">Utwórz zapytanie innego tooidentify trendów — tematy</span><span class="sxs-lookup"><span data-stu-id="d56c1-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="d56c1-340">Inne zapytanie, można użyć toounderstand Twitter wskaźniki nastrojów klientów jest oparta na [przedłużanie okna](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="d56c1-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="d56c1-341">Tematy trendów tooidentify, możesz wyszukiwać tematy przekraczających wartość progową uwagi w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="d56c1-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="d56c1-342">Do celów tego samouczka hello możesz sprawdzić tematów, które są wymienione więcej niż 20 razy w hello ostatnich 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="d56c1-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="d56c1-343">W bloku zadania powitania kliknij **zatrzymać** toostop hello zadania.</span><span class="sxs-lookup"><span data-stu-id="d56c1-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="d56c1-344">W hello **topologii zadania** kliknij hello **zapytania** pole.</span><span class="sxs-lookup"><span data-stu-id="d56c1-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="d56c1-345">Zmień hello zapytania toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="d56c1-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="d56c1-346">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d56c1-346">Click **Save**.</span></span>

5. <span data-ttu-id="d56c1-347">Upewnij się, że ten TwitterWpfClient aplikacji hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d56c1-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="d56c1-348">Kliknij przycisk **Start** toorestart hello zadania przy użyciu hello nowe zapytanie.</span><span class="sxs-lookup"><span data-stu-id="d56c1-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="d56c1-349">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d56c1-349">Get support</span></span>
<span data-ttu-id="d56c1-350">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="d56c1-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d56c1-351">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d56c1-351">Next steps</span></span>
* [<span data-ttu-id="d56c1-352">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="d56c1-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d56c1-353">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="d56c1-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d56c1-354">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="d56c1-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d56c1-355">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="d56c1-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d56c1-356">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="d56c1-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
