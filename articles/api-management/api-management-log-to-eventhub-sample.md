---
title: "interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope aaaMonitor | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja prezentacja zasad dziennika do Centrum eventhub hello łączącego Azure API Management, Azure Event Hubs i Runscope dla protokołu HTTP, rejestrowania i monitorowania"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Monitoruj swoje interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope
Witaj [usługi Zarządzanie interfejsami API](api-management-key-concepts.md) zawiera wiele możliwości tooenhance hello przetwarzania HTTP tooyour wysłanych żądań interfejsu API protokołu HTTP. Jednak hello istnienie hello żądań i odpowiedzi są przejściowej. Witaj żądań i przelewa się przez interfejs API zaplecza tooyour usługi Zarządzanie interfejsami API hello. Interfejs API przetwarza hello żądania i odpowiedzi przechodzi wstecz przez konsumentów toohello interfejsu API. Hello usługi Zarządzanie interfejsami API utrzymuje niektórych ważnych statystyk dotyczących hello interfejsów API do wyświetlenia hello wydawcy portalu w pulpicie nawigacyjnym, ale poza tym, szczegóły hello znikną.

Za pomocą hello [dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [zasad](api-management-howto-policies.md) w hello usługi Zarządzanie interfejsami API można wysyłać żadnych szczegółów z hello żądań i odpowiedzi tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md). Istnieje wiele powodów może być toogenerate zdarzenia z komunikaty HTTP wysyłane tooyour interfejsów API. Oto kilka przykładów dziennik inspekcji aktualizacji, analizy użycia, alerty wyjątków i 3 integracji strony.   

W tym artykule pokazano, jak toocapture hello całego żądań i odpowiedzi komunikat HTTP, przesyła tooan Centrum zdarzeń i następnie przekazywania tej usługi innej firmy tooa komunikat zawiera HTTP rejestrowania i monitorowania usług.

## <a name="why-send-from-api-management-service"></a>Dlaczego należy wysłać z interfejsu API usługi zarządzania?
Jest możliwe toowrite oprogramowania pośredniczącego protokołu HTTP, który można podłączyć do interfejsu API HTTP struktur toocapture żądań i odpowiedzi HTTP źródła je do rejestrowania i monitorowania systemów. podejście toothis wadą interfejsu Hello jest oprogramowanie pośredniczące HTTP hello musi toobe zintegrowane hello zaplecza interfejsu API i musi odpowiadać hello platforma hello interfejsu API. Jeśli istnieje wiele interfejsów API każdej z nich należy wdrożyć hello oprogramowania pośredniczącego. Często jest przyczyn, dlaczego nie można zaktualizować interfejsów API w wewnętrznej bazie danych.

Przy użyciu toointegrate usługi Azure API Management hello z infrastrukturą rejestrowania zapewnia rozwiązanie scentralizowany i niezależne od platformy. Jest również skalowalne, w części powodu toohello [— replikacja geograficzna](api-management-howto-deploy-multi-region.md) możliwości usługi Azure API Management.

## <a name="why-send-tooan-azure-event-hub"></a>Dlaczego wysłać tooan Centrum zdarzeń Azure?
Dlaczego warto utworzyć zasady, które jest określone tooAzure Event Hubs, jest uzasadnione tooask? Istnieje wiele różnych miejscach, w którym można toolog Moje żądania. Dlaczego nie wystarczy wysłać hello bezpośrednio żądań przeznaczenia toohello?  To opcja. Podczas tworzenia żądania rejestrowania z interfejsu API usługi zarządzania, jest jednak konieczne tooconsider jak rejestrowanie komunikatów będzie miało wpływ wydajność hello hello interfejsu API. Stopniowa wzrost obciążenia są obsługiwane przez odpowiednie zwiększenie dostępnych wystąpień składników systemu, czy dzięki wykorzystaniu — replikacja geograficzna. Krótki największego ruchu może jednak spowodować znacznie opóźnione, jeżeli infrastruktura toologging żądania uruchomienia tooslow pod obciążeniem toobe żądań.

Hello Azure Event Hubs jest zaprojektowana tooingress dużych ilości danych, o pojemności zajmujących się znacznie większej liczby zdarzeń niż liczba hello HTTP żądania większości procesu interfejsów API. Witaj Centrum zdarzeń pełni rolę bufora zaawansowane między interfejsu API usługi i hello infrastruktury zarządzania, który będzie przechowywać i przetwarzać wiadomości powitania. Dzięki temu, że wydajność interfejsu API nie będzie ponieść powodu toohello rejestrowania infrastruktury.  

Po hello danych został przekazany tooan Centrum zdarzeń jest trwały i oczekuje na otrzymanie tooprocess konsumentów Centrum zdarzeń go. Witaj Centrum zdarzeń nie zależy sposób przetwarzania, ją po prostu dba upewnienie się, że wiadomość hello zostanie dostarczona pomyślnie.     

Centra zdarzeń ma grupy konsumentów toomultiple hello możliwości toostream zdarzenia. Dzięki temu toobe zdarzenia przetwarzane przez całkowicie różnych systemów. Dzięki temu, obsługa wielu scenariuszy integracji bez umieszczania Dodawanie opóźnień w hello przetwarzanie żądania interfejsu API hello w ramach usługi Zarządzanie interfejsami API hello potrzeb toobe generowane tylko jedno zdarzenie.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Protokół http i aplikacji komunikatów toosend zasad
Centrum zdarzeń akceptuje dane zdarzeń prosty ciąg znaków. Zawartość tego ciągu Hello są całkowicie włączone tooyou. toobe toopackage stanie up żądania HTTP i wysłać go poza tooEvent koncentratory potrzebujemy ciąg hello tooformat informacje hello żądania lub odpowiedzi. W sytuacjach, takich jak ta Jeśli istniejący format, który można ponownie użyć, następnie może nie być toowrite własnej analizy kodu. Początkowo I uznawane za pomocą hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) do wysyłania żądań i odpowiedzi HTTP. Jednak ten format jest zoptymalizowany do przechowywania w formacie JSON na podstawie sekwencji żądań HTTP. Zawiera liczbę obowiązkowe elementy dodane niepotrzebnych złożoności dla scenariusza hello przekazywania wiadomości powitania HTTP za pośrednictwem przewodowy hello.  

Opcja alternatywna został toouse hello `application/http` typ nośnika zgodnie z opisem w specyfikacji hello HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230). Ten typ nośnika wykorzystuje hello dokładnie takiego samego formatu czyli używane tooactually wysyłać wiadomości HTTP za pośrednictwem przewodowy hello, ale cała wiadomość hello można umieścić w treści hello innego żądania HTTP. W tym przypadku po prostu zamierzamy treści hello toouse jako tooEvent toosend naszych komunikat koncentratorów. Wygodnie jest analizatorem w [klienta Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotek, które mogą przeanalizować tego formatu oraz przekształcać je do natywnego hello `HttpRequestMessage` i `HttpResponseMessage` obiektów.

toocreate stanie toobe tego komunikatu, potrzebujemy tootake korzystać na podstawie języka C# [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx) w usłudze Azure API Management. Oto hello zasada, która wysyła tooAzure komunikat żądania HTTP usługi Event Hubs.

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>Deklaracja zasad
Istnieje kilka rzeczy określonego warto zauważyć o wyrażenie zasad. Zasada dziennika do Centrum eventhub Hello ma atrybut o nazwie rejestratora id, który odwołuje się nazwa toohello rejestratora, który został utworzony w ramach hello usługi Zarządzanie interfejsami API. Witaj szczegóły jak toosetup rejestratora Centrum zdarzeń w usłudze API Management hello można znaleźć w dokumencie hello [jak toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management](api-management-howto-log-event-hubs.md). drugi atrybut Hello jest opcjonalnym parametrem, który powoduje, że usługa Event Hubs które wiadomość hello toostore partycji w. Centra zdarzeń Użyj partycji tooenable scalabilty i wymagają co najmniej dwa. Witaj uporządkowanego dostarczenia komunikatów jest gwarantowaną jedynie w partycji. Jeśli firma Microsoft nie poinstruować Centrum zdarzeń, w których wiadomości powitania tooplace partycji, zostanie użyty algorytm okrężnego toodistribute hello obciążenia. Mogą jednak powodować część naszego toobe komunikaty przetwarzane poza kolejnością.  

### <a name="partitions"></a>Partycje
tooensure nasze komunikaty są dostarczane tooconsumers w odpowiedniej kolejności i skorzystać z zalet możliwości dystrybucji obciążenia hello partycji, wybrano toosend HTTP żądania wiadomości tooone partycji i partycji drugi tooa komunikatów odpowiedzi HTTP. Zapewni to rozkład obciążenia nawet i można gwarantujemy, że wszystkie żądania, które będą używane w kolejności i wszystkie odpowiedzi zostaną użyte w kolejności. Istnieje możliwość toobe odpowiedzi, użyty przed hello odpowiednie żądanie, ale który nie jest problem jak mamy inny mechanizm korelowanie żądań tooresponses i wiemy, że żądania zawsze występować przed odpowiedzi.

### <a name="http-payloads"></a>Ładunki HTTP
Po utworzeniu hello `requestLine` sprawdzamy toosee, jeśli treść żądania hello powinny być obcinana. Treść żądania Hello jest skróconą tooonly 1024. Może zostać zwiększona, jednak poszczególne wiadomości Centrum zdarzeń są too256KB ograniczone, istnieje duże prawdopodobieństwo, że niektóre komunikaty HTTP organów zostanie nie mieści się w pojedynczym komunikacie. Podczas rejestrowania i analiza znaczną ilość informacji mogą pochodzić z właśnie wiersz żądania HTTP hello i nagłówków. Ponadto wiele żądań interfejsu API zwracać tylko małych jednostek tak hello utraty wartość informacji przez Obcinanie dużych jednostek jest dość minimalny zmniejszenia toohello porównania transferu, przetwarzania i przechowywania koszty i tookeep całą zawartość treści. Jednego końcowego Uwaga dotycząca przetwarzanie treści hello jest, że potrzebujemy toopass `true` toohello jako<string>— metoda () ponieważ możemy czytania hello treść, jednak podano również chcesz hello interfejs API zaplecza toobe tooread stanie hello treści. Przez przekazanie toothis wartość true, metoda możemy spowodować toobe treści hello buforowane, dzięki czemu mogą być odczytywane po raz drugi. Jest to ważne toobe uwagę Jeśli interfejs API, który nie przekazywania bardzo dużych plików ani nie używa długiego sondowania. W takich przypadkach byłoby najlepsze tooavoid odczytu treści hello w ogóle.   

### <a name="http-headers"></a>Nagłówki HTTP
Nagłówki HTTP może być po prostu transferowanych za pośrednictwem do formatu wiadomość hello w formacie pary klucz/wartość prostą. Wybraliśmy toostrip limit zabezpieczeń określonych pól, tooavoid niepotrzebnie przeciek informacji o poświadczeniach. Jest mało prawdopodobne, że klucze interfejsu API i inne poświadczenia mają być używane do celów analizy. Jeśli Życzymy analizy toodo na powitania użytkownika i określonego produktu hello używają, firma Microsoft może pobrać który z hello `context` obiektu i Dodaj ten komunikat toohello.     

### <a name="message-metadata"></a>Komunikat metadanych
Podczas tworzenia Centrum zdarzeń toohello toosend całą wiadomość hello, hello pierwszego wiersza nie jest częścią hello `application/http` wiadomości. pierwszy wiersz Hello jest dodatkowe metadane składające się z tego, czy wiadomość hello jest komunikat żądania lub odpowiedzi i identyfikator komunikatu, która jest używana toocorrelate żądań tooresponses. Identyfikator komunikatu Hello jest tworzona przy użyciu innej zasady, która wygląda następująco:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Komunikat żądania hello, przechowywane czy w zmiennej, dopóki hello odpowiedzi został zwrócony i po prostu przesłany hello żądań i odpowiedzi w jednym komunikacie można został utworzony. Jednak wysyłania hello żądań i odpowiedzi niezależnie i używając toocorrelate identyfikator komunikatu Witaj dwie, uzyskujemy nieco większej elastyczności rozmiar wiadomości powitania, hello możliwości tootake korzystać z wielu partycji przy jednoczesnym zachowaniu kolejności wiadomości i hello żądania będą wyświetlane na pulpicie nawigacyjnym naszych rejestrowania wcześniej. Może istnieć niektórych sytuacji, gdy prawidłowej odpowiedzi nigdy nie są wysyłane z Centrum zdarzeń toohello, prawdopodobnie powodu tooa błąd krytyczny żądania usługi Zarządzanie interfejsami API hello, ale wciąż będzie istnieje rekord hello żądania.

wiadomość Hello zasad toosend hello odpowiedzi HTTP wygląda bardzo podobnie żądania toohello i aby umożliwić ukończenie hello konfiguracji zasad wygląda następująco:

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

Witaj `set-variable` zasad tworzy wartość, który jest dostępny dla obu hello `log-to-eventhub` zasad w hello `<inbound>` sekcji i hello `<outbound>` sekcji.  

## <a name="receiving-events-from-event-hubs"></a>Odbieranie zdarzeń z usługi Event Hubs
Zdarzenia z Centrum zdarzeń Azure są odbierane przy użyciu hello [protokołu AMQP](http://www.amqp.org/). Zespół Microsoft Service Bus Hello zostały wprowadzone klienta wykorzystywanie zdarzenia łatwiejsze hello toomake dostępnych bibliotek. Istnieją dwa różne podejścia obsługiwane, co jest *konsumenta bezpośredniego* i hello innych używa hello `EventProcessorHost` klasy. Przykłady te dwie metody znajdują się w hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md). jest Hello krótkiej hello różnice, `Direct Consumer` umożliwia pełną kontrolę i hello `EventProcessorHost` wykonuje część hello żmudne procesy robocze, dla ale powoduje pewne założenia, o jaki będzie przetwarzać tych zdarzeń.  

### <a name="eventprocessorhost"></a>EventProcessorHost
W tym przykładzie używamy hello `EventProcessorHost` dla uproszczenia, jednak ją może nie hello najlepszym rozwiązaniem dla tego scenariusza. `EventProcessorHost`Witaj Praca upewnieniu się, że nie masz tooworry wątki problemów w obrębie klasy procesora określonego zdarzenia — informacje. Jednak w naszym scenariuszu będziemy są po prostu konwertowania formatu tooanother wiadomość hello i przekazanie jej wzdłuż tooanother usługi przy użyciu metody asynchronicznej. Nie istnieje potrzeba aktualizowania stanu udostępnionego i w związku z tym ryzyko problemy wielowątkowości. W przypadku większości scenariuszy `EventProcessorHost` hello najlepszym rozwiązaniem jest prawdopodobnie i na pewno jest łatwiejsze opcja hello.     

### <a name="ieventprocessor"></a>IEventProcessor
pojęcie centralnej Hello przy użyciu `EventProcessorHost` jest toocreate implementacja hello `IEventProcessor` interfejs, który zawiera metodę hello `ProcessEventAsync`. Witaj użycia tej metody jest następujący:

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

Lista obiektów EventData są przekazywane do metody hello i możemy iteracja tej listy. Bajty Hello każdej metody są parsowane do obiektu HttpMessage, a ten obiekt jest przekazywana tooan wystąpienie IHttpMessageProcessor.

### <a name="httpmessage"></a>HttpMessage
Witaj `HttpMessage` wystąpienia zawiera trzy elementy danych:

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

Witaj `HttpMessage` wystąpienie zawiera `MessageId` identyfikuje identyfikator GUID, który pozwala nam żądania hello HTTP tooconnect wartość odpowiadająca mu reakcja HTTP toohello i wartość logiczną, jeśli obiekt hello zawiera wystąpienie HttpRequestMessage i HttpResponseMessage. Za pomocą hello wbudowane klasy HTTP z `System.Net.Http`, została tootake mogli korzystać z hello `application/http` analizy kodu, który znajduje się w `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hello `HttpMessage` wystąpienia jest następnie przekazywany tooimplementation z `IHttpMessageProcessor` czyli interfejs utworzono toodecouple hello odbieranie i interpretacji hello zdarzeń z Centrum zdarzeń platformy Azure i hello rzeczywiste przetwarzania go.

## <a name="forwarding-hello-http-message"></a>Komunikat HTTP hello przekazywania
Dla tego przykładu I uzgodnionych byłoby interesujące hello toopush żądania HTTP przez zbyt[Runscope](http://www.runscope.com). Runscope to usługa w chmurze, która specjalizuje się w protokole HTTP, debugowanie, rejestrowania i monitorowania. Mają one warstwę bezpłatna, dzięki czemu jest łatwe tootry i umożliwia żądań HTTP hello toosee do transmisji w czasie rzeczywistym za pomocą naszej usługi Zarządzanie interfejsami API.

Witaj `IHttpMessageProcessor` implementacji wygląda tak,

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

Została tootake mogli korzystać z [istniejącej biblioteki klienta dla Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) w ten sposób można łatwo toopush `HttpRequestMessage` i `HttpResponseMessage` wystąpienia się ich użytkowania. W kolejności tooaccess hello Runscope interfejsu API, będziesz potrzebować konta i klucz interfejsu API. Instrukcje dotyczące pobierania klucza interfejsu API można znaleźć w hello [tooAccess tworzenie aplikacji interfejsu API Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.

## <a name="complete-sample"></a>Kompletnego przykładu
Witaj [kod źródłowy](https://github.com/darrelmiller/ApimEventProcessor) i testy dla przykładu hello są w serwisie GitHub. Konieczne będzie [usługi interfejsu API zarządzania](api-management-get-started.md), [połączonego Centrum zdarzeń](api-management-howto-log-event-hubs.md), a [konta magazynu](../storage/common/storage-create-storage-account.md) toorun hello próbki dla siebie.   

Witaj próbki jest po prostu prostą aplikację konsoli, która nasłuchuje zdarzenia pochodzące z Centrum zdarzeń, konwertuje je do `HttpRequestMessage` i `HttpResponseMessage` obiekty i przekazuje je na toohello Runscope interfejsu API.

W hello po animowany obraz widoczne wniosku tooan interfejsu API w portalu dla deweloperów, odbierane, hello konsoli aplikacji przedstawiający hello wiadomości powitania przetwarzane i przesyłane dalej i następnie hello żądań i odpowiedzi, które pojawiają się w hello Runscope ruchu Inspektor.

![Pokaz żądanie przesyłane dalej tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Podsumowanie
Usługi Zarządzanie interfejsami API Azure udostępnia ruch hello HTTP toocapture doskonale nadaje się podróży tooand z swoje interfejsy API. Usługa Azure Event Hubs to wysoce skalowalne, ekonomiczne rozwiązanie do przechwytywania tego ruchu i skierowanie go do systemów przetwarzania dodatkowej do rejestrowania, monitorowania i inne zaawansowane opcje analizy. Łączenie too3rd strona ruchu monitorowania systemów, takich jak Runscope jest prostą jako dozen zaledwie kilku wierszach kodu.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat usługi Azure Event Hubs
  * [Wprowadzenie do usługi Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Odbieranie komunikatów za pomocą klasy EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Przewodnik programowania w usłudze Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* Dowiedz się więcej na temat integracji usługi API Management i usługi Event Hubs
  * [Jak toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management](api-management-howto-log-event-hubs.md)
  * [Odwołanie do jednostki rejestratora](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [informacje o zasadach dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
