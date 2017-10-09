---
title: "aaaSecurity zagadnienia dotyczące serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje zagadnienia dotyczące zabezpieczeń dla przy użyciu serwera Proxy aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Zagadnienia dotyczące zabezpieczeń w celu uzyskania dostępu do aplikacji zdalnie z serwera Proxy aplikacji usługi Azure AD

W tym artykule opisano, jak serwer Proxy usługi Azure Active Directory aplikacji udostępnia usługa bezpiecznego publikowania i zdalny dostęp do aplikacji.

powitania po diagramie przedstawiono sposób usługi Azure AD umożliwia aplikacji lokalnych tooyour bezpieczny dostęp zdalny.

 ![Diagram bezpieczny dostęp zdalny za pośrednictwem serwera Proxy aplikacji usługi Azure AD](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Korzyści w zakresie zabezpieczeń

Serwer Proxy aplikacji usługi Azure AD oferują hello następujące korzyści w zakresie zabezpieczeń:

### <a name="authenticated-access"></a>Uwierzytelniony dostęp 

Jeśli toouse usługi Azure Active Directory wstępnego uwierzytelniania, następnie tylko uwierzytelnionego połączenia można uzyskać dostęp do sieci.

Serwer Proxy aplikacji usługi Azure AD zależy od hello Azure AD usługi tokenu zabezpieczającego (STS) do wszystkich uwierzytelniania.  Wstępnego uwierzytelniania, ze swej natury blokuje znaczących anonimowe ataki, ponieważ tylko uwierzytelnionych tożsamości można uzyskać dostępu do aplikacji zaplecza hello.

Jeśli wybierzesz Passthrough jako metody uwierzytelniania wstępnego nie pobieraj takich korzyści. 

### <a name="conditional-access"></a>Dostęp warunkowy

Zastosowanie bardziej zaawansowane funkcje kontroli zasad przed tooyour sieciowe są wyznaczane połączenia.

Z [dostępu warunkowego](active-directory-conditional-access-azuread-connected-apps.md), można zdefiniować ograniczenia w jaki ruch jest dozwolony tooaccess aplikacji zaplecza. Można utworzyć zasady, które ograniczają logowania na podstawie lokalizacji, siły uwierzytelniania i profil użytkownika ryzyka.

Umożliwia także zasady dostępu warunkowego tooconfigure uwierzytelnianie wieloskładnikowe, dodając kolejną warstwę zabezpieczeń tooyour użytkownika uwierzytelnienia. 

### <a name="traffic-termination"></a>Zakończenie ruchu

Cały ruch zakończeniem w chmurze hello.

Ponieważ serwera Proxy aplikacji usługi Azure AD jest wstecznego serwera proxy, wszystkie aplikacje tooback-end ruchu jest kończona na powitania usługi. Witaj sesji można pobrać przywróciła tylko z serwerem zaplecza hello, co oznacza, że serwery zaplecza nie są widoczne ruchu toodirect HTTP. Ta konfiguracja oznacza lepszej ochrony przed atakami ukierunkowanymi.

### <a name="all-access-is-outbound"></a>Dostęp jest wychodzący 

Nie trzeba tooopen sieci firmowej toohello połączeń przychodzących.

Łączniki serwera Proxy aplikacji należy używać tylko połączeń wychodzących toohello usługi Azure AD serwera Proxy aplikacji usługi, co oznacza, że nie jest konieczne tooopen portów zapory dla połączeń przychodzących. Serwery proxy tradycyjnych wymagane sieci obwodowej (znanej także jako *DMZ*, *strefą zdemilitaryzowaną*, lub *podsiecią ekranowaną*) i dozwolone toounauthenticated dostępu połączenia na krawędzi sieci hello. Ten scenariusz wymaga wiele dodatkowych inwestycji w aplikacji sieci web zapory ruchu tooanalyze produktów, a oferują dodanie ochrony toohello środowiska. Przy użyciu serwera Proxy aplikacji nie wymagają sieci obwodowej, ponieważ wszystkie połączenia są wychodzących i odbywać za pośrednictwem bezpiecznego kanału.

Aby uzyskać więcej informacji na temat łączników, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Analizy skali chmury i uczenia maszynowego 

Pobierz najnowocześniejsze zabezpieczenia.

Ponieważ jest częścią usługi Azure Active Directory, mogą korzystać z serwera Proxy aplikacji [Azure AD Identity Protection](active-directory-identityprotection.md), machine learning-driven analizy i danych z hello Microsoft Security Response Center i jednostki. Razem możemy aktywne identyfikowanie złamany kont i zapewniają ochronę w czasie rzeczywistym z logowania o wysokim ryzyku. Firma Microsoft uwzględniać wiele czynników, takich jak dostęp z zainfekowanych urządzeń przez nadanie sieci i lokalizacje nietypowe i prawdopodobne.

Wiele z tych raportów i zdarzenia są już dostępne za pośrednictwem interfejsu API dla integracji z informacji o zabezpieczeniach i systemami zarządzania (SIEM) zdarzenia.

### <a name="remote-access-as-a-service"></a>Dostęp zdalny w trybie usługi

Nie masz tooworry o zachowaniu i stosowanie poprawek serwerów lokalnych.

Konta nadal atakowany oprogramowania dla dużej liczby ataków. Serwer Proxy aplikacji usługi Azure AD jest usługi Internet skalowania, która jest właścicielem firmy Microsoft, dzięki czemu zawsze uzyskać hello najnowsze poprawki zabezpieczeń i aktualizacje.

tooimprove hello zabezpieczeń aplikacji opublikowanych przez serwer Proxy aplikacji usługi Azure AD, możemy zablokować robotów przez przeszukiwarkę sieci web do indeksowania i archiwizowania aplikacji. Zawsze robota przez przeszukiwarkę sieci web próbuje pobrać ustawienia robota opublikowanej aplikacji, serwer Proxy aplikacji odpowiedzi z plikiem robots.txt, która obejmuje `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Pod maską hello

Serwer Proxy aplikacji usługi Azure AD składa się z dwóch części:

* Witaj w usłudze w chmurze: ta usługa działa na platformie Azure i jest, gdzie powitania klienta/użytkownika zewnętrznego połączenia są nawiązywane.
* [Witaj łącznika lokalnego](application-proxy-understand-connectors.md): składnik lokalnego łącznika hello nasłuchuje żądań z usługi Serwer Proxy aplikacji hello Azure AD i obsługuje połączenia toohello wewnętrznych aplikacji. 

Przepływ między hello łącznika i usługę serwera Proxy aplikacji hello jest ustanawiane po:

* Łącznik Hello jest najpierw skonfigurować.
* Łącznik Hello pobiera informacje o konfiguracji na powitania serwera Proxy aplikacji usługi.
* Użytkownik uzyskuje dostęp do opublikowanej aplikacji.

>[!NOTE]
>Cała komunikacja odbywa się za pośrednictwem protokołu SSL, a pochodzą zawsze na powitania toohello łącznika serwera Proxy aplikacji usługi. Usługa Hello jest tylko ruchu wychodzącego.

Łącznik Hello używa toohello tooauthenticate certyfikatu klienta usługi Serwer Proxy aplikacji dla prawie wszystkich połączeń. Hello tylko wyjątek toothis proces jest hello kroku konfiguracji początkowej, której certyfikat klienta na powitania zostanie nawiązane.

### <a name="installing-hello-connector"></a>Instalowanie łącznika hello

Jeśli najpierw skonfigurowano łącznik hello hello następujących zdarzeń przepływu miejsce:

1. Usługa toohello rejestracji łącznika Hello odbywa się w ramach instalacji hello hello łącznika. Użytkownicy są tooenter zostanie wyświetlony monit o ich poświadczeń administratora usługi Azure AD. Token z tego uwierzytelnienia zostanie przedstawiony toohello usługi serwera Proxy aplikacji usługi Azure AD.
2. powitania serwera Proxy aplikacji usługi oblicza hello tokenu. Zapewnia hello użytkownik jest administratorem firmy, w ramach dzierżawy hello, który hello token został wystawiony dla. Jeśli użytkownik hello nie jest administratorem, hello proces zostanie zakończony.
3. Łącznik Hello generuje żądanie certyfikatu klienta i przekazuje je, wraz z tokenu, toohello powitania serwera Proxy aplikacji usługi. Usługa Hello z kolei weryfikuje hello token i podpisuje żądanie certyfikatu powitania klienta.
4. Łącznik Hello korzysta z certyfikatu klienta hello przyszłych komunikacji z powitania serwera Proxy aplikacji usługi.
5. Łącznik Hello wykonuje początkowej ściągania danych konfiguracji systemu hello z hello usługi za pomocą swojego certyfikatu klienta, a jest teraz gotowy tootake żądań.

### <a name="updating-hello-configuration-settings"></a>Aktualizowanie ustawień konfiguracji hello

Zawsze, gdy usługa serwera Proxy aplikacji hello aktualizuje ustawienia konfiguracji hello, hello następujących zdarzeń przepływu miejsce:

1. Łącznik Hello łączy punktu końcowego konfiguracji toohello w powitania serwera Proxy aplikacji usługi za pomocą swojego certyfikatu klienta.
2. Po zweryfikowaniu certyfikat klienta na powitania powitania serwera Proxy aplikacji usługi zwraca łącznik toohello danych konfiguracji (na przykład grupy łącznika hello hello łącznik powinien być częścią).
3. Jeśli bieżący certyfikat hello jest więcej niż 180 dni, łącznik hello generuje żądania nowego certyfikatu, które skutecznie aktualizuje certyfikat klienta na powitania raz na 180 dni.

### <a name="accessing-published-applications"></a>Uzyskiwanie dostępu do opublikowanych aplikacji

Gdy użytkownicy uzyskują dostęp do opublikowanej aplikacji, hello następujące zdarzenia miejsce między usługą Serwer Proxy aplikacji hello i łącznika serwera Proxy aplikacji hello:

1. [Usługa Hello uwierzytelnia użytkownika hello aplikacji hello](#the-service-checks-the-configuration-settings-for-the-app)
2. [Usługa Hello umieszcza żądania w kolejce łącznika hello](#The-service-places-a-request-in-the-connector-queue)
3. [Łącznik przetworzy żądanie hello z kolejki hello](#the-connector-receives-the-request-from-the-queue)
4. [Łącznik Hello czeka na odpowiedź](#the-connector-waits-for-a-response)
5. [Witaj usługi strumieni danych toohello użytkownika](#the-service-streams-data-to-the-user)

Zachowaj odczytu toolearn więcej informacji na temat co ma miejsce w każdej z tych kroków.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. Witaj usługa uwierzytelnia użytkownika hello aplikacji hello

Jeśli toouse aplikacji hello Passthrough jest skonfigurowany jako metody uwierzytelniania wstępnego, są pomijane kroki hello w tej sekcji.

Jeśli toopreauthenticate aplikacji hello jest skonfigurowany z usługą Azure AD, użytkownicy są przekierowane toohello tooauthenticate STS usługi Azure AD i hello następujące kroki została wykonana:

1. Serwer Proxy aplikacji sprawdza, czy wszystkie wymagania dotyczące zasad dostępu warunkowego dla określonej aplikacji hello. Ten krok zapewnia, że użytkownik hello przypisano toohello aplikacji. Jeśli wymagana jest weryfikacja dwuetapowa, hello uwierzytelniania sekwencji monituje użytkownika hello drugiej metody uwierzytelniania.

2. Po upływie wszystkie testy, hello Zabezpieczającego usług Azure AD wystawia token podpisanej aplikacji hello i przekierowuje hello toohello wstecz użytkownika serwera Proxy aplikacji usługi.

3. Serwer Proxy aplikacji sprawdza, czy hello token został wystawiony toocorrect hello aplikacji. Wykonuje także inne kontrole, takich jak zapewnienie, że hello token został podpisany przez usługę Azure AD i że jest nadal okna hello prawidłowe.

4. Serwer Proxy aplikacji ustawia tooindicate pliku cookie uwierzytelniania szyfrowanego wystąpienia aplikacji toohello uwierzytelniania. Hello pliku cookie zawiera znacznik czasu wygaśnięcia, oparty na powitania token z usługi Azure AD i innych danych, takie jak nazwa użytkownika hello hello uwierzytelniania jest oparta na. Witaj plik cookie jest zaszyfrowany przy użyciu klucza prywatnego znane toohello serwera Proxy aplikacji usługi.

5. Aplikacji serwera Proxy przekierowania hello użytkownika wstecz toohello pierwotnie żądanego adresu URL.

W przypadku niepowodzenia dowolną część hello kroki wstępnego uwierzytelniania użytkownika hello żądanie zostanie odrzucone i użytkownika hello jest wyświetlany komunikat informujący o hello źródłem problemu hello.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. hello usługi umieszcza żądania w kolejce łącznika hello

Łączniki Zachowaj toohello otwarte połączenia wychodzącego serwera Proxy aplikacji usługi. Gdy nadejdzie żądanie, usługi hello kolejkuje Żądanie hello na jednym z hello otwarte połączenia dla toopick łącznika hello w górę.

Żądanie hello zawiera elementy z aplikacji hello, takich jak nagłówki żądania hello, dane z pliku cookie hello zaszyfrowane, hello użytkownika hello żądanie i co hello żądań identyfikatora. Mimo że danych z zaszyfrowanego pliku cookie hello są wysyłane z żądaniem hello, nie jest hello uwierzytelniania samego pliku cookie.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. hello łącznika przetwarza żądanie hello z hello kolejki. 

Na podstawie hello żądania, serwer Proxy aplikacji wykonuje jeden z hello następujące akcje:

* Jeśli Żądanie hello jest prostą operacją (na przykład, Brak danych w treści hello, ponieważ jest z RESTful *UZYSKAĆ* żądania), łącznik hello sprawia, że połączenie toohello wewnętrzny zasób docelowy i czeka na odpowiedź.

* Jeśli Żądanie hello ma danych skojarzonych z nim w treści hello (na przykład RESTful *POST* operacji), łącznik hello ustanawia wychodzące połączenie przy użyciu powitania klienta certyfikatu toohello serwera Proxy aplikacji wystąpienia. Sprawia, że te dane hello toorequest połączenia, a otworzyć zasobu wewnętrznego toohello połączenia. Po otrzymaniu żądania hello z hello łącznika usługi Serwer Proxy aplikacji hello zaczyna akceptować zawartości z hello użytkownika i przekazuje łącznik toohello danych. Łącznik Hello przekazuje z kolei hello zasobu wewnętrznego toohello danych.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. łącznik hello czeka na odpowiedź.

Po hello żądań i przekazywanie toohello całą zawartość kopii end została ukończona, łącznik hello czeka na odpowiedź.

Po otrzymaniu odpowiedzi łącznika hello sprawia, że usługi serwera Proxy aplikacji toohello wychodzące połączenie, tooreturn hello szczegółów nagłówka i rozpocząć przesyłanie strumieniowe hello zwracanych danych.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. użytkownik toohello hello usługi strumieni danych. 

Przetwarza aplikacji hello może występować w tym miejscu. Jeśli skonfigurowano serwer Proxy aplikacji tootranslate nagłówków i adresy URL w aplikacji, przetwarzanie odbywa się zgodnie z potrzebami w tym kroku.


## <a name="next-steps"></a>Następne kroki

[Zagadnienia dotyczące topologii sieci przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-network-topology-considerations.md)

[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
