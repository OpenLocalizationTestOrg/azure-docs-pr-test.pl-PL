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
# <a name="azure-app-service-api-app-triggers"></a>Wyzwalacze aplikacji interfejsu API w usłudze Azure App Service
> [!NOTE]
> Ta wersja artykułu ma zastosowanie do aplikacji interfejsu API w wersji schematu 2014-12-01-preview.
>
>

## <a name="overview"></a>Omówienie
W tym artykule wyjaśniono, jak wdrożyć wyzwalacze aplikacji interfejsu API i używanie w aplikacji logiki.

Wszystkie fragmenty kodu, w tym temacie są kopiowane z [przykładowy kod aplikacji interfejsu API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Należy pamiętać, że musisz pobrać kodu w tym artykule, aby skompilować i uruchomić następujący pakiet nuget: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Co to są wyzwalacze aplikacji interfejsu API?
Jest typowym scenariuszem dla aplikacji interfejsu API uruchomienie zdarzenia, dzięki czemu klienci w aplikacji interfejsu API można podjąć odpowiednie działania w odpowiedzi na zdarzenia. Mechanizm na podstawie interfejsu API REST, który obsługuje ten scenariusz jest nazywany wyzwalaczem aplikacji interfejsu API.

Na przykład, załóżmy, że kod klienta używa [aplikacji w usłudze Twitter interfejsu API łącznika](../connectors/connectors-create-api-twitter.md) i kodu musi wykonać czynności w oparciu o nowych tweetów, które zawierają słów. W takim przypadku można skonfigurować wyzwalacz sondowania lub wypychanych ułatwia te wymagania.

## <a name="poll-trigger-versus-push-trigger"></a>Wyzwalacz sondowania i wyzwalacz wypychania
Obecnie obsługiwane są dwa typy wyzwalaczy:

* Wyzwalacz sondowania - sondowania klienta aplikacji interfejsu API dla powiadomienie o zdarzeniu o uruchomiona
* Gdy generowane zdarzenie wyzwalacz wypychania - klienta jest powiadamiany o przez aplikację interfejsu API

### <a name="poll-trigger"></a>Wyzwalacz sondowania
Wyzwalacz sondowania jest zaimplementowany jako regularne interfejsu API REST i zamierza sondowanie Aby otrzymywać powiadomienia klientów (na przykład aplikacji logiki). Klient może zachować stanu, sam wyzwalacz sondowania jest bezstanowe.

Następujące informacje dotyczące żądania i odpowiedzi pakiety zilustrować niektóre kluczowe aspekty kontraktu wyzwalacza sondowania:

* Żądanie
  * Metoda HTTP: GET
  * Parametry
    * triggerState — ten parametr opcjonalny umożliwia klientom określić ich stan, aby poprawnie zdecydować, czy zwracać powiadomienie, lub nie wyzwalacza sondowania na podstawie określonego stanu.
    * Parametry specyficzne dla interfejsu API
* Odpowiedź
  * Kod stanu **200** — żądanie jest prawidłowe, i znajduje się powiadomienie z wyzwalacza. Zawartość powiadomienia będzie treść odpowiedzi. Nagłówek "Spróbuj ponownie po" w odpowiedzi wskazuje, czy dane dodatkowe powiadomień musi być pobrana z wywołaniem kolejnych żądań.
  * Kod stanu **202** — żądanie jest prawidłowe, ale nie żadne nowe powiadomienie z wyzwalacza.
  * Kod stanu **4xx** -żądania jest nieprawidłowy. Klient nie powinna ponowić żądanie.
  * Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy. Klient powinna ponowić żądanie.

Poniższy fragment kodu przedstawiono przykładowy sposób implementowania wyzwalacz sondowania.

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

Aby przetestować tego wyzwalacza sondowania, wykonaj następujące kroki:

1. Wdrażanie aplikacji interfejsu API z ustawieniem uwierzytelniania **publicznego anonimowe**.
2. Wywołanie **touch** operacji dostępu do pliku. Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.
   ![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Wywołaj wyzwalacz sondowania z **triggerState** ustawiona sygnaturę czasową przed krok 2. Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.
   ![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Wyzwalacz wypychania
Wyzwalacz wypychania jest implementowany jako regularne interfejsu API REST, który wypycha powiadomienia do klientów, które zostały zarejestrowane, aby otrzymać powiadomienie, gdy określone zdarzenia.

Następujące informacje dotyczące żądania i odpowiedzi pakiety zilustrować niektóre kluczowe aspekty kontraktu wyzwalacza wypychania.

* Żądanie
  * Metoda HTTP: umieszczanie
  * Parametry
    * Identyfikator_wyzwalacza: wymagany - nieprzezroczyste ciąg (na przykład identyfikator GUID), który reprezentuje rejestracji wyzwalacz wypychania.
    * callbackUrl: wymagana — adres URL wywołania zwrotnego do wywołania, gdy generowane zdarzenie. Wywołanie jest proste wywołanie POST HTTP.
    * Parametry specyficzne dla interfejsu API
* Odpowiedź
  * Kod stanu **200** -żądania, aby zarejestrować klienta powiodło się.
  * Kod stanu **4xx** -żądania jest nieprawidłowy. Klient nie powinna ponowić żądanie.
  * Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy. Klient powinna ponowić żądanie.
* Wywołanie zwrotne
  * Metoda HTTP: POST
  * Treść żądania: zawartości powiadomienia.

Poniższy fragment kodu przedstawiono przykładowy sposób implementowania wyzwalacz wypychania:

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

Aby przetestować tego wyzwalacza sondowania, wykonaj następujące kroki:

1. Wdrażanie aplikacji interfejsu API z ustawieniem uwierzytelniania **publicznego anonimowe**.
2. Przejdź do [http://requestb.in/](http://requestb.in/) utworzyć RequestBin, która będzie służyć jako adres URL wywołania zwrotnego.
3. Wywołaj wyzwalacz za pomocą identyfikatora GUID jako **Identyfikator_wyzwalacza** i RequestBin adresu URL jako **callbackUrl**.
   ![Wywołaj wyzwalacz wypychania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Wywołanie **touch** operacji dostępu do pliku. Na poniższej ilustracji przedstawiono przykładowe żądanie za pośrednictwem Postman.
   ![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Sprawdź RequestBin, aby upewnić się, że wywołanie zwrotne wyzwalacza wypychania została wywołana z danych wyjściowych właściwości.
   ![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Opisz Wyzwalacze w definicji interfejsu API
Po implementacja wyzwalacze i wdrażanie aplikacji interfejsu API na platformie Azure, przejdź do **definicji interfejsu API** bloku w portalu Azure w wersji zapoznawczej i zostaną wyświetlone wyzwalacze są rozpoznawane automatycznie w interfejsie użytkownika, które wynikają z definicji interfejsu API programu Swagger 2.0 w aplikacji interfejsu API.

![Blok definicji interfejsu API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Jeśli klikniesz przycisk **pobierania programu Swagger** przycisk i Otwórz plik JSON, zobaczysz wyniki podobne do następujących:

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

Właściwość rozszerzenia **x-ms-schedular wyzwalacza** jest sposób wyzwalacze są opisane w definicji interfejsu API i jest automatycznie dodawany przez bramę aplikacji interfejsu API w przypadku żądania definicji interfejsu API za pośrednictwem bramy, jeśli żądanie do jednej z następujących kryteriów. (Można również dodać tę właściwość ręcznie.)

* Wyzwalacz sondowania
  * Jeśli metoda HTTP jest **UZYSKAĆ**.
  * Jeśli **operationId** właściwości zawiera ciąg **wyzwalacza**.
  * Jeśli **parametry** właściwość zawiera parametru z **nazwa** ustawioną właściwość **triggerState**.
* Wyzwalacz wypychania
  * Jeśli metoda HTTP jest **PUT**.
  * Jeśli **operationId** właściwości zawiera ciąg **wyzwalacza**.
  * Jeśli **parametry** właściwość zawiera parametru z **nazwa** ustawioną właściwość **Identyfikator_wyzwalacza**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Użyj wyzwalacze aplikacji interfejsu API w aplikacji logiki
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a>Wyświetlanie i konfigurowanie wyzwalacze aplikacji interfejsu API w Projektancie aplikacji logiki
Jeśli tworzysz aplikację logiki w tej samej grupie zasobów co w aplikacji interfejsu API, można dodać go do obszaru projektowania przez kliknięcie go. Poniższych ilustracjach przedstawiono to:

![Wyzwalacze w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Skonfiguruj wyzwalacza sondowania w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Skonfigurować wypychaną wyzwalacza w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Optymalizacja wyzwalacze aplikacji interfejsu API dla usługi Logic apps
Po dodaniu wyzwalacze aplikacji interfejsu API, istnieje kilka rzeczy, które można wykonać, aby ulepszyć środowisko użytkownika podczas korzystania z aplikacji interfejsu API w aplikacji logiki.

Na przykład **triggerState** parametr wyzwalacze sondowania powinien mieć ustawioną poniższe wyrażenie w aplikacji logiki. To wyrażenie należy ocenić ostatniego wywołania wyzwalacza z aplikacji logiki i zwraca tę wartość.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Uwaga: Aby uzyskać informacje o funkcji używane w wyrażeniu powyżej, zapoznaj się z dokumentacją na [język definicji przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Użytkownicy aplikacji logiki powinny zawierać wyrażenie powyżej dla **triggerState** parametr przy użyciu wyzwalacza. Możliwe wartości ustawienia wstępnego przez projektanta aplikacji logiki za pośrednictwem właściwości rozszerzenia są **x-ms harmonogram zalecenie**.  **X-ms widoczność** rozszerzenie właściwości można ustawić na wartość *wewnętrzny* tak, aby parametr sam nie jest wyświetlony w projektancie.  Poniższy fragment kodu przedstawia który.

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

Wyzwalacze wypychania **Identyfikator_wyzwalacza** parametru musi jednoznacznie identyfikować aplikacji logiki. Zalecanym najlepszym rozwiązaniem jest ustawiona na nazwę przepływu pracy przy użyciu następującego wyrażenia:

    @workflow().name

Przy użyciu **x-ms harmonogram zalecenie** i **x-ms widoczność** właściwości rozszerzenia w jego definicji interfejsu API, aplikacji interfejsu API można przekazać do projektanta aplikacji logiki, aby automatycznie tego wyrażenia zestawu dla użytkownika.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Dodaj rozszerzenie właściwości w definicji interfejsu API
Informacje dodatkowe metadane — takie jak właściwości rozszerzenia **x-ms harmonogram zalecenie** i **x-ms widoczność** — można dodać definicji interfejsu API w jednym z dwóch sposobów: statyczne lub dynamiczne.

Statyczne metadanych można edytować bezpośrednio */metadata/apiDefinition.swagger.json* pliku w projekcie i ręcznie dodać właściwości.

Przy użyciu dynamicznych metadanych aplikacji interfejsu API można edytować plik SwaggerConfig.cs, aby dodać filtr operacji, które można dodać te rozszerzenia.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Poniżej przedstawiono przykładowy sposób tej klasy można zastosować do ułatwienia scenariusza dynamicznej metadanych.

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
