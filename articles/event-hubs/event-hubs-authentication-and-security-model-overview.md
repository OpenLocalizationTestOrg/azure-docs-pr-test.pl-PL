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
# <a name="event-hubs-authentication-and-security-model-overview"></a>Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs
model zabezpieczeń usługi Azure Event Hubs Hello spełnia hello następujące wymagania:

* Tylko klientów, które są dostępne prawidłowe poświadczenia można wysłać danych tooan zdarzenia koncentratora.
* Klient nie może spersonifikować innego klienta.
* Wysyłanie Centrum zdarzeń tooan dane mogą zostać zablokowane nieautoryzowanego klienta.

## <a name="client-authentication"></a>Uwierzytelnianie klienta
model zabezpieczeń usługi Event Hubs Hello jest oparty na kombinacji [dostępu sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) tokeny i *wydawców zdarzeń*. Wydawca zdarzeń definiuje wirtualnego punktu końcowego dla Centrum zdarzeń. Wydawca Hello można tylko Centrum zdarzeń tooan toosend używanych w wiadomości. Nie jest możliwe tooreceive komunikaty z wydawcą.

Zazwyczaj Centrum zdarzeń zostają jednego wydawcy na klienta. Wszystkich wiadomości wysłanych tooany hello wydawców Centrum zdarzeń są dodawane do kolejki w tym Centrum zdarzeń. Wydawcy Włącz szczegółowej kontroli dostępu i ograniczania przepustowości.

Każdy klient usługi Event Hubs jest przypisany unikatowy tokenem, który jest przekazany toohello klienta. tokeny Hello są tworzone w taki sposób, że każdy unikatowy token udziela dostępu tooa inny unikatowy wydawcy. Klient, który posiada tokenu można wysłać tylko tooone wydawcy, ale nie inne wydawcy. Jeśli wielu klientów udziału hello tego samego tokenu, a następnie każdego z nich udostępnia wydawcy.

Chociaż nie jest to zalecane, jest możliwe tooequip urządzeń z tokenami określającymi udzielenie Centrum zdarzeń tooan bezpośredni dostęp. Dowolne urządzenie, która przechowuje ten token może wysyłać komunikaty bezpośrednio do tego Centrum zdarzeń. Takie urządzenia nie będzie toothrottling podmiotu. Ponadto urządzenia hello nie może być na liście zabronionych numerów wysyłania toothat Centrum zdarzeń.

Wszystkie tokeny są podpisane za pomocą klucza sygnatury dostępu Współdzielonego. Zwykle wszystkie tokeny są podpisane za pomocą hello tego samego klucza. Klienci nie są znane klucza hello; Zapobiega to produkcyjny tokenów innych klientów.

### <a name="create-hello-sas-key"></a>Utwórz klucz sygnatury dostępu Współdzielonego hello

Podczas tworzenia przestrzeni nazw usługi Event Hubs, usługa hello generuje klucz sygnatury dostępu Współdzielonego 256-bitowe o nazwie **RootManageSharedAccessKey**. Tego klucza przyznaje wysyłania, nasłuchiwania i Zarządzanie prawami toohello w przestrzeni nazw. Można również utworzyć dodatkowych kluczy. Zalecane jest, aby utworzyć klucz, że przyznaje wysyłać uprawnienia toohello określonego zdarzenia koncentratora. Witaj pozostałej części tego tematu, zakłada się, o nazwie ten klucz **EventHubSendKey**.

Witaj poniższy przykład tworzy klucz tylko do wysyłania, podczas tworzenia Centrum zdarzeń hello:

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

### <a name="generate-tokens"></a>Generowanie tokenów

Można generować tokeny przy użyciu klucza sygnatury dostępu Współdzielonego hello. Musi mieć tylko jeden token na klienta. Następnie można wyprodukować tokeny przy użyciu hello następujące metody. Wszystkie tokeny są generowane przy użyciu hello **EventHubSendKey** klucza. Każdy token jest przypisany unikatowy identyfikator URI.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Podczas wywoływania tej metody, hello URI powinny być określone jako `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Wszystkie tokeny hello identyfikatora URI jest identyczny z wyjątkiem hello `PUBLISHER_NAME`, powinny być różne dla każdego tokenu. W idealnym przypadku `PUBLISHER_NAME` reprezentuje hello identyfikator powitania klienta, który odbiera token.

Ta metoda generuje token z następującej struktury hello:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

czas wygaśnięcia tokenu Hello jest określona w sekundach od 1 stycznia 1970. Witaj, poniżej przedstawiono przykładowy tokenu:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Zwykle tokeny hello mają cykl życia podobny lub przekracza hello żywotność powitania klienta. Jeśli klient hello ma tooobtain możliwości hello nowy token, można tokeny z krótszy czas działania.

### <a name="sending-data"></a>Wysyłanie danych
Po utworzeniu hello tokenów każdego klienta jest udostępniane z własną unikatową tokenu.

Gdy klient hello wysyła dane do Centrum zdarzeń, znaczniki jego żądanie wysłania z tokenem hello. tooprevent osoba atakująca podsłuchiwaniu i kradzież hello token, hello komunikacji między powitania klienta i Centrum zdarzeń hello musi odbywa się za pośrednictwem kanału szyfrowanego.

### <a name="blacklisting-clients"></a>List dozwolonych klientów
Token zostanie ukradzione przez osobę atakującą, osoba atakująca hello mogą personifikować klienta hello ukradł których token. List dozwolonych klienta renderuje ten klient nie można użyć do czasu otrzymania nowy token, który używa innego wydawcę.

## <a name="authentication-of-back-end-applications"></a>Uwierzytelnianie przy użyciu zaplecza aplikacji

tooauthenticate zaplecza aplikacji, które wykorzystują hello dane generowane przez klientów usługi Event Hubs, usługa Event Hubs wykorzystuje model zabezpieczeń podobne model toohello, który służy do tematów usługi Service Bus. Centra zdarzeń w grupy odbiorców jest tematu usługi Service Bus tooa subskrypcji tooa równoważne. Klienta można utworzyć grupy odbiorców, jeżeli grupy odbiorców hello hello żądania toocreate towarzyszy token czy przyznaje Zarządzanie uprawnieniami do Centrum zdarzeń hello, lub dla toowhich przestrzeni nazw hello hello Centrum zdarzeń należy. Klient jest dozwolone, tooconsume danych z grupy odbiorców Jeśli żądania odbierania hello towarzyszy token że przyznaje otrzymywać prawa w danej grupie odbiorców, hello Centrum zdarzeń lub Centrum zdarzeń hello hello przestrzeni nazw toowhich należy.

Bieżąca wersja usługi Service Bus Hello nie obsługuje zasady sygnatury dostępu Współdzielonego dla poszczególnych subskrypcji. powitalne samo grupy konsumentów centrów zdarzeń. Obsługa sygnatury dostępu Współdzielonego zostanie dodana dla obu funkcji w przyszłości hello.

W hello braku uwierzytelniania sygnatury dostępu Współdzielonego dla poszczególnych odbiorców grup można użyć toosecure klucze SAS wszystkich grup odbiorców przy użyciu klucza wspólnego. Takie podejście umożliwia danych tooconsume aplikacji z dowolnej grupy konsumentów hello Centrum zdarzeń.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Event Hubs, odwiedź hello następujące tematy:

* [Omówienie usługi Event Hubs]
* [Omówienie sygnatur dostępu współdzielonego]
* [Przykładowe aplikacje korzystające z usługi Event Hubs]

[Omówienie usługi Event Hubs]: event-hubs-what-is-event-hubs.md
[Przykładowe aplikacje korzystające z usługi Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Omówienie sygnatur dostępu współdzielonego]: ../service-bus-messaging/service-bus-sas.md

