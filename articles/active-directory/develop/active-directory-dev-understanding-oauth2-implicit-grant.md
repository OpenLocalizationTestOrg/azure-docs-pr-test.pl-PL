---
title: "hello aaaUnderstanding OAuth2 niejawne Przyznaj przepływu w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o implementacji usługi Azure Active Directory przepływu niejawne Przyznaj hello OAuth2, oraz czy jest odpowiednie dla aplikacji."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Opis hello OAuth2 niejawne Przyznaj przepływu w usłudze Azure Active Directory (AD)
niejawne Przyznaj Hello OAuth2 jest odpowiedzialne za trwa grant hello z najdłuższym listy problemy z zabezpieczeniami w specyfikacji protokołu OAuth2 hello hello. I jeszcze, jest implementowany przez ADAL JS i hello jedną, zalecamy podczas pisania aplikacji JEDNOSTRONICOWEJ podejście hello. Co daje? Jest to kwestia kompromisów: i jak okaże się niejawne Przyznaj hello jest hello najlepszym podejściem może prowadzić do aplikacji, które wykorzystują interfejs API sieci Web za pośrednictwem kodu JavaScript w przeglądarce.

## <a name="what-is-hello-oauth2-implicit-grant"></a>Co to jest niejawne Przyznaj hello OAuth2?
Witaj quintessential [udzielania kodu autoryzacji OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.1) jest hello udzielania autoryzacji, które używa dwóch osobnych punktów końcowych. punkt końcowy autoryzacji Hello jest używany na etapie interakcji użytkownika hello, co powoduje kod autoryzacji. punktu końcowego tokena Hello jest następnie używany przez klienta na powitania wymiany hello kod tokenu dostępu, a często również token odświeżania. Aplikacje sieci Web są wymagane toopresent własnych aplikacji poświadczenia toohello punktu końcowego tokena, dzięki czemu hello autoryzacji serwer może uwierzytelnić powitania klienta.

Witaj [OAuth2 niejawne Przyznaj](https://tools.ietf.org/html/rfc6749#section-1.3.2) jest wariant innych przyznaje autoryzacji. Umożliwia tooobtain klienta tokenu dostępu (i żądaniu, korzystając z [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) bezpośrednio z punktu końcowego autoryzacji hello, bez kontaktowania się z punktu końcowego tokena hello ani uwierzytelniania powitania klienta. Ten wariant zostało zaprojektowane specjalnie dla aplikacji działających w przeglądarce sieci Web oparte na języku JavaScript: w oryginalnej specyfikację OAuth2 hello tokeny są zwracane w fragmentu identyfikatora URI. Dzięki temu hello tokenu usługi bits dostępne toohello kodu JavaScript w kliencie hello, ale gwarantuje, że nie będą uwzględniane w przekierowuje kierunku powitania serwera. Zwracanie tokeny za pośrednictwem przeglądarki przekierowuje bezpośrednio z punktu końcowego autoryzacji hello. Ma ona zaletą hello wyeliminowanie wszelkie wymagania dotyczące wielu wywołań źródła, które są niezbędne, jeśli hello aplikacji JavaScript jest wymagana toocontact punktu końcowego tokena hello.

Istotne cechy niejawne Przyznaj hello OAuth2 jest hello fakt, że takie przepływów nigdy nie należy zwracać klienta toohello tokenów odświeżania. Jak zostanie wyświetlone w następnej sekcji hello, który nie jest naprawdę konieczne i faktycznie jest problem z zabezpieczeniami.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Przyznanie odpowiedniego scenariusze hello OAuth2 niejawne
Jak specyfikację OAuth2 hello sam deklaruje, hello niejawne Przyznaj została opracowana tooenable agenta użytkownika aplikacje — czyli toosay JavaScript wykonywania w przeglądarce. Definiowanie cech takich aplikacji Hello jest, że kod JavaScript jest używana do uzyskiwania dostępu do zasobów serwera (zwykle interfejs API sieci Web) i aktualizowania aplikacji hello UX odpowiednio. Pomyśl o aplikacjach, takich jak usługi Gmail lub Outlook Web Access: po wybraniu wiadomości ze skrzynki odbiorczej wiadomość hello tylko wizualizacji panel zmienia toodisplay hello wyboru nowego, podczas hello reszty strony hello pozostaje niezmieniona. W przeciwieństwie do tradycyjnych przekierowania aplikacji opartych na sieci Web, to, gdzie każdej interakcji użytkownika powoduje odświeżenie strony całą stronę i renderowanie strony pełnego hello nową odpowiedź serwera.

Aplikacje jednostronicowe lub źródła noszą nazwę aplikacji, które mają bardzo tooits podejście oparty na języku JavaScript hello: hello chodzi o to, że te aplikacje tylko obsługiwać początkowej strony HTML i JavaScript skojarzone z wszystkich kolejnych interakcjach prowadzone przez Wywołania interfejsu API sieci Web są wykonywane za pośrednictwem kodu JavaScript. Jednak hybrydowego podejścia, gdzie aplikacji hello jest przeważnie oparte na odświeżenie strony, ale wykonuje okazjonalne wywołania JS, nie są rzadko — hello dyskusji o użyciu niejawnego przepływu dotyczy tych również.

Aplikacje oparte na przekierowaniu zwykle bezpieczne ich żądania za pomocą plików cookie, jednak, które podejście nie działa także dla aplikacji JavaScript. Pliki cookie są prawidłowe tylko względem domeny hello one zostały wygenerowane, gdy wywołania języka JavaScript mogą być kierowane do innych domen. W rzeczywistości, który często będzie hello przypadku: reakcji aplikacji wywoływanie interfejsu API programu Graph firmy Microsoft, interfejsu API usługi Office, interfejsu API Azure — wszystkie znajdującej się poza domeną hello, z którym aplikacji hello jest obsługiwana. Rosnącą dla aplikacji JavaScript jest toohave nie wewnętrznej bazy danych na wszystkich jednostki uzależnionej 100% na 3 tooimplement interfejsów API sieci Web producentów ich funkcję biznesową.

Obecnie hello preferowaną metodą ochrony tooa wywołania interfejsu API sieci Web jest toouse hello OAuth2 elementu nośnego token metody, których każdego wywołania towarzyszy token dostępu OAuth2. Hello interfejsu API sieci Web sprawdza hello przychodzący token dostępu i, jeśli znajdzie się w jej hello niezbędne zakresy, udziela dostępu toohello żądanej operacji. przepływu niejawnego Hello zawiera wygodny mechanizm aplikacji JavaScript tokenów dostępu tooobtain interfejs API sieci Web oferującemu wiele korzyści z przestrzegania toocookies:

* Tokeny można niezawodnie uzyskać bez potrzeby wielu wywołań pochodzenia — obowiązkowe rejestracji toowhich identyfikator URI przekierowania hello tokeny są zwrócić gwarantuje, że tokeny nie są przemieszczeniu
* Aplikacji JavaScript można uzyskać tyle tokenów dostępu potrzebują, na tyle interfejsów API sieci Web ich elementami docelowymi — bez żadnych ograniczeń w domenach
* Funkcje HTML5, takie jak sesji lub Magazyn lokalny przyznać pełną kontrolę nad buforowaniem tokena i zarządzanie okresem istnienia plików cookie zarządzania jest nieprzezroczysta toohello aplikacji
* Tokeny dostępu nie są podatne lokacji tooCross (CSRF) fałszerstwie żądania

Przepływ niejawne Przyznaj Hello nie wystawia tokeny odświeżania, przede wszystkim ze względów bezpieczeństwa. Token odświeżania nie jest w ściśle zakresu jako tokenów dostępu, udzielanie znacznie więcej mocy dlatego inflicting znacznie więcej szkód w przypadku, gdy jest wyciekiem. W hello niejawnego przepływu tokeny są dostarczane w adresie URL hello, dlatego hello ryzyko przechwycenia wyższe niż w udzielania kodu autoryzacji hello.

Jednak pamiętaj, że aplikacja JavaScript ma inny mechanizm dyspozycji do odnawiania tokenów dostępu bez monitowania wielokrotnie hello poświadczenia użytkownika. Witaj aplikacja może używać ukryte iframe tooperform nowy token żądania do hello autoryzacji punktu końcowego usługi Azure AD: tak długo, jak przeglądarki hello jest nadal aktywna sesja (do odczytu: ma plik cookie sesji) względem domeny hello Azure AD hello żądanie uwierzytelnienia może wystąpić pomyślnie bez konieczności interakcji z użytkownikiem.

Ten model umożliwia hello JavaScript aplikacji hello tooindependently odnowić tokenów dostępu, a nawet uzyskać nowe nowego interfejsu API (pod warunkiem, że hello użytkownika wcześniej zgodę dla nich. Dzięki temu można uniknąć hello dodany konieczności pobierania, utrzymywaniem i ochrona artefaktów wysokiej wartości, takie jak token odświeżania. Witaj artefaktu co umożliwia odnowienie dyskretnej hello, hello pliku cookie sesji usługi Azure AD, odbywa się poza aplikacji hello. Zaletą tej metody jest użytkownika można wylogować się z usługi Azure AD przy użyciu aplikacji hello rejestracji w usłudze Azure AD, uruchomiony w dowolnym hello kartach przeglądarki. Spowoduje to usunięcie hello hello pliku cookie z sesji usługi Azure AD i hello aplikacji JavaScript automatycznie utracisz możliwość hello toorenew tokeny dla hello wylogowywanie użytkownika.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>Niejawne Przyznaj hello jest odpowiednia do mojej aplikacji?
niejawne Przyznaj Hello niesie ze sobą ryzyka więcej niż inne przyznaje i obszarów hello należy tooare uwagi toopay dobrze udokumentowane. Na przykład [tooImpersonate nieprawidłowe użycie elementu Token dostępu właściciela zasobu w przepływu niejawnego] [ OAuth2-Spec-Implicit-Misuse] i [modelu zagrożeń OAuth 2.0 i zagadnienia dotyczące zabezpieczeń] [ OAuth2-Threat-Model-And-Security-Implications]). Przede wszystkim powodu toohello fakt, że ten tooenable aplikacjom wykonanie kodu active, obsługiwane przez przeglądarkę tooa zasób zdalny jest jednak hello wyższy profil ryzyka. Jeśli planujesz architekturę SPA nie składniki wewnętrznej bazy danych lub mają tooinvoke interfejs API sieci Web za pośrednictwem kodu JavaScript, zalecane jest użycie przepływu niejawnego hello uzyskania tokenu.

Jeśli aplikacja jest klientami, hello niejawnego przepływu nie stanowi doskonałe dopasowanie. Witaj braku pliku cookie sesji hello Azure AD w kontekście powitania klienta natywnego pozbawia aplikacji hello środki utrzymania długotrwałe sesji. Co oznacza aplikacji monitują wielokrotnie hello użytkownika podczas uzyskiwania tokenów dostępu dla nowych zasobów.

Jeśli tworzysz aplikację sieci Web, w tym wewnętrznej bazie danych i korzystanie z interfejsu API z jego kod zaplecza przepływu niejawnego hello również nie jest odpowiedni. Inne przyznaje nadaj znacznie więcej możliwości. Na przykład przyznania poświadczeń klienta hello OAuth2 zapewnia hello możliwości tooobtain tokeny odzwierciedlające hello uprawnienia przypisane toohello samej aplikacji, jako min. toouser delegowania. Oznacza to, że klient hello ma hello możliwości toomaintain dostęp programistyczny tooresources nawet wtedy, gdy użytkownik jest aktywnie niezaangażowanych w sesji i tak dalej. Nie tylko który, ale takie przyznaje nadać wyższy gwarancje bezpieczeństwa. Na przykład tokeny dostępu nigdy nie przesyłania za pośrednictwem przeglądarki użytkownika hello, nie ryzyka są zapisywane w historii przeglądarki hello i tak dalej. Aplikacja kliencka Hello można również wykonywać silnego uwierzytelniania podczas żądania tokenu.

## <a name="next-steps"></a>Następne kroki
* Aby zapoznać się z pełną listą zasoby dla deweloperów, protokoły hello i autoryzacji OAuth2 udzielić pomocy technicznej przepływów przez usługę Azure AD, takich jak informacje można znaleźć toohello [przewodnik dewelopera usługi Azure AD][AAD-Developers-Guide]
* Zobacz [jak toointegrate aplikacji z usługą Azure AD] [ ACOM-How-To-Integrate] dla dodatkowych głębokość na proces integracji aplikacji hello.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
