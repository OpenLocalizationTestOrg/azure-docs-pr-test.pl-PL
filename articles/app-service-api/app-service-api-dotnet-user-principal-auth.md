---
title: "Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak chronić aplikację interfejsu API w usłudze Azure App Service, zezwalając na dostęp tylko do uwierzytelnionych użytkowników."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service
## <a name="overview"></a>Omówienie
W tym artykule przedstawiono sposób ochrony aplikacji interfejsu API platformy Azure, tak aby tylko uwierzytelnieni użytkownicy mogą wywołać ją. Zakłada się, że znasz [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md).

Dowiesz się:

* Jak skonfigurować dostawcę uwierzytelniania przy użyciu szczegółów dla usługi Azure Active Directory (Azure AD).
* Jak korzystać z chronionej aplikacji interfejsu API za pomocą [Active Directory Authentication Library (ADAL) dla języka JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Ten artykuł zawiera dwie sekcje:

* [Sposób konfigurowania uwierzytelniania użytkownika w usłudze Azure App Service](#authconfig) sekcji ogólnie opisano sposób konfigurowania uwierzytelniania użytkowników w dowolnej aplikacji interfejsu API i dotyczą wszystkich platform obsługiwanych przez usługę App Service, w tym .NET, Node.js i Java.
* Począwszy od [kontynuowanie samouczków aplikacji interfejsu API programu .NET](#tutorialstart) sekcji tego artykułu prowadzi użytkownika przez konfigurowanie przykładowej aplikacji AngularJS fronton i zaplecze .NET, tak aby były używane do uwierzytelniania użytkowników usługi Azure Active Directory. 

## <a id="authconfig"></a>Jak skonfigurować uwierzytelnianie użytkowników w usłudze Azure App Service
Ta sekcja zawiera ogólne instrukcje, które są stosowane do wszystkich aplikacji interfejsu API. Dla określonego kroki, aby do .NET listy czy przykładowej aplikacji, przejdź do [kontynuowanie samouczki dotyczące rozpoczynania pracy .NET](#tutorialstart).

1. W [portalu Azure](https://portal.azure.com/), przejdź do **ustawienia** bloku aplikacji interfejsu API, który chcesz chronić, Znajdź **funkcje** sekcji, a następnie kliknij przycisk **uwierzytelniania / autoryzacji**.
   
    ![Portal Azure uwierzytelniania/autoryzacji](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. Wybierz jedną z opcji z **działania należy podjąć w przypadku nieuwierzytelnionego żądania** listy rozwijanej.
   
   * Jeśli chcesz tylko uwierzytelnione wywołania do aplikacji interfejsu API, wybierz jedną z **Zaloguj się przy użyciu...**  opcje. Ta opcja umożliwia ochronę w aplikacji interfejsu API bez pisania żadnego kodu działającą w nim.
   * Jeśli chcesz, aby wszystkie wywołania do aplikacji interfejsu API, wybierz **Zezwalaj na żądanie (żadnej akcji)**. Ta opcja umożliwia bezpośrednie nieuwierzytelnione wywoływania do wybranej dostawców uwierzytelniania. Po wybraniu tej opcji należy napisać kod do obsługi autoryzacji.
     
     Aby uzyskać więcej informacji, zobacz [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options) (Uwierzytelnianie i autoryzacja aplikacji interfejsu API w usłudze Azure App Service).
4. Wybierz co najmniej jeden z **dostawców uwierzytelniania**.
   
    Na ilustracji przedstawiono opcje, które wymagają wszystkim zainteresowanym mają być uwierzytelniani przez usługę Azure AD.
   
    ![Blok uwierzytelniania/autoryzacji portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Po wybraniu dostawcy uwierzytelniania portal zawiera blok konfiguracji dla tego dostawcy. 
   
    Aby uzyskać szczegółowe instrukcje dotyczące sposobu konfigurowania bloków konfiguracji dostawcy uwierzytelniania, zobacz [sposobu konfigurowania aplikacji usługi aplikacji do użycia usługi Azure Active Directory logowania](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (Łącze prowadzi do artykuł na temat usługi Azure AD, ale samym artykule zawiera kart, które łącza do artykułów dla dostawców uwierzytelniania).
5. Po zakończeniu korzystania z bloku konfiguracji dostawcy uwierzytelniania, kliknij przycisk **OK**.
6. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.

Po zakończeniu usługi aplikacji uwierzytelnia wszystkie wywołania interfejsu API przed dotarciem aplikacji interfejsu API. Usługi uwierzytelniania działać takie same dla wszystkich języków, które obsługuje usługi aplikacji, w tym .NET, Node.js i Java. 

Aby uwierzytelnione wywołania interfejsu API, wywołujący zawiera token elementu nośnego OAuth 2.0 dostawcy uwierzytelniania w nagłówku autoryzacji żądania HTTP. Tokenu można uzyskać przy użyciu zestawu SDK w dostawcy uwierzytelniania.

## <a id="tutorialstart"></a>Kontynuowanie samouczków aplikacji interfejsu API programu .NET
Jeśli wykonujesz Node.js lub Java samouczków dla aplikacji interfejsu API, przejdź do następnego artykuł [uwierzytelnianie główną usługi dla aplikacji interfejsu API](app-service-api-dotnet-service-principal-auth.md). 

Jeśli po serii samouczek platformy .NET dla aplikacji interfejsu API i już wdrożono przykładową aplikację zgodnie ze wskazówkami zawartymi w [pierwszy](app-service-api-dotnet-get-started.md) i [drugi](app-service-api-cors-consume-javascript.md) samouczki, przejdź do [Konfigurowanie uwierzytelniania w aplikacji usługi i usługi Azure AD](#azureauth) sekcji.

Do wykonania tego samouczka bez pośrednictwa samouczki pierwszego i drugiego, należy wykonać następujące kroki, które wyjaśniono, jak rozpocząć pracę przy użyciu zautomatyzowanego procesu wdrażania przykładowej aplikacji.

> [!NOTE]
> Poniższe kroki dotrzeć do tego samego punktu początkowego tak, jakby były dwóch pierwszych samouczków, z jednym wyjątkiem: Visual Studio nie będzie już wiesz, które aplikacji sieci web lub aplikacji interfejsu API, który pobiera wdrożony każdego projektu. Oznacza to, że nie będziesz mieć dokładne instrukcje w tym samouczku, które opisują sposób wdrażania do prawej obiektów docelowych. Jeśli nie masz doświadczenia z ustaleniem, jak wykonać kroki wdrażania na własną, najlepiej wykonaj samouczek serii z [pierwszy samouczek](app-service-api-dotnet-get-started.md) niż zacząć to zautomatyzowanego procesu wdrażania.
> 
> 

1. Upewnij się, że wszystkie wymagania wstępne wymienione w [pierwszy samouczek](app-service-api-dotnet-get-started.md). Oprócz wymagania wstępne wymienione te samouczki uwierzytelniania przyjęto założenie, że użytkownicy mający doświadczenie z usługi aplikacji — aplikacje sieci web i aplikacji API apps w Visual Studio i portalu Azure.
2. Kliknij przycisk **wdrażanie na platformie Azure** przycisk [plik readme repozytorium przykładowej listy zadań do wykonania](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) umożliwiają wdrażanie aplikacji interfejsu API i aplikacji sieci web. Zanotuj grupę zasobów platformy Azure, która pobiera utworzony, ponieważ możesz użyć tej funkcji do wyszukania nazwy aplikacji interfejsu API i aplikacji sieci web.
3. Pobrać lub sklonować [repozytorium przykładowej listy zadań do wykonania](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) można pobrać kodu, który lokalnie będzie działać z programu Visual Studio.

## <a id="azureauth"></a>Konfigurowanie uwierzytelniania w aplikacji usługi i usługi Azure AD
Masz teraz aplikacji uruchomionych w usłudze Azure App Service bez wymaga uwierzytelnienia użytkowników. W tej sekcji możesz dodać uwierzytelniania, wykonując następujące zadania:

* Konfigurowanie usługi aplikacji, aby wymagać uwierzytelniania usługi Azure Active Directory (Azure AD) w celu wywołania aplikacji interfejsu API warstwy środkowej.
* Tworzenie aplikacji usługi Azure AD.
* Konfigurowanie aplikacji usługi Azure AD do wysyłania tokenu elementu nośnego po logowania do AngularJS frontonu. 

Jeśli wystąpiły problemy podczas zgodnie z instrukcjami samouczka zobacz [Rozwiązywanie problemów](#troubleshooting) sekcji na końcu samouczka. 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a>Konfigurowanie uwierzytelniania dla aplikacji interfejsu API warstwy środkowej
1. W [portalu Azure](https://portal.azure.com/), przejdź do **ustawienia** znaleźć bloku aplikacji interfejsu API utworzonej dla projektu ToDoListAPI **funkcje** sekcji, a następnie kliknij przycisk **uwierzytelniania / autoryzacji**.
   
    ![Portal Azure uwierzytelniania/autoryzacji](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. W **działania należy podjąć w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory**.
   
    Ta opcja zapewnia, że żadne żądania unauathenticated osiągną aplikacji interfejsu API. 
4. W obszarze **dostawców uwierzytelniania**, kliknij przycisk **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. W **ustawień usługi Azure Active Directory** bloku, kliknij przycisk **Express**
   
    ![Opcja uwierzytelniania/autoryzacji Express portalu Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Z **Express** opcji usługi aplikacji może automatycznie tworzyć aplikację usługi Azure AD w usługi Azure AD [dzierżawy](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Nie masz utworzyć dzierżawcę, ponieważ każde konto Azure automatycznie ma jeden.
6. W obszarze **tryb zarządzania**, kliknij przycisk **Utwórz nową aplikację usługi AD** , jeśli nie została jeszcze wybrana i zwróć uwagę, wartość, która znajduje się w **tworzenie aplikacji** pole tekstowe; będzie wyszukiwanie tej usługi AAD aplikacji w klasycznym portalu Azure później.
   
    ![Ustawienia portalu Azure usługi Azure AD](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure automatycznie utworzy aplikację usługi Azure AD o nazwie wskazanych w dzierżawie usługi Azure AD. Domyślnie aplikacja Azure AD nosi nazwę taki sam jak w aplikacji interfejsu API. Jeśli wolisz, możesz wprowadzić inną nazwę.
7. Kliknij przycisk **OK**.
8. W **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Obecnie tylko użytkownicy w Twojej dzierżawie usługi Azure AD można wywołać w aplikacji interfejsu API.

### <a name="optional-test-the-api-app"></a>Opcjonalnie: Testowanie aplikacji interfejsu API
1. W przeglądarce przejdź do adresu URL aplikacji interfejsu API: w **aplikacji interfejsu API** bloku w portalu Azure, kliknij łącze w obszarze **adres URL**.  
   
    Użytkownik zostanie przekierowany do ekran logowania, ponieważ nieuwierzytelnione żądania nie mogą nawiązać połączenia w aplikacji interfejsu API.
   
    Przeglądarka przechodzi do strony "został pomyślnie utworzony", przeglądarka może już zostać zarejestrowana na — w takim przypadku otwórz sesję InPrivate lub Incognito okno i przejdź do adresu URL aplikacji interfejsu API.
2. Zaloguj się przy użyciu poświadczeń dla użytkownika w dzierżawie usługi Azure AD.
   
    Gdy użytkownik jest zalogowany, "został pomyślnie utworzony" strona jest wyświetlana w przeglądarce.
3. Zamknij przeglądarkę.

### <a name="configure-the-azure-ad-application"></a>Konfigurowanie aplikacji usługi Azure AD
Podczas konfigurowania uwierzytelniania usługi Azure AD usługi aplikacji tworzona aplikacja usługi Azure AD. Domyślnie nowe usługi Azure AD aplikacji został skonfigurowany do zapewnienia tokenu elementu nośnego do adresu URL aplikacji interfejsu API. W tej sekcji służy do konfigurowania aplikacji usługi Azure AD w celu umożliwienia tokenu elementu nośnego AngularJS frontonie zamiast bezpośrednio do aplikacji interfejsu API warstwy środkowej. Fronton AngularJS wyśle ten token do aplikacji interfejsu API, gdy wywołuje aplikację interfejsu API.

> [!NOTE]
> Aby zachować procesu jako proste, jak to możliwe, ten samouczek używa jednej usługi Azure AD aplikacji frontonu i środka warstwy aplikacji interfejsu API. Innym rozwiązaniem jest korzystanie z dwóch aplikacji usługi Azure AD. W takim przypadku trzeba udzielić zezwolenia aplikacji usługi Azure AD frontonu do wywoływania warstwy środkowej aplikacji usługi Azure AD. Takie podejście wieloma aplikacjami pozwoli uzyskać większą kontrolę nad uprawnieniami do każdej warstwy.
> 
> 

1. W [klasycznego portalu Azure](https://manage.windowsazure.com/), przejdź do **usługi Azure Active Directory**.
   
   Należy skorzystać z klasycznego portalu, ponieważ niektóre ustawienia usługi Azure Active Directory, które wymagają dostępu do nie są jeszcze dostępne w bieżącym portalu Azure.
2. Na **katalogu** kliknij dzierżawę usługi AAD.
   
   ![Azure AD w klasycznym portalu](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Kliknij przycisk **aplikacji > aplikacje Moja firma jest właścicielem**, a następnie kliknij znacznik wyboru.
   
   Należy również odświeżyć stronę, aby wyświetlić nową aplikację.
4. Na liście aplikacji kliknij nazwę tego typu Azure utworzony po włączeniu uwierzytelniania dla aplikacji interfejsu API.
   
   ![Karta aplikacje AD platformy Azure](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Kliknij pozycję **Konfiguruj**.
   
   ![Karta Konfigurowanie AD platformy Azure](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Ustaw **adres URL logowania** na adres URL aplikacji sieci web AngularJS, nie ma ukośników.
   
   Na przykład: https://todolistangular.azurewebsites.net
   
   ![Adres URL logowania](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Ustaw **adres URL odpowiedzi** na adres URL aplikacji sieci web, nie ma ukośników.
   
   Na przykład: https://todolistsangular.azurewebsites.net
8. Kliknij pozycję **Zapisz**.
   
   ![Adres URL odpowiedzi](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. W dolnej części strony kliknij **manifest Zarządzaj > Pobierz manifest**.
   
   ![Pobierz manifest](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Pobierz plik do lokalizacji, w którym można go edytować.
11. Pobrany plik manifestu, wyszukiwanie `oauth2AllowImplicitFlow` właściwości. Zmień wartość tej właściwości z `false` do `true`, a następnie zapisz plik.
    
    To ustawienie jest wymagane do uzyskania dostępu z poziomu aplikacji jednostronicowej JavaScript. Umożliwia on token elementu nośnego Oauth 2.0, który ma zostać zwrócona w fragmentu adresu URL.
12. Kliknij przycisk **manifest Zarządzaj > manifest przekazywania**i przekazywanie pliku, które zostało zaktualizowane w poprzednim kroku.
    
    ![Przekaż manifestu](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopiuj **identyfikator klienta** wartość i zapisz go w innym miejscu możesz pobrać go z później.

## <a name="configure-the-todolistangular-project-to-use-authentication"></a>Konfigurowanie projektu ToDoListAngular uwierzytelniania
W tej sekcji możesz zmienić AngularJS frontonu tak aby były używane do uzyskania tokenu elementu nośnego dla zalogowanego użytkownika z usługi Azure AD Active Directory Authentication Library (ADAL) dla JS. Kod będzie zawierać token w żądaniach HTTP wysyłane do warstwy środkowej, jak pokazano na poniższym diagramie. 

![Diagram uwierzytelniania użytkownika](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Wprowadź następujące zmiany w plikach projektu ToDoListAngular.

1. Otwórz *index.cshtml* pliku.
2. Usuń znaczniki komentarza wierszy, które odwołują się Active Directory Authentication Library (ADAL) dla skryptów Javascript.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Otwórz *app/scripts/app.js* pliku.
4. Komentarz blok kodu oznaczone jako "bez uwierzytelniania" i Usuń komentarz blok kodu oznaczone jako "uwierzytelniania z".
   
    Ta zmiana odwołuje się do dostawcy uwierzytelniania ADAL JS i udostępnia wartości konfiguracji. W poniższych krokach można ustawić wartości konfiguracji dla aplikacji interfejsu API i aplikacji usługi Azure AD.
5. W kodzie, który ustawia `endpoints` zmiennej, Ustaw adres URL interfejsu API na adres URL aplikacji interfejsu API utworzone dla projektu ToDoListAPI i Ustaw identyfikator aplikacji usługi Azure AD do Identyfikatora klienta, które zostały skopiowane z klasycznego portalu Azure.
   
    Kod teraz jest podobny do poniższego przykładu.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. W wywołaniu `adalProvider.init`ustaw `tenant` do nazwy dzierżawcy i `clientId` tę samą wartość używana w poprzednim kroku.
   
    Kod teraz jest podobny do poniższego przykładu.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Te zmiany do `app.js` Określ, czy kod wywołujący i wywoływane interfejsu API są w tej samej aplikacji usługi Azure AD.
7. Otwórz *app/scripts/homeCtrl.js* pliku.
8. Komentarz blok kodu oznaczone jako "bez uwierzytelniania" i Usuń komentarz blok kodu oznaczone jako "uwierzytelniania z".
9. Otwórz *app/scripts/indexCtrl.js* pliku.
10. Komentarz blok kodu oznaczone jako "bez uwierzytelniania" i Usuń komentarz blok kodu oznaczone jako "uwierzytelniania z".

### <a name="deploy-the-todolistangular-project-to-azure"></a>Wdrażanie projektu ToDoListAngular na platformie Azure
1. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy projekt ToDoListAngular, a następnie kliknij polecenie **Opublikuj**.
2. Kliknij przycisk **Opublikuj**.
   
    Visual Studio wdroży projekt i otworzy w przeglądarce podstawowy adres URL aplikacji sieci web. Wyświetli stronę błędu 403, co jest zrozumiałe próbę przejść do podstawowego adresu URL interfejsu API sieci Web w przeglądarce.
   
    Nadal trzeba wprowadzić zmianę do aplikacji interfejsu API warstwy środkowej, zanim można przetestować aplikację.
3. Zamknij przeglądarkę.

## <a name="configure-the-todolistapi-project-to-use-authentication"></a>Konfigurowanie projektu ToDoListAPI uwierzytelniania
Obecnie wysyła projekt ToDoListAPI "*" jako `owner` wartość ToDoListDataAPI. W tej sekcji możesz zmienić kod do wysyłania Identyfikatora zalogowanego użytkownika.

Wprowadź następujące zmiany w projekcie ToDoListAPI.

1. Otwórz *Controllers/ToDoListController.cs* pliku, a następnie usuń komentarz linii w każdej metody akcji, która ustawia `owner` do usługi Azure AD `NameIdentifier` wartości oświadczenia. Na przykład:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Ważne**: nie Usuń komentarz kodu w `ToDoListDataAPI` metody, należy to zrobić później w samouczku główna uwierzytelniania usługi.

### <a name="deploy-the-todolistapi-project-to-azure"></a>Wdrażanie projektu ToDoListAPI na platformie Azure
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListAPI, a następnie kliknij przycisk **publikowania**.
2. Kliknij przycisk **Opublikuj**.
   
    Visual Studio wdroży projekt i otworzy w przeglądarce podstawowy adres URL aplikacji interfejsu API.
3. Zamknij przeglądarkę.

### <a name="test-the-application"></a>Testowanie aplikacji
1. Przejdź do adresu URL aplikacji sieci web **przy użyciu protokołu HTTPS, a nie HTTP**.
2. Kliknij przycisk **listy zadań do wykonania** kartę.
   
    Zostanie wyświetlony monit logowania.
3. Zaloguj się przy użyciu poświadczeń użytkownika w dzierżawie usługi AAD.
4. **Listy zadań do wykonania** zostanie wyświetlona strona.
   
   ![Lista zadań do wykonania strony](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Nie elementów do wykonania są wyświetlane, ponieważ do tej pory wszystkie zostały one dla właściciela "*". Teraz warstwy środkowej żąda elementów dla zalogowanego użytkownika, a jeszcze nie zostały utworzone.
5. Dodawanie nowych elementów do wykonania, aby sprawdzić, czy aplikacja działa.
6. W innym oknie przeglądarki, przejdź do adresu URL interfejsu użytkownika programu Swagger dla aplikacji interfejsu API ToDoListDataAPI, a następnie kliknij przycisk **ToDoList > Pobierz**. Wprowadź gwiazdkę dla `owner` parametr, a następnie kliknij przycisk **wypróbować jej możliwości**.
   
   Odpowiedź pokazuje, że rzeczywiste nowych elementów do wykonania identyfikator użytkownika usługi Azure AD w właściwości Owner.
   
   ![Identyfikator właściciela w formacie JSON odpowiedzi](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a>Kompilowanie projektów od podstaw
Dwa projekty interfejsu API sieci Web zostały utworzone przy użyciu **aplikacji interfejsu API Azure** projektu szablonu i zastępowanie domyślnego kontrolera wartości z kontrolerem listy zadań. 

Aby uzyskać informacje o sposobie tworzenia aplikacji jednostronicowej AngularJS z wewnętrznej sieci Web API 2, zobacz [ręce w laboratorium: tworzenie jednej strony aplikacji JEDNOSTRONICOWEJ z interfejsu API sieci Web platformy ASP.NET i Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Aby uzyskać informacje o sposobie dodawania kod uwierzytelniania usługi Azure AD zobacz następujące zasoby:

* [Zabezpieczanie AngularJS pojedynczej strony aplikacji za pomocą usługi Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Wprowadzenie v1 ADAL JS](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Upewnij się, że użytkownik nie należy mylić (warstwy środkowej) ToDoListAPI i ToDoListDataAPI (warstwy danych). Na przykład Sprawdź, czy dodani uwierzytelniania do aplikacji interfejsu API warstwy środkowej, a nie w warstwie danych. 
* Upewnij się, czy kod źródłowy AngularJS odwołuje się adres URL aplikacji interfejsu API warstwy środkowej (ToDoListAPI, nie ToDoListDataAPI) i Azure poprawny identyfikator klienta usługi AD. 

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób użycia uwierzytelniania usługi aplikacji — dla aplikacji interfejsu API i sposób wywołania aplikacji interfejsu API przy użyciu biblioteki ADAL JS. W następnym samouczku dowiesz się, jak [bezpieczny dostęp do aplikacji interfejsu API dla scenariuszy service-to-service](app-service-api-dotnet-service-principal-auth.md).

