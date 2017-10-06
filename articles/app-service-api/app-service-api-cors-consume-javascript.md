---
title: "obsługuje aaaCORS w usłudze App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak obsługują toouse CORS w usłudze Azure App Service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Korzystanie z aplikacji interfejsu API z poziomu języka JavaScript przy użyciu mechanizmu CORS
Usługa App Service oferuje wbudowaną obsługę [między CORS Origin Resource Sharing ()](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), co pozwala JavaScript klientów toomake międzydomenowego wywołuje tooAPIs, które są obsługiwane w aplikacjach interfejsu API. Usługi aplikacji — umożliwia konfigurowanie mechanizmu CORS access tooyour interfejsu API bez pisania żadnego kodu interfejsu API.

Ten artykuł zawiera dwie sekcje:

* Witaj [jak tooconfigure CORS](#corsconfig) sekcji opisano w sposób ogólny tooconfigure CORS dla dowolnej aplikacji interfejsu API, aplikacji sieci web lub aplikacji mobilnej. Ma to zastosowanie jednakowo tooall platform, które są obsługiwane przez usługę App Service, w tym .NET, Node.js i Java. 
* Począwszy od hello [kontynuowanie samouczki dotyczące rozpoczynania pracy .NET hello](#tutorialstart) sekcji hello artykuł stanowi początek samouczka demonstrującego Obsługa mechanizmu CORS w postaci jak w [hello pierwszej aplikacji interfejsu API samouczku ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Jak tooconfigure CORS w usłudze Azure App Service
Mechanizm CORS można skonfigurować w portalu Azure hello lub za pomocą [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) narzędzia.

#### <a name="configure-cors-in-hello-azure-portal"></a>Konfigurowanie mechanizmu CORS w portalu Azure hello
1. W przeglądarce Przejdź toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji interfejsu API.
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. W hello **ustawienia** bloku, który zostanie otwarty po prawej toohello hello **aplikacji interfejsu API** bloku, Znajdź hello **interfejsu API** sekcji, a następnie kliknij przycisk **CORS**.
   
   ![Wybieranie pozycji CORS w bloku Ustawienia](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. W polu tekstowym hello wprowadź hello adres URL lub adresów URL, które mają toocome wywołania języka JavaScript tooallow z.

    Na przykład jeśli wdrożono JavaScript aplikacji tooa aplikacji sieci web o nazwie todolistangular, wpisz "https://todolistangular.azurewebsites.net". Alternatywnie można wprowadzić toospecify gwiazdki (*), że wszystkie domeny pochodzenia są akceptowane.


1. Kliknij pozycję **Zapisz**.
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Po kliknięciu **zapisać**, aplikacja hello interfejsu API będzie akceptować JavaScript wywołania z hello określonych adresów URL.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Konfigurowanie mechanizmu CORS za pomocą narzędzi usługi Azure Resource Manager
Mechanizm CORS można skonfigurować dla aplikacji interfejsu API, za pomocą [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) narzędzi wiersza polecenia, takich jak [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) i hello [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md). 

Na przykład szablonu usługi Azure Resource Manager, który ustawia właściwości CORS hello Otwórz hello [plik azuredeploy.json w repozytorium hello w tym samouczku przykładowej aplikacji](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Znajdź sekcję hello szablonu hello, która wygląda podobnie poniższy przykład hello:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Kontynuowanie hello platformy .NET — Wprowadzenie — samouczek
Jeśli wykonujesz hello Node.js lub Java serii wprowadzającej dla aplikacji interfejsu API, masz hello Ukończono pobieranie kończysz tę serię. Pomiń toohello [następne kroki](#next-steps) sekcji toofind sugestie dotyczące kontynuowanie poznawania usługi API Apps.

Hello dalszej części tego artykułu stanowi kontynuację serii wprowadzającej .NET hello przyjęto założenie, że udało Ci się ukończyć [hello pierwszy samouczek](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Wdrażanie hello projektu tooa nowej aplikacji sieci web ToDoListAngular
W [hello pierwszy samouczek](app-service-api-dotnet-get-started.md), utworzono aplikację interfejsu API warstwy środkowej i aplikacji interfejsu API warstwy danych. W tym samouczku utworzysz aplikację sieci web jednostronicowej aplikacji JEDNOSTRONICOWEJ, aplikacja interfejsu API warstwy środkowej hello wywołania. Hello SPA toowork masz tooenable CORS w aplikacji interfejsu API warstwy środkowej hello. 

W hello [Przykładowa aplikacja ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projekt ToDoListAngular hello jest prostym klientem AngularJS, która wywołuje hello warstwy środkowej ToDoListAPI interfejsu API sieci Web projektu. Witaj kodu JavaScript na powitania *app/scripts/todoListSvc.js* plik wywołuje interfejs API hello za pomocą dostawcy usługi AngularJS HTTP hello. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Utwórz nową aplikację sieci web dla projektu ToDoListAngular hello
Witaj toocreate procedury nowej aplikacji sieci web usługi aplikacji i wdrażania projektu tooit jest podobne toowhat instrukcji dotyczących [tworzenie i wdrażanie aplikacji interfejsu API w pierwszym samouczku tej serii hello](app-service-api-dotnet-get-started.md#createapiapp). Witaj tylko różnica polega na ten typ aplikacji hello jest **aplikacji sieci Web** zamiast **aplikacji interfejsu API**.  Aby uzyskać zrzuty ekranu hello w oknach dialogowych zobacz 

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListAngular hello, a następnie kliknij przycisk **publikowania**.
2. W hello **profilu** kartę hello **publikowanie w sieci Web** kreatora, kliknij przycisk **Microsoft Azure App Service**.
3. W hello **usługi aplikacji** okno dialogowe, kliknij przycisk **nowy**.
4. W hello **hostingu** kartę hello **Tworzenie usługi App Service** okna dialogowego wprowadź **Nazwa aplikacji sieci Web** jest unikatowa w hello *azurewebsites.net* domeny. 
5. Wybierz hello Azure **subskrypcji** ma toowork z.
6. W hello **grupy zasobów** listy rozwijanej wybierz hello utworzoną wcześniej tej samej grupie zasobów.
7. W hello **Plan usługi App Service** listy rozwijanej wybierz hello wcześniej utworzony plan. 
8. Kliknij przycisk **Utwórz**.
   
    Visual Studio utworzy aplikację sieci web hello, tworzy profil publikowania dla niego i wyświetla hello **połączenia** krok hello **publikowanie w sieci Web** kreatora.
   
    W tym momencie nie klikaj pozycji **Opublikuj**. W następującej sekcji hello możesz skonfigurować hello nowej aplikacji sieci web aplikacji toocall hello interfejsu API warstwy środkowej działającej w usłudze App Service. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Ustaw hello adresu URL warstwy środkowej w ustawieniach aplikacji sieci web
1. Przejdź toohello [portalu Azure](https://portal.azure.com/), a następnie przejdź toohello **aplikacji sieci Web** bloku dla aplikacji sieci web hello utworzony projekt TodoListAngular (frontonu) hello toohost.
2. Kliknij kolejno pozycje **Ustawienia > Ustawienia aplikacji**.
3. W hello **ustawień aplikacji** Dodaj hello następujący klucz i wartość:
   
   | Klucz | Wartość | Przykład |
   | --- | --- | --- |
   | toDoListAPIURL |https://{nazwa aplikacji interfejsu API warstwy środkowej}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Kliknij pozycję **Zapisz**.
   
    Gdy hello kod działa na platformie Azure, ta wartość zastępuje hello URL localhost, który znajduje się w hello *Web.config* pliku. 
   
    Kod Hello pobiera wartość ustawienia hello jest *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Witaj kodu w *todoListSvc.js* używa ustawienia hello:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Wdrażanie hello sieci web projektu toohello nowej aplikacji sieci web ToDoListAngular
* W programie Visual Studio w hello **połączenia** krok hello **publikowanie w sieci Web** kreatora, kliknij przycisk **publikowania**.
  
   Visual Studio wdroży hello ToDoListAngular projektu toohello nowej aplikacji sieci web i otworzy przeglądarki toohello adres URL aplikacji sieci web hello. 

### <a name="test-hello-application-without-cors-enabled"></a>Testowanie aplikacji hello bez włączonego mechanizmu CORS
1. W przeglądarce Developer Tools Otwórz okno konsoli hello.
2. W oknie przeglądarki hello Wyświetla hello interfejs użytkownika klienta AngularJS, kliknij przycisk hello **tooDo listy** łącza.
   
    Hello kod JavaScript próbuje warstwy środkowej toocall hello aplikacji interfejsu API, ale wywołanie hello nie powiedzie się, ponieważ fronton hello jest uruchomiony w innej domenie niż hello wstecz zakończenia. okno konsoli narzędzi dla deweloperów w przeglądarce Hello zawiera komunikat o błędzie między źródłami.
   
    ![Komunikat o błędzie między źródłami](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Konfigurowanie mechanizmu CORS dla aplikacji interfejsu API warstwy środkowej hello
W tej sekcji skonfigurujesz ustawienia mechanizmu CORS hello na platformie Azure dla aplikacji interfejsu API ToDoListAPI warstwy środkowej hello. To ustawienie umożliwia hello warstwę środkową interfejsu API aplikacji tooreceive wywołania języka JavaScript z aplikacji sieci web hello, który został utworzony dla projektu ToDoListAngular hello.

1. W przeglądarce Przejdź toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **usługi aplikacji**, a następnie kliknij przycisk aplikacji hello interfejsu API (warstwy środkowej) ToDoListAPI.
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. W hello **ustawienia** bloku, który zostanie otwarty po prawej toohello hello **aplikacji interfejsu API** bloku, Znajdź hello **interfejsu API** sekcji, a następnie kliknij przycisk **CORS**.
   
   ![Wybieranie mechanizmu CORS w portalu](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. W polu tekstowym hello wprowadź adres URL hello aplikacji sieci web ToDoListAngular (frontonu) hello. Na przykład, jeśli wdrożono hello ToDoListAngular projektu tooa sieci web aplikacji o nazwie todolistangular0121, zezwala na wywołania z adresu URL hello `https://todolistangular0121.azurewebsites.net`.
   
   Alternatywnie można wprowadzić toospecify gwiazdki (*), że wszystkie domeny pochodzenia są akceptowane.
5. Kliknij pozycję **Zapisz**.
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Po kliknięciu **zapisać**, aplikacja hello interfejsu API będzie akceptować JavaScript wywołania z hello określonego adresu URL. Na tym zrzucie ekranu aplikacji interfejsu API ToDoListAPI0223 hello będzie akceptować wywołań klienta języka JavaScript z aplikacji sieci web ToDoListAngular hello.

### <a name="test-hello-application-with-cors-enabled"></a>Testowanie aplikacji hello z włączonym mechanizmem CORS
* Otwórz przeglądarkę toohello adres URL HTTPS aplikacji sieci web hello. 
  
    Ta aplikacja hello czasu pozwala wyświetlić, dodawanie, edytowanie i usuwanie elementów do wykonania. 
  
    ![Strona z listą tooDo przykładowej aplikacji](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>Porównanie mechanizmu CORS usługi App Service i mechanizmu CORS interfejsu API sieci Web
W projekcie interfejsu API sieci Web można zainstalować hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify pakietu NuGet w kodzie domen interfejsu API będzie akceptować wywołania języka JavaScript z.

Obsługa mechanizmu CORS interfejsu API sieci Web jest bardziej elastyczna niż obsługa mechanizmu CORS usługi App Service. Na przykład za pomocą kodu można określić różne dozwolone źródła dla różnych metod akcji, natomiast mechanizm CORS usługi App Service pozwala skonfigurować tylko jeden zestaw dozwolonych źródeł dla wszystkich metod aplikacji interfejsu API.

> [!NOTE]
> Nie próbuj toouse zarówno mechanizmu CORS interfejsu API sieci Web i mechanizmu CORS usługi App Service w jednej aplikacji interfejsu API. Mechanizm CORS usługi App Service ma wyższy priorytet, co sprawia, że użycie mechanizmu CORS interfejsu API sieci Web nie odniesie żadnego skutku. Na przykład jeśli jedną domenę pochodzenia w usłudze App Service, a następnie włączyć wszystkie domeny pochodzenia w kodzie interfejsu API sieci Web, aplikacja interfejsu API platformy Azure będzie akceptować tylko wywołania z domeny hello, określone na platformie Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Jak tooenable CORS w kodzie interfejsu API sieci Web
następujące kroki Hello podsumowanie hello procesu włączania obsługi mechanizmu CORS interfejsu API sieci Web. Aby uzyskać więcej informacji, zobacz [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Włączanie żądań Cross-Origin w interfejsie API sieci Web 2 platformy ASP.NET).

1. W projekcie interfejsu API sieci Web, należy zainstalować hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pakietu NuGet.
2. Obejmują `config.EnableCors()` wiersza kodu w hello **zarejestrować** metody hello **WebApiConfig** klasy, jak hello poniższy przykład. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. W kontrolerze interfejsu API sieci Web Dodaj `using` instrukcji dla hello `System.Web.Http.Cors` przestrzeni nazw i Dodaj hello `EnableCors` atrybutu toohello klasy lub tooindividual metody akcji kontrolera. W hello poniższy przykład obsługi mechanizmu CORS dotyczy całego kontrolera toohello.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Używanie usługi Azure API Management z usługą API Apps
Jeśli używasz usługi Azure API Management z aplikacją interfejsu API, Konfigurowanie mechanizmu CORS w usłudze API Management zamiast w aplikacji interfejsu API hello. Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Omówienie usługi Azure API Management (klip wideo, informacje dotyczące mechanizmu CORS są prezentowane od momentu 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [Zasady usługi API Management obejmujące różne domeny](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
W przypadku napotkania problemów podczas pracy z tym samouczkiem skorzystaj z poniższych sugestii dotyczących ich rozwiązywania.

* Upewnij się, że używasz najnowszej wersji hello hello [zestawu Azure SDK dla platformy .NET dla programu Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Upewnij się, że wprowadzono `https` w hello ustawienia mechanizmu CORS i upewnij się, że używasz `https` toorun hello frontonu sieci web aplikacji.
* Upewnij się, czy wprowadzono hello ustawienia mechanizmu CORS w aplikacji interfejsu API warstwy środkowej hello, a nie w aplikacji frontonu sieci web hello.
* Jeśli konfigurujesz mechanizm CORS w kodzie aplikacji i usłudze Azure App Service, należy pamiętać, że ustawienia mechanizmu CORS usługi aplikacji hello zastąpią instrukcje zawarte w kodzie aplikacji. 

toolearn więcej informacji na temat funkcji programu Visual Studio, które ułatwiają rozwiązywanie problemów, zobacz [Rozwiązywanie problemów z usługi aplikacji Azure aplikacji w programie Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono, jak tooenable mechanizmu CORS usługi App Service obsługuje tak, że kod języka JavaScript klienta można wywołać interfejsu API w innej domenie. toolearn więcej o aplikacjach interfejsu API, przeczytaj hello [tooauthentication wprowadzenie w usłudze App Service](../app-service/app-service-authentication-overview.md), a następnie przejdź toohello [uwierzytelniania użytkowników dla aplikacji interfejsu API](app-service-api-dotnet-user-principal-auth.md) samouczka.

