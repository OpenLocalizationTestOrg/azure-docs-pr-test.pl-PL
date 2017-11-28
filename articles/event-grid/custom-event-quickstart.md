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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="39c71-103">Tworzenie i kierowanie zdarzeń niestandardowych za pomocą usługi Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="39c71-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="39c71-104">Siatki zdarzeń platformy Azure to usługa obsługi zdarzeń hello chmury.</span><span class="sxs-lookup"><span data-stu-id="39c71-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="39c71-105">W tym artykule Użyj hello Azure CLI toocreate niestandardowego tematu, subskrypcja tematu toohello i wyzwolić hello zdarzeń tooview hello wynik.</span><span class="sxs-lookup"><span data-stu-id="39c71-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="39c71-106">Zwykle możesz wysłać punktu końcowego tooan zdarzenia, który odpowiada toohello zdarzenia, takie jak webhook lub funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39c71-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="39c71-107">Jednak toosimplify tego artykułu, możesz wysłać hello zdarzenia tooa URL, który tylko zbiera wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="39c71-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="39c71-108">Utworzysz ten adres URL przy użyciu narzędzia open source innego producenta o nazwie [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="39c71-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="39c71-109">**RequestBin** to narzędzie typu „open source”, które nie jest przeznaczone do użycia przy wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="39c71-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="39c71-110">Użycie Hello tutaj narzędzia hello jest całkowicie demonstrative.</span><span class="sxs-lookup"><span data-stu-id="39c71-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="39c71-111">Jeśli w czasie powiadomień wypychanych więcej niż jedno zdarzenie, możesz nie zobaczyć wszystkich zdarzeń w narzędziu hello.</span><span class="sxs-lookup"><span data-stu-id="39c71-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="39c71-112">Gdy skończysz, zostanie wyświetlony, że hello danych zdarzeń został wysłany tooan punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="39c71-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Dane zdarzenia](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="39c71-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym artykule wymaga czy korzystasz z najnowszej wersji hello Azure CLI (2.0.14 lub nowsza).</span><span class="sxs-lookup"><span data-stu-id="39c71-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="39c71-115">Wersja hello toofind, uruchom `az --version`.</span><span class="sxs-lookup"><span data-stu-id="39c71-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="39c71-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39c71-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="39c71-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="39c71-117">Create a resource group</span></span>

<span data-ttu-id="39c71-118">Tematy usługi Event Grid to zasoby platformy Azure i muszą być umieszczone w grupie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39c71-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="39c71-119">Grupa zasobów Hello jest logiczną kolekcji, w której maszyny wirtualne Azure zasoby są wdrażane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="39c71-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="39c71-120">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="39c71-121">Witaj poniższy przykład tworzy grupę zasobów o nazwie *gridResourceGroup* w hello *westus2* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="39c71-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="39c71-122">Tworzenie tematu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="39c71-122">Create a custom topic</span></span>

<span data-ttu-id="39c71-123">Temat udostępnia zdefiniowany przez użytkownika punkt końcowy, do którego wysyłane są zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="39c71-124">Witaj poniższy przykład tworzy temat hello w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="39c71-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="39c71-125">Zamień `<topic_name>` na unikatową nazwę tematu.</span><span class="sxs-lookup"><span data-stu-id="39c71-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="39c71-126">Nazwa tematu Hello musi być unikatowa, ponieważ jest reprezentowany przez wpis DNS.</span><span class="sxs-lookup"><span data-stu-id="39c71-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="39c71-127">Dla wersji zapoznawczej hello obsługuje zdarzenia siatki **westus2** i **westcentralus** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="39c71-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="39c71-128">Tworzenie punktu końcowego komunikatów</span><span class="sxs-lookup"><span data-stu-id="39c71-128">Create a message endpoint</span></span>

<span data-ttu-id="39c71-129">Przed subskrypcję tematu toohello, Utwórzmy punktu końcowego hello hello komunikatu o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="39c71-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="39c71-130">Zamiast napisać kod toorespond toohello zdarzeń, Utwórzmy punktu końcowego, który zbiera wiadomości powitania, dlatego można je wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="39c71-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="39c71-131">RequestBin jest typu open source, narzędzia innej firmy, umożliwiający toocreate punktu końcowego i Wyświetl żądania, które są wysyłane tooit.</span><span class="sxs-lookup"><span data-stu-id="39c71-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="39c71-132">Przejdź za[RequestBin](https://requestb.in/)i kliknij przycisk **utworzyć RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="39c71-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="39c71-133">Skopiuj adres URL bin hello, ponieważ potrzebne podczas subskrypcję tematu toohello.</span><span class="sxs-lookup"><span data-stu-id="39c71-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="39c71-134">Subskrypcja tematu tooa</span><span class="sxs-lookup"><span data-stu-id="39c71-134">Subscribe tooa topic</span></span>

<span data-ttu-id="39c71-135">Subskrypcja tooa tematu tootell siatki zdarzeń zdarzenia, które chcesz tootrack.</span><span class="sxs-lookup"><span data-stu-id="39c71-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="39c71-136">Witaj poniższy przykład subskrybuje tematu toohello utworzone i przekazuje hello adres URL z RequestBin jako punktu końcowego hello powiadomienia o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="39c71-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="39c71-137">Zastąp `<event_subscription_name>` o unikatowej nazwie dla Twojej subskrypcji i `<URL_from_RequestBin>` wartością hello z hello powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="39c71-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="39c71-138">Określając punkt końcowy podczas subskrypcji, siatki zdarzeń obsługuje routing hello punktu końcowego toothat zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="39c71-139">Aby uzyskać `<topic_name>`, użyj wartości hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="39c71-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="39c71-140">Wyślij temat tooyour zdarzenia</span><span class="sxs-lookup"><span data-stu-id="39c71-140">Send an event tooyour topic</span></span>

<span data-ttu-id="39c71-141">Teraz załóżmy wyzwolenia zdarzenia toosee jak siatki zdarzeń rozpowszechnia punkt końcowy tooyour wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="39c71-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="39c71-142">Po pierwsze umożliwia pobieranie hello adresu URL i klucza hello tematu.</span><span class="sxs-lookup"><span data-stu-id="39c71-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="39c71-143">Ponownie jako `<topic_name>` użyj nazwy tematu.</span><span class="sxs-lookup"><span data-stu-id="39c71-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="39c71-144">toosimplify w tym artykule, firma Microsoft zdefiniowane przykładowe zdarzenie danych toosend toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="39c71-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="39c71-145">Zwykle aplikacja lub usługa Azure są wysyłane dane zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="39c71-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="39c71-146">Poniższy przykład Hello pobiera dane zdarzeń hello:</span><span class="sxs-lookup"><span data-stu-id="39c71-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="39c71-147">Jeśli użytkownik `echo "$body"` widać hello pełnego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="39c71-148">Witaj `data` element hello JSON jest ładunku hello wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="39c71-149">W tym polu można umieścić dowolną poprawnie sformułowaną zawartość JSON.</span><span class="sxs-lookup"><span data-stu-id="39c71-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="39c71-150">Umożliwia także pole tematu hello zaawansowane routingu i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="39c71-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="39c71-151">CURL to narzędzie, które wykonuje żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="39c71-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="39c71-152">W tym artykule używamy temat tooour CURL toosend hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="39c71-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="39c71-153">Zostały wyzwolone hello zdarzeń i siatki zdarzenia wysyłane końcowych toohello wiadomość hello skonfigurowaną podczas subskrybowania.</span><span class="sxs-lookup"><span data-stu-id="39c71-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="39c71-154">Przeglądaj toohello RequestBin adres URL, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="39c71-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="39c71-155">Ewentualnie kliknij przycisk Refresh (Odśwież) w otwartej przeglądarce narzędzia RequestBin.</span><span class="sxs-lookup"><span data-stu-id="39c71-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="39c71-156">Zostanie wyświetlony hello zdarzenia, które zostały wysłane.</span><span class="sxs-lookup"><span data-stu-id="39c71-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="39c71-157">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="39c71-157">Clean up resources</span></span>
<span data-ttu-id="39c71-158">Jeśli planujesz toocontinue pracy z tym zdarzeniem, wykonaj nie wyczyścić zasoby hello utworzone w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="39c71-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="39c71-159">Jeśli nie planujesz toocontinue, użyj hello następujące polecenia toodelete hello zasobów utworzonej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="39c71-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="39c71-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39c71-160">Next steps</span></span>

<span data-ttu-id="39c71-161">Teraz, gdy wiesz, jak toocreate tematów i subskrypcji zdarzeń, Dowiedz się więcej o jakie siatki zdarzeń można to robić:</span><span class="sxs-lookup"><span data-stu-id="39c71-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="39c71-162">Event Grid — informacje</span><span class="sxs-lookup"><span data-stu-id="39c71-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="39c71-163">Monitorowanie zmian maszyn wirtualnych za pomocą usług Azure Event Grid i Logic Apps</span><span class="sxs-lookup"><span data-stu-id="39c71-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
