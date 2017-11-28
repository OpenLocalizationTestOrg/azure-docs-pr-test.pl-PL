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
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="eb722-103">Korzystanie z aplikacji interfejsu API z poziomu języka JavaScript przy użyciu mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="eb722-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="eb722-104">Usługa App Service oferuje wbudowaną obsługę [między CORS Origin Resource Sharing ()](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), co pozwala JavaScript klientów toomake międzydomenowego wywołuje tooAPIs, które są obsługiwane w aplikacjach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="eb722-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="eb722-105">Usługi aplikacji — umożliwia konfigurowanie mechanizmu CORS access tooyour interfejsu API bez pisania żadnego kodu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="eb722-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="eb722-106">Ten artykuł zawiera dwie sekcje:</span><span class="sxs-lookup"><span data-stu-id="eb722-106">This article contains two sections:</span></span>

* <span data-ttu-id="eb722-107">Witaj [jak tooconfigure CORS](#corsconfig) sekcji opisano w sposób ogólny tooconfigure CORS dla dowolnej aplikacji interfejsu API, aplikacji sieci web lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="eb722-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="eb722-108">Ma to zastosowanie jednakowo tooall platform, które są obsługiwane przez usługę App Service, w tym .NET, Node.js i Java.</span><span class="sxs-lookup"><span data-stu-id="eb722-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="eb722-109">Począwszy od hello [kontynuowanie samouczki dotyczące rozpoczynania pracy .NET hello](#tutorialstart) sekcji hello artykuł stanowi początek samouczka demonstrującego Obsługa mechanizmu CORS w postaci jak w [hello pierwszej aplikacji interfejsu API samouczku ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb722-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="eb722-110"><a id="corsconfig"></a>Jak tooconfigure CORS w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="eb722-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="eb722-111">Mechanizm CORS można skonfigurować w portalu Azure hello lub za pomocą [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="eb722-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="eb722-112">Konfigurowanie mechanizmu CORS w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="eb722-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="eb722-113">W przeglądarce Przejdź toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb722-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eb722-114">Kliknij przycisk **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="eb722-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="eb722-116">W hello **ustawienia** bloku, który zostanie otwarty po prawej toohello hello **aplikacji interfejsu API** bloku, Znajdź hello **interfejsu API** sekcji, a następnie kliknij przycisk **CORS**.</span><span class="sxs-lookup"><span data-stu-id="eb722-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Wybieranie pozycji CORS w bloku Ustawienia](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="eb722-118">W polu tekstowym hello wprowadź hello adres URL lub adresów URL, które mają toocome wywołania języka JavaScript tooallow z.</span><span class="sxs-lookup"><span data-stu-id="eb722-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="eb722-119">Na przykład jeśli wdrożono JavaScript aplikacji tooa aplikacji sieci web o nazwie todolistangular, wpisz "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="eb722-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="eb722-120">Alternatywnie można wprowadzić toospecify gwiazdki (*), że wszystkie domeny pochodzenia są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="eb722-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="eb722-121">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eb722-121">Click **Save**.</span></span>
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="eb722-123">Po kliknięciu **zapisać**, aplikacja hello interfejsu API będzie akceptować JavaScript wywołania z hello określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="eb722-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="eb722-124">Konfigurowanie mechanizmu CORS za pomocą narzędzi usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eb722-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="eb722-125">Mechanizm CORS można skonfigurować dla aplikacji interfejsu API, za pomocą [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) narzędzi wiersza polecenia, takich jak [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) i hello [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="eb722-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="eb722-126">Na przykład szablonu usługi Azure Resource Manager, który ustawia właściwości CORS hello Otwórz hello [plik azuredeploy.json w repozytorium hello w tym samouczku przykładowej aplikacji](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="eb722-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="eb722-127">Znajdź sekcję hello szablonu hello, która wygląda podobnie poniższy przykład hello:</span><span class="sxs-lookup"><span data-stu-id="eb722-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="eb722-128"><a id="tutorialstart"></a>Kontynuowanie hello platformy .NET — Wprowadzenie — samouczek</span><span class="sxs-lookup"><span data-stu-id="eb722-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="eb722-129">Jeśli wykonujesz hello Node.js lub Java serii wprowadzającej dla aplikacji interfejsu API, masz hello Ukończono pobieranie kończysz tę serię.</span><span class="sxs-lookup"><span data-stu-id="eb722-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="eb722-130">Pomiń toohello [następne kroki](#next-steps) sekcji toofind sugestie dotyczące kontynuowanie poznawania usługi API Apps.</span><span class="sxs-lookup"><span data-stu-id="eb722-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="eb722-131">Hello dalszej części tego artykułu stanowi kontynuację serii wprowadzającej .NET hello przyjęto założenie, że udało Ci się ukończyć [hello pierwszy samouczek](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb722-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="eb722-132">Wdrażanie hello projektu tooa nowej aplikacji sieci web ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="eb722-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="eb722-133">W [hello pierwszy samouczek](app-service-api-dotnet-get-started.md), utworzono aplikację interfejsu API warstwy środkowej i aplikacji interfejsu API warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="eb722-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="eb722-134">W tym samouczku utworzysz aplikację sieci web jednostronicowej aplikacji JEDNOSTRONICOWEJ, aplikacja interfejsu API warstwy środkowej hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="eb722-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="eb722-135">Hello SPA toowork masz tooenable CORS w aplikacji interfejsu API warstwy środkowej hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="eb722-136">W hello [Przykładowa aplikacja ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projekt ToDoListAngular hello jest prostym klientem AngularJS, która wywołuje hello warstwy środkowej ToDoListAPI interfejsu API sieci Web projektu.</span><span class="sxs-lookup"><span data-stu-id="eb722-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="eb722-137">Witaj kodu JavaScript na powitania *app/scripts/todoListSvc.js* plik wywołuje interfejs API hello za pomocą dostawcy usługi AngularJS HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="eb722-138">Utwórz nową aplikację sieci web dla projektu ToDoListAngular hello</span><span class="sxs-lookup"><span data-stu-id="eb722-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="eb722-139">Witaj toocreate procedury nowej aplikacji sieci web usługi aplikacji i wdrażania projektu tooit jest podobne toowhat instrukcji dotyczących [tworzenie i wdrażanie aplikacji interfejsu API w pierwszym samouczku tej serii hello](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="eb722-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="eb722-140">Witaj tylko różnica polega na ten typ aplikacji hello jest **aplikacji sieci Web** zamiast **aplikacji interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="eb722-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="eb722-141">Aby uzyskać zrzuty ekranu hello w oknach dialogowych zobacz</span><span class="sxs-lookup"><span data-stu-id="eb722-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="eb722-142">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt ToDoListAngular hello, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="eb722-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="eb722-143">W hello **profilu** kartę hello **publikowanie w sieci Web** kreatora, kliknij przycisk **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="eb722-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="eb722-144">W hello **usługi aplikacji** okno dialogowe, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="eb722-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="eb722-145">W hello **hostingu** kartę hello **Tworzenie usługi App Service** okna dialogowego wprowadź **Nazwa aplikacji sieci Web** jest unikatowa w hello *azurewebsites.net* domeny.</span><span class="sxs-lookup"><span data-stu-id="eb722-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="eb722-146">Wybierz hello Azure **subskrypcji** ma toowork z.</span><span class="sxs-lookup"><span data-stu-id="eb722-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="eb722-147">W hello **grupy zasobów** listy rozwijanej wybierz hello utworzoną wcześniej tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb722-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="eb722-148">W hello **Plan usługi App Service** listy rozwijanej wybierz hello wcześniej utworzony plan.</span><span class="sxs-lookup"><span data-stu-id="eb722-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="eb722-149">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eb722-149">Click **Create**.</span></span>
   
    <span data-ttu-id="eb722-150">Visual Studio utworzy aplikację sieci web hello, tworzy profil publikowania dla niego i wyświetla hello **połączenia** krok hello **publikowanie w sieci Web** kreatora.</span><span class="sxs-lookup"><span data-stu-id="eb722-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="eb722-151">W tym momencie nie klikaj pozycji **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="eb722-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="eb722-152">W następującej sekcji hello możesz skonfigurować hello nowej aplikacji sieci web aplikacji toocall hello interfejsu API warstwy środkowej działającej w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="eb722-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="eb722-153">Ustaw hello adresu URL warstwy środkowej w ustawieniach aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="eb722-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="eb722-154">Przejdź toohello [portalu Azure](https://portal.azure.com/), a następnie przejdź toohello **aplikacji sieci Web** bloku dla aplikacji sieci web hello utworzony projekt TodoListAngular (frontonu) hello toohost.</span><span class="sxs-lookup"><span data-stu-id="eb722-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="eb722-155">Kliknij kolejno pozycje **Ustawienia > Ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="eb722-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="eb722-156">W hello **ustawień aplikacji** Dodaj hello następujący klucz i wartość:</span><span class="sxs-lookup"><span data-stu-id="eb722-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="eb722-157">Klucz</span><span class="sxs-lookup"><span data-stu-id="eb722-157">Key</span></span> | <span data-ttu-id="eb722-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="eb722-158">Value</span></span> | <span data-ttu-id="eb722-159">Przykład</span><span class="sxs-lookup"><span data-stu-id="eb722-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="eb722-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="eb722-160">toDoListAPIURL</span></span> |<span data-ttu-id="eb722-161">https://{nazwa aplikacji interfejsu API warstwy środkowej}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="eb722-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="eb722-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="eb722-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="eb722-163">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eb722-163">Click **Save**.</span></span>
   
    <span data-ttu-id="eb722-164">Gdy hello kod działa na platformie Azure, ta wartość zastępuje hello URL localhost, który znajduje się w hello *Web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="eb722-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="eb722-165">Kod Hello pobiera wartość ustawienia hello jest *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="eb722-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="eb722-166">Witaj kodu w *todoListSvc.js* używa ustawienia hello:</span><span class="sxs-lookup"><span data-stu-id="eb722-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="eb722-167">Wdrażanie hello sieci web projektu toohello nowej aplikacji sieci web ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="eb722-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="eb722-168">W programie Visual Studio w hello **połączenia** krok hello **publikowanie w sieci Web** kreatora, kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="eb722-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="eb722-169">Visual Studio wdroży hello ToDoListAngular projektu toohello nowej aplikacji sieci web i otworzy przeglądarki toohello adres URL aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="eb722-170">Testowanie aplikacji hello bez włączonego mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="eb722-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="eb722-171">W przeglądarce Developer Tools Otwórz okno konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="eb722-172">W oknie przeglądarki hello Wyświetla hello interfejs użytkownika klienta AngularJS, kliknij przycisk hello **tooDo listy** łącza.</span><span class="sxs-lookup"><span data-stu-id="eb722-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="eb722-173">Hello kod JavaScript próbuje warstwy środkowej toocall hello aplikacji interfejsu API, ale wywołanie hello nie powiedzie się, ponieważ fronton hello jest uruchomiony w innej domenie niż hello wstecz zakończenia.</span><span class="sxs-lookup"><span data-stu-id="eb722-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="eb722-174">okno konsoli narzędzi dla deweloperów w przeglądarce Hello zawiera komunikat o błędzie między źródłami.</span><span class="sxs-lookup"><span data-stu-id="eb722-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Komunikat o błędzie między źródłami](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="eb722-176">Konfigurowanie mechanizmu CORS dla aplikacji interfejsu API warstwy środkowej hello</span><span class="sxs-lookup"><span data-stu-id="eb722-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="eb722-177">W tej sekcji skonfigurujesz ustawienia mechanizmu CORS hello na platformie Azure dla aplikacji interfejsu API ToDoListAPI warstwy środkowej hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="eb722-178">To ustawienie umożliwia hello warstwę środkową interfejsu API aplikacji tooreceive wywołania języka JavaScript z aplikacji sieci web hello, który został utworzony dla projektu ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="eb722-179">W przeglądarce Przejdź toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb722-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eb722-180">Kliknij przycisk **usługi aplikacji**, a następnie kliknij przycisk aplikacji hello interfejsu API (warstwy środkowej) ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="eb722-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="eb722-182">W hello **ustawienia** bloku, który zostanie otwarty po prawej toohello hello **aplikacji interfejsu API** bloku, Znajdź hello **interfejsu API** sekcji, a następnie kliknij przycisk **CORS**.</span><span class="sxs-lookup"><span data-stu-id="eb722-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Wybieranie mechanizmu CORS w portalu](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="eb722-184">W polu tekstowym hello wprowadź adres URL hello aplikacji sieci web ToDoListAngular (frontonu) hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="eb722-185">Na przykład, jeśli wdrożono hello ToDoListAngular projektu tooa sieci web aplikacji o nazwie todolistangular0121, zezwala na wywołania z adresu URL hello `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="eb722-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="eb722-186">Alternatywnie można wprowadzić toospecify gwiazdki (*), że wszystkie domeny pochodzenia są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="eb722-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="eb722-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eb722-187">Click **Save**.</span></span>
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="eb722-189">Po kliknięciu **zapisać**, aplikacja hello interfejsu API będzie akceptować JavaScript wywołania z hello określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="eb722-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="eb722-190">Na tym zrzucie ekranu aplikacji interfejsu API ToDoListAPI0223 hello będzie akceptować wywołań klienta języka JavaScript z aplikacji sieci web ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="eb722-191">Testowanie aplikacji hello z włączonym mechanizmem CORS</span><span class="sxs-lookup"><span data-stu-id="eb722-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="eb722-192">Otwórz przeglądarkę toohello adres URL HTTPS aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="eb722-193">Ta aplikacja hello czasu pozwala wyświetlić, dodawanie, edytowanie i usuwanie elementów do wykonania.</span><span class="sxs-lookup"><span data-stu-id="eb722-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Strona z listą tooDo przykładowej aplikacji](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="eb722-195">Porównanie mechanizmu CORS usługi App Service i mechanizmu CORS interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="eb722-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="eb722-196">W projekcie interfejsu API sieci Web można zainstalować hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify pakietu NuGet w kodzie domen interfejsu API będzie akceptować wywołania języka JavaScript z.</span><span class="sxs-lookup"><span data-stu-id="eb722-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="eb722-197">Obsługa mechanizmu CORS interfejsu API sieci Web jest bardziej elastyczna niż obsługa mechanizmu CORS usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="eb722-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="eb722-198">Na przykład za pomocą kodu można określić różne dozwolone źródła dla różnych metod akcji, natomiast mechanizm CORS usługi App Service pozwala skonfigurować tylko jeden zestaw dozwolonych źródeł dla wszystkich metod aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="eb722-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="eb722-199">Nie próbuj toouse zarówno mechanizmu CORS interfejsu API sieci Web i mechanizmu CORS usługi App Service w jednej aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="eb722-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="eb722-200">Mechanizm CORS usługi App Service ma wyższy priorytet, co sprawia, że użycie mechanizmu CORS interfejsu API sieci Web nie odniesie żadnego skutku.</span><span class="sxs-lookup"><span data-stu-id="eb722-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="eb722-201">Na przykład jeśli jedną domenę pochodzenia w usłudze App Service, a następnie włączyć wszystkie domeny pochodzenia w kodzie interfejsu API sieci Web, aplikacja interfejsu API platformy Azure będzie akceptować tylko wywołania z domeny hello, określone na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb722-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="eb722-202">Jak tooenable CORS w kodzie interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="eb722-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="eb722-203">następujące kroki Hello podsumowanie hello procesu włączania obsługi mechanizmu CORS interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="eb722-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="eb722-204">Aby uzyskać więcej informacji, zobacz [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Włączanie żądań Cross-Origin w interfejsie API sieci Web 2 platformy ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="eb722-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="eb722-205">W projekcie interfejsu API sieci Web, należy zainstalować hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="eb722-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="eb722-206">Obejmują `config.EnableCors()` wiersza kodu w hello **zarejestrować** metody hello **WebApiConfig** klasy, jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="eb722-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
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
3. <span data-ttu-id="eb722-207">W kontrolerze interfejsu API sieci Web Dodaj `using` instrukcji dla hello `System.Web.Http.Cors` przestrzeni nazw i Dodaj hello `EnableCors` atrybutu toohello klasy lub tooindividual metody akcji kontrolera.</span><span class="sxs-lookup"><span data-stu-id="eb722-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="eb722-208">W hello poniższy przykład obsługi mechanizmu CORS dotyczy całego kontrolera toohello.</span><span class="sxs-lookup"><span data-stu-id="eb722-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="eb722-209">Używanie usługi Azure API Management z usługą API Apps</span><span class="sxs-lookup"><span data-stu-id="eb722-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="eb722-210">Jeśli używasz usługi Azure API Management z aplikacją interfejsu API, Konfigurowanie mechanizmu CORS w usłudze API Management zamiast w aplikacji interfejsu API hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="eb722-211">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="eb722-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="eb722-212">Omówienie usługi Azure API Management (klip wideo, informacje dotyczące mechanizmu CORS są prezentowane od momentu 12:10)</span><span class="sxs-lookup"><span data-stu-id="eb722-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="eb722-213">Zasady usługi API Management obejmujące różne domeny</span><span class="sxs-lookup"><span data-stu-id="eb722-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="eb722-214">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="eb722-214">Troubleshooting</span></span>
<span data-ttu-id="eb722-215">W przypadku napotkania problemów podczas pracy z tym samouczkiem skorzystaj z poniższych sugestii dotyczących ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="eb722-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="eb722-216">Upewnij się, że używasz najnowszej wersji hello hello [zestawu Azure SDK dla platformy .NET dla programu Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="eb722-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="eb722-217">Upewnij się, że wprowadzono `https` w hello ustawienia mechanizmu CORS i upewnij się, że używasz `https` toorun hello frontonu sieci web aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb722-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="eb722-218">Upewnij się, czy wprowadzono hello ustawienia mechanizmu CORS w aplikacji interfejsu API warstwy środkowej hello, a nie w aplikacji frontonu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="eb722-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="eb722-219">Jeśli konfigurujesz mechanizm CORS w kodzie aplikacji i usłudze Azure App Service, należy pamiętać, że ustawienia mechanizmu CORS usługi aplikacji hello zastąpią instrukcje zawarte w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb722-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="eb722-220">toolearn więcej informacji na temat funkcji programu Visual Studio, które ułatwiają rozwiązywanie problemów, zobacz [Rozwiązywanie problemów z usługi aplikacji Azure aplikacji w programie Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="eb722-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb722-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb722-221">Next steps</span></span>
<span data-ttu-id="eb722-222">W tym artykule przedstawiono, jak tooenable mechanizmu CORS usługi App Service obsługuje tak, że kod języka JavaScript klienta można wywołać interfejsu API w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="eb722-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="eb722-223">toolearn więcej o aplikacjach interfejsu API, przeczytaj hello [tooauthentication wprowadzenie w usłudze App Service](../app-service/app-service-authentication-overview.md), a następnie przejdź toohello [uwierzytelniania użytkowników dla aplikacji interfejsu API](app-service-api-dotnet-user-principal-auth.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="eb722-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

