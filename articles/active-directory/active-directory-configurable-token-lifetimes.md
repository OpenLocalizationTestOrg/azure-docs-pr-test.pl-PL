---
title: "aaaConfigurable token okresy istnienia w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset okresy istnienia tokeny wystawione przez usługę Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Można skonfigurować tokenu okresy istnienia w usłudze Azure Active Directory (publicznej wersji zapoznawczej)
Można określić okres istnienia hello token wystawiony przez usługę Azure Active Directory (Azure AD). Można ustawić tokenu okresy istnienia dla wszystkich aplikacji w organizacji, dla wielodostępnych aplikacji (wielu organizacji) lub nazwy głównej usługi określonego w organizacji.

> [!NOTE]
> Ta funkcja jest obecnie w wersji zapoznawczej. Można przygotować toorevert lub Usuń wszystkie zmiany. Funkcja Hello jest dostępna w żadnych subskrypcji usługi Azure Active Directory w publicznej wersji zapoznawczej. Gdy funkcja hello staje się ogólnie dostępna, niektórych aspektów funkcji hello mogą jednak wymagać [Azure Active Directory Premium](active-directory-get-started-premium.md) subskrypcji.
>
>

W usłudze Azure AD obiekt zasad reprezentuje zestaw reguł, które są wymuszane na poszczególne aplikacje lub wszystkie aplikacje w organizacji. Każdy typ zasad ma unikatową strukturę, z zestawem właściwości, które są stosowane tooobjects toowhich, które są przypisane.

Zasady można wyznaczyć jako hello domyślne zasady dla Twojej organizacji. zasady Hello jest stosowane tooany aplikacji w organizacji hello, dopóki nie zostanie on przesłonięty przez zasady z wyższym priorytetem. Można również przypisać toospecific zasad aplikacji. Witaj według priorytetu zależy od typu zasad.


## <a name="token-types"></a>Typy tokenów

Można ustawić zasady okres istnienia tokenu dla tokenów odświeżania, tokeny dostępu, tokeny sesji i tokeny Identyfikatora.

### <a name="access-tokens"></a>Tokeny dostępu
Korzystaj z dostępu klientów tokeny tooaccess chronionego zasobu. Token dostępu może służyć tylko dla określonej kombinacji użytkownika, klienta i zasobów. Tokeny dostępu nie może zostać odwołany i są prawidłowe, aż do ich wygaśnięcia. Aktora złośliwy, który uzyskał token dostępu może być używany dla zakresu jego okres istnienia. Dopasowywanie istnienia hello dostępu token jest zależność między poprawianie wydajności systemu i zwiększa hello ilość czasu, który hello klienta zachowuje dostępu po wyłączeniu konta użytkownika hello. Ulepszony system wydajność jest osiągana, zmniejszając hello liczbę razy, gdy klient musi tooacquire tokenu dostępu świeże.

### <a name="refresh-tokens"></a>Tokenów odświeżania
Gdy klient uzyskuje tooaccess tokenu dostępu do chronionego zasobu, klient hello odbiera zarówno token odświeżania i tokenu dostępu. token odświeżania Hello jest tooobtain używane nowe dostępu/odświeżanie tokenu pary po wygaśnięciu hello bieżącego tokenu dostępu. Token odświeżania jest kombinacją powiązanej tooa użytkownika i klienta. Mogą być odwoływane token odświeżania, a ważności tokenu hello jest sprawdzana za każdym razem, gdy hello token jest używany.

Jest ważne toomake różnicy między klienci poufne i publicznej. Aby uzyskać więcej informacji o różnych typach klientów, zobacz [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Token okresy istnienia z tokenów odświeżania poufne klienta
Poufne klienci znajdują się aplikacje, które można bezpiecznie przechowywać hasła klienta (klucz tajny). One udowodnić, że żądania pochodzą z powitania klienta aplikacji, a nie z złośliwego aktora. Na przykład aplikacja sieci web jest poufne klienta, ponieważ umożliwia przechowywanie klucza tajnego klienta na powitania serwera sieci web. Nie jest widoczne. Ponieważ te przepływy są bardziej bezpieczne, hello domyślnych okresów istnienia jest przepływów toothese wystawionych tokenów odświeżania `until-revoked`, nie można zmienić za pomocą zasad i nie zostanie odwołany na resetowanie haseł dobrowolny.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Token okresy istnienia z tokenów odświeżania publicznych klienta

Klienci publiczny nie może bezpiecznie przechowywać hasła klienta (klucz tajny). Na przykład aplikacji systemu iOS/Android nie może zasłaniają klucz tajny z hello właściciela zasobu, aby został oznaczony jako publiczny klienta. Można ustawić zasady zasobów tooprevent tokenów odświeżania z klientów publicznych starsze niż w określonym przedziale czasu uzyskania nowej pary tokenu dostępu/odświeżania. (toodo hello, użyj właściwości odświeżanie tokenu maksymalny czas nieaktywności.) Można też użyć zasad tooset okresu poza które tokeny odświeżania hello nie są akceptowane. (toodo hello, użyj właściwości odświeżanie tokenu maksymalny wiek.) Okres istnienia hello toocontrol token odświeżania, kiedy i jak często hello użytkownika jest wymagane tooreenter poświadczeń, zamiast trwa dyskretnie ponownie uwierzytelnić, korzystając z aplikacji publicznych klienta można dostosować.

### <a name="id-tokens"></a>Tokeny Identyfikatora
Identyfikator tokeny są przekazywane toowebsites i klientach natywnych. Tokeny Identyfikatora zawierają informacje profilu użytkownika. Identyfikator tokenu jest kombinacją określonych powiązanej tooa użytkownika i klienta. Identyfikator tokeny są uznawane za prawidłowe aż do ich wygaśnięcia. Zwykle, aplikacji sieci web odpowiada użytkownik okres istnienia sesji w istnienia toohello aplikacji hello hello identyfikator tokenu wydanych hello użytkownika. Można dostosować okres istnienia hello identyfikator tokenu toocontrol częstotliwość hello aplikacji sieci web wygasa sesji aplikacji hello i jak często wymaga toobe użytkownika hello ponownie uwierzytelnić z usługą Azure AD (dyskretnie lub interaktywnego).

### <a name="single-sign-on-session-tokens"></a>Tokeny sesji rejestracji jednokrotnej
Gdy użytkownik jest uwierzytelniany w usłudze Azure AD i wybiera hello **wylogowuj mnie** pole wyboru sesji rejestracji jednokrotnej (SSO) jest nawiązywane z przeglądarki i Azure AD hello użytkownika. token rejestracji Jednokrotnej Hello, w postaci hello pliku cookie, reprezentuje tej sesji. Należy pamiętać, że tokenu sesji rejestracji Jednokrotnej hello nie jest powiązane tooa określonego zasobu/klienta aplikacji. Mogą być odwoływane tokeny sesji logowania jednokrotnego, a ich ważność jest sprawdzana za każdym razem, gdy są one używane.

Dwa rodzaje tokeny sesji rejestracji Jednokrotnej używa usługi Azure AD: stałe i nietrwałe. Tokeny trwały sesji są przechowywane jako trwałe pliki cookie przez przeglądarkę hello. Tokeny nietrwałych sesji są przechowywane jako pliki cookie z sesji. (Pliki cookie z sesji zostaną zniszczone zamknięcie przeglądarki hello).

Tokeny nietrwałych sesji ma 24-godzinny okres istnienia. Trwałe tokeny będą miały okres istnienia 180 dni. Zawsze, gdy tokenu sesji rejestracji Jednokrotnej jest używana w okresie ważności okres ważności hello jest dłuższy innego 24 godzin lub 180 dni, w zależności od typu tokenu hello. Jeśli tokenu sesji logowania jednokrotnego nie jest używana w okresie ważności, jest on uznawany za wygasła i została już zaakceptowana.

Można użyć zasad tooset hello czasu wystawiony tokenu sesji z pierwszego hello poza które hello tokenu sesji jest już akceptowane. (toodo hello, użyj właściwości maksymalny wiek tokenu sesji.) Można dostosować hello okres istnienia sesji toocontrol token, kiedy i jak często użytkownik jest tooreenter wymaganych poświadczeń, zamiast dyskretnie uwierzytelnianego, korzystając z aplikacji sieci web.

### <a name="token-lifetime-policy-properties"></a>Okres istnienia tokenu właściwości zasady
Zasady okres istnienia tokenu jest typem obiektu zasad, który zawiera reguły okres istnienia tokenu. Użyj właściwości hello toocontrol zasad hello określony okres istnienia tokenu. Jeśli żadne zasady nie jest ustawiona, hello system wymusza hello domyślna wartość okresu istnienia.

### <a name="configurable-token-lifetime-properties"></a>Właściwości można skonfigurować okres istnienia tokenu
| Właściwość | Ciąg właściwości zasady | Dotyczy | Domyślne | Minimalne | Maksymalna |
| --- | --- | --- | --- | --- | --- |
| Okres istnienia tokenu dostępu |AccessTokenLifetime |Tokeny dostępu, tokeny Identyfikatora, SAML2 tokenów |1 godzina |10 minut |1 dzień |
| Odśwież tokenu maksymalny czas nieaktywny |MaxInactiveTime |Tokenów odświeżania |14 dni |10 minut |90 dni |
| Token odświeżania Jednoskładnikowego maksymalny wiek |MaxAgeSingleFactor |Odśwież tokeny (dla wszystkich użytkowników) |Dopóki odwołany |10 minut |Dopóki odwołany<sup>1</sup> |
| Maksymalny wiek tokenu wieloskładnikowego odświeżania |MaxAgeMultiFactor |Odśwież tokeny (dla wszystkich użytkowników) |Dopóki odwołany |10 minut |Dopóki odwołany<sup>1</sup> |
| Maksymalny wiek tokenu sesji Jednoskładnikowego |MaxAgeSessionSingleFactor<sup>2</sup> |Tokeny sesji (stałe i nietrwałe) |Dopóki odwołany |10 minut |Dopóki odwołany<sup>1</sup> |
| Maksymalny wiek tokenu wieloskładnikowego sesji |MaxAgeSessionMultiFactor<sup>3</sup> |Tokeny sesji (stałe i nietrwałe) |Dopóki odwołany |10 minut |Dopóki odwołany<sup>1</sup> |

* <sup>1</sup>hello jawne maksymalnie ustawioną dla tych atrybutów jest 365 dni.
* <sup>2</sup>Jeśli **MaxAgeSessionSingleFactor** nie jest ustawiona, ta wartość ma hello **MaxAgeSingleFactor** wartości. Jeśli parametr nie jest ustawiona, właściwość hello przyjmuje wartość domyślną hello (do odwołane).
* <sup>3</sup>Jeśli **MaxAgeSessionMultiFactor** nie jest ustawiona, ta wartość ma hello **MaxAgeMultiFactor** wartości. Jeśli parametr nie jest ustawiona, właściwość hello przyjmuje wartość domyślną hello (do odwołane).

### <a name="exceptions"></a>Wyjątki
| Właściwość | Dotyczy | Domyślne |
| --- | --- | --- |
| Odśwież tokenu maksymalny wiek (wydane dla użytkowników federacyjnych, którzy mają informacji o odwołaniu niewystarczające<sup>1</sup>) |Tokenów odświeżania (wydane dla użytkowników federacyjnych, którzy mają informacji o odwołaniu niewystarczające<sup>1</sup>) |12 godzin |
| Odśwież tokenu czas nieaktywności Max (wystawiony dla poufnych klientów) |Odśwież tokenów (wystawionych dla klientów poufnych) |90 dni |
| Odśwież tokenu maksymalny wiek (wystawiony dla poufnych klientów) |Odśwież tokenów (wystawionych dla klientów poufnych) |Dopóki odwołany |

* <sup>1</sup>federacyjnym użytkowników, którzy mają wszyscy użytkownicy, którzy nie mają zawierać informacji o odwołaniu niewystarczające hello atrybutu "LastPasswordChangeTimestamp" zsynchronizowane. Ci użytkownicy są podane to krótkie maksymalny wiek, ponieważ AAD jest tooverify, gdy tokeny toorevoke, które są powiązane tooan starą poświadczeń (takich jak hasła, które zostały zmienione) i musi sprawdzić w częściej tooensure użytkownika hello i skojarzone tokeny są nadal w dobrym stanie. tooimprove to środowisko dzierżawy, który Administratorzy musi zapewnić, że trwa synchronizacja hello atrybutu "LastPasswordChangeTimestamp" (to może być ustawiony na powitania obiektu użytkownika przy użyciu programu Powershell lub za pośrednictwem aplikacja AADSync).

### <a name="policy-evaluation-and-prioritization"></a>Ocena zasad i priorytety
Można utworzyć, a następnie przypisać okres istnienia tokenu zasad tooa określonej aplikacji, tooyour organizacji i tooservice podmiotów zabezpieczeń. Wiele zasad mogą być stosowane tooa określonej aplikacji. Witaj okres istnienia tokenu zasady, które obowiązuje obowiązują następujące reguły:

* Jeśli zasady jest jawnie przypisanej nazwy głównej usługi toohello, jest wymuszana.
* Jeśli żadne zasady nie jest jawnie przypisane toohello nazwy głównej usługi, jawnie przypisanej organizacji nadrzędnej toohello nazwy głównej usługi hello zasady są wymuszane.
* Jeśli żadne zasady nie przypisano jawnie nazwy głównej usługi toohello lub toohello organizacji, przypisane toohello aplikacji hello zasady są wymuszane.
* Jeśli żadne zasady nie przypisano toohello service principal, hello organizacji lub obiekt aplikacji hello, hello wartości domyślne są wymuszane. (Zobacz tabelę hello w [właściwości można skonfigurować okres istnienia tokenu](#configurable-token-lifetime-properties).)

Aby uzyskać więcej informacji na temat hello relacji między obiektami aplikacji i głównej usługi, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](active-directory-application-objects.md).

Ważność tokenu jest oceniane w czasie hello hello token jest używany. zasady Hello o najwyższym priorytecie hello na powitania aplikacji, która jest uzyskiwany obowiązuje.

> [!NOTE]
> Oto przykładowy scenariusz.
>
> Użytkownik chce tooaccess dwóch aplikacji sieci web: aplikacja sieci Web A i B. aplikacji sieci Web
> 
> Czynniki:
> * Zarówno aplikacji sieci web znajdują się w hello sam nadrzędnego organizacji.
> * Tokenu okresu istnienia zasad 1 z sesji tokenu maksymalny wiek osiem godzin jest ustawiony jako domyślny organizacji nadrzędnej hello.
> * Aplikacji sieci Web A to aplikacja sieci web użycia regularne i nie jest połączony tooany zasad.
> * B aplikacji sieci Web jest używana do bardzo poufnych procesów. Nazwy głównej usługi jest połączonego tooToken okres istnienia zasad 2, którego sesja tokenu maksymalny wiek 30 minut.
>
> Godzinie 12:00 hello użytkownik uruchamia nową sesję i prób tooaccess A. aplikacji sieci Web hello przekierowanego tooAzure AD i użytkownika monitu toosign w. Spowoduje to utworzenie pliku cookie, który ma w przeglądarce hello tokenu sesji. Użytkownik Hello jest przekierowane tooWeb wstecz A aplikacji z tokenem identyfikator umożliwiający tooaccess użytkownika hello aplikacji hello.
>
> Na 12:15:00 hello użytkownik spróbuje tooaccess B. aplikacji sieci Web hello przeglądarka przekierowuje tooAzure AD, które wykrywa hello pliku cookie sesji. Nazwy głównej usługi B aplikacji sieci Web jest połączonych tooToken okres istnienia zasad 2, ale jest również częścią hello nadrzędnej organizacji. domyślnie tokenu okresu istnienia zasad 1. Tokenu okresu istnienia zasady 2 zostanie zastosowana, ponieważ zasady połączone tooservice podmiotów ma wyższy priorytet niż zasady domyślne organizacji. tokenu sesji Hello było początkowo wydane w ramach hello ostatnich 30 minut, dlatego jest uznawany za ważny. Użytkownik Hello jest przekierowane tooWeb wstecz B aplikacji z tokenem identyfikator, który przyznaje im dostęp.
>
> 1:00 PM hello prób tooaccess A. aplikacji sieci Web hello użytkownika jest przekierowane tooAzure AD. A aplikacji sieci Web nie jest połączony tooany zasady, ale ponieważ jest w organizacji z domyślnego tokenu okresu istnienia zasad 1, ta zasada zostanie uwzględniona. Wykryto Hello pliku cookie sesji, które było początkowo wydane w ramach hello ostatnich ośmiu godzin. Użytkownik Hello jest dyskretnie przekierowanego tooWeb wstecz A aplikacji z tokenem nowy identyfikator. Witaj użytkownik nie jest wymagane tooauthenticate.
>
> Natychmiast potem hello użytkownik spróbuje tooaccess B. aplikacji sieci Web hello użytkownika jest przekierowane tooAzure AD. Jak przedtem tokenu okresu istnienia zasad 2 obowiązuje. Ponieważ hello token został wystawiony ponad 30 minut temu, użytkownik hello jest tooreenter zostanie wyświetlony monit o ich poświadczeń logowania. Tokenu sesji całkowicie nowy i identyfikator token są wystawiane. Witaj, użytkownik może uzyskać dostęp B. aplikacji sieci Web
>
>

## <a name="configurable-policy-property-details"></a>Zasady można skonfigurować właściwości szczegóły
### <a name="access-token-lifetime"></a>Okres istnienia tokenu dostępu
**Ciąg:** AccessTokenLifetime

**Wpływ:** tokenów dostępu, tokeny Identyfikatora

**Podsumowanie:** ta zasada kontroluje, jak długo dostępu i tokeny Identyfikatora dla tego zasobu są uznawane za prawidłowe. Zmniejszenie hello okres istnienia tokenu dostępu właściwości zmniejsza ryzyko hello tokenu dostępu lub identyfikator token używany przez złośliwe aktora przez dłuższy czas. (Te tokenów nie może zostać odwołany.) zależność Hello jest czy to niekorzystny wpływ na wydajność, ponieważ tokeny hello ma toobe zastąpione częściej.

### <a name="refresh-token-max-inactive-time"></a>Odśwież tokenu maksymalny czas nieaktywny
**Ciąg:** MaxInactiveTime

**Wpływ:** tokenów odświeżania

**Podsumowanie:** ta zasada kontroluje, jak stary token odświeżania może być, zanim klient może już używać go tooretrieve nową parę tokenu dostępu/odświeżania podczas próby tooaccess tego zasobu. Ponieważ zazwyczaj nowy token odświeżania jest zwracany, gdy jest używany token odświeżania, ta zasada uniemożliwia dostęp, jeśli hello klient próbuje tooaccess wszystkich zasobów za pomocą tokenu odświeżania bieżącego hello podczas hello określony czas.

Ta zasada powoduje użytkowników, którzy nie są aktywne na ich tooretrieve tooreauthenticate klienta nowy token odświeżania.

Hello odświeżanie tokenu maksymalny czas nieaktywności właściwości musi być ustawiona tooa mniejszą wartość niż hello Jednoskładnikowego Token maksymalny wiek i hello wieloskładnikowego odświeżanie tokenu maksymalny wiek właściwości.

### <a name="single-factor-refresh-token-max-age"></a>Token odświeżania Jednoskładnikowego maksymalny wiek
**Ciąg:** MaxAgeSingleFactor

**Wpływ:** tokenów odświeżania

**Podsumowanie:** to określa zasady jak długo użytkownik służy tooget token odświeżania, nowy dostępu/odświeżanie tokenu pary po ich ostatniego uwierzytelnieniu pomyślnie za pomocą tylko jednego współczynnik. Po użytkownik jest uwierzytelniany i odbiera nowy token odświeżania, hello użytkownik może użyć przepływu tokenu odświeżania hello na powitania określony czas. (Dotyczy to tak długo, jak bieżący token odświeżania hello nie został odwołany, a nie pozostanie nieużywane przez czas dłuższy niż czas nieaktywności hello.) W tym momencie użytkownik hello jest wymuszone tooreauthenticate tooreceive nowy token odświeżania.

Zmniejszenie hello maksymalny wiek wymusza częściej tooauthenticate użytkowników. Ponieważ uwierzytelniania jednoskładnikowego jest uważany za mniej bezpieczne niż uwierzytelnianie wieloskładnikowe, zalecamy ustawienie tej właściwości wartości tooa który jest taki sam tooor wcześniejsza niż hello właściwości wieloskładnikowego odświeżanie tokenu maksymalny wiek.

### <a name="multi-factor-refresh-token-max-age"></a>Maksymalny wiek tokenu wieloskładnikowego odświeżania
**Ciąg:** MaxAgeMultiFactor

**Wpływ:** tokenów odświeżania

**Podsumowanie:** to określa zasady jak długo użytkownik służy tooget token odświeżania, nowy dostępu/odświeżanie tokenu pary po ich ostatniego uwierzytelnieniu pomyślnie za pomocą wiele czynników. Po użytkownik jest uwierzytelniany i odbiera nowy token odświeżania, hello użytkownik może użyć przepływu tokenu odświeżania hello na powitania określony czas. (Dotyczy to tak długo, jak bieżący token odświeżania hello nie został odwołany i nie jest nieużywane przez czas dłuższy niż czas nieaktywności hello.) W tym momencie użytkownicy muszą tooreceive tooreauthenticate nowy token odświeżania.

Zmniejszenie hello maksymalny wiek wymusza częściej tooauthenticate użytkowników. Ponieważ przyjęto, że uwierzytelniania jednoskładnikowego jest mniej bezpieczne niż uwierzytelnianie wieloskładnikowe, zaleca się ustawienie tooa wartość tej właściwości, która jest równa tooor większą niż hello Jednoskładnikowego odświeżanie tokenu maksymalny wiek właściwości.

### <a name="single-factor-session-token-max-age"></a>Maksymalny wiek tokenu sesji Jednoskładnikowego
**Ciąg:** MaxAgeSessionSingleFactor

**Wpływ:** tokeny sesji (stałe i nietrwałe)

**Podsumowanie:** to zasady Określa jak długo użytkownik może używać tooget tokenu sesji, nowy identyfikator i sesji token po ich ostatniego uwierzytelnieniu pomyślnie za pomocą tylko jednego współczynnik. Po użytkownik jest uwierzytelniany i otrzymuje token nowej sesji, hello użytkownik może użyć przepływu tokenu sesji hello na powitania określony czas. (Dotyczy to tak długo, jak hello tokenu bieżącej sesji nie został odwołany i nie wygasł.) Po hello określony czas, użytkownik hello jest wymuszone tooreauthenticate tooreceive token nowej sesji.

Zmniejszenie hello maksymalny wiek wymusza częściej tooauthenticate użytkowników. Ponieważ przyjęto, że uwierzytelniania jednoskładnikowego jest mniej bezpieczne niż uwierzytelnianie wieloskładnikowe, zaleca się ustawienie tooa wartość tej właściwości, która jest równa właściwości Multi-Factor sesji tokenu maksymalny wiek tooor poniżej hello.

### <a name="multi-factor-session-token-max-age"></a>Maksymalny wiek tokenu wieloskładnikowego sesji
**Ciąg:** MaxAgeSessionMultiFactor

**Wpływ:** tokeny sesji (stałe i nietrwałe)

**Podsumowanie:** to zasady Określa jak długo użytkownik może używać tooget tokenu sesji, nowy identyfikator i sesji token po hello ostatniego pomyślnie uwierzytelnione przy użyciu wiele czynników. Po użytkownik jest uwierzytelniany i otrzymuje token nowej sesji, hello użytkownik może użyć przepływu tokenu sesji hello na powitania określony czas. (Dotyczy to tak długo, jak hello tokenu bieżącej sesji nie został odwołany i nie wygasł.) Po hello określony czas, użytkownik hello jest wymuszone tooreauthenticate tooreceive token nowej sesji.

Zmniejszenie hello maksymalny wiek wymusza częściej tooauthenticate użytkowników. Ponieważ przyjęto, że uwierzytelniania jednoskładnikowego jest mniej bezpieczne niż uwierzytelnianie wieloskładnikowe, zaleca się ustawienie tooa wartość tej właściwości, która jest równa tooor większą niż hello Jednoskładnikowego sesji tokenu maksymalny wiek właściwości.

## <a name="example-token-lifetime-policies"></a>Przykładowe zasady okres istnienia tokenu
Wiele scenariuszy są możliwe w usłudze Azure AD, gdy można tworzyć i zarządzać istnienia tokenu dla aplikacji, nazwy główne usług i Twojej organizacji. W tej sekcji możemy przeprowadzenie kilka typowych scenariuszy zasad, które mogą pomóc Ci skonfigurować nowe zasady:

* Okres istnienia tokenu
* Token maksymalny czas nieaktywny
* Maksymalny wiek token

W przykładach hello, możesz dowiedzieć się jak:

* Zarządzanie organizacji domyślne zasady
* Tworzenie zasad dla rejestracji w sieci web
* Tworzenie zasad dla natywnych aplikacji, która wywołuje interfejs API sieci web
* Zarządzanie zasadami zaawansowane

### <a name="prerequisites"></a>Wymagania wstępne
Następujące przykłady hello służy do tworzenia, aktualizacji, łączenie i usuwania zasady dla aplikacji, nazwy główne usług i Twojej organizacji. Jeśli nowy tooAzure AD, firma Microsoft zaleca zapoznanie się [jak dzierżawy tooget usługi Azure AD](active-directory-howto-tenant.md) przed przystąpieniem do tych przykładów.  

tooget pracę, hello następujące kroki:

1. Pobierz najnowsze hello [Azure AD PowerShell modułu publicznej wersji zapoznawczej](https://www.powershellgallery.com/packages/AzureADPreview).
2. Uruchom hello `Connect` toosign polecenia w tooyour konta administratora usługi Azure AD. Uruchom to polecenie za każdym razem, należy uruchomić nową sesję.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee wszystkie zasady, które zostały utworzone w organizacji, hello uruchom następujące polecenie. Po większości operacji w hello następujące scenariusze, uruchom to polecenie. Polecenia hello również pomaga uzyskać hello ** ** zasad.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Przykład: Zarządzanie organizacji domyślne zasady
W tym przykładzie utworzysz zasady, które pozwala użytkownikom zalogować się rzadziej w całej organizacji. toodo, Utwórz zasadę okres istnienia tokenu Jednoskładnikowego Odśwież tokenów, która jest stosowana w całej organizacji. Hello zasady są stosowane tooevery aplikacji w organizacji, a nazwy głównej usługi tooeach, który nie ma jeszcze zestaw zasad.

1. Utwórz zasadę okres ważności tokenu.

    1.  Ustaw hello tokenu odświeżania Jednoskładnikowego zbyt "do odwołanych." Hello token nie wygasa, dopóki dostęp został odwołany. Utwórz powitania po definicji zasad:

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  toocreate hello zasad, uruchom następujące polecenie hello:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee nowe zasady, a zasady hello tooget **ObjectId**Uruchom hello następujące polecenie:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Aktualizuj zasady hello.

    Możesz określić hello pierwszej zasady, w tym przykładzie nie jest tak rygorystycznych, jak usługa wymaga. Uruchom z tokenu odświeżania Jednoskładnikowego tooexpire dwóch dni tooset hello następujące polecenie:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Przykład: Tworzenie zasad dla rejestracji w sieci web

W tym przykładzie należy utworzyć zasadę, która wymaga tooauthenticate użytkownicy często w aplikacji sieci web. Ta zasada ustawia okres istnienia tokenów dostępu/identyfikator hello hello i hello maksymalny wiek nazwy głównej usługi toohello tokenu wieloskładnikowego sesji aplikacji sieci web.

1. Utwórz zasadę okres ważności tokenu.

    Te zasady dla sieci web logowania, Ustawia okres istnienia tokenu dostępu/identyfikator hello i hello sesji jednoskładnikowego maksymalny wiek tokenu tootwo godzin.

    1.  toocreate hello zasad, uruchom to polecenie:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee nowe zasady, a zasady hello tooget **ObjectId**Uruchom hello następujące polecenie:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Przypisz hello zasad tooyour service principal. Należy również tooget hello **ObjectId** z Twojej nazwy głównej usługi. 

    1.  toosee nazwy główne usług wszystkich organizacji, można zbadać [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Lub, w [Explorer Azure AD Graph](https://graphexplorer.cloudapp.net/), zaloguj się tooyour konto usługi Azure AD.

    2.  Jeśli masz hello **ObjectId** z Twojej nazwy głównej usługi, uruchom hello następujące polecenie:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Przykład: Tworzenie zasad dla natywnych aplikacji, która wywołuje interfejs API sieci web
W tym przykładzie utworzysz zasady, które często wymaga tooauthenticate użytkowników. Witaj zasad powoduje nieznaczne również wydłużenie hello ilość czasu, który użytkownik może być nieaktywne, zanim hello użytkownik musi ponownie uwierzytelniać. Hello zasady są stosowane toohello interfejsu API sieci web. Aplikacji natywnej hello żądań interfejsu API sieci web hello jako zasób, dotyczą te zasady.

1. Utwórz zasadę okres ważności tokenu.

    1.  toocreate ścisłych zasad dla składnika web API, uruchom następujące polecenie hello:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee nowe zasady, a zasady hello tooget **ObjectId**Uruchom hello następujące polecenie:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Przypisz hello zasad tooyour — interfejs API sieci web. Należy również tooget hello **ObjectId** aplikacji. Witaj najlepsze sposób toofind aplikacji **ObjectId** jest toouse hello [portalu Azure](https://portal.azure.com/).

   Jeśli masz hello **ObjectId** aplikacji, uruchom następujące polecenie hello:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Przykład: Zarządzanie zaawansowane zasad
W tym przykładzie utworzysz zasady kilka, toolearn działania hello priorytet systemu. Możesz także dowiedzieć się jak toomanage wiele zasad, które są stosowane tooseveral obiektów.

1. Utwórz zasadę okres ważności tokenu.

    1.  toocreate domyślne zasady organizacji, która ustawia hello too30 okres istnienia tokenu odświeżania Jednoskładnikowego dni, uruchom następujące polecenie hello:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee nowe zasady, a zasady hello tooget **ObjectId**Uruchom hello następujące polecenie:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Przypisz hello zasad tooa service principal.

    Masz teraz zasady, która ma zastosowanie toohello całej organizacji. Może mają te zasady 30-dniowej toopreserve dla podmiotu określonej usługi, ale zmiana hello organizacji domyślne zasady toohello górnej granicy "do odwołanych."

    1.  toosee nazwy główne usług wszystkich organizacji, można zbadać [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Lub, w [Explorer Azure AD Graph](https://graphexplorer.cloudapp.net/), zaloguj się przy użyciu konta usługi Azure AD.

    2.  Jeśli masz hello **ObjectId** z Twojej nazwy głównej usługi, uruchom hello następujące polecenie:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Zestaw hello `IsOrganizationDefault` Flaga toofalse:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Utwórz nowe zasady domyślne organizacji:

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Masz teraz hello oryginalnego zasad tooyour połączonej nazwy głównej usługi i hello nowych zasad jest ustawiona jako zasada domyślna Twojej organizacji. Jest ważne tooremember czy podmiotów tooservice zastosować zasady mają priorytet nad organizacji domyślne zasady.

## <a name="cmdlet-reference"></a>Dokumentacja poleceń cmdlet

### <a name="manage-policies"></a>Zarządzanie zasadami

Możesz użyć hello następujące polecenia cmdlet toomanage zasady.

#### <a name="new-azureadpolicy"></a>Nowe AzureADPolicy

Tworzy nowe zasady.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Tablica stringified JSON, który zawiera wszystkie zasady hello reguły. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Ciąg hello nazwę zasady. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |Jeśli PRAWDA, ustawia hello zasad jako zasady domyślne hello organizacji. W przypadku wartości FAŁSZ nie działa. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |Typ zasad. Okresy istnienia tokenu zawsze używaj "TokenLifetimePolicy." | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[Opcjonalnie] |Ustawia alternatywny identyfikator hello zasad. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Pobiera wszystkie zasady usługi Azure AD lub określonych zasad.

```PowerShell
Get-AzureADPolicy
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code>[Opcjonalnie] |**Identyfikator obiektu (Id)** zasad hello ma. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Pobiera wszystkie aplikacje i nazwy główne usług, które są połączone tooa zasad.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** zasad hello ma. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Zestaw AzureADPolicy
Aktualizuje istniejące zasady.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** zasad hello ma. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Ciąg hello nazwę zasady. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code>[Opcjonalnie] |Tablica stringified JSON, który zawiera wszystkie zasady hello reguły. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code>[Opcjonalnie] |Jeśli PRAWDA, ustawia hello zasad jako zasady domyślne hello organizacji. W przypadku wartości FAŁSZ nie działa. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code>[Opcjonalnie] |Typ zasad. Okresy istnienia tokenu zawsze używaj "TokenLifetimePolicy." |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[Opcjonalnie] |Ustawia alternatywny identyfikator hello zasad. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Usuń AzureADPolicy
Usuwa hello określone zasady.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** zasad hello ma. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Zasady aplikacji
Możesz użyć następującego polecenia cmdlet dla zasad aplikacji hello.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Dodaj AzureADApplicationPolicy
Łącza hello określone zasady tooan aplikacji.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**Identyfikator obiektu** hello zasad. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Pobiera hello zasady, które jest przypisane tooan aplikacji.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Usuń AzureADApplicationPolicy
Usuwa zasady z aplikacją.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**Identyfikator obiektu** hello zasad. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Zasady głównej usługi
Możesz użyć hello następującego polecenia cmdlet dla zasad główną usługi.

#### <a name="add-azureadserviceprincipalpolicy"></a>Dodaj AzureADServicePrincipalPolicy
Łącza hello nazwy głównej usługi tooa określonych zasad.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**Identyfikator obiektu** hello zasad. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Pobiera podmiot zabezpieczeń wszelkie zasady połączone toohello określonej usługi.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Usuń AzureADServicePrincipalPolicy
Usuwa zasady hello z hello określoną usługę podmiotu.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| Parametry | Opis | Przykład |
| --- | --- | --- |
| <code>&#8209;Id</code> |**Identyfikator obiektu (Id)** aplikacji hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**Identyfikator obiektu** hello zasad. | `-PolicyId <ObjectId of Policy>` |
