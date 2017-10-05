---
title: "Monitorowanie interfejsów API za pomocą usługi Azure API Management, usługa Event Hubs i Runscope | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja prezentacja zasad dziennika do Centrum eventhub połączenia usługi Azure API Management, Azure Event Hubs i Runscope dla protokołu HTTP, rejestrowania i monitorowania"
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
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="6b133-103">Monitoruj swoje interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope</span><span class="sxs-lookup"><span data-stu-id="6b133-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="6b133-104">[Usługi Zarządzanie interfejsami API](api-management-key-concepts.md) zawiera wiele możliwości przetwarzania żądania HTTP wysyłane do interfejsu API protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b133-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="6b133-105">Istnienie żądań i odpowiedzi są jednak przejściowej.</span><span class="sxs-lookup"><span data-stu-id="6b133-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="6b133-106">Żądanie, a następnie za pomocą usługi Zarządzanie interfejsami API z wewnętrzną bazą danych interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="6b133-107">Interfejs API przetwarza żądania i odpowiedzi przechodzi wstecz przez konsumenta interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="6b133-108">Usługi Zarządzanie interfejsami API utrzymuje niektórych ważnych statystyk dotyczących interfejsów API do wyświetlenia na pulpicie nawigacyjnym portalu wydawcy w ale ponad, czy szczegóły znikną.</span><span class="sxs-lookup"><span data-stu-id="6b133-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="6b133-109">Za pomocą [dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [zasad](api-management-howto-policies.md) usługi Zarządzanie interfejsami API można wysyłać żadnych szczegółów z żądania i odpowiedzi na [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="6b133-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="6b133-110">Istnieje wiele przyczyn, dlaczego warto generowanie zdarzeń z wiadomości HTTP są wysyłane do swoje interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="6b133-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="6b133-111">Oto kilka przykładów dziennik inspekcji aktualizacji, analizy użycia, alerty wyjątków i 3 integracji strony.</span><span class="sxs-lookup"><span data-stu-id="6b133-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="6b133-112">W tym artykule przedstawiono sposób przechwytywania cały komunikat żądania i odpowiedzi HTTP, wysyłają je do Centrum zdarzeń i następnie przekazywania wiadomości osobie trzeciej usługa, która zapewnia HTTP rejestrowania i monitorowania usług.</span><span class="sxs-lookup"><span data-stu-id="6b133-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="6b133-113">Dlaczego należy wysłać z interfejsu API usługi zarządzania?</span><span class="sxs-lookup"><span data-stu-id="6b133-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="6b133-114">Istnieje możliwość zapisu oprogramowania pośredniczącego protokołu HTTP, który można podłączyć do struktur HTTP API do przechwytywania żądań i odpowiedzi HTTP i ich źródła do rejestrowania i monitorowania systemów.</span><span class="sxs-lookup"><span data-stu-id="6b133-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="6b133-115">Wadą tego podejścia interfejsu jest oprogramowanie pośredniczące HTTP musi być zintegrowane zaplecza interfejsu API i musi odpowiadać platformy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="6b133-116">Jeśli istnieje wiele interfejsów API każdej z nich należy wdrożyć oprogramowanie pośredniczące.</span><span class="sxs-lookup"><span data-stu-id="6b133-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="6b133-117">Często jest przyczyn, dlaczego nie można zaktualizować interfejsów API w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6b133-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="6b133-118">Za pomocą usługi Zarządzanie interfejsami API Azure do integracji z infrastrukturą rejestrowania zapewnia rozwiązanie scentralizowany i niezależne od platformy.</span><span class="sxs-lookup"><span data-stu-id="6b133-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="6b133-119">Jest również skalowalne, w części ze względu na [— replikacja geograficzna](api-management-howto-deploy-multi-region.md) możliwości usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="6b133-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="6b133-120">Dlaczego są wysyłane do usługi Azure Event Hub?</span><span class="sxs-lookup"><span data-stu-id="6b133-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="6b133-121">Jest to uzasadnione na pytanie, dlaczego Tworzenie zasad, które są specyficzne dla usługi Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="6b133-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="6b133-122">Istnieje wiele różnych miejscach, w którym chcieć Moje żądania logowania.</span><span class="sxs-lookup"><span data-stu-id="6b133-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="6b133-123">Dlaczego nie wystarczy wysłać żądania bezpośrednio do końcowego miejsca docelowego?</span><span class="sxs-lookup"><span data-stu-id="6b133-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="6b133-124">To opcja.</span><span class="sxs-lookup"><span data-stu-id="6b133-124">That is an option.</span></span> <span data-ttu-id="6b133-125">Podczas tworzenia żądania rejestrowania z interfejsu API usługi zarządzania, należy wziąć pod uwagę, jak rejestrowanie komunikatów ma wpływ na wydajność, interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="6b133-126">Stopniowa wzrost obciążenia są obsługiwane przez odpowiednie zwiększenie dostępnych wystąpień składników systemu, czy dzięki wykorzystaniu — replikacja geograficzna.</span><span class="sxs-lookup"><span data-stu-id="6b133-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="6b133-127">Krótki największego ruchu może jednak spowodować żądań znacznie opóźnionych żądań rejestrowania infrastruktury uruchomić zmniejszyć obciążenie.</span><span class="sxs-lookup"><span data-stu-id="6b133-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="6b133-128">Azure Event Hubs jest przeznaczona do transferu dużych ilości danych, o pojemności na potrzeby zajmujących się znacznie większej liczby zdarzeń niż liczba żądań HTTP większości procesu interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="6b133-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="6b133-129">Centrum zdarzeń pełni rolę bufora zaawansowane między usługą zarządzania interfejsu API i infrastrukturę, która będzie przechowywać i przetwarzać komunikaty.</span><span class="sxs-lookup"><span data-stu-id="6b133-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="6b133-130">Dzięki temu, że z powodu infrastruktury rejestrowania nie będzie pogorszyć wydajność z interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="6b133-131">Gdy dane został przekazany do Centrum zdarzeń jest trwały i będzie oczekiwał na konsumentów Centrum zdarzeń go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="6b133-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="6b133-132">Centrum zdarzeń nie zależy sposób przetwarzania, ją po prostu dba upewnienie się, że wiadomość zostanie dostarczona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6b133-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="6b133-133">Centra zdarzeń mają możliwość strumienia zdarzeń do wielu grup odbiorców.</span><span class="sxs-lookup"><span data-stu-id="6b133-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="6b133-134">Dzięki temu zdarzenia, które mają być przetwarzane przez całkowicie różnych systemów.</span><span class="sxs-lookup"><span data-stu-id="6b133-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="6b133-135">Dzięki temu, obsługa wielu scenariuszy integracji bez umieszczania Dodawanie opóźnień w przetwarzania żądania interfejsu API w usłudze API Management, jak tylko jedno zdarzenie ma zostać wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="6b133-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="6b133-136">Zasady do wysyłania wiadomości protokół http i aplikacji</span><span class="sxs-lookup"><span data-stu-id="6b133-136">A policy to send application/http messages</span></span>
<span data-ttu-id="6b133-137">Centrum zdarzeń akceptuje dane zdarzeń prosty ciąg znaków.</span><span class="sxs-lookup"><span data-stu-id="6b133-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="6b133-138">Zawartość tego ciągu jest całkowicie od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b133-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="6b133-139">Aby można było spakować żądania HTTP i wysłania go do usługi Event Hubs należy sformatować ciągu z żądania lub odpowiedzi informacji.</span><span class="sxs-lookup"><span data-stu-id="6b133-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="6b133-140">W sytuacjach, takich jak ta Jeśli istniejący format można ponownie użyć, a następnie firma Microsoft nie trzeba napisać własne analizy kodu.</span><span class="sxs-lookup"><span data-stu-id="6b133-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="6b133-141">Początkowo I uznawane za pomocą [HAR](http://www.softwareishard.com/blog/har-12-spec/) do wysyłania żądań i odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b133-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="6b133-142">Jednak ten format jest zoptymalizowany do przechowywania w formacie JSON na podstawie sekwencji żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b133-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="6b133-143">Zawiera liczbę obowiązkowe elementy dodane niepotrzebnych złożoności scenariusza przekazywania komunikatu HTTP przez sieć.</span><span class="sxs-lookup"><span data-stu-id="6b133-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="6b133-144">Opcja alternatywna było jednoczesne używanie `application/http` typ nośnika zgodnie z opisem w specyfikacji HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="6b133-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="6b133-145">Ten typ nośnika używa dokładnie tego samego formatu używanego do faktycznego wysyłania wiadomości HTTP przez sieć, ale cały komunikat można umieścić w treści żądania HTTP innego.</span><span class="sxs-lookup"><span data-stu-id="6b133-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="6b133-146">W tym przypadku po prostu zamierzamy być treści wiadomości do wysłania do usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="6b133-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="6b133-147">Wygodnie jest analizatorem w [klienta Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotek, które mogą przeanalizować tego formatu oraz przekształcać je do natywnego `HttpRequestMessage` i `HttpResponseMessage` obiektów.</span><span class="sxs-lookup"><span data-stu-id="6b133-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="6b133-148">Aby można było utworzyć tę wiadomość należy przeprowadzać na podstawie języka C# [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx) w usłudze Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="6b133-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="6b133-149">Poniżej przedstawiono zasady, która wysyła komunikat żądania HTTP do usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="6b133-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="6b133-150">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="6b133-150">Policy declaration</span></span>
<span data-ttu-id="6b133-151">Istnieje kilka rzeczy określonego warto zauważyć o wyrażenie zasad.</span><span class="sxs-lookup"><span data-stu-id="6b133-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="6b133-152">Zasada dziennika do Centrum eventhub ma atrybut o nazwie rejestratora id, który odwołuje się do nazwy rejestratora, który został utworzony w ramach usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="6b133-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="6b133-153">Szczegóły dotyczące konfiguracji rejestratora Centrum zdarzeń w usłudze API Management znajduje się w dokumencie [sposób rejestrowania zdarzeń do usługi Azure Event Hubs w usłudze Azure API Management](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="6b133-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="6b133-154">Drugi atrybut jest opcjonalnym parametrem, który powoduje, że usługa Event Hubs, która partycji do przechowywania wiadomości w.</span><span class="sxs-lookup"><span data-stu-id="6b133-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="6b133-155">Centra zdarzeń partycje służą do włączenia scalabilty i wymagają co najmniej dwa.</span><span class="sxs-lookup"><span data-stu-id="6b133-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="6b133-156">Uporządkowanego dostarczenia komunikatów jest gwarantowaną jedynie w partycji.</span><span class="sxs-lookup"><span data-stu-id="6b133-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="6b133-157">Jeśli można wydać Centrum zdarzeń, w których partycji można umieścić wiadomości, zostanie użyty algorytm okrężnego rozłożenie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6b133-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="6b133-158">Mogą jednak powodować niektóre nasze komunikaty do przetwarzania poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="6b133-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="6b133-159">Partycje</span><span class="sxs-lookup"><span data-stu-id="6b133-159">Partitions</span></span>
<span data-ttu-id="6b133-160">Aby zapewnić naszym wiadomości są dostarczane do odbiorców w kolejności i skorzystać z zalet możliwości rozkładu obciążenia partycji, wybrano wysyłać żądania HTTP do jednej partycji i komunikatów odpowiedzi HTTP do drugiej partycji.</span><span class="sxs-lookup"><span data-stu-id="6b133-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="6b133-161">Zapewni to rozkład obciążenia nawet i można gwarantujemy, że wszystkie żądania, które będą używane w kolejności i wszystkie odpowiedzi zostaną użyte w kolejności.</span><span class="sxs-lookup"><span data-stu-id="6b133-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="6b133-162">Istnieje możliwość odpowiedzi zużywanych przed odpowiednie żądanie, ale który nie jest problem jak mamy inny mechanizm korelowanie żądania do odpowiedzi i wiemy, że żądania zawsze występować przed odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6b133-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="6b133-163">Ładunki HTTP</span><span class="sxs-lookup"><span data-stu-id="6b133-163">HTTP payloads</span></span>
<span data-ttu-id="6b133-164">Po budynku `requestLine` możemy sprawdzić, czy obcięte treści żądania.</span><span class="sxs-lookup"><span data-stu-id="6b133-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="6b133-165">Treść żądania jest obcinana tylko 1024 znaki.</span><span class="sxs-lookup"><span data-stu-id="6b133-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="6b133-166">To można zwiększyć, ale poszczególne wiadomości Centrum zdarzeń są ograniczone do 256KB, więc istnieje duże prawdopodobieństwo, że niektóre komunikaty HTTP organów zostanie nie mieści się w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="6b133-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="6b133-167">Podczas rejestrowania i analiza znaczną ilość informacji mogą pochodzić z właśnie wiersz żądania HTTP i nagłówków.</span><span class="sxs-lookup"><span data-stu-id="6b133-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="6b133-168">Ponadto wiele żądań interfejsu API zwracać tylko małych jednostek, i dlatego utraty wartość informacji przez Obcinanie dużych jednostek jest dość minimalnego w odróżnieniu od skrócenie transferu, przetwarzania i kosztów magazynowania, aby zachować całą zawartość treści.</span><span class="sxs-lookup"><span data-stu-id="6b133-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="6b133-169">Jeden końcowego Uwaga dotycząca przetwarzanie treści jest potrzebujemy przekazać `true` do As<string>— metoda () ponieważ firma Microsoft czytają zawartość treści, jednak podano również mają zaplecza interfejsu API, aby można było odczytać treści.</span><span class="sxs-lookup"><span data-stu-id="6b133-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="6b133-170">Przekazując wartość PRAWDA, aby ta metoda możemy spowodować jednostkę do buforowanego, dzięki czemu mogą być odczytywane po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="6b133-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="6b133-171">Jest to ważne, należy pamiętać o Jeśli interfejs API, który nie przekazywania bardzo dużych plików ani nie używa długiego sondowania.</span><span class="sxs-lookup"><span data-stu-id="6b133-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="6b133-172">W takich przypadkach byłoby unikanie odczytu treści w ogóle.</span><span class="sxs-lookup"><span data-stu-id="6b133-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="6b133-173">Nagłówki HTTP</span><span class="sxs-lookup"><span data-stu-id="6b133-173">HTTP headers</span></span>
<span data-ttu-id="6b133-174">Nagłówki HTTP może być po prostu transferowanych za pośrednictwem do formatu wiadomości w formacie pary klucz/wartość prostą.</span><span class="sxs-lookup"><span data-stu-id="6b133-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="6b133-175">Wybraliśmy usuwają niektórych zabezpieczeń pól, aby uniknąć niepotrzebnego przeciek informacji o poświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="6b133-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="6b133-176">Jest mało prawdopodobne, że klucze interfejsu API i inne poświadczenia mają być używane do celów analizy.</span><span class="sxs-lookup"><span data-stu-id="6b133-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="6b133-177">Jeśli Życzymy czy analizy na użytkownika i określonego produktu używają, można pobrać z `context` obiektu i dodać go do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6b133-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="6b133-178">Komunikat metadanych</span><span class="sxs-lookup"><span data-stu-id="6b133-178">Message Metadata</span></span>
<span data-ttu-id="6b133-179">Podczas kompilowania pełny komunikat do wysłania do Centrum zdarzeń, pierwszy wiersz nie jest częścią faktycznie `application/http` wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6b133-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="6b133-180">Pierwszy wiersz jest dodatkowe metadane składające się z tego, czy wiadomość jest żądanie lub komunikat odpowiedzi i identyfikator komunikatu, który służy do skorelowania żądań do odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6b133-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="6b133-181">Identyfikator komunikatu jest tworzona przy użyciu innej zasady, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6b133-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="6b133-182">Firma Microsoft może utworzyć komunikat żądania, który przechowywana w zmiennej, dopóki odpowiedzi został zwrócony, a następnie po prostu wysyłała żądań i odpowiedzi jako pojedynczy komunikat.</span><span class="sxs-lookup"><span data-stu-id="6b133-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="6b133-183">Jednak wysyłania żądań i odpowiedzi niezależnie i za pomocą identyfikatora komunikatu do skorelowania dwa, uzyskujemy nieco większą elastyczność w rozmiar komunikatu, możliwość wykorzystania wiele partycji, jednocześnie zachowując kolejność wiadomości i żądania zostanie wyświetlony w naszym rejestrowania pulpitu nawigacyjnego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6b133-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="6b133-184">Może istnieć sytuacje, w których prawidłowej odpowiedzi nigdy nie są wysyłane do Centrum zdarzeń, prawdopodobnie z powodu błędu krytycznego żądania w usłudze API Management, ale wciąż będzie istnieje rekord żądania.</span><span class="sxs-lookup"><span data-stu-id="6b133-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="6b133-185">Zasady można wysłać komunikatu odpowiedzi HTTP wygląda bardzo podobnie do żądania i dlatego konfiguracji zasad pełną wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6b133-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="6b133-186">`set-variable` Zasad tworzy wartość, który jest dostępny dla obu `log-to-eventhub` zasad w `<inbound>` sekcji i `<outbound>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="6b133-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="6b133-187">Odbieranie zdarzeń z usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b133-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="6b133-188">Zdarzenia z Centrum zdarzeń Azure są odbierane przy użyciu [protokołu AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="6b133-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="6b133-189">Zespół Microsoft Service Bus zostały wprowadzone klienta biblioteki dostępne ułatwić korzystanie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="6b133-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="6b133-190">Istnieją dwa różne podejścia obsługiwane, co jest *konsumenta bezpośredniego* , a drugi używa `EventProcessorHost` klasy.</span><span class="sxs-lookup"><span data-stu-id="6b133-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="6b133-191">Przykłady te dwie metody znajdują się w [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6b133-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="6b133-192">Jest krótkiej różnice, `Direct Consumer` umożliwia pełną kontrolę i `EventProcessorHost` wykonuje część pracy żmudne procesy, dla ale powoduje pewne założenia, o jaki będzie przetwarzać tych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="6b133-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="6b133-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="6b133-193">EventProcessorHost</span></span>
<span data-ttu-id="6b133-194">W tym przykładzie używamy `EventProcessorHost` dla uproszczenia, jednak może ona nie najlepszym rozwiązaniem dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="6b133-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="6b133-195">`EventProcessorHost`wykonuje pracę twardych zagwarantowanie, że nie trzeba martwić wątkowość problemów w obrębie klasy procesora konkretnego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="6b133-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="6b133-196">Jednak w naszym scenariuszu firma Microsoft są po prostu Konwertowanie wiadomości do innego formatu i przekazanie jej wraz z inną usługą przy użyciu metody asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="6b133-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="6b133-197">Nie istnieje potrzeba aktualizowania stanu udostępnionego i w związku z tym ryzyko problemy wielowątkowości.</span><span class="sxs-lookup"><span data-stu-id="6b133-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="6b133-198">W przypadku większości scenariuszy `EventProcessorHost` najlepszym rozwiązaniem jest prawdopodobnie i na pewno jest łatwiejsze opcji.</span><span class="sxs-lookup"><span data-stu-id="6b133-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="6b133-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="6b133-199">IEventProcessor</span></span>
<span data-ttu-id="6b133-200">Centralna koncepcji przy użyciu `EventProcessorHost` jest utworzenie implementacja `IEventProcessor` interfejs, który zawiera metodę `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="6b133-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="6b133-201">Użycia tej metody jest następujący:</span><span class="sxs-lookup"><span data-stu-id="6b133-201">The essence of that method is shown here:</span></span>

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

<span data-ttu-id="6b133-202">Lista obiektów EventData są przekazywane do metody i możemy iteracja tej listy.</span><span class="sxs-lookup"><span data-stu-id="6b133-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="6b133-203">Bajty każdej metody są parsowane do obiektu HttpMessage, a ten obiekt jest przekazywana do wystąpienia IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="6b133-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="6b133-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="6b133-204">HttpMessage</span></span>
<span data-ttu-id="6b133-205">`HttpMessage` Wystąpienia zawiera trzy elementy danych:</span><span class="sxs-lookup"><span data-stu-id="6b133-205">The `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="6b133-206">`HttpMessage` Wystąpienie zawiera `MessageId` identyfikator GUID, który pozwala na żądania HTTP łączyć się z odpowiedniego odpowiedzi HTTP i wartość logiczna, która określa, czy obiekt zawiera wystąpienie HttpRequestMessage i HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="6b133-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="6b133-207">Przy użyciu wbudowanych w klasach HTTP z `System.Net.Http`, I mógł korzystać z `application/http` analizy kodu, który znajduje się w `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="6b133-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="6b133-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="6b133-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="6b133-209">`HttpMessage` Wystąpienia jest następnie przekazywane do wykonania `IHttpMessageProcessor` czyli interfejs został utworzony na odłączeniu odbieranie i interpretacji zdarzenia z Centrum zdarzeń platformy Azure i odpowiada za przetwarzanie.</span><span class="sxs-lookup"><span data-stu-id="6b133-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="6b133-210">Przekazywanie komunikatów HTTP</span><span class="sxs-lookup"><span data-stu-id="6b133-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="6b133-211">Dla tego przykładu I uzgodnionych byłoby interesujące do dystrybuowania żądań HTTP za pośrednictwem do [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="6b133-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="6b133-212">Runscope to usługa w chmurze, która specjalizuje się w protokole HTTP, debugowanie, rejestrowania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="6b133-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="6b133-213">Mają one warstwę bezpłatna, dzięki czemu ułatwia spróbuj i pozwala zobaczyć żądania HTTP do transmisji w czasie rzeczywistym za pomocą naszej usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="6b133-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="6b133-214">`IHttpMessageProcessor` Implementacji wygląda tak,</span><span class="sxs-lookup"><span data-stu-id="6b133-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="6b133-215">I mógł korzystać z [istniejącej biblioteki klienta dla Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) ułatwia wypchnąć `HttpRequestMessage` i `HttpResponseMessage` wystąpienia się ich użytkowania.</span><span class="sxs-lookup"><span data-stu-id="6b133-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="6b133-216">Aby uzyskać dostęp do interfejsu API Runscope należy konta i klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b133-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="6b133-217">Instrukcje dotyczące pobierania klucza interfejsu API można znaleźć w [tworzenie aplikacji interfejsu API Runscope dostępu](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="6b133-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="6b133-218">Kompletnego przykładu</span><span class="sxs-lookup"><span data-stu-id="6b133-218">Complete sample</span></span>
<span data-ttu-id="6b133-219">[Kod źródłowy](https://github.com/darrelmiller/ApimEventProcessor) i testy przykładowej są w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b133-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="6b133-220">Konieczne będzie [usługi interfejsu API zarządzania](api-management-get-started.md), [połączonego Centrum zdarzeń](api-management-howto-log-event-hubs.md), a [konta magazynu](../storage/common/storage-create-storage-account.md) do uruchomienia przykładu dla siebie.</span><span class="sxs-lookup"><span data-stu-id="6b133-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="6b133-221">Próbka jest po prostu prostą aplikację konsoli, która nasłuchuje zdarzenia pochodzące z Centrum zdarzeń, konwertuje je do `HttpRequestMessage` i `HttpResponseMessage` obiekty i przekazuje je do interfejsu API Runscope.</span><span class="sxs-lookup"><span data-stu-id="6b133-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="6b133-222">Na poniższej ilustracji animowany widać żądanie do interfejsu API w portalu dla deweloperów aplikacji konsoli przedstawiający wiadomości odebrane, przetwarzane i przesyłane dalej, a następnie żądania i odpowiedzi, które pojawiają się w inspektora Runscope ruchu.</span><span class="sxs-lookup"><span data-stu-id="6b133-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Pokaz żądanie przesyłane dalej do Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="6b133-224">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6b133-224">Summary</span></span>
<span data-ttu-id="6b133-225">Usługi Zarządzanie interfejsami API Azure udostępnia doskonale nadaje się do przechwytywania ruchu HTTP do i z swoje interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="6b133-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="6b133-226">Usługa Azure Event Hubs to wysoce skalowalne, ekonomiczne rozwiązanie do przechwytywania tego ruchu i skierowanie go do systemów przetwarzania dodatkowej do rejestrowania, monitorowania i inne zaawansowane opcje analizy.</span><span class="sxs-lookup"><span data-stu-id="6b133-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="6b133-227">Łączenie z usługą 3 ruchu strony monitorowanie systemów, takich jak Runscope jest prostą jako dozen zaledwie kilku wierszach kodu.</span><span class="sxs-lookup"><span data-stu-id="6b133-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b133-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b133-228">Next steps</span></span>
* <span data-ttu-id="6b133-229">Dowiedz się więcej na temat usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b133-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="6b133-230">Wprowadzenie do usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b133-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="6b133-231">Odbieranie komunikatów za pomocą klasy EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="6b133-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="6b133-232">Przewodnik programowania w usłudze Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b133-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="6b133-233">Dowiedz się więcej na temat integracji usługi API Management i usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b133-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="6b133-234">Jak mają być rejestrowane zdarzenia do usługi Azure Event Hubs w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="6b133-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="6b133-235">Odwołanie do jednostki rejestratora</span><span class="sxs-lookup"><span data-stu-id="6b133-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="6b133-236">informacje o zasadach dziennika do Centrum eventhub</span><span class="sxs-lookup"><span data-stu-id="6b133-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
