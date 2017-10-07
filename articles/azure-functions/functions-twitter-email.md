---
title: "aaaCreate funkcja, która integruje się z usługą Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzy funkcję, która integruje się z usługi Azure Logic Apps i kognitywnych usług Azure toocategorize w tweet wskaźniki nastrojów klientów i wysyłania powiadomień, gdy jest słaba wskaźniki nastrojów klientów."
services: functions, logic-apps, cognitive-services
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="162ec-104">Tworzy funkcję, która integruje się z usługą Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="162ec-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="162ec-105">Azure Functions można integrować z Azure Logic Apps w hello projektanta aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ec-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="162ec-106">Integracja ta umożliwia używanie hello obliczeniowych zasilania funkcji orchestrations z innymi usługami innych firm i Azure.</span><span class="sxs-lookup"><span data-stu-id="162ec-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="162ec-107">W tym samouczku przedstawiono sposób toouse działa z Azure kognitywnych usługi i aplikacje logiki tooanalyze wskaźniki nastrojów klientów z wpisów Twitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="162ec-108">Funkcja HTTP wyzwalane kategoryzuje tweetów jako zielone, żółte lub czerwone oparte na powitania wynik wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="162ec-109">Zostanie wysłana wiadomość e-mail, po wykryciu niską wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-109">An email is sent when poor sentiment is detected.</span></span> 

![pierwsze dwa kroki obrazu aplikacji w Projektancie aplikacji logiki](media/functions-twitter-email/designer1.png)

<span data-ttu-id="162ec-111">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="162ec-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="162ec-112">Utwórz konto usługi kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="162ec-113">Utwórz funkcję, który kategoryzuje tweet wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="162ec-114">Tworzenie aplikacji logiki łączącej tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="162ec-115">Dodaj aplikację logiki toohello wykrywania wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="162ec-116">Połącz hello logiki aplikacji toohello funkcji.</span><span class="sxs-lookup"><span data-stu-id="162ec-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="162ec-117">Wyślij wiadomość e-mail, oparte na powitania odpowiedzi z funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="162ec-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="162ec-118">Prerequisites</span></span>

+ <span data-ttu-id="162ec-119">Aktywny [Twitter](https://twitter.com/) konta.</span><span class="sxs-lookup"><span data-stu-id="162ec-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="162ec-120">[Outlook.com](https://outlook.com/) konta (w przypadku wysyłania powiadomień).</span><span class="sxs-lookup"><span data-stu-id="162ec-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="162ec-121">W tym temacie używa jako początkowy punkt zasobów hello utworzone w [tworzenie pierwszej funkcji z portalu Azure hello](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="162ec-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="162ec-122">Jeśli jeszcze tego nie zrobiono, wykonaj te kroki teraz toocreate aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="162ec-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="162ec-123">Utwórz konto usługi kognitywnych</span><span class="sxs-lookup"><span data-stu-id="162ec-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="162ec-124">Konto usługi kognitywnych jest wymagane toodetect hello wskaźniki nastrojów klientów tweetów monitorowane.</span><span class="sxs-lookup"><span data-stu-id="162ec-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="162ec-125">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="162ec-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="162ec-126">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="162ec-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="162ec-127">Kliknij przycisk **dane i analiza** > **kognitywnych usług**.</span><span class="sxs-lookup"><span data-stu-id="162ec-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="162ec-128">Następnie użyj ustawień hello jako określone w tabeli hello zaakceptować hello i sprawdź **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="162ec-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Tworzenie bloku kognitywnych konta](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="162ec-130">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="162ec-130">Setting</span></span>      |  <span data-ttu-id="162ec-131">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="162ec-131">Suggested value</span></span>   | <span data-ttu-id="162ec-132">Opis</span><span class="sxs-lookup"><span data-stu-id="162ec-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="162ec-133">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="162ec-133">**Name**</span></span> | <span data-ttu-id="162ec-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="162ec-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="162ec-135">Wybierz unikatową nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="162ec-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="162ec-136">**Typ interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="162ec-136">**API type**</span></span> | <span data-ttu-id="162ec-137">Interfejs API analizy tekstu</span><span class="sxs-lookup"><span data-stu-id="162ec-137">Text Analytics API</span></span> | <span data-ttu-id="162ec-138">Interfejs API używany tooanalyze tekstu.</span><span class="sxs-lookup"><span data-stu-id="162ec-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="162ec-139">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="162ec-139">**Location**</span></span> | <span data-ttu-id="162ec-140">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="162ec-140">West US</span></span> | <span data-ttu-id="162ec-141">Obecnie tylko **zachodnie stany USA** jest dostępna dla Analiza tekstu.</span><span class="sxs-lookup"><span data-stu-id="162ec-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="162ec-142">**Warstwa cenowa**</span><span class="sxs-lookup"><span data-stu-id="162ec-142">**Pricing tier**</span></span> | <span data-ttu-id="162ec-143">F0</span><span class="sxs-lookup"><span data-stu-id="162ec-143">F0</span></span> | <span data-ttu-id="162ec-144">Rozpocznij od hello najniższej warstwy.</span><span class="sxs-lookup"><span data-stu-id="162ec-144">Start with hello lowest tier.</span></span> <span data-ttu-id="162ec-145">Po uruchomieniu poza wywołania skalować tooa wyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="162ec-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="162ec-146">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="162ec-146">**Resource group**</span></span> | <span data-ttu-id="162ec-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="162ec-147">myResourceGroup</span></span> | <span data-ttu-id="162ec-148">Użyj hello sama grupa zasobów dla wszystkich usług w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="162ec-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="162ec-149">Kliknij przycisk **Utwórz** toocreate Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="162ec-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="162ec-150">Po utworzeniu konta powitania kliknij pulpitu nawigacyjnego przypiętych toohello nowego konta usługi kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="162ec-151">Hello konta, kliknij przycisk **klucze**, a następnie skopiuj wartość hello **klucz 1** i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="162ec-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="162ec-152">Możesz użyć tego klucza tooconnect hello logiki aplikacji tooyour konta usług kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![Klucze](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="162ec-154">Utwórz hello — funkcja</span><span class="sxs-lookup"><span data-stu-id="162ec-154">Create hello function</span></span>

<span data-ttu-id="162ec-155">Funkcje zawiera toooffload doskonały sposób przetwarzania zadania w przepływie pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ec-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="162ec-156">W tym samouczku używana HTTP wyzwalane funkcja tooprocess tweet wskaźniki nastrojów klientów wyniki z kognitywnych usług i zwrócenie wartości kategorii.</span><span class="sxs-lookup"><span data-stu-id="162ec-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="162ec-157">Rozwiń funkcji aplikacji, kliknij hello  **+**  obok przycisku zbyt**funkcje**, kliknij przycisk hello **HTTPTrigger** szablonu.</span><span class="sxs-lookup"><span data-stu-id="162ec-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="162ec-158">Typ `CategorizeSentiment` dla funkcji hello **nazwa** i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="162ec-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Funkcja blok aplikacje, funkcje +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="162ec-160">Zamień zawartość hello pliku run.csx hello hello następującego kodu, a następnie kliknij przycisk **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="162ec-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="162ec-161">Ten kod funkcja zwraca oparte na wynik wskaźniki nastrojów klientów hello uzyskany w żądaniu hello kategorii koloru.</span><span class="sxs-lookup"><span data-stu-id="162ec-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="162ec-162">Funkcja hello tootest, kliknij przycisk **testu** na powitania prawej tooexpand hello testu kartę. Wpisz wartość `0.2` dla hello **treść żądania**, a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="162ec-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="162ec-163">Wartość **czerwony** jest zwracany w treści hello hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="162ec-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Funkcja hello testu w hello portalu Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="162ec-165">Zostanie zainstalowana funkcja, który kategoryzuje wyniki wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="162ec-166">Następnie należy utworzyć aplikację logiki, która integruje się funkcji z konta usługi kognitywnych i Twitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="162ec-167">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ec-167">Create a logic app</span></span>   

1. <span data-ttu-id="162ec-168">W portalu Azure Witaj, kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="162ec-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="162ec-169">Kliknij przycisk **integracji przedsiębiorstwa** > **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="162ec-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="162ec-170">Następnie sprawdź ustawienia hello używany jako określone w tabeli hello **toodashboard numeru Pin**i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="162ec-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="162ec-171">Następnie wpisz **nazwa** jak `TweetSentiment`, użyj hello ustawień określonych w tabeli hello zaakceptować hello i sprawdź **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="162ec-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Tworzenie aplikacji logiki w hello portalu Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="162ec-173">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="162ec-173">Setting</span></span>      |  <span data-ttu-id="162ec-174">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="162ec-174">Suggested value</span></span>   | <span data-ttu-id="162ec-175">Opis</span><span class="sxs-lookup"><span data-stu-id="162ec-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="162ec-176">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="162ec-176">**Name**</span></span> | <span data-ttu-id="162ec-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="162ec-177">TweetSentiment</span></span> | <span data-ttu-id="162ec-178">Wybierz odpowiednią nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ec-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="162ec-179">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="162ec-179">**Resource group**</span></span> | <span data-ttu-id="162ec-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="162ec-180">myResourceGroup</span></span> | <span data-ttu-id="162ec-181">Interfejs API używany tooanalyze tekstu.</span><span class="sxs-lookup"><span data-stu-id="162ec-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="162ec-182">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="162ec-182">**Location**</span></span> | <span data-ttu-id="162ec-183">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="162ec-183">East US</span></span> | <span data-ttu-id="162ec-184">Wybierz lokalizację tooyou Zamknij.</span><span class="sxs-lookup"><span data-stu-id="162ec-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="162ec-185">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="162ec-185">**Resource group**</span></span> | <span data-ttu-id="162ec-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="162ec-186">myResourceGroup</span></span> | <span data-ttu-id="162ec-187">Wybierz jak poprzednio hello tego samego istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="162ec-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="162ec-188">Kliknij przycisk **Utwórz** toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ec-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="162ec-189">Po utworzeniu aplikacji hello, kliknij pozycję pulpit nawigacyjny przypiętych toohello nowej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ec-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="162ec-190">Następnie w hello projektanta aplikacji logiki, przewiń w dół i kliknij przycisk hello **pustą aplikację logiki** szablonu.</span><span class="sxs-lookup"><span data-stu-id="162ec-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Pusty szablon aplikacji logiki](media/functions-twitter-email/blank.png)

<span data-ttu-id="162ec-192">Możesz teraz użyć hello projektanta aplikacji logiki tooadd usługi i wyzwalacze tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ec-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="162ec-193">Połącz tooTwitter</span><span class="sxs-lookup"><span data-stu-id="162ec-193">Connect tooTwitter</span></span>

<span data-ttu-id="162ec-194">Najpierw utwórz tooyour połączenia konta w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="162ec-195">Aplikacja logiki Hello sonduje wyszukiwane tweety, które wyzwolenia toorun aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="162ec-196">W Projektancie powitania kliknij hello **Twitter** usługi, a następnie kliknij przycisk hello **po jest przesyłana z nowego tweet** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="162ec-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="162ec-197">Zaloguj się tooyour konta w usłudze Twitter i autoryzować Logic Apps toouse Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="162ec-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="162ec-198">Użyj ustawienia wyzwalacza Twitter hello określoną w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Ustawienia łącznika usługi Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="162ec-200">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="162ec-200">Setting</span></span>      |  <span data-ttu-id="162ec-201">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="162ec-201">Suggested value</span></span>   | <span data-ttu-id="162ec-202">Opis</span><span class="sxs-lookup"><span data-stu-id="162ec-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="162ec-203">**Wyszukiwanie tekstu**</span><span class="sxs-lookup"><span data-stu-id="162ec-203">**Search text**</span></span> | <span data-ttu-id="162ec-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="162ec-204">#Azure</span></span> | <span data-ttu-id="162ec-205">Użyj hasztagiem, będącą popularnych dla nowych tweetów toogenerate w polu Interwał powitania wybrany.</span><span class="sxs-lookup"><span data-stu-id="162ec-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="162ec-206">Gdy przy użyciu warstwę bezpłatna hello i z hasztagiem jest zbyt popularne, możesz szybko zużywać hello transakcji na koncie usługi kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="162ec-207">**Częstotliwość**</span><span class="sxs-lookup"><span data-stu-id="162ec-207">**Frequency**</span></span> | <span data-ttu-id="162ec-208">Minuta</span><span class="sxs-lookup"><span data-stu-id="162ec-208">Minute</span></span> | <span data-ttu-id="162ec-209">Jednostka częstotliwość Hello używana do sondowania Twitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="162ec-210">**Interwał**</span><span class="sxs-lookup"><span data-stu-id="162ec-210">**Interval**</span></span> | <span data-ttu-id="162ec-211">15</span><span class="sxs-lookup"><span data-stu-id="162ec-211">15</span></span> | <span data-ttu-id="162ec-212">Witaj czas między żądania usługi Twitter, w jednostkach częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="162ec-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="162ec-213">Kliknij przycisk **zapisać** tooyour tooconnect konta w usłudze Twitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="162ec-214">Aplikacja jest teraz połączony tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="162ec-215">Następnie połączenie tootext analytics toodetect hello wskaźniki nastrojów klientów tweetów zebrane.</span><span class="sxs-lookup"><span data-stu-id="162ec-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="162ec-216">Dodaj wykrywania wskaźniki nastrojów klientów</span><span class="sxs-lookup"><span data-stu-id="162ec-216">Add sentiment detection</span></span>

1. <span data-ttu-id="162ec-217">Kliknij przycisk **nowy krok**, a następnie **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="162ec-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nowy krok, a następnie dodaj akcję](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="162ec-219">W **wybierz akcję**, kliknij przycisk **Analiza tekstu**, a następnie kliknij przycisk hello **wykrywa wskaźniki nastrojów klientów** akcji.</span><span class="sxs-lookup"><span data-stu-id="162ec-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Wykrywa wskaźniki nastrojów klientów](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="162ec-221">Wpisz nazwę połączenia, takich jak `MyCognitiveServicesConnection`, Wklej hello klucza dla usługi kognitywnych konta zapisane i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="162ec-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="162ec-222">Kliknij przycisk **tooanalyze tekst** > **Tweetować tekst**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="162ec-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Wykrywa wskaźniki nastrojów klientów](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="162ec-224">Teraz, gdy skonfigurowano wykrywania wskaźniki nastrojów klientów, można dodać funkcji tooyour połączenia, który wykorzystuje hello wskaźniki nastrojów klientów wynik w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="162ec-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="162ec-225">Połącz funkcja tooyour dane wyjściowe wskaźniki nastrojów klientów</span><span class="sxs-lookup"><span data-stu-id="162ec-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="162ec-226">W hello projektanta aplikacji logiki, kliknij przycisk **nowy krok** > **Dodaj akcję**, a następnie kliknij przycisk **usługi Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="162ec-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="162ec-227">Kliknij przycisk **należy wybrać funkcję Azure**, wybierz pozycję hello **CategorizeSentiment** funkcja utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="162ec-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Azure funkcja okno Wybierz funkcję platformy Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="162ec-229">W **treść żądania**, kliknij przycisk **wynik** , a następnie **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="162ec-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Wynik](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="162ec-231">Teraz funkcja jest wyzwalane, gdy wynik wskaźniki nastrojów klientów są wysyłane z hello logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ec-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="162ec-232">Oznaczone kolorami kategorii jest zwracana aplikacji logiki toohello przez funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="162ec-233">Następnie dodaj powiadomienie e-mail, który jest wysyłany, gdy wartość wskaźniki nastrojów klientów **czerwony** zostanie zwrócona przez funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="162ec-234">Dodawanie powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="162ec-234">Add email notifications</span></span>

<span data-ttu-id="162ec-235">Ostatnia część przepływu pracy hello Hello jest tootrigger wiadomość e-mail, gdy hello wskaźniki nastrojów klientów są oceniane jako _czerwony_.</span><span class="sxs-lookup"><span data-stu-id="162ec-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="162ec-236">W tym temacie używa łącznika usługi Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="162ec-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="162ec-237">Można wykonać podobne kroki toouse łącznika usługi Gmail lub Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="162ec-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="162ec-238">W hello projektanta aplikacji logiki, kliknij przycisk **nowy krok** > **Dodaj warunek**.</span><span class="sxs-lookup"><span data-stu-id="162ec-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="162ec-239">Kliknij przycisk **wybierz wartość**, następnie kliknij przycisk **treści**.</span><span class="sxs-lookup"><span data-stu-id="162ec-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="162ec-240">Wybierz **jest równa**, kliknij przycisk **wybierz wartość** i typ `RED`i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="162ec-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Dodaj aplikację logiki toohello warunku.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="162ec-242">W **Jeśli tak, nic nie RÓB**, kliknij przycisk **Dodaj akcję**, wyszukaj `outlook.com`, kliknij przycisk **wysłać wiadomość e-mail**i zaloguj się na tooyour konta w usłudze Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="162ec-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Wybierz akcję hello warunku.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="162ec-244">Jeśli nie masz konta usługi Outlook.com, można wybrać innego łącznika, takich jak usługi Gmail lub Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="162ec-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="162ec-245">W hello **wysłać wiadomość e-mail** działania, użyj ustawienia poczty e-mail hello jako określone w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Skonfiguruj hello wiadomości e-mail w przypadku wysyłania hello akcji poczty e-mail.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="162ec-247">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="162ec-247">Setting</span></span>      |  <span data-ttu-id="162ec-248">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="162ec-248">Suggested value</span></span>   | <span data-ttu-id="162ec-249">Opis</span><span class="sxs-lookup"><span data-stu-id="162ec-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="162ec-250">**Aby**</span><span class="sxs-lookup"><span data-stu-id="162ec-250">**To**</span></span> | <span data-ttu-id="162ec-251">Wpisz swój adres e-mail</span><span class="sxs-lookup"><span data-stu-id="162ec-251">Type your email address</span></span> | <span data-ttu-id="162ec-252">adres e-mail Hello, która odbiera powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="162ec-253">**Temat**</span><span class="sxs-lookup"><span data-stu-id="162ec-253">**Subject**</span></span> | <span data-ttu-id="162ec-254">Ujemna tweet wykryto wskaźniki nastrojów klientów</span><span class="sxs-lookup"><span data-stu-id="162ec-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="162ec-255">wiersz tematu Hello hello powiadomienia pocztą e-mail.</span><span class="sxs-lookup"><span data-stu-id="162ec-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="162ec-256">**Treści**</span><span class="sxs-lookup"><span data-stu-id="162ec-256">**Body**</span></span> | <span data-ttu-id="162ec-257">Tekst tweet, lokalizacji</span><span class="sxs-lookup"><span data-stu-id="162ec-257">Tweet text, Location</span></span> | <span data-ttu-id="162ec-258">Kliknij przycisk hello **Tweetować tekst** i **lokalizacji** parametrów.</span><span class="sxs-lookup"><span data-stu-id="162ec-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="162ec-259">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="162ec-259">Click **Save**.</span></span>

<span data-ttu-id="162ec-260">Teraz, hello przepływ pracy zostanie zakończone, można włączyć aplikacji logiki hello i można znaleźć funkcji hello w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="162ec-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="162ec-261">Przepływ testowej pracy w hello</span><span class="sxs-lookup"><span data-stu-id="162ec-261">Test hello workflow</span></span>

1. <span data-ttu-id="162ec-262">W hello projektanta aplikacji logiki, kliknij przycisk **Uruchom** toostart hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ec-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="162ec-263">W kolumnie po lewej stronie powitania kliknij **omówienie** toosee stan hello hello logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="162ec-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Stan wykonania aplikacji logiki](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="162ec-265">(Opcjonalnie) Kliknij jeden z hello działa toosee szczegóły hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="162ec-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="162ec-266">Przejdź tooyour funkcji, sprawdź dzienniki hello i sprawdź, czy wskaźniki nastrojów klientów wartości były odbierane i przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="162ec-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Wyświetl dzienniki — funkcja](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="162ec-268">Po wykryciu potencjalnie ujemna wskaźniki nastrojów klientów, otrzymasz wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="162ec-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="162ec-269">Jeśli nie otrzymasz wiadomość e-mail, można zmienić hello funkcja kodu tooreturn czerwony zawsze:</span><span class="sxs-lookup"><span data-stu-id="162ec-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="162ec-270">Po zweryfikowaniu powiadomienia e-mail, należy zmienić wstecz toohello oryginalny kod:</span><span class="sxs-lookup"><span data-stu-id="162ec-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="162ec-271">Po ukończeniu tego samouczka, należy wyłączyć hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="162ec-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="162ec-272">Wyłączenie aplikacji hello, można uniknąć obciążona do wykonania i wykorzystuje się hello transakcji na koncie usługi kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="162ec-273">Teraz już wspomniano, jak łatwo jest funkcji toointegrate w przepływie pracy Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="162ec-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="162ec-274">Wyłącz hello aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="162ec-274">Disable hello logic app</span></span>

<span data-ttu-id="162ec-275">toodisable hello aplikacji logiki, kliknij przycisk **omówienie** , a następnie kliknij przycisk **wyłączyć** u góry hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="162ec-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="162ec-276">Powoduje to zatrzymanie hello aplikacji logiki z systemem i bez usuwania aplikacji hello są naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="162ec-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Dzienniki funkcji](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="162ec-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="162ec-278">Next steps</span></span>

<span data-ttu-id="162ec-279">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="162ec-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="162ec-280">Utwórz konto usługi kognitywnych.</span><span class="sxs-lookup"><span data-stu-id="162ec-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="162ec-281">Utwórz funkcję, który kategoryzuje tweet wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="162ec-282">Tworzenie aplikacji logiki łączącej tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="162ec-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="162ec-283">Dodaj aplikację logiki toohello wykrywania wskaźniki nastrojów klientów.</span><span class="sxs-lookup"><span data-stu-id="162ec-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="162ec-284">Połącz hello logiki aplikacji toohello funkcji.</span><span class="sxs-lookup"><span data-stu-id="162ec-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="162ec-285">Wyślij wiadomość e-mail, oparte na powitania odpowiedzi z funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="162ec-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="162ec-286">Jak przejść dalej toolearn samouczka toohello toocreate niekorzystającą interfejsu API dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="162ec-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="162ec-287">Tworzenie bezserwerowego interfejsu API za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="162ec-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="162ec-288">toolearn więcej informacji na temat aplikacji logiki, zobacz [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="162ec-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

