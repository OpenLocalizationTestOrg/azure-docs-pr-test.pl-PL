---
title: "aaaHow toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management."
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
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="13ed0-103">Jak toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="13ed0-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="13ed0-104">Usługa Azure Event Hubs to wysoce skalowalna Usługa transferu danych, który może obsługiwać miliony zdarzeń na sekundę, dzięki czemu możliwe jest przetwarzanie i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello.</span><span class="sxs-lookup"><span data-stu-id="13ed0-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="13ed0-105">Usługa Event Hubs działa jako "drzwi wejściowe" dla potoku zdarzeń hello, a po pobraniu danych do Centrum zdarzeń, można je przekształcać i przechowywane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania.</span><span class="sxs-lookup"><span data-stu-id="13ed0-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="13ed0-106">Usługa Event Hubs oddziela hello Wytwarzanie strumienia zdarzeń od użycia hello tych zdarzeń, dzięki czemu odbiorcy zdarzeń mogą uzyskiwać dostęp do zdarzeń hello w swoim własnym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="13ed0-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="13ed0-107">W tym artykule jest toohello Pomocnika [zintegrować zarządzanie interfejsami API Azure z usługą Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) wideo i opisano sposób toolog zarządzanie interfejsami API zdarzenia przy użyciu usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="13ed0-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="13ed0-108">Tworzenie Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13ed0-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="13ed0-109">toocreate z nowym Centrum zdarzeń logowania toohello [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**usługi Service Bus ** -> **Centrum zdarzeń**->**szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="13ed0-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="13ed0-110">Wprowadź nazwę Centrum zdarzeń, region, wybierz subskrypcję, a następnie wybierz obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="13ed0-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="13ed0-111">Jeśli nie utworzono jeszcze przestrzeni nazw można go utworzyć, wpisując nazwę w hello **Namespace** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="13ed0-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="13ed0-112">Po skonfigurowaniu wszystkich właściwości, kliknij przycisk **Utwórz nowe Centrum zdarzeń** hello toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Tworzenie Centrum zdarzeń][create-event-hub]

<span data-ttu-id="13ed0-114">Następnie przejdź toohello **Konfiguruj** karcie nowe Centrum zdarzeń i utworzyć dwa **udostępnionych zasady dostępu**.</span><span class="sxs-lookup"><span data-stu-id="13ed0-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="13ed0-115">Nazwa pierwszej hello **wysyłanie** i nadaj mu **wysyłania** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="13ed0-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Wysyłanie zasad][sending-policy]

<span data-ttu-id="13ed0-117">Nazwa hello drugi **odbieranie**, nadaj **nasłuchiwania** uprawnienia, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="13ed0-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Odebranie zasad][receiving-policy]

<span data-ttu-id="13ed0-119">Wszystkie zasady dostępu współdzielonego umożliwia toosend aplikacji i otrzymywać zdarzeń tooand hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="13ed0-120">Parametry połączenia hello tooaccess dla tych zasad Przejdź toohello **pulpitu nawigacyjnego** hello Centrum zdarzeń i kliknij na karcie **informacje o połączeniu**.</span><span class="sxs-lookup"><span data-stu-id="13ed0-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Parametry połączenia][event-hub-dashboard]

<span data-ttu-id="13ed0-122">Witaj **wysyłanie** ciąg połączenia jest używany podczas rejestrowania zdarzeń i hello **odbieranie** ciąg połączenia jest używany podczas pobierania zdarzeń z hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Parametry połączenia][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="13ed0-124">Utworzyć zarządzanie interfejsami API rejestratora</span><span class="sxs-lookup"><span data-stu-id="13ed0-124">Create an API Management logger</span></span>
<span data-ttu-id="13ed0-125">Teraz, gdy masz Centrum zdarzeń hello następnym krokiem jest tooconfigure [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) w zarządzania infrastrukturą interfejsu API usługi tak, aby móc zarejestrować zdarzenia toohello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="13ed0-126">Zarządzanie interfejsami API rejestratorów są skonfigurowane przy użyciu hello [interfejsu API REST zarządzania interfejsu API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="13ed0-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="13ed0-127">Przed użyciem hello interfejsu API REST dla powitania po raz pierwszy, przejrzyj hello [wymagania wstępne](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) i upewnij się, że masz [włączone toohello dostępu do interfejsu API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="13ed0-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="13ed0-128">toocreate rejestratora, upewnij się przy użyciu powitania po szablon adresu URL żądania HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="13ed0-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="13ed0-129">Zastąp `{your service}` o nazwie hello wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="13ed0-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="13ed0-130">Zastąp `{new logger name}` nazwą hello odpowiednią dla Twojego nowego rejestratora.</span><span class="sxs-lookup"><span data-stu-id="13ed0-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="13ed0-131">Po skonfigurowaniu hello będzie odwoływać się ta nazwa [dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) zasad</span><span class="sxs-lookup"><span data-stu-id="13ed0-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="13ed0-132">Dodaj następujące nagłówki żądania toohello hello.</span><span class="sxs-lookup"><span data-stu-id="13ed0-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="13ed0-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="13ed0-133">Content-Type : application/json</span></span>
* <span data-ttu-id="13ed0-134">Autoryzacji: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="13ed0-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="13ed0-135">Aby uzyskać instrukcje dotyczące generowania hello `SharedAccessSignature` zobacz [Azure API Management REST API uwierzytelniania](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="13ed0-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="13ed0-136">Określ hello treści żądania przy użyciu następującego szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="13ed0-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="13ed0-137">`type`musi być ustawiona zbyt`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="13ed0-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="13ed0-138">`description`zapewnia opcjonalny opis rejestratora hello i w razie potrzeby może być ciągiem o zerowej długości.</span><span class="sxs-lookup"><span data-stu-id="13ed0-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="13ed0-139">`credentials`zawiera hello `name` i `connectionString` Azure Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="13ed0-140">Po dokonaniu hello żądania, jeśli Rejestrator hello jest tworzony kod stanu `201 Created` jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="13ed0-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="13ed0-141">Pozostałe możliwe kody powrotu i ich przyczyny, zobacz [utworzyć Rejestrator](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="13ed0-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="13ed0-142">toosee jak wykonywać inne operacje, takie jak listy, update i delete, zobacz hello [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dokumentacji jednostki.</span><span class="sxs-lookup"><span data-stu-id="13ed0-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="13ed0-143">Konfigurowanie zasad dziennika do eventhubs</span><span class="sxs-lookup"><span data-stu-id="13ed0-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="13ed0-144">Po Twoje rejestratora jest skonfigurowany w usłudze API Management, można skonfigurować zasady dziennika do eventhubs toolog hello potrzeby zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="13ed0-145">Witaj dziennika do eventhubs zasady mogą być używane w obu hello sekcji zasady ruchu przychodzącego lub hello wychodzącego zasad sekcji.</span><span class="sxs-lookup"><span data-stu-id="13ed0-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="13ed0-146">tooconfigure zasad logowania toohello [portalu Azure](https://portal.azure.com), przejdź do usługi API Management tooyour i kliknij **portal wydawcy** tooaccess hello portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="13ed0-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portal wydawcy][publisher-portal]

<span data-ttu-id="13ed0-148">Kliknij przycisk **zasady** w menu Zarządzanie interfejsami API hello powitania po lewej stronie, wybierz żądany produkt hello i interfejsu API, a następnie kliknij przycisk **Dodaj zasady**.</span><span class="sxs-lookup"><span data-stu-id="13ed0-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="13ed0-149">W tym przykładzie Trwa dodawanie toohello zasad **Echo API** w hello **nieograniczone** produktu.</span><span class="sxs-lookup"><span data-stu-id="13ed0-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Dodawanie zasad][add-policy]

<span data-ttu-id="13ed0-151">Umieść kursor w hello `inbound` zasad i kliknij pozycję hello **tooEventHub dziennika** hello tooinsert zasad `log-to-eventhub` szablon zasad w instrukcji.</span><span class="sxs-lookup"><span data-stu-id="13ed0-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Edytor zasad][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="13ed0-153">Zastąp `logger-id` o nazwie hello hello zarządzanie interfejsami API rejestratora skonfigurowana w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="13ed0-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="13ed0-154">Można użyć dowolne wyrażenie zwracające ciąg jako wartość hello hello `log-to-eventhub` elementu.</span><span class="sxs-lookup"><span data-stu-id="13ed0-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="13ed0-155">W tym przykładzie jest rejestrowane ciąg zawierający hello daty i godziny, nazwę usługi, identyfikator żądania, żądania adresu ip oraz nazwy operacji.</span><span class="sxs-lookup"><span data-stu-id="13ed0-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="13ed0-156">Kliknij przycisk **zapisać** toosave hello zaktualizowano konfigurację zasad.</span><span class="sxs-lookup"><span data-stu-id="13ed0-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="13ed0-157">Natychmiast po ich zapisaniu zasady hello są aktywne, a zdarzenia są rejestrowane toohello wyznaczony Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13ed0-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13ed0-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13ed0-158">Next steps</span></span>
* <span data-ttu-id="13ed0-159">Dowiedz się więcej na temat usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13ed0-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="13ed0-160">Wprowadzenie do usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13ed0-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="13ed0-161">Odbieranie komunikatów za pomocą klasy EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="13ed0-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="13ed0-162">Przewodnik programowania w usłudze Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13ed0-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="13ed0-163">Dowiedz się więcej na temat integracji usługi API Management i usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="13ed0-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="13ed0-164">Odwołanie do jednostki rejestratora</span><span class="sxs-lookup"><span data-stu-id="13ed0-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="13ed0-165">informacje o zasadach dziennika do Centrum eventhub</span><span class="sxs-lookup"><span data-stu-id="13ed0-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="13ed0-166">Monitoruj swoje interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope</span><span class="sxs-lookup"><span data-stu-id="13ed0-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="13ed0-167">Obejrzyj przewodnik wideo</span><span class="sxs-lookup"><span data-stu-id="13ed0-167">Watch a video walkthrough</span></span>
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
