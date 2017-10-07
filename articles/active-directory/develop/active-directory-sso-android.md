---
title: "aaaHow tooenable logowania jednokrotnego wielu aplikacji w systemie Android przy użyciu biblioteki ADAL | Dokumentacja firmy Microsoft"
description: 'Jak funkcji hello toouse hello tooenable ADAL SDK rejestracji jednokrotnej w aplikacji. '
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>Jak tooenable logowania jednokrotnego wielu aplikacji w systemie Android przy użyciu biblioteki ADAL
Zapewnianie pojedynczego logowania jednokrotnego (SSO), aby użytkownicy tylko muszą tooenter swoje poświadczenia raz i mieć tych poświadczeń, które są automatycznie pracy w aplikacjach teraz jest oczekiwany przez klientów. Hello trudności w wprowadzić swoją nazwę użytkownika i hasło na małego ekranu, często razy łączyć się przy użyciu dodatkowego składnika (2FA), takich jak rozmowa telefoniczna lub kod wysłana wiadomość SMS, powoduje niezadowolenie szybki, jeśli użytkownik ma toodo to więcej niż jeden raz na produkt.

Ponadto w przypadku zastosowania platformą tożsamości, które inne aplikacje mogą używać takich jak Accounts Microsoft lub konta służbowego z usługi Office 365, klienci oczekują, że te poświadczenia toobe toouse dostępne we wszystkich aplikacjach niezależnie hello dostawcy.

Hello platformy pakietu Microsoft Identity, wraz z nasze zestawy SDK tożsamości Microsoft działa wszystkich tego twardym i zapewnia hello toodelight możliwości swoich klientów za pomocą logowania jednokrotnego, albo w ramach własnego pakietu aplikacji, lub jako z możliwości brokera i wystawcy uwierzytelnienia aplikacje na powitania wszystkich danych z urządzenia.

W tym przewodniku informuje o sposobie tooconfigure naszego zestawu SDK w ramach Twojej aplikacji tooprovide klientów tooyour tego korzyści.

Ten przewodnik dotyczy:

* Usługa Azure Active Directory
* Azure Active Directory B2C
* B2B usługi Azure Active Directory
* Dostęp warunkowy usługi Azure Active Directory

poprzedniego dokumentu Hello przyjęto założenie, wiesz, jak za[udostępnić aplikacje w portalu starszych hello usługi Azure Active Directory](active-directory-how-to-integrate.md) i zintegrowane aplikacji z hello [zestawu SDK systemu Android tożsamości Microsoft](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Pojęcia dotyczące logowania jednokrotnego hello platformą tożsamości Microsoft
### <a name="microsoft-identity-brokers"></a>Brokerzy tożsamość firmy Microsoft
Firma Microsoft udostępnia aplikacji dla każdej platformy przenośne, które umożliwiają mostkowania hello poświadczeń w aplikacjach pochodzących od różnych dostawców i umożliwia specjalne udoskonalone funkcje, które wymagają pojedynczego bezpiecznym miejscu w przypadku toovalidate poświadczeń. Nazywamy je **brokerzy**. W systemach iOS i Android te są realizowane za pośrednictwem aplikacji do pobrania czy klientów zainstalować niezależnie lub można je przesłać toohello urządzeń przez użytkowników, którzy zarządzają niektórych lub wszystkich urządzeń hello dla swoich pracowników firmy. Te brokerzy obsługuje zarządzanie zabezpieczeń tylko dla niektórych aplikacji lub hello wszystkich danych z urządzenia oparte na potrzeby administratorzy IT. W systemie Windows ta funkcja jest dostarczana przez selektora konta wbudowane w system operacyjny toohello technicznie nazywane hello brokera uwierzytelniania sieci Web.

Aby uzyskać więcej informacji na temat używamy tych brokerów i jak klienci mogą je wyświetlać w ich przepływu logowania dla platformy pakietu Microsoft Identity hello na.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Wzorce do logowania na urządzeniach przenośnych
Toocredentials dostępu na urządzeniach wykonaj dwa podstawowe wzorce platformy pakietu Microsoft Identity hello:

* Logowania asystowaną bez brokera
* Broker asystowaną logowania

#### <a name="non-broker-assisted-logins"></a>Logowania asystowaną bez brokera
Inne niż brokera asystowaną logowania są funkcji logowania, które wykonana wbudowany z aplikacji hello i Użyj magazynu lokalnego hello hello urządzenia dla tej aplikacji. Ten magazyn może być współużytkowany przez aplikacje, ale poświadczenia hello są ściśle powiązane toohello aplikacji lub pakietu aplikacji przy użyciu to poświadczenie. W przypadku najprawdopodobniej wystąpienia to w wielu aplikacjach mobilnych podczas wprowadzania nazwy użytkownika i hasła w samej aplikacji hello.

Te nazwy logowania ma hello następujące korzyści:

* Środowisko użytkownika istnieje w całości w aplikacji hello.
* Poświadczenia mogą być współużytkowane przez aplikacje, które są podpisane przez hello tego samego certyfikatu, podając mechanizm obsługi rejestracji jednokrotnej tooyour aplikacji.
* Formant wokół hello środowisko logowania jest dostarczany aplikacji toohello przed i po zalogowaniu.

Te nazwy logowania ma następujące wady hello:

* Użytkownika nie może występować jednokrotnego we wszystkich aplikacji, które używają pakietu Microsoft Identity przez te firmy Microsoft Identities skonfigurowane w aplikacji.
* Nie można używać aplikacji z bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub zestawu InTune hello Użyj produktów.
* Używana aplikacja nie obsługuje uwierzytelniania opartego na certyfikatach dla użytkowników biznesowych.

Oto reprezentację jak zestawy SDK tożsamości Microsoft hello pracować z hello udostępniony magazyn tooenable Twojej aplikacji rejestracji Jednokrotnej:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Broker asystowaną logowania
Asystowane brokera logowania są środowiska logowania, przeprowadzone w ciągu hello brokera aplikacji, które obsługują hello magazynu i zabezpieczeń hello brokera tooshare poświadczeń we wszystkich aplikacjach na urządzeniu hello stosowane hello pakietu Microsoft Identity platformy. Oznacza to, że aplikacje zależne od hello brokera toosign użytkowników w. W systemach iOS i Android brokerzy te są realizowane za pośrednictwem aplikacji do pobrania, czy klientów zainstalować niezależnie lub można je przesłać toohello urządzenia przez firmę, użytkowników, którzy zarządzają hello urządzenie ich użytkownika. Przykładem tego typu aplikacji jest aplikacją Microsoft Authenticator hello w systemie iOS. W systemie Windows ta funkcja jest dostarczana przez selektora konta wbudowane w system operacyjny toohello technicznie nazywane hello brokera uwierzytelniania sieci Web.
środowisko Hello jest zależna od platformy i czasami mogą być destrukcyjne toousers Jeśli nie poprawnie zarządzane. Znasz prawdopodobnie najbardziej tego wzorca Jeśli masz zainstalowaną aplikację usługi Facebook hello i używać funkcji usługi Facebook połączenie z innej aplikacji. Witaj używa platformy pakietu Microsoft Identity hello tego samego wzorca.

Dla systemu iOS prowadzi to animacji "przejścia" tooa aplikacji wysyłania tła toohello podczas aplikacji Microsoft Authenticator hello pochodzi pierwszego planu toohello dla tooselect użytkownika hello konto, które chciałby toosign przy użyciu.  

Dla systemów Android i Windows hello konta selektora jest wyświetlany u góry aplikację, która jest prostszy toohello użytkownika.

#### <a name="how-hello-broker-gets-invoked"></a>Sposób wywoływania pobiera hello brokera
Jeśli zgodny brokera jest zainstalowany na urządzeniu hello, takich jak hello Microsoft Authenticator aplikacji hello zestawów SDK programu Microsoft Identity będzie automatycznie hello pracy wywoływania brokera hello automatycznie, gdy użytkownik wskazuje życzą toolog przy użyciu dowolnego konta z Platforma Microsoft Identity Hello. To konto może być Account firmy Microsoft, służbowy lub konta służbowego lub konta, które należy podać i hosta na platformie Azure przy użyciu naszych produktów B2C i B2B. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>Jak firma Microsoft zapewnia aplikacji hello jest prawidłowy
 
 Hello potrzeby tooensure hello tożsamość aplikacji wywołania hello brokera jest toohello kluczową rolę zabezpieczeń, dostarczamy w danych logowania brokera wspierana. Z systemem iOS ani Android wymusza unikatowych identyfikatorów, które są prawidłowe tylko dla danej aplikacji, więc złośliwego aplikacji może "sfałszować" identyfikator uzasadnionych aplikacji i odbierać tokeny hello przeznaczone dla aplikacji uzasadnionych hello. tooensure, który zawsze komunikują się firma Microsoft z prawej aplikacji hello w czasie wykonywania, poprosimy hello developer tooprovide redirectURI niestandardowych podczas rejestrowania aplikacji z firmą Microsoft. **Jak deweloperzy powinien spreparować identyfikator URI przekierowania omówiono szczegółowo poniżej.** To niestandardowe redirectURI zawiera odcisk palca certyfikatu hello aplikacji hello i jest zapewniana toobe unikatowy toohello aplikacji przez hello sklepu Google Play. Po uruchomieniu brokera hello brokera hello zapyta hello tooprovide systemu operacyjnego Android za pomocą hello odcisk palca certyfikatu tego brokera hello wywołany. Hello broker zawiera ten tooMicrosoft odcisk palca certyfikatu w hello wywołania tooour tożsamości systemu. W przypadku certyfikatów hello odcisk palca aplikacji hello jest niezgodna z odcisk palca certyfikatu hello toous przez dewelopera hello podczas rejestracji, firma Microsoft będzie odmawiał dostępu toohello tokeny dla aplikacji hello zasobów hello jest żądanie. Tego wyboru gwarantuje, że tylko aplikacja hello zarejestrowany przez dewelopera hello odbiera tokenów.

**Deweloper Hello ma wybór hello hello zestaw SDK programu Microsoft Identity wywołuje brokera hello lub korzysta z przepływu asystowaną hello bez brokera.** Jednak jeśli hello developer wybierze nie toouse hello wspierana brokera przepływu utracą zaletą hello przy użyciu poświadczeń logowania jednokrotnego użytkownika hello zostało już dodane na urządzeniu hello i uniemożliwia ich aplikacji z użycia przy użyciu funkcji biznesowych firmy Microsoft Umożliwia klientom, takich jak dostęp warunkowy, możliwości zarządzania usługi Intune i uwierzytelnianie oparte na certyfikatach.

Te nazwy logowania ma hello następujące korzyści:

* Użytkownik napotyka logowania jednokrotnego w swoich aplikacjach bez względu na powitania dostawcy.
* Aplikacji można użyć bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub zestawu InTune hello produktów.
* Aplikacja może obsługiwać uwierzytelnianie oparte na certyfikatach dla użytkowników biznesowych.
* Bardziej bezpieczne logowanie występować jako hello tożsamości aplikacji hello i użytkownika hello są weryfikowane przez aplikację brokera hello z algorytmów zabezpieczeń i szyfrowania.

Te nazwy logowania ma następujące wady hello:

* W systemie iOS hello użytkownika jest są przenoszone poza środowisko aplikacji, a poświadczenia zostały wybrane.
* Wystąpić utrata hello możliwości toomanage hello logowania dla klientów w aplikacji.

Oto reprezentację jak hello zestawów SDK programu Microsoft Identity współpracują z hello broker tooenable aplikacji rejestracji Jednokrotnej:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

Dzięki tym informacje powinno być możliwe toobetter poznanie i wdrożenie logowania jednokrotnego w aplikacji przy użyciu platformy pakietu Microsoft Identity hello i zestawy SDK.

## <a name="enabling-cross-app-sso-using-adal"></a>Włączanie logowania jednokrotnego wielu aplikacji za pomocą biblioteki ADAL
W tym miejscu użyjemy hello ADAL zestawu SDK systemu Android do:

* Włącz brokera z systemem innym niż asystowaną pomocą rejestracji Jednokrotnej dla pakietu aplikacji
* Włączanie obsługi wspierana brokera logowania jednokrotnego

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Włączanie rejestracji Jednokrotnej z systemem innym niż brokera asystowaną pomocą rejestracji Jednokrotnej
Dla innych niż brokera asystowaną logowania jednokrotnego w aplikacjach hello zestawów SDK programu Microsoft Identity Zarządzanie znacznie hello złożoność logowania jednokrotnego dla Ciebie. W tym znajdowanie hello prawo użytkownika w pamięci podręcznej hello i utrzymywanie lista zalogowany użytkowników możesz tooquery.

tooenable logowania jednokrotnego w aplikacjach własnej potrzebne hello toodo następujące:

1. Upewnij się, wszystkie Twoje aplikacje użytkownika hello tego samego Identyfikatora klienta lub identyfikator aplikacji.
2. Upewnij się, że wszystkie aplikacje mają hello ustawione w tej samej SharedUserID.
3. Upewnij się, że wszystkie Twoje hello udziału aplikacji tego samego certyfikatu podpisywania z hello Google Play przechowywać, dzięki czemu można udostępniać magazynu.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Krok 1: Przy użyciu hello na tym samym identyfikatorze klienta / IDENTYFIKATORA aplikacji dla wszystkich hello aplikacji w pakietu aplikacji
Aby tooknow platformy pakietu Microsoft Identity hello, że tokeny tooshare jest dozwolony w aplikacji należy poszczególnych aplikacji hello tooshare tego samego Identyfikatora klienta lub identyfikator aplikacji. Jest to hello Unikatowy identyfikator, który podano tooyou podczas rejestrowania swoją pierwszą aplikację w portalu hello.

Możesz się zastanawiać, jak należy określić różnych aplikacji hello toohello pakietu Microsoft Identity usługa korzysta z tego samego identyfikatora aplikacji. Witaj odpowiedzi jest z hello **identyfikator URI przekierowania**. Każda aplikacja może mieć wiele identyfikator URI przekierowania zarejestrowany w hello przechodzenia do portalu. Każdej aplikacji w zestawie ma inny identyfikator URI przekierowania. Jak wygląda przykład znajduje się poniżej:

Identyfikator URI przekierowania App1`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

Identyfikator URI przekierowania App2`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

Identyfikator URI przekierowania App3:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

Te są zagnieżdżone w ramach tego samego Identyfikatora klienta hello / identyfikator aplikacji i wyszukiwać na podstawie hello przekierowania URI powrocie toous w konfiguracji zestawu SDK.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Należy pamiętać, że format tych identyfikatorów przekierowania hello opisano poniżej. Identyfikator URI przekierowania może używać, chyba że chcesz toosupport hello brokera, w tym przypadku one musi wyglądać hello powyżej*

#### <a name="step-2-configuring-shared-storage-in-android"></a>Krok 2: Konfigurowanie magazynu udostępnionego w systemie Android
Ustawienie hello `SharedUserID` wykracza poza zakres tego dokumentu hello, ale może być rozpoznawane przez odczytanie hello dokumentacji systemu Google Android na powitania [manifestu](http://developer.android.com/guide/topics/manifest/manifest-element.html). Ważne jest określenie mają sharedUserID Twojego zostanie wywołana i używać go do wszystkich aplikacji sieci.

Po utworzeniu hello `SharedUserID` w aplikacjach użytkownika są gotowe toouse logowania jednokrotnego.

> [!WARNING]
> Po udostępnieniu magazynu przez aplikacje dowolnej aplikacji, można usunąć użytkowników lub gorsze usunąć wszystkie tokeny hello w aplikacji. Jest to szczególnie Fatalne, jeśli masz aplikacje, które opierają się na powitania Praca w tle toodo tokenów. Udostępnianie magazynu oznacza, że należy zachować ostrożność bardzo w operacjach Usuń wszystkie za pośrednictwem hello zestawów SDK programu Microsoft Identity.
> 
> 

Gotowe. we wszystkich aplikacji Hello zestaw SDK programu Microsoft Identity teraz udostępniać poświadczeń. Lista użytkowników Hello również zostaną udostępnione w wystąpieniach aplikacji.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Włączanie logowania jednokrotnego dla brokera asystowaną pomocą rejestracji Jednokrotnej
Witaj możliwość toouse aplikacji żadnych broker jest zainstalowana na urządzeniu hello jest **domyślnie wyłączone**. W celu toouse aplikacji z brokera hello należy wykonać pewne dodatkowe czynności konfiguracyjne i dodać niektórych aplikacji tooyour kodu.

Witaj toofollow kroki są następujące:

1. Włącz tryb brokera w kodzie aplikacji toohello wywołania MS SDK
2. Ustanów nowy identyfikator URI przekierowania i podaj, aplikacja hello tooboth i rejestracji aplikacji
3. Konfigurowanie hello odpowiednie uprawnienia w hello manifestu systemu Android

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Krok 1: Włącz broker tryb w aplikacji
Hello możliwości dla twojej aplikacji toouse hello broker jest włączona, podczas tworzenia powitania "ustawienia" lub początkowej konfiguracji wystąpienia uwierzytelniania. Można to zrobić przez ustawienie danego typu ApplicationSettings w kodzie:

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>Krok 2: Ustanowić nowe przekierowania identyfikatorem URI ze schematem adresu URL
Czy możemy zawsze zwracać poświadczeń hello tokeny właściwej aplikacji toohello tooensure kolejności potrzebujemy toomake się, że firma Microsoft wywołania zwrotnego, że tooyour aplikacji w taki sposób, aby hello systemu operacyjnego Android można sprawdzić. system operacyjny Android Hello używa hello skrót certyfikatu hello hello sklepu Google Play. To nie może być sfałszowane przez nieautoryzowanej aplikacji. W związku z tym możemy wykorzystać to wraz z hello URI naszych tooensure aplikacji brokera, że tokeny hello są zwracane toohello właściwej aplikacji. Wymagamy możesz tooestablish przekierowanie Unikatowy identyfikator URI, zarówno w aplikacji i Ustaw jako identyfikator URI przekierowania w portalu deweloperów.

Identyfikator URI przekierowania musi być w formie prawidłowego hello:

`msauth://packagename/Base64UrlencodedSignature`

przykład: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

Ten identyfikator URI przekierowania musi toobe określone w Twojej rejestracji aplikacji przy użyciu hello [portalu Azure](https://portal.azure.com/). Aby uzyskać więcej informacji dotyczących rejestracji aplikacji usługi Azure AD, zobacz [integracji z usługą Azure Active Directory](active-directory-how-to-integrate.md).

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>Krok 3: Konfigurowanie hello odpowiednie uprawnienia w aplikacji
Broker aplikacji w systemie Android używa funkcji Menedżera kont hello hello system operacyjny Android toomanage poświadczeń w aplikacjach. W kolejności toouse hello brokera w systemie Android manifest aplikacji musi mieć uprawnienia toouse elementu AccountManager kont. To została omówiona szczegółowo w hello [Google dokumentację Menedżera kont w tym miejscu](http://developer.android.com/reference/android/accounts/AccountManager.html)

W szczególności te uprawnienia są:

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>Skonfigurowaniu logowania jednokrotnego!
Teraz hello zestaw SDK programu Microsoft Identity automatycznie zarówno udostępnianie poświadczeń w aplikacji i wywołać hello brokera, jeśli jest obecny na urządzeniu.

