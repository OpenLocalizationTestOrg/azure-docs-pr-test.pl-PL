---
title: "CENC z wieloma DRM i kontrolą dostępu: odwołanie do projektu i wdrożenia na platformie Azure i usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toolicensing hello Microsoft® Smooth Streaming klienta Eksportowanie zestawu."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>Szyfrowanie CENC przy użyciu technologii Multi-DRM i kontroli dostępu: odwołanie do projektowania i implementacji na platformie Azure i w usłudze Azure Media Services
 
## <a name="introduction"></a>Wprowadzenie
Należy dobrze znany jest toodesign złożonych zadań i tworzenie Podsystem DRM dla OTT lub w trybie online, rozwiązań do przesyłania strumieniowego. I jest wspólny rozwiązaniem dla operatorów/online toooutsource dostawców wideo tej części toospecialized DRM usługodawców. Hello celem niniejszego dokumentu jest toopresent odwołanie do projektu i implementacji w OTT lub online rozwiązania do przesyłania strumieniowego podsystemu DRM end-to-end.

czytniki Hello celem tego dokumentu są Inżynierowie pracujący w podsystemie DRM OTT online przesyłania strumieniowego/kilku-screen rozwiązania lub dowolnego czytników zainteresowane w podsystemie DRM. Hello zakłada się, że czytników zapoznali się z co najmniej jednej z technologii DRM hello na rynku hello, takich jak PlayReady i Widevine, FairPlay Adobe dostępu.

Przez DRM będziemy również obejmować (Common Encryption) CENC z wieloma DRM. Główne trendu w online przesyłania strumieniowego oraz z branży OTT jest toouse CENC z kilku-native DRM na różnych platformach klienckich, jest shift z poprzednich trend hello przy użyciu pojedynczego DRM i zestawu SDK klienta dla różnych platform klienta. Jeśli używasz CENC z kilku native DRM, zarówno PlayReady i Widevine są szyfrowane na powitania [Common Encryption (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) specyfikacji.

Witaj zalet CENC z wieloma DRM są następujące:

1. Zmniejsza koszt, ponieważ przetwarzanie pojedynczego szyfrowania jest używany przeznaczonych dla różnych platform z jego DRMs natywnego; szyfrowania
2. Zmniejsza koszt hello zarządzanie zasobami zaszyfrowane, ponieważ jest wymagana tylko jednej kopii zaszyfrowanych zasoby;
3. Eliminuje licencjonowania koszt, ponieważ aplikacja native client DRM hello jest zwykle wolnego miejsca na jego natywnego platformy klientów DRM.

Microsoft została active promotor kreska i CENC wraz z niektórych odtwarzaczy branży głównych. Microsoft Azure Media Services obsługiwał obsługę kreska i CENC. Ostatnie anonsów, zobacz Mingfei w blogach: [usług dostarczania licencji Announcing Google Widevine w usłudze Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/), i [usługi Azure Media Services dodaje tworzenia pakietów Google Widevine dostarczania strumienia wieloma DRM](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Informacje w tym artykule
Celem Hello w tym artykule obejmuje następujące hello:

1. Zawiera odwołanie do projektu podsystemu DRM przy użyciu CENC z wieloma DRM;
2. Udostępnia implementację odwołania na platformie Microsoft Azure/usługi Azure Media Services;
3. W tym artykule omówiono niektóre tematy projekt i implementację.

W artykule Witaj "wieloma DRM" obejmuje następujące hello:

1. Microsoft PlayReady
2. Google Widevine
3. FairPlay firmy Apple 

Witaj Poniższa tabela zawiera podsumowanie hello aplikacji natywnych platformy lub natywne i przeglądarek obsługiwanych przez każdy DRM.

| **Platforma klienta** | **Obsługa natywnego DRM** | **Przeglądarka/aplikacji** | **Formatów przesyłania strumieniowego** |
| --- | --- | --- | --- |
| **Inteligentne telewizorach, operator odbiornikami, odbiornikami OTT** |PlayReady przede wszystkim i/lub Widevine i/lub innych |Linux, Opera, WebKit, innych |Różne formaty. |
| **Urządzenia z systemem Windows 10 (komputera z systemem Windows, tablety z systemem Windows, Windows Phone, Xbox)** |PlayReady |MS krawędzi/IE11/EME<br/><br/><br/>PLATFORMY UNIWERSALNEJ SYSTEMU WINDOWS |DASH (dla protokołu HLS, PlayReady nie jest obsługiwane)<br/><br/>DASH, Smooth Streaming (HLS dla, PlayReady nie jest obsługiwane) |
| **Urządzenia z systemem android (telefon i Tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), OS X, klientów i Apple TV** |FairPlay |Safari 8 +/ EME |HLS |


Biorąc pod uwagę hello bieżący stan wdrożenia dla każdego DRM, usługi będą zazwyczaj toomake DRMs tooimplement 2 lub 3 się, że adres wszystkie typy hello punktów końcowych w hello najlepsze sposób.

Zależności między złożoności hello hello usługi logiki i złożoności hello na powitania klienta po stronie tooreach poziom użytkownika doświadczenia w hello różnych klientów.

toomake wybór, należy uwzględnić następujące kwestie następujące fakty:

* PlayReady natywnie jest zaimplementowana w każde urządzenie z systemem Windows, na niektórych urządzeniach z systemem Android i dostępne za pośrednictwem zestawów SDK oprogramowania w praktycznie dowolnej platformie
* Natywnie zaimplementowano Widevine, każde urządzenie z systemem Android, Chrome i niektóre inne urządzenia
* FairPlay jest dostępna tylko w systemach iOS i Mac OS klientów lub za pomocą programu iTunes.

Dlatego typowe wieloma DRM mogą być następujące:

* Opcja 1: PlayReady i Widevine
* Opcja 2: PlayReady i Widevine FairPlay

## <a name="a-reference-design"></a>Odwołanie do projektu
W tej sekcji możemy przedstawić projekt odwołania, który jest niezależny tootechnologies używane tooimplement go.

Podsystem DRM może zawierać hello następujące składniki:

1. Zarządzanie kluczami
2. OPAKOWYWANIE DRM
3. Dostarczanie licencji DRM
4. Sprawdź uprawnienia
5. Uwierzytelniania/autoryzacji
6. Player
7. Pochodzenie/CDN

Witaj poniższym diagramie przedstawiono hello wysokiego poziomu interakcji między składnikami hello w podsystemie DRM.

![Podsystem DRM z CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Istnieją trzy podstawowe "warstwy" w projekcie hello:

1. Warstwa zaplecza (w kolorze czarnym), które nie są widoczne na zewnątrz;
2. Warstwa "DMZ" (niebieski) zawierający wszystkie hello punkty końcowe skierowane publicznych;
3. Publiczny Internet warstwę (niebieski światła) zawierającą CDN i odtwarzacze z ruchem w publicznej sieci Internet.

Powinien być narzędziem do zarządzania zawartością kontrolowania ochrony DRM, niezależnie od szyfrowania statyczne lub dynamiczne. dane wejściowe Hello szyfrowania DRM powinna zawierać:

1. Zawartość wideo MBR;
2. Klucz zawartości;
3. Adresy URL pozyskiwania licencji.

Podczas odtwarzania hello wysokiego poziomu przebieg jest:

1. Użytkownik jest uwierzytelniony;
2. Token autoryzacji jest tworzony dla użytkownika hello;
3. Zawartość DRM chronione (manifest) jest pobrany tooplayer;
4. Odtwarzacz przesyła serwerów toolicense żądania nabycie licencji wraz z klucza identyfikator i autoryzacji tokenu.

Przed przenoszenie toohello następnego tematu kilka słów na temat hello projekt zarządzania kluczami.

| **ContentKey — zasobów** | **Scenariusz** |
| --- | --- |
| 1 – 1 |najprostszym przypadku Hello. Zapewnia on hello Najdrobniejsze formantu. Jednak to zazwyczaj wynikiem hello najwyższy koszt dostarczania licencji. W minimalnej jedną licencję żądania jest wymagana dla każdego chronionego zasobu. |
| 1-do wielu |Można użyć hello zawartości klucza dla wielu zasobów. Na przykład dla wszystkich zasobów hello w grupę logiczną, takie jak genre lub podzbiór genre (lub gen film), można użyć jednego klucza zawartości. |
| Wiele do-1 |Wiele kluczy zawartości są wymagane dla każdego zasobu. <br/><br/>Na przykład jeśli potrzebujesz tooapply dynamicznej ochrony CENC z wieloma DRM MPEG DASH i dynamicznego szyfrowania AES-128 dla protokołu HLS należy dwa osobne klucze zawartości, każdy z własną ContentKeyType. (Używana na potrzeby dynamicznej CENC ochrony klucza zawartości hello, ContentKeyType.CommonEncryption należy używać, natomiast w przypadku zawartości, powinien zostać użyty klucz używany do dynamicznego szyfrowania AES-128, ContentKeyType.EnvelopeEncryption hello.)<br/><br/>Inny przykład DASH CENC ochrony zawartości, teoretycznie, jeden klucz zawartości mogą być używane tooprotect strumienia wideo i innej zawartości klucza tooprotect strumieniem audio. |
| Wiele — zbyt wielu |Kombinacja hello powyżej dwóch scenariuszy: jeden zestaw zawartości klucze są używane dla każdego z hello wiele zasobów w hello zasobów tego samego "grupy". |

Innym ważnym czynnikiem tooconsider jest wykorzystanie hello stałe i nietrwałe licencji.

Te zagadnienia są ważne

Mają one bezpośredni wpływ toolicense dostarczania koszt użycie chmury publicznej w celu dostarczania licencji. Zastanówmy hello następujące dwa tooillustrate przypadków projektowania:

1. Miesięczna subskrypcja: Użyj trwałego licencji i 1-do wielu zawartości mapowanie klucz do zasobów. Na przykład wszystkie filmy dzieci hello używamy jednego klucza zawartości do szyfrowania. W takim przypadku:

    Łączna liczba licencji # wymagane dla wszystkich dzieci filmy urządzenia = 1
2. Miesięczna subskrypcja: Użyj nietrwałe licencji i 1-do-1 mapowanie między klucz zawartości i zasobów. W takim przypadku:

    Łączna liczba licencji # wymagane dla wszystkich dzieci filmy urządzenia = [filmy # obserwowane] x [sesji #]

Jak łatwo można zauważyć, powitalne dwóch różnych projektów spowodować licencji bardzo różnią się żądanie dlatego wzorców dostarczania licencji kosztów w przypadku usługi dostarczania licencji przez chmury publicznej, takich jak usługi Azure Media Services.

## <a name="mapping-design-tootechnology-for-implementation"></a>Mapowanie projektu tootechnology dla implementacji
Następnie możemy mapy naszych tootechnologies ogólnego projektu na platformie Microsoft Azure/usługi Azure Media Services, określając toouse technologii, które dla każdego bloku konstrukcyjnego.

Witaj poniższej tabeli przedstawiono hello mapowania:

| **Bloków konstrukcyjnych** | **Technologia** |
| --- | --- |
| **Player** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **Dostawcy tożsamości (IDP)** |Usługa Azure Active Directory |
| **Bezpieczne usługi tokenów (STS)** |Usługa Azure Active Directory |
| **Przepływ pracy ochrony DRM** |Dynamiczne ochrony usługi Azure Media Services |
| **Dostarczania licencji DRM** |1. Usługi Azure Media Services licencji dostarczania (PlayReady i Widevine, FairPlay), lub <br/>2. Serwer licencji Axinom <br/>3. Serwer licencji PlayReady niestandardowych |
| **Punkt początkowy** |Punkt końcowy przesyłania strumieniowego usługi Azure Media Services |
| **Zarządzanie kluczami** |Nie jest wymagane dla implementacji |
| **Zarządzanie zawartością** |Aplikacji konsolowej C# |

Innymi słowy zarówno dostawcy tożsamości (IDP) i Secure Token Service (STS) będzie usługi Azure AD. Dla odtwarzacza, użyjemy [interfejsu API usługi Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). Zarówno usługi Azure Media Services, jak i usługi Azure Media Player obsługuje kreska i CENC z wieloma DRM.

powitania po diagramie przedstawiono hello ogólną strukturę i przepływ z hello powyżej technologii mapowania.

![CENC na AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

W kolejności tooset dynamiczne szyfrowanie CENC narzędzie do zarządzania zawartością hello użyje hello następujące dane wejściowe:

1. Otwórz zawartość;
2. Klucz zawartości z klucza generowania i zarządzania nimi;
3. Adresy URL pozyskiwania licencji;
4. Lista informacji z usługi Azure AD.

Witaj dane wyjściowe narzędzia do zarządzania zawartością hello będą:

1. ContentKeyAuthorizationPolicy zawierający specyfikacji hello na sposób dostarczania licencji weryfikuje JWT token i specyfikacji licencji DRM.
2. AssetDeliveryPolicy zawierający specyfikacje na format, ochrony DRM i adresy URL pozyskiwania licencji przesyłania strumieniowego.

W czasie wykonywania, przepływ hello jest jak poniżej:

1. Podczas uwierzytelniania użytkownika zostanie wygenerowany JWT token;
2. Jednym z hello oświadczeń zawartych w hello JWT token jest "grupy" oświadczenie zawierające Identyfikatora obiektu grupy hello "EntitledUserGroup". To oświadczenie będzie służyć do przekazywania "Sprawdź uprawnienia".
3. Pliki do pobrania odtwarzacz klienta manifest CENC zawartości chronionej i "widzi" hello poniżej:

   1. Identyfikator, klucza
   2. zawartość Hello jest chroniony, CENC
   3. Adresy URL pozyskiwania licencji.
4. Odtwarzacz wysyła żądanie nabycie licencji oparte na powitania przeglądarki/DRM obsługiwane. Żądanie nabycie licencji hello, identyfikator klucza i hello JWT również zostaną przesłane tokenu. Usługi dostarczania licencji zweryfikuje tokenu JWT hello i oświadczenia hello zawierała przed wystawieniem hello potrzebnych licencji.

## <a name="implementation"></a>Wdrażanie
### <a name="implementation-procedures"></a>Procedury implementacji
Implementacja Hello obejmuje hello następujące kroki:

1. Przygotowanie ich testu: kodowanie/pakietów testów wideo toomulti szybkości transmisji bitów pofragmentowany plik MP4 w usłudze Azure Media Services. Ten zasób nie jest chroniony DRM. DRM ochrony zostaną wykonane przez dynamiczne ochrony później.
2. Tworzenie klucza identyfikator i zawartości kluczy (opcjonalnie z klucza inicjatora). W tym przypadku systemem zarządzania kluczami nie jest potrzebna, ponieważ firma Microsoft ma do czynienia z tylko jednego zestawu kluczy identyfikator i klucz zawartości do kilku zasobów testu;
3. Za pomocą interfejsu API usług AMS tooconfigure wieloma DRM licencji dostarczania usług hello testu zasobów. Jeśli używasz serwerów licencji niestandardowych przez firmy lub dostawców firmy zamiast usług licencyjnych w usłudze Azure Media Services, można pominąć ten krok i określ adresy URL pozyskiwania licencji w kroku hello konfigurowania dostarczania licencji. Interfejs API usług AMS jest wymagane toospecify niektóre szczegółowe konfiguracje, takie jak ograniczenia zasad autoryzacji, licencji szablonów odpowiedzi dla różnych usług licencji DRM, itd. W tej chwili hello portalu Azure nie obsługuje jeszcze zapewnić hello potrzebne interfejsu użytkownika dla tej konfiguracji. Można znaleźć informacji o poziomie interfejsu API i przykładowy kod w dokumencie Julia Kornich: [za pomocą PlayReady i Widevine, dynamicznego szyfrowania Common Encryption](media-services-protect-with-drm.md).
4. Użyj zasad dostarczania elementów zawartości tooconfigure interfejsu API usług AMS hello trwałego testu. Można znaleźć informacji o poziomie interfejsu API i przykładowy kod w dokumencie Julia Kornich: [za pomocą PlayReady i Widevine, dynamicznego szyfrowania Common Encryption](media-services-protect-with-drm.md).
5. Tworzenie i konfigurowanie dzierżawy usługi Azure Active Directory w środowisku Azure.
6. Utworzyć kilka grup i kont użytkowników w dzierżawie usługi Azure Active Directory: należy utworzyć co najmniej "EntitledUser" grupy i Dodaj grupę użytkowników toothis. Użytkownicy w tej grupie, przechodzą wyboru uprawnień w nabycie licencji i użytkowników w tej grupie nie powiedzie się uwierzytelnianie toopass i nie będą mogli tooacquire licencji. Bycia członkiem tej grupy "EntitledUser" to oświadczenie wymagane "grupy" hello tokenu JWT wystawione przez usługę Azure AD. To wymaganie oświadczeń powinny być określone w kroku usługi dostarczania licencji DRM wielu Konfigurowanie.
7. Tworzenie aplikacji platformy ASP.NET MVC, która będzie obsługiwać odtwarzacza wideo. Ta aplikacja ASP.NET będą chronione przy użyciu uwierzytelniania użytkownika względem hello dzierżawy usługi Azure Active Directory. Oświadczenia właściwe zostaną uwzględnione w tokenów dostępu hello uzyskane po uwierzytelnieniu użytkownika. Interfejs API OpenID Connect jest zalecane dla tego kroku. Należy hello tooinstall następujące pakiety NuGet:
   * Pakiet instalacyjny Microsoft.Azure.ActiveDirectory.GraphClient
   * Pakiet instalacyjny Microsoft.Owin.Security.OpenIdConnect
   * Pakiet instalacyjny Microsoft.Owin.Security.Cookies
   * Instalacja pakietu Microsoft.Owin.Host.SystemWeb
   * Pakiet instalacyjny Microsoft.IdentityModel.Clients.ActiveDirectory
8. Tworzenie przy użyciu odtwarzacza [interfejsu API usługi Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). [Interfejs API ProtectionInfo Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/) pozwala toospecify toouse technologii DRM, które na innej platformie DRM.
9. Macierzy testów:

| **DRM** | **Przeglądarka** | **Wynik dla prawo użytkownika** | **Wynik nie jest uprawniony użytkownik** |
| --- | --- | --- | --- |
| **PlayReady** |Krawędź MS lub IE11 w systemie Windows 10 |Powiodło się |Niepowodzenie |
| **Widevine** |Chrome w systemie Windows 10 |Powiodło się |Niepowodzenie |
| **FairPlay** |TBD | | |

George Trifonov Azure Media Services zespołu został zapisany blogu udostępnia szczegółowe kroki w procesie konfigurowania usługi Azure Active Directory dla aplikacji ASP.NET MVC player: [integracji Azure Media Services OWIN MVC na podstawie aplikacji w usłudze Azure Active Directory i ograniczenie klucza dostarczania zawartości na podstawie oświadczeń JWT](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George również został zapisany na blogu [JWT token uwierzytelniania w usłudze Azure Media Services i szyfrowania dynamicznego](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). A Oto jego [w integracji usługi Azure AD z usługi Azure Media Services klucza dostawy](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Aby uzyskać informacje dotyczące usługi Azure Active Directory:

* Możesz znaleźć informacje dla deweloperów w [Azure Active Directory przewodnik dewelopera](../active-directory/active-directory-developers-guide.md).
* Można znaleźć informacje o Administratorze w [administrowania Your Azure AD Directory](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Niektóre pytań w implementacji
W implementacji hello istnieją pewne "pytań". Miejmy nadzieję, że następujące listy "pytań" hello ułatwiają rozwiązywanie problemów w przypadku napotkania problemów.

1. **Wystawca** URL powinien kończyć się **"/"**.  

    **Grupy odbiorców** powinny być hello identyfikator klienta aplikacji odtwarzacza i należy również dodać **"/"** na końcu hello hello adres URL wystawcy.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    W [dekodera tokenów JWT](http://jwt.calebb.net/), powinny pojawić się **lub** i **iss** jak poniżej w hello JWT token:

    ![gotcha 1.](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Dodaj uprawnienia toohello aplikacji w usłudze AAD (na karcie Konfiguracja aplikacji hello). Jest to wymagane dla każdej aplikacji (w wersji lokalnej i wdrożone).

    ![gotcha 2](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Użyj wystawcy prawo hello w konfigurowaniu dynamiczne CENC ochrony:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    Witaj następujące działania będą nieprawidłowe:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Hello identyfikator GUID to identyfikator hello AAD dzierżawcy. Witaj identyfikator GUID można znaleźć w menu podręcznym punktów końcowych w portalu Azure.
4. Członkostwo w grupie GRANT oświadczeń uprawnień. Upewnij się, że w pliku manifestu aplikacji usługi AAD, będziemy mieć następujące hello

    "groupMembershipClaims": "All" (wartość domyślna hello ma wartość null)
5. TokenType odpowiednie ustawienie podczas tworzenia wymagania ograniczeń.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Dodawanie obsługi JWT (AAD) dodatkowo tooSWT (ACS), domyślne hello TokenType to TokenType.JWT. Jeśli używasz SWT/ACS, należy ustawić tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Dodatkowe tematy dotyczące implementacji
Następnie firma Microsoft będzie dysk uss niektóre dodatkowe tematy w naszym projektowania i implementacji.

### <a name="http-or-https"></a>HTTP lub HTTPS?
Hello aplikacja odtwarzacza ASP.NET MVC, który budujemy musi spełniać następujące hello:

1. Uwierzytelnianie użytkowników za pomocą usługi Azure AD, którą należy toobe w obszarze protokołu HTTPS.
2. Wymiany tokenu JWT między klientem a usługą Azure AD, wymagający toobe w obszarze protokołu HTTPS.
3. Nabycie licencji DRM przez powitania klienta, co jest wymagane toobe w obszarze HTTPS, jeśli dostarczania licencji są dostarczane przez usługi Azure Media Services. Oczywiście pakiet produktów PlayReady nie wprowadzić HTTPS w celu dostarczania licencji. Jeśli serwer licencji PlayReady znajduje się poza usługi Azure Media Services, można użyć protokołu HTTP lub HTTPS.

W związku z tym hello aplikacja odtwarzacza ASP.NET będzie używać protokołu HTTPS, najlepszym rozwiązaniem. Oznacza to hello Azure Media Player się na stronie w obszarze HTTPS. Niemniej jednak w przypadku przesyłania strumieniowego możemy użyć protokołu HTTP, dlatego potrzebujemy tooconsider mieszanym problem zawartości.

1. Przeglądarka nie zezwala na zawartość mieszana. Ale zezwalaj na wtyczki dodatku Silverlight i OSMF do sprawnego i KRESKI. Zawartość mieszana jest problem dotyczący zabezpieczeń — ze względu na zagrożenie toohello z tooinject możliwości hello złośliwego JS, co może powodować hello toobe danych klienta na ryzyko.  Przeglądarki blokować to domyślnie i wykonanej do tej pory jest hello tylko sposób toowork wokół niego w po stronie serwera (źródło) hello tooallow wszystkich domenach (niezależnie od tego, https lub http). To prawdopodobnie nie jest dobrze albo.
2. Firma Microsoft należy unikać zawartości mieszanej: zarówno za pomocą protokołu HTTP albo oba rozwiązania używają protokołu HTTPS. Podczas odtwarzania zawartości mieszanej techniczna silverlightSS wymaga wyczyszczenia mieszanych ostrzeżenie zawartości. techniczna flashSS obsługuje zawartość mieszaną bez mieszanych ostrzeżenia zawartości.
3. Jeśli punkt końcowy przesyłania strumieniowego został utworzony przed 2014 sierpnia, nie obsługuje protokołu HTTPS. W takim przypadku Utwórz i używać nowego punktu końcowego przesyłania strumieniowego dla protokołu HTTPS.

W implementacji odwołanie hello, dla zawartości DRM chronionych aplikacji i przesyłania strumieniowego będą HTTTPS. Otwórz zawartość hello player nie być konieczne uwierzytelniania lub licencji, dlatego należy hello liberty toouse albo protokołu HTTP lub HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Usługa Azure Active Directory Przerzucanie klucza podpisywania
Jest to ważne tootake punktu pod uwagę implementacji. Jeśli użytkownik nie należy traktować to w implementacji, system ukończyć powitalnych ostatecznie przestaną działać całkowicie w ciągu maksymalnie 6 tygodni.

Usługi Azure AD używa branżowy standard tooestablish zaufania między sobą i aplikacji przy użyciu usługi Azure AD. W szczególności usługi Azure AD używa klucza podpisywania, który składa się z pary kluczy publicznych i prywatnych. W usłudze Azure AD tworzy token zabezpieczający, który zawiera informacje o użytkowniku hello, token ten jest podpisany przez usługę Azure AD przy użyciu jego klucz prywatny, przed wysłaniem wstecz toohello aplikacji. tooverify, który hello token jest prawidłowy i faktycznie zdalnych z usługi Azure AD, aplikacja hello zweryfikować podpisu tokenu hello przy użyciu klucza publicznego hello udostępnianych przez usługi Azure AD, zawarte w dokument metadanych usług federacyjnych hello dzierżawy. Ten publiczny klucz — Witaj, z którego pochodzi klucza podpisywania — jest hello używaną tego samego dla wszystkich dzierżawców w usłudze Azure AD.

Szczegółowe informacje o Przerzucanie klucza usługi Azure AD można znaleźć w dokumencie hello: [ważne informacje dotyczące podpisywania przerzucania klucza w usłudze Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Między hello [pary kluczy publiczno prywatnych](https://login.microsoftonline.com/common/discovery/keys/),

* klucz prywatny Hello jest używany przez usługi Azure Active Directory toogenerate tokenu JWT;
* klucz publiczny Hello jest używany przez aplikację takie jak usługi dostarczania licencji DRM w AMS tooverify hello JWT token;

W celu zabezpieczenia usługi Azure Active Directory obraca tego certyfikatu okresowo (co tydzień). W przypadku naruszenia zabezpieczeń Przerzucanie klucza hello może wystąpić dowolnej chwili. W związku z tym usługi dostarczania licencji hello w AMS należy tooupdate hello klucza publicznego używany jako pary kluczy hello obraca usługi Azure AD, w przeciwnym razie token uwierzytelniania w AMS zakończy się niepowodzeniem i pojawi się żadna licencja.

Jest to osiągane przez ustawienie TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument podczas konfigurowania usług dostarczania licencji DRM.

Hello przepływu tokenu JWT jest poniżej:

1. Usługi Azure AD wystawia hello JWT token hello bieżącego klucza prywatnego dla użytkowników uwierzytelnionych;
2. Gdy odtwarzacza widzi CENC z wieloma DRM chroniona zawartość, najpierw zlokalizuje hello tokenu JWT wystawione przez usługę Azure AD.
3. Odtwarzacz Hello wysyła żądanie nabycie licencji z usługi dostarczania toolicense tokenu JWT hello w AMS;
4. Witaj usług dostarczania licencji w AMS użyje hello bieżącego/prawidłowy klucz publiczny z tokenu JWT hello tooverify usługi Azure AD, przed wystawieniem licencji.

Będzie można zawsze sprawdzanie usług dostarczania licencji DRM hello bieżącego/prawidłowy klucz publiczny z usługi Azure AD. klucz publiczny Hello przedstawiony przez usługę Azure AD będzie hello klucz używany do weryfikowania tokenu JWT wystawione przez usługę Azure AD.

Co zrobić, jeśli Przerzucanie klucza hello się stanie po AAD generuje JWT token, ale przed hello JWT token jest wysyłany przez odtwarzacze tooDRM usług dostarczania licencji w AMS na potrzeby weryfikacji?

Ponieważ klucz mogła zostać wycofana w dowolnym momencie, jest zawsze więcej niż jeden prawidłowy klucz publiczny dostępna hello dokument metadanych usług federacyjnych. Azure dostarczania licencji Media Services można użyć dowolnego z hello określić klucze w dokumencie hello, ponieważ jeden klucz mogła zostać wycofana wkrótce innego mogą być zastąpienia i tak dalej.

### <a name="where-is-hello-access-token"></a>Gdzie jest hello tokenu dostępu?
Jeśli przyjrzymy się jak aplikacji sieci web wywołuje aplikację interfejsu API w obszarze [tożsamość aplikacji z OAuth 2.0 klienta poświadczenia Grant](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), przepływ uwierzytelniania hello jest poniżej:

1. Użytkownik jest zalogowany tooAzure AD w aplikacji sieci web hello (zobacz hello [tooWeb przeglądarki sieci Web aplikacji](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. punkt końcowy autoryzacji Hello Azure AD przekierowuje hello aplikacji klienckiej wstecz toohello agenta użytkownika z kodem autoryzacji. agent użytkownika Hello zwraca identyfikator URI przekierowania autoryzacji kodu toohello aplikacji klienckiej.
3. Aplikacja sieci web Hello musi tooacquire tokenu dostępu, który można uwierzytelnić interfejsu API sieci web toohello i pobrać hello żądanego zasobu. Powoduje to dodanie tooAzure żądania AD dla punktu końcowego tokena, hello poświadczeń, identyfikator klienta i aplikacji sieci web interfejsu API identyfikator URI. Przedstawia tooprove kod autoryzacji hello tego hello użytkownik zgodził.
4. Usługi Azure AD uwierzytelnia aplikacji hello i zwraca token dostępu JWT jest interfejs API sieci web hello toocall używane.
5. Przy użyciu protokołu HTTPS aplikacja sieci web hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.

W tym przepływie "tożsamość aplikacji" hello interfejsu API sieci web ufa tego hello sieci web aplikacji hello uwierzytelnionego użytkownika. Z tego powodu ten wzorzec jest wywoływana zaufany podsystem. Witaj [diagramu na tej stronie](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) w tym artykule opisano, jak kod autoryzacji przyznać przepływ działania.

W nabycie licencji z ograniczenia tokenu, możemy po hello tego samego wzorca zaufany podsystem. I usługi dostarczania licencji hello w usłudze Azure Media Services jest hello zasobu interfejsu API sieci web, hello "zasobu wewnętrznej bazy danych" tooaccess wymaga aplikacji sieci web. Dlatego w przypadku hello tokenu dostępu?

Firma Microsoft są w rzeczywistości uzyskiwania tokenu dostępu z usługi Azure AD. Po uwierzytelnieniu użytkownik pomyślnie zostanie zwrócony kod autoryzacji. Kod autoryzacji Hello jest następnie używany razem z identyfikator i aplikacji klucz klienta, tooexchange tokenu dostępu. I token dostępu hello dla uzyskiwania dostępu do aplikacji "wskaźnik" wskazuje lub reprezentujący usługi dostarczania licencji usługi Azure Media Services.

Firma Microsoft muszą tooregister i skonfigurować aplikację "wskaźnik" hello w usłudze Azure AD, wykonując poniższe kroki hello:

1. W dzierżawie powitalnych usługi Azure AD

   * Dodawanie aplikacji (zasobów) z adresem URL logowania:

   https://[resource_name].azurewebsites.NET/ i

   * adres URL Identyfikatora aplikacji:

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Dodaj nowy klucz hello zasobów aplikacji;
3. Aktualizacja pliku manifestu aplikacji hello tak, aby właściwość groupMembershipClaims hello hello następujące wartości: "groupMembershipClaims": "Wszystkie",  
4. W aplikacji usługi Azure AD hello wskazanie toohello aplikacji sieci web player, w sekcji hello "aplikacje tooother uprawnienia" Dodaj hello zasobów aplikacji, która została dodana w kroku 1. Sprawdź znacznik "Dostępu [resource_name]" w obszarze "delegowane uprawnienia". Daje to uprawnienia aplikacji sieci web hello toocreate tokenów dostępu do uzyskiwania dostępu do hello zasobów aplikacji. Ten krok należy wykonać dla wersji zarówno lokalnych, jak i wdrożonej aplikacji sieci web hello Jeśli tworzysz aplikację sieci web programu Visual Studio i platformy Azure.

W związku z tym hello tokenu JWT wystawione przez usługę Azure AD jest token dostępu hello dla uzyskiwania dostępu do tego zasobu "wskaźnik".

### <a name="what-about-live-streaming"></a>Jak Live przesyłania strumieniowego?
W powyższym hello naszych dyskusji ma zostały koncentrujących się na zasoby na żądanie. Jak transmisja strumieniowa na żywo?

Witaj szczęście jest której można dokładnie hello sam projekt i implementację ochrony transmisja strumieniowa na żywo w usłudze Azure Media Services, traktując zasobów hello skojarzonego z programem jako zasób"VOD".

W szczególności jest dobrze znanych czy toodo live streaming w usłudze Azure Media Services, należy toocreate kanał, a następnie program hello kanału. toocreate hello program, należy toocreate zasób będzie zawierać hello na żywo archiwum hello programu. W kolejności tooprovide CENC z wieloma DRM ochrony zawartości na żywo hello, wszystko, czego potrzebujesz toodo, jest tooapply hello tego samego zasobu toohello instalacji/przetwarzania tak, jakby było "zasobów VOD" przed rozpoczęciem powitalne program.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Co serwerów licencji poza usługi Azure Media Services?
Często klienci mogą zainwestowały w licencji farmy serwerów jest w ich własnych danych Centrum lub hostowanej przez dostawców usług DRM. Na szczęście ochrony zawartości Azure Media Services umożliwia toooperate w trybie hybrydowego: zawartości hostowanej i dynamicznie chroniony w usłudze Azure Media Services, podczas gdy licencji DRM są dostarczane przez serwery poza usługi Azure Media Services. W tym przypadku są hello następujące zagadnienia dotyczące zmian:

1. Hello Secure Token Service musi tooissue tokeny są akceptowane i można sprawdzić w farmie serwerów licencji hello. Na przykład serwerów licencji Widevine hello udostępnionych przez Axinom wymaga określonych token JWT, zawierający "uprawnienie komunikat". W związku z tym należy toohave tooissue STS takie tokenu JWT. Autorzy Hello zakończył takie implementację i hello szczegółowe informacje można znaleźć w powitania po dokumentu w [Centrum dokumentacji platformy Azure](https://azure.microsoft.com/documentation/): [toodeliver przy użyciu Axinom Widevine licencje tooAzure Media Services](media-services-axinom-integration.md).
2. Usługi dostarczania licencji tooconfigure (ContentKeyAuthorizationPolicy) w usłudze Azure Media Services nie są już potrzebne. Co należy toodo jest adresy URL pozyskiwania licencji hello tooprovide (w przypadku PlayReady i Widevine FairPlay) podczas konfigurowania AssetDeliveryPolicy z konfigurowaniem CENC z wieloma DRM.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>Co zrobić, jeśli ma toouse STS niestandardowych?
Może istnieć kilka przyczyn, które klient może wybrać toouse niestandardowych STS (Secure Token Service) udostępnia tokenów JWT. Niektóre z nich są:

1. Witaj dostawcy tożsamości (IDP) używany przez powitania klienta nie obsługuje usługi STS. W takim przypadku niestandardowych STS może być opcję.
2. powitania klienta może być konieczne bardziej elastyczne lub zwiększenie poziomu kontroli w integracji usługi STS z systemem rozliczeniowym subskrybenta klienta. Na przykład MVPD operator mogą oferować wielu pakietów subskrybenta OTT, takie jak sportowy — wersja premium, podstawowa, operator hello itp. może być toomatch hello oświadczenia do tokenu z pakietem subskrybenta, tak aby tylko zawartości w pakiecie prawo hello jest udostępniana. W takim przypadku niestandardowych STS zawiera hello potrzebne elastyczność i kontrolę.

Dwie zmiany należy toobe podjęta, gdy przy użyciu niestandardowych STS:

1. Podczas konfigurowania usługi dostarczania licencji dla zasobu, należy klucz zabezpieczeń hello toospecify używany do weryfikacji przez hello niestandardowych STS (więcej szczegóły poniżej) zamiast hello bieżącego klucza z usługi Azure Active Directory.
2. Po wygenerowaniu tokenu JTW klucza zabezpieczeń określono zamiast hello klucza prywatnego certyfikatu hello bieżącego X509 w usłudze Azure Active Directory.

Istnieją dwa typy kluczy zabezpieczeń:

1. Klucz symetryczny: hello takim samym kluczu jest używany zarówno generowania i weryfikowania tokenu JWT;
2. Klucza asymetrycznego: pary kluczy publiczno prywatnych w X509 używany jest certyfikat z kluczem prywatnym do szyfrowania/generowania JWT token i hello klucz publiczny do weryfikowania hello tokenu.

#### <a name="tech-note"></a>Uwaga techniczna
Jeśli używasz .NET Framework / C# jako platformy programowanie hello X509 certyfikat używany dla klucza asymetrycznego zabezpieczeń musi mieć klucz o długości co najmniej 2048. Jest to wymagane klasy hello System.IdentityModel.Tokens.X509AsymmetricSecurityKey w programie .NET Framework. W przeciwnym razie zostanie wygenerowany hello następujący wyjątek:

IDX10630: hello "System.IdentityModel.Tokens.X509AsymmetricSecurityKey" do podpisywania nie może być mniejsza niż "2048" bitów.

## <a name="hello-completed-system-and-test"></a>system Hello ukończone i testu
Firma Microsoft przeprowadzi kilka scenariuszy w systemie end-to-end ukończyć powitalnych tak, aby czytelnicy mogą mieć basic "obraz" hello zachowanie przed pobraniem konta logowania.

Witaj player aplikacji sieci web i jej logowania można znaleźć [tutaj](https://openidconnectweb.azurewebsites.net/).

Jeśli potrzebne jest "bez zintegrowany" scenariusz: zasoby wideo hostowanych w usłudze Azure Media Services, które są albo niechronionej lub DRM chronione, ale bez tokenu uwierzytelniania (toowhoever licencji, ją wystawiania), możesz przetestować go bez logowania (przełączanie tooHTTP Jeśli Twoje strumieniowe przesyłanie wideo za pośrednictwem protokołu HTTP).

Jeśli potrzebne jest na trasie zintegrowane scenariusz: zasoby wideo podlega dynamicznej ochrony DRM w usłudze Azure Media Services z tokenu uwierzytelniania i tokenu JWT generowane przez usługę Azure AD, należy toologin.

### <a name="user-login"></a>Dane logowania użytkownika
W kolejności tootest hello end-to-end zintegrowanego DRM systemu należy toohave "konto", utworzone lub dodane.

Jakiego konta?

Mimo że Azure pierwotnie zezwalała na dostęp tylko przez użytkowników kont Microsoft, teraz zezwala na dostęp przez użytkowników z tymi dwoma systemami. To została wykonana przez o wszystkich hello właściwości platformy Azure ufają usłudze Azure AD do uwierzytelniania, o usłudze Azure AD uwierzytelnia użytkowników w organizacji i istnieje relacja Federacji gdzie usługa Azure AD ufa hello Microsoft systemowi obsługi tożsamości konsumentów tooauthenticate konsumentów. W związku z tym usługi Azure AD jest konta Microsoft "Gość" tooauthenticate stanie, a także "natywne" konta usługi Azure AD.

Ponieważ usługa Azure AD ufa domeny konta Microsoft (MSA), można dodać wszystkich kont z dowolnej powitania po toohello domen niestandardowych usługi Azure AD dzierżawy i użyj toologin konta hello:

| **Nazwa domeny** | **Domeny** |
| --- | --- |
| **Domena dzierżawy niestandardowych usługi Azure AD** |somename.onmicrosoft.com |
| **Domeny firmowej** |Microsoft.com |
| **Domena konta Microsoft (MSA)** |Outlook.com, live.com, hotmail.com |

Możesz skontaktować się żadnego hello autorów toohave konto utworzone lub dodane.

Poniżej przedstawiono hello zrzuty ekranu strony logowania innego używany przez inną domenę konta.

**Konto domeny dzierżawy niestandardowych usługi Azure AD**: W tym przypadku, zobacz stronę logowania dostosowane hello domeny dzierżawcy hello niestandardowych usługi Azure AD.

![Konto domeny dzierżawcy niestandardowe usługi Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Konto domeny firmy Microsoft z kartami inteligentnymi**: W tym przypadku zobacz stronę logowania hello dostosowane przez firmę Microsoft firmowej IT z uwierzytelniania dwuskładnikowego.

![Konto domeny dzierżawcy niestandardowe usługi Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Konto Microsoft (MSA)**: W tym przypadku zostanie wyświetlona strona logowania hello Account firmy Microsoft dla konsumentów.

![Konto domeny dzierżawcy niestandardowe usługi Azure AD](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Przy użyciu nośnika zaszyfrowanych rozszerzeń dla PlayReady
W przeglądarce nowoczesnych z zaszyfrowanych nośnika rozszerzenia (EME) dla PlayReady będzie pomocy technicznej, takich jak przeglądarki programu Internet Explorer 11 na Windows 8.1 lub nowszej i Microsoft Edge w systemie Windows 10, PlayReady hello podstawowej DRM dla EME.

![Przy użyciu EME PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

obszar ciemny player Hello jest ze względu na fakt toohello PlayReady ochrony uniemożliwia z wprowadzeniem Przechwytywanie ekranu chronionego wideo.

Witaj następujący ekran pokazuje hello player wtyczek i MSE/EME pomocy technicznej.

![Przy użyciu EME PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME Microsoft Edge i 11 programu Internet Explorer w systemie Windows 10 umożliwia wywoływanie z [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) na urządzeniach z systemem Windows 10, które obsługują. PlayReady SL3000 odblokowuje przepływu hello zawartości rozszerzone premium (4K, HDR, itp.) i nowe modele dostarczania zawartości (wczesne okno rozszerzone zawartości).

Skupić się na urządzeniach z systemem Windows hello: PlayReady jest hello tylko DRM w sprz hello dostępnej na urządzeniach z systemem Windows (PlayReady SL3000). Usługi przesyłania strumieniowego za pomocą PlayReady za pośrednictwem EME lub aplikacji platformy uniwersalnej systemu Windows i oferują wyższej jakości wideo za pomocą PlayReady SL3000 niż innym DRM. Zwykle zawartości 2K będzie przechodził przez Chrome lub Firefox i 4 K zawartości za pomocą programu Microsoft Edge/IE11 lub aplikacji platformy uniwersalnej systemu Windows na hello tym samym urządzeniu (w zależności od ustawienia usługi i implementację).

#### <a name="using-eme-for-widevine"></a>Przy użyciu EME Widevine
Na nowoczesne przeglądarki z obsługą EME/Widevine, takie jak Chrome 41 + w systemie Windows 10, Windows 8.1, Mac OS x Yosemite i Chrome na Android 4.4.4 Google Widevine jest hello DRM za EME.

![Przy użyciu EME Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Należy zauważyć, że Widevine nie zapobiega z wprowadzeniem przechwytywania ekranu chronione wideo.

![Przy użyciu EME Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Użytkownicy nie prawo
Jeśli użytkownik nie jest członkiem grupy "Użytkownicy pod tytułem", użytkownik hello nie będzie możliwe toopass "Sprawdź uprawnienia" i usługi licencji multi DRM hello odmówi tooissue hello żądanej licencji, jak pokazano poniżej. Witaj szczegółowy opis jest "uzyskania licencji nie powiodło się", który jest zgodnie z założeniami.

![Cofanie przysługujących użytkowników](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Usługą niestandardowych Secure Token
W scenariuszu hello uruchomionych niestandardowych Secure Token Service (STS) tokenu JWT hello zostaną wystawione przez usługę STS niestandardowych hello przy użyciu klucza w konfiguracji symetrycznej lub asymetrycznej.

Witaj przypadek użycia klucza symetrycznego (za pomocą przeglądarki Chrome):

![Uruchomiona STS niestandardowych](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Witaj przypadek użycia klucza asymetrycznego za pośrednictwem X509 certyfikatu (przy użyciu nowoczesnych przeglądarka firmy Microsoft).

![Uruchomiona STS niestandardowych](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

W obu hello powyżej przypadkach pozostaje uwierzytelniania użytkownika hello sam — za pomocą usługi Azure AD. Witaj jedyna różnica polega na tym, że tokeny JWT są wystawiane przez hello STS niestandardowych zamiast usługi Azure AD. Oczywiście, podczas konfigurowania ochrony CENC dynamicznych, hello ograniczenia usługi dostarczania licencji określa hello typ tokenu JWT klucza w konfiguracji symetrycznej lub asymetrycznej.

## <a name="summary"></a>Podsumowanie
W tym dokumencie omówiono CENC z kilku native DRM i kontroli dostępu za pośrednictwem tokenu uwierzytelniania: projekt i jego wdrożenie za pomocą usługi Azure, Azure Media Services i usługi Azure Media Player.

* Odwołania projektu są prezentowane zawierający wszystkie składniki wymagane hello w podsystemie DRM/CENC;
* Odwołanie do implementacji na platformie Azure, Azure Media Services i Azure Media Player.
* Omówiono także niektóre tematy, które są bezpośrednio związane z hello projektowania i implementacji.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
