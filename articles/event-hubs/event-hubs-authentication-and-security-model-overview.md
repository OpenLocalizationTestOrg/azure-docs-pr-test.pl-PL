---
title: "Omówienie modelu uwierzytelniania i zabezpieczeń usługi Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="38c93-103">Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="38c93-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="38c93-104">Model zabezpieczeń usługi Azure Event Hubs spełnia następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="38c93-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="38c93-105">Tylko klientów, które są dostępne prawidłowe poświadczenia może wysyłać dane do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="38c93-106">Klient nie może spersonifikować innego klienta.</span><span class="sxs-lookup"><span data-stu-id="38c93-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="38c93-107">Nieautoryzowanego klienta, który może zostać zablokowany wysyłania danych do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="38c93-108">Uwierzytelnianie klienta</span><span class="sxs-lookup"><span data-stu-id="38c93-108">Client authentication</span></span>
<span data-ttu-id="38c93-109">Model zabezpieczeń usługi Event Hubs jest oparty na kombinacji [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) tokeny i *wydawców zdarzeń*.</span><span class="sxs-lookup"><span data-stu-id="38c93-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="38c93-110">Wydawca zdarzeń definiuje wirtualnego punktu końcowego dla Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="38c93-111">Wydawcą może służyć tylko do wysyłania komunikatów do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="38c93-112">Nie jest możliwe odbieranie komunikatów z wydawcą.</span><span class="sxs-lookup"><span data-stu-id="38c93-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="38c93-113">Zazwyczaj Centrum zdarzeń zostają jednego wydawcy na klienta.</span><span class="sxs-lookup"><span data-stu-id="38c93-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="38c93-114">Wszystkie komunikaty, które są wysyłane do żadnych wydawców Centrum zdarzeń są dodawane do kolejki w tym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="38c93-115">Wydawcy Włącz szczegółowej kontroli dostępu i ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="38c93-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="38c93-116">Każdy klient usługi Event Hubs jest przypisany unikatowy tokenem, który zostanie przekazany do klienta.</span><span class="sxs-lookup"><span data-stu-id="38c93-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="38c93-117">Tokeny są tworzone w taki sposób, że każdy unikatowy token nieograniczony dostęp do różnych unikatowy wydawcy.</span><span class="sxs-lookup"><span data-stu-id="38c93-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="38c93-118">Klient, który posiada tokenu można wysłać tylko jednego wydawcy, ale nie inne wydawcy.</span><span class="sxs-lookup"><span data-stu-id="38c93-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="38c93-119">Jeśli wielu klientów współużytkować ten sam token, każde z nich udostępnia wydawcy.</span><span class="sxs-lookup"><span data-stu-id="38c93-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="38c93-120">Chociaż nie jest to zalecane, istnieje możliwość wyposażyć urządzeń z tokenami określającymi udzielenie bezpośredni dostęp do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="38c93-121">Dowolne urządzenie, która przechowuje ten token może wysyłać komunikaty bezpośrednio do tego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="38c93-122">Takie urządzenia nie będą podlegać ograniczania.</span><span class="sxs-lookup"><span data-stu-id="38c93-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="38c93-123">Ponadto urządzenie nie może być na liście zabronionych numerów wysyłaniu do tego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="38c93-124">Wszystkie tokeny są podpisane za pomocą klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="38c93-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="38c93-125">Zwykle wszystkie tokeny są podpisane za pomocą tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="38c93-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="38c93-126">Klienci nie są znane klucza; Zapobiega to produkcyjny tokenów innych klientów.</span><span class="sxs-lookup"><span data-stu-id="38c93-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="38c93-127">Utwórz klucz sygnatury dostępu Współdzielonego</span><span class="sxs-lookup"><span data-stu-id="38c93-127">Create the SAS key</span></span>

<span data-ttu-id="38c93-128">Podczas tworzenia przestrzeni nazw usługi Event Hubs, Usługa generuje klucz sygnatury dostępu Współdzielonego 256-bitowe o nazwie **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="38c93-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="38c93-129">Tego klucza przyznaje wysyłania, nasłuchiwania i Zarządzanie prawami do przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="38c93-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="38c93-130">Można również utworzyć dodatkowych kluczy.</span><span class="sxs-lookup"><span data-stu-id="38c93-130">You can also create additional keys.</span></span> <span data-ttu-id="38c93-131">Zaleca się, że tworzenia klucza, że przyznaje wysyłać uprawnienia do konkretnego zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="38c93-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="38c93-132">W pozostałej części tego tematu, zakłada się, o nazwie ten klucz **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="38c93-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="38c93-133">W poniższym przykładzie jest tworzony klucz tylko do wysyłania podczas tworzenia Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="38c93-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="38c93-134">Generowanie tokenów</span><span class="sxs-lookup"><span data-stu-id="38c93-134">Generate tokens</span></span>

<span data-ttu-id="38c93-135">Można generować tokeny przy użyciu klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="38c93-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="38c93-136">Musi mieć tylko jeden token na klienta.</span><span class="sxs-lookup"><span data-stu-id="38c93-136">You must produce only one token per client.</span></span> <span data-ttu-id="38c93-137">Następnie można wyprodukować tokeny przy użyciu następującej metody.</span><span class="sxs-lookup"><span data-stu-id="38c93-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="38c93-138">Wszystkie tokeny są generowane przy użyciu **EventHubSendKey** klucza.</span><span class="sxs-lookup"><span data-stu-id="38c93-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="38c93-139">Każdy token jest przypisany unikatowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="38c93-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="38c93-140">Podczas wywoływania tej metody, należy określić identyfikator URI jako `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="38c93-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="38c93-141">Wszystkie tokeny identyfikator URI jest taki sam, z wyjątkiem produktów `PUBLISHER_NAME`, powinny być różne dla każdego tokenu.</span><span class="sxs-lookup"><span data-stu-id="38c93-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="38c93-142">W idealnym przypadku `PUBLISHER_NAME` reprezentuje identyfikator klienta, który odbiera token.</span><span class="sxs-lookup"><span data-stu-id="38c93-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="38c93-143">Ta metoda generuje token o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="38c93-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="38c93-144">Czas wygaśnięcia tokenu jest określona w sekundach od 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="38c93-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="38c93-145">Poniżej przedstawiono przykład tokenu:</span><span class="sxs-lookup"><span data-stu-id="38c93-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="38c93-146">Zwykle tokeny mają cykl życia, który podobny lub przekroczenie czasu działania klienta.</span><span class="sxs-lookup"><span data-stu-id="38c93-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="38c93-147">Jeśli klient ma możliwość uzyskać nowy token, można tokeny z krótszy czas działania.</span><span class="sxs-lookup"><span data-stu-id="38c93-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="38c93-148">Wysyłanie danych</span><span class="sxs-lookup"><span data-stu-id="38c93-148">Sending data</span></span>
<span data-ttu-id="38c93-149">Po utworzeniu tokenów każdego klienta jest udostępniane z własną unikatową tokenu.</span><span class="sxs-lookup"><span data-stu-id="38c93-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="38c93-150">Gdy klient wysyła dane do Centrum zdarzeń, znaczniki jego żądanie wysłania z tokenem.</span><span class="sxs-lookup"><span data-stu-id="38c93-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="38c93-151">Osobie atakującej z podsłuchiwaniu i kradzież token, komunikacja między klientem a Centrum zdarzeń musi nastąpić za pośrednictwem kanału szyfrowanego.</span><span class="sxs-lookup"><span data-stu-id="38c93-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="38c93-152">List dozwolonych klientów</span><span class="sxs-lookup"><span data-stu-id="38c93-152">Blacklisting clients</span></span>
<span data-ttu-id="38c93-153">Token zostanie ukradzione przez osobę atakującą, osoba atakująca może personifikować klienta, których token został kradzieży.</span><span class="sxs-lookup"><span data-stu-id="38c93-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="38c93-154">List dozwolonych klienta renderuje ten klient nie można użyć do czasu otrzymania nowy token, który używa innego wydawcę.</span><span class="sxs-lookup"><span data-stu-id="38c93-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="38c93-155">Uwierzytelnianie przy użyciu zaplecza aplikacji</span><span class="sxs-lookup"><span data-stu-id="38c93-155">Authentication of back-end applications</span></span>

<span data-ttu-id="38c93-156">Na potrzeby uwierzytelniania aplikacji zaplecza, które wykorzystują dane generowane przez klientów usługi Event Hubs, usługa Event Hubs wykorzystuje model zabezpieczeń, która jest podobna do modelu, który służy do tematów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="38c93-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="38c93-157">Centra zdarzeń w grupy odbiorców jest odpowiednikiem subskrypcję tematu usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="38c93-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="38c93-158">Klienta można utworzyć grupy odbiorców, jeśli żądanie utworzenia grupy odbiorców jest powiązany token że przyznaje zarządzać uprawnieniami do Centrum zdarzeń lub przestrzeni nazw, do którego należy Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="38c93-159">Klient może wykorzystywać dane z grupy odbiorców, jeśli żądania odbierania towarzyszy token, który przyznaje prawa receive w danej grupie odbiorców, Centrum zdarzeń lub przestrzeni nazw, do którego należy Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="38c93-160">Bieżąca wersja usługi Service Bus nie obsługuje zasady sygnatury dostępu Współdzielonego dla pojedynczych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="38c93-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="38c93-161">To samo dotyczy grupy konsumentów usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="38c93-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="38c93-162">Obsługa sygnatury dostępu Współdzielonego zostanie dodana dla obu funkcji w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="38c93-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="38c93-163">W przypadku braku uwierzytelniania sygnatury dostępu Współdzielonego dla grupy konsumentów poszczególnych kluczy SAS służy do bezpiecznego wszystkie grupy konsumentów ze wspólnego klucza.</span><span class="sxs-lookup"><span data-stu-id="38c93-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="38c93-164">Takie podejście umożliwia aplikacji do pracy z danymi z dowolnej grupy konsumentów Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38c93-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38c93-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38c93-165">Next steps</span></span>
<span data-ttu-id="38c93-166">Aby dowiedzieć się więcej na temat usługi Event Hubs, można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="38c93-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="38c93-167">[Omówienie usługi Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="38c93-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="38c93-168">[Omówienie sygnatur dostępu współdzielonego]</span><span class="sxs-lookup"><span data-stu-id="38c93-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="38c93-169">[Przykładowe aplikacje korzystające z usługi Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="38c93-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="38c93-170">[Omówienie usługi Event Hubs]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="38c93-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="38c93-171">[Przykładowe aplikacje korzystające z usługi Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="38c93-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="38c93-172">[Omówienie sygnatur dostępu współdzielonego]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="38c93-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

