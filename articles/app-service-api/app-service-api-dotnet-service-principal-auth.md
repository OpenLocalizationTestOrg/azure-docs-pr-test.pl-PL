---
title: "aaaService główna uwierzytelniania dla aplikacji interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacja tooprotect interfejsu API w usłudze Azure App Service dla scenariuszy service-to-service."
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
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uwierzytelniania usługi aplikacji toouse dla *wewnętrzny* dostęp do aplikacji tooAPI. Scenariusz wewnętrzny jest, gdzie masz aplikację interfejsu API, które mają toobe eksploatacyjny tylko przez kod aplikacji. Hello zalecany sposób tooimplement w tym scenariuszu w usłudze aplikacji hello tooprotect toouse usługi Azure AD nosi nazwę aplikacji interfejsu API. Wywołania aplikacji interfejsu API hello chronione przy użyciu tokenu elementu nośnego, który można pobrać z usługi Azure AD przez udostępnienie tożsamość aplikacji poświadczeń (nazwy głównej usługi). Aby toousing alternatyw usługi Azure AD, zobacz hello **do usługi uwierzytelniania** sekcji hello [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

W tym artykule dowiesz się:

* Jak aplikacja tooprotect interfejsu API usługi Azure Active Directory (Azure AD) toouse ze nieuwierzytelniony dostępu.
* Jak tooconsume chronionego interfejsu API aplikacji z aplikacji interfejsu API, aplikacji sieci web lub aplikacji mobilnej przy użyciu poświadczeń podmiotu zabezpieczeń (tożsamość aplikacji) usługi Azure AD. Aby uzyskać informacje na temat tooconsume z aplikacji logiki, zobacz [przy użyciu niestandardowego interfejsu API hostowanych w usłudze aplikacji z usługą Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).
* Jak toomake upewnić się, że hello chronione aplikacji interfejsu API nie można wywołać z poziomu przeglądarki przy zalogowanych użytkowników.
* Jak toomake pewność, że hello chronione aplikacji interfejsu API tylko może być wywoływany przez określony nazwy głównej usługi Azure AD.

Witaj artykuł zawiera dwie sekcje:

* Witaj [jak tooconfigure usługi podmiotu zabezpieczeń uwierzytelniania w usłudze Azure App Service](#authconfig) sekcji opisano w sposób ogólny tooconfigure uwierzytelniania dla dowolnej aplikacji interfejsu API i jak tooconsume hello chronione aplikacji interfejsu API. Ta sekcja dotyczy jednakowo tooall platform obsługiwanych przez usługę App Service, w tym .NET, Node.js i Java.
* Począwszy od hello [kontynuowanie samouczki dotyczące rozpoczynania pracy .NET hello](#tutorialstart) sekcji hello samouczek przeprowadzi Cię przez konfigurowania scenariusza "dostęp do" przykładową aplikację .NET w aplikacji usługi. 

## <a id="authconfig"></a>Jak tooconfigure usługi podmiotu zabezpieczeń uwierzytelniania w usłudze Azure App Service
Ta sekcja zawiera ogólne instrukcje dotyczące tooany aplikacji interfejsu API. Dla tooDo toohello określonych czynności .NET listy przykładowej aplikacji, przejdź zbyt[kontynuowanie serii samouczek aplikacji interfejsu API programu .NET hello](#tutorialstart).

1. W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **ustawienia** bloku aplikacji interfejsu API hello mają tooprotect, a następnie znajdź hello **funkcje** sekcji, a następnie kliknij przycisk **Uwierzytelniania / autoryzacji**.
   
    ![Uwierzytelnianie/autoryzację, w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. W hello **tootake akcji w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory** .
4. W obszarze **dostawców uwierzytelniania**, wybierz pozycję **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Skonfiguruj hello **ustawień usługi Azure Active Directory** toocreate bloku Azure nowej aplikacji usługi AD, lub użyj istniejącej aplikacji usługi Azure AD, jeśli masz już konto, które mają toouse.
   
    Scenariusze wewnętrzny zwykle obejmują wywołanie aplikacji interfejsu API aplikacji interfejsu API. Oddzielne Azure można użyć tylko jednej aplikacji usługi Azure AD lub aplikacji usługi AD dla każdej aplikacji interfejsu API.
   
    Aby uzyskać szczegółowe informacje dotyczące tego bloku, zobacz [jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Po zakończeniu korzystania z bloku konfiguracji dostawcy uwierzytelniania hello, kliknij przycisk **OK**.
7. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Po zakończeniu usługi aplikacji — tylko zezwala na żądania pochodzące z wywołań w dzierżawie usługi Azure AD hello skonfigurowane. Brak kodu uwierzytelniania i autoryzacji jest wymagany w aplikacji interfejsu API hello chronione. Witaj tokenu elementu nośnego jest przekazywana toohello interfejsu API aplikacji wraz z oświadczeń często używane w nagłówkach HTTP, a może odczytywać dane toovalidate kodu, które żądania są z określonego obiektu wywołującego, takich jak nazwy głównej usługi.

Ta funkcja uwierzytelniania działa hello tak samo dla wszystkich języków obsługuje usługi aplikacji, w tym .NET, Node.js i Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Jak tooconsume hello chronione aplikacji interfejsu API
obiekt wywołujący Hello podać tokenu elementu nośnego usługi Azure AD z interfejsu API. tooget przy użyciu poświadczeń główna usługi tokenu elementu nośnego, wywołujący hello używa biblioteki uwierzytelniania usługi Active Directory (ADAL dla [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), lub [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget token hello kod, który wywołuje ADAL zapewnia hello tooADAL następujących informacji:

* Nazwa Hello dzierżawy usługi Azure AD.
* Witaj identyfikator i klienta klucz tajny klienta (klucz aplikacji) skojarzone z obiektem wywołującym hello aplikacji hello Azure AD.
* Identyfikator klienta aplikacji usługi Azure AD skojarzonej z hello hello Hello chronione aplikacji interfejsu API. (Jeśli jest używany tylko jednej aplikacji usługi Azure AD, to jest hello tego samego Identyfikatora klienta jako jeden dla obiekt wywołujący hello hello.)

Te wartości są dostępne na stronach hello Azure AD hello [klasycznego portalu Azure](https://manage.windowsazure.com/).

Po hello token zostały nabyte, wywołujący hello obejmuje żądań HTTP w nagłówku autoryzacji hello.  Usługa aplikacji weryfikuje hello token i umożliwia hello żądań tooreach hello chronione aplikacji interfejsu API.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Jak tooprotect aplikacji hello interfejsu API przed dostępem użytkowników w hello sam dzierżawy
Tokenów elementu nośnego dla użytkowników w tej samej dzierżawy są uznawane za prawidłowe dla hello hello chronione aplikacji interfejsu API.  Jeśli chcesz, aby tooensure, który można wywołać tylko nazwy głównej usługi hello chronionej aplikacji interfejsu API, Dodaj kod w hello chronione hello toovalidate aplikacji interfejsu API po oświadczeń z tokenu hello:

* `appid`powinien być hello identyfikator klienta aplikacji usługi Azure AD hello, który jest skojarzony z obiektem wywołującym hello. 
* `oid`(`objectidentifier`) powinna być identyfikator podmiotu zabezpieczeń usługi hello hello wywołującego. 

Usługa App Service zapewnia również hello `objectidentifier` oświadczeń w nagłówku hello X-MS-CLIENT-podmiot zabezpieczeń-ID.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Jak tooprotect hello aplikacji interfejsu API z dostęp za pomocą przeglądarki
Nie zweryfikować oświadczenia w kodzie aplikacji interfejsu API hello chroniony, a Użyj oddzielnej aplikacji usługi Azure AD dla hello chronione aplikacji interfejsu API, upewnij się, że hello, że adres URL odpowiedzi aplikacji usługi Azure AD jest nie tak samo jak hello podstawowy adres URL aplikacji interfejsu API hello. Jeśli hello adres URL odpowiedzi wskazuje bezpośrednio aplikacji interfejsu API toohello chronione, użytkownik w dzierżawie powitalnych tej samej usługi Azure AD można Przeglądaj toohello aplikacji interfejsu API, zaloguj się na i pomyślnie wywołać interfejs API hello.

## <a id="tutorialstart"></a>Kontynuowanie serii samouczek hello aplikacji interfejsu API programu .NET
Jeśli wykonujesz hello Node.js lub Java samouczek serii dla aplikacji interfejsu API, Pomiń toohello [następne kroki](#next-steps) sekcji. 

Hello dalszej części tego artykułu nadal serii samouczek aplikacji interfejsu API programu .NET hello i przyjęto założenie, że zostały wykonane hello [samouczek uwierzytelniania użytkownika](app-service-api-dotnet-user-principal-auth.md) i mieć hello przykładowej aplikacji działających na platformie Azure przy użyciu uwierzytelniania użytkownika włączone.

## <a name="set-up-authentication-in-azure"></a>Konfigurowanie uwierzytelniania w systemie Azure
W tej sekcji można skonfigurować usługę aplikacji, aby tego hello żądań tylko HTTP umożliwia aplikacji interfejsu API warstwy danych hello tooreach są hello te, które prawidłowy Azure AD tokenów elementu nośnego. 

W następującej sekcji hello skonfiguruj toosend aplikacji interfejsu API warstwy środkowej hello aplikacji tooAzure poświadczeń AD, wrócić tokenu elementu nośnego i wysłać aplikacji interfejsu API warstwy danych toohello tokenu elementu nośnego hello. Ten proces przedstawiono na powitania diagramu.

![Diagram uwierzytelniania usługi](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Jeśli wystąpiły problemy podczas hello samouczek zalecenia, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji na końcu hello hello samouczka. 

1. W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **ustawienia** bloku aplikacji hello interfejsu API dla aplikacji interfejsu API (warstwy danych) ToDoListDataAPI hello utworzone, a następnie kliknij przycisk **ustawienia**.
2. W hello **ustawienia** bloku, Znajdź hello **funkcje** sekcji, a następnie kliknij przycisk **uwierzytelniania / autoryzacji**.
   
    ![Uwierzytelnianie/autoryzację, w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
4. W hello **tootake akcji w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory**.
   
    To jest ustawienie hello, powodujący tooensure App Service, tylko uwierzytelnienia aplikacji interfejsu API hello reach żądania. Dla żądania, które mają tokenów elementu nośnego prawidłowe, usługi aplikacji przekazuje tokeny hello wzdłuż aplikacji toohello interfejsu API i wypełnia nagłówków HTTP z często używanych oświadczeń toomake informacji kodu tooyour łatwo dostępne.
5. W obszarze **dostawców uwierzytelniania**, kliknij przycisk **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji w portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. W hello **ustawień usługi Azure Active Directory** bloku, kliknij przycisk **Express**.
   
    Z hello **Express** opcji Azure można automatycznie utworzyć aplikację AAD w usługi Azure AD [dzierżawy](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Nie masz toocreate dzierżawy, ponieważ jeden ma automatycznie co konto platformy Azure.
7. W obszarze **tryb zarządzania**, kliknij przycisk **Utwórz nową aplikację usługi AD** Jeśli nie została jeszcze wybrana.
   
    Hello portal podłącza hello **tworzenie aplikacji** pole wprowadzania wartości domyślnej. Domyślnie program hello aplikacji usługi Azure AD o nazwie hello takie same jak aplikacja hello interfejsu API. Jeśli wolisz, możesz wprowadzić inną nazwę.
   
    ![Ustawienia usługi Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Uwaga**: Alternatywnie można użyć jednej usługi Azure AD aplikacji hello zarówno wywołania aplikacji interfejsu API i hello chronione aplikacji interfejsu API. Jeśli została wybrana opcja to alternatywne rozwiązanie, nie musisz hello **Utwórz nową aplikację usługi AD** opcji w tym miejscu, ponieważ utworzonej wcześniej w samouczku uwierzytelniania użytkownika hello aplikacji usługi Azure AD. W tym samouczku użyjesz rozdzielenie aplikacji usługi Azure AD, dla hello wywołanie aplikacji interfejsu API i hello chronione aplikacji interfejsu API.
8. Zanotuj wartość hello hello **tworzenie aplikacji** pole wprowadzania; będzie wyszukiwania tej aplikacji usługi AAD w hello klasycznego portalu Azure później.
9. Kliknij przycisk **OK**.
10. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
    
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Usługi aplikacji — tworzy aplikację usługi Azure Active Directory z **adres URL logowania** i **adres URL odpowiedzi** automatycznie ustawione toohello adres URL aplikacji interfejsu API. ostatnie wartości Hello umożliwia użytkownikom w sieci toolog dzierżawy usługi AAD w i aplikacji interfejsu API hello dostępu.

### <a name="verify-that-hello-api-app-is-protected"></a>Sprawdź, czy jest chroniony, aplikacja hello interfejsu API
1. W przeglądarce Przejdź toohello adres URL aplikacji hello interfejsu API: w hello **aplikacji interfejsu API** bloku w hello portalu Azure, kliknij łącze hello w obszarze **adres URL**. 
   
    Jesteś ekran logowania przekierowanego tooa ponieważ nieuwierzytelnione żądania nie są dozwolone w aplikacji interfejsu API hello tooreach. 
   
    Jeśli przeglądarki Przejdź toohello interfejs użytkownika programu Swagger, przeglądarka może już być zalogowany — w takim przypadku otwórz sesję InPrivate lub Incognito okno i przejdź toohello URL interfejsu użytkownika programu Swagger.
2. Zaloguj się przy użyciu poświadczeń użytkownika w dzierżawie usługi AAD.
   
   Gdy użytkownik jest zalogowany, hello "Pomyślnie utworzono" strona zostanie wyświetlona w przeglądarce hello.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Konfigurowanie tooacquire projektu ToDoListAPI hello i Wyślij token usługi Azure AD hello
W tej sekcji hello następujących zadań:

* Dodaj kod w aplikacji interfejsu API warstwy środkowej hello, który używa usługi Azure AD aplikacji poświadczenia tooacquire token i wysłać go przy użyciu protokołu HTTP żądania aplikacji interfejsu API warstwy danych toohello.
* Pobierz hello poświadczenia, które są potrzebne z usługi Azure AD.
* Wprowadź poświadczenia hello w usłudze Azure App Service ustawienia środowiska środowiska uruchomieniowego w aplikacji interfejsu API warstwy środkowej hello. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Konfigurowanie tooacquire projektu ToDoListAPI hello i Wyślij token usługi Azure AD hello
Wprowadź następujące zmiany w projekcie ToDoListAPI hello w programie Visual Studio hello.

1. Usuń znaczniki komentarza cały kod hello w hello *ServicePrincipal.cs* pliku.
   
    To jest kod hello używa biblioteki ADAL dla tokenu elementu nośnego hello Azure AD tooacquire .NET.  Używa kilku wartości konfiguracji, które zostanie ustawiona w środowisku platformy Azure środowiska uruchomieniowego hello później. Oto kod hello: 
   
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
   
    **Uwaga:** ten kod wymaga pakietu NuGet programu .NET (Microsoft.IdentityModel.Clients.ActiveDirectory), który jest już zainstalowany w projekcie hello hello biblioteki ADAL. Jeśli zostały tworzenia tego projektu od podstaw, trzeba będzie tooinstall tego pakietu. Ten pakiet nie jest automatycznie instalowany przez szablon nowego projektu aplikacji interfejsu API hello.
2. W *kontrolerów/ToDoListController*, usuń znaczniki komentarza hello kodu w hello `NewDataAPIClient` metodę, która dodaje hello tokenu tooHTTP żądań w nagłówku autoryzacji hello.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Wdrażanie projektu ToDoListAPI hello. (Kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **Publikuj > Publikuj**.)
   
    Visual Studio wdroży projekt hello i otwiera podstawowy adres URL przeglądarki toohello aplikacji sieci web. Wyświetli stronę błędu 403, co jest zrozumiałe dla próba toogo tooa interfejsu API sieci Web podstawowego adresu URL w przeglądarce.
4. Zamknij hello przeglądarki.

### <a name="get-azure-ad-configuration-values"></a>Pobiera wartości konfiguracji usługi Azure AD
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), przejdź do zbyt**usługi Azure Active Directory**.
2. Na powitania **katalogu** kliknij dzierżawę usługi AAD.
3. Kliknij przycisk **aplikacji > aplikacje Moja firma jest właścicielem**, a następnie kliknij znacznik wyboru hello.
4. Liście hello aplikacji kliknij nazwę hello hello, który Azure utworzony po włączeniu uwierzytelniania dla aplikacji interfejsu API (warstwy danych) ToDoListDataAPI hello.
5. Kliknij przycisk hello **Konfiguruj** kartę.
6. Kopiuj hello **identyfikator klienta** wartość i zapisz go w innym możesz pobrać go z później. 
7. W hello klasycznego portalu Azure Przejdź wstecz listy toohello **aplikacji Moja firma jest właścicielem**i kliknij aplikację AAD hello, który został utworzony dla aplikacji interfejsu API ToDoListAPI warstwy środkowej hello (hello utworzonej w poprzedniej samouczek hello, nie Witaj, jeden utworzonego w ramach tego samouczka).
8. Kliknij przycisk hello **Konfiguruj** kartę.
9. Kopiuj hello **identyfikator klienta** wartość i zapisz go w innym możesz pobrać go z później.
10. W obszarze **klucze**, wybierz pozycję **1 rok** z hello **wybierz czas trwania** listy rozwijanej.
11. Kliknij pozycję **Zapisz**.
    
     ![Generowanie klucza aplikacji](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Skopiuj wartość klucza hello i zapisz go w innym, które możesz pobrać go z później.
    
     ![Skopiuj nowy klucz aplikacji](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Konfigurowanie ustawień usługi Azure AD w aplikacji interfejsu API warstwy środkowej hello środowiska uruchomieniowego
1. Przejdź toohello [portalu Azure](https://portal.azure.com/), a następnie przejdź toohello **aplikacji interfejsu API** bloku aplikacji hello interfejsu API, który jest hostem projektu TodoListAPI (warstwy środkowej) hello.
2. Kliknij kolejno pozycje **Ustawienia > Ustawienia aplikacji**.
3. W hello **ustawień aplikacji** Dodaj hello następujące klucze i wartości:
   
   | **Klucz** | IDA: urzędu |
   | --- | --- |
   | **Wartość** |https://login.microsoftonline.com/ {nazwa dzierżawy usługi Azure AD} |
   | **Przykład** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Klucz** | IDA: ClientId |
   | --- | --- |
   | **Wartość** |Identyfikator klienta hello wywoływania aplikacji (warstwy środkowej - ToDoListAPI) |
   | **Przykład** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Klucz** | IDA: ClientSecret |
   | --- | --- |
   | **Wartość** |Klucz aplikacji hello wywoływania aplikacji (warstwy środkowej - ToDoListAPI) |
   | **Przykład** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Klucz** | IDA: zasobów |
   | --- | --- |
   | **Wartość** |Identyfikator klienta o nazwie aplikacji hello (- projekt ToDoListDataAPI warstwy danych) |
   | **Przykład** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Uwaga**: dla `ida:Resource`, upewnij się, że używasz o nazwie aplikacji hello **identyfikator klienta** i nie jego **identyfikator URI aplikacji**.
   
    `ida:ClientId`i `ida:Resource` są różne wartości w tym samouczku, ponieważ używasz Rozdziel usługi Azure AD applicaations hello warstwy środkowej i warstwy danych. Przy użyciu pojedynczej aplikacji usługi Azure AD dla hello wywołanie aplikacji interfejsu API i hello chronione aplikacji interfejsu API, należy użyć hello samą wartość w obu `ida:ClientId` i `ida:Resource`.
   
    Hello kodzie użyto ConfigurationManager tooget tych wartości, więc może być przechowywany w pliku Web.config hello projektu lub środowisko uruchomieniowe Azure hello. Po uruchomieniu aplikacji ASP.NET w usłudze Azure App Service ustawienia środowiska automatycznie zastąpić ustawienia z pliku Web.config. Ustawienia środowiska są zwykle [bardziej bezpieczny sposób toostore poufne informacje porównać pliku Web.config tooa](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Kliknij pozycję **Zapisz**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Testowanie aplikacji hello
1. W przeglądarce Przejdź toohello adres URL HTTPS aplikacji sieci web frontonu AngularJS hello.
2. Kliknij przycisk hello **tooDo listy** kartę i zaloguj się przy użyciu poświadczeń użytkownika w dzierżawie usługi Azure AD. 
3. Dodaj tooverify elementy zadań do wykonania, która aplikacja hello działa.
   
    ![Strona z listą tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Jeśli aplikacja hello nie działać zgodnie z oczekiwaniami, należy dokładnie sprawdzić wszystkie ustawienia hello, wprowadzony w hello portalu Azure. Jeśli są wyświetlane wszystkie ustawienia hello toobe poprawne, zobacz hello [Rozwiązywanie problemów](#troubleshooting) dalszej części tego samouczka.

## <a name="protect-hello-api-app-from-browser-access"></a>Ochrona aplikacji interfejsu API hello z dostęp za pomocą przeglądarki
W tym samouczku utworzona oddzielna aplikacji usługi Azure AD dla aplikacji hello API ToDoListDataAPI (warstwy danych). Jak przedstawiono, gdy usługi aplikacji — tworzy aplikację usługi AAD konfiguruje hello usługi AAD aplikacji w taki sposób, który pozwala na adres URL aplikacji przez użytkownika toogo toohello interfejsu API w przeglądarce i dziennika. Oznacza to, istnieje możliwość, że użytkownik końcowy w dzierżawie usługi Azure AD, a nie tylko nazwy głównej usługi, tooaccess hello interfejsu API. 

Jeśli chcesz dostęp za pomocą przeglądarki tooprevent bez pisania żadnego kodu hello chronione aplikacji interfejsu API, można zmienić hello **adres URL odpowiedzi** w hello usługi AAD aplikacji tak, aby różni się od aplikacji hello interfejsu API bazowy adres URL. 

### <a name="disable-browser-access"></a>Wyłącz dostęp za pomocą przeglądarki
1. W portalu klasycznym hello **Konfiguruj** karcie hello usługi AAD aplikacji, która została utworzona dla hello TodoListService, zmień wartość hello w hello **adres URL odpowiedzi** pola tak, aby prawidłowy adres URL, ale nie hello interfejsu API aplikacji ADRES URL.
2. Kliknij pozycję **Zapisz**.

### <a name="verify-browser-access-no-longer-works"></a>Sprawdź, czy dostęp za pomocą przeglądarki przestanie działać.
Wcześniej upewnieniu się, że adres URL aplikacji interfejsu API toohello można przejść z przeglądarką logując się przy użyciu poświadczeń użytkownika. W tej sekcji możesz sprawdzić, czy nie jest to możliwe. 

1. W nowym oknie przeglądarki Przejdź toohello adres URL aplikacji interfejsu API hello ponownie.
2. Logowanie, gdy monit toodo tak.
3. Logowania zakończy się pomyślnie, ale prowadzi tooan strony błędu.
   
    Skonfigurowano hello usługi AAD aplikacji, aby użytkownicy w dzierżawie usługi AAD hello nie może zalogować się i dostęp do interfejsu API hello w przeglądarce. Można nadal dostęp do aplikacji interfejsu API hello przy użyciu tokenu głównej usługi, które można sprawdzić, przechodząc adres URL aplikacji sieci web toohello i dodanie więcej elementów do wykonania.

## <a name="restrict-access-tooa-particular-service-principal"></a>Ogranicz nazwy głównej usługi określonego tooa dostępu
Teraz każdego obiektu wywołującego, który można uzyskać token dla użytkownika lub nazwy głównej usługi w dzierżawie usługi Azure AD można wywołać aplikacji hello API TodoListDataAPI (warstwy danych). Można toomake się, że tej aplikacji interfejsu API warstwy danych hello akceptuje tylko wywołania z aplikacji interfejsu API (warstwy środkowej) TodoListAPI hello i tylko z określoną usługą podmiot zabezpieczeń. 

Ograniczenia te można dodać, dodając hello toovalidate kodu `appid` i `objectidentifier` oświadczenia na przychodzące wywołania.

W tym samouczku, możesz zaznaczyć hello kodu, który sprawdza identyfikator aplikacji i usług identyfikator podmiotu zabezpieczeń bezpośrednio w akcji kontrolera.  Alternatywne to toouse niestandardowego `Authorize` atrybutu lub toodo tej weryfikacji w sekwencjach uruchamiania (np. oprogramowanie pośredniczące OWIN). Na przykład hello ostatnie zobacz [tej aplikacji przykładowej](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Należy powitania po projekt TodoListDataAPI toohello zmiany.

1. Otwórz hello *Controllers/TodoListController.cs* pliku.
2. Usuń znaczniki komentarza hello wierszy, które ustawić `trustedCallerClientId` i `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Usuń znaczniki komentarza hello kodu w hello CheckCallerId metody. Ta metoda jest wywoływana na początku każdej metody akcji w kontrolerze hello hello. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Należy ponownie wdrożyć tooAzure projekt ToDoListDataAPI hello usługi aplikacji.
5. W przeglądarce Przejdź adres URL HTTPS toohello AngularJS fronton aplikacji sieci web, a strona główna powitania kliknij hello **tooDo listy** kartę.
   
    Aplikacja Hello nie działa, ponieważ wywołania zakończenia toohello ponownie kończą się niepowodzeniem. Nowy kod Hello jest sprawdzanie rzeczywisty identyfikator appid i elemencie objectidentifier, ale nie ma jeszcze toocheck poprawnych wartości hello przed ich. Przeglądarka Hello konsoli narzędzi dla deweloperów zgłasza, że ten serwer hello zwrócił błąd HTTP 401.
   
    ![Błąd w Developer Tools konsoli](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Następujące kroki hello służy do konfigurowania hello oczekiwanych wartości.
6. Przy użyciu programu PowerShell usługi Azure AD, uzyskać wartość hello hello usługi głównej hello aplikacji usługi Azure AD, utworzonej dla projektu TodoListWebApp hello.
   
    a. Aby uzyskać instrukcje dotyczące tooinstall programu Azure PowerShell i połączenia tooyour subskrypcji, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. tooget listę nazwy główne usług, wykonanie hello `Login-AzureRmAccount` polecenia, a następnie hello `Get-AzureRmADServicePrincipal` polecenia.
   
    c. Znajdź hello objectid dla hello nazwy głównej usługi hello TodoListAPI aplikacji i zapisz go w lokalizacji, w której można skopiować z później.
7. W hello portalu Azure Przejdź toohello bloku aplikacji interfejsu API dla aplikacji interfejsu API hello wdrożony projekt ToDoListDataAPI hello do.
8. Kliknij przycisk **Ustawienia > Ustawienia aplikacji**.
9. W hello **ustawień aplikacji** Dodaj hello następujące klucze i wartości:
   
   | **Klucz** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Wartość** |Identyfikator podmiotu zabezpieczeń usługi wywołania aplikacji |
   | **Przykład** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Klucz** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Wartość** |Identyfikator klienta aplikacji - skopiowane z aplikacji Azure AD TodoListAPI hello wywołania |
   | **Przykład** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Kliknij pozycję **Zapisz**.
    
     ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. W przeglądarce adres zwrotny URL aplikacji sieci web toohello, a strona główna powitania kliknij hello **tooDo listy** kartę.
    
     Ta aplikacja hello czas działa zgodnie z oczekiwaniami, ponieważ hello wywołującego zaufanych aplikacji identyfikator i identyfikator podmiotu zabezpieczeń usługi hello oczekiwanej wartości.
    
     ![Strona z listą tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Kompilowanie projektów powitania od podstaw
Witaj dwa projekty interfejsu API sieci Web zostały utworzone przy użyciu hello **aplikacji interfejsu API Azure** szablonu i zastąpienie hello domyślne wartości kontroler z kontrolerem listy zadań projektu. Uzyskania tokeny podmiotu zabezpieczeń usługi Azure AD w projekcie ToDoListAPI hello hello [Active Directory Authentication Library (ADAL) dla platformy .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) zainstalowano pakiet NuGet.

Aby uzyskać informacje na temat za tworzenie aplikacji jednostronicowej AngularJS z interfejsu API sieci Web wewnętrznej jak ToDoListAngular, zobacz [ręce w laboratorium: tworzenie jednej strony aplikacji JEDNOSTRONICOWEJ z interfejsu API sieci Web platformy ASP.NET i Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Aby uzyskać informacje na temat tooadd kod uwierzytelniania usługi Azure AD, zobacz [zabezpieczanie AngularJS jednej strony aplikacji za pomocą usługi Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Upewnij się, że użytkownik nie należy mylić (warstwy środkowej) ToDoListAPI i ToDoListDataAPI (warstwy danych). Na przykład, w tym samouczku, możesz dodać uwierzytelniania toohello aplikacji warstwy danych interfejsu API, **, ale klucz aplikacji hello muszą pochodzić z hello aplikacji usługi Azure AD, który został utworzony dla aplikacji interfejsu API warstwy środkowej hello**.

## <a name="next-steps"></a>Następne kroki
To jest ostatni samouczek hello w hello serii aplikacje interfejsu API. 

Aby uzyskać więcej informacji na temat usługi Azure Active Directory zobacz następujące zasoby hello.

* [Przewodnik Azure deweloperzy AD](http://aka.ms/aaddev)
* [Scenariusze usługi Azure AD](http://aka.ms/aadscenarios)
* [Przykłady Azure AD](http://aka.ms/aadsamples)
  
    Witaj [aplikacji sieci Web-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) przypomina próbki toowhat jest wyświetlany w tym samouczku, ale bez korzystania z usługi aplikacji uwierzytelniania.

Aby uzyskać informacje o innych metodach toodeploy Visual Studio projektów tooAPI aplikacji, za pomocą programu Visual Studio lub [automatyzacji wdrażania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) z [systemu kontroli źródła](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), zobacz [jak toodeploy Usługa aplikacji Azure aplikacji](../app-service-web/web-sites-deploy.md).

