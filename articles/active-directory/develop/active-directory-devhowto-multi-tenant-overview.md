---
title: "toobuild aaaHow aplikacji, które można zarejestrować się w każdy użytkownik usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Krok po kroku instrukcje tworzenia aplikacji, które można zalogować użytkownika z dowolnej dzierżawy usługi Azure Active Directory nazywanego także wielodostępnych aplikacji."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Jak toosign w dowolnej usługi Azure Active Directory (AD) użytkownika za pomocą hello wzorzec wielodostępnych aplikacji
Jeśli oferujesz oprogramowania jako toomany aplikacji usługi organizacji, można skonfigurować Twojej aplikacji tooaccept logowania z dowolnej dzierżawy usługi Azure AD.  W usłudze Azure AD jest to, co dzierżawy wielu aplikacji.  Użytkownicy w dowolnej dzierżawy usługi Azure AD będą mogli toosign w aplikacji tooyour po zgodę toouse konto za pomocą aplikacji.  

Jeśli masz istniejącej aplikacji, która ma swój własny system konta lub inne rodzaje logowania od innych dostawców w chmurze obsługuje dodawanie usługi Azure AD logowania z dowolnej dzierżawy jest proste. Tylko rejestrowanie aplikacji, Dodaj kod logowania za pomocą protokołu OAuth2, OpenID Connect lub SAML i umieść przycisk "Logowania w with Microsoft" w swojej aplikacji. Kliknij przycisk powitania po toolearn przycisk więcej na temat znakowania aplikacji.

[! [Zaloguj przycisk] [AAD-logowania]][AAD-App-Branding]

W tym artykule przyjęto założenie, że znasz już tworzenia aplikacji pojedynczej dzierżawy dla usługi Azure AD.  Jeśli nie masz, head, Utwórz kopię zapasową toohello [strony głównej przewodnik dewelopera] [ AAD-Dev-Guide] i wypróbować jeden z naszych Szybki Start!

Istnieją cztery tooconvert prostych czynności w aplikacji do usługi Azure AD wielodostępnych aplikacji:

1. Aktualizowanie aplikacji rejestracji toobe wielu dzierżawy
2. Zaktualizuj/Common toohello kodu toosend żądania punktu końcowego 
3. Aktualizacja Twojego toohandle kodu wielu wartości wystawcy
4. Zrozumienie zgody użytkownika i administratora i zmienić odpowiedni kod

Przyjrzyjmy się każdego kroku szczegółowo. Można także przejść bezpośrednio za[tej listy próbek wielodostępne][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Aktualizacja rejestracji toobe wieloma dzierżawcami
Domyślnie rejestracji aplikacji/interfejsu API sieci web w usłudze Azure AD są pojedynczej dzierżawy.  Umożliwia rejestrację wielodostępne znajdując hello "wielu dzierżawcza" Przełącz się na stronie właściwości hello Twojej rejestracji aplikacji w hello [portalu Azure] [ AZURE-portal] i ustawienie jej zbyt "Yes".

Należy również zauważyć, zanim aplikacji może się wieloma dzierżawcami usługi Azure AD wymaga hello z toobe aplikacji hello globalnie unikatowy identyfikator URI aplikacji. Identyfikator URI aplikacji Hello jest jeden z sposobów hello, który aplikacja zostanie zidentyfikowana w wiadomości protokołu.  Dla aplikacji pojedynczej dzierżawy jest wystarczająca dla toobe identyfikator URI aplikacji hello jest unikatowa w ramach tej dzierżawy.  Aplikacji wielodostępnych musi być globalnie unikatowe dzięki usłudze Azure AD można znaleźć aplikacji hello we wszystkich dzierżawców.  Globalne unikatowość jest wymuszana przez wymaganie toohave identyfikator URI aplikacji hello nazwę hosta pasującą zweryfikowanej domeny hello dzierżawy usługi Azure AD.  Na przykład, jeśli hello nazwę dzierżawy został contoso.onmicrosoft.com, a następnie prawidłowy identyfikator URI aplikacji będzie `https://contoso.onmicrosoft.com/myapp`.  Gdyby dzierżawy zweryfikowanej domeny `contoso.com`, również będą prawidłowy identyfikator URI aplikacji, a następnie `https://contoso.com/myapp`.  Ustawienie aplikacji jako wielodostępnej zakończy się niepowodzeniem, jeśli identyfikator URI aplikacji hello nie będzie zgodna z tego wzorca.

Aplikacja Native client są wielodostępne domyślnie.  Nie trzeba tootake toomake żadnych akcji klienta natywnego dzierżawy usługi rejestracji aplikacji.

## <a name="update-your-code-toosend-requests-toocommon"></a>Aktualizacja Twojego kodu toosend żądań zbyt/wspólne
W aplikacji pojedynczej dzierżawy żądań logowania są wysyłane dzierżawy toohello logowania punktu końcowego. Na przykład dla contoso.onmicrosoft.com będzie hello punktu końcowego:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Wysyłane żądania punktu końcowego dzierżawcy tooa może podpisywać użytkowników (lub gości), w tym tooapplications dzierżawy w tej dzierżawie.  Przy użyciu aplikacji wielodostępnych aplikacji hello nie może ustalić góry użytkownika hello dzierżawy jest, więc nie można wysłać żądania punktu końcowego tooa dzierżawcy.  Zamiast tego żądania wysyłane tooan punktu końcowego, który multiplexes między dzierżaw wszystkie usługi Azure AD:

    https://login.microsoftonline.com/common

Jeśli usługi Azure AD odbiera żądanie na powitania/wspólnego punktu końcowego, jego zalogowaniu użytkownika hello i konsekwencją odnajduje użytkownika hello dzierżawy, który jest z.  Hello/wspólnego punktu końcowego działa z wszystkimi hello protokoły obsługiwane przez usługę Azure AD: OpenID Connect, OAuth 2.0 SAML 2.0 i WS-Federation.

następnie aplikacja toohello logowania odpowiedzi Hello zawiera token reprezentujący hello użytkownika.  wartości wystawcy Hello w tokenie hello informuje aplikacji użytkownika hello dzierżawy jest z.  Gdy zwraca odpowiedź z hello/wspólnego punktu końcowego, wartości wystawcy hello w tokenie hello będzie odpowiadać toohello użytkownika dzierżawcy.  Jest ważne toonote hello/wspólnego punktu końcowego nie jest dzierżawcy i nie jest wystawcę, jest po prostu multiplekser.  Używając/Common hello logikę w aplikacji tokenów toovalidate musi tootake toobe zaktualizować to pod uwagę. 

Jak wspomniano wcześniej, wielodostępnych aplikacji powinny również zapewnić spójne środowisko logowania dla użytkowników, następujące hello znakowania wytyczne aplikacji usługi Azure AD. Kliknij przycisk powitania po toolearn przycisk więcej na temat znakowania aplikacji.

[! [Zaloguj przycisk] [AAD-logowania]][AAD-App-Branding]

Spójrzmy na użycie hello/Common hello punktu końcowego i implementacji kodu bardziej szczegółowo.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Aktualizacja Twojego toohandle kodu wielu wartości wystawcy
Aplikacje sieci Web i interfejsów API sieci web odbierają i sprawdzania poprawności tokenów z usługi Azure AD.  

> [!NOTE]
> Aplikacje klienckie natywnego żądania i odbierać tokeny od usługi Azure AD, jak tak toosend ich tooAPIs, w którym są weryfikowane.  Natywnych aplikacji nie sprawdzania poprawności tokenów i należy je traktować jako przezroczystości.
> 
> 

Zobaczmy, w jaki sposób aplikacja weryfikuje tokeny odbiera z usługi Azure AD.  Stosowanie pojedynczej dzierżawy potrwa zwykle wartość punktu końcowego, takie jak:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

i przy jego użyciu tooconstruct adres URL metadanych (w tym przypadku OpenID Connect), takich jak:

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload dwa najistotniejsze informacje, które są używane toovalidate tokenów: hello dzierżawy podpisywania kluczy i wartości wystawcy.  Każdej dzierżawy usługi Azure AD ma wartość unikatowy wystawcy hello formularza:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

gdzie wartości identyfikatora GUID hello jest hello rename wersja identyfikator dzierżawcy hello hello dzierżawcy.  Po kliknięciu hello poprzedzających link metadanych dla `contoso.onmicrosoft.com`, ta wartość wystawcy dokumentu hello.

Gdy aplikacji pojedynczej dzierżawy weryfikuje token, sprawdza hello podpisu tokenu hello przed hello kluczy z dokumentu metadanych hello podpisywania. Dzięki temu toomake się, że wartości wystawcy hello w hello tokenu dopasowań hello jedną znalezionego w hello dokument metadanych.

Od hello/wspólnego punktu końcowego nie odpowiada żadnemu tooa dzierżawy, a nie wystawcy należy zbadać wartości wystawcy hello w metadanych hello / wspólnej składa się z szablonem adresu URL zamiast rzeczywista wartość:

    https://sts.windows.net/{tenantid}/

W związku z tym aplikacji wielodostępnych nie można sprawdzić poprawności tokenów porównując tylko wartości wystawcy hello w metadanych hello z hello `issuer` wartość hello tokenu.  Aplikacji wielodostępnych musi toodecide logiki wartości wystawcy, które są prawidłowe i mają nie, oparte na powitania dzierżawy część Witaj wystawca wartość Identyfikatora.  

Na przykład jeśli aplikacja wielodostępne zezwala tylko logowania z określonym dzierżawców, którzy utworzyli konto usługi, następnie powinien sprawdzić wartości wystawcy hello lub hello `tid` wartości w hello tokenu toomake się tym dzierżawy znajduje się w ich lista oświadczenia Subskrybenci.  Aplikacji wielodostępnych tylko dotyczy osób, nie decyzje żadnych dostępu oparte na dzierżaw następnie zignorowanie wartości wystawcy hello całkowicie.

W hello wielodostępne próbek w hello [powiązane zawartości](#related-content) sekcja na końcu tego artykułu, sprawdzania poprawności wystawcy hello jest wyłączone tooenable żadnych toosign dzierżawy usługi Azure AD w.

Teraz Przyjrzyjmy się hello czynności użytkownika dla użytkowników, którzy są podpisywania w aplikacjach toomulti dzierżawy.

## <a name="understanding-user-and-admin-consent"></a>Opis użytkowników i zgody administratora
Dla toosign użytkownika w tooan aplikacji w usłudze Azure AD aplikacja hello musi być reprezentowana w dzierżawie powitalnych użytkownika.  Dzięki temu organizacji hello toodo rzeczy, jak zastosować unikatowych zasad podczas ich dzierżawy logowania toohello aplikacji.  W przypadku aplikacji pojedynczej dzierżawy tej rejestracji jest proste; ma ona hello jedną, która jest wywoływana podczas rejestrowania aplikacji hello w hello [portalu Azure][AZURE-portal].

Dla aplikacji wielodostępnych hello rejestracji początkowej dla aplikacji hello przebywa w hello dzierżawy usługi Azure AD używane przez dewelopera hello.  Po zalogowaniu użytkownika z innej dzierżawy w aplikacji toohello powitania po raz pierwszy, usługi Azure AD prosi o aplikacja hello żąda uprawnienia toohello tooconsent.  Jeśli ich zgody, a następnie wywołać reprezentację aplikacji hello *nazwy głównej usługi* jest tworzony w hello użytkownika dzierżawcy i można kontynuować logowania. W katalogu hello, który rejestruje aplikacji toohello zgody użytkownika hello tworzona jest również delegowania. Zobacz [obiekty aplikacji i nazwy głównej usługi] [ AAD-App-SP-Objects] szczegółowe informacje na temat aplikacji hello aplikacji i ServicePrincipal obiektów i ich relacji tooeach innych.

![Zgody toosingle warstwy aplikacji][Consent-Single-Tier] 

To środowisko zgody zależy aplikacja hello żąda uprawnienia hello.  Usługi Azure AD obsługuje dwa rodzaje uprawnienia tylko do aplikacji i delegowani:

* Delegowane uprawnienia przyznaje aplikacji hello możliwości tooact jak zalogowanego użytkownika dla podzbioru hello rzeczy hello użytkownika.  Na przykład można przyznać aplikacji hello delegowane uprawnienia tooread hello podpisany w kalendarzu użytkownika.
* Uprawnienia tylko do aplikacji otrzymuje bezpośrednio toohello tożsamość aplikacji hello.  Na przykład można przyznać aplikacji hello uprawnienia tylko do aplikacji tooread hello listy użytkowników w dzierżawie, niezależnie od tego, który jest zalogowany toohello aplikacji.

Niektóre uprawnienia można przyzwolenie tooby zwykłego użytkownika, a inne wymagają zgody administratora dzierżawy. 

### <a name="admin-consent"></a>Zgody administratora
Uprawnienia tylko do aplikacji zawsze Wymagaj zgody administratora dzierżawy.  Jeśli użytkownik próbuje toosign w aplikacji toohello aplikacji żąda uprawnienia tylko do aplikacji, zostanie wyświetlony komunikat o błędzie informujący, że użytkownik hello nie jest w stanie tooconsent.

Niektóre delegowane uprawnienia również wymagać zgody administratora dzierżawy.  Na przykład hello możliwości toowrite wstecz tooAzure AD jako zalogowany użytkownik hello wymaga zgody administratora dzierżawy.  Podobnie jak uprawnienia tylko do aplikacji Jeśli zwykłego użytkownika spróbuje toosign w aplikacji tooan, który żąda uprawnień delegowanych, które wymaga zgody administratora aplikacji spowoduje wystąpienie błędu.  Określa, czy uprawnienia wymaga zgody administratora jest określany przez dewelopera hello, która wydała hello zasobów i można znaleźć w dokumentacji hello hello zasobu.  Łączy tootopics opisujące dostępne uprawnienia hello hello interfejsu API usługi Azure AD Graph i interfejsu API Graph usługi Microsoft są w hello [powiązane zawartości](#related-content) sekcji tego artykułu.

Jeśli aplikacja używa uprawnienia, które wymagają zgody administratora, należy toohave gestu, takich jak przycisk lub łącza, gdzie Witaj, Administratorze mogą inicjować hello akcji.  Żądanie hello aplikacji wysyła ta akcja jest zwykle żądania autoryzacji OAuth2/OpenID Connect, lecz zawiera również hello `prompt=admin_consent` parametr ciągu zapytania.  Po zgodził Witaj, Administratorze i nazwy głównej usługi hello jest tworzony w dzierżawie powitania klienta, kolejne żądania logowania nie ma potrzeby hello `prompt=admin_consent` parametru. Ponieważ hello administrator decyzję hello zażądał uprawnienia są dopuszczalne, nie innych użytkowników w dzierżawie powitalnych pojawi się monit o zgodę od tej pory.

Witaj `prompt=admin_consent` parametru można również przez aplikacje, które zażądać uprawnień, które nie wymagają zgody administratora. Odbywa się po aplikacji hello wymaga obsługi gdzie Witaj, Administratorze dzierżawy "zarejestrowaniu" co w czasie, a nie inne użytkownicy otrzymają monit o zgodę od tego momentu na.

Jeśli aplikacja wymaga zgody administratora, a administrator zaloguje się do jednak hello `prompt=admin_consent` parametru nie są wysyłane, Witaj, Administratorze pomyślnie zgody aplikacji toohello **tylko dla swojego konta użytkownika**.  Regularne użytkownicy nie będą nadal mogli toosign w i zgody toohello aplikacji.  Jest to przydatne, jeśli ma być toogive hello dzierżawy administratora hello możliwości tooexplore aplikację przed umożliwieniem dostępu do innych użytkowników.

Administrator dzierżawy można wyłączyć możliwość hello tooapplications tooconsent normalnych użytkowników.  Ta funkcja jest wyłączona, zgody administratora jest zawsze wymagane do konfigurowania w dzierżawie powitalnych toobe aplikacji hello.  Chcąc tootest aplikacji przy użyciu zwykłego użytkownika zgody wyłączone, można znaleźć hello przełącznik konfiguracji w dzierżawie powitalnych usługi Azure AD sekcji konfiguracji hello [portalu Azure][AZURE-portal].

> [!NOTE]
> Niektóre aplikacje mają środowisko, w którym normalnych użytkowników są początkowo stanie tooconsent i nowszych aplikacji hello może obejmować hello administratora oraz zażądać uprawnień, które wymagają zgody administratora.  Brak nie toodo sposób to rejestracji pojedynczej aplikacji w usłudze Azure AD dzisiaj.  punkt końcowy v2 Hello nadchodzących usługi Azure AD umożliwi aplikacji toorequest uprawnienia w czasie wykonywania, zamiast w czasie rejestracji spowoduje włączenie tego scenariusza.  Aby uzyskać więcej informacji, zobacz hello [przewodnik dewelopera usługi Azure AD App Model v2][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Aplikacje wielowarstwowe i zgody
Aplikacja może mieć wielu warstw, każdy reprezentowany przez jego własnej rejestracji w usłudze Azure AD.  Na przykład natywnych aplikacji, która wywołuje interfejs API sieci web lub aplikacji sieci web która wywołuje interfejs API sieci web.  W obu przypadkach powitania klienta (aplikacji sieci web lub aplikacji natywnej) żąda uprawnienia toocall hello zasobów (interfejs API sieci web).  Dla powitania klienta toobe pomyślnie zgodę na klienta dzierżawy, wszystkie toowhich zasobów wymaga uprawnień musi już istnieć w dzierżawie powitania klienta.  Jeśli ten warunek nie jest spełniony, usługi Azure AD będzie zwracać najpierw należy dodać błędu hello zasobów.

**Konfiguracja wielu warstw w pojedynczej dzierżawy**

Może to być problem, jeśli aplikacja logicznej składa się z dwóch lub więcej rejestracji aplikacji, na przykład oddzielnych klienta i zasobów.  Jak można uzyskać zasobu hello na powitania klienta dzierżawy pierwszy?  Usługi Azure AD obejmuje przypadek przez włączenie klienta i toobe zasobów zgodę w jednym kroku. Witaj, użytkownik widzi łączną sumę hello hello uprawnień wymaganych przez powitania klienta i zasobów na stronie zgoda hello.  tooenable to zachowanie rejestracji aplikacji hello zasobów musi zawierać identyfikator aplikacji hello klienta jako `knownClientApplications` w manifeście aplikacji.  Na przykład:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Ta właściwość może zostać zaktualizowana przy użyciu zasobów hello [manifest aplikacji][AAD-App-Manifest]. To jest przedstawiona w klientami wielowarstwowych wywołanie interfejsu API sieci web przykładowej hello [powiązane zawartości](#related-content) sekcji na końcu hello w tym artykule. Witaj następujący diagram zawiera omówienie zgody dla aplikacji wielowarstwowych zarejestrowane w pojedynczej dzierżawy:

![Wyrazić zgodę, aplikacja kliencka znane toomulti warstwy][Consent-Multi-Tier-Known-Client] 

**Konfiguracja wielu warstw w wielu dzierżawców**

Podobne przypadku się stanie w przypadku różnych warstw hello aplikacji są rejestrowane w różnym dzierżawcom.  Na przykład rozważmy hello tworzenia aplikacji klientami, która wywołuje hello interfejsu API Office 365 Exchange Online.  natywny hello toodevelop aplikacji i nowszy toorun natywnych aplikacji hello w dzierżawie klienta, nazwy głównej usługi Exchange Online hello musi być obecny.  W takim przypadku hello deweloperów i klient musi zakupić usługi Exchange Online dla toobe główna usługi hello utworzone w swoich dzierżaw.  

W przypadku hello interfejs API utworzony przez organizację innych niż Microsoft Projektant hello hello interfejsu API musi tooprovide sposób ich stosowania hello tooconsent klientów do ich klientom dzierżaw. Witaj zalecane projektu jest dla hello 3 strona developer toobuild hello interfejsu API w taki sposób, że można działa również jako tooimplement klienta sieci web rejestracji:

1. Wykonaj hello wcześniejszych sekcjach hello tooensure interfejsu API zaimplementowano wymagania dotyczące rejestracji/kod wielodostępnych aplikacji hello
2. Ponadto role/zakresy hello tooexposing interfejsu API, upewnij się, hello rejestracji zawiera hello "Zaloguj się i odczytuj profil użytkownika" uprawnienia usługi Azure AD (domyślnie dostępne)
3. Implementuje stronę logowania — w/tworzenia konta w powitania klienta sieci web, po hello [zgody administratora](#admin-consent) wskazówki wymienione powyżej 
4. Po hello użytkownik zgadza toohello aplikacji, hello service principal role i zgody delegowania łącza są tworzone w swojej dzierżawy, a natywnych aplikacji hello może uzyskać tokenów dla hello interfejsu API

powitania po diagram zawiera omówienie zgody dla aplikacji wielowarstwowych zarejestrowane w różnych dzierżawców:

![Zgody warstwy toomulti wieloosobowa aplikacji][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Cofnięcie zgody
Użytkownicy i Administratorzy można odwołać zgody tooyour aplikacji w dowolnym momencie:

* Użytkownicy odwołać dostępu tooindividual aplikacji, usuwając je z ich [aplikacji panelu dostępu] [ AAD-Access-Panel] listy.
* Administratorzy odwołać dostępu tooapplications, usuwając je z usługi Azure AD przy użyciu sekcji zarządzania hello Azure AD hello [portalu Azure][AZURE-portal].

Jeśli administrator wyrazi na to zgody tooan aplikacji dla wszystkich użytkowników w dzierżawie, użytkownicy nie mogą indywidualnie odwołać dostęp.  Tylko hello administrator można odwołać dostęp i tylko dla całej aplikacji hello.

### <a name="consent-and-protocol-support"></a>Obsługa protokołu i zgodę
Zgoda jest obsługiwana w usłudze Azure AD za pomocą protokołu OpenID Connect, hello OAuth, WS-Federation oraz SAML protokołów.  Witaj protokołów języka SAML i WS-Federation nie obsługują hello `prompt=admin_consent` parametru, więc zgody administratora tylko jest to możliwe za pośrednictwem protokołu OAuth i OpenID Connect.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Aplikacje wielodostępne i buforowanie tokeny dostępu
Aplikacje wielodostępne można również uzyskać toocall tokenów dostępu do interfejsów API, które są chronione przez usługę Azure AD.  Typowym błędem podczas korzystania z aplikacją wielodostępne hello Active Directory Authentication Library (ADAL) jest żądaniem tooinitially token dla użytkownika za pomocą/Common, otrzymują odpowiedź, a następnie żądania tokenu kolejnych dla tego samego użytkownika również przy użyciu/Common.  Ponieważ hello odpowiedzi z usługi Azure AD pochodzi od dzierżawcy, nie/wspólne, ADAL buforuje hello token jako pochodzącej z hello dzierżawy. Hello kolejne wywołania tooget zbyt/wspólnego, jest token dostępu dla wpisu pamięci podręcznej hello hello użytkownika Chybienia i hello użytkownika zostanie wyświetlony monit o toosign w ponownie.  tooavoid Brak pamięci podręcznej hello, upewnij się, że wezwań do już zalogowanego użytkownika są wykonywane punktu końcowego toohello dzierżawcy.

## <a name="next-steps"></a>Następne kroki
W tym artykule należy przedstawiono sposób toobuild aplikacji, która może zalogować użytkownika z dowolnej dzierżawy usługi Azure Active Directory. Po włączeniu rejestracji jednokrotnej między aplikacji i usługi Azure Active Directory, należy zaktualizować Twojej aplikacji tooaccess interfejsach API udostępnianych przez zasoby firmy Microsoft, takich jak usługi Office 365. Dlatego możesz zaoferować spersonalizowane środowisko w aplikacji, na przykład przedstawiający informacje kontekstowe toohello użytkowników, takich jak ich obraz profilu lub ich dalej terminu kalendarza. toolearn więcej informacji na temat tworzenia interfejsu API wywołuje tooAzure usługi Active Directory i usługi Office 365, takich jak program Exchange, SharePoint, OneDrive, OneNote, planowania, Excel i więcej, odwiedź stronę: [interfejsu API programu Microsoft Graph][MSFT-Graph-overview].


## <a name="related-content"></a>Zawartość pokrewna
* [Przykłady aplikacji z wieloma dzierżawcami][AAD-Samples-MT]
* [Znakowania wytyczne dotyczące aplikacji][AAD-App-Branding]
* [Przewodnik dewelopera usługi Azure AD][AAD-Dev-Guide]
* [Obiekty aplikacji i nazwy głównej usługi][AAD-App-SP-Objects]
* [Integrowanie aplikacji z usługą Azure Active Directory][AAD-Integrating-Apps]
* [Omówienie hello zgody Framework][AAD-Consent-Overview]
* [Zakresy uprawnień Microsoft Graph API][MSFT-Graph-permision-scopes]
* [Zakresy uprawnień usługi Azure AD Graph API][AAD-Graph-Perm-Scopes]

Użyj powitania po opinii tooprovide sekcji komentarzy i pomóc nam dostosować i kształtu zawartość.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














