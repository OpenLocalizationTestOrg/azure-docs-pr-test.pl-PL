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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Jak toolog zdarzenia tooAzure centra zdarzeń w usłudze Azure API Management
Usługa Azure Event Hubs to wysoce skalowalna Usługa transferu danych, który może obsługiwać miliony zdarzeń na sekundę, dzięki czemu możliwe jest przetwarzanie i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Usługa Event Hubs działa jako "drzwi wejściowe" dla potoku zdarzeń hello, a po pobraniu danych do Centrum zdarzeń, można je przekształcać i przechowywane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania. Usługa Event Hubs oddziela hello Wytwarzanie strumienia zdarzeń od użycia hello tych zdarzeń, dzięki czemu odbiorcy zdarzeń mogą uzyskiwać dostęp do zdarzeń hello w swoim własnym harmonogramem.

W tym artykule jest toohello Pomocnika [zintegrować zarządzanie interfejsami API Azure z usługą Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) wideo i opisano sposób toolog zarządzanie interfejsami API zdarzenia przy użyciu usługi Azure Event Hubs.

## <a name="create-an-azure-event-hub"></a>Tworzenie Centrum zdarzeń platformy Azure
toocreate z nowym Centrum zdarzeń logowania toohello [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**usługi Service Bus ** -> **Centrum zdarzeń**->**szybkie tworzenie**. Wprowadź nazwę Centrum zdarzeń, region, wybierz subskrypcję, a następnie wybierz obszar nazw. Jeśli nie utworzono jeszcze przestrzeni nazw można go utworzyć, wpisując nazwę w hello **Namespace** pola tekstowego. Po skonfigurowaniu wszystkich właściwości, kliknij przycisk **Utwórz nowe Centrum zdarzeń** hello toocreate Centrum zdarzeń.

![Tworzenie Centrum zdarzeń][create-event-hub]

Następnie przejdź toohello **Konfiguruj** karcie nowe Centrum zdarzeń i utworzyć dwa **udostępnionych zasady dostępu**. Nazwa pierwszej hello **wysyłanie** i nadaj mu **wysyłania** uprawnienia.

![Wysyłanie zasad][sending-policy]

Nazwa hello drugi **odbieranie**, nadaj **nasłuchiwania** uprawnienia, a następnie kliknij przycisk **zapisać**.

![Odebranie zasad][receiving-policy]

Wszystkie zasady dostępu współdzielonego umożliwia toosend aplikacji i otrzymywać zdarzeń tooand hello Centrum zdarzeń. Parametry połączenia hello tooaccess dla tych zasad Przejdź toohello **pulpitu nawigacyjnego** hello Centrum zdarzeń i kliknij na karcie **informacje o połączeniu**.

![Parametry połączenia][event-hub-dashboard]

Witaj **wysyłanie** ciąg połączenia jest używany podczas rejestrowania zdarzeń i hello **odbieranie** ciąg połączenia jest używany podczas pobierania zdarzeń z hello Centrum zdarzeń.

![Parametry połączenia][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Utworzyć zarządzanie interfejsami API rejestratora
Teraz, gdy masz Centrum zdarzeń hello następnym krokiem jest tooconfigure [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) w zarządzania infrastrukturą interfejsu API usługi tak, aby móc zarejestrować zdarzenia toohello Centrum zdarzeń.

Zarządzanie interfejsami API rejestratorów są skonfigurowane przy użyciu hello [interfejsu API REST zarządzania interfejsu API](http://aka.ms/smapi). Przed użyciem hello interfejsu API REST dla powitania po raz pierwszy, przejrzyj hello [wymagania wstępne](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) i upewnij się, że masz [włączone toohello dostępu do interfejsu API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate rejestratora, upewnij się przy użyciu powitania po szablon adresu URL żądania HTTP PUT.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Zastąp `{your service}` o nazwie hello wystąpienia usługi Zarządzanie interfejsami API.
* Zastąp `{new logger name}` nazwą hello odpowiednią dla Twojego nowego rejestratora. Po skonfigurowaniu hello będzie odwoływać się ta nazwa [dziennika do Centrum eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) zasad

Dodaj następujące nagłówki żądania toohello hello.

* Content-Type: application/json
* Autoryzacji: SharedAccessSignature 58...
  * Aby uzyskać instrukcje dotyczące generowania hello `SharedAccessSignature` zobacz [Azure API Management REST API uwierzytelniania](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Określ hello treści żądania przy użyciu następującego szablonu hello.

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

* `type`musi być ustawiona zbyt`AzureEventHub`.
* `description`zapewnia opcjonalny opis rejestratora hello i w razie potrzeby może być ciągiem o zerowej długości.
* `credentials`zawiera hello `name` i `connectionString` Azure Centrum zdarzeń.

Po dokonaniu hello żądania, jeśli Rejestrator hello jest tworzony kod stanu `201 Created` jest zwracany.

> [!NOTE]
> Pozostałe możliwe kody powrotu i ich przyczyny, zobacz [utworzyć Rejestrator](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee jak wykonywać inne operacje, takie jak listy, update i delete, zobacz hello [rejestratora](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dokumentacji jednostki.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Konfigurowanie zasad dziennika do eventhubs
Po Twoje rejestratora jest skonfigurowany w usłudze API Management, można skonfigurować zasady dziennika do eventhubs toolog hello potrzeby zdarzeń. Witaj dziennika do eventhubs zasady mogą być używane w obu hello sekcji zasady ruchu przychodzącego lub hello wychodzącego zasad sekcji.

tooconfigure zasad logowania toohello [portalu Azure](https://portal.azure.com), przejdź do usługi API Management tooyour i kliknij **portal wydawcy** tooaccess hello portalu wydawcy.

![Portal wydawcy][publisher-portal]

Kliknij przycisk **zasady** w menu Zarządzanie interfejsami API hello powitania po lewej stronie, wybierz żądany produkt hello i interfejsu API, a następnie kliknij przycisk **Dodaj zasady**. W tym przykładzie Trwa dodawanie toohello zasad **Echo API** w hello **nieograniczone** produktu.

![Dodawanie zasad][add-policy]

Umieść kursor w hello `inbound` zasad i kliknij pozycję hello **tooEventHub dziennika** hello tooinsert zasad `log-to-eventhub` szablon zasad w instrukcji.

![Edytor zasad][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Zastąp `logger-id` o nazwie hello hello zarządzanie interfejsami API rejestratora skonfigurowana w poprzednim kroku hello.

Można użyć dowolne wyrażenie zwracające ciąg jako wartość hello hello `log-to-eventhub` elementu. W tym przykładzie jest rejestrowane ciąg zawierający hello daty i godziny, nazwę usługi, identyfikator żądania, żądania adresu ip oraz nazwy operacji.

Kliknij przycisk **zapisać** toosave hello zaktualizowano konfigurację zasad. Natychmiast po ich zapisaniu zasady hello są aktywne, a zdarzenia są rejestrowane toohello wyznaczony Centrum zdarzeń.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat usługi Azure Event Hubs
  * [Wprowadzenie do usługi Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Odbieranie komunikatów za pomocą klasy EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Przewodnik programowania w usłudze Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* Dowiedz się więcej na temat integracji usługi API Management i usługi Event Hubs
  * [Odwołanie do jednostki rejestratora](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [informacje o zasadach dziennika do Centrum eventhub](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Monitoruj swoje interfejsy API z usługi Azure API Management, usługa Event Hubs i Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Obejrzyj przewodnik wideo
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
