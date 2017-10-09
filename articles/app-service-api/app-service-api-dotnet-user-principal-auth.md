---
title: "aaaUser uwierzytelniania dla aplikacji interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprotect aplikację interfejsu API w usłudze Azure App Service, umożliwiając dostęp tooauthenticated tylko użytkowników."
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
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service
## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooprotect aplikacji interfejsu API platformy Azure, tak że tylko użytkownicy uwierzytelnieni można wywołać ją. Witaj artykule przyjęto założenie, że znasz hello [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md).

Dowiesz się:

* Jak tooconfigure dostawcę uwierzytelniania przy użyciu szczegółów dla usługi Azure Active Directory (Azure AD).
* Jak hello tooconsume chronionej aplikacji interfejsu API za pomocą [Active Directory Authentication Library (ADAL) dla języka JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Witaj artykuł zawiera dwie sekcje:

* Witaj [jak tooconfigure uwierzytelniania użytkowników w usłudze Azure App Service](#authconfig) sekcji opisano w sposób ogólny tooconfigure uwierzytelniania użytkowników w dowolnej aplikacji interfejsu API i stosuje jednakowo tooall platform obsługiwanych przez usługę App Service, w tym .NET, Node.js i Java.
* Począwszy od hello [kontynuowanie samouczków aplikacji interfejsu API programu .NET hello](#tutorialstart) sekcji, hello przewodniki artykułu użytkownika przez proces konfigurowania przykładowej aplikacji przy użyciu .NET wstecz zakończenia i frontonu AngularJS, korzystającą z usługi Azure Active Directory dla użytkownika uwierzytelnianie. 

## <a id="authconfig"></a>Jak tooconfigure uwierzytelniania użytkowników w usłudze Azure App Service
Ta sekcja zawiera ogólne instrukcje dotyczące tooany aplikacji interfejsu API. Dla tooDo toohello określonych czynności .NET listy przykładowej aplikacji, przejdź zbyt[kontynuowanie samouczki dotyczące rozpoczynania pracy .NET hello](#tutorialstart).

1. W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **ustawienia** bloku aplikacji hello interfejsu API, które mają tooprotect, Znajdź hello **funkcje** sekcji, a następnie kliknij przycisk  **Uwierzytelnianie / autoryzacja**.
   
    ![Portal Azure uwierzytelniania/autoryzacji](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. Wybierz jedną z opcji hello z hello **tootake akcji w przypadku nieuwierzytelnionego żądania** listy rozwijanej.
   
   * Jeśli chcesz tylko tooreach uwierzytelnionego połączenia aplikacji interfejsu API, wybierz jedną z hello **Zaloguj się przy użyciu...**  opcje. Ta opcja umożliwia tooprotect hello interfejsu API aplikacji bez pisania żadnego kodu działającą w nim.
   * Wszystkie wywołania tooreach aplikacji interfejsu API, wybierz opcję **Zezwalaj na żądanie (żadnej akcji)**. Możesz użyć tej opcji toodirect nieuwierzytelniony wywołań tooa wybór dostawców uwierzytelniania. Po wybraniu tej opcji należy toowrite kodu toohandle autoryzacji.
     
     Aby uzyskać więcej informacji, zobacz [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options) (Uwierzytelnianie i autoryzacja aplikacji interfejsu API w usłudze Azure App Service).
4. Wybierz co najmniej jeden hello **dostawców uwierzytelniania**.
   
    Obraz powitania zawiera opcje, które wymagają wszystkich toobe wywołań uwierzytelniony przez usługę Azure AD.
   
    ![Blok uwierzytelniania/autoryzacji portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Po wybraniu dostawcy uwierzytelniania hello portal Wyświetla blok konfiguracji dla tego dostawcy. 
   
    Aby uzyskać szczegółowe instrukcje, które opisują sposób tooconfigure hello bloków konfiguracji dostawcy uwierzytelniania, zobacz [jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (łącze hello prowadzi tooan artykuł na temat usługi Azure AD, ale samym artykule hello zawiera karty, które łącze tooarticles dla hello innych dostawców uwierzytelniania).
5. Po zakończeniu korzystania z bloku konfiguracji dostawcy uwierzytelniania hello, kliknij przycisk **OK**.
6. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.

Po zakończeniu usługi aplikacji uwierzytelnia wszystkie wywołania interfejsu API przed dotarciem hello aplikacji interfejsu API. działają usługi uwierzytelniania Hello hello takie same dla wszystkich języków, które obsługuje usługi aplikacji, w tym .NET, Node.js i Java. 

toomake uwierzytelnione wywołania interfejsu API, wywołujący hello zawiera token elementu nośnego OAuth 2.0 dostawcy uwierzytelniania hello w nagłówku autoryzacji hello żądań HTTP. Hello token można uzyskać przy użyciu dostawcy uwierzytelniania hello zestawu SDK.

## <a id="tutorialstart"></a>Kontynuowanie hello samouczków aplikacji interfejsu API programu .NET
Jeśli wykonujesz hello Node.js lub Java samouczków dotyczących aplikacji interfejsu API, Pomiń toohello kolejnym artykule [uwierzytelnianie główną usługi dla aplikacji interfejsu API](app-service-api-dotnet-service-principal-auth.md). 

Jeśli po hello serii samouczek platformy .NET dla aplikacji interfejsu API i został już wdrożony na powitania przykładowej aplikacji, zgodnie ze wskazówkami zawartymi w hello [pierwszy](app-service-api-dotnet-get-started.md) i [drugi](app-service-api-cors-consume-javascript.md) samouczki, Pomiń toohello [— Konfiguracja Uwierzytelnianie w aplikacji usługi i Azure AD](#azureauth) sekcji.

Jeśli chcesz toofollow w tym samouczku bez pośrednictwa hello pierwszego i drugiego samouczki, hello następujące kroki, które opisano sposób uruchamiania tooget przy użyciu zautomatyzowanego procesu toodeploy hello przykładowej aplikacji.

> [!NOTE]
> Witaj następujące kroki ułatwiające rozpoczęcie toohello uruchomienie tego samego punktu tak, jakby hello dwóch pierwszych samouczków, z jednym wyjątkiem: Visual Studio nie będzie już wiesz, które aplikacji sieci web lub aplikacji interfejsu API, który pobiera wdrożony każdego projektu. Oznacza to, nie będziesz mieć dokładne instrukcje w tym samouczku, które opisują sposób toodeploy toohello prawo celów. Jeśli nie masz doświadczenia z ustaleniem, jak kroki wdrożenia hello toodo samodzielnie, jest lepsze toofollow hello samouczek serii z hello [pierwszy samouczek](app-service-api-dotnet-get-started.md) niż toostart z tym zautomatyzowanego procesu wdrażania.
> 
> 

1. Upewnij się, że wszystkie wymagania wstępne hello na liście hello [pierwszy samouczek](app-service-api-dotnet-get-started.md). W przypadku dodawania toohello wymagania wstępne wymienione te samouczki uwierzytelniania założono, że mający doświadczenie z usługi aplikacji — aplikacje sieci web i aplikacji API apps w programie Visual Studio i hello portalu Azure.
2. Kliknij hello **wdrażanie tooAzure** przycisku na powitania [plik readme repozytorium przykładowej listy tooDo](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello interfejsu API apps i hello sieci web aplikacji. Zanotuj hello grupy zasobów platformy Azure, który jest tworzony w trakcie używania tego nowsze toolook aplikacji sieci web i nazwy aplikacji interfejsu API.
3. Pobieranie lub hello w klonowania [repozytorium przykładowej listy tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) tooget hello kodu, który lokalnie będzie działać z programu Visual Studio.

## <a id="azureauth"></a>Konfigurowanie uwierzytelniania w aplikacji usługi i usługi Azure AD
Masz teraz hello aplikacji uruchomionych w usłudze Azure App Service bez wymaga uwierzytelnienia użytkowników. W tej sekcji możesz dodać uwierzytelniania, wykonując hello następujące zadania:

* Skonfiguruj uwierzytelnianie usługi Azure Active Directory (Azure AD) toorequire usługi aplikacji — dla aplikacji interfejsu API warstwy środkowej hello podczas wywoływania.
* Tworzenie aplikacji usługi Azure AD.
* Po frontonu logowania toohello AngularJS, należy skonfigurować tokenu elementu nośnego hello toosend aplikacji hello Azure AD. 

Jeśli wystąpiły problemy podczas hello samouczek zalecenia, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji na końcu hello hello samouczka. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Konfigurowanie uwierzytelniania dla aplikacji interfejsu API warstwy środkowej hello
1. W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **ustawienia** bloku aplikacji hello interfejsu API, który został utworzony dla projektu ToDoListAPI hello, Znajdź hello **funkcje** sekcji, a następnie Kliknij przycisk **uwierzytelniania / autoryzacji**.
   
    ![Portal Azure uwierzytelniania/autoryzacji](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **na**.
3. W hello **tootake akcji w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj się za pomocą usługi Azure Active Directory**.
   
    Ta opcja zapewnia, że żadne żądania unauathenticated osiągną hello aplikacji interfejsu API. 
4. W obszarze **dostawców uwierzytelniania**, kliknij przycisk **usługi Azure Active Directory**.
   
    ![Blok uwierzytelniania/autoryzacji portalu Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. W hello **ustawień usługi Azure Active Directory** bloku, kliknij przycisk **Express**
   
    ![Opcja uwierzytelniania/autoryzacji Express portalu Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Z hello **Express** opcji usługi aplikacji może automatycznie tworzyć aplikację usługi Azure AD w usługi Azure AD [dzierżawy](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Nie masz toocreate dzierżawy, ponieważ jeden ma automatycznie co konto platformy Azure.
6. W obszarze **tryb zarządzania**, kliknij przycisk **Utwórz nową aplikację usługi AD** , jeśli nie została jeszcze wybrana i zwróć uwagę, wartość hello hello **tworzenie aplikacji** pole tekstowe; będzie wyszukiwanie tej usługi AAD Aplikacja w hello klasycznego portalu Azure później.
   
    ![Ustawienia portalu Azure usługi Azure AD](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure automatycznie utworzy aplikację usługi Azure AD o nazwie wskazanych hello w dzierżawie usługi Azure AD. Domyślnie program hello aplikacji usługi Azure AD o nazwie hello takie same jak aplikacja hello interfejsu API. Jeśli wolisz, możesz wprowadzić inną nazwę.
7. Kliknij przycisk **OK**.
8. W hello **uwierzytelniania / autoryzacji** bloku, kliknij przycisk **zapisać**.
   
    ![Klikanie pozycji Zapisz.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Obecnie tylko użytkownicy w Twojej dzierżawie usługi Azure AD mogą wywoływać hello aplikacji interfejsu API.

### <a name="optional-test-hello-api-app"></a>Opcjonalnie: Testowanie aplikacji hello interfejsu API
1. W przeglądarce Przejdź toohello adres URL aplikacji hello interfejsu API: w hello **aplikacji interfejsu API** bloku w hello portalu Azure, kliknij łącze hello w obszarze **adres URL**.  
   
    Jesteś ekran logowania przekierowanego tooa ponieważ nieuwierzytelnione żądania nie są dozwolone w aplikacji interfejsu API hello tooreach.
   
    Jeśli przeglądarka przejdzie do strony toohello "Pomyślnie utworzono", mogą już zarejestrowane przeglądarki hello — w takim przypadku otwórz sesję InPrivate lub Incognito okno i przejdź do adresu URL aplikacji toohello interfejsu API.
2. Zaloguj się przy użyciu poświadczeń dla użytkownika w dzierżawie usługi Azure AD.
   
    Gdy użytkownik jest zalogowany, hello "Pomyślnie utworzono" strona zostanie wyświetlona w przeglądarce hello.
3. Zamknij hello przeglądarki.

### <a name="configure-hello-azure-ad-application"></a>Konfigurowanie aplikacji hello Azure AD
Podczas konfigurowania uwierzytelniania usługi Azure AD usługi aplikacji tworzona aplikacja usługi Azure AD. Domyślnie aplikacja hello nowej usługi Azure AD został adres URL skonfigurowany tooprovide hello elementu nośnego toohello tokenu aplikacji interfejsu API. W tej sekcji skonfigurujesz hello Azure AD aplikacji tooprovide hello elementu nośnego tokenu toohello AngularJS frontonu zamiast bezpośrednio aplikacji interfejsu API warstwy środkowej toohello. Witaj AngularJS frontonu wyśle hello toohello token interfejsu API aplikacji, gdy wywołuje aplikację interfejsu API hello.

> [!NOTE]
> proces hello tookeep tak proste, jak to możliwe, w tym samouczku używana jednej usługi Azure AD aplikacji hello frontonu i hello aplikacji interfejsu API warstwy środkowej. Innym rozwiązaniem jest toouse dwóch aplikacji usługi Azure AD. W takim przypadku trzeba toogive hello frontonu dla usługi Azure AD aplikacji uprawnienia toocall hello warstwy środkowej przez aplikację usługi Azure AD. Takie podejście wieloma aplikacjami pozwoli uzyskać większą kontrolę nad warstwy tooeach uprawnienia.
> 
> 

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), przejdź do zbyt**usługi Azure Active Directory**.
   
   Masz toouse hello klasycznego portalu, ponieważ niektóre ustawienia usługi Azure Active Directory, które należy uzyskać dostęp nie jest jeszcze dostępna w bieżącym portalu Azure hello tooare.
2. Na powitania **katalogu** kliknij dzierżawę usługi AAD.
   
   ![Azure AD w klasycznym portalu](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Kliknij przycisk **aplikacji > aplikacje Moja firma jest właścicielem**, a następnie kliknij znacznik wyboru hello.
   
   Można również zainstalować toorefresh hello strony toosee hello nowej aplikacji.
4. Liście hello aplikacji kliknij nazwę hello hello, który Azure utworzony po włączeniu uwierzytelniania dla aplikacji interfejsu API.
   
   ![Karta aplikacje AD platformy Azure](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Kliknij pozycję **Konfiguruj**.
   
   ![Karta Konfigurowanie AD platformy Azure](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Ustaw **adres URL logowania** toohello adres URL aplikacji sieci web AngularJS, nie ma ukośników.
   
   Na przykład: https://todolistangular.azurewebsites.net
   
   ![Adres URL logowania](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Ustaw **adres URL odpowiedzi** toohello adres URL aplikacji sieci web, nie ma ukośników.
   
   Na przykład: https://todolistsangular.azurewebsites.net
8. Kliknij pozycję **Zapisz**.
   
   ![Adres URL odpowiedzi](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. U dołu hello hello strony, kliknij przycisk **manifest Zarządzaj > Pobierz manifest**.
   
   ![Pobierz manifest](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Pobierz tooa lokalizację pliku hello, gdzie można go edytować.
11. W pliku manifestu hello pobrane, wyszukaj hello `oauth2AllowImplicitFlow` właściwości. Zmień wartość hello tej właściwości z `false` zbyt`true`, a następnie zapisz plik hello.
    
    To ustawienie jest wymagane do uzyskania dostępu z poziomu aplikacji jednostronicowej JavaScript. Umożliwia on hello Oauth 2.0 elementu nośnego tokenu toobe zwracane w hello fragmentu adresu URL.
12. Kliknij przycisk **manifest Zarządzaj > manifest przekazywania**oraz przekazywanie hello zaktualizowane w hello poprzedzających krok.
    
    ![Przekaż manifestu](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopiuj hello **identyfikator klienta** wartość i zapisz go w innym miejscu możesz pobrać go z później.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Skonfiguruj uwierzytelnianie toouse projektu ToDoListAngular hello
W tej sekcji możesz zmienić hello AngularJS frontonu tak, aby korzystała Active Directory Authentication Library (ADAL) dla tooacquire JS tokenu elementu nośnego hello zalogowanego użytkownika z usługi Azure AD. Kod Hello włączy hello token żądania HTTP wysyłane toohello warstwy środkowej, pokazane na powitania po diagramu. 

![Diagram uwierzytelniania użytkownika](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Należy powitania po toofiles zmiany w hello projektu ToDoListAngular.

1. Otwórz hello *index.cshtml* pliku.
2. Usuń znaczniki komentarza hello wierszy, które odwołują się hello Active Directory Authentication Library (ADAL) dla skryptów Javascript.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Otwórz hello *app/scripts/app.js* pliku.
4. Komentarz hello bloku kodu oznaczony jako przeznaczony do "bez uwierzytelniania" i Usuń komentarz hello bloku kodu oznaczone jako "uwierzytelniania z".
   
    Ta zmiana odwołuje się do dostawcy uwierzytelniania ADAL JS hello i udostępnia tooit wartości konfiguracji. W hello następujące kroki, można ustawić wartości konfiguracji hello aplikacji interfejsu API i aplikacji usługi Azure AD.
5. W kodzie hello, która ustawia hello `endpoints` hello zmiennej, Ustaw adres URL interfejsu API toohello adres URL aplikacji hello interfejsu API, który został utworzony dla projektu ToDoListAPI hello i ustawić hello Azure AD identyfikator toohello identyfikator klienta aplikacji skopiowany z hello klasycznego portalu Azure.
   
    Kod Hello jest teraz toohello podobnie poniższy przykład.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Hello zbyt wywołać`adalProvider.init`ustaw `tenant` tooyour nazwa dzierżawcy i `clientId` toosame wartość używana w poprzednim kroku hello.
   
    Kod Hello jest teraz toohello podobnie poniższy przykład.
   
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
   
    Te zmiany zbyt`app.js` zdecydować, że kod wywołujący hello i hello wywołuje interfejs API w aplikacji hello tej samej usługi Azure AD.
7. Otwórz hello *app/scripts/homeCtrl.js* pliku.
8. Komentarz hello bloku kodu oznaczony jako przeznaczony do "bez uwierzytelniania" i Usuń komentarz hello bloku kodu oznaczone jako "uwierzytelniania z".
9. Otwórz hello *app/scripts/indexCtrl.js* pliku.
10. Komentarz hello bloku kodu oznaczony jako przeznaczony do "bez uwierzytelniania" i Usuń komentarz hello bloku kodu oznaczone jako "uwierzytelniania z".

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Wdrażanie tooAzure projektu ToDoListAngular hello
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListAngular hello, a następnie kliknij przycisk **publikowania**.
2. Kliknij przycisk **Opublikuj**.
   
    Visual Studio wdroży projekt hello i otwiera podstawowy adres URL przeglądarki toohello aplikacji sieci web. Wyświetli stronę błędu 403, co jest zrozumiałe dla próba toogo tooa interfejsu API sieci Web podstawowego adresu URL w przeglądarce.
   
    Nadal masz toomake warstwy środkowej toohello aplikacji interfejsu API zmiany przed można przetestować aplikację hello.
3. Zamknij hello przeglądarki.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Skonfiguruj uwierzytelnianie toouse projektu ToDoListAPI hello
Obecnie hello wysyła projektu ToDoListAPI "*" jako hello `owner` tooToDoListDataAPI wartość. W tej sekcji możesz zmienić identyfikator hello toosend kodu hello hello zalogowanego użytkownika.

Wprowadź następujące zmiany w projekcie ToDoListAPI hello hello.

1. Otwórz hello *Controllers/ToDoListController.cs* pliku, a następnie usuń komentarz linii hello w każdej metody akcji, która ustawia `owner` toohello usługi Azure AD `NameIdentifier` wartości oświadczenia. Na przykład:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Ważne**: nie Usuń komentarz kodu w hello `ToDoListDataAPI` metody, należy to zrobić później hello usługi uwierzytelniania główna samouczek.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Wdrażanie tooAzure projektu ToDoListAPI hello
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListAPI hello, a następnie kliknij przycisk **publikowania**.
2. Kliknij przycisk **Opublikuj**.
   
    Visual Studio wdroży projekt hello i otwiera podstawowy adres URL przeglądarki toohello aplikacji interfejsu API.
3. Zamknij hello przeglądarki.

### <a name="test-hello-application"></a>Testowanie aplikacji hello
1. Przejdź do adresu URL toohello hello aplikacji sieci web, **przy użyciu protokołu HTTPS, a nie HTTP**.
2. Kliknij przycisk hello **tooDo listy** kartę.
   
    Jesteś zostanie wyświetlony monit o toolog w.
3. Zaloguj się za pomocą hello poświadczeń użytkownika w dzierżawie usługi AAD.
4. Witaj **tooDo listy** zostanie wyświetlona strona.
   
   ![Strona z listą tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Nie elementów do wykonania są wyświetlane, ponieważ do tej pory wszystkie zostały one dla właściciela "*". Teraz warstwy środkowej hello żąda elementy hello zalogowanego użytkownika, a jeszcze nie zostały utworzone.
5. Dodaj nowy tooverify elementy zadań do wykonania aplikacja hello działa.
6. W innym oknie przeglądarki Przejdź toohello Swagger URL interfejsu użytkownika dla aplikacji interfejsu API ToDoListDataAPI hello i kliknij polecenie **ToDoList > Pobierz**. Wprowadź znak gwiazdki hello `owner` parametr, a następnie kliknij przycisk **wypróbować jej możliwości**.
   
   odpowiedź Hello pokazuje, że hello nowych elementów do wykonania ma identyfikator użytkownika hello rzeczywiste usługi Azure AD w hello właściwości Owner.
   
   ![Identyfikator właściciela w formacie JSON odpowiedzi](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Kompilowanie projektów powitania od podstaw
Witaj dwa projekty interfejsu API sieci Web zostały utworzone przy użyciu hello **aplikacji interfejsu API Azure** szablonu i zastąpienie hello domyślne wartości kontroler z kontrolerem listy zadań projektu. 

Aby uzyskać informacje na temat za tworzenie aplikacji jednostronicowej AngularJS ze zaplecze 2 interfejsu API sieci Web, zobacz [ręce w laboratorium: tworzenie jednej strony aplikacji JEDNOSTRONICOWEJ z interfejsu API sieci Web platformy ASP.NET i Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Aby uzyskać informacje na temat tooadd kod uwierzytelniania usługi Azure AD, zobacz następujące zasoby hello:

* [Zabezpieczanie AngularJS pojedynczej strony aplikacji za pomocą usługi Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Wprowadzenie v1 ADAL JS](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Upewnij się, że użytkownik nie należy mylić (warstwy środkowej) ToDoListAPI i ToDoListDataAPI (warstwy danych). Na przykład Sprawdź, czy dodani aplikacji interfejsu API warstwy środkowej toohello uwierzytelniania, nie hello warstwy danych. 
* Upewnij się, że adres URL aplikacji hello AngularJS źródła kodu odwołania hello warstwy środkowej API (ToDoListAPI, nie ToDoListDataAPI) i hello poprawne identyfikator klienta usługi Azure AD. 

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób toouse uwierzytelniania usługi aplikacji — dla aplikacji interfejsu API i jak toocall hello aplikacji interfejsu API za pomocą hello bibliotekę ADAL JS. W następnym samouczku hello dowiesz się, jak za[bezpiecznego dostępu do aplikacji tooyour interfejsu API dla scenariuszy service to service](app-service-api-dotnet-service-principal-auth.md).

