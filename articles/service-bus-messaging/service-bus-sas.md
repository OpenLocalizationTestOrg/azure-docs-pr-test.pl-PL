---
title: "Uwierzytelnianie usługi Service Bus aaaAzure za pomocą sygnatury dostępu współdzielonego | Dokumentacja firmy Microsoft"
description: "Omówienie uwierzytelniania magistrali usług przy użyciu sygnatury dostępu współdzielonego Przegląd, szczegółowe informacje dotyczące uwierzytelniania sygnatury dostępu Współdzielonego za pomocą usługi Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Uwierzytelnianie usługi Service Bus za pomocą sygnatury dostępu współdzielonego

*Sygnatury dostępu współdzielonego* (SAS) są hello zabezpieczeń podstawowego mechanizmu komunikatów usługi Service Bus. W tym artykule omówiono SAS, jak działają i jak toouse ich w sposób niezależny od platformy.

Uwierzytelniania sygnatury dostępu Współdzielonego umożliwia aplikacji tooauthenticate tooService magistrali przy użyciu klawisza dostępu skonfigurowane na powitania przestrzeni nazw lub na powitania wiadomości jednostki (kolejka lub temat) określone prawa, które są skojarzone. Następnie można użyć tego klucza toogenerate tokenu sygnatury dostępu Współdzielonego, którego klienci mogą z kolei używać tooService tooauthenticate magistrali.

Obsługa uwierzytelniania sygnatury dostępu Współdzielonego jest dostępna w hello Azure SDK w wersji 2.0 lub nowszej.

## <a name="overview-of-sas"></a>Omówienie SAS

Udostępniony sygnatur dostępu są mechanizmu uwierzytelniania na podstawie bezpiecznego wartości skrótu SHA-256 lub identyfikatorów URI. Jest bardzo zaawansowanym mechanizmem, który jest używany przez wszystkie usługi Service Bus. W rzeczywistości SAS ma dwa składniki: *udostępnionych zasad dostępu* i *udostępnionego sygnatury dostępu* (często nazywane *tokenu*).

Skojarzenia zabezpieczeń uwierzytelniania w usłudze Service Bus wymaga konfiguracji hello klucza kryptograficznego ze skojarzonymi prawami do zasobu usługi Service Bus. Klienci oświadczeń dostępu tooService magistrali zasoby z uwzględnieniem tokenu sygnatury dostępu Współdzielonego. Token ten składa się z zasobów hello identyfikatora URI, do której uzyskuje dostęp i wygaśnięcia podpisany hello skonfigurowany klucz.

Można konfigurować reguły autoryzacji sygnatura dostępu współdzielonego usługi Service Bus [przekazuje](service-bus-fundamentals-hybrid-solutions.md#relays), [kolejek](service-bus-fundamentals-hybrid-solutions.md#queues), i [tematy](service-bus-fundamentals-hybrid-solutions.md#topics).

Uwierzytelniania sygnatury dostępu Współdzielonego przy użyciu hello następujące elementy:

* [Reguły autoryzacji dostępu do udostępnionych](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256-bitowego szyfrowania klucza podstawowego w reprezentacji Base64, opcjonalny klucz pomocniczy i nazwę klucza i skojarzonymi prawami (kolekcja *nasłuchiwania*, *wysyłania*, lub *Zarządzaj* praw).
* [Udostępnione sygnatury dostępu](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) tokenu: wygenerowanych przy użyciu hello HMAC SHA256 ciągu zasobu, składające się z hello identyfikatora URI zasobu hello, który jest dostępny i wygaśnięcia za hello klucza kryptograficznego. Podpis Hello i inne elementy opisane w hello następujące sekcje są sformatowane na ciąg hello tooform tokenu sygnatury dostępu Współdzielonego.

## <a name="shared-access-policy"></a>Zasady dostępu współużytkowanego

Ważną kwestią toounderstand temat sygnatury dostępu Współdzielonego jest jego rozpoczyna się od zasad. Dla każdej zasady zdecydujesz się na trzy informacje: **nazwa**, **zakres**, i **uprawnienia**. Witaj **nazwa** jest po prostu; unikatową nazwę w ramach tego zakresu. Witaj zakres jest dość proste: jego hello identyfikator URI zasobu hello. W przypadku przestrzeni nazw usługi Service Bus zakres hello jest hello pełną nazwę domeny (FQDN), takich jak `https://<yournamespace>.servicebus.windows.net/`.

przede wszystkim wyjaśnień Hello uprawnienia dostępne dla zasad:

* Send
* Nasłuchiwanie
* Zarządzanie

Po utworzeniu zasad hello jest przypisany *klucza podstawowego* i *klucza pomocniczego*. Są to silną kryptograficznie kluczy. Nie utracone lub ich wyciek — zawsze będzie dostępna w hello [portalu Azure][Azure portal]. Możesz użyć dowolnej hello wygenerowane klucze i można je odtworzyć w dowolnym momencie. Jednak jeśli ponownie wygenerować lub zmienić hello klucza podstawowego w zasadach hello żadnych sygnatur dostępu współdzielonego z niej utworzyć zostaną unieważnione.

Po utworzeniu przestrzeni nazw usługi Service Bus automatycznie utworzone zasady dla całej przestrzeni nazw hello o nazwie **RootManageSharedAccessKey**, a ta zasada ma wszystkie uprawnienia. Nie Zaloguj się jako **głównego**, dlatego nie używaj tej zasady, chyba że naprawdę powody. Możesz utworzyć dodatkowe zasady w hello **Konfiguruj** kartę dla przestrzeni nazw hello w portalu hello. Jest ważne toonote, który poziomu drzewa pojedynczego w usłudze Service Bus (przestrzeń nazw, kolejki, itp.) tylko może zawierać maksymalnie too12 tooit zasady dołączone.

## <a name="configuration-for-shared-access-signature-authentication"></a>Konfiguracja uwierzytelniania sygnatura dostępu współdzielonego
Można skonfigurować hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) reguły w przestrzeni nazw usługi Service Bus, kolejki i tematy. Konfigurowanie [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) usługi Service Bus subskrypcji nie jest obecnie obsługiwane, ale może użyć reguły skonfigurowane na przestrzeń nazw lub temat toosubscriptions dostępu toosecure. Dla przykładu pracy, która ilustruje tę procedurę, zobacz hello [uwierzytelniania przy użyciu dostępu sygnatury dostępu Współdzielonego z subskrypcjami magistrali usługi](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) próbki.

Maksymalnie 12 tych zasad można skonfigurować dla przestrzeni nazw usługi Service Bus, kolejka lub temat. Zasady, które są skonfigurowane w przestrzeni nazw usługi Service Bus zastosować tooall jednostki w tej przestrzeni nazw.

![SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO](./media/service-bus-sas/service-bus-namespace.png)

Na tym rysunku hello *manageRuleNS*, *sendRuleNS*, i *listenRuleNS* zastosować reguły autoryzacji tooboth kolejka K1 i tematu T1, podczas gdy *listenRuleQ*  i *sendRuleQ* zastosować tooqueue P1 i *sendRuleT* ma zastosowanie tylko tootopic T1.

Witaj parametrów klucza [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) są następujące:

| Parametr | Opis |
| --- | --- |
| *Nazwa klucza* |Ciąg opisujący hello reguły autoryzacji. |
| *PrimaryKey* |Algorytmem Base64 256-bitowego klucza podstawowego dla podpisywania i sprawdzania poprawności tokenu sygnatury dostępu Współdzielonego hello. |
| *Klucz pomocniczy* |Algorytmem Base64 256-bitowego klucza pomocniczego do podpisywania i sprawdzania poprawności tokenu sygnatury dostępu Współdzielonego hello. |
| *AccessRights* |Lista prawa dostępu przyznane przez regułę autoryzacji hello. Te prawa można dowolną kolekcję nasłuchiwania, wysyłania i Zarządzanie prawami. |

Po zainicjowaniu obsługi przestrzeni nazw usługi Service Bus, [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), z [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) ustawić także**RootManageSharedAccessKey**, domyślnie zostanie utworzona.

## <a name="generate-a-shared-access-signature-token"></a>Generowanie sygnaturą dostępu współdzielonego (token)

same zasady Hello nie jest hello tokenu dostępu dla usługi Service Bus. Jest obiekt hello, z których hello token dostępu jest generowany — przy użyciu albo hello klucz podstawowy lub pomocniczy. Każdy klient, który ma określone w regule autoryzacji dostępu współdzielonego hello kluczy podpisywania toohello dostępu mogą generować hello tokenu sygnatury dostępu Współdzielonego. Hello token jest generowany przez dokładnie obsługuje tworzenie ciągu w hello następującego formatu:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Gdzie `signature-string` jest skrót hello algorytmu SHA-256 zakresu hello hello tokenu (**zakres** zgodnie z opisem w poprzedniej sekcji hello) z znaku CRLF dołączany i czas wygaśnięcia (w sekundach od epoki hello: `00:00:00 UTC` na 1 stycznia 1970). 

> [!NOTE]
> tooavoid czas wygaśnięcia tokenu krótkie, zaleca się kodowania wartość czasu wygaśnięcia hello jako liczbę całkowitą bez znaku przynajmniej 32-bitowej lub najlepiej całkowitą long (64-bitowe).  
> 
> 

Skrót Hello wygląda podobnie toohello po pseudo kod i zwraca 32 bajtów.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

wartości nie mieszane Hello są w hello **SharedAccessSignature** ciąg, dzięki czemu hello adresata można obliczyć skrótu hello z hello takie same parametry, toobe się upewnić, że zwraca hello takiego samego wyniku. Hello identyfikator URI określa zakres hello i nazwę klucza hello identyfikuje hello zasad toobe używane toocompute hello wyznaczania wartości skrótu. Jest to ważne z punktu widzenia zabezpieczeń. Jeśli nie jest zgodna z którego odbiorca hello (usługi Service Bus) oblicza hello podpisu, nastąpi odmowa dostępu. W tym momencie można się tego nadawcy hello ma klucz toohello dostępu i powinny mieć przyznane prawa hello określonym w zasadach hello.

Należy pamiętać, że należy używać hello zakodowany identyfikator URI zasobu dla tej operacji. Identyfikator URI zasobu Hello jest powitalne pełny identyfikator URI hello dostęp do toowhich zasobów usługi Service Bus jest określona. Na przykład `http://<namespace>.servicebus.windows.net/<entityPath>` lub `sb://<namespace>.servicebus.windows.net/<entityPath>`, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

reguły autoryzacji dostępu współdzielonego Hello używany do podpisywania musi być skonfigurowany w jednostce hello określona przez ten identyfikator URI lub za pomocą jednej z jej nadrzędnych hierarchicznej. Na przykład `http://contoso.servicebus.windows.net/contosoTopics/T1` lub `http://contoso.servicebus.windows.net` w poprzednim przykładzie hello.

Token sygnatury dostępu Współdzielonego jest prawidłowa dla wszystkich zasobów w ramach hello `<resourceURI>` używane w hello `signature-string`.

Witaj [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) w hello SAS token odnosi się toohello **keyName** z hello toogenerate hello token używany reguły autoryzacji dostępu współdzielonego.

Hello *adresu URL-zakodowane resourceURI* musi być hello tak samo jak hello identyfikator URI używany w ciągu znak hello podczas obliczania hello hello podpisu. Powinien być [procent, kodowane](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Zalecane jest okresowo generować ponownie klucze hello używane w hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) obiektu. Aplikacje powinny używać zazwyczaj hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate tokenu sygnatury dostępu Współdzielonego. Podczas ponownego generowania kluczy hello, należy zastąpić hello [klucz pomocniczy](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) z hello stary serwer podstawowy, a dla klucza wygenerowanie nowego klucza hello nowego klucza podstawowego. Dzięki temu toocontinue tokeny do autoryzacji, które zostały wydane z hello starego klucza podstawowego i które nie zostały jeszcze wygasnąć.

Jeśli masz klucze hello toorevoke klucz zostanie naruszony, można ponownie wygenerować zarówno hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) i hello [klucz pomocniczy](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) z [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), zastępowane nowych kluczy. Ta procedura powoduje unieważnienie wszystkie tokeny podpisane z kluczami starego hello.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Jak toouse sygnatura dostępu współdzielonego uwierzytelniania za pomocą usługi Service Bus

Witaj następujące scenariusze obejmują konfigurowanie reguł autoryzacji, generowanie tokeny sygnatury dostępu Współdzielonego i uwierzytelnianiem klienta.

Dla pełnej pracy przykładowej aplikacji usługi Service Bus, która ilustruje hello konfiguracji i używa autoryzacji sygnatury dostępu Współdzielonego, zobacz [sygnatura dostępu współdzielonego uwierzytelniania za pomocą usługi Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Powiązane próbki, która ilustruje hello stosowania reguły autoryzacji sygnatury dostępu Współdzielonego skonfigurowane na przestrzeni nazw lub tematy subskrypcje usługi Service Bus toosecure jest dostępnych tutaj: [uwierzytelniania przy użyciu dostępu sygnatury dostępu Współdzielonego z subskrypcji magistrali usług ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Reguły dostępu do udostępnionych autoryzacji dostępu na przestrzeni nazw

Operacje na głównych nazw usługi Service Bus hello wymagają uwierzytelniania certyfikatów. Należy przekazać certyfikatu zarządzania dla subskrypcji platformy Azure. tooupload certyfikat zarządzania, wykonaj kroki hello [tutaj](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), przy użyciu hello [portalu Azure][Azure portal]. Aby uzyskać więcej informacji o certyfikatach zarządzania platformy Azure, zobacz hello [Omówienie certyfikatów Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

punkt końcowy Hello dla uzyskiwania dostępu do reguł autoryzacji dostępu współdzielonego w przestrzeni nazw usługi Service Bus jest następujący:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) obiektu w przestrzeni nazw usługi Service Bus, wykonaj operację POST na ten punkt końcowy z informacjami o reguły hello zserializowanym w formacie JSON i XML. Na przykład:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Podobnie za pomocą operacji GET, na hello punktu końcowego tooread hello autoryzacji reguły skonfigurowane na powitania przestrzeni nazw.

tooupdate lub Usuń regułę autoryzacji określonych Użyj hello następującego punktu końcowego:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Reguły dostępu do udostępnionych autoryzacji dostępu na jednostkę

Dostęp można uzyskać [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) obiektu skonfigurowany dla kolejki usługi Service Bus lub temat za pośrednictwem hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) kolekcji w hello odpowiadającego [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) lub [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Witaj następującego kodu pokazuje, jak reguły autoryzacji tooadd dla kolejki.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Użyj autoryzacji sygnatura dostępu współdzielonego

Aplikacje przy użyciu hello Azure .NET SDK z bibliotekami .NET magistrali usługi hello mogą używać autoryzacji sygnatury dostępu Współdzielonego za pośrednictwem hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) klasy. Witaj poniższy kod przedstawia użycie hello kolejki usługi Service Bus tooa toosend wiadomości powitania dostawcy tokenu.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Aplikacje umożliwia także SAS do uwierzytelniania przy użyciu ciągu połączenia SAS w metodach, które akceptują parametrów połączenia.

Należy pamiętać, że toouse autoryzacji sygnatury dostępu Współdzielonego z przekaźników usługi Service Bus, można użyć klawiszy SAS skonfigurowane na powitania przestrzeń nazw magistrali usług. W przypadku utworzenia jawnie przekaźnik na powitania przestrzeni nazw ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) z [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) obiektu, można ustawić zasady sygnatury dostępu Współdzielonego hello tylko dla tego przekazywania. toouse autoryzacji sygnatury dostępu Współdzielonego z subskrypcji usługi Service Bus, można użyć skonfigurowane na przestrzeni nazw usługi Service Bus lub na temat kluczy sygnatury dostępu Współdzielonego.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Użyj hello Shared Access Signature (na poziomie protokołu HTTP)

Teraz, gdy wiesz, jak toocreate sygnatury dostępu współdzielonego dla dowolnego jednostek usługi Service Bus, jesteś gotowe tooperform HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Należy pamiętać, że wszystko działa. Można utworzyć sygnatury dostępu Współdzielonego dla kolejki, tematu lub subskrypcji. 

Jeśli przekażesz klienta lub nadawcy tokenu sygnatury dostępu Współdzielonego, nie ma klucza hello bezpośrednio i ich nie można wycofać hello skrótu tooobtain go. W efekcie masz kontroli nad co mogą uzyskiwać dostęp do, jak długo. Tooremember ważne jest, że zmiana hello klucza podstawowego w zasadach hello żadnych sygnatur dostępu współdzielonego z niej utworzyć zostaną unieważnione.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Użyj hello Shared Access Signature (na poziomie protokołu AMQP)

W poprzedniej sekcji hello widać, jak toouse hello tokenu sygnatury dostępu Współdzielonego z żądaniem HTTP POST do wysyłania danych toohello usługi Service Bus. Wiesz, można uzyskać dostępu do usługi Service Bus przy użyciu hello zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) będący toouse protokołu hello preferowana ze względu na wydajność w wielu scenariuszach. w dokumencie hello opisano Hello użycia tokenu sygnatury dostępu Współdzielonego za pomocą protokołu AMQP [AMQP Claim-Based zabezpieczeń wersja 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) będący w pracy projekt od 2013, ale dobrze obsługiwane przez platformę Azure dzisiaj.

Przed rozpoczęciem toosend danych tooService magistrali wydawcy hello musi wysłać tokenu sygnatury dostępu Współdzielonego hello wewnątrz protokołu AMQP tooa dobrze zdefiniowany AMQP węzła komunikatu o nazwie **$cbs** (możesz wyświetlić go jako "specjalne" kolejki używane przez hello tooacquire usługi i sprawdź poprawność wszystkich tokeny sygnatury dostępu Współdzielonego Hello). Wydawca Hello musi określać hello **ReplyTo** pól wewnątrz wiadomości powitania protokołu AMQP; to jest węzeł hello, w których hello usługi odpowiedzi wydawcy toohello o hello wynik weryfikacji tokenu hello (żądania/odpowiedzi prostego wzorca między Wydawca i usługi). Ten węzeł odpowiedzi jest tworzona "na powitania bieżąco," mówiąc o "dynamiczne tworzenie zdalnego węzła", zgodnie z opisem w specyfikacji hello protokołu AMQP 1.0. Po sprawdzeniu, czy tokenu sygnatury dostępu Współdzielonego hello jest prawidłowy, hello wydawcy Przejdź dalej i uruchomić usługę toohello danych toosend.

Witaj poniższej procedurze pokazano, jak toosend hello tokenu sygnatury dostępu Współdzielonego przy użyciu hello protokołu AMQP [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) biblioteki. Jest to przydatne, jeśli nie możesz użyć oficjalne hello zestaw SDK usługi Service Bus (na przykład na WinRT, .net Compact Framework, .net Micro Framework i Mono) opracowywanie w języku C\#. Oczywiście Ta biblioteka jest przydatne toohelp zrozumieć, jak opartego na oświadczeniach zabezpieczeń działa na poziomie protokołu AMQP hello, jak przedstawiono, jak to działa na poziomie hello HTTP (z POST protokołu HTTP żądania i hello SAS token wysłany wewnątrz hello "" Nagłówek uwierzytelnienia). Jeśli nie ma potrzeby takich głębokie wiedzą na temat protokołu AMQP, możesz użyć oficjalne hello zestawu SDK magistrali usług z platformą .net Framework aplikacji, co zrobić to za Ciebie.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hello `PutCbsToken()` metody odbiera hello *połączenia* (wystąpienie klasy połączenia protokołu AMQP zgodnie z hello [AMQP .NET Lite biblioteki](https://github.com/Azure/amqpnetlite)) reprezentujący usługi toohello połączeń TCP hello i hello *sasToken* parametr, który jest toosend tokenu sygnatury dostępu Współdzielonego hello. 

> [!NOTE]
> Należy pamiętać, że połączenie hello jest utworzone za pomocą **mechanizmu uwierzytelniania SASL ustawić tooEXTERNAL** (i nie hello zwykły domyślne nazwy użytkownika i hasło używany, gdy nie ma potrzeby tokenu sygnatury dostępu Współdzielonego hello toosend).
> 
> 

Następnie wydawcy hello tworzy dwa łącza AMQP wysyłania tokenu sygnatury dostępu Współdzielonego hello i odbierania odpowiedzi hello (wynik weryfikacji tokenu hello) z usługi hello.

wiadomości powitania AMQP zawiera zbiór właściwości i dodatkowe informacje od prostego komunikatu. token sygnatury dostępu Współdzielonego Hello jest hello treści wiadomości powitania (przy użyciu jego konstruktora). Witaj **"ReplyTo"** właściwość jest ustawiona nazwa węzła toohello do odbierania wynik weryfikacji hello łącze odbiornika hello (można zmienić jego nazwę, i zostanie utworzony dynamicznie przez usługę hello). Hello ostatnich trzech właściwości aplikacji/niestandardowe są używane przez tooindicate usługi hello jakie działanie ma tooexecute. Zgodnie z opisem w hello CBS specyfikacji wersji roboczej, muszą one być hello **nazwy operacji** hello ("put-token"), **typu tokenu** (w tym przypadku "servicebus.windows.net:sastoken"), a hello **" Nazwa"hello odbiorców** toowhich hello token dotyczy (jednostka całego hello).

Po wysłaniu tokenu sygnatury dostępu Współdzielonego hello hello nadawcy łącze, hello wydawcy musi odczytu odpowiedzi hello hello odbiornika łącze. odpowiedź Hello jest prosty komunikat protokołu AMQP z właściwością aplikacji o nazwie **"Kod stanu"** zawierających hello takie same wartości jak kod stanu HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Uprawnienia wymagane dla operacji usługi Service Bus

Witaj poniższej tabeli przedstawiono hello prawa dostępu wymagane przez różne operacje na zasobów usługi Service Bus.

| Operacja | Oświadczenia wymagane | Zakres oświadczeń |
| --- | --- | --- |
| **Namespace** | | |
| Konfiguruj reguły autoryzacji w przestrzeni nazw |Zarządzanie |Każdy adres przestrzeni nazw |
| **Rejestr usługi** | | |
| Wyliczanie zasad prywatnych |Zarządzanie |Każdy adres przestrzeni nazw |
| Rozpoczęcie nasłuchiwania na przestrzeni nazw |Nasłuchiwanie |Każdy adres przestrzeni nazw |
| Wysyłanie wiadomości tooa odbiornika w przestrzeni nazw |Send |Każdy adres przestrzeni nazw |
| **Kolejki** | | |
| Tworzenie kolejki |Zarządzanie |Każdy adres przestrzeni nazw |
| Usuwanie kolejki |Zarządzanie |Każdy adres prawidłową kolejką |
| Wyliczanie kolejek |Zarządzanie |Katalogu zasobów/kolejek |
| Opis kolejki hello pobierania |Zarządzanie |Każdy adres prawidłową kolejką |
| Konfigurowanie reguł autoryzacji dla kolejki |Zarządzanie |Każdy adres prawidłową kolejką |
| Wyślij do kolejki toohello |Send |Każdy adres prawidłową kolejką |
| Odbieranie komunikatów z kolejki |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| Porzuć lub wykonać wiadomości po otrzymaniu wiadomości powitania w trybie blokady podglądu |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| Odroczenie komunikat dla nowszej pobierania |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| Wiadomości utraconych wiadomości |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| Pobierz stan hello skojarzony z sesją kolejki komunikatów |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| Ustaw stan hello skojarzonych z sesją kolejki komunikatów |Nasłuchiwanie |Każdy adres prawidłową kolejką |
| **Temat** | | |
| Tworzenie tematu |Zarządzanie |Każdy adres przestrzeni nazw |
| Usunięcie tematu |Zarządzanie |Każdy adres nieprawidłowy temat |
| Wyliczanie — tematy |Zarządzanie |Katalogu zasobów/tematy |
| Opis tematu hello pobierania |Zarządzanie |Każdy adres nieprawidłowy temat |
| Konfigurowanie reguł autoryzacji dla tematu |Zarządzanie |Każdy adres nieprawidłowy temat |
| Wyślij toohello tematu |Send |Każdy adres nieprawidłowy temat |
| **Subskrypcja** | | |
| Tworzenie subskrypcji |Zarządzanie |Każdy adres przestrzeni nazw |
| Usuń subskrypcję |Zarządzanie |.. /myTopic/Subscriptions/mySubscription |
| Wyliczanie subskrypcji |Zarządzanie |.. / myTopic/subskrypcji |
| Pobrać opisu subskrypcji |Zarządzanie |.. /myTopic/Subscriptions/mySubscription |
| Porzuć lub wykonać wiadomości po otrzymaniu wiadomości powitania w trybie blokady podglądu |Nasłuchiwanie |.. /myTopic/Subscriptions/mySubscription |
| Odroczenie komunikat dla nowszej pobierania |Nasłuchiwanie |.. /myTopic/Subscriptions/mySubscription |
| Wiadomości utraconych wiadomości |Nasłuchiwanie |.. /myTopic/Subscriptions/mySubscription |
| Pobierz stan hello skojarzony z sesją tematu |Nasłuchiwanie |.. /myTopic/Subscriptions/mySubscription |
| Ustaw stan hello skojarzonych z sesją tematu |Nasłuchiwanie |.. /myTopic/Subscriptions/mySubscription |
| **Reguły** | | |
| Utwórz regułę |Zarządzanie |.. /myTopic/Subscriptions/mySubscription |
| Usuwanie reguły |Zarządzanie |.. /myTopic/Subscriptions/mySubscription |
| Wyliczanie zasad |Zarządzanie lub nasłuchiwania |.. /myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat komunikatów usługi Service Bus, zobacz następujące tematy hello.

* [Podstawy usługi Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Kolejki, tematy i subskrypcje usługi Service Bus](service-bus-queues-topics-subscriptions.md)
* [Jak toouse kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Jak toouse usługi Service Bus tematów i subskrypcji](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com