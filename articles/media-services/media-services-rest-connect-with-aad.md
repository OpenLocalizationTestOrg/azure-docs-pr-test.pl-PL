---
title: "aaaUse tooaccess uwierzytelniania usługi Azure AD Azure Media Services API z POZOSTAŁĄ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooaccess interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure Active Directory przy użyciu REST."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Użyj usługi Azure AD authentication tooaccess hello Azure Media Services API z POZOSTAŁĄ

Zespół usługi Azure Media Services Hello wydała obsługę uwierzytelniania usługi Azure Active Directory (Azure AD) dla dostępu do usługi Azure Media Services. On również ogłosiła uwierzytelniania usługi kontroli dostępu platformy Azure toodeprecate planów dla dostępu usługi Media Services. Ponieważ każda subskrypcja platformy Azure i co konto usługi Media Services dzierżawy dołączonych tooan usługi Azure AD, obsługę uwierzytelniania usługi Azure AD oferuje wiele korzyści w zakresie zabezpieczeń. Szczegółowe informacje dotyczące tej zmiany i migracji (Jeśli używasz hello .NET SDK usługi Media Services dla aplikacji), można znaleźć w następujących hello blogu ogłoszeń i artykuły:

- [Usługa Azure Media Services ogłasza pomocy technicznej dla usługi Azure AD i amortyzacja uwierzytelniania kontroli dostępu](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [Interfejs API usług Media Azure dostępu przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md)
- [Korzystanie z usługi Azure AD authentication tooaccess interfejsu API usługi Azure Media Services za pomocą programu Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Wprowadzenie do uwierzytelniania usługi Azure AD przy użyciu hello portalu Azure](media-services-portal-get-started-with-aad.md)

Niektórzy klienci muszą toodevelop ich rozwiązań Media Services, w obszarze hello następujące ograniczenia:

*   Korzystają z języka programowania, który nie jest program Microsoft .NET lub C# lub nie jest hello środowiska uruchomieniowego systemu Windows.
*   Bibliotek platformy Azure AD, takich jak biblioteki uwierzytelniania usługi Active Directory są niedostępne dla hello język programowania lub nie może służyć do ich środowiska uruchomieniowego.

Niektórzy klienci mają opracowanych aplikacji przy użyciu interfejsu API REST dla uwierzytelniania kontroli dostępu i dostępu do usługi Azure Media Services. Dla tych klientów należy sposób toouse tylko hello interfejsu API REST dla uwierzytelniania usługi Azure AD i dostęp do kolejnych usługi Azure Media Services. Należy toonot polegać na żadnym z bibliotek usługi Azure AD hello lub na powitania .NET SDK usługi Media Services. W tym artykule firma Microsoft opisano rozwiązania i podaj przykładowy kod dla tego scenariusza. Ponieważ wszystkie wywołania interfejsu API REST, z nie zależność od usługi Azure AD jest kod hello lub biblioteki usługi Azure Media Services hello kodu można łatwo zostać przetłumaczone tooany inny język programowania.

> [!IMPORTANT]
> Obecnie usługa Media Services obsługuje hello Azure kontroli dostępu usług uwierzytelniania modelu. Jednak kontroli dostępu uwierzytelniania zostaną wycofane 1 czerwca 2018. Zaleca się, jak najszybciej migracji model uwierzytelniania toohello usługi Azure AD.


## <a name="design"></a>Projektowanie

W tym artykule używamy hello następującego projektu uwierzytelniania i autoryzacji:

*  Protokół HCAP: OAuth 2.0. OAuth 2.0 to standard zabezpieczeń sieci web, który obejmuje zarówno uwierzytelniania i autoryzacji. Jest on obsługiwany przez Google, Microsoft, Facebook i PayPal. Został on ratyfikacji października 2012. Firma Microsoft obsługuje mocno OAuth 2.0 i OpenID Connect. Obsługiwane są zarówno z tymi standardami w wielu usługach i bibliotek klienckich, włącznie z usługi Azure Active Directory, Otwórz interfejs sieci Web dla platformy .NET (OWIN) Katana i bibliotek usługi Azure AD.
*  Przyznaj typu: typ przyznania poświadczeń klienta. Poświadczenia klienta jest jednym z typów przydziałów cztery hello w OAuth 2.0. Często jest używane dla dostępu do usługi Azure AD Microsoft Graph API.
*  Tryb uwierzytelniania: nazwy głównej usługi. Witaj innych tryb uwierzytelniania jest użytkownika lub uwierzytelnianie interakcyjne.

Łącznie cztery aplikacje lub usługi są zaangażowane w przepływ uwierzytelniania i autoryzacji hello Azure AD dla usługi Media Services. w hello w poniższej tabeli opisano Hello aplikacji i usług oraz przepływu hello:

|Typ aplikacji |Aplikacja |Ruch|
|---|---|---|
|Klient | Klient aplikacji lub rozwiązania | Ta aplikacja (w rzeczywistości jego agent proxy) jest zarejestrowana w hello dzierżawy usługi Azure AD, w których hello Azure media subskrypcji i hello znajdują się konta usługi. Witaj nazwy głównej usługi aplikacji hello zarejestrowany następnie udzielany jest właścicielem lub współautorem roli w hello kontroli dostępu (IAM) konta usługi media hello. nazwy głównej usługi Hello jest reprezentowana przez powitania klienta identyfikator i klienta klucz tajny aplikacji. |
|Dostawcy tożsamości (IDP) | Azure AD jako dostawca tożsamości | jednostki usługi zarejestrowanych aplikacji Hello (identyfikator klienta i klucz tajny klienta) jest uwierzytelniony przez usługę Azure AD jako dostawca tożsamości hello. To uwierzytelnianie jest wykonywane wewnętrznie i niejawnie. Jak przepływ poświadczeń klienta powitania klienta jest uwierzytelniany zamiast hello użytkownika. |
|Secure Token Service (STS) / serwera OAuth | Azure AD jako Usługa STS | Po uwierzytelnieniu przez hello IDP (lub serwera OAuth względem OAuth 2.0) tokenu dostępu lub tokenu Web JSON (JWT) jest wystawiony przez usługę Azure AD jako serwera STS/OAuth dla zasobu warstwy środkowej toohello dostępu: w tym przypadku hello punkt końcowy interfejsu API REST usługi multimediów. |
|Zasób | Interfejs API REST usługi Media Services | Każdego wywołania interfejsu API REST usług Media jest upoważniony przez tokenu dostępu, który został wystawiony przez usługę Azure AD jako STS lub powitania serwera OAuth. |

Uruchom hello przykładowy kod i przechwycić token JWT lub tokenu dostępu, hello JWT zawiera hello następujące atrybuty:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Poniżej przedstawiono hello mapowania między hello atrybutów w hello JWT i hello cztery aplikacje lub usługi w powyższej tabeli hello:

|Typ aplikacji |Aplikacja |Atrybut JWT |
|---|---|---|
|Klient |Klient aplikacji lub rozwiązania |AppID: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". Identyfikator klienta Hello aplikacji zostanie zarejestrowana tooAzure AD w następnej sekcji hello. |
|Dostawcy tożsamości (IDP) | Azure AD jako dostawca tożsamości |IDP: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Witaj identyfikator GUID jest dzierżawy identyfikator Microsoft hello (microsoft.onmicrosoft.com). Każdy dzierżawca ma własną, unikatowy identyfikator. |
|Secure Token Service (STS) / serwera OAuth |Azure AD jako Usługa STS | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Witaj identyfikator GUID jest dzierżawy identyfikator Microsoft hello (microsoft.onmicrosoft.com). |
|Zasób | Interfejs API REST usługi Media Services |lub: "https://rest.media.azure.net". Adresat Hello lub odbiorców hello tokenu dostępu. |

## <a name="steps-for-setup"></a>Kroki instalacji

tooregister i konfigurowanie aplikacji usługi Azure AD do uwierzytelniania usługi Azure AD i tooobtain token dostępu dla wywołaniem punktu końcowego z interfejsu API REST usługi Azure Media hello, pełną hello następujące kroki:

1.  W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), zarejestruj dzierżawy usługi Azure AD toohello aplikacji (na przykład wzmediaservice) usługi Azure AD (na przykład microsoft.onmicrosoft.com). Nie ma znaczenia, czy zarejestrowany jako aplikacji sieci web lub aplikacji natywnej. Ponadto można wybrać adres URL logowania, a adres URL odpowiedzi (na przykład http://wzmediaservice.com dla obu).
2. W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), przejdź toohello **Konfiguruj** kartę aplikacji. Uwaga hello **identyfikator klienta**. Następnie w obszarze **klucze**, generowanie **klucz klienta** (klucz tajny klienta). 

    > [!NOTE] 
    > Zanotuj klucz tajny powitania klienta. Nie można wyświetlić ponownie.
    
3.  W hello [portalu Azure](http://ms.portal.azure.com), przejdź do konta usługi Media Services toohello. Wybierz hello **kontroli dostępu** okienka (IAM). Dodaj nowy element członkowski ma hello właściciela lub Rola współautora hello. Dla podmiotu hello wyszukiwania dla nazwy aplikacji hello zarejestrowaną w kroku 1 (w tym przykładzie wzmediaservice).

## <a name="info-toocollect"></a>Informacje o toocollect

tooprepare REST kodowania, zbieranie powitania po tooinclude punktów danych w kodzie hello:

*   Azure AD jako punkt końcowy usługi STS: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Z tego punktu końcowego tokenu JWT dostępu jest wymagany. Ponadto tooserving jako dostawca tożsamości, usługi Azure AD służy również jako tokenu Zabezpieczającego. Usługa Azure AD wystawia token JWT uzyskać dostęp do zasobów (token dostępu). JWT token ma różne oświadczenia.
*   Azure Media interfejsu API REST usług jako zasób lub odbiorców: https://rest.media.azure.net.
*   Identyfikator klienta: Zobacz krok 2 w [kroki instalacji](#steps-for-setup).
*   Klucz tajny klienta: zobacz krok 2 w [kroki instalacji](#steps-for-setup).
*   Usługa Media Services konto interfejsu API REST punktu końcowego w hello następującego formatu:

    https://[media_service_account_name].restv2. [data_center].media.azure.net/API 

    Jest to hello punktu końcowego, z których wszystkie API REST usługi Media w aplikacji wywołań. Na przykład https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Następnie możesz umieścić te pięć parametrów w pliku web.config lub app.config toouse w kodzie.

## <a name="sample-code"></a>Przykładowy kod

Można znaleźć hello przykładowy kod w [Azure AD Authentication Azure Media Services dostępu: zarówno za pośrednictwem interfejsu API REST](https://github.com/willzhan/WAMSRESTSoln).

Witaj przykładowy kod ma dwie części:

*   Projekt biblioteki DLL, który ma wszystkie hello kodu interfejsu API REST usługi Azure AD uwierzytelniania i autoryzacji. Ma również metody do tworzenia interfejsu API REST wywołania toohello interfejsu API REST usług Media punktu końcowego, przy hello tokenu dostępu.
*   Klient testu konsoli, która inicjuje uwierzytelniania usługi Azure AD i wywołuje innego interfejsu API REST usługi Media.

Witaj przykładowy projekt ma trzy funkcje:

*   Azure AD uwierzytelnienia za pomocą poświadczeń klienta hello przyznać za pośrednictwem hello interfejsu API REST.
*   Azure Media Services dostęp przy użyciu hello interfejsu API REST.
*   Dostępu do magazynu Azure za pomocą tylko hello interfejsu API REST (jako toocreate używane konto usługi Media Services przy użyciu interfejsu API REST).


## <a name="where-is-hello-refresh-token"></a>Gdzie znajduje się token odświeżania hello?

Niektóre czytniki może poprosić o: gdzie jest token odświeżania hello? Dlaczego nie używać tokenu odświeżania w tym miejscu?

Celem Hello token odświeżania nie jest toorefresh tokenu dostępu. Zamiast tego jest zaprojektowana toobypass interwencji użytkownika końcowego uwierzytelniania lub użytkownika i nadal uzyskać token prawidłowy dostępu po wygaśnięciu tokenu wcześniej. Lepsze nazwę token odświeżania może być następująca: "obejścia ponownie-konta w tokenu".

Jeśli używasz hello OAuth 2.0 autoryzacji przyznać przepływu (nazwa użytkownika i hasło, działając w imieniu użytkownika), token odświeżania pomaga Uzyskaj token dostępu odnowionego bez interwencji użytkownika żądania. Jednak hello OAuth 2.0 poświadczenia klienta umożliwiają przepływ, które opisano w tym artykule, powitania klienta działa w swoim imieniu. Nie wymagają interwencji użytkownika na wszystkich i powitania serwera autoryzacji nie wymaga zbyt i nie będzie zapewniają token odświeżania. Jeśli debugowanie hello **GetUrlEncodedJWT** metody, można zauważyć, że hello odpowiedź z punktu końcowego tokena hello ma tokenu dostępu, ale nie token odświeżania.

## <a name="next-steps"></a>Następne kroki

Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-dotnet-upload-files.md).
