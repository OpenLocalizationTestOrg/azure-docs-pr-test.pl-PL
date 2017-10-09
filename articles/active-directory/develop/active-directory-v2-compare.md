---
title: "aaaWhat różni się w punktu końcowego v2.0 usługi Azure AD hello? | Microsoft Docs"
description: "Porównanie hello oryginalnego usługi Azure AD i punkty końcowe v2.0 hello."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Czym się różni punktu końcowego v2.0 hello?
Jeśli zaznajomieni z usługą Azure Active Directory lub mieć zintegrowanych aplikacji z usługą Azure AD w przeszłości hello, może być pewne różnice w hello punktu końcowego v2.0, nie oczekuje.  Ten dokument uwidacznia różnic zrozumienie.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Konta Microsoft i konta usługi Azure AD
punktu końcowego v2.0 Hello pozwalają deweloperom toowrite aplikacje, które akceptują logowanie z konta Microsoft Accounts i usługi Azure AD przy użyciu punktu końcowego uwierzytelniania pojedynczego.  Dzięki temu hello toowrite możliwości aplikacji całkowicie konta niezwiązane z żadnym; może być ignorujących typu hello hello loguje użytkownika przy użyciu konta.  Oczywiście możesz *można* uświadomić aplikacji hello typ konta używane w określonej sesji, ale nie masz.

Na przykład jeśli aplikacja hello [Microsoft Graph](https://graph.microsoft.io), niektóre dodatkowe funkcje i dane będą dostępne tooenterprise użytkowników, takich jak ich witryn programu SharePoint lub dane katalogu.  Nawet w przypadku wielu akcji takich jak [odczytywanie poczty użytkownika](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), dokładnie można pisać kod hello hello takie same dla konta Microsoft Accounts i usługi Azure AD.  

Integrowanie aplikacji z Accounts Microsoft i kontami usługi Azure AD jest teraz jeden prosty proces.  Można użyć jednego zestawu punktów końcowych, jednej biblioteki i jednej aplikacji rejestracji toogain dostępu tooboth hello konsumenckie i korporacyjne względem.  więcej informacji o toolearn hello punktu końcowego v2.0, zapoznaj się z [hello omówienie](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Nowy portal rejestracji aplikacji
tooregister aplikacji, która współdziała z punktu końcowego v2.0 hello, należy użyć nowego portalu rejestracji aplikacji: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  To jest portal hello, gdzie można uzyskać identyfikator aplikacji, dostosowanie wyglądu hello stronę logowania w aplikacji i inne.  Tooaccess hello portal wystarczy konta Microsoft, jej — osobistych lub pracy/służbowe konto.

## <a name="one-app-id-for-all-platforms"></a>Identyfikator jedną aplikację dla wszystkich platform
Jeśli używano usługi Azure Active Directory, prawdopodobnie została zarejestrowana kilka różnych aplikacji dla jednego projektu.  Na przykład, jeśli utworzono zarówno witrynę sieci Web i aplikacji systemu iOS, trzeba było tooregister je oddzielnie, za pomocą dwóch różnych identyfikatorów aplikacji. portal rejestracji aplikacji Hello Azure AD wymuszone można toomake tej różnicy podczas rejestracji:

![Rejestracja aplikacji starego interfejsu użytkownika](../../media/active-directory-v2-flows/old_app_registration.PNG)

Podobnie jeśli masz witrynę sieci Web i zaplecza, interfejs api sieci web może zarejestrowano jako osobnych aplikacji w usłudze Azure AD.  Lub jeśli masz aplikację systemu iOS i Android — aplikacja również może być zarejestrowany dwóch różnych aplikacji.  Zarejestrowanie każdego składnika aplikacji doprowadziły toosome nieoczekiwane zachowania dla deweloperów i klientów:

* Poszczególne składniki znajdowały się jako osobne aplikację w dzierżawie usługi Azure Active Directory hello każdego klienta.
* Administrator dzierżawy próba tooapply zasad do zarządzania dostępem do lub usuwanie aplikacji zostałyby toodo tak dla każdego składnika aplikacji hello.
* Gdy klienci zgodę tooan aplikacji, każdy składnik zostanie wyświetlony na ekranie zgody hello jako różnych aplikacji.

Z punktem końcowym v2.0 hello może teraz rejestrować wszystkie składniki projektu jako rejestracja jednej aplikacji i użycie jednego identyfikatora aplikacji dla całego projektu.  Możesz dodać kilka tooa "platformy" każdego projektu i podaj hello odpowiednie dane dla każdej platformy, które można dodać.  Oczywiście można utworzyć dowolną liczbę aplikacji, w zależności od wymagań, ale dla większości przypadków hello tylko jeden identyfikator aplikacji powinna być konieczne.

Naszym celem jest ten będzie prowadzić tooa więcej uproszczone zarządzanie aplikacjami i środowisko programistyczne czy utworzyć więcej skonsolidowanego widoku pojedynczego projektu, który może działać na.

## <a name="scopes-not-resources"></a>Zakresy, nie zasobów
W usłudze Azure Active Directory, aplikacja może zachowywać się jak **zasobów**, lub odbiorcy tokenów.  Zasób można zdefiniować wiele **zakresy** lub **oAuth2Permissions** siebie, dzięki czemu aplikacje klienckie toorequest tokenów toothat zasobów dla zestawu zakresów.  Należy wziąć pod uwagę hello Azure AD Graph API, na przykład zasób:

* Identyfikator zasobu lub `AppID URI`:`https://graph.windows.net/`
* Zakresy, lub `OAuth2Permissions`: `Directory.Read`, `Directory.Write`itp.  

Wszystko to jest spełniony dla punktu końcowego v2.0 hello hello.  Aplikacja nadal może działać jako zasób, Zdefiniuj zakresy oraz być identyfikowany przez identyfikator URI.  Aplikacje klienckie nadal mogą żądać zakresy toothose dostępu.  Jednak sposób hello, w którym klient żąda uprawnienia została zmieniona.  W ciągu ostatnich hello OAuth 2.0 autoryzować tooAzure żądania, które AD może sprawdzono, takich jak:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

gdzie hello **zasobów** parametru wskazanych żąda autoryzacji dla aplikacji klienckich hello zasobów.  Usługi Azure AD obliczana hello uprawnień wymaganych przez aplikacji hello na podstawie konfiguracji statycznej w hello portalu Azure i odpowiednio wystawionych tokenów.  Teraz hello tego samego protokołu OAuth 2.0 autoryzować żądania prawdopodobnie:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

gdzie hello **zakres** parametr wskazuje żąda autoryzacji dla aplikacji hello zasobów i uprawnienia. Witaj żądanego zasobu jest nadal bardzo obecne w żądaniu hello — po prostu ujęty w każdej wartości hello hello parametru zakresu.  Za pomocą parametru zakresu hello w ten sposób umożliwia toobe punktu końcowego v2.0 hello bardziej zgodne ze specyfikacją hello OAuth 2.0 i bardziej dokładnie wyrównana z typowe rozwiązania z branży.  Umożliwia również aplikacji tooperform [przyrostowe zgody](#incremental-and-dynamic-consent), który jest opisany w następnej sekcji hello.

## <a name="incremental-and-dynamic-consent"></a>Zgody przyrostowych i dynamicznych
Aplikacje zarejestrowane w toospecify usługi Azure AD wcześniej wymagane ich wymaganych uprawnień OAuth 2.0 w hello portalu Azure w czasie tworzenia aplikacji:

![Uprawnienia rejestracji interfejsu użytkownika](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

wymagana jest aplikacja zostały skonfigurowane uprawnienia Hello **statycznie**.  Dozwolone konfiguracji tooexist aplikacji hello w hello portalu Azure, i przechowywane kodu hello nieuprzywilejowany i proste, przedstawiono kilka problemów dla deweloperów:

* Aplikacja ma tooknow wszystkie uprawnienia hello kiedykolwiek wymagałoby w czasie tworzenia aplikacji.  Dodanie uprawnień w czasie było trudne procesu.
* Aplikacja ma tooknow wszystkie zasoby hello kiedykolwiek dostęp do góry.  Był trudny toocreate aplikacje, które można uzyskać dostępu do dowolnej liczby zasobów.
* Aplikacja ma toorequest wszystkie uprawnienia hello, które kiedykolwiek wymagałoby od użytkownika hello pierwszego logowania.  W niektórych przypadkach doprowadziło to tooa bardzo długą listę uprawnień, które nie zaleca się użytkowników końcowych z zatwierdzanie dostępu aplikacji hello na początkowej logowania.

Z punktem końcowym v2.0 hello, można określić uprawnienia hello potrzeb aplikacji **dynamicznie**, w czasie wykonywania, podczas normalnego użytkowania aplikacji.  toodo tak, można określić hello zakresów potrzeb aplikacji na dowolnym etapie w czasie przez włączenie ich w hello `scope` parametr żądania autoryzacji:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Witaj powyżej prosi o uprawnienie dla tooread aplikacji hello użytkownika usługi Azure AD directory danych, a także katalog tootheir danych zapisu.  Jeśli użytkownik hello zgodził toothose uprawnienia w przeszłości hello dla tej konkretnej aplikacji, wystarczy wprowadzić swoje poświadczenia, a zalogować się do aplikacji hello.  Hello użytkownik zgodził nie tooany tych uprawnień, punktu końcowego v2.0 hello poprosi użytkownika hello zgody toothose uprawnienia.  toolearn więcej, możesz przeczytać na [uprawnień, zgody i zakresy](active-directory-v2-scopes.md).

Możliwość aplikacji uprawnienia toorequest dynamicznie za pośrednictwem hello `scope` parametru zapewnia pełną kontrolę nad środowiskiem użytkownika.  Jeśli chcesz, możesz toofrontload Twojej zgody środowisko i poproś o wszystkie uprawnienia w jednym żądaniu początkowej autoryzacji.  Jeśli aplikacja wymaga dużej liczby uprawnień, można też toogather te uprawnienia od użytkownika hello przyrostowo, jak próbują toouse określonych funkcji aplikacji w czasie.

## <a name="well-known-scopes"></a>Dobrze znane zakresów
#### <a name="offline-access"></a>Dostęp w trybie offline
Aplikacje przy użyciu punktu końcowego v2.0 hello może wymagać hello stosowania nowe uprawnienie dobrze znane aplikacje — hello `offline_access` zakresu.  Wszystkie aplikacje należy toorequest to uprawnienie, jeśli potrzebna jest tooaccess zasobów w imieniu hello użytkownika przez dłuższy okres czasu, nawet jeśli hello użytkownika może nie być aktywnie używających aplikacji hello.  Witaj `offline_access` zakres będzie pojawiał się toohello użytkownika w zgody okna jako "Dostęp do danych w trybie offline", które hello użytkownik musi zaakceptować.  Żądania hello `offline_access` uprawnień umożliwi tooreceive aplikacji sieci web refresh_tokens OAuth 2.0 z punktu końcowego v2.0 hello.  Refresh_tokens są długotrwałe i może zostać wymienione na nowe access_tokens OAuth 2.0 przez dłuższy czas dostępu.  

Jeśli aplikacja nie żąda hello `offline_access` zakresu, nie będą otrzymywali refresh_tokens.  Oznacza to, że gdy zrealizować authorization_code w przepływu kodu autoryzacji hello OAuth 2.0, tylko otrzymasz Wstecz ' access_token ' hello `/token` punktu końcowego.  Tego ' access_token ' pozostanie ważny krótkim czasie (zazwyczaj jedna godzina), ale ostatecznie wygaśnie.  W tym punkcie w czasie, aplikacji, należy tooredirect hello użytkownika wstecz toohello `/authorize` tooretrieve punktu końcowego authorization_code nowe.  Podczas tego przekierowania hello użytkownik może lub może nie wymagają poświadczeń tooenter ponownie lub ponownie zgody toopermissions, w zależności od typu hello hello aplikacji.

więcej informacji na temat protokołu OAuth 2.0, refresh_tokens i access_tokens, wyewidencjonowanie hello toolearn [referencyjne protokołu v2.0](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, profil a poczty e-mail
W przeszłości hello najprostsze przepływ protokołu OpenID Connect logowania w usłudze Azure Active Directory zapewni szereg informacji o użytkowniku hello w żądaniu wynikowy hello.  Hello oświadczeń w żądaniu może zawierać hello użytkownika nazwę, preferowaną nazwy użytkownika, adres e-mail, identyfikator obiektu i więcej.

Możemy teraz Ograniczanie informacji hello tego hello `openid` zakresu zapewnia dostęp do aplikacji.  zakres "openid" Hello będzie tylko umożliwiają toosign aplikacji hello użytkownika w i wyświetlony identyfikator specyficzny dla aplikacji hello użytkownika.  Jeśli chcesz tooobtain dane osobowe lub informacje o użytkowniku hello w aplikacji, aplikacji należy toorequest dodatkowych uprawnień od hello użytkownika.  Wprowadzamy dwa nowe zakresy — Witaj `email` i `profile` zakresy — które umożliwiają toodo tak.

Witaj `email` zakres jest bardzo prosta — umożliwia aplikacji dostęp toohello użytkownika podstawowego adresu e-mail za pośrednictwem hello `email` oświadczeń w żądaniu hello.  Witaj `profile` zakresu zapewnia tooall dostępu do Twojej aplikacji inne podstawowe informacje dotyczące użytkownika hello — ich nazwy, preferowane username identyfikator obiektu i tak dalej.

Dzięki temu można toocode aplikacji w sposób minimalnego ujawnienie — tylko poproś użytkownika hello zestawu hello informacji, że aplikacja wymaga toodo swojego zadania.  Aby uzyskać więcej informacji o tych zakresów, można znaleźć zbyt[hello dokumentacja zakresu v2.0](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Token oświadczeń
Witaj oświadczeń z tokenów wystawionych przez punktu końcowego v2.0 hello nie będzie identyczne tootokens wystawiony przez punkty końcowe hello ogólnie dostępna usługa Azure AD — migracja toohello nowej usługi aplikacji nie powinna przyjęto założenie, że danego oświadczenia będą istnieć w id_tokens lub access_tokens. toolearn o określonych oświadczeń hello emitowanych w tokenów w wersji 2.0, zobacz hello [odwołania do tokenu v2.0](active-directory-v2-tokens.md).

## <a name="limitations"></a>Ograniczenia
Istnieje kilka ograniczeń toobe uwagę podczas korzystania z punktu v2.0 hello.  Zobacz toohello [v2.0 ograniczenia doc](active-directory-v2-limitations.md) toosee w przypadku spełnienia jednego z tych ograniczeń tooyour danego scenariusza.
