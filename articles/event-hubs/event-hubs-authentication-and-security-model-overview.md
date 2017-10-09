---
title: "aaaOverview modelu uwierzytelniania i zabezpieczeń usługi Azure Event Hubs | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="19433-103">Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19433-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="19433-104">model zabezpieczeń usługi Azure Event Hubs Hello spełnia hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="19433-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="19433-105">Tylko klientów, które są dostępne prawidłowe poświadczenia można wysłać danych tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="19433-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="19433-106">Klient nie może spersonifikować innego klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="19433-107">Wysyłanie Centrum zdarzeń tooan dane mogą zostać zablokowane nieautoryzowanego klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="19433-108">Uwierzytelnianie klienta</span><span class="sxs-lookup"><span data-stu-id="19433-108">Client authentication</span></span>
<span data-ttu-id="19433-109">model zabezpieczeń usługi Event Hubs Hello jest oparty na kombinacji [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) tokeny i *wydawców zdarzeń*.</span><span class="sxs-lookup"><span data-stu-id="19433-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="19433-110">Wydawca zdarzeń definiuje wirtualnego punktu końcowego dla Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="19433-111">Wydawca Hello można tylko Centrum zdarzeń tooan toosend używanych w wiadomości.</span><span class="sxs-lookup"><span data-stu-id="19433-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="19433-112">Nie jest możliwe tooreceive komunikaty z wydawcą.</span><span class="sxs-lookup"><span data-stu-id="19433-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="19433-113">Zazwyczaj Centrum zdarzeń zostają jednego wydawcy na klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="19433-114">Wszystkich wiadomości wysłanych tooany hello wydawców Centrum zdarzeń są dodawane do kolejki w tym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="19433-115">Wydawcy Włącz szczegółowej kontroli dostępu i ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="19433-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="19433-116">Każdy klient usługi Event Hubs jest przypisany unikatowy tokenem, który jest przekazany toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="19433-117">tokeny Hello są tworzone w taki sposób, że każdy unikatowy token udziela dostępu tooa inny unikatowy wydawcy.</span><span class="sxs-lookup"><span data-stu-id="19433-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="19433-118">Klient, który posiada tokenu można wysłać tylko tooone wydawcy, ale nie inne wydawcy.</span><span class="sxs-lookup"><span data-stu-id="19433-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="19433-119">Jeśli wielu klientów udziału hello tego samego tokenu, a następnie każdego z nich udostępnia wydawcy.</span><span class="sxs-lookup"><span data-stu-id="19433-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="19433-120">Chociaż nie jest to zalecane, jest możliwe tooequip urządzeń z tokenami określającymi udzielenie Centrum zdarzeń tooan bezpośredni dostęp.</span><span class="sxs-lookup"><span data-stu-id="19433-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="19433-121">Dowolne urządzenie, która przechowuje ten token może wysyłać komunikaty bezpośrednio do tego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="19433-122">Takie urządzenia nie będzie toothrottling podmiotu.</span><span class="sxs-lookup"><span data-stu-id="19433-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="19433-123">Ponadto urządzenia hello nie może być na liście zabronionych numerów wysyłania toothat Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="19433-124">Wszystkie tokeny są podpisane za pomocą klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="19433-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="19433-125">Zwykle wszystkie tokeny są podpisane za pomocą hello tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="19433-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="19433-126">Klienci nie są znane klucza hello; Zapobiega to produkcyjny tokenów innych klientów.</span><span class="sxs-lookup"><span data-stu-id="19433-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="19433-127">Utwórz klucz sygnatury dostępu Współdzielonego hello</span><span class="sxs-lookup"><span data-stu-id="19433-127">Create hello SAS key</span></span>

<span data-ttu-id="19433-128">Podczas tworzenia przestrzeni nazw usługi Event Hubs, usługa hello generuje klucz sygnatury dostępu Współdzielonego 256-bitowe o nazwie **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="19433-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="19433-129">Tego klucza przyznaje wysyłania, nasłuchiwania i Zarządzanie prawami toohello w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="19433-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="19433-130">Można również utworzyć dodatkowych kluczy.</span><span class="sxs-lookup"><span data-stu-id="19433-130">You can also create additional keys.</span></span> <span data-ttu-id="19433-131">Zalecane jest, aby utworzyć klucz, że przyznaje wysyłać uprawnienia toohello określonego zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="19433-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="19433-132">Witaj pozostałej części tego tematu, zakłada się, o nazwie ten klucz **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="19433-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="19433-133">Witaj poniższy przykład tworzy klucz tylko do wysyłania, podczas tworzenia Centrum zdarzeń hello:</span><span class="sxs-lookup"><span data-stu-id="19433-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="19433-134">Generowanie tokenów</span><span class="sxs-lookup"><span data-stu-id="19433-134">Generate tokens</span></span>

<span data-ttu-id="19433-135">Można generować tokeny przy użyciu klucza sygnatury dostępu Współdzielonego hello.</span><span class="sxs-lookup"><span data-stu-id="19433-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="19433-136">Musi mieć tylko jeden token na klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-136">You must produce only one token per client.</span></span> <span data-ttu-id="19433-137">Następnie można wyprodukować tokeny przy użyciu hello następujące metody.</span><span class="sxs-lookup"><span data-stu-id="19433-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="19433-138">Wszystkie tokeny są generowane przy użyciu hello **EventHubSendKey** klucza.</span><span class="sxs-lookup"><span data-stu-id="19433-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="19433-139">Każdy token jest przypisany unikatowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="19433-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="19433-140">Podczas wywoływania tej metody, hello URI powinny być określone jako `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="19433-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="19433-141">Wszystkie tokeny hello identyfikatora URI jest identyczny z wyjątkiem hello `PUBLISHER_NAME`, powinny być różne dla każdego tokenu.</span><span class="sxs-lookup"><span data-stu-id="19433-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="19433-142">W idealnym przypadku `PUBLISHER_NAME` reprezentuje hello identyfikator powitania klienta, który odbiera token.</span><span class="sxs-lookup"><span data-stu-id="19433-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="19433-143">Ta metoda generuje token z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="19433-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="19433-144">czas wygaśnięcia tokenu Hello jest określona w sekundach od 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="19433-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="19433-145">Witaj, poniżej przedstawiono przykładowy tokenu:</span><span class="sxs-lookup"><span data-stu-id="19433-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="19433-146">Zwykle tokeny hello mają cykl życia podobny lub przekracza hello żywotność powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="19433-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="19433-147">Jeśli klient hello ma tooobtain możliwości hello nowy token, można tokeny z krótszy czas działania.</span><span class="sxs-lookup"><span data-stu-id="19433-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="19433-148">Wysyłanie danych</span><span class="sxs-lookup"><span data-stu-id="19433-148">Sending data</span></span>
<span data-ttu-id="19433-149">Po utworzeniu hello tokenów każdego klienta jest udostępniane z własną unikatową tokenu.</span><span class="sxs-lookup"><span data-stu-id="19433-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="19433-150">Gdy klient hello wysyła dane do Centrum zdarzeń, znaczniki jego żądanie wysłania z tokenem hello.</span><span class="sxs-lookup"><span data-stu-id="19433-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="19433-151">tooprevent osoba atakująca podsłuchiwaniu i kradzież hello token, hello komunikacji między powitania klienta i Centrum zdarzeń hello musi odbywa się za pośrednictwem kanału szyfrowanego.</span><span class="sxs-lookup"><span data-stu-id="19433-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="19433-152">List dozwolonych klientów</span><span class="sxs-lookup"><span data-stu-id="19433-152">Blacklisting clients</span></span>
<span data-ttu-id="19433-153">Token zostanie ukradzione przez osobę atakującą, osoba atakująca hello mogą personifikować klienta hello ukradł których token.</span><span class="sxs-lookup"><span data-stu-id="19433-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="19433-154">List dozwolonych klienta renderuje ten klient nie można użyć do czasu otrzymania nowy token, który używa innego wydawcę.</span><span class="sxs-lookup"><span data-stu-id="19433-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="19433-155">Uwierzytelnianie przy użyciu zaplecza aplikacji</span><span class="sxs-lookup"><span data-stu-id="19433-155">Authentication of back-end applications</span></span>

<span data-ttu-id="19433-156">tooauthenticate zaplecza aplikacji, które wykorzystują hello dane generowane przez klientów usługi Event Hubs, usługa Event Hubs wykorzystuje model zabezpieczeń podobne model toohello, który służy do tematów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="19433-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="19433-157">Centra zdarzeń w grupy odbiorców jest tematu usługi Service Bus tooa subskrypcji tooa równoważne.</span><span class="sxs-lookup"><span data-stu-id="19433-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="19433-158">Klienta można utworzyć grupy odbiorców, jeżeli grupy odbiorców hello hello żądania toocreate towarzyszy token czy przyznaje Zarządzanie uprawnieniami do Centrum zdarzeń hello, lub dla toowhich przestrzeni nazw hello hello Centrum zdarzeń należy.</span><span class="sxs-lookup"><span data-stu-id="19433-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="19433-159">Klient jest dozwolone, tooconsume danych z grupy odbiorców Jeśli żądania odbierania hello towarzyszy token że przyznaje otrzymywać prawa w danej grupie odbiorców, hello Centrum zdarzeń lub Centrum zdarzeń hello hello przestrzeni nazw toowhich należy.</span><span class="sxs-lookup"><span data-stu-id="19433-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="19433-160">Bieżąca wersja usługi Service Bus Hello nie obsługuje zasady sygnatury dostępu Współdzielonego dla poszczególnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="19433-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="19433-161">powitalne samo grupy konsumentów centrów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="19433-162">Obsługa sygnatury dostępu Współdzielonego zostanie dodana dla obu funkcji w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="19433-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="19433-163">W hello braku uwierzytelniania sygnatury dostępu Współdzielonego dla poszczególnych odbiorców grup można użyć toosecure klucze SAS wszystkich grup odbiorców przy użyciu klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="19433-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="19433-164">Takie podejście umożliwia danych tooconsume aplikacji z dowolnej grupy konsumentów hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19433-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19433-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19433-165">Next steps</span></span>
<span data-ttu-id="19433-166">toolearn więcej informacji na temat usługi Event Hubs, odwiedź hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="19433-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="19433-167">[Omówienie usługi Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="19433-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="19433-168">[Omówienie sygnatur dostępu współdzielonego]</span><span class="sxs-lookup"><span data-stu-id="19433-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="19433-169">[Przykładowe aplikacje korzystające z usługi Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="19433-169">[Sample applications that use Event Hubs]</span></span>

[Omówienie usługi Event Hubs]: event-hubs-what-is-event-hubs.md
[Przykładowe aplikacje korzystające z usługi Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Omówienie sygnatur dostępu współdzielonego]: ../service-bus-messaging/service-bus-sas.md

