---
title: "aaaProtect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprotect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Jak tooprotect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API
Witaj, po wideo pokazuje, jak toobuild zaplecza interfejsu API sieci Web i chronić go z usługą Azure Active Directory i zarządzanie interfejsami API przy użyciu protokołu OAuth 2.0.  Ten artykuł zawiera omówienie i dodatkowe informacje dotyczące hello kroki hello wideo. To 24 minutę wideo pokazuje, jak do:

* Tworzenie zaplecza interfejsu API sieci Web i zabezpiecz ją przy użyciu usługi AAD — począwszy od 1:30
* Importowanie hello API zarządzanie interfejsami API — począwszy od 7:10
* Skonfiguruj hello Developer portal toocall hello interfejsu API — począwszy od 9:09
* Konfigurowanie aplikacji komputerowych hello toocall interfejsu API — począwszy od 18:08
* Skonfiguruj toopre zasady sprawdzania poprawności tokenu JWT-autoryzować żądania — począwszy od 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Utwórz katalog usługi Azure AD
toosecure kopii interfejsu API sieci Web przy użyciu usługi Azure Active Directory, musisz najpierw mieć dzierżawę usługi AAD. W tym wideo dzierżawa o nazwie **APIMDemo** jest używany. toocreate dzierżawę usługi AAD logowania toohello [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**Active Katalog**->**katalogu**->**Utwórz niestandardowy**. 

![Usługa Azure Active Directory][api-management-create-aad-menu]

W tym przykładzie katalog o nazwie **APIMDemo** jest tworzony z domyślnej domeny o nazwie **DemoAPIM.onmicrosoft.com**. Ten katalog jest używany w całym hello wideo.

![Usługa Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Tworzenie usługi interfejsu API sieci Web zabezpieczonych przez usługi Azure Active Directory
W tym kroku zaplecza interfejsu API sieci Web jest tworzony przy użyciu programu Visual Studio 2013. W tym kroku hello wideo rozpoczyna się od 1:30. toocreate projektu zaplecza interfejsu API sieci Web w programie Visual Studio kliknij **pliku**->**nowy**->**projektu**i wybierz polecenie **sieci Web ASP.NET Aplikacja** z hello **Web** listy szablonów. W tym wideo hello projektu o nazwie **APIMAADDemo**. Kliknij przycisk **OK** toocreate hello projektu. 

![Visual Studio][api-management-new-web-app]

Kliknij przycisk **interfejsu API sieci Web** z hello **wybierz listę szablonów** toocreate projekt interfejsu API sieci Web. Kliknij tooconfigure uwierzytelniania katalogu Azure **Zmień uwierzytelnianie**.

![Nowy projekt][api-management-new-project]

Kliknij przycisk **konta organizacyjne**, a następnie określ hello **domeny** dzierżawy usługi AAD. W tym hello przykład domena jest **DemoAPIM.onmicrosoft.com**. hello domeny katalogu można je uzyskać z hello **domen** katalogu.

![Domeny][api-management-aad-domains]

Skonfiguruj ustawienia hello potrzebne w hello **Zmień uwierzytelnianie** okno dialogowe i kliknij przycisk **OK**.

![Zmienianie uwierzytelniania][api-management-change-authentication]

Po kliknięciu **OK** programu Visual Studio będzie podejmować tooregister do aplikacji z katalogu usługi Azure AD i może być zostanie wyświetlony monit o toosign w przez program Visual Studio. Zaloguj się przy użyciu konta administracyjnego dla katalogu.

![Zaloguj się tooVisual w Studio][api-management-sign-in-vidual-studio]

tooconfigure pole tego projektu jako hello wyboru interfejsu API sieci Web Azure **Host w chmurze hello** , a następnie kliknij przycisk **OK**.

![Nowy projekt][api-management-new-project-cloud]

Zostanie wyświetlony monit o toosign w tooAzure może być, a następnie można skonfigurować hello aplikacji sieci Web.

![Konfigurowanie][api-management-configure-web-app]

W tym przykładzie nowy **planu usługi aplikacji** o nazwie **APIMAADDemo** jest określona.

Kliknij przycisk **OK** tooconfigure hello aplikacji sieci Web i Utwórz projekt hello.

## <a name="add-hello-code-toohello-web-api-project"></a>Dodaj projekt interfejsu API sieci Web toohello kodu hello
następnym krokiem Hello wideo hello dodaje hello kodu toohello interfejsu API sieci Web projektu. Ten krok zostanie uruchomiony na 4:35.

Witaj interfejsu API sieci Web w tym przykładzie implementuje Kalkulator podstawowe usługi przy użyciu modelu i kontrolera. Kliknij prawym przyciskiem myszy tooadd hello model dla usługi hello, **modele** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**, **klasy**. Nazwa klasy hello `CalcInput` i kliknij przycisk **Dodaj**.

Dodaj następujące hello `using` instrukcji toohello początku hello `CalcInput.cs` pliku.

```c#
using Newtonsoft.Json;
```

Zastąp hello wygenerowane klasy hello następującego kodu.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Kliknij prawym przyciskiem myszy **kontrolerów** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**->**kontrolera**. Wybierz **kontrolera 2 interfejsu API sieci Web — pusty** i kliknij przycisk **Dodaj**. Typ **CalcController** dla hello kontrolera nazwę, a następnie kliknij przycisk **Dodaj**.

![Dodawanie kontrolera][api-management-add-controller]

Dodaj następujące hello `using` instrukcji toohello początku hello `CalcController.cs` pliku.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Zastąp hello wygenerowane klasy kontrolera hello następującego kodu. Ten kod implementuje hello `Add`, `Subtract`, `Multiply`, i `Divide` operacji hello podstawowe Kalkulator interfejsu API.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Naciśnij klawisz **F6** toobuild i sprawdź hello rozwiązania.

## <a name="publish-hello-project-tooazure"></a>Publikowanie hello tooAzure projektu
W ten krok hello Visual Studio projektu jest tooAzure opublikowane. W tym kroku hello wideo rozpoczyna się od 5:45.

toopublish hello tooAzure projektu, kliknij prawym przyciskiem myszy hello **APIMAADDemo** projekt w programie Visual Studio i wybierz pozycję **publikowania**. Zachowaj ustawienia domyślne hello w hello **publikowanie w sieci Web** okno dialogowe i kliknij przycisk **publikowania**.

![Publikowanie w sieci Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Przyznaj uprawnienia aplikacji usługi wewnętrznej bazy danych toohello usługi Azure AD
Nowa aplikacja hello usługi wewnętrznej bazy danych jest tworzony w katalogu usługi Azure AD w ramach konfigurowania hello i proces publikowania projektu interfejsu API sieci Web. W tym kroku hello wideo zaczynając od 6:13 uprawnienia są przyznawane toohello interfejsu API sieci Web zaplecza.

![Aplikacja][api-management-aad-backend-app]

Kliknij nazwę hello hello aplikacji tooconfigure hello wymagane uprawnienia. Przejdź toohello **Konfiguruj** i przewiń w dół toohello **uprawnienia aplikacji tooother** sekcji. Kliknij przycisk hello **uprawnienia aplikacji** listy rozwijanej obok **Windows** **usługi Azure Active Directory**, sprawdź pole hello **odczytuj dane katalogu**i kliknij przycisk **zapisać**.

![Dodaj uprawnienia][api-management-aad-add-permissions]

> [!NOTE]
> Jeśli **Windows** **usługi Azure Active Directory** jest niewymienione w obszarze uprawnienia tooother aplikacji, kliknij przycisk **dodać aplikację** i dodaj go z listy hello.
> 
> 

Zanotuj hello **identyfikator URI aplikacji** do użycia w kolejnym kroku po skonfigurowaniu aplikacji usługi Azure AD do portalu dla deweloperów usługi API Management hello.

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Importowanie hello interfejsu API sieci Web do zarządzania interfejsem API
Interfejsy API są skonfigurowane z hello interfejsu API wydawcy portalu, który jest dostępny za pośrednictwem hello portalu Azure. tooreach, kliknij przycisk **wydawcy portalu** z paska narzędzi hello usługi Zarządzanie interfejsami API. Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [pierwszy interfejs API zarządzania] [ Manage your first API] samouczka.

![Portal wydawcy][api-management-management-console]

Operacje mogą być [ręcznie dodawać tooAPIs](api-management-howto-add-operations.md), lub mogą być importowane. W tym wideo operacje są importowane w formacie struktury Swagger, zaczynając od 6:40.

Utwórz plik o nazwie `calcapi.json` o następującej zawartości i zapisaniu tooyour komputera. Upewnij się, że hello `host` atrybut wskazuje tooyour interfejsu API sieci Web zaplecza. W tym przykładzie `"host": "apimaaddemo.azurewebsites.net"` jest używany.

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

Kalkulator hello tooimport interfejsu API, kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Import API**.

![Przycisk do importowania interfejsu API][api-management-import-api]

Wykonaj następujące kroki tooconfigure hello Kalkulator API hello.

1. Kliknij przycisk **z pliku**, Przeglądaj toohello `calculator.json` można zapisać pliku, a następnie kliknij przycisk hello **Swagger** przycisk radiowy.
2. Typ **obliczenia** do hello **sufiks adresu URL interfejsu API sieci Web** pola tekstowego.
3. Kliknij hello **produktów (opcjonalnie)** polu i wybierz polecenie **Starter**.
4. Kliknij przycisk **zapisać** hello tooimport interfejsu API.

![Dodawanie nowego interfejsu API][api-management-import-new-api]

Po zaimportowaniu hello API hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Wywołanie interfejsu API hello niepomyślnie z portalu dla deweloperów hello
W tym momencie hello interfejsu API został zaimportowany do interfejsu API zarządzania, ale nie można jeszcze można wywołać pomyślnie z portalu dla deweloperów hello ponieważ hello usługi wewnętrznej bazy danych jest chroniony za pomocą uwierzytelniania usługi Azure AD. To jest przedstawiona w hello wideo, zaczynając od 7:40 przy użyciu hello następujące kroki.

Kliknij przycisk **portalu dla deweloperów** z hello prawym górnym rogu strony hello wydawcy portalu.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** i kliknij przycisk hello **Kalkulator** interfejsu API.

![Portal dla deweloperów][api-management-dev-portal-apis]

Kliknij przycisk **wypróbuj**.

![Wypróbuj][api-management-dev-portal-try-it]

Kliknij przycisk **wysyłania** i zwróć uwagę na stan odpowiedzi hello **401 nieautoryzowane**.

![Send][api-management-dev-portal-send-401]

Hello żądania nie ma autoryzacji, ponieważ interfejs API zaplecza hello jest chroniony przez usługę Azure Active Directory. Przed wywołaniem metody interfejsu API hello pomyślnie portalu dla deweloperów hello musi być deweloperzy tooauthorize skonfigurowany przy użyciu protokołu OAuth 2.0. Ten proces jest opisany w hello następujące sekcje.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Zarejestruj portalu dla deweloperów hello jako aplikację AAD
Witaj pierwszym etapem konfigurowania deweloperzy tooauthorize portalu deweloperów hello przy użyciu protokołu OAuth 2.0 jest portalu dla deweloperów hello tooregister jako aplikację AAD. Jest to wykazać, zaczynając od 8:27 hello wideo.

Przejdź dzierżawy toohello usługi Azure AD z pierwszym krokiem hello ten film, w tym przykładzie **APIMDemo** i przejdź toohello **aplikacji** kartę.

![Nowa aplikacja][api-management-aad-new-application-devportal]

Kliknij przycisk hello **Dodaj** przycisk toocreate nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.

![Nowa aplikacja][api-management-new-aad-application-menu]

Wybierz **sieci Web, aplikacji i/lub interfejs API sieci Web**, wprowadź nazwę i kliknij strzałkę dalej hello. W tym przykładzie **APIMDeveloperPortal** jest używany.

![Nowa aplikacja][api-management-aad-new-application-devportal-1]

Aby uzyskać **adres URL logowania** wprowadź adres URL hello usługi API Management i Dołącz `/signin`. W tym przykładzie `https://contoso5.portal.azure-api.net/signin` jest używany.

Aby uzyskać **adres URL identyfikatora aplikacji** wprowadź adres URL hello usługi API Management i Dołącz niektóre unikatowe znaki. Mogą to być wszystkie odpowiednie znaki w tym przykładzie `https://contoso5.portal.azure-api.net/dp` jest używany. Gdy potrzebne hello **właściwości aplikacji** są skonfigurowane, kliknij przycisk hello znacznik wyboru toocreate hello aplikacji.

![Nowa aplikacja][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Konfigurowanie serwera autoryzacji usługi API Management OAuth 2.0
Witaj następnym krokiem jest tooconfigure serwera autoryzacji OAuth 2.0 w usłudze API Management. Ten krok jest przedstawiona w hello wideo, zaczynając od 9:43.

Kliknij przycisk **zabezpieczeń** hello zarządzanie interfejsami API menu po lewej stronie powitania kliknij **OAuth 2.0**, a następnie kliknij przycisk **dodać autoryzacji** serwera.

![Dodawanie serwera autoryzacji][api-management-add-authorization-server]

Wprowadź nazwę i opcjonalny opis w hello **nazwa** i **opis** pola. Te pola są używane tooidentify serwera autoryzacji hello OAuth 2.0 w wystąpieniu usługi Zarządzanie interfejsami API hello. W tym przykładzie **pokaz serwera autoryzacji** jest używany. Później podczas określania toobe serwera OAuth 2.0, używany do uwierzytelniania dla interfejsu API, możesz wybrać tej nazwy.

Dla hello **adres URL strony rejestracji klienta** wprowadź wartość symbolu zastępczego, takich jak `http://localhost`.  Witaj **adres URL strony rejestracji klienta** punktów toohello strony przez użytkowników, można użyć toocreate i skonfiguruj swoje własne konta dla dostawcy OAuth 2.0, które obsługują zarządzanie kontami użytkowników. W tym przykładzie użytkowników nie tworzyć i konfigurować własne konta, więc symbol zastępczy jest używany.

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-1]

Następnie określ **adres URL punktu końcowego autoryzacji** i **adres URL punktu końcowego tokenu**.

![Serwer autoryzacji][api-management-add-authorization-server-1a]

Te wartości można pobrać z hello **punkty końcowe aplikacji** strony hello utworzona dla portalu dla deweloperów hello aplikacji usługi AAD. punkty końcowe hello tooaccess Przejdź toohello **Konfiguruj** hello usługi AAD aplikacji i kliknij polecenie **wyświetlić punkty końcowe**.

![Aplikacja][api-management-aad-devportal-application]

![Wyświetl punkty końcowe][api-management-aad-view-endpoints]

Kopiuj hello **punktu końcowego autoryzacji OAuth 2.0** i wklej go do hello **adres URL punktu końcowego autoryzacji** pola tekstowego.

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2]

Kopiuj hello **punkt końcowy tokenu OAuth 2.0** i wklej go do hello **tokenu końcowego adresu URL** pole tekstowe.

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2a]

Ponadto toopasting w punktu końcowego tokena hello, Dodaj parametr treści dodatkowe o nazwie **zasobów** i wartości hello Użyj hello **identyfikator URI aplikacji** z hello usługi AAD aplikacji hello usługi wewnętrznej bazy danych, który został utworzenia projektu Visual Studio hello został opublikowany.

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

Następnie określ hello poświadczeń klienta. Są to poświadczenia hello zasobu hello tooaccess, w tym przypadku hello portalu dla deweloperów.

![Poświadczenia klienta][api-management-client-credentials]

Witaj tooget **identyfikator klienta**, przejdź toohello **Konfiguruj** kartę hello aplikację AAD dla deweloperów hello hello portalu i skopiuj **identyfikator klienta**.

Witaj tooget **klucz tajny klienta** kliknij hello **wybierz czas trwania** listy rozwijanej w hello **klucze** sekcji i określ interwał. W tym przykładzie używany jest 1 rok.

![Identyfikator klienta][api-management-aad-client-id]

Kliknij przycisk **zapisać** toosave hello konfiguracji oraz wyświetlania hello klucza. 

> [!IMPORTANT]
> Zanotuj tego klucza. Po zamknięciu okna konfiguracji usługi Azure Active Directory hello hello klucza nie może ponownie wyświetlone.
> 
> 

Kopiuj hello klucza toohello Schowka, portal wydawcy wstecz toohello przełącznika, Wklej klucz hello do hello **klucz tajny klienta** polem tekstowym i kliknij przycisk **zapisać**.

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-3]

Bezpośrednio po poświadczeń klienta hello jest udzielania kodu autoryzacji. Skopiuj ten kod autoryzacji i tooyour tyłu przełącznika aplikacji portalu dewelopera usługi Azure AD skonfigurować stronę i wkleić udzielania autoryzacji hello hello **adres URL odpowiedzi** , a następnie kliknij przycisk **zapisać** ponownie.

![Adres URL odpowiedzi][api-management-aad-reply-url]

Witaj następnym krokiem jest tooconfigure hello uprawnienia do portalu dla deweloperów hello usługi AAD aplikacji. Kliknij przycisk **uprawnienia aplikacji** i zaznacz pole hello **odczytuj dane katalogu**. Kliknij przycisk **zapisać** toosave to zmienić, a następnie kliknij przycisk **Dodaj aplikację**.

![Dodaj uprawnienia][api-management-add-devportal-permissions]

Kliknij ikonę wyszukiwania hello, typ **APIM** do hello począwszy od, wybierz **APIMAADDemo**i kliknij przycisk hello toosave znacznik wyboru.

![Dodaj uprawnienia][api-management-aad-add-app-permissions]

Kliknij przycisk **delegowane uprawnienia** dla **APIMAADDemo** i zaznacz pole hello **APIMAADDemo dostępu**i kliknij przycisk **zapisać**. Dzięki temu deweloper hello usługi zaplecza hello tooaccess aplikacji portalu.

![Dodaj uprawnienia][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Włącz autoryzację użytkownika OAuth 2.0 na powitania Kalkulator interfejsu API
Teraz, gdy hello OAuth 2.0 serwer jest skonfigurowany, możesz je określić w hello ustawienia zabezpieczeń dla interfejsu API. Ten krok jest przedstawiona w hello wideo, zaczynając od 14:30.

Kliknij przycisk **interfejsów API** w hello menu po lewej stronie i kliknij przycisk **Kalkulator** tooview i jego ustawień.

![Kalkulator interfejsu API][api-management-calc-api]

Przejdź toohello **zabezpieczeń** pozycję Sprawdź hello **OAuth 2.0** pole wyboru, wybierz powitania serwera autoryzacji żądany z hello **serwera autoryzacji** listy rozwijanej i kliknij przycisk **Zapisać**.

![Kalkulator interfejsu API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Pomyślne wywołanie hello Kalkulator interfejsu API z portalu dla deweloperów hello
Teraz, gdy autoryzacji OAuth 2.0 hello jest skonfigurowany na powitania interfejsu API, jego operacji może pomyślnie wywołana z Centrum deweloperów hello. Ten krok jest przedstawiona w hello wideo, zaczynając od 15:00.

Przejdź wstecz toohello **Dodaj dwie liczb całkowitych** operacji usługi Kalkulator hello w portalu dla deweloperów hello i kliknij **wypróbuj**. Uwaga hello nowy element hello **autoryzacji** sekcji odpowiedniego serwera autoryzacji toohello właśnie został dodany.

![Kalkulator interfejsu API][api-management-calc-authorization-server]

Wybierz **kod autoryzacji** z autoryzacji hello listy rozwijanej liście, a następnie wprowadź poświadczenia hello hello toouse konta. Jeśli nastąpiło już zalogowanie się przy użyciu konta hello może nie być wyświetlony monit.

![Kalkulator interfejsu API][api-management-devportal-authorization-code]

Kliknij przycisk **wysyłania** i hello Uwaga **stanu odpowiedzi** z **200 OK** i hello wyniki operacji hello hello zawartości odpowiedzi.

![Kalkulator interfejsu API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Konfigurowanie aplikacji komputerowych hello toocall interfejsu API
Witaj następnej procedury w hello wideo rozpoczyna się od 16:30 i konfiguruje prostą aplikację pulpitu hello toocall interfejsu API. pierwszym krokiem Hello jest tooregister hello aplikację w usłudze Azure AD i nadaj mu dostępu toohello katalogu i toohello usługi wewnętrznej bazy danych. Na 18:25 istnieje Przykładowa aplikacja hello podczas wywoływania operacji na powitania Kalkulator interfejsu API.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Skonfiguruj toopre zasady sprawdzania poprawności tokenu JWT-autoryzować żądania
Witaj ostatnia procedura hello wideo rozpoczyna się od 20:48 i pokazano, jak toouse hello [JWT do zweryfikowania](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre zasad-autoryzować żądania weryfikując hello tokenów dostępu dla każdego żądania przychodzącego. Jeśli Żądanie hello nie jest weryfikowany przez hello zasady sprawdzania poprawności tokenów JWT, Żądanie hello jest blokowany przez interfejs API zarządzania i nie są przekazywane toohello wewnętrznej bazy danych.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Aby innego demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too13:50. Szybkie przewijanie do przodu too15:00 zasady hello toosee skonfigurowane w edytorze zasad hello, a następnie too18:50 dla pokaz wywołanie operacji z portalu dla deweloperów hello zarówno z i bez hello wymagany token autoryzacji.

## <a name="next-steps"></a>Następne kroki
* Zapoznaj się z kilku [wideo](https://azure.microsoft.com/documentation/videos/index/?services=api-management) o zarządzanie interfejsami API.
* Dla innych sposobów toosecure usługi wewnętrznej bazy danych, zobacz [uwierzytelnianie wzajemne certyfikatu](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
