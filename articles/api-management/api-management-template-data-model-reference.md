---
title: "model danych szablonu usługi API Management aaaAzure, odwołanie | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello jednostki i typu oświadczenia dla najczęściej używane w modelach danych hello hello developer portal szablonów w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Odwołanie modelu danych Azure API Management szablonu
W tym temacie opisano hello jednostki i typu oświadczenia dla najczęściej używane w modelach danych hello hello developer portal szablonów w usłudze Azure API Management.  
  
 Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [Interfejs API](#API)  
-   [Podsumowanie interfejsu API](#APISummary)  
-   [Aplikacji](#Application)  
-   [Załącznika](#Attachment)  
-   [Przykładowy kod](#Sample)  
-   [Komentarz](#Comment)  
-   [Filtrowanie](#Filtering)  
-   [Nagłówek](#Header)  
-   [Żądania HTTP](#HTTPRequest)  
-   [Odpowiedź HTTP](#HTTPResponse)  
-   [Problem](#Issue)  
-   [Operacja](#Operation)  
-   [Operacja menu](#Menu)  
-   [Operacja elementu menu](#MenuItem)  
-   [Stronicowania](#Paging)  
-   [Parametr](#Parameter)  
-   [Produktu](#Product)  
-   [Dostawca](#Provider)  
-   [Reprezentacja wartości](#Representation)  
-   [Subskrypcja](#Subscription)  
-   [Podsumowanie subskrypcji](#SubscriptionSummary)  
-   [Informacje o koncie użytkownika](#UserAccountInfo)  
-   [Logowanie użytkownika](#UseSignIn)  
-   [Tworzenia konta użytkownika](#UserSignUp)  
  
##  <a name="API"></a>INTERFEJS API  
 Witaj `API` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|id|Ciąg|Identyfikator zasobu. Interfejs API hello w ramach bieżącego wystąpienia usługi Zarządzanie interfejsami API hello jest unikatowym identyfikatorem. wartość Hello jest prawidłowy względny adres URL w formacie hello `apis/{id}` gdzie `{id}` jest identyfikatorem interfejsu API. Ta właściwość jest tylko do odczytu.|  
|name|Ciąg|Nazwa hello interfejsu API. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|description|Ciąg|Opis hello interfejsu API. Nie może być pusta. Może obejmować formatowanie tagów HTML. Maksymalna długość wynosi 1000 znaków.|  
|serviceUrl|Ciąg|Bezwzględny adres URL usługi zaplecza hello implementacja tego interfejsu API.|  
|Ścieżka|Ciąg|Względny adres URL, który unikatowo identyfikuje ten interfejs API i wszystkie jego ścieżki zasobu w wystąpieniu usługi Zarządzanie interfejsami API hello. Dodawany jest podstawowy adres URL punktu końcowego toohello interfejsu API określona podczas tooform tworzenia wystąpienia usługi hello publiczny adres URL dla tego interfejsu API.|  
|protokoły|Tablica numer|W tym artykule opisano na powitania protokołów, które można wywołać operacji w tym interfejsie API. Dozwolone wartości to `1 - http` i `2 - https`, lub obie.|  
|authenticationSettings|[Ustawienia uwierzytelniania serwera autoryzacji](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Kolekcja ustawień uwierzytelniania zawarte w tym interfejsie API.|  
|subscriptionKeyParameterNames|Obiekt|Opcjonalna właściwość, które mogą być używane toospecify niestandardowych nazw parametrów zapytania lub nagłówek zawierający klucz subskrypcji hello. Jeśli ta właściwość ma musi zawierać co najmniej jeden z dwóch następujących właściwości hello.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a>Podsumowanie interfejsu API  
 Witaj `API summary` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|id|Ciąg|Identyfikator zasobu. Interfejs API hello w ramach bieżącego wystąpienia usługi Zarządzanie interfejsami API hello jest unikatowym identyfikatorem. wartość Hello jest prawidłowy względny adres URL w formacie hello `apis/{id}` gdzie `{id}` jest identyfikatorem interfejsu API. Ta właściwość jest tylko do odczytu.|  
|name|Ciąg|Nazwa hello interfejsu API. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|description|Ciąg|Opis hello interfejsu API. Nie może być pusta. Może obejmować formatowanie tagów HTML. Maksymalna długość wynosi 1000 znaków.|  
  
##  <a name="Application"></a>Aplikacji  
 Witaj `application` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Witaj Unikatowy identyfikator aplikacji hello.|  
|Tytuł|Ciąg|Tytuł Hello aplikacji hello.|  
|Opis|Ciąg|Opis Hello aplikacji hello.|  
|Url|IDENTYFIKATOR URI|Witaj identyfikator URI aplikacji hello.|  
|Wersja|Ciąg|Informacje o wersji dla aplikacji hello.|  
|Wymagania|Ciąg|Opis wymagań aplikacji hello.|  
|Stan|Numer|Witaj bieżący stan aplikacji hello.<br /><br /> -0 - zarejestrowany<br /><br /> -1 - przesłane<br /><br /> -2 - opublikowane<br /><br /> -3 - odrzucone<br /><br /> -4 - nieopublikowane|  
|RegistrationDate|Data i godzina|Aplikacja hello Data i godzina Hello została zarejestrowana.|  
|CategoryId|Numer|Kategoria Hello aplikacji hello (Finance, rozrywka itp.)|  
|DeveloperId|Ciąg|Unikatowy identyfikator Hello hello dewelopera, który przesłał aplikacji hello.|  
|Załączniki|Kolekcja [załącznika](#Attachment) jednostek.|Wszystkie załączniki dla aplikacji hello, takie jak zrzuty ekranu lub ikony.|  
|Ikona|[Załącznika](#Attachment)|Witaj Witaj ikona dla aplikacji hello.|  
  
##  <a name="Attachment"></a>Załącznika  
 Witaj `attachment` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Unikatowy identyfikator|Ciąg|Witaj Unikatowy identyfikator hello załącznika.|  
|Url|Ciąg|adres URL Hello hello zasobów.|  
|Typ|Ciąg|Typ Hello załącznika.|  
|Typ zawartości|Ciąg|Typ nośnika Hello hello załącznika.|  
  
##  <a name="Sample"></a>Przykładowy kod  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Tytuł|Ciąg|Nazwa Hello hello operacji.|  
|fragment kodu|Ciąg|Ta właściwość jest przestarzała i nie powinna być używana.|  
|Pędzel|Ciąg|Które kodu kolorowania toobe szablonu używany podczas wyświetlania hello przykładowy kod. Dozwolone wartości to `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby`, i `csharp`.|  
|szablon|Ciąg|Nazwa Hello ten kod przykładowy szablon.|  
|Treści|Ciąg|Symbolu zastępczego dla części próbki kodu hello hello fragment kodu.|  
|— Metoda|Ciąg|Metoda HTTP operacji hello Hello.|  
|Schemat|Ciąg|Witaj toouse protokołu dla żądania operacji hello.|  
|Ścieżka|Ciąg|Ścieżka Hello hello operacji.|  
|query|Ciąg|Przykład zdefiniowanych parametrów ciągu zapytania.|  
|Host|Ciąg|adres URL Hello bramy usługi Zarządzanie interfejsami API hello hello interfejsu API, który zawiera tę operację.|  
|Nagłówki|Kolekcja [nagłówka](#Header) jednostek.|Nagłówki dla tej operacji.|  
|parameters|Kolekcja [parametru](#Parameter) jednostek.|Parametry, które są zdefiniowane dla tej operacji.|  
  
##  <a name="Comment"></a>Komentarz  
 Witaj `API` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Numer|Identyfikator Hello hello komentarza.|  
|Commenttext —|Ciąg|Treść Hello hello komentarza. Może obejmować HTML.|  
|DeveloperCompany|Ciąg|Nazwa firmy Hello hello developer.|  
|PostedOn|Data i godzina|Witaj Data i godzina hello komentarz został opublikowany.|  
  
##  <a name="Issue"></a>Problem  
 Witaj `issue` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Unikatowy identyfikator Hello hello problemu.|  
|ApiID|Ciąg|Identyfikator Hello hello interfejsu API, dla którego ten problem został zgłoszony.|  
|Tytuł|Ciąg|Tytuł hello problem.|  
|Opis|Ciąg|Opis problemu hello.|  
|SubscriptionDeveloperName|Ciąg|Imię developer hello, który zgłosił problem hello.|  
|IssueState|Ciąg|bieżący stan Hello hello problemu. Możliwe wartości to proponowany, Opened, zamknięte.|  
|ReportedOn|Data i godzina|Hello Data i godzina hello problem został zgłoszony.|  
|Komentarze|Kolekcja [komentarz](#Comment) jednostek.|Komentarze dotyczące tego problemu.|  
|Załączniki|Kolekcja [załącznika](api-management-template-data-model-reference.md#Attachment) jednostek.|Wszelkie problemy toohello załączników.|  
|Usługi|Kolekcja [interfejsu API](#API) jednostek.|Witaj interfejsów API subskrypcję użytkownika hello tooby zgłosić problem hello.|  
  
##  <a name="Filtering"></a>Filtrowanie  
 Witaj `filtering` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|wzorzec|Ciąg|Witaj bieżącego wyszukiwany termin; lub `null` Jeśli brak szukanego terminu.|  
|Symbol zastępczy|Ciąg|Witaj toodisplay tekst w polu wyszukiwania powitania po Brak szukanego terminu określony.|  
  
##  <a name="Header"></a>Nagłówek  
 W tej sekcji opisano hello `parameter` reprezentacji.  
  
|Właściwość|Opis|Typ|  
|--------------|-----------------|----------|  
|name|Ciąg|Nazwa parametru.|  
|description|Ciąg|Opis parametru.|  
|wartość|Ciąg|Wartość nagłówka.|  
|Właściwość TypeName|Ciąg|Typ danych wartości nagłówka.|  
|Opcje|Ciąg|Opcje.|  
|Wymagane|Wartość logiczna|Określa, czy nagłówek hello jest wymagana.|  
|Tylko do odczytu|Wartość logiczna|Określa, czy nagłówek hello jest tylko do odczytu.|  
  
##  <a name="HTTPRequest"></a>Żądania HTTP  
 W tej sekcji opisano hello `request` reprezentacji.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|description|Ciąg|Opis żądania operacji.|  
|Nagłówki|Tablica [nagłówka](#Header) jednostek.|Nagłówki żądań.|  
|parameters|Tablica [parametru](#Parameter)|Kolekcja parametrów żądania operacji.|  
|oświadczenia|Tablica [reprezentacja](#Representation)|Kolekcja reprezentacje żądania operacji.|  
  
##  <a name="HTTPResponse"></a>Odpowiedź HTTP  
 W tej sekcji opisano hello `response` reprezentacji.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|statusCode|Dodatnia liczba całkowita|Kod stanu odpowiedzi operacji.|  
|description|Ciąg|Opis odpowiedzi operacji.|  
|oświadczenia|Tablica [reprezentacja](#Representation)|Kolekcja reprezentacje odpowiedzi operacji.|  
  
##  <a name="Operation"></a>Operacja  
 Witaj `operation` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|id|Ciąg|Identyfikator zasobu. Identyfikuje hello operacji w ramach hello bieżącego wystąpienia usługi Zarządzanie interfejsami API. wartość Hello jest prawidłowy względny adres URL w formacie hello `apis/{aid}/operations/{id}` gdzie `{aid}` jest identyfikatorem interfejsu API i `{id}` jest identyfikator operacji. Ta właściwość jest tylko do odczytu.|  
|name|Ciąg|Nazwa operacji hello. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|description|Ciąg|Opis operacji hello. Nie może być pusta. Może obejmować formatowanie tagów HTML. Maksymalna długość wynosi 1000 znaków.|  
|Schemat|Ciąg|W tym artykule opisano na powitania protokołów, które można wywołać operacji w tym interfejsie API. Dozwolone wartości to `http`, `https`, lub obie `http` i `https`.|  
|Obiekt uriTemplate|Ciąg|Względna szablon adres URL identyfikujący zasób docelowy powitania dla tej operacji. Mogą zawierać parametrów. Przykład:`customers/{cid}/orders/{oid}/?date={date}`|  
|Host|Ciąg|Hello interfejsu API zarządzania bramy adres URL, który obsługuje hello interfejsu API.|  
|HttpMethod|Ciąg|Metoda operacji HTTP.|  
|Żądanie|[Żądania HTTP](#HTTPRequest)|Obiekt zawierający informacje dotyczące żądania.|  
|odpowiedzi|Tablica [odpowiedzi HTTP](#HTTPResponse)|Tablica operacji [odpowiedzi HTTP](#HTTPResponse) jednostek.|  
  
##  <a name="Menu"></a>Operacja menu  
 Witaj `operation menu` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|apiId|Ciąg|Identyfikator Hello hello bieżącego interfejsu API.|  
|CurrentOperationId|Ciąg|Identyfikator Hello hello bieżącej operacji.|  
|Akcja|Ciąg|Typ menu Hello.|  
|Elementy MenuItem|Kolekcja [element menu operacji](#MenuItem) jednostek.|operacje Hello hello bieżącego interfejsu API.|  
  
##  <a name="MenuItem"></a>Operacja elementu menu  
 Witaj `operation menu item` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Identyfikator Hello hello operacji.|  
|Tytuł|Ciąg|Opis Hello hello operacji.|  
|HttpMethod|Ciąg|Metoda Http operacji hello Hello.|  
  
##  <a name="Paging"></a>Stronicowania  
 Witaj `paging` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Strona|Numer|Witaj numer bieżącej strony.|  
|Wartość PageSize|Numer|Witaj toobe maksymalna liczba wyników wyświetlone na jednej stronie.|  
|TotalItemCount|Numer|Witaj liczba elementów do wyświetlenia.|  
|ShowAll|Wartość logiczna|Określa, czy toosho wszystkie wyniki na jednej stronie.|  
|PageCount|Numer|Witaj liczba stron wyników.|  
  
##  <a name="Parameter"></a>Parametr  
 W tej sekcji opisano hello `parameter` reprezentacji.  
  
|Właściwość|Opis|Typ|  
|--------------|-----------------|----------|  
|name|Ciąg|Nazwa parametru.|  
|description|Ciąg|Opis parametru.|  
|wartość|Ciąg|Wartość parametru.|  
|Opcje|Tablica ciągów|Wartości zdefiniowane dla wartości parametrów zapytania.|  
|Wymagane|Wartość logiczna|Określa, czy parametr jest wymagany.|  
|rodzaj|Numer|Określa, czy ten parametr jest parametr path (1) lub parametr querystring (2).|  
|Właściwość TypeName|Ciąg|Typ parametru.|  
  
##  <a name="Product"></a>Produktu  
 Witaj `product` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Identyfikator zasobu. Identyfikuje hello produktu w ramach hello bieżącego wystąpienia usługi Zarządzanie interfejsami API. wartość Hello jest prawidłowy względny adres URL w formacie hello `products/{pid}` gdzie `{pid}` to identyfikator produktu. Ta właściwość jest tylko do odczytu.|  
|Tytuł|Ciąg|Nazwa produktu hello. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|Opis|Ciąg|Opis produktu hello. Nie może być pusta. Może obejmować formatowanie tagów HTML. Maksymalna długość wynosi 1000 znaków.|  
|Warunki|Ciąg|Warunki użytkowania produktów. Deweloperzy toosubscribe toohello produktu w trakcie zostanie wyświetlone i wymagane tooaccept niniejsze warunki przed zakończeniem procesu subskrypcji hello.|  
|ProductState|Numer|Określa, czy produkt hello jest opublikowana lub nie. Opublikowane produkty są wykrywalny przez deweloperów na powitania portalu dla deweloperów. Produkty opublikowane nie są widoczne tylko tooadministrators.<br /><br /> Witaj dopuszczalne wartości stanu produktu są:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|Wartość logiczna|Określa, czy użytkownik może mieć wiele subskrypcji toothis produktu na powitania tym samym czasie.|  
|MultipleSubscriptionsCount|Numer|Liczba Hello produktu toothis subskrypcji przez hello bieżącego użytkownika.|  
  
##  <a name="Provider"></a>Dostawcy  
 Witaj `provider` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Właściwości|Słownik ciągu|Właściwości dla tego dostawcy uwierzytelniania.|  
|Typ authenticationType|Ciąg|Typ dostawcy Hello. (Azure Active Directory, Facebook logowania, konta Google, Microsoft Account, Twitter).|  
|Podpis|Ciąg|Nazwa wyświetlana dostawcy hello.|  
  
##  <a name="Representation"></a>Reprezentacja wartości  
 W tej sekcji opisano `representation`.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Typ zawartości|Ciąg|Określa zarejestrowane lub niestandardowy typ zawartości dla tego reprezentacja, np. `application/xml`.|  
|próbki|Ciąg|Przykład Witaj reprezentacji.|  
  
##  <a name="Subscription"></a>Subskrypcji  
 Witaj `subscription` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Identyfikator zasobu. Identyfikuje hello subskrypcji w ramach hello bieżącego wystąpienia usługi Zarządzanie interfejsami API. wartość Hello jest prawidłowy względny adres URL w formacie hello `subscriptions/{sid}` gdzie `{sid}` jest identyfikator subskrypcji. Ta właściwość jest tylko do odczytu.|  
|Identyfikator produktu|Ciąg|Identyfikator zasobu produktu Hello hello subskrypcję produktu. wartość Hello jest prawidłowy względny adres URL w formacie hello `products/{pid}` gdzie `{pid}` to identyfikator produktu.|  
|ProductTitle|Ciąg|Nazwa produktu hello. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|ProductDescription|Ciąg|Opis produktu hello. Nie może być pusta. Może obejmować formatowanie tagów HTML. Maksymalna długość wynosi 1000 znaków.|  
|ProductDetailsUrl|Ciąg|Względny adres URL toohello szczegółowe informacje.|  
|state|Ciąg|Stan Hello hello subskrypcji. Dostępne są następujące stany:<br /><br /> - `0 - suspended`— Witaj subskrypcji jest zablokowany i hello subskrybenta nie można wywołać wszystkie interfejsy API hello produktu.<br /><br /> - `1 - active`— Witaj subskrypcja jest aktywna.<br /><br /> - `2 - expired`— Witaj subskrypcja osiągnęła daty jego wygaśnięcia i została zdezaktywowana.<br /><br /> - `3 - submitted`— Żądanie subskrypcji hello przez dewelopera hello, ale nie została jeszcze ma zostały zatwierdzone lub odrzucone.<br /><br /> - `4 - rejected`— Witaj subskrypcji żądanie zostało odrzucone przez administratora.<br /><br /> - `5 - cancelled`— Witaj subskrypcja została anulowana przez dewelopera hello lub administratora.|  
|Nazwa wyświetlana|Ciąg|Nazwa wyświetlana hello subskrypcji.|  
|CreatedDate|Data i godzina|Witaj Data hello subskrypcji został utworzony w formacie ISO 8601: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|Wartość logiczna|Określa, czy hello subskrypcji można anulować przez hello bieżącego użytkownika.|  
|IsAwaitingApproval|Wartość logiczna|Określa, czy subskrypcja hello oczekuje na zatwierdzenie.|  
|datą rozpoczęcia|Data i godzina|Witaj Data subskrypcji hello rozpoczęcia w formacie ISO 8601: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|Data i godzina|Data wygaśnięcia Hello hello subskrypcji, w formacie ISO 8601: `2014-06-24T16:25:00Z`.|  
|NotificationDate|Data i godzina|Data powiadomienia Hello hello subskrypcji, w formacie ISO 8601: `2014-06-24T16:25:00Z`.|  
|primaryKey|Ciąg|klucz podstawowy subskrypcji Hello. Maksymalna długość wynosi 256 znaków.|  
|Klucz pomocniczy|Ciąg|Klucz pomocniczy subskrypcji Hello. Maksymalna długość wynosi 256 znaków.|  
|CanBeRenewed|Wartość logiczna|Określa, czy subskrypcja hello mogą być odnawiane przez hello bieżącego użytkownika.|  
|HasExpired|Wartość logiczna|Określa, czy hello subskrypcja utraciła ważność.|  
|IsRejected|Wartość logiczna|Określa, czy hello subskrypcji żądanie zostało odrzucone.|  
|cancelUrl|Ciąg|Witaj względny adres Url toocancel hello subskrypcji.|  
|RenewUrl|Ciąg|Witaj względny adres Url toorenew hello subskrypcji.|  
  
##  <a name="SubscriptionSummary"></a>Podsumowanie subskrypcji  
 Witaj `subscription summary` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Identyfikator|Ciąg|Identyfikator zasobu. Identyfikuje hello subskrypcji w ramach hello bieżącego wystąpienia usługi Zarządzanie interfejsami API. wartość Hello jest prawidłowy względny adres URL w formacie hello `subscriptions/{sid}` gdzie `{sid}` jest identyfikator subskrypcji. Ta właściwość jest tylko do odczytu.|  
|Nazwa wyświetlana|Ciąg|Nazwa subskrypcji hello wyświetlana Hello|  
  
##  <a name="UserAccountInfo"></a>Informacje o koncie użytkownika  
 Witaj `user account info` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Imię|Ciąg|Imię. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|Nazwisko|Ciąg|Nazwisko. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|Adres e-mail|Ciąg|Adres e-mail. Nie może być pusta i musi być unikatowa w obrębie hello wystąpienie usługi. Maksymalna długość to 254 znaków.|  
|Hasło|Ciąg|Hasło do konta użytkownika.|  
|NameIdentifier|Ciąg|Identyfikatora konta, hello taki sam jak adres e-mail użytkownika hello.|  
|ProviderName|Ciąg|Nazwa dostawcy uwierzytelniania.|  
|IsBasicAccount|Wartość logiczna|Wartość true, jeśli konto zostało zarejestrowane za pomocą poczty e-mail i hasło; wartość false, jeśli konto hello został zarejestrowany przy użyciu dostawcy.|  
  
##  <a name="UseSignIn"></a>Logowanie użytkownika  
 Witaj `user sign in` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Adres e-mail|Ciąg|Adres e-mail. Nie może być pusta i musi być unikatowa w obrębie hello wystąpienie usługi. Maksymalna długość to 254 znaków.|  
|Hasło|Ciąg|Hasło do konta użytkownika.|  
|ReturnUrl|Ciąg|Witaj adres URL strony hello gdzie hello użytkownik kliknął logowania.|  
|RememberMe|Wartość logiczna|Określa, czy toosave hello informacje o użytkowniku.|  
|RegistrationEnabled|Wartość logiczna|Określa, czy rejestracja jest włączona.|  
|DelegationEnabled|Wartość logiczna|Określa, czy delegowany logowania jest włączona.|  
|DelegationUrl|Ciąg|Witaj delegowane znaku w adresie url, jeśli włączone.|  
|SsoSignUpUrl|Ciąg|Hello pojedynczego logowania adres URL dla użytkownika hello, jeśli jest obecny.|  
|AuxServiceUrl|Ciąg|Jeśli hello bieżący użytkownik jest administratorem, jest to wystąpienie usługi toohello łącze w hello klasycznego portalu Azure.|  
|Dostawcy|Kolekcja [dostawcy](#Provider) jednostek|Witaj dostawców uwierzytelniania dla tego użytkownika.|  
|UserRegistrationTerms|Ciąg|Warunki, które użytkownik musi wyrazić zgodę toobefore logowania.|  
|UserRegistrationTermsEnabled|Wartość logiczna|Czy warunki są włączone.|  
  
##  <a name="UserSignUp"></a>Tworzenia konta użytkownika  
 Witaj `user sign up` jednostka ma hello następujące właściwości.  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|PasswordConfirm|Wartość logiczna|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up)kontroli rejestracji.|  
|Hasło|Ciąg|Hasło do konta użytkownika.|  
|PasswordVerdictLevel|Numer|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up)kontroli rejestracji.|  
|UserRegistrationTerms|Ciąg|Warunki, które użytkownik musi wyrazić zgodę toobefore logowania.|  
|UserRegistrationTermsOptions|Numer|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up)kontroli rejestracji.|  
|ConsentAccepted|Wartość logiczna|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up)kontroli rejestracji.|  
|Adres e-mail|Ciąg|Adres e-mail. Nie może być pusta i musi być unikatowa w obrębie hello wystąpienie usługi. Maksymalna długość to 254 znaków.|  
|Imię|Ciąg|Imię. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|Nazwisko|Ciąg|Nazwisko. Nie może być pusta. Maksymalna długość wynosi 100 znaków.|  
|Danych użytkownika|Ciąg|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up) formantu.|  
|NameIdentifier|Ciąg|Wartość używana przez hello [rejestracji](api-management-page-controls.md#sign-up)kontroli rejestracji.|  
|ProviderName|Ciąg|Nazwa dostawcy uwierzytelniania.|

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).
