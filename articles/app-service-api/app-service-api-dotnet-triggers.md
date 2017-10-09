---
title: "Wyzwalacze aplikacji interfejsu API usługi aaaApp | Dokumentacja firmy Microsoft"
description: "Jak tooimplement wyzwala w aplikacji interfejsu API w usłudze Azure App Service"
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
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="fd0bf-103">Wyzwalacze aplikacji interfejsu API w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fd0bf-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="fd0bf-104">Ta wersja artykułu hello ma zastosowanie tooAPI aplikacji w wersji schematu 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="fd0bf-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fd0bf-105">Overview</span></span>
<span data-ttu-id="fd0bf-106">W tym artykule opisano sposób aplikacji interfejsu API tooimplement wyzwala i używanie w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="fd0bf-107">Wszystkie hello fragmentów kodu w tym temacie są kopiowane z hello [przykładowy kod aplikacji interfejsu API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="fd0bf-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="fd0bf-108">Uwaga należy hello toodownload następującego pakietu nuget dla kodu hello toobuild ten artykuł, a następnie uruchom: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="fd0bf-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="fd0bf-109">Co to są wyzwalacze aplikacji interfejsu API?</span><span class="sxs-lookup"><span data-stu-id="fd0bf-109">What are API app triggers?</span></span>
<span data-ttu-id="fd0bf-110">Tak, aby klientom Witaj aplikacji interfejsu API można podjąć odpowiednie działania hello w zdarzeniu toohello odpowiedzi jest typowym scenariuszem dla toofire aplikacji interfejsu API zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="fd0bf-111">Hello mechanizm na podstawie interfejsu API REST, który obsługuje ten scenariusz jest nazywany wyzwalaczem aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="fd0bf-112">Na przykład, załóżmy, że kod klienta używa hello [aplikacji w usłudze Twitter interfejsu API łącznika](../connectors/connectors-create-api-twitter.md) i kodu musi tooperform działania oparte na nowych tweetów, które zawierają słów.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="fd0bf-113">W takim przypadku można skonfigurować sondowania lub wypychanej toofacilitate wyzwalacza te wymagania.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="fd0bf-114">Wyzwalacz sondowania i wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="fd0bf-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="fd0bf-115">Obecnie obsługiwane są dwa typy wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="fd0bf-116">Wyzwalacz sondowania - Klient sonduje hello aplikacji interfejsu API dla powiadomienie o zdarzeniu o uruchomiona</span><span class="sxs-lookup"><span data-stu-id="fd0bf-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="fd0bf-117">Wyzwalacz wypychania - klienta jest powiadamiany za pomocą aplikacji hello interfejsu API po zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fd0bf-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="fd0bf-118">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="fd0bf-118">Poll trigger</span></span>
<span data-ttu-id="fd0bf-119">Wyzwalacz sondowania jest zaimplementowany jako regularne interfejsu API REST i oczekuje na jego toopoll klientów (na przykład aplikacji logiki) w kolejności tooget powiadomień.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="fd0bf-120">Podczas powitania klienta mogą zachować stanu, wyzwalacz sondowania hello, sam jest bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="fd0bf-121">następujące informacje dotyczące żądania i odpowiedzi pakietów hello Hello zilustrować niektóre kluczowe aspekty hello sondowania wyzwalacza kontraktu:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="fd0bf-122">Żądanie</span><span class="sxs-lookup"><span data-stu-id="fd0bf-122">Request</span></span>
  * <span data-ttu-id="fd0bf-123">Metoda HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="fd0bf-123">HTTP method: GET</span></span>
  * <span data-ttu-id="fd0bf-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="fd0bf-124">Parameters</span></span>
    * <span data-ttu-id="fd0bf-125">triggerState — ten parametr opcjonalny umożliwia klientom toospecify ich stan, który hello wyzwalacza sondowania mogła poprawnie zdecydować, czy nie na podstawie hello lub powiadamiania tooreturn określony stan.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="fd0bf-126">Parametry specyficzne dla interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fd0bf-126">API-specific parameters</span></span>
* <span data-ttu-id="fd0bf-127">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="fd0bf-127">Response</span></span>
  * <span data-ttu-id="fd0bf-128">Kod stanu **200** — żądanie jest prawidłowe, i znajduje się powiadomienie z hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="fd0bf-129">zawartość Hello hello powiadomienia będzie hello treść odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="fd0bf-130">Nagłówek "Spróbuj ponownie po" w odpowiedzi hello wskazuje, czy dane dodatkowe powiadomień musi być pobrana z wywołaniem kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="fd0bf-131">Kod stanu **202** — żądanie jest prawidłowe, ale nie żadne nowe powiadomienie z hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="fd0bf-132">Kod stanu **4xx** -żądania jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="fd0bf-133">powitania klienta nie powinna ponowić żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="fd0bf-134">Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="fd0bf-135">powitania klienta powinna ponowić żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-135">hello client should retry hello request.</span></span>

<span data-ttu-id="fd0bf-136">Hello następującego fragmentu kodu przedstawiono przykładowy sposób wyzwolenia tooimplement sondowania.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="fd0bf-137">tootest wyzwalać to sondowania, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="fd0bf-138">Wdrażanie hello aplikacji interfejsu API z ustawieniem uwierzytelniania z **publicznego anonimowe**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="fd0bf-139">Wywołaj hello **touch** tootouch operacji pliku.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="fd0bf-140">powitania po obraz zawiera przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="fd0bf-141">![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="fd0bf-142">Wywołaj wyzwalacz sondowania hello z hello **triggerState** ustawiona przed tooStep sygnatury czasu tooa #2.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="fd0bf-143">Witaj poniższy obraz przedstawia hello przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="fd0bf-144">![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="fd0bf-145">Wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="fd0bf-145">Push trigger</span></span>
<span data-ttu-id="fd0bf-146">Wyzwalacz wypychania jest implementowany jako regularne interfejsu API REST, który wypycha tooclients powiadomienia, które zostały zarejestrowane toobe powiadomienie, gdy określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="fd0bf-147">następujące informacje dotyczące żądania i odpowiedzi pakietów hello Hello ilustrują niektóre kluczowe aspekty hello wypychania wyzwalacza kontraktu.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="fd0bf-148">Żądanie</span><span class="sxs-lookup"><span data-stu-id="fd0bf-148">Request</span></span>
  * <span data-ttu-id="fd0bf-149">Metoda HTTP: umieszczanie</span><span class="sxs-lookup"><span data-stu-id="fd0bf-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="fd0bf-150">Parametry</span><span class="sxs-lookup"><span data-stu-id="fd0bf-150">Parameters</span></span>
    * <span data-ttu-id="fd0bf-151">Identyfikator_wyzwalacza: wymagany - nieprzezroczyste ciąg (na przykład identyfikator GUID), czy reprezentuje hello rejestracji wyzwalacz wypychania.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="fd0bf-152">callbackUrl: wymagana — adres URL hello wywołania zwrotnego tooinvoke po hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="fd0bf-153">Wywołanie Hello jest proste wywołanie POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="fd0bf-154">Parametry specyficzne dla interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fd0bf-154">API-specific parameters</span></span>
* <span data-ttu-id="fd0bf-155">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="fd0bf-155">Response</span></span>
  * <span data-ttu-id="fd0bf-156">Kod stanu **200** -żądania tooregister klienta powiodło się.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="fd0bf-157">Kod stanu **4xx** -żądania jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="fd0bf-158">powitania klienta nie powinna ponowić żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="fd0bf-159">Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="fd0bf-160">powitania klienta powinna ponowić żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="fd0bf-161">Wywołanie zwrotne</span><span class="sxs-lookup"><span data-stu-id="fd0bf-161">Callback</span></span>
  * <span data-ttu-id="fd0bf-162">Metoda HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="fd0bf-162">HTTP method: POST</span></span>
  * <span data-ttu-id="fd0bf-163">Treść żądania: zawartości powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-163">Request body: Notification content.</span></span>

<span data-ttu-id="fd0bf-164">Hello następującego fragmentu kodu przedstawiono przykładowy sposób wyzwolenia tooimplement wypychanej:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
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
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="fd0bf-165">tootest wyzwalać to sondowania, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="fd0bf-166">Wdrażanie hello aplikacji interfejsu API z ustawieniem uwierzytelniania z **publicznego anonimowe**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="fd0bf-167">Przeglądaj zbyt[http://requestb.in/](http://requestb.in/) toocreate RequestBin, która będzie służyć jako adres URL wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="fd0bf-168">Wywołaj wyzwalacz wypychania hello za pomocą identyfikatora GUID jako **Identyfikator_wyzwalacza** i hello RequestBin URL jako **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="fd0bf-169">![Wywołaj wyzwalacz wypychania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="fd0bf-170">Wywołaj hello **touch** tootouch operacji pliku.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="fd0bf-171">powitania po obraz zawiera przykładowe żądanie za pośrednictwem Postman.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="fd0bf-172">![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="fd0bf-173">Sprawdź, czy tooconfirm RequestBin hello, który hello wywołania zwrotnego wyzwalacz wypychania jest wywoływana z danych wyjściowych właściwości.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="fd0bf-174">![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="fd0bf-175">Opisz Wyzwalacze w definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fd0bf-175">Describe triggers in API definition</span></span>
<span data-ttu-id="fd0bf-176">Po Implementowanie hello wyzwalaczy i wdrażanie Twojego tooAzure aplikacji interfejsu API, przejdź toohello **definicji interfejsu API** bloku w portalu Azure w wersji zapoznawczej hello i zostaną wyświetlone wyzwalacze są rozpoznawane automatycznie w hello interfejsu użytkownika, który jest wymuszany przez Witaj definicji interfejsu API programu Swagger 2.0 aplikacji hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Blok definicji interfejsu API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="fd0bf-178">Jeśli klikniesz przycisk hello **pobierania programu Swagger** przycisk i otwórz hello pliku JSON, zobaczysz wyniki toohello podobne następujące:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="fd0bf-179">Właściwość rozszerzenia Hello **x-ms-schedular wyzwalacza** jest sposób wyzwalacze są opisane w definicji interfejsu API i jest automatycznie dodawany przez bramę aplikacji hello interfejsu API w przypadku żądania definicji interfejsu API hello za pośrednictwem bramy hello hello żądanie tooone z Witaj, następujące kryteria.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="fd0bf-180">(Można również dodać tę właściwość ręcznie.)</span><span class="sxs-lookup"><span data-stu-id="fd0bf-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="fd0bf-181">Wyzwalacz sondowania</span><span class="sxs-lookup"><span data-stu-id="fd0bf-181">Poll trigger</span></span>
  * <span data-ttu-id="fd0bf-182">Jeśli hello metoda HTTP jest **UZYSKAĆ**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="fd0bf-183">Jeśli hello **operationId** właściwości zawiera ciąg hello **wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="fd0bf-184">Jeśli hello **parametry** właściwość zawiera parametru z **nazwa** właściwość zbyt**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="fd0bf-185">Wyzwalacz wypychania</span><span class="sxs-lookup"><span data-stu-id="fd0bf-185">Push trigger</span></span>
  * <span data-ttu-id="fd0bf-186">Jeśli hello metoda HTTP jest **PUT**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="fd0bf-187">Jeśli hello **operationId** właściwości zawiera ciąg hello **wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="fd0bf-188">Jeśli hello **parametry** właściwość zawiera parametru z **nazwa** właściwość zbyt**Identyfikator_wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="fd0bf-189">Użyj wyzwalacze aplikacji interfejsu API w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="fd0bf-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="fd0bf-190">Wyświetlanie i konfigurowanie wyzwalacze aplikacji interfejsu API w Projektancie aplikacji logiki hello</span><span class="sxs-lookup"><span data-stu-id="fd0bf-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="fd0bf-191">Jeśli tworzysz aplikację logiki w hello tej samej grupie zasobów co hello aplikacji interfejsu API, będziesz w stanie tooadd on toohello kanwy projektanta przez kliknięcie go.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="fd0bf-192">następujące obrazy Hello ilustrację:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-192">hello following images illustrate this:</span></span>

![Wyzwalacze w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Skonfiguruj wyzwalacza sondowania w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Skonfigurować wypychaną wyzwalacza w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="fd0bf-196">Optymalizacja wyzwalacze aplikacji interfejsu API dla usługi Logic apps</span><span class="sxs-lookup"><span data-stu-id="fd0bf-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="fd0bf-197">Po dodaniu aplikacji interfejsu API tooan wyzwalaczy, istnieje kilka sposobów tooimprove hello środowisko podczas korzystania z aplikacji hello interfejsu API w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="fd0bf-198">Na przykład Witaj **triggerState** toohello po wyrażeniu w aplikacji logiki hello powinien być ustawiony parametr wyzwalacze sondowania.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="fd0bf-199">To wyrażenie należy ocenić hello wywołanie ostatniej hello wyzwalacza z aplikacji logiki hello i zwraca tę wartość.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="fd0bf-200">Uwaga: Aby uzyskać informacje o funkcji hello używanych w powyższych wyrażenie hello, znajduje się w dokumentacji toohello w [język definicji przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd0bf-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="fd0bf-201">Użytkownicy aplikacji logiki wymagałoby wyrażenie hello tooprovide powyżej dla hello **triggerState** parametr podczas używania hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="fd0bf-202">Jest możliwe toohave ustawienia tej wartości przez projektanta aplikacji logiki hello za pośrednictwem właściwości rozszerzenia hello **x-ms harmonogram zalecenie**.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="fd0bf-203">Hello **x-ms widoczność** rozszerzenie właściwości można ustawić wartość tooa *wewnętrzny* tak, aby nie ma parametru hello, sama hello projektanta.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="fd0bf-204">powitania po fragment kodu przedstawia który.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="fd0bf-205">Wyzwalacze wypychania hello **Identyfikator_wyzwalacza** parametru musi jednoznacznie identyfikować hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="fd0bf-206">Zalecanym najlepszym rozwiązaniem jest tooset hello ta nazwa toohello właściwości przepływu pracy hello przy użyciu następującego wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="fd0bf-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="fd0bf-207">Przy użyciu hello **x-ms harmonogram zalecenie** i **x-ms widoczność** właściwości rozszerzenia w jego definicji interfejsu API, hello aplikacji interfejsu API można uzyskać, ustaw tę wartość tooautomatically projektanta aplikacji logiki toohello wyrażenie dla hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="fd0bf-208">Dodaj rozszerzenie właściwości w definicji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="fd0bf-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="fd0bf-209">Informacje dodatkowe metadane — takie jak właściwości rozszerzenia hello **x-ms harmonogram zalecenie** i **x-ms widoczność** — można dodać definicji hello interfejsu API w jednym z dwóch sposobów: statyczne lub dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="fd0bf-210">Statyczne metadanych można bezpośrednio edytować hello */metadata/apiDefinition.swagger.json* pliku w projekcie i ręcznie dodać hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="fd0bf-211">Przy użyciu dynamicznych metadanych aplikacji interfejsu API można edytować hello SwaggerConfig.cs pliku tooadd filtr operacji, które można dodać te rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="fd0bf-212">Hello poniżej znajduje się przykład jak ta klasa może być scenariusza dynamicznej metadanych hello toofacilitate zaimplementowany.</span><span class="sxs-lookup"><span data-stu-id="fd0bf-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
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
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
