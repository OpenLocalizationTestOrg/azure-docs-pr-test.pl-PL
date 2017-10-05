---
title: "Wyzwalacze aplikacji interfejsu API usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Jak zaimplementować Wyzwalacze w aplikacji interfejsu API w usłudze Azure App Service"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="99bb9-103">Wyzwalacze aplikacji interfejsu API w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="99bb9-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="99bb9-104">Ta wersja artykułu ma zastosowanie do aplikacji interfejsu API w wersji schematu 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="99bb9-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="99bb9-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="99bb9-105">Overview</span></span>
<span data-ttu-id="99bb9-106">W tym artykule wyjaśniono, jak wdrożyć wyzwalacze aplikacji interfejsu API i używanie w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="99bb9-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="99bb9-107">Wszystkie fragmenty kodu, w tym temacie są kopiowane z [przykładowy kod aplikacji interfejsu API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="99bb9-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="99bb9-108">Należy pamiętać, że musisz pobrać kodu w tym artykule, aby skompilować i uruchomić następujący pakiet nuget: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="99bb9-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="99bb9-109">Co to są wyzwalacze aplikacji interfejsu API?</span><span class="sxs-lookup"><span data-stu-id="99bb9-109">What are API app triggers?</span></span>
<span data-ttu-id="99bb9-110">Jest typowym scenariuszem dla aplikacji interfejsu API uruchomienie zdarzenia, dzięki czemu klienci w aplikacji interfejsu API można podjąć odpowiednie działania w odpowiedzi na zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="99bb9-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="99bb9-111">Mechanizm na podstawie interfejsu API REST, który obsługuje ten scenariusz jest nazywany wyzwalaczem aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="99bb9-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="99bb9-112">Na przykład, załóżmy, że kod klienta używa [aplikacji w usłudze Twitter interfejsu API łącznika](../connectors/connectors-create-api-twitter.md) i kodu musi wykonać czynności w oparciu o nowych tweetów, które zawierają słów.</span><span class="sxs-lookup"><span data-stu-id="99bb9-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="99bb9-113">W takim przypadku można skonfigurować wyzwalacz sondowania lub wypychanych ułatwia te wymagania.</span><span class="sxs-lookup"><span data-stu-id="99bb9-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="99bb9-114">Wyzwalacz sondowania i wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="99bb9-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="99bb9-115">Obecnie obsługiwane są dwa typy wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="99bb9-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="99bb9-116">Wyzwalacz sondowania - sondowania klienta aplikacji interfejsu API dla powiadomienie o zdarzeniu o uruchomiona</span><span class="sxs-lookup"><span data-stu-id="99bb9-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="99bb9-117">Gdy generowane zdarzenie wyzwalacz wypychania - klienta jest powiadamiany o przez aplikację interfejsu API</span><span class="sxs-lookup"><span data-stu-id="99bb9-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="99bb9-118">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="99bb9-118">Poll trigger</span></span>
<span data-ttu-id="99bb9-119">Wyzwalacz sondowania jest zaimplementowany jako regularne interfejsu API REST i zamierza sondowanie Aby otrzymywać powiadomienia klientów (na przykład aplikacji logiki).</span><span class="sxs-lookup"><span data-stu-id="99bb9-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="99bb9-120">Klient może zachować stanu, sam wyzwalacz sondowania jest bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="99bb9-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="99bb9-121">Następujące informacje dotyczące żądania i odpowiedzi pakiety zilustrować niektóre kluczowe aspekty kontraktu wyzwalacza sondowania:</span><span class="sxs-lookup"><span data-stu-id="99bb9-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="99bb9-122">Żądanie</span><span class="sxs-lookup"><span data-stu-id="99bb9-122">Request</span></span>
  * <span data-ttu-id="99bb9-123">Metoda HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="99bb9-123">HTTP method: GET</span></span>
  * <span data-ttu-id="99bb9-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="99bb9-124">Parameters</span></span>
    * <span data-ttu-id="99bb9-125">triggerState — ten parametr opcjonalny umożliwia klientom określić ich stan, aby poprawnie zdecydować, czy zwracać powiadomienie, lub nie wyzwalacza sondowania na podstawie określonego stanu.</span><span class="sxs-lookup"><span data-stu-id="99bb9-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="99bb9-126">Parametry specyficzne dla interfejsu API</span><span class="sxs-lookup"><span data-stu-id="99bb9-126">API-specific parameters</span></span>
* <span data-ttu-id="99bb9-127">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="99bb9-127">Response</span></span>
  * <span data-ttu-id="99bb9-128">Kod stanu **200** — żądanie jest prawidłowe, i znajduje się powiadomienie z wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="99bb9-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="99bb9-129">Zawartość powiadomienia będzie treść odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="99bb9-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="99bb9-130">Nagłówek "Spróbuj ponownie po" w odpowiedzi wskazuje, czy dane dodatkowe powiadomień musi być pobrana z wywołaniem kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="99bb9-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="99bb9-131">Kod stanu **202** — żądanie jest prawidłowe, ale nie żadne nowe powiadomienie z wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="99bb9-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="99bb9-132">Kod stanu **4xx** -żądania jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="99bb9-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="99bb9-133">Klient nie powinna ponowić żądanie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="99bb9-134">Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="99bb9-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="99bb9-135">Klient powinna ponowić żądanie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-135">The client should retry the request.</span></span>

<span data-ttu-id="99bb9-136">Poniższy fragment kodu przedstawiono przykładowy sposób implementowania wyzwalacz sondowania.</span><span class="sxs-lookup"><span data-stu-id="99bb9-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="99bb9-137">Aby przetestować tego wyzwalacza sondowania, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="99bb9-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="99bb9-138">Wdrażanie aplikacji interfejsu API z ustawieniem uwierzytelniania **publicznego anonimowe**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="99bb9-139">Wywołanie **touch** operacji dostępu do pliku.</span><span class="sxs-lookup"><span data-stu-id="99bb9-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="99bb9-140">Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="99bb9-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="99bb9-141">![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="99bb9-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="99bb9-142">Wywołaj wyzwalacz sondowania z **triggerState** ustawiona sygnaturę czasową przed krok 2.</span><span class="sxs-lookup"><span data-stu-id="99bb9-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="99bb9-143">Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="99bb9-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="99bb9-144">![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="99bb9-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="99bb9-145">Wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="99bb9-145">Push trigger</span></span>
<span data-ttu-id="99bb9-146">Wyzwalacz wypychania jest implementowany jako regularne interfejsu API REST, który wypycha powiadomienia do klientów, które zostały zarejestrowane, aby otrzymać powiadomienie, gdy określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="99bb9-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="99bb9-147">Następujące informacje dotyczące żądania i odpowiedzi pakiety zilustrować niektóre kluczowe aspekty kontraktu wyzwalacza wypychania.</span><span class="sxs-lookup"><span data-stu-id="99bb9-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="99bb9-148">Żądanie</span><span class="sxs-lookup"><span data-stu-id="99bb9-148">Request</span></span>
  * <span data-ttu-id="99bb9-149">Metoda HTTP: umieszczanie</span><span class="sxs-lookup"><span data-stu-id="99bb9-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="99bb9-150">Parametry</span><span class="sxs-lookup"><span data-stu-id="99bb9-150">Parameters</span></span>
    * <span data-ttu-id="99bb9-151">Identyfikator_wyzwalacza: wymagany - nieprzezroczyste ciąg (na przykład identyfikator GUID), który reprezentuje rejestracji wyzwalacz wypychania.</span><span class="sxs-lookup"><span data-stu-id="99bb9-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="99bb9-152">callbackUrl: wymagana — adres URL wywołania zwrotnego do wywołania, gdy generowane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="99bb9-153">Wywołanie jest proste wywołanie POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="99bb9-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="99bb9-154">Parametry specyficzne dla interfejsu API</span><span class="sxs-lookup"><span data-stu-id="99bb9-154">API-specific parameters</span></span>
* <span data-ttu-id="99bb9-155">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="99bb9-155">Response</span></span>
  * <span data-ttu-id="99bb9-156">Kod stanu **200** -żądania, aby zarejestrować klienta powiodło się.</span><span class="sxs-lookup"><span data-stu-id="99bb9-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="99bb9-157">Kod stanu **4xx** -żądania jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="99bb9-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="99bb9-158">Klient nie powinna ponowić żądanie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="99bb9-159">Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="99bb9-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="99bb9-160">Klient powinna ponowić żądanie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-160">The client should retry the request.</span></span>
* <span data-ttu-id="99bb9-161">Wywołanie zwrotne</span><span class="sxs-lookup"><span data-stu-id="99bb9-161">Callback</span></span>
  * <span data-ttu-id="99bb9-162">Metoda HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="99bb9-162">HTTP method: POST</span></span>
  * <span data-ttu-id="99bb9-163">Treść żądania: zawartości powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="99bb9-163">Request body: Notification content.</span></span>

<span data-ttu-id="99bb9-164">Poniższy fragment kodu przedstawiono przykładowy sposób implementowania wyzwalacz wypychania:</span><span class="sxs-lookup"><span data-stu-id="99bb9-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="99bb9-165">Aby przetestować tego wyzwalacza sondowania, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="99bb9-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="99bb9-166">Wdrażanie aplikacji interfejsu API z ustawieniem uwierzytelniania **publicznego anonimowe**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="99bb9-167">Przejdź do [http://requestb.in/](http://requestb.in/) utworzyć RequestBin, która będzie służyć jako adres URL wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="99bb9-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="99bb9-168">Wywołaj wyzwalacz za pomocą identyfikatora GUID jako **Identyfikator_wyzwalacza** i RequestBin adresu URL jako **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="99bb9-169">![Wywołaj wyzwalacz wypychania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="99bb9-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="99bb9-170">Wywołanie **touch** operacji dostępu do pliku.</span><span class="sxs-lookup"><span data-stu-id="99bb9-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="99bb9-171">Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="99bb9-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="99bb9-172">![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="99bb9-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="99bb9-173">Sprawdź RequestBin, aby upewnić się, że wywołanie zwrotne wyzwalacza wypychania została wywołana z danych wyjściowych właściwości.</span><span class="sxs-lookup"><span data-stu-id="99bb9-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="99bb9-174">![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="99bb9-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="99bb9-175">Opisz Wyzwalacze w definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="99bb9-175">Describe triggers in API definition</span></span>
<span data-ttu-id="99bb9-176">Po implementacja wyzwalacze i wdrażanie aplikacji interfejsu API na platformie Azure, przejdź do **definicji interfejsu API** bloku w portalu Azure w wersji zapoznawczej i zostaną wyświetlone wyzwalacze są rozpoznawane automatycznie w interfejsie użytkownika, które wynikają z definicji interfejsu API programu Swagger 2.0 w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="99bb9-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Blok definicji interfejsu API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="99bb9-178">Jeśli klikniesz przycisk **pobierania programu Swagger** przycisk i Otwórz plik JSON, zobaczysz wyniki podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="99bb9-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="99bb9-179">Właściwość rozszerzenia **x-ms-schedular wyzwalacza** jest sposób wyzwalacze są opisane w definicji interfejsu API i jest automatycznie dodawany przez bramę aplikacji interfejsu API w przypadku żądania definicji interfejsu API za pośrednictwem bramy, jeśli żądanie do jednej z następujących kryteriów.</span><span class="sxs-lookup"><span data-stu-id="99bb9-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="99bb9-180">(Można również dodać tę właściwość ręcznie.)</span><span class="sxs-lookup"><span data-stu-id="99bb9-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="99bb9-181">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="99bb9-181">Poll trigger</span></span>
  * <span data-ttu-id="99bb9-182">Jeśli metoda HTTP jest **UZYSKAĆ**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="99bb9-183">Jeśli **operationId** właściwości zawiera ciąg **wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="99bb9-184">Jeśli **parametry** właściwość zawiera parametru z **nazwa** ustawioną właściwość **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="99bb9-185">Wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="99bb9-185">Push trigger</span></span>
  * <span data-ttu-id="99bb9-186">Jeśli metoda HTTP jest **PUT**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="99bb9-187">Jeśli **operationId** właściwości zawiera ciąg **wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="99bb9-188">Jeśli **parametry** właściwość zawiera parametru z **nazwa** ustawioną właściwość **Identyfikator_wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="99bb9-189">Użyj wyzwalacze aplikacji interfejsu API w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="99bb9-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="99bb9-190">Wyświetlanie i konfigurowanie wyzwalacze aplikacji interfejsu API w Projektancie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="99bb9-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="99bb9-191">Jeśli tworzysz aplikację logiki w tej samej grupie zasobów co w aplikacji interfejsu API, można dodać go do obszaru projektowania przez kliknięcie go.</span><span class="sxs-lookup"><span data-stu-id="99bb9-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="99bb9-192">Poniższych ilustracjach przedstawiono to:</span><span class="sxs-lookup"><span data-stu-id="99bb9-192">The following images illustrate this:</span></span>

![Wyzwalacze w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Skonfiguruj wyzwalacza sondowania w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Skonfigurować wypychaną wyzwalacza w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="99bb9-196">Optymalizacja wyzwalacze aplikacji interfejsu API dla usługi Logic apps</span><span class="sxs-lookup"><span data-stu-id="99bb9-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="99bb9-197">Po dodaniu wyzwalacze aplikacji interfejsu API, istnieje kilka rzeczy, które można wykonać, aby ulepszyć środowisko użytkownika podczas korzystania z aplikacji interfejsu API w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="99bb9-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="99bb9-198">Na przykład **triggerState** parametr wyzwalacze sondowania powinien mieć ustawioną poniższe wyrażenie w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="99bb9-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="99bb9-199">To wyrażenie należy ocenić ostatniego wywołania wyzwalacza z aplikacji logiki i zwraca tę wartość.</span><span class="sxs-lookup"><span data-stu-id="99bb9-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="99bb9-200">Uwaga: Aby uzyskać informacje o funkcji używane w wyrażeniu powyżej, zapoznaj się z dokumentacją na [język definicji przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="99bb9-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="99bb9-201">Użytkownicy aplikacji logiki powinny zawierać wyrażenie powyżej dla **triggerState** parametr przy użyciu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="99bb9-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="99bb9-202">Możliwe wartości ustawienia wstępnego przez projektanta aplikacji logiki za pośrednictwem właściwości rozszerzenia są **x-ms harmonogram zalecenie**.</span><span class="sxs-lookup"><span data-stu-id="99bb9-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="99bb9-203">**X-ms widoczność** rozszerzenie właściwości można ustawić na wartość *wewnętrzny* tak, aby parametr sam nie jest wyświetlony w projektancie.</span><span class="sxs-lookup"><span data-stu-id="99bb9-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="99bb9-204">Poniższy fragment kodu przedstawia który.</span><span class="sxs-lookup"><span data-stu-id="99bb9-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="99bb9-205">Wyzwalacze wypychania **Identyfikator_wyzwalacza** parametru musi jednoznacznie identyfikować aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="99bb9-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="99bb9-206">Zalecanym najlepszym rozwiązaniem jest ustawiona na nazwę przepływu pracy przy użyciu następującego wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="99bb9-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="99bb9-207">Przy użyciu **x-ms harmonogram zalecenie** i **x-ms widoczność** właściwości rozszerzenia w jego definicji interfejsu API, aplikacji interfejsu API można przekazać do projektanta aplikacji logiki, aby automatycznie tego wyrażenia zestawu dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99bb9-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="99bb9-208">Dodaj rozszerzenie właściwości w definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="99bb9-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="99bb9-209">Informacje dodatkowe metadane — takie jak właściwości rozszerzenia **x-ms harmonogram zalecenie** i **x-ms widoczność** — można dodać definicji interfejsu API w jednym z dwóch sposobów: statyczne lub dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="99bb9-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="99bb9-210">Statyczne metadanych można edytować bezpośrednio */metadata/apiDefinition.swagger.json* pliku w projekcie i ręcznie dodać właściwości.</span><span class="sxs-lookup"><span data-stu-id="99bb9-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="99bb9-211">Przy użyciu dynamicznych metadanych aplikacji interfejsu API można edytować plik SwaggerConfig.cs, aby dodać filtr operacji, które można dodać te rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="99bb9-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="99bb9-212">Poniżej przedstawiono przykładowy sposób tej klasy można zastosować do ułatwienia scenariusza dynamicznej metadanych.</span><span class="sxs-lookup"><span data-stu-id="99bb9-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
