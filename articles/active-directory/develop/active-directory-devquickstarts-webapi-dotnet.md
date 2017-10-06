---
title: aaaAzure AD .NET sieci web interfejsu API wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejs API sieci web .NET MVC która integruje się z usługą Azure AD do uwierzytelniania i autoryzacji."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Zabezpieczanie interfejsu API sieci web za pomocą tokenów elementu nośnego z usługi Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Jeśli tworzysz aplikację, która zapewnia dostęp do zasobów tooprotected należy tooknow jak tooprevent nieuzasadnione uzyskiwać dostęp do zasobów toothose.
Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie toohelp chronić interfejsu API sieci web przy użyciu tokenów dostępu do elementu nośnego OAuth 2.0 tylko kilka wierszy kodu.

W aplikacji sieci web ASP.NET można osiągnąć tę ochronę za pomocą implementacja firmy Microsoft hello hello społeczność oprogramowania pośredniczącego OWIN uwzględnione w programie .NET Framework 4.5. W tym miejscu użyjemy toobuild OWIN interfejs API sieci web "tooDo listy" który:

* Określa, które interfejsy API są chronione.
* Sprawdza, czy hello wywołania interfejsu API sieci web zawiera tokenu dostępu prawidłowe.

tooDo hello toobuild listy interfejsu API, musisz najpierw:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji.
3. Konfigurowanie klienta aplikacji toocall hello interfejsu API sieci web.

Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Każdy jest rozwiązanie Visual Studio 2013. Należy również dzierżawa usługi Azure AD, w których tooregister aplikacji. Jeśli nie masz już, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Krok 1: Rejestrowanie aplikacji w usłudze Azure AD
toohelp zabezpieczyć aplikację, należy najpierw toocreate aplikację w dzierżawie i dostarczają usługi Azure AD kilka kluczowych informacji.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Na górnym pasku powitania kliknij swoje konto. W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.

3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.

4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.

5. Postępuj zgodnie z monitami hello i utworzyć nową **aplikacji sieci Web i/lub interfejs API sieci Web**.
  * **Nazwa** opisuje toousers Twojej aplikacji. Wprowadź **tooDo usługi listy**.
  * **Identyfikator Uri przekierowania** inną schemat i ciąg tooreturn dowolne tokeny zażądał aplikacja korzysta z usługi Azure AD. Wprowadź `https://localhost:44321/` dla tej wartości.

6. Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji. Wprowadź identyfikator specyficznego dla dzierżawy. Na przykład wprowadź wartość `https://contoso.onmicrosoft.com/TodoListService`.

7. Zapisz konfigurację hello. Pozostaw portalu hello otwarty, ponieważ potrzebna będzie również tooregister aplikacja kliencka wkrótce.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Krok 2: Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji
przychodzące żądania toovalidate i tokeny należy tooset się toocommunicate Twojej aplikacji z usługą Azure AD.

1. toobegin, otwórz rozwiązanie hello i Dodaj projekt TodoListService toohello pakiety NuGet hello OWIN oprogramowanie pośredniczące przy użyciu konsoli Menedżera pakietów hello.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Dodaj OWIN klasy toohello TodoListService projekt startowy o nazwie `Startup.cs`.  Projekt powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** > **nowy element**, a następnie wyszukaj **OWIN**. oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.

3. Zmiana deklaracji klasy hello zbyt`public partial class Startup`. Już zaimplementowano część tej klasy dla Ciebie w innym pliku. W hello `Configuration(…)` metody wywoływania zbyt`ConfgureAuth(…)` tooset się uwierzytelniania dla aplikacji sieci web.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(…)` metody. Witaj parametrów, które należy podać w `WindowsAzureActiveDirectoryBearerAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Teraz można używać `[Authorize]` toohelp atrybutów ochrony kontrolerów i akcji z uwierzytelniania elementu nośnego tokenu Web JSON (JWT). Dekoracji hello `Controllers\TodoListController.cs` klasy z tagiem autoryzacji. Spowoduje to wymuszenie hello toosign użytkownika w przed uzyskaniem dostępu do tej strony.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden hello `TodoListController` interfejsów API, akcja hello mogą muszą uzyskiwać dostęp do tooinformation o hello wywołującego. OWIN zapewnia dostęp toohello oświadczenia w tokenie hello elementu nośnego za pośrednictwem hello `ClaimsPrincpal` obiektu.  

6. Typowe wymagania dotyczące interfejsów API sieci web jest hello toovalidate "zakresy" występuje w tokenie hello. Dzięki temu użytkownik hello zgodził toohello uprawnienia wymagane tooaccess hello tooDo usługi listy.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Otwórz hello `web.config` plików w katalogu głównym hello hello TodoListService projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.
  * `ida:Tenant`to nazwa hello dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.
  * `ida:Audience`jest hello identyfikator URI aplikacji hello, wprowadzony w portalu Azure hello aplikacji.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Krok 3: Konfigurowanie aplikacji klienta i uruchamianie usługi hello
Zanim zobaczysz hello tooDo usługi listy w akcji, potrzebujesz tooconfigure hello tooDo listy klienta, można uzyskać tokenów z usługi Azure AD i wprowadzić wywołania toohello usługi.

1. Przejdź wstecz toohello [portalu Azure](https://portal.azure.com).

2. Utwórz nową aplikację w dzierżawie usługi Azure AD, a następnie wybierz **natywną aplikację kliencką** hello wynikowego wiersza.
  * **Nazwa** opisuje toousers Twojej aplikacji.
  * Wprowadź `http://TodoListClient/` dla hello **identyfikator Uri przekierowania** wartość.

3. Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji. Ta wartość jest potrzebny w następnych krokach hello, dlatego skopiuj go ze strony aplikacji hello.

4. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**. Zlokalizuj i wybierz tooDo hello usługi listy i Dodaj hello **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**, a następnie kliknij przycisk **gotowe**.

5. W programie Visual Studio Otwórz `App.config` w hello TodoListClient projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.

  * `ida:Tenant`to nazwa hello dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.
  * `ida:ClientId`jest identyfikator aplikacji hello skopiowany z hello portalu Azure.
  * `todo:TodoListResourceId`Identyfikator URI aplikacji hello tooDo aplikacji z listy, wprowadzony w portalu Azure hello hello jest.

## <a name="next-steps"></a>Następne kroki
Ponadto wyczyścić, skompilować i uruchomić każdy projekt. Jeśli nie jest jeszcze teraz jest toocreate czas hello nowego użytkownika w dzierżawie z *. onmicrosoft.com domeny. Zaloguj się toohello tooDo listy klienta z użytkownikiem, a następnie dodaj listy zadań do wykonania niektórych zadań toohello użytkownika.

Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Możesz teraz przejść na toomore tożsamości scenariuszy.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
