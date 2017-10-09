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
# <a name="azure-app-service-api-app-triggers"></a>Wyzwalacze aplikacji interfejsu API w usłudze Azure App Service
> [!NOTE]
> Ta wersja artykułu hello ma zastosowanie tooAPI aplikacji w wersji schematu 2014-12-01-preview.
>
>

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób aplikacji interfejsu API tooimplement wyzwala i używanie w aplikacji logiki.

Wszystkie hello fragmentów kodu w tym temacie są kopiowane z hello [przykładowy kod aplikacji interfejsu API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Uwaga należy hello toodownload następującego pakietu nuget dla kodu hello toobuild ten artykuł, a następnie uruchom: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Co to są wyzwalacze aplikacji interfejsu API?
Tak, aby klientom Witaj aplikacji interfejsu API można podjąć odpowiednie działania hello w zdarzeniu toohello odpowiedzi jest typowym scenariuszem dla toofire aplikacji interfejsu API zdarzenia. Hello mechanizm na podstawie interfejsu API REST, który obsługuje ten scenariusz jest nazywany wyzwalaczem aplikacji interfejsu API.

Na przykład, załóżmy, że kod klienta używa hello [aplikacji w usłudze Twitter interfejsu API łącznika](../connectors/connectors-create-api-twitter.md) i kodu musi tooperform działania oparte na nowych tweetów, które zawierają słów. W takim przypadku można skonfigurować sondowania lub wypychanej toofacilitate wyzwalacza te wymagania.

## <a name="poll-trigger-versus-push-trigger"></a>Wyzwalacz sondowania i wyzwalacz wypychania
Obecnie obsługiwane są dwa typy wyzwalaczy:

* Wyzwalacz sondowania - Klient sonduje hello aplikacji interfejsu API dla powiadomienie o zdarzeniu o uruchomiona
* Wyzwalacz wypychania - klienta jest powiadamiany za pomocą aplikacji hello interfejsu API po zdarzenia

### <a name="poll-trigger"></a>Wyzwalacz sondowania
Wyzwalacz sondowania jest zaimplementowany jako regularne interfejsu API REST i oczekuje na jego toopoll klientów (na przykład aplikacji logiki) w kolejności tooget powiadomień. Podczas powitania klienta mogą zachować stanu, wyzwalacz sondowania hello, sam jest bezstanowe.

następujące informacje dotyczące żądania i odpowiedzi pakietów hello Hello zilustrować niektóre kluczowe aspekty hello sondowania wyzwalacza kontraktu:

* Żądanie
  * Metoda HTTP: GET
  * Parametry
    * triggerState — ten parametr opcjonalny umożliwia klientom toospecify ich stan, który hello wyzwalacza sondowania mogła poprawnie zdecydować, czy nie na podstawie hello lub powiadamiania tooreturn określony stan.
    * Parametry specyficzne dla interfejsu API
* Odpowiedź
  * Kod stanu **200** — żądanie jest prawidłowe, i znajduje się powiadomienie z hello wyzwalacza. zawartość Hello hello powiadomienia będzie hello treść odpowiedzi. Nagłówek "Spróbuj ponownie po" w odpowiedzi hello wskazuje, czy dane dodatkowe powiadomień musi być pobrana z wywołaniem kolejnych żądań.
  * Kod stanu **202** — żądanie jest prawidłowe, ale nie żadne nowe powiadomienie z hello wyzwalacza.
  * Kod stanu **4xx** -żądania jest nieprawidłowy. powitania klienta nie powinna ponowić żądanie hello.
  * Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy. powitania klienta powinna ponowić żądanie hello.

Hello następującego fragmentu kodu przedstawiono przykładowy sposób wyzwolenia tooimplement sondowania.

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

tootest wyzwalać to sondowania, wykonaj następujące kroki:

1. Wdrażanie hello aplikacji interfejsu API z ustawieniem uwierzytelniania z **publicznego anonimowe**.
2. Wywołaj hello **touch** tootouch operacji pliku. powitania po obraz zawiera przykładowe żądanie za pośrednictwem Postman.
   ![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Wywołaj wyzwalacz sondowania hello z hello **triggerState** ustawiona przed tooStep sygnatury czasu tooa #2. Witaj poniższy obraz przedstawia hello przykładowe żądanie za pośrednictwem Postman.
   ![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Wyzwalacz wypychania
Wyzwalacz wypychania jest implementowany jako regularne interfejsu API REST, który wypycha tooclients powiadomienia, które zostały zarejestrowane toobe powiadomienie, gdy określone zdarzenia.

następujące informacje dotyczące żądania i odpowiedzi pakietów hello Hello ilustrują niektóre kluczowe aspekty hello wypychania wyzwalacza kontraktu.

* Żądanie
  * Metoda HTTP: umieszczanie
  * Parametry
    * Identyfikator_wyzwalacza: wymagany - nieprzezroczyste ciąg (na przykład identyfikator GUID), czy reprezentuje hello rejestracji wyzwalacz wypychania.
    * callbackUrl: wymagana — adres URL hello wywołania zwrotnego tooinvoke po hello zdarzeń. Wywołanie Hello jest proste wywołanie POST HTTP.
    * Parametry specyficzne dla interfejsu API
* Odpowiedź
  * Kod stanu **200** -żądania tooregister klienta powiodło się.
  * Kod stanu **4xx** -żądania jest nieprawidłowy. powitania klienta nie powinna ponowić żądanie hello.
  * Kod stanu **5xx** — żądanie spowodowało wewnętrzny błąd serwera i/lub problem tymczasowy. powitania klienta powinna ponowić żądanie hello.
* Wywołanie zwrotne
  * Metoda HTTP: POST
  * Treść żądania: zawartości powiadomienia.

Hello następującego fragmentu kodu przedstawiono przykładowy sposób wyzwolenia tooimplement wypychanej:

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

tootest wyzwalać to sondowania, wykonaj następujące kroki:

1. Wdrażanie hello aplikacji interfejsu API z ustawieniem uwierzytelniania z **publicznego anonimowe**.
2. Przeglądaj zbyt[http://requestb.in/](http://requestb.in/) toocreate RequestBin, która będzie służyć jako adres URL wywołania zwrotnego.
3. Wywołaj wyzwalacz wypychania hello za pomocą identyfikatora GUID jako **Identyfikator_wyzwalacza** i hello RequestBin URL jako **callbackUrl**.
   ![Wywołaj wyzwalacz wypychania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Wywołaj hello **touch** tootouch operacji pliku. powitania po obraz zawiera przykładowe żądanie za pośrednictwem Postman.
   ![Wywołanie operacji Touch za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Sprawdź, czy tooconfirm RequestBin hello, który hello wywołania zwrotnego wyzwalacz wypychania jest wywoływana z danych wyjściowych właściwości.
   ![Wywołaj wyzwalacz sondowania za pośrednictwem Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Opisz Wyzwalacze w definicji interfejsu API
Po Implementowanie hello wyzwalaczy i wdrażanie Twojego tooAzure aplikacji interfejsu API, przejdź toohello **definicji interfejsu API** bloku w portalu Azure w wersji zapoznawczej hello i zostaną wyświetlone wyzwalacze są rozpoznawane automatycznie w hello interfejsu użytkownika, który jest wymuszany przez Witaj definicji interfejsu API programu Swagger 2.0 aplikacji hello interfejsu API.

![Blok definicji interfejsu API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Jeśli klikniesz przycisk hello **pobierania programu Swagger** przycisk i otwórz hello pliku JSON, zobaczysz wyniki toohello podobne następujące:

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

Właściwość rozszerzenia Hello **x-ms-schedular wyzwalacza** jest sposób wyzwalacze są opisane w definicji interfejsu API i jest automatycznie dodawany przez bramę aplikacji hello interfejsu API w przypadku żądania definicji interfejsu API hello za pośrednictwem bramy hello hello żądanie tooone z Witaj, następujące kryteria. (Można również dodać tę właściwość ręcznie.)

* Wyzwalacz sondowania
  * Jeśli hello metoda HTTP jest **UZYSKAĆ**.
  * Jeśli hello **operationId** właściwości zawiera ciąg hello **wyzwalacza**.
  * Jeśli hello **parametry** właściwość zawiera parametru z **nazwa** właściwość zbyt**triggerState**.
* Wyzwalacz wypychania
  * Jeśli hello metoda HTTP jest **PUT**.
  * Jeśli hello **operationId** właściwości zawiera ciąg hello **wyzwalacza**.
  * Jeśli hello **parametry** właściwość zawiera parametru z **nazwa** właściwość zbyt**Identyfikator_wyzwalacza**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Użyj wyzwalacze aplikacji interfejsu API w aplikacji logiki
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Wyświetlanie i konfigurowanie wyzwalacze aplikacji interfejsu API w Projektancie aplikacji logiki hello
Jeśli tworzysz aplikację logiki w hello tej samej grupie zasobów co hello aplikacji interfejsu API, będziesz w stanie tooadd on toohello kanwy projektanta przez kliknięcie go. następujące obrazy Hello ilustrację:

![Wyzwalacze w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Skonfiguruj wyzwalacza sondowania w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Skonfigurować wypychaną wyzwalacza w Projektancie aplikacji logiki](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Optymalizacja wyzwalacze aplikacji interfejsu API dla usługi Logic apps
Po dodaniu aplikacji interfejsu API tooan wyzwalaczy, istnieje kilka sposobów tooimprove hello środowisko podczas korzystania z aplikacji hello interfejsu API w aplikacji logiki.

Na przykład Witaj **triggerState** toohello po wyrażeniu w aplikacji logiki hello powinien być ustawiony parametr wyzwalacze sondowania. To wyrażenie należy ocenić hello wywołanie ostatniej hello wyzwalacza z aplikacji logiki hello i zwraca tę wartość.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Uwaga: Aby uzyskać informacje o funkcji hello używanych w powyższych wyrażenie hello, znajduje się w dokumentacji toohello w [język definicji przepływu pracy aplikacji logiki](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Użytkownicy aplikacji logiki wymagałoby wyrażenie hello tooprovide powyżej dla hello **triggerState** parametr podczas używania hello wyzwalacza. Jest możliwe toohave ustawienia tej wartości przez projektanta aplikacji logiki hello za pośrednictwem właściwości rozszerzenia hello **x-ms harmonogram zalecenie**.  Hello **x-ms widoczność** rozszerzenie właściwości można ustawić wartość tooa *wewnętrzny* tak, aby nie ma parametru hello, sama hello projektanta.  powitania po fragment kodu przedstawia który.

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

Wyzwalacze wypychania hello **Identyfikator_wyzwalacza** parametru musi jednoznacznie identyfikować hello aplikacji logiki. Zalecanym najlepszym rozwiązaniem jest tooset hello ta nazwa toohello właściwości przepływu pracy hello przy użyciu następującego wyrażenia:

    @workflow().name

Przy użyciu hello **x-ms harmonogram zalecenie** i **x-ms widoczność** właściwości rozszerzenia w jego definicji interfejsu API, hello aplikacji interfejsu API można uzyskać, ustaw tę wartość tooautomatically projektanta aplikacji logiki toohello wyrażenie dla hello użytkownika.

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
Informacje dodatkowe metadane — takie jak właściwości rozszerzenia hello **x-ms harmonogram zalecenie** i **x-ms widoczność** — można dodać definicji hello interfejsu API w jednym z dwóch sposobów: statyczne lub dynamiczne.

Statyczne metadanych można bezpośrednio edytować hello */metadata/apiDefinition.swagger.json* pliku w projekcie i ręcznie dodać hello właściwości.

Przy użyciu dynamicznych metadanych aplikacji interfejsu API można edytować hello SwaggerConfig.cs pliku tooadd filtr operacji, które można dodać te rozszerzenia.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hello poniżej znajduje się przykład jak ta klasa może być scenariusza dynamicznej metadanych hello toofacilitate zaimplementowany.

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
