---
title: "Jak mają być rejestrowane zdarzenia do usługi Azure Event Hubs w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie rejestrowania zdarzeń do usługi Azure Event Hubs w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="02713-103">Jak mają być rejestrowane zdarzenia do usługi Azure Event Hubs w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="02713-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="02713-104">Azure Event Hubs to wysoce skalowalna usługa transferu danych przychodzących, która może obsługiwać miliony zdarzeń na sekundę, dzięki czemu możliwe jest przetwarzanie i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje.</span><span class="sxs-lookup"><span data-stu-id="02713-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="02713-105">Usługa Event Hubs działa jako "drzwi wejściowe" dla potoku zdarzeń, a po pobraniu danych do Centrum zdarzeń, można je przekształcać i przechowywane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania.</span><span class="sxs-lookup"><span data-stu-id="02713-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="02713-106">Usługa Event Hubs oddziela wytwarzanie strumienia zdarzeń od użycia tych zdarzeń, dzięki czemu odbiorcy zdarzeń mogą uzyskiwać dostęp do zdarzeń zgodnie z własnym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="02713-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="02713-107">W tym artykule jest dodatek do [zintegrować zarządzanie interfejsami API Azure z usługą Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) wideo i opisuje sposób rejestrowania zdarzeń interfejsu API zarządzania przy użyciu usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="02713-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="02713-108">Tworzenie Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="02713-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="02713-109">Aby utworzyć nowe Centrum zdarzeń, zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**usługi Service Bus**->**Centrum zdarzeń**->**szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="02713-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="02713-110">Wprowadź nazwę Centrum zdarzeń, region, wybierz subskrypcję, a następnie wybierz obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="02713-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="02713-111">Jeśli nie utworzono jeszcze przestrzeni nazw można go utworzyć, wpisując nazwę w **Namespace** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="02713-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="02713-112">Po skonfigurowaniu wszystkich właściwości, kliknij przycisk **Utwórz nowe Centrum zdarzeń** do tworzenia Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Tworzenie Centrum zdarzeń][create-event-hub]

<span data-ttu-id="02713-114">Następnie przejdź do **Konfiguruj** karcie nowe Centrum zdarzeń i utworzyć dwa **udostępnionych zasady dostępu**.</span><span class="sxs-lookup"><span data-stu-id="02713-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="02713-115">Nazwa pierwszego **wysyłanie** i nadaj mu **wysyłania** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="02713-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Wysyłanie zasad][sending-policy]

<span data-ttu-id="02713-117">Nazwa drugi **odbieranie**, nadaj **nasłuchiwania** uprawnienia, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="02713-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Odebranie zasad][receiving-policy]

<span data-ttu-id="02713-119">Wszystkie zasady dostępu współdzielonego umożliwia aplikacji wysyłanie i odbieranie zdarzeń z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="02713-120">Aby uzyskać dostęp do parametrów połączenia dla tych zasad, przejdź do **pulpitu nawigacyjnego** Centrum zdarzeń i kliknij na karcie **informacje o połączeniu**.</span><span class="sxs-lookup"><span data-stu-id="02713-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Parametry połączenia][event-hub-dashboard]

<span data-ttu-id="02713-122">**Wysyłanie** ciąg połączenia jest używany podczas rejestrowania zdarzeń i **odbieranie** ciąg połączenia jest używany podczas pobierania zdarzeń z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Parametry połączenia][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="02713-124">Utworzyć zarządzanie interfejsami API rejestratora</span><span class="sxs-lookup"><span data-stu-id="02713-124">Create an API Management logger</span></span>
<span data-ttu-id="02713-125">Teraz, gdy masz Centrum zdarzeń, następnym krokiem jest skonfigurowanie [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) w zarządzania infrastrukturą interfejsu API usługi tak, aby móc zarejestrować zdarzenia do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="02713-126">Zarządzanie interfejsami API rejestratorów są skonfigurowane przy użyciu [interfejsu API REST zarządzania interfejsu API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="02713-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="02713-127">Przed rozpoczęciem korzystania z interfejsu API REST po raz pierwszy, przejrzyj [wymagania wstępne](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) i upewnij się, że masz [włączony dostęp do interfejsu API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="02713-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="02713-128">Aby utworzyć rejestrator, należy przy użyciu następującego szablonu adresu URL żądania HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="02713-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="02713-129">Zastąp `{your service}` nazwą wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="02713-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="02713-130">Zastąp `{new logger name}` z żądaną nazwą dla Twojego nowego rejestratora.</span><span class="sxs-lookup"><span data-stu-id="02713-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="02713-131">Ta nazwa będzie odwoływać, podczas konfigurowania [dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) zasad</span><span class="sxs-lookup"><span data-stu-id="02713-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="02713-132">Dodaj następujące nagłówki na żądanie.</span><span class="sxs-lookup"><span data-stu-id="02713-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="02713-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="02713-133">Content-Type : application/json</span></span>
* <span data-ttu-id="02713-134">Autoryzacji: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="02713-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="02713-135">Aby uzyskać instrukcje dotyczące generowania `SharedAccessSignature` zobacz [Azure API Management REST API uwierzytelniania](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="02713-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="02713-136">Określ treści żądania, korzystając z poniższego szablonu.</span><span class="sxs-lookup"><span data-stu-id="02713-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="02713-137">`type`należy wybrać opcję `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="02713-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="02713-138">`description`zapewnia opcjonalny opis rejestratora i w razie potrzeby może być ciągiem o zerowej długości.</span><span class="sxs-lookup"><span data-stu-id="02713-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="02713-139">`credentials`zawiera `name` i `connectionString` Azure Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="02713-140">Po dokonaniu żądania, jeśli rejestrator jest tworzony kod stanu `201 Created` jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="02713-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="02713-141">Pozostałe możliwe kody powrotu i ich przyczyny, zobacz [utworzyć Rejestrator](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="02713-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="02713-142">Aby zobaczyć, jak wykonywać inne operacje, takie jak listy, update i delete, zobacz [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dokumentacji jednostki.</span><span class="sxs-lookup"><span data-stu-id="02713-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="02713-143">Konfigurowanie zasad dziennika do eventhubs</span><span class="sxs-lookup"><span data-stu-id="02713-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="02713-144">Po Twoje rejestratora jest skonfigurowany w usłudze API Management, można skonfigurować zasad dziennika do eventhubs żądanego zdarzenia logowania.</span><span class="sxs-lookup"><span data-stu-id="02713-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="02713-145">Zasada dziennika do eventhubs może służyć w sekcji zasady ruchu przychodzącego lub sekcji zasady ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="02713-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="02713-146">Aby skonfigurować zasady, zaloguj się do [portalu Azure](https://portal.azure.com), przejdź do usługi API Management i kliknij przycisk **portal wydawcy** dostęp do portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="02713-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Portal wydawcy][publisher-portal]

<span data-ttu-id="02713-148">Kliknij przycisk **zasady** zarządzanie interfejsami API menu po lewej stronie, wybierz żądany produktu i interfejsu API, a następnie kliknij przycisk **Dodaj zasady**.</span><span class="sxs-lookup"><span data-stu-id="02713-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="02713-149">W tym przykładzie Trwa dodawanie zasad, aby **Echo API** w **nieograniczone** produktu.</span><span class="sxs-lookup"><span data-stu-id="02713-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Dodawanie zasad][add-policy]

<span data-ttu-id="02713-151">Umieść kursor w `inbound` sekcji zasad i kliknij przycisk **dziennika do Centrum EventHub** zasad, aby wstawić `log-to-eventhub` szablon zasad w instrukcji.</span><span class="sxs-lookup"><span data-stu-id="02713-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Edytor zasad][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="02713-153">Zastąp `logger-id` nazwą rejestratora zarządzanie interfejsami API skonfigurowana w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="02713-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="02713-154">Można użyć dowolne wyrażenie zwracające ciąg jako wartość `log-to-eventhub` elementu.</span><span class="sxs-lookup"><span data-stu-id="02713-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="02713-155">W tym przykładzie jest rejestrowane ciąg zawierający daty i godziny, nazwę usługi, identyfikator żądania, żądania adresu ip oraz nazwy operacji.</span><span class="sxs-lookup"><span data-stu-id="02713-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="02713-156">Kliknij przycisk **zapisać** Aby zapisać konfigurację zaktualizowane zasady.</span><span class="sxs-lookup"><span data-stu-id="02713-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="02713-157">Natychmiast po ich zapisaniu zasady są aktywne, a zdarzenia są rejestrowane w wyznaczonym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02713-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02713-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02713-158">Next steps</span></span>
* <span data-ttu-id="02713-159">Dowiedz się więcej na temat usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="02713-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="02713-160">Wprowadzenie do usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="02713-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="02713-161">Odbieranie komunikatów za pomocą klasy EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="02713-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="02713-162">Przewodnik programowania w usłudze Event Hubs</span><span class="sxs-lookup"><span data-stu-id="02713-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="02713-163">Dowiedz się więcej na temat integracji usługi API Management i usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="02713-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="02713-164">Odwołanie do jednostki rejestratora</span><span class="sxs-lookup"><span data-stu-id="02713-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="02713-165">informacje o zasadach dziennika do Centrum eventhub</span><span class="sxs-lookup"><span data-stu-id="02713-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="02713-166">Monitoruj swoje interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope</span><span class="sxs-lookup"><span data-stu-id="02713-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="02713-167">Obejrzyj przewodnik wideo</span><span class="sxs-lookup"><span data-stu-id="02713-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
