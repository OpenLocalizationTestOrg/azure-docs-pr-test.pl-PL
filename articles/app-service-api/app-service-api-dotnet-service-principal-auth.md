---
title: "Uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak chronić aplikację interfejsu API w usłudze Azure App Service dla scenariuszy service-to-service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób korzystania z usługi aplikacji uwierzytelniania dla *wewnętrzny* dostęp do aplikacji interfejsu API. Scenariusz wewnętrzny jest, gdzie masz aplikację interfejsu API, które mają być dostępne tylko przez kod aplikacji. Zalecanym sposobem wdrożenia tego scenariusza, w usłudze App Service jest o nazwie aplikacji interfejsu API ochrony przy użyciu usługi Azure AD. Należy wywołać chronionej aplikacji interfejsu API z tokenu elementu nośnego, który można pobrać z usługi Azure AD przez udostępnienie tożsamość aplikacji poświadczeń (nazwy głównej usługi). Wariantów przy użyciu usługi Azure AD, zobacz **do usługi uwierzytelniania** sekcji [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

W tym artykule dowiesz się:

* Jak używać usługi Azure Active Directory (Azure AD) do ochrony aplikacji interfejsu API przed nieuwierzytelnionym dostępem.
* Jak korzystać z chronionej aplikacji interfejsu API z aplikacji interfejsu API, aplikacji sieci web lub aplikacji mobilnej przy użyciu poświadczeń podmiotu zabezpieczeń (tożsamość aplikacji) usługi Azure AD. Aby uzyskać informacje o sposobie korzystania z aplikacji logiki, zobacz [przy użyciu niestandardowego interfejsu API hostowanych w usłudze aplikacji z usługą Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).
* Jak upewnij się, że chronionej aplikacji interfejsu API nie można wywołać z poziomu przeglądarki przy zalogowanych użytkowników.
* W jaki sposób upewnij się, że chronionej aplikacji interfejsu API można wywołać tylko przez określonych Azure AD service principal.

Ten artykuł zawiera dwie sekcje:

* [Jak skonfigurować usługę podmiotu zabezpieczeń uwierzytelniania w usłudze Azure App Service](#authconfig) sekcji wyjaśniono, ogólnie rzecz biorąc, jak skonfigurować uwierzytelnianie dla dowolnej aplikacji interfejsu API oraz sposób korzystać z chronionej aplikacji interfejsu API. Ta sekcja dotyczy jednakowo do wszystkich platform obsługiwanych przez usługę App Service, w tym .NET, Node.js i Java.
* Począwszy od [kontynuowanie samouczki dotyczące rozpoczynania pracy .NET](#tutorialstart) sekcji samouczka instrukcje konfigurowania scenariusza "dostęp do" przykładową aplikację .NET w aplikacji usługi. 

## <a id="authconfig"></a>Jak skonfigurować usługę podmiotu zabezpieczeń uwierzytelniania w usłudze Azure App Service
Ta sekcja zawiera ogólne instrukcje, które są stosowane do wszystkich aplikacji interfejsu API. Dla określonego kroki, aby do .NET listy czy przykładowej aplikacji, przejdź do [kontynuowanie serii samouczek aplikacji interfejsu API programu .NET](#tutorialstart).

1. W [portalu Azure](https://portal.azure.com/), przejdź do **ustawienia** bloku aplikacji interfejsu API, który chcesz chronić, a następnie znajdź **funkcje** sekcji, a następnie kliknij przycisk  **Uwierzytelnianie / autoryzacja**.
   
    ![Uwierzytelnianie/autoryzację, w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. W **działania należy podjąć w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory** .
4. W obszarze **dostawców uwierzytelniania**, wybierz pozycję **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Skonfiguruj **ustawień usługi Azure Active Directory** bloku, aby utworzyć nową aplikację usługi Azure AD, lub użyj istniejącej aplikacji usługi Azure AD, jeśli masz już konto, którego chcesz używać.
   
    Scenariusze wewnętrzny zwykle obejmują wywołanie aplikacji interfejsu API aplikacji interfejsu API. Oddzielne Azure można użyć tylko jednej aplikacji usługi Azure AD lub aplikacji usługi AD dla każdej aplikacji interfejsu API.
   
    Aby uzyskać szczegółowe informacje dotyczące tego bloku, zobacz [sposobu konfigurowania aplikacji usługi aplikacji do użycia usługi Azure Active Directory logowania](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Po zakończeniu korzystania z bloku konfiguracji dostawcy uwierzytelniania, kliknij przycisk **OK**.
7. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Po zakończeniu App Service tylko zezwala na żądania pochodzące z wywołań w skonfigurowanego dzierżawy usługi Azure AD. Brak kodu uwierzytelniania i autoryzacji jest wymagany w chronionej aplikacji interfejsu API. Token elementu nośnego, są przekazywane do aplikacji interfejsu API wraz z powszechnie oświadczeń używanych w nagłówkach HTTP, a może odczytywać dane kod, aby sprawdzić, czy żądania są z określonego obiektu wywołującego, takich jak nazwy głównej usługi.

Ta funkcja uwierzytelniania działa tak samo dla wszystkich języków, które obsługuje usługi aplikacji, w tym .NET, Node.js i Java. 

#### <a name="how-to-consume-the-protected-api-app"></a>Jak korzystać z chronionej aplikacji interfejsu API
Obiekt wywołujący musi dostarczyć token elementu nośnego usługi Azure AD wywołań interfejsu API. Do pobrania tokenu elementu nośnego przy użyciu poświadczenia główne, wywołujący korzysta z biblioteki uwierzytelniania usługi Active Directory (ADAL dla [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), lub [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). Aby uzyskać token, kod, który wywołuje ADAL zawiera do biblioteki ADAL następujące informacje:

* Nazwa dzierżawy usługi Azure AD.
* Identyfikator klienta i klucz tajny klienta (klucz aplikacji) skojarzone z funkcją wywołującą aplikacji usługi Azure AD.
* Identyfikator klienta aplikacji usługi Azure AD skojarzonej z chronionej aplikacji interfejsu API. (Jeśli jest używany tylko jednej aplikacji usługi Azure AD, to ten sam identyfikator klienta, jak dla obiekt wywołujący.)

Te wartości są dostępne na stronach usługi Azure AD [klasycznego portalu Azure](https://manage.windowsazure.com/).

Po uzyskano token, wywołujący obejmuje żądań HTTP w nagłówku autoryzacji.  Usługi aplikacji sprawdza poprawność tokenu i umożliwia żądań do chronionej aplikacji interfejsu API.

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a>Ochrona aplikacji interfejsu API przed dostępem użytkowników w tej samej dzierżawy
Tokenów elementu nośnego dla użytkowników w tej samej dzierżawy są uznawane za prawidłowe dla chronionej aplikacji interfejsu API.  Jeśli chcesz upewnić się, że tylko nazwy głównej usługi można wywołać chronionej aplikacji interfejsu API, należy dodać kodu w chronionej aplikacji interfejsu API do sprawdzania poprawności następujących oświadczeń z tokenu:

* `appid`powinien być identyfikator klienta aplikacji usługi Azure AD, która jest skojarzona z funkcją wywołującą. 
* `oid`(`objectidentifier`) powinna być identyfikator podmiotu zabezpieczeń usługi obiektu wywołującego. 

Usługi aplikacji są także `objectidentifier` oświadczeń nagłówka X-MS-CLIENT-podmiot zabezpieczeń-ID.

### <a name="how-to-protect-the-api-app-from-browser-access"></a>Ochrona aplikacji interfejsu API z dostęp za pomocą przeglądarki
Jeśli nie można zweryfikować oświadczenia w kodzie w chronionej aplikacji interfejsu API i używać oddzielnego aplikacji usługi Azure AD dla chronionej aplikacji interfejsu API, upewnij się, że adres URL odpowiedzi aplikacji usługi Azure AD nie jest taki sam jak podstawowy adres URL aplikacji interfejsu API. Jeśli adres URL odpowiedzi wskazuje bezpośrednio do chronionej aplikacji interfejsu API, użytkowników w tej samej dzierżawy usługi Azure AD można przejść do aplikacji interfejsu API, zaloguj się na i pomyślnie wywołać interfejs API.

## <a id="tutorialstart"></a>Kontynuowanie serii samouczek aplikacji interfejsu API programu .NET
Jeśli korzystasz z serii samouczek środowiska Node.js lub Java dla aplikacji interfejsu API, przejdź do [następne kroki](#next-steps) sekcji. 

W dalszej części tego artykułu nadal serii samouczek aplikacji interfejsu API programu .NET i przyjęto założenie, że zostały wykonane [samouczek uwierzytelniania użytkownika](app-service-api-dotnet-user-principal-auth.md) i przykładowej aplikacji działających na platformie Azure z włączone uwierzytelnianie użytkownika.

## <a name="set-up-authentication-in-azure"></a>Konfigurowanie uwierzytelniania w systemie Azure
W tej sekcji można skonfigurować usługi aplikacji tak, aby tylko żądania HTTP, umożliwia uzyskanie aplikacji interfejsu API warstwy danych są tymi, które mają prawidłowy Azure AD tokenów elementu nośnego. 

W poniższej sekcji skonfigurujesz aplikacji interfejsu API warstwy środkowej do wysyłania poświadczeń aplikacji do usługi Azure AD, wrócić tokenu elementu nośnego i Wyślij token elementu nośnego w aplikacji interfejsu API warstwy danych. Ten proces przedstawiono na schemacie.

![Diagram uwierzytelniania usługi](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Jeśli wystąpiły problemy podczas zgodnie z instrukcjami samouczka zobacz [Rozwiązywanie problemów](#troubleshooting) sekcji na końcu samouczka. 

1. W [portalu Azure](https://portal.azure.com/), przejdź do **ustawienia** bloku aplikacji interfejsu API, które utworzono dla aplikacji interfejsu API ToDoListDataAPI (warstwy danych), a następnie kliknij przycisk **ustawienia**.
2. W **ustawienia** bloku znaleźć **funkcje** sekcji, a następnie kliknij przycisk **uwierzytelniania / autoryzacji**.
   
    ![Uwierzytelnianie/autoryzację, w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
4. W **działania należy podjąć w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory**.
   
    To ustawienie powoduje, że usługi aplikacji w celu zapewnienia tylko uwierzytelnienia żądania reach aplikacji interfejsu API. Dla żądania, które mają tokenów elementu nośnego prawidłowe usługi aplikacji przekazuje tokeny wzdłuż w aplikacji interfejsu API i wypełnia nagłówków HTTP z często używanych oświadczeń do łatwo udostępnić te informacje w kodzie.
5. W obszarze **dostawców uwierzytelniania**, kliknij przycisk **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. W **ustawień usługi Azure Active Directory** bloku, kliknij przycisk **Express**.
   
    Z **Express** opcji Azure można automatycznie utworzyć aplikację AAD w usługi Azure AD [dzierżawy](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Nie masz utworzyć dzierżawcę, ponieważ każde konto Azure automatycznie ma jeden.
7. W obszarze **tryb zarządzania**, kliknij przycisk **Utwórz nową aplikację usługi AD** Jeśli nie została jeszcze wybrana.
   
    Podłącza portalu **tworzenie aplikacji** pole wprowadzania wartości domyślnej. Domyślnie aplikacja Azure AD nosi nazwę taki sam jak w aplikacji interfejsu API. Jeśli wolisz, możesz wprowadzić inną nazwę.
   
    ![Ustawienia usługi Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Uwaga**: Alternatywnie można użyć jednej usługi Azure AD aplikacji dla wywołania aplikacji interfejsu API i chronionej aplikacji interfejsu API. W przypadku wybrania to alternatywne rozwiązanie nie jest wymagane **Utwórz nową aplikację usługi AD** opcji w tym miejscu, ponieważ utworzonej wcześniej w samouczku uwierzytelniania użytkownika aplikacji usługi Azure AD. W tym samouczku użyjesz rozdzielenie aplikacji usługi Azure AD dla wywołania aplikacji interfejsu API i chronionej aplikacji interfejsu API.
8. Zanotuj wartość, która znajduje się w **tworzenie aplikacji** pole wprowadzania; będzie wyszukiwanie tej usługi AAD aplikacji w klasycznym portalu Azure później.
9. Kliknij przycisk **OK**.
10. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
    
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Usługi aplikacji — tworzy aplikację usługi Azure Active Directory z **adres URL logowania** i **adres URL odpowiedzi** automatycznie Ustaw adres URL aplikacji interfejsu API. Ostatnie wartość włącza użytkowników w dzierżawie usługi AAD do logowania i dostępu do aplikacji interfejsu API.

### <a name="verify-that-the-api-app-is-protected"></a>Sprawdź, czy w aplikacji interfejsu API jest chroniony
1. W przeglądarce przejdź do adresu URL aplikacji interfejsu API: w **aplikacji interfejsu API** bloku w portalu Azure, kliknij łącze w obszarze **adres URL**. 
   
    Użytkownik zostanie przekierowany do ekran logowania, ponieważ nieuwierzytelnione żądania nie mogą nawiązać połączenia w aplikacji interfejsu API. 
   
    Jeśli w przeglądarce przejdź do interfejsu użytkownika programu Swagger, mogą już zarejestrowane przeglądarce — w takim przypadku otwórz sesję InPrivate lub Incognito okno i przejdź do adresu URL programu Swagger interfejsu użytkownika.
2. Zaloguj się przy użyciu poświadczeń użytkownika w dzierżawie usługi AAD.
   
   Gdy użytkownik jest zalogowany, "został pomyślnie utworzony" strona jest wyświetlana w przeglądarce.

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Konfigurowanie projektu ToDoListAPI nabywanie i Wyślij token usługi Azure AD
W tej sekcji możesz wykonać następujące zadania:

* Dodaj kod w aplikacji interfejsu API warstwy środkowej, który używa poświadczeń aplikacji usługi Azure AD do uzyskania tokenu i wysyłania żądań HTTP do aplikacji interfejsu API warstwy danych.
* Pobierz poświadczenia, które są potrzebne z usługi Azure AD.
* Wprowadź poświadczenia w usłudze Azure App Service ustawienia środowiska środowiska uruchomieniowego w aplikacji interfejsu API warstwy środkowej. 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Konfigurowanie projektu ToDoListAPI nabywanie i Wyślij token usługi Azure AD
Wprowadź następujące zmiany w projekcie ToDoListAPI w programie Visual Studio.

1. Usuń znaczniki komentarza cały kod w *ServicePrincipal.cs* pliku.
   
    To jest kod, który używa biblioteki ADAL dla platformy .NET można uzyskać tokenu elementu nośnego usługi Azure AD.  Używa kilka wartości konfiguracji, które zostaną ustawione w środowisko uruchomieniowe platformy Azure później. Oto kod: 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Uwaga:** ten kod wymaga biblioteki ADAL dla pakietu NuGet programu .NET (Microsoft.IdentityModel.Clients.ActiveDirectory), który jest już zainstalowany w projekcie. W przypadku tego projektu zostały tworzenia od początku, trzeba zainstalować ten pakiet. Ten pakiet nie jest automatycznie instalowany przez szablon nowego projektu aplikacji interfejsu API.
2. W *kontrolerów/ToDoListController*, Usuń komentarz kodu w `NewDataAPIClient` metodę, która dodaje token do HTTP żądań w nagłówku autoryzacji.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Wdrażanie projektu ToDoListAPI. (Kliknij projekt prawym przyciskiem myszy, a następnie kliknij przycisk **Publikuj > Publikuj**.)
   
    Visual Studio wdroży projekt i otworzy w przeglądarce podstawowy adres URL aplikacji sieci web. Wyświetli stronę błędu 403, co jest zrozumiałe próbę przejść do podstawowego adresu URL interfejsu API sieci Web w przeglądarce.
4. Zamknij przeglądarkę.

### <a name="get-azure-ad-configuration-values"></a>Pobiera wartości konfiguracji usługi Azure AD
1. W [klasycznego portalu Azure](https://manage.windowsazure.com/), przejdź do **usługi Azure Active Directory**.
2. Na **katalogu** kliknij dzierżawę usługi AAD.
3. Kliknij przycisk **aplikacji > aplikacje Moja firma jest właścicielem**, a następnie kliknij znacznik wyboru.
4. Na liście aplikacji kliknij nazwę tego typu Azure utworzony po włączeniu uwierzytelniania dla aplikacji interfejsu API ToDoListDataAPI (warstwy danych).
5. Kliknij kartę **Konfiguracja**.
6. Kopiuj **identyfikator klienta** wartość i zapisz go w innym możesz pobrać go z później. 
7. Azure klasycznego portalu przejdź do listy **aplikacji Moja firma jest właścicielem**i kliknij utworzony dla aplikacji interfejsu API ToDoListAPI warstwy środkowej (utworzonym w poprzednim samouczek, nie można utworzyć aplikację AAD w tym samouczku).
8. Kliknij kartę **Konfiguracja**.
9. Kopiuj **identyfikator klienta** wartość i zapisz go w innym możesz pobrać go z później.
10. W obszarze **klucze**, wybierz pozycję **1 rok** z **wybierz czas trwania** listy rozwijanej.
11. Kliknij pozycję **Zapisz**.
    
     ![Generowanie klucza aplikacji](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Skopiuj wartość tego klucza i zapisz go w innym, które możesz pobrać go z później.
    
     ![Skopiuj nowy klucz aplikacji](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a>Konfigurowanie ustawień usługi Azure AD w aplikacji interfejsu API warstwy środkowej środowiska uruchomieniowego
1. Przejdź do [portalu Azure](https://portal.azure.com/), a następnie przejdź do **aplikacji interfejsu API** bloku aplikacji interfejsu API, który jest hostem projektu TodoListAPI (warstwy środkowej).
2. Kliknij kolejno pozycje **Ustawienia > Ustawienia aplikacji**.
3. W **ustawień aplikacji** Dodaj następujące klucze i wartości:
   
   | **Klucz** | IDA: urzędu |
   | --- | --- |
   | **Wartość** |https://login.microsoftonline.com/ {nazwa dzierżawy usługi Azure AD} |
   | **Przykład** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Klucz** | IDA: ClientId |
   | --- | --- |
   | **Wartość** |Identyfikator klienta aplikacji wywołującej (warstwy środkowej - ToDoListAPI) |
   | **Przykład** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Klucz** | IDA: ClientSecret |
   | --- | --- |
   | **Wartość** |Klucz aplikacji z aplikacji wywołującej (warstwy środkowej - ToDoListAPI) |
   | **Przykład** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Klucz** | IDA: zasobów |
   | --- | --- |
   | **Wartość** |Identyfikator klienta aplikacji o nazwie (- projekt ToDoListDataAPI warstwy danych) |
   | **Przykład** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Uwaga**: dla `ida:Resource`, upewnij się, że używasz aplikacji o nazwie **identyfikator klienta** i nie jego **identyfikator URI aplikacji**.
   
    `ida:ClientId`i `ida:Resource` są różne wartości w tym samouczku, ponieważ używasz oddzielnych applicaations usługi Azure AD dla warstwy środkowej i warstwy danych. Przy użyciu pojedynczej aplikacji usługi Azure AD dla wywołania aplikacji interfejsu API i chronionej aplikacji interfejsu API będzie używać tej samej wartości w obu `ida:ClientId` i `ida:Resource`.
   
    Kod używa program Configuration Manager, aby uzyskać te wartości, więc może być przechowywany w pliku Web.config projektu lub środowisko uruchomieniowe platformy Azure. Po uruchomieniu aplikacji ASP.NET w usłudze Azure App Service ustawienia środowiska automatycznie zastąpić ustawienia z pliku Web.config. Ustawienia środowiska są zwykle [bardziej bezpieczny sposób przechowywania informacji poufnych porównane do pliku Web.config](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Kliknij pozycję **Zapisz**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a>Testowanie aplikacji
1. W przeglądarce przejdź do adresu URL HTTPS aplikacji sieci web frontonu AngularJS.
2. Kliknij przycisk **listy zadań do wykonania** kartę i zaloguj się przy użyciu poświadczeń użytkownika w dzierżawie usługi Azure AD. 
3. Dodawanie elementów do wykonania, aby sprawdzić, czy aplikacja działa.
   
    ![Lista zadań do wykonania strony](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Jeśli aplikacja nie działa zgodnie z oczekiwaniami, należy dokładnie sprawdzić wszystkie ustawienia, która została wprowadzona w portalu Azure. Jeśli wszystkie ustawienia wydają się być poprawne, zobacz [Rozwiązywanie problemów](#troubleshooting) dalszej części tego samouczka.

## <a name="protect-the-api-app-from-browser-access"></a>Ochrona aplikacji interfejsu API przed dostępem przeglądarki
W tym samouczku utworzona oddzielna aplikacji usługi Azure AD dla aplikacji interfejsu API ToDoListDataAPI (warstwy danych). Jak przedstawiono, gdy usługi aplikacji — tworzy aplikację usługi AAD, konfiguruje usługi AAD aplikacji w taki sposób, który umożliwia użytkownikowi przejdź do adresu URL aplikacji interfejsu API w przeglądarce i zaloguj się. Oznacza to, że istnieje możliwość, że użytkownik końcowy w dzierżawie usługi Azure AD, nie tylko nazwę główną usługi, aby dostęp do interfejsu API. 

Jeśli chcesz uniemożliwić dostęp za pomocą przeglądarki bez pisania żadnego kodu w chronionej aplikacji interfejsu API, można zmienić **adres URL odpowiedzi** w aplikacji AAD bazowy adres URL, aby różni się od aplikacji interfejsu API. 

### <a name="disable-browser-access"></a>Wyłącz dostęp za pomocą przeglądarki
1. W portalu klasycznym **Konfiguruj** karcie dla aplikacji usługi AAD, który został utworzony dla TodoListService, zmień wartość w **adres URL odpowiedzi** pola tak, aby prawidłowy adres URL, ale nie adres URL aplikacji interfejsu API.
2. Kliknij pozycję **Zapisz**.

### <a name="verify-browser-access-no-longer-works"></a>Sprawdź, czy dostęp za pomocą przeglądarki przestanie działać.
Wcześniej upewnieniu się, że można przejść do adresu URL aplikacji interfejsu API z poziomu przeglądarki logując się przy użyciu poświadczeń użytkownika. W tej sekcji możesz sprawdzić, czy nie jest to możliwe. 

1. W nowym oknie przeglądarki przejdź do adresu URL aplikacji interfejsu API ponownie.
2. Zaloguj się po wyświetleniu monitu, aby to zrobić.
3. Logowania zakończy się pomyślnie, ale prowadzi do strony błędu.
   
    Skonfigurowano usługi AAD aplikacji, aby użytkownicy w dzierżawie usługi AAD nie może zalogować się i dostęp do interfejsu API w przeglądarce. Można nadal dostęp do aplikacji interfejsu API przy użyciu tokenu głównej usługi, które można sprawdzić, przechodząc do adresu URL aplikacji sieci web i dodanie więcej elementów do wykonania.

## <a name="restrict-access-to-a-particular-service-principal"></a>Ograniczanie dostępu do określonej usługi podmiot zabezpieczeń
Teraz każdego obiektu wywołującego, który można uzyskać token dla użytkownika lub nazwy głównej usługi w dzierżawie usługi Azure AD można wywołać w aplikacji interfejsu API TodoListDataAPI (warstwy danych). Możesz upewnić się, że aplikacji interfejsu API warstwy danych akceptuje tylko wywołania z aplikacji interfejsu API (warstwy środkowej) TodoListAPI, a tylko z określoną usługą podmiot zabezpieczeń. 

Ograniczenia te można dodać, dodając kod do sprawdzania poprawności `appid` i `objectidentifier` oświadczenia na przychodzące wywołania.

W ramach tego samouczka należy umieścić kod, który sprawdza identyfikator aplikacji i usług identyfikator podmiotu zabezpieczeń bezpośrednio w akcji kontrolera.  Alternatywy mają używać niestandardowego `Authorize` atrybutu lub w tej weryfikacji w uruchamiania sekwencje (np. oprogramowanie pośredniczące OWIN). Na przykład tych, zobacz [tej aplikacji przykładowej](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Wprowadź następujące zmiany w projekcie TodoListDataAPI.

1. Otwórz *Controllers/TodoListController.cs* pliku.
2. Usuń znaczniki komentarza wierszy, które ustawić `trustedCallerClientId` i `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Usuń znaczniki komentarza kod w metodzie CheckCallerId. Ta metoda jest wywoływana na początku każdej metody akcji w kontrolerze. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. Należy ponownie wdrożyć projekt ToDoListDataAPI w usłudze Azure App Service.
5. W przeglądarce, kliknij polecenie Przejdź do adresu URL HTTPS aplikacji sieci web frontonu AngularJS, a na stronie głównej **listy zadań do wykonania** kartę.
   
    Aplikacja nie działa, ponieważ wywołania wewnętrznej kończą się niepowodzeniem. Nowy kod sprawdza rzeczywisty identyfikator appid i elemencie objectidentifier, ale nie ma jeszcze prawidłowych wartości w celu sprawdzania ich względem. Przeglądarka konsoli narzędzi dla deweloperów zgłasza, że serwer zwrócił błąd HTTP 401.
   
    ![Błąd w Developer Tools konsoli](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    W poniższych krokach można skonfigurować oczekiwanych wartości.
6. Przy użyciu programu PowerShell usługi Azure AD, pobrać wartości nazwy głównej usługi dla aplikacji usługi Azure AD, który został utworzony dla projektu TodoListWebApp.
   
    a. Aby uzyskać instrukcje dotyczące sposobu instalowania programu Azure PowerShell i nawiązać połączenia z subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. Aby uzyskać listę podmiotów zabezpieczeń, usługi, należy wykonać `Login-AzureRmAccount` polecenia, a następnie `Get-AzureRmADServicePrincipal` polecenia.
   
    c. Znajdź identyfikator obiektu dla nazwy głównej usługi aplikacji TodoListAPI i zapisać go w lokalizacji można skopiować z później.
7. W portalu Azure przejdź do bloku aplikacji interfejsu API dla aplikacji interfejsu API, który wdrożony projekt ToDoListDataAPI w celu.
8. Kliknij przycisk **Ustawienia > Ustawienia aplikacji**.
9. W **ustawień aplikacji** Dodaj następujące klucze i wartości:
   
   | **Klucz** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Wartość** |Identyfikator podmiotu zabezpieczeń usługi wywołania aplikacji |
   | **Przykład** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Klucz** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Wartość** |Identyfikator klienta aplikacji - skopiowane z aplikacji TodoListAPI usługi Azure AD podczas wywoływania |
   | **Przykład** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Kliknij pozycję **Zapisz**.
    
     ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. W przeglądarce, wróć do adresu URL aplikacji sieci web, a na stronie głównej kliknij **listy zadań do wykonania** kartę.
    
     Teraz aplikacja działa zgodnie z oczekiwaniami, ponieważ aplikacja zaufany obiekt wywołujący identyfikator i identyfikator podmiotu zabezpieczeń usługi są oczekiwanych wartości.
    
     ![Lista zadań do wykonania strony](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a>Kompilowanie projektów od podstaw
Dwa projekty interfejsu API sieci Web zostały utworzone przy użyciu **aplikacji interfejsu API Azure** projektu szablonu i zastępowanie domyślnego kontrolera wartości z kontrolerem listy zadań. Uzyskania tokeny podmiotu zabezpieczeń usługi Azure AD w projekcie ToDoListAPI [Active Directory Authentication Library (ADAL) dla platformy .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) zainstalowano pakiet NuGet.

Aby uzyskać informacje o sposobie tworzenia aplikacji jednostronicowej AngularJS z interfejsu API sieci Web wewnętrznej jak ToDoListAngular, zobacz [ręce w laboratorium: tworzenie jednej strony aplikacji JEDNOSTRONICOWEJ z interfejsu API sieci Web platformy ASP.NET i Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Aby uzyskać informacje o sposobie dodawania kod uwierzytelniania usługi Azure AD, zobacz [zabezpieczanie AngularJS jednej strony aplikacji za pomocą usługi Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Upewnij się, że użytkownik nie należy mylić (warstwy środkowej) ToDoListAPI i ToDoListDataAPI (warstwy danych). Na przykład, w tym samouczku można dodać uwierzytelniania w aplikacji interfejsu API warstwy danych **, ale klucz aplikacji muszą pochodzić z aplikacji usługi Azure AD, który został utworzony dla aplikacji interfejsu API warstwy środkowej**.

## <a name="next-steps"></a>Następne kroki
To jest ostatni samouczek w serii aplikacje interfejsu API. 

Aby uzyskać więcej informacji na temat usługi Azure Active Directory zobacz następujące zasoby.

* [Przewodnik Azure deweloperzy AD](http://aka.ms/aaddev)
* [Scenariusze usługi Azure AD](http://aka.ms/aadscenarios)
* [Przykłady Azure AD](http://aka.ms/aadsamples)
  
    [Aplikacji sieci Web-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) próbki jest podobny do przedstawiono, w tym samouczku, ale bez korzystania z usługi aplikacji uwierzytelniania.

Informacje o inne sposoby wdrażania projektów programu Visual Studio do aplikacji interfejsu API za pomocą programu Visual Studio lub [automatyzacji wdrażania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) z [systemu kontroli źródła](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), zobacz [sposobu wdrażania platformy Azure Aplikacji usługi app Service](../app-service-web/web-sites-deploy.md).

