---
title: "zdarzenia aaaCustom siatki zdarzeń Azure | Dokumentacja firmy Microsoft"
description: "Użyj siatki zdarzeń Azure toopublish tematu i subskrypcji zdarzeń toothat."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Tworzenie i kierowanie zdarzeń niestandardowych za pomocą usługi Azure Event Grid

Siatki zdarzeń platformy Azure to usługa obsługi zdarzeń hello chmury. W tym artykule Użyj hello Azure CLI toocreate niestandardowego tematu, subskrypcja tematu toohello i wyzwolić hello zdarzeń tooview hello wynik. Zwykle możesz wysłać punktu końcowego tooan zdarzenia, który odpowiada toohello zdarzenia, takie jak webhook lub funkcji platformy Azure. Jednak toosimplify tego artykułu, możesz wysłać hello zdarzenia tooa URL, który tylko zbiera wiadomości powitania. Utworzysz ten adres URL przy użyciu narzędzia open source innego producenta o nazwie [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** to narzędzie typu „open source”, które nie jest przeznaczone do użycia przy wysokiej przepływności. Użycie Hello tutaj narzędzia hello jest całkowicie demonstrative. Jeśli w czasie powiadomień wypychanych więcej niż jedno zdarzenie, możesz nie zobaczyć wszystkich zdarzeń w narzędziu hello.

Gdy skończysz, zostanie wyświetlony, że hello danych zdarzeń został wysłany tooan punktu końcowego.

![Dane zdarzenia](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym artykule wymaga czy korzystasz z najnowszej wersji hello Azure CLI (2.0.14 lub nowsza). Wersja hello toofind, uruchom `az --version`. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Tematy usługi Event Grid to zasoby platformy Azure i muszą być umieszczone w grupie zasobów platformy Azure. Grupa zasobów Hello jest logiczną kolekcji, w której maszyny wirtualne Azure zasoby są wdrażane i zarządzane.

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *gridResourceGroup* w hello *westus2* lokalizacji.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Tworzenie tematu niestandardowego

Temat udostępnia zdefiniowany przez użytkownika punkt końcowy, do którego wysyłane są zdarzenia. Witaj poniższy przykład tworzy temat hello w grupie zasobów. Zamień `<topic_name>` na unikatową nazwę tematu. Nazwa tematu Hello musi być unikatowa, ponieważ jest reprezentowany przez wpis DNS. Dla wersji zapoznawczej hello obsługuje zdarzenia siatki **westus2** i **westcentralus** lokalizacji.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Tworzenie punktu końcowego komunikatów

Przed subskrypcję tematu toohello, Utwórzmy punktu końcowego hello hello komunikatu o zdarzeniu. Zamiast napisać kod toorespond toohello zdarzeń, Utwórzmy punktu końcowego, który zbiera wiadomości powitania, dlatego można je wyświetlić. RequestBin jest typu open source, narzędzia innej firmy, umożliwiający toocreate punktu końcowego i Wyświetl żądania, które są wysyłane tooit. Przejdź za[RequestBin](https://requestb.in/)i kliknij przycisk **utworzyć RequestBin**.  Skopiuj adres URL bin hello, ponieważ potrzebne podczas subskrypcję tematu toohello.

## <a name="subscribe-tooa-topic"></a>Subskrypcja tematu tooa

Subskrypcja tooa tematu tootell siatki zdarzeń zdarzenia, które chcesz tootrack. Witaj poniższy przykład subskrybuje tematu toohello utworzone i przekazuje hello adres URL z RequestBin jako punktu końcowego hello powiadomienia o zdarzeniach. Zastąp `<event_subscription_name>` o unikatowej nazwie dla Twojej subskrypcji i `<URL_from_RequestBin>` wartością hello z hello powyższej sekcji. Określając punkt końcowy podczas subskrypcji, siatki zdarzeń obsługuje routing hello punktu końcowego toothat zdarzenia. Aby uzyskać `<topic_name>`, użyj wartości hello utworzony wcześniej. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Wyślij temat tooyour zdarzenia

Teraz załóżmy wyzwolenia zdarzenia toosee jak siatki zdarzeń rozpowszechnia punkt końcowy tooyour wiadomość hello. Po pierwsze umożliwia pobieranie hello adresu URL i klucza hello tematu. Ponownie jako `<topic_name>` użyj nazwy tematu.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify w tym artykule, firma Microsoft zdefiniowane przykładowe zdarzenie danych toosend toohello tematu. Zwykle aplikacja lub usługa Azure są wysyłane dane zdarzeń hello. Poniższy przykład Hello pobiera dane zdarzeń hello:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Jeśli użytkownik `echo "$body"` widać hello pełnego zdarzenia. Witaj `data` element hello JSON jest ładunku hello wydarzenia. W tym polu można umieścić dowolną poprawnie sformułowaną zawartość JSON. Umożliwia także pole tematu hello zaawansowane routingu i filtrowania.

CURL to narzędzie, które wykonuje żądania HTTP. W tym artykule używamy temat tooour CURL toosend hello zdarzenia. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Zostały wyzwolone hello zdarzeń i siatki zdarzenia wysyłane końcowych toohello wiadomość hello skonfigurowaną podczas subskrybowania. Przeglądaj toohello RequestBin adres URL, który został utworzony wcześniej. Ewentualnie kliknij przycisk Refresh (Odśwież) w otwartej przeglądarce narzędzia RequestBin. Zostanie wyświetlony hello zdarzenia, które zostały wysłane. 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Jeśli planujesz toocontinue pracy z tym zdarzeniem, wykonaj nie wyczyścić zasoby hello utworzone w tym artykule. Jeśli nie planujesz toocontinue, użyj hello następujące polecenia toodelete hello zasobów utworzonej w tym artykule.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Następne kroki

Teraz, gdy wiesz, jak toocreate tematów i subskrypcji zdarzeń, Dowiedz się więcej o jakie siatki zdarzeń można to robić:

- [Event Grid — informacje](overview.md)
- [Monitorowanie zmian maszyn wirtualnych za pomocą usług Azure Event Grid i Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)
