---
title: aaaExporting tooPowerApps API hostowanymi na platformie Azure i Microsoft Flow | Dokumentacja firmy Microsoft
description: "Omówienie sposobu tooexpose interfejsu API hostowanych w tooPowerApps usługi aplikacji i Flow firmy Microsoft"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Eksportowanie tooPowerApps API hostowanymi na platformie Azure i Flow firmy Microsoft

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Tworzenie niestandardowych łączniki dla PowerApps i Flow firmy Microsoft

[Rozwiązanie PowerApps](https://powerapps.com) to usługa do tworzenia i używania aplikacje biznesowe niestandardowego połączenia danych tooyour i użycia między platformami. [Microsoft Flow](https://flow.microsoft.com) pozwala łatwo tooautomate przepływów pracy i procesów biznesowych między ulubionych aplikacji i usług. Zarówno PowerApps i Microsoft Flow pochodzą z różnych źródeł toodata łączników, takich jak usługi Office 365, Dynamics 365 Salesforce i więcej. Jednak użytkownicy muszą również źródeł danych stanie tooleverage toobe i interfejsów API konstruowany przez organizację.

Podobnie deweloperów, którzy tooexpose ich interfejsów API więcej szeroko w hello organizacji możesz toomake ich tooPowerApps dostępne interfejsy API i użytkownicy Flow firmy Microsoft. W tym temacie opisano sposób wbudowane tooexpose interfejsu API z usługi aplikacji Azure lub usługi Azure Functions tooPowerApps i Flow firmy Microsoft. [Usługa aplikacji Azure](https://azure.microsoft.com/services/app-service/) jest oferty platformy jako usługi, który umożliwia deweloperom tooquickly i łatwo kompilacji korporacyjnej, mobilne i sieci web, aplikacje interfejsu API. [Środowisko Azure Functions](https://azure.microsoft.com/services/functions/) to rozwiązanie oparte na zdarzeniu niekorzystającą obliczeniowe umożliwiający tooquickly autora kod, który można reagować tooother części systemu i skali na podstawie zapotrzebowania.

toolearn więcej informacji na temat tych usług, zobacz:
- [Rozwiązanie PowerApps z przewodnikiem Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Uczenie z przewodnikiem przepływu firmy Microsoft](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Co to jest usługa App Service?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Co to jest Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Udostępnianie definicji interfejsu API

Interfejsy API są często opisane przy użyciu [dokumentu OpenAPI](https://www.openapis.org/) (czasem określana tooas dokumentu "Swagger"). Zawiera wszystkie hello informacje, jakie operacje są dostępne i struktury danych hello. PowerApps i Microsoft Flow można tworzyć niestandardowe łączniki dla każdego dokumentu OpenAPI 2.0. Po utworzeniu niestandardowego łącznika może służyć w hello dokładnie tak samo jak jeden z hello łączników i szybko można zintegrować aplikacji.

Azure App Service i usługi Azure Functions [wbudowana obsługa](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) do tworzenia i zarządzania dokumentami OpenAPI hostingu. W kolejności toocreate niestandardowego łącznika dla sieci web, mobilnych, interfejsu API lub funkcji aplikacji PowerApps i przepływów muszą toobe podane kopię hello definicji.

> [!NOTE]
> Ponieważ kopię hello definicji interfejsu API jest używany, PowerApps i Microsoft Flow nie będą od razu wiedzieć o aktualizacji lub aplikacji toohello zmiany podziału. Jeśli nowa wersja interfejsu API hello jest dostępny, te kroki należy powtórzyć dla hello nowej wersji. 

tooprovide rozwiązania PowerApps i Flow Microsoft hello hostowanej definicji interfejsu API dla aplikacji, wykonaj następujące kroki:

1. Otwórz hello [Azure Portal](https://portal.azure.com) i przejdź tooyour aplikację usługi aplikacji lub usługi Azure Functions.

    Jeśli przy użyciu usługi Azure App Service, wybierz **definicji interfejsu API** z listy ustawień hello. 
    
    Jeśli używasz usługi Azure Functions, wybierz aplikację funkcji, a następnie wybierz **funkcji platformy**, a następnie **definicji interfejsu API**. Możesz również wybrać tooopen hello **definicji interfejsu API (wersja zapoznawcza)** karcie zamiast tego.

2. Jeśli podano definicji interfejsu API, zobaczysz **wyeksportować tooPowerApps + Microsoft Flow** przycisku. Kliknij przycisk proces eksportu hello toobegin.

3. Wybierz hello **Eksport tryb**. Określa hello kroki należy toocreate toofollow łącznika. Usługa App Service oferuje dwie opcje dostarczanie PowerApps i Microsoft Flow definicja interfejsu API:

    **Express** umożliwia tworzenie łącznika niestandardowego hello z wewnątrz hello portalu Azure. Wymaga to hello bieżącej zalogowany użytkownik ma uprawnienia toocreate łączników w środowisku docelowym hello. Jest to zalecane podejście spełnieniu tego wymogu hello. Jeśli ten tryb jest używany, wykonaj hello [Express eksportu](#express) poniższe instrukcje.

    **Ręczne** umożliwia eksportowanie kopii hello definicji interfejsu API, które można zaimportować za pomocą hello rozwiązania PowerApps lub portale Flow firmy Microsoft. Jest to zalecane podejście, jeśli hello użytkowników platformy Azure i hello użytkownika z uprawnienia toocreate łączników są różne osoby lub łącznika hello musi toobe utworzony w innej dzierżawie powitalnych. Jeśli ten tryb jest używany, wykonaj hello [ręczne eksportu i importu](#manual) poniższe instrukcje.

<a name="express"></a>
## <a name="express-export"></a>Express eksportu

W tej sekcji będzie utworzyć nowy łącznik niestandardowych z wewnątrz hello portalu Azure. Należy zalogować się do toowhich dzierżawy hello mają tooexport i musisz mieć uprawnienia toocreate niestandardowego łącznika w środowisko docelowe hello.

1. Wybierz środowisko hello, w którym chcesz toocreate hello łącznika. Następnie podaj nazwę łącznik niestandardowy.

2. Jeśli definicja interfejsu API zawiera żadnych definicji zabezpieczeń, to zostanie wywołana w kroku #2. W razie potrzeby podaj zabezpieczeń hello szczegóły konfiguracji potrzebne toogrant użytkownicy uzyskują dostęp do interfejsu API tooyour. Aby uzyskać więcej informacji, zobacz [uwierzytelniania](#auth) poniżej. 

3. Kliknij przycisk **OK** toocreate łącznik niestandardowy.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Ręczne eksportu i importu

W kolejności toocreate niestandardowego łącznika dla sieci web i mobilnych, interfejsu API lub funkcji aplikacji będą potrzebne dwa kroki:

1. [Pobieranie definicji interfejsu API hello z usługi aplikacji lub usługi Azure Functions](#export)
2. [Importowanie definicji interfejsu API hello PowerApps i Flow firmy Microsoft](#import)

Jest to możliwe, następujące dwa kroki należy toobe przeprowadzonych przez oddzielne osób w organizacji, jak określony użytkownik może nie mieć uprawnień tooperform zarówno akcje. W takim przypadku deweloperze, który ma toohello dostępu współautora aplikację usługi aplikacji lub usługi Azure Functions należy definicji interfejsu API hello tooobtain (pojedynczy plik JSON) lub tooit łącza. Następnie należy tooprovide właściciela tej definicji w tooa rozwiązania PowerApps lub Flow firmy Microsoft. Tego właściciela można użyć łącznika niestandardowego toocreate hello hello metadanych.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Pobieranie definicji interfejsu API hello z usługi aplikacji lub usługi Azure Functions

W tej sekcji będzie eksportować hello definicji interfejsu API dla interfejsu API usługi aplikacji, używane w dalszej części portalu rozwiązania PowerApps lub Microsoft Flow hello toobe.

1. Możesz wybrać tooeither **pobrać definicji interfejsu API hello** lub **Uzyskaj link**. Zależności wybierzesz, wynik hello znajdzie się w następnej sekcji hello. Wybierz jedną z poniższych opcji i wykonaj instrukcje hello.
 
2. Jeśli definicja interfejsu API zawiera żadnych definicji zabezpieczeń, to zostanie wywołana w kroku #2. Podczas importowania PowerApps i Microsoft Flow wykryje to i wyświetli monit o podanie informacji o zabezpieczeniach. Zbierz hello poświadczenia powiązane tooeach definicji do użycia w następnej sekcji hello. Aby uzyskać więcej informacji, zobacz [uwierzytelniania](#auth) poniżej. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Importowanie definicji interfejsu API hello PowerApps i Flow firmy Microsoft

W tej sekcji utworzysz niestandardowego łącznika w rozwiązaniu PowerApps i Flow firmy Microsoft przy użyciu definicji interfejsu API hello uzyskany wcześniej. Niestandardowe łączników są współużytkowane Witaj dwie usługi, wystarczy tylko raz tooimport hello definicji. Aby uzyskać więcej informacji na łączników niestandardowych, zobacz [zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps] i [zarejestrować i używania niestandardowych łączników w Microsoft Flow].

1. Otwórz hello [portalu sieci web w rozwiązaniu Powerapps](https://web.powerapps.com) lub hello [portalu sieci web Microsoft Flow](https://flow.microsoft.com/)i zaloguj się. 

2. Kliknij przycisk hello **ustawienia** przycisk (hello koło zębate ikonę) w prawym górnym rogu hello hello strony i wybierz **łączniki niestandardowe**. 

3. Kliknij przycisk **Tworzenie niestandardowego łącznika**.

4. Na powitania **ogólne** karcie, podaj nazwę dla interfejsu API, a następnie przekaż hello OpenAPI definicji lub wklej adres URL metadanych hello. Kliknij przycisk **kontynuować**.

4. Na powitania **zabezpieczeń** karcie, jeśli zostanie wyświetlony monit o tooprovide szczegóły uwierzytelniania, wprowadź wartości hello uzyskanych w poprzedniej sekcji hello. Jeśli nie, przejdź do następnego kroku toohello.

5. Na powitania **definicje** , wszystkie operacje hello zdefiniowane w pliku OpenAPI są wypełniane automatycznie. Jeśli wszystkie wymagane operacje są zdefiniowane, można przejść toohello następnego kroku. Jeśli nie, można dodawać i modyfikować tutaj operacji.

6. Kliknij przycisk **utworzyć łącznik**. Wywołania API tootest, przejdź toohello następnego kroku.

7. Na powitania **testu** , Utwórz połączenie, wybierz tootest operacji, a następnie wprowadzić wszystkie dane wymagane przez operację hello.

8. Kliknij przycisk **Operacja testowania**.


<a name="auth"></a>
## <a name="authentication"></a>Authentication

PowerApps i Microsoft Flow obsługują kolekcja dostawców tożsamości, które mogą być używane toolog użytkownicy łącznik niestandardowy. Jeśli Twój interfejs API wymaga uwierzytelnienia, upewnij się, że jest przechwytywany jako _definicji zabezpieczeń_ w dokumencie OpenAPI. Podczas eksportowania konieczne będzie tooprovide konfiguracji wartości, które umożliwiają rozwiązanie PowerApps akcji logowania tooperform Flow firmy Microsoft.

W tej sekcji omówiono hello typy uwierzytelniania, które są obsługiwane przez przepływu express hello: klucz interfejsu API, Azure Active Directory i rodzajowy OAuth 2.0. Aby uzyskać pełną listę dostawców i każda wymaga poświadczeń hello, zobacz [zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps] i [zarejestrować i używania niestandardowych łączników w Microsoft Flow].

### <a name="api-key"></a>Klucz interfejsu API
W przypadku tego systemu zabezpieczeń użytkowników hello łącznika będzie pełnił rolę klucza hello zostanie wyświetlony monit o tooprovide, podczas tworzenia połączenia. Możesz podać toohelp nazwa klucza interfejsu API ich o klucz, do którego jest potrzebny. Dla usługi Azure Functions zazwyczaj będzie jeden z kluczy hosta hello, obejmujące kilka funkcji w ramach hello funkcji aplikacji.

### <a name="azure-active-directory"></a>Usługa Azure Active Directory
Podczas konfigurowania łącznika niestandardowego, który wymaga logowania usługi AAD, wymagane są dwa rejestracji aplikacji usługi AAD: jeden interfejs API zaplecza hello toomodel i jeden łącznik hello toomodel w rozwiązaniu PowerApps i przepływów.

Interfejs API powinien być skonfigurowany toowork przy pierwszej rejestracji hello, a to będzie już można podjąć się użycie hello [uwierzytelniania/autoryzacji dla aplikacji usługi](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) funkcji.

Konieczne będzie toomanually utworzyć drugi rejestrację hello łącznika hello hello kroki opisane w [Dodawanie aplikacji AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Witaj rejestracji musi toohave delegowany dostęp tooyour API i adres URL odpowiedzi `https://msmanaged-na.consent.azure-apim.net/redirect`. Zobacz [w tym przykładzie](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) uzyskać więcej szczegółów, podstawiając Twój interfejs API dla hello Azure Resource Manager.

wymagane są następujące wartości konfiguracji Hello:
- **Identyfikator klienta** — Witaj identyfikator klienta łącznika AAD rejestracji
- **Klucz tajny klienta** — klucz tajny klienta na powitania łącznika AAD rejestracji
- **Adres URL logowania** — Witaj podstawowy adres URL usługi AAD. W publicznej Azure zwykle są to `https://login.windows.net`.
- **Identyfikator dzierżawy** — Witaj identyfikator używany do logowania hello toobe dzierżawy hello. Ta powinna być "typowych" lub hello identyfikator dzierżawy hello, w których hello jest tworzony łącznika.
- **Adres URL zasobu** — Witaj adresu URL zasobu Twojej rejestracji usługi AAD zaplecza interfejsu API

> [!IMPORTANT]
> Jeśli innej osoby zaimportować definicję hello interfejsu API w rozwiązaniu PowerApps i Microsoft Flow jako część przepływu ręczne hello, konieczne będzie tooprovide z hello identyfikator i klienta klucz tajny klienta **rejestracji łącznika hello**, jak również jako adres URL zasobu hello interfejsu API. Upewnij się, że tych kluczy tajnych są zarządzane w bezpieczny sposób. **Nie udostępniaj poświadczeń zabezpieczeń hello hello API sam.**

### <a name="generic-oauth-20"></a>Ogólny OAuth 2.0
Hello ogólnego obsługi protokołu OAuth 2.0 umożliwia toointegrate z każdego dostawcy OAuth 2.0. Dzięki temu można toobring w niestandardowego dostawcę, który nie jest obsługiwany natywnie.

wymagane są następujące wartości konfiguracji Hello:
- **Identyfikator klienta** — Witaj identyfikator klienta OAuth 2.0
- **Klucz tajny klienta** — klucz tajny klienta hello OAuth 2.0
- **Adres URL autoryzacji** — Witaj adresu URL autoryzacji OAuth 2.0
- **Adres URL token** — Witaj adresu URL tokenu OAuth 2.0
- **Odśwież adres URL** — Witaj URL odświeżania OAuth 2.0



[zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[zarejestrować i używania niestandardowych łączników w Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
