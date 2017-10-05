---
title: "Eksportowanie interfejs API hostowanymi na platformie Azure do PowerApps i przepływów Microsoft | Dokumentacja firmy Microsoft"
description: "Omówienie sposobu uwidacznia interfejs API hostowany w usłudze App Service w rozwiązaniu PowerApps i Flow firmy Microsoft"
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
ms.openlocfilehash: 0d166a2e5b60c3b9f911f9fc3ad49ad7f252abb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-an-azure-hosted-api-to-powerapps-and-microsoft-flow"></a>Eksportowanie interfejs API hostowanymi na platformie Azure do PowerApps i przepływów firmy Microsoft

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Tworzenie niestandardowych łączniki dla PowerApps i Flow firmy Microsoft

[Rozwiązanie PowerApps](https://powerapps.com) to usługa do tworzenia i używania aplikacji biznesowych niestandardowych, Połącz z danymi, które działają na różnych platformach. [Microsoft Flow](https://flow.microsoft.com) można łatwo automatyzować przepływy pracy i procesy biznesowe między ulubionych aplikacji i usług. Zarówno PowerApps i Microsoft Flow wyposażone w szereg łączników do źródeł danych, takich jak usługi Office 365, Dynamics 365 Salesforce i więcej. Jednak użytkownicy również muszą mieć możliwość wykorzystania źródeł danych i interfejsów API konstruowany przez organizację.

Podobnie deweloperów, które mają być ujawnia swoje interfejsy API szerzej w organizacji może być konieczne udostępnienie ich interfejsów API użytkownikom PowerApps i Flow firmy Microsoft. W tym temacie opisano, jak do udostępnienia interfejsu API z usługi aplikacji Azure lub usługi Azure Functions do PowerApps i Flow firmy Microsoft. [Usługa aplikacji Azure](https://azure.microsoft.com/services/app-service/) jest ofertę platformy jako usługa, która umożliwia deweloperom szybkie i łatwe tworzenie aplikacji interfejsu API, mobilne i sieci web korporacyjnej. [Środowisko Azure Functions](https://azure.microsoft.com/services/functions/) to rozwiązanie oparte na zdarzeniu niekorzystającą obliczeniowe, które pozwala na szybkie kodu autora mogą reagować na inne części systemu i skali na podstawie zapotrzebowania.

Aby dowiedzieć się więcej na temat tych usług, zobacz:
- [Rozwiązanie PowerApps z przewodnikiem Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Uczenie z przewodnikiem przepływu firmy Microsoft](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Co to jest usługa App Service?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Co to jest Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Udostępnianie definicji interfejsu API

Interfejsy API są często opisane przy użyciu [dokumentu OpenAPI](https://www.openapis.org/) (czasem określana jako dokument "Swagger"). Zawiera wszystkie informacje, jakie operacje są dostępne i struktury danych. PowerApps i Microsoft Flow można tworzyć niestandardowe łączniki dla każdego dokumentu OpenAPI 2.0. Po utworzeniu niestandardowego łącznika można dokładnie tak samo jak jedną z wbudowanych łączników i szybko można zintegrować aplikacji.

Azure App Service i usługi Azure Functions [wbudowana obsługa](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) do tworzenia i zarządzania dokumentami OpenAPI hostingu. Aby utworzyć niestandardowy łącznik dla sieci web, mobilnych, interfejsu API lub funkcji aplikacji, PowerApps i przepływów muszą mieć kopię definicji.

> [!NOTE]
> Ponieważ kopię definicji interfejsu API jest używany z PowerApps i Microsoft Flow nie będą od razu wiedzieć o aktualizacje i zmiany podziału do aplikacji. Jeśli nowa wersja interfejsu API jest dostępny, należy powtórzyć te kroki dla nowej wersji. 

Aby zapewnić PowerApps i Microsoft Flow hostowanej definicji interfejsu API dla aplikacji, wykonaj następujące kroki:

1. Otwórz [Azure Portal](https://portal.azure.com) i przejdź do aplikacji usługi aplikacji lub usługi Azure Functions.

    Jeśli przy użyciu usługi Azure App Service, wybierz **definicji interfejsu API** na liście ustawień. 
    
    Jeśli używasz usługi Azure Functions, wybierz aplikację funkcji, a następnie wybierz **funkcji platformy**, a następnie **definicji interfejsu API**. Można również wybrać otwieranie **definicji interfejsu API (wersja zapoznawcza)** karcie zamiast tego.

2. Jeśli podano definicji interfejsu API, zobaczysz **wyeksportować do rozwiązania PowerApps + Microsoft Flow** przycisku. Kliknij ten przycisk, aby rozpocząć proces eksportu.

3. Wybierz **Eksport tryb**. Określa czynności, które należy wykonać, aby utworzyć łącznik. Usługa App Service oferuje dwie opcje dostarczanie PowerApps i Microsoft Flow definicja interfejsu API:

    **Express** umożliwia tworzenie niestandardowych łącznik z portalu Azure. Wymaga to, że bieżącej zalogowany użytkownik ma uprawnienia do tworzenia łączników w środowisku docelowym. Jest to zalecane podejście, jeśli ten wymóg może zostać spełniony. Jeśli ten tryb jest używany, wykonaj [Express eksportu](#express) poniższe instrukcje.

    **Ręczne** umożliwia eksportowanie kopii definicji interfejsu API, które można zaimportować przy użyciu portali rozwiązania PowerApps lub Flow firmy Microsoft. Jest to zalecane podejście, jeśli użytkowników platformy Azure i użytkownik z uprawnieniami do tworzenia łączników są różne osoby, lub Jeśli łącznik musi zostać utworzona w innej dzierżawie. Jeśli ten tryb jest używany, wykonaj [ręczne eksportu i importu](#manual) poniższe instrukcje.

<a name="express"></a>
## <a name="express-export"></a>Express eksportu

W tej sekcji utworzysz nowego niestandardowego łącznika z w portalu Azure. Użytkownik musi być zalogowany do dzierżawy, do którego chcesz wyeksportować, a musi mieć uprawnienia do tworzenia niestandardowego łącznika w środowisku docelowym.

1. Wybierz środowisko, w którym chcesz utworzyć łącznik. Następnie podaj nazwę łącznik niestandardowy.

2. Jeśli definicja interfejsu API zawiera żadnych definicji zabezpieczeń, to zostanie wywołana w kroku #2. Jeśli to konieczne, podaj szczegóły konfiguracji zabezpieczeń, konieczne jest zezwolenie użytkownikom na dostęp do interfejsu API. Aby uzyskać więcej informacji, zobacz [uwierzytelniania](#auth) poniżej. 

3. Kliknij przycisk **OK** można utworzyć łącznik niestandardowy.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Ręczne eksportu i importu

Aby utworzyć niestandardowy łącznik dla sieci web, mobilnych, interfejsu API lub funkcji aplikacji, będą potrzebne dwa kroki:

1. [Pobieranie definicji interfejsu API z usługi aplikacji lub usługi Azure Functions](#export)
2. [Importowanie definicji interfejsu API PowerApps i Flow firmy Microsoft](#import)

Istnieje możliwość, że te dwa kroki należy przeprowadzane przez oddzielne osób w organizacji, jako określony użytkownik może nie mieć uprawnień do wykonania obu czynności. W takim przypadku deweloperze, który ma współautora dostęp do aplikacji usługi aplikacji lub usługi Azure Functions trzeba uzyskać definicji interfejsu API (pojedynczy plik JSON) lub do niej łącza. Następnie należy podać tej definicji do właściciela rozwiązania PowerApps lub Flow firmy Microsoft. Tego właściciela umożliwia utworzenie łącznika niestandardowych metadanych.

<a name="export"></a>
### <a name="retrieving-the-api-definition-from-app-service-or-azure-functions"></a>Pobieranie definicji interfejsu API z usługi aplikacji lub usługi Azure Functions

W tej sekcji będzie eksportować definicji interfejsu API dla aplikacji usługi interfejsu API, do użycia później w rozwiązaniu PowerApps lub Microsoft Flow portalu.

1. Można albo **Pobierz definicję interfejsu API** lub **Uzyskaj link**. Jeżeli wybierzesz, wynik będzie znajdować się w następnej sekcji. Wybierz jedną z tych opcji i postępuj zgodnie z instrukcjami.
 
2. Jeśli definicja interfejsu API zawiera żadnych definicji zabezpieczeń, to zostanie wywołana w kroku #2. Podczas importowania PowerApps i Microsoft Flow wykryje to i wyświetli monit o podanie informacji o zabezpieczeniach. Zbierz poświadczenia związane z każdej definicji do użycia w następnej sekcji. Aby uzyskać więcej informacji, zobacz [uwierzytelniania](#auth) poniżej. 

<a name="import"></a>
### <a name="importing-the-api-definition-into-powerapps-and-microsoft-flow"></a>Importowanie definicji interfejsu API PowerApps i Flow firmy Microsoft

W tej sekcji utworzysz niestandardowego łącznika w rozwiązaniu PowerApps i Flow firmy Microsoft przy użyciu definicji interfejsu API uzyskany wcześniej. Niestandardowe łączników są współużytkowane przez dwie usługi, więc musisz zaimportować definicję raz. Aby uzyskać więcej informacji na łączników niestandardowych, zobacz [zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps] i [zarejestrować i używania niestandardowych łączników w Microsoft Flow].

1. Otwórz [portalu sieci web w rozwiązaniu Powerapps](https://web.powerapps.com) lub [portalu sieci web Microsoft Flow](https://flow.microsoft.com/)i zaloguj się. 

2. Kliknij przycisk **ustawienia** przycisk (koło zębate ikonę) w prawym górnym rogu strony i wybierz **łączniki niestandardowe**. 

3. Kliknij przycisk **Tworzenie niestandardowego łącznika**.

4. Na **ogólne** karcie, podaj nazwę dla interfejsu API, a następnie przekaż definicji OpenAPI lub wklej adres URL metadanych. Kliknij przycisk **kontynuować**.

4. Na **zabezpieczeń** karcie, jeśli zostanie wyświetlony monit, aby podać szczegóły uwierzytelnianie, wprowadź wartości uzyskane w poprzedniej sekcji. Jeśli nie, przejdź do następnego kroku.

5. Na **definicje** , wszystkie operacje określone w pliku OpenAPI są wypełniane automatycznie. Jeśli wszystkie wymagane operacje są zdefiniowane, można przejść do następnego kroku. Jeśli nie, można dodawać i modyfikować tutaj operacji.

6. Kliknij przycisk **utworzyć łącznik**. Jeśli chcesz przetestować wywołań interfejsu API, przejdź do następnego kroku.

7. Na **Test** , Utwórz połączenie, wybierz operację, aby przetestować, a następnie wprowadzić wszelkich danych wymaganych przez operację.

8. Kliknij przycisk **Operacja testowania**.


<a name="auth"></a>
## <a name="authentication"></a>Authentication

PowerApps i Microsoft Flow obsługują kolekcja dostawców tożsamości, które mogą być używane do logowania użytkowników łącznik niestandardowy. Jeśli Twój interfejs API wymaga uwierzytelnienia, upewnij się, że jest przechwytywany jako _definicji zabezpieczeń_ w dokumencie OpenAPI. Podczas eksportowania należy podać wartości konfiguracji, które umożliwia rozwiązanie PowerApps Flow firmy Microsoft do wykonania akcji logowania.

W tej sekcji opisano typy uwierzytelniania, które są obsługiwane przez express przepływu: klucz interfejsu API, Azure Active Directory i rodzajowy OAuth 2.0. Pełną listę dostawców i każda wymaga poświadczeń, zobacz [zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps] i [zarejestrować i używania niestandardowych łączników w Microsoft Flow].

### <a name="api-key"></a>Klucz interfejsu API
W przypadku tego systemu zabezpieczeń użytkowników łącznika wyświetli monit o podanie klucza podczas tworzenia połączenia. Możesz podać nazwa klucza interfejsu API, aby go poinformować, klucz, do którego jest potrzebny. Dla usługi Azure Functions zazwyczaj będzie jeden z kluczy hosta, obejmujące kilka funkcji w funkcji aplikacji.

### <a name="azure-active-directory"></a>Usługa Azure Active Directory
Podczas konfigurowania łącznika niestandardowego, który wymaga logowania usługi AAD, wymagane są dwa rejestracji aplikacji usługi AAD: jeden do modelowania zaplecza interfejsu API, a drugi do modelowania łącznika w rozwiązaniu PowerApps i przepływów.

Interfejs API powinny być skonfigurowane do pracy z pierwszej rejestracji, a to będzie już można podjąć się jeśli użyto [uwierzytelniania/autoryzacji dla aplikacji usługi](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) funkcji.

Konieczne będzie ręczne tworzenie rejestracji drugi łącznik, wykonując kroki opisane w [Dodawanie aplikacji AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Rejestracja musi mieć delegowane dostęp do interfejsu API i adres URL odpowiedzi `https://msmanaged-na.consent.azure-apim.net/redirect`. Zobacz [w tym przykładzie](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) uzyskać więcej szczegółów, podstawiając Twój interfejs API usługi Azure Resource Manager.

Wymagane są następujące wartości konfiguracji:
- **Identyfikator klienta** — identyfikator klienta łącznika AAD rejestracji
- **Klucz tajny klienta** — klucz tajny klienta łącznika AAD rejestracji
- **Adres URL logowania** — podstawowy adres URL dla usługi AAD. W publicznej Azure zwykle są to `https://login.windows.net`.
- **Identyfikator dzierżawy** — identyfikator dzierżawcy do użycia dla danych logowania. Powinno to być "typowych" lub identyfikator dzierżawy, w którym jest tworzona łącznika.
- **Adres URL zasobu** — adres URL zasobu Twojej rejestracji usługi AAD zaplecza interfejsu API

> [!IMPORTANT]
> Jeśli innej osoby zaimportować definicję interfejsu API w rozwiązaniu PowerApps i Microsoft Flow jako część przepływu ręczne, należy podać je z Identyfikatorem klienta i klucz tajny klienta **rejestracji łącznika**, a także adres URL zasobu interfejsu API. Upewnij się, że tych kluczy tajnych są zarządzane w bezpieczny sposób. **Nie udostępniaj poświadczenia zabezpieczeń samego interfejsu API.**

### <a name="generic-oauth-20"></a>Ogólny OAuth 2.0
Ogólny obsługi protokołu OAuth 2.0 umożliwia integrację z każdego dostawcy OAuth 2.0. Dzięki temu można przenieść niestandardowego dostawcę, który nie jest obsługiwany natywnie.

Wymagane są następujące wartości konfiguracji:
- **Identyfikator klienta** — identyfikator klienta OAuth 2.0
- **Klucz tajny klienta** — klucz tajny klienta OAuth 2.0
- **Adres URL autoryzacji** -adresu URL autoryzacji OAuth 2.0
- **Adres URL token** — adres URL tokenu OAuth 2.0
- **Odśwież adres URL** — adres URL odświeżania OAuth 2.0



[zarejestrować i używanie łączników niestandardowych w rozwiązaniu PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[zarejestrować i używania niestandardowych łączników w Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
