---
title: "Obsługa mechanizmu CORS w usłudze App Service | Microsoft Docs"
description: "Dowiedz się, jak korzystać z obsługi mechanizmu CORS w usłudze Azure App Service."
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
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="63b47-103">Korzystanie z aplikacji interfejsu API z poziomu języka JavaScript przy użyciu mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="63b47-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="63b47-104">Usługa App Service udostępnia wbudowaną obsługę [współużytkowania zasobów między źródłami (CORS, Cross-Origin Resource Sharing)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), co pozwala klientom języka JavaScript wykonywać międzydomenowe wywołania interfejsów API hostowanych w Aplikacjach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="63b47-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="63b47-105">Usługa App Service umożliwia skonfigurowanie dostępu do interfejsu API za pomocą mechanizmu CORS bez pisania żadnego kodu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="63b47-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="63b47-106">Ten artykuł zawiera dwie sekcje:</span><span class="sxs-lookup"><span data-stu-id="63b47-106">This article contains two sections:</span></span>

* <span data-ttu-id="63b47-107">W sekcji [Konfigurowanie mechanizmu CORS](#corsconfig) ogólnie opisano konfigurowanie mechanizmu CORS w przypadku dowolnej aplikacji interfejsu API, aplikacji sieci Web lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="63b47-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="63b47-108">Te informacje dotyczą wszystkich platform obsługiwanych przez usługę App Service, w tym .NET, Node.js i Java.</span><span class="sxs-lookup"><span data-stu-id="63b47-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="63b47-109">Sekcja [Kolejne kroki samouczka ułatwiającego rozpoczęcie pracy z platformą .NET](#tutorialstart) stanowi początek samouczka demonstrującego obsługę mechanizmu CORS. Te informacje rozszerzają zagadnienia omówione w [pierwszym samouczku zawierającym wprowadzenie do usługi API Apps](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="63b47-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="63b47-110"><a id="corsconfig"></a> Konfigurowanie mechanizmu CORS w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="63b47-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="63b47-111">Mechanizm CORS można skonfigurować w witrynie Azure Portal lub za pomocą narzędzi usługi [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63b47-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="63b47-112">Konfigurowanie mechanizmu CORS w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="63b47-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="63b47-113">Otwórz witrynę [Azure Portal](https://portal.azure.com/) w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="63b47-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="63b47-114">Kliknij pozycję **App Services**, a następnie kliknij nazwę aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="63b47-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="63b47-116">W bloku **Ustawienia**, który pojawi się na prawo od bloku **Aplikacja interfejsu API**, znajdź sekcję **API**, a następnie kliknij pozycję **CORS**.</span><span class="sxs-lookup"><span data-stu-id="63b47-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Wybieranie pozycji CORS w bloku Ustawienia](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="63b47-118">W polu tekstowym wprowadź adres lub adresy URL, z których mają być dozwolone wywołania języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="63b47-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="63b47-119">Jeśli na przykład aplikację języka JavaScript wdrożono w aplikacji sieci Web o nazwie ToDoListAngular, wpisz adres „https://todolistangular.azurewebsites.net”.</span><span class="sxs-lookup"><span data-stu-id="63b47-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="63b47-120">Alternatywnie można wprowadzić gwiazdkę (*), aby określić, że wszystkie domeny pochodzenia są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="63b47-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="63b47-121">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="63b47-121">Click **Save**.</span></span>
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="63b47-123">Po kliknięciu pozycji **Zapisz** aplikacja interfejsu API będzie akceptować wywołania języka JavaScript pochodzące z określonych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="63b47-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="63b47-124">Konfigurowanie mechanizmu CORS za pomocą narzędzi usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63b47-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="63b47-125">Mechanizm CORS dla aplikacji interfejsu API można również skonfigurować za pomocą [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) i narzędzi wiersza polecenia, takich jak [program Azure PowerShell](/powershell/azureps-cmdlets-docs) i [interfejs wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="63b47-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="63b47-126">Aby zobaczyć przykładowy szablon usługi Azure Resource Manager, który umożliwia ustawienie właściwości CORS, otwórz [plik azuredeploy.json znajdujący się w repozytorium przykładowej aplikacji opisanej w tym samouczku ](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="63b47-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="63b47-127">Znajdź sekcję szablonu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="63b47-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="63b47-128"><a id="tutorialstart"></a> Kolejne kroki samouczka ułatwiającego rozpoczęcie pracy z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="63b47-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="63b47-129">Jeśli korzystasz z serii szkoleń wprowadzających do Aplikacji interfejsu API dotyczących platform Node.js lub Java, to w tym momencie kończysz tę serię.</span><span class="sxs-lookup"><span data-stu-id="63b47-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="63b47-130">Sekcja [Następne kroki](#next-steps) zawiera propozycje materiałów, które umożliwiają kontynuowanie poznawania usługi API Apps.</span><span class="sxs-lookup"><span data-stu-id="63b47-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="63b47-131">W dalszej części tego artykułu, która stanowi kontynuację serii wprowadzającej do platformy .NET, założono, że udało Ci się ukończyć [pierwszy samouczek](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="63b47-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="63b47-132">Wdrażanie projektu ToDoListAngular w nowej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="63b47-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="63b47-133">W [pierwszym samouczku](app-service-api-dotnet-get-started.md) utworzono aplikacje interfejsu API warstwy środkowej i warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="63b47-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="63b47-134">Bieżący samouczek obejmuje utworzenie jednostronicowej aplikacji sieci Web, która wywołuje aplikację interfejsu API warstwy środkowej.</span><span class="sxs-lookup"><span data-stu-id="63b47-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="63b47-135">Aby aplikacja jednostronicowa działała, musisz włączyć mechanizm CORS w aplikacji interfejsu API warstwy środkowej.</span><span class="sxs-lookup"><span data-stu-id="63b47-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="63b47-136">[Przykładowa aplikacja ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) zawiera projekt ToDoListAngular, który jest prostym klientem AngularJS wywołującym projekt interfejsu API sieci Web warstwy środkowej ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="63b47-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="63b47-137">Kod języka JavaScript zawarty w pliku *app/scripts/todoListSvc.js* wywołuje funkcje interfejsu API przy użyciu dostawcy usługi HTTP AngularJS.</span><span class="sxs-lookup"><span data-stu-id="63b47-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="63b47-138">Tworzenie nowej aplikacji sieci Web dla projektu ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="63b47-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="63b47-139">Procedura obejmująca tworzenie nowej aplikacji sieci Web usługi App Service i wdrażanie w niej projektu jest podobna do instrukcji dotyczących [tworzenia i wdrażania aplikacji interfejsu API zawartych w pierwszym samouczku tej serii](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="63b47-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="63b47-140">Jedyna różnica polega na tym, że typ aplikacji to **aplikacja sieci Web**, a nie **aplikacja interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="63b47-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="63b47-141">Aby zapoznać się ze zrzutami ekranu okien dialogowych, zobacz</span><span class="sxs-lookup"><span data-stu-id="63b47-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="63b47-142">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy projekt ToDoListAngular, a następnie kliknij polecenie **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="63b47-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="63b47-143">Na karcie **Profil** kreatora **Publikowanie w sieci Web** kliknij pozycję **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="63b47-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="63b47-144">W oknie dialogowym **App Service** kliknij pozycję **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="63b47-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="63b47-145">Na karcie **Hosting** okna dialogowego **Tworzenie usługi App Service** wpisz **nazwę aplikacji sieci Web** unikatową w domenie *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="63b47-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="63b47-146">Wybierz **subskrypcję** platformy Azure, której chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="63b47-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="63b47-147">Z listy rozwijanej **Grupa zasobów** wybierz wcześniej utworzoną grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="63b47-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="63b47-148">Z listy rozwijanej **Plan usługi App Service** wybierz wcześniej utworzony plan.</span><span class="sxs-lookup"><span data-stu-id="63b47-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="63b47-149">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="63b47-149">Click **Create**.</span></span>
   
    <span data-ttu-id="63b47-150">Program Visual Studio utworzy aplikację sieci Web wraz z odpowiednim profilem publikowania i przejdzie do kroku **Połączenie** kreatora **Publikowanie w sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="63b47-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="63b47-151">W tym momencie nie klikaj pozycji **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="63b47-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="63b47-152">W następnej sekcji zostanie skonfigurowana nowa aplikacja sieci Web wywołująca aplikację interfejsu API warstwy środkowej, w której działa usługa App Service.</span><span class="sxs-lookup"><span data-stu-id="63b47-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="63b47-153">Konfigurowanie adresu URL warstwy środkowej w ustawieniach aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="63b47-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="63b47-154">Otwórz witrynę [Azure Portal](https://portal.azure.com/) i przejdź do bloku **Aplikacja sieci Web** dla aplikacji sieci Web utworzonej w celu hostowania projektu TodoListAngular (frontonu).</span><span class="sxs-lookup"><span data-stu-id="63b47-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="63b47-155">Kliknij kolejno pozycje **Ustawienia > Ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="63b47-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="63b47-156">W sekcji **Ustawienia aplikacji** dodaj następujący klucz i wartość:</span><span class="sxs-lookup"><span data-stu-id="63b47-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="63b47-157">Klucz</span><span class="sxs-lookup"><span data-stu-id="63b47-157">Key</span></span> | <span data-ttu-id="63b47-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="63b47-158">Value</span></span> | <span data-ttu-id="63b47-159">Przykład</span><span class="sxs-lookup"><span data-stu-id="63b47-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="63b47-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="63b47-160">toDoListAPIURL</span></span> |<span data-ttu-id="63b47-161">https://{nazwa aplikacji interfejsu API warstwy środkowej}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="63b47-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="63b47-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="63b47-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="63b47-163">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="63b47-163">Click **Save**.</span></span>
   
    <span data-ttu-id="63b47-164">Gdy kod działa na platformie Azure, ta wartość zastępuje adres URL localhost, który został określony w pliku *Web.config*.</span><span class="sxs-lookup"><span data-stu-id="63b47-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="63b47-165">Kod, który służy do pobierania wartości ustawienia, znajduje się w pliku *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="63b47-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="63b47-166">Kod w pliku *todoListSvc.js* używa tego ustawienia:</span><span class="sxs-lookup"><span data-stu-id="63b47-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
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

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="63b47-167">Wdrażanie projektu sieci Web ToDoListAngular w nowej aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="63b47-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="63b47-168">W programie Visual Studio w kroku **Połączenie** kreatora **Publikowanie w sieci Web** kliknij pozycję **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="63b47-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="63b47-169">Program Visual Studio wdroży projekt ToDoListAngular w nowej aplikacji sieci Web i otworzy w przeglądarce adres URL aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b47-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="63b47-170">Testowanie aplikacji bez włączonego mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="63b47-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="63b47-171">W obszarze narzędzi dla deweloperów w przeglądarce otwórz okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="63b47-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="63b47-172">W oknie przeglądarki, w którym zostanie wyświetlony interfejs użytkownika klienta AngularJS, kliknij link **listy zadań do wykonania**.</span><span class="sxs-lookup"><span data-stu-id="63b47-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="63b47-173">Próba wywołania aplikacji interfejsu API warstwy środkowej przez kod języka JavaScript kończy się niepowodzeniem, ponieważ fronton jest uruchomiony w innej domenie niż wewnętrzna baza danych.</span><span class="sxs-lookup"><span data-stu-id="63b47-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="63b47-174">W oknie konsoli narzędzi dla deweloperów w przeglądarce pojawi się komunikat o błędzie między źródłami.</span><span class="sxs-lookup"><span data-stu-id="63b47-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Komunikat o błędzie między źródłami](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="63b47-176">Konfigurowanie mechanizmu CORS dla aplikacji interfejsu API warstwy środkowej</span><span class="sxs-lookup"><span data-stu-id="63b47-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="63b47-177">Ta sekcja dotyczy konfiguracji ustawienia mechanizmu CORS na platformie Azure na potrzeby aplikacji interfejsu API warstwy środkowej ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="63b47-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="63b47-178">To ustawienie umożliwia aplikacji interfejsu API warstwy środkowej odbieranie wywołań języka JavaScript z aplikacji sieci Web utworzonej dla projektu ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="63b47-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="63b47-179">Otwórz [portal Azure](https://portal.azure.com/) w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="63b47-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="63b47-180">Kliknij pozycję **App Services**, a następnie kliknij aplikację interfejsu API (warstwy środkowej) ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="63b47-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Wybieranie aplikacji interfejsu API w portalu](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="63b47-182">W bloku **Ustawienia**, który pojawi się na prawo od bloku **Aplikacja interfejsu API**, znajdź sekcję **API**, a następnie kliknij pozycję **CORS**.</span><span class="sxs-lookup"><span data-stu-id="63b47-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Wybieranie mechanizmu CORS w portalu](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="63b47-184">W polu tekstowym wpisz adres URL aplikacji sieci Web ToDoListAngular (frontonu).</span><span class="sxs-lookup"><span data-stu-id="63b47-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="63b47-185">Jeśli na przykład projekt ToDoListAngular wdrożono w aplikacji sieci Web o nazwie todolistangular0121, musisz zezwolić na wywołania pochodzące z adresu URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="63b47-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="63b47-186">Alternatywnie można wprowadzić gwiazdkę (*), aby określić, że wszystkie domeny pochodzenia są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="63b47-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="63b47-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="63b47-187">Click **Save**.</span></span>
   
   ![Klikanie pozycji Zapisz.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="63b47-189">Po kliknięciu pozycji **Zapisz** aplikacja interfejsu API będzie akceptować wywołania języka JavaScript pochodzące z określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="63b47-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="63b47-190">Na tym zrzucie ekranu widać, że skonfigurowano akceptowanie wywołań klienta języka JavaScript pochodzących z aplikacji sieci Web ToDoListAngular przez aplikację interfejsu API ToDoListAPI0223.</span><span class="sxs-lookup"><span data-stu-id="63b47-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="63b47-191">Testowanie aplikacji z włączonym mechanizmem CORS</span><span class="sxs-lookup"><span data-stu-id="63b47-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="63b47-192">Otwórz w przeglądarce adres URL HTTPS aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b47-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="63b47-193">W tej konfiguracji aplikacja pozwala wyświetlać, dodawać, edytować i usuwać elementy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="63b47-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Strona z listą zadań do wykonania w przykładowej aplikacji](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="63b47-195">Porównanie mechanizmu CORS usługi App Service i mechanizmu CORS interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="63b47-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="63b47-196">W projekcie interfejsu API sieci Web można zainstalować pakiet NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/), aby móc za pomocą kodu określać domeny, z których mogą pochodzić wywołania języka JavaScript akceptowane przez interfejs API.</span><span class="sxs-lookup"><span data-stu-id="63b47-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="63b47-197">Obsługa mechanizmu CORS interfejsu API sieci Web jest bardziej elastyczna niż obsługa mechanizmu CORS usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="63b47-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="63b47-198">Na przykład za pomocą kodu można określić różne dozwolone źródła dla różnych metod akcji, natomiast mechanizm CORS usługi App Service pozwala skonfigurować tylko jeden zestaw dozwolonych źródeł dla wszystkich metod aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="63b47-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="63b47-199">W jednej aplikacji interfejsu API nie należy jednocześnie używać mechanizmu CORS interfejsu API sieci Web i mechanizmu CORS usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="63b47-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="63b47-200">Mechanizm CORS usługi App Service ma wyższy priorytet, co sprawia, że użycie mechanizmu CORS interfejsu API sieci Web nie odniesie żadnego skutku.</span><span class="sxs-lookup"><span data-stu-id="63b47-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="63b47-201">Jeśli na przykład w kodzie interfejsu API sieci Web włączysz wszystkie domeny pochodzenia, ale tylko jedną domenę pochodzenia w usłudze App Service, to aplikacja interfejsu API platformy Azure będzie akceptować tylko wywołania z domeny określonej w ustawieniach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b47-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="63b47-202">Włączanie mechanizmu CORS w kodzie interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="63b47-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="63b47-203">Poniższe instrukcje stanowią podsumowanie procesu włączania obsługi mechanizmu CORS interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b47-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="63b47-204">Aby uzyskać więcej informacji, zobacz [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Włączanie żądań Cross-Origin w interfejsie API sieci Web 2 platformy ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="63b47-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="63b47-205">W projekcie interfejsu API sieci Web zainstaluj pakiet NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/).</span><span class="sxs-lookup"><span data-stu-id="63b47-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="63b47-206">Dodaj wiersz `config.EnableCors()` w kodzie metody **Register** klasy **WebApiConfig**, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="63b47-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
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
3. <span data-ttu-id="63b47-207">W kontrolerze interfejsu API sieci Web dodaj instrukcję `using` dla przestrzeni nazw `System.Web.Http.Cors` i dodaj atrybut `EnableCors` do klasy kontrolera lub poszczególnych metod akcji.</span><span class="sxs-lookup"><span data-stu-id="63b47-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="63b47-208">W poniższym przykładzie obsługa mechanizmu CORS dotyczy całego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="63b47-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="63b47-209">Używanie usługi Azure API Management z usługą API Apps</span><span class="sxs-lookup"><span data-stu-id="63b47-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="63b47-210">Jeśli używasz usługi Azure API Management razem z aplikacją interfejsu API, skonfiguruj mechanizm CORS w usłudze API Management zamiast w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="63b47-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="63b47-211">Więcej informacji zawierają następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="63b47-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="63b47-212">Omówienie usługi Azure API Management (klip wideo, informacje dotyczące mechanizmu CORS są prezentowane od momentu 12:10)</span><span class="sxs-lookup"><span data-stu-id="63b47-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="63b47-213">Zasady usługi API Management obejmujące różne domeny</span><span class="sxs-lookup"><span data-stu-id="63b47-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="63b47-214">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="63b47-214">Troubleshooting</span></span>
<span data-ttu-id="63b47-215">W przypadku napotkania problemów podczas pracy z tym samouczkiem skorzystaj z poniższych sugestii dotyczących ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="63b47-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="63b47-216">Upewnij się, że używasz najnowszej wersji [zestawu Azure SDK dla platformy .NET dla programu Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="63b47-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="63b47-217">Upewnij się, że wprowadzono adres `https` w ustawieniach mechanizmu CORS i sprawdź, czy adres `https` jest używany do uruchomienia aplikacji frontonu sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b47-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="63b47-218">Upewnij się, że ustawienia mechanizmu CORS skonfigurowano w aplikacji interfejsu API warstwy środkowej, a nie w aplikacji frontonu sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b47-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="63b47-219">Jeśli konfigurujesz mechanizm CORS zarówno w kodzie aplikacji, jak i usłudze Azure App Service, pamiętaj o tym, że ustawienia mechanizmu CORS Usługi aplikacji zastąpią instrukcje zawarte w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="63b47-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="63b47-220">Aby dowiedzieć się więcej o funkcjach programu Visual Studio, które ułatwiają rozwiązywanie problemów, zobacz [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (Rozwiązywanie problemów z aplikacjami usługi Azure App Service w programie Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="63b47-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63b47-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63b47-221">Next steps</span></span>
<span data-ttu-id="63b47-222">W tym artykule pokazano, jak włączyć obsługę mechanizmu CORS usługi App Service w celu umożliwienia wywołania funkcji API z innej domeny przez kod języka JavaScript klienta.</span><span class="sxs-lookup"><span data-stu-id="63b47-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="63b47-223">Aby dowiedzieć się więcej o aplikacjach interfejsu API, zapoznaj się z [wprowadzeniem do uwierzytelniania w usłudze App Service](../app-service/app-service-authentication-overview.md), a następnie przejdź do samouczka dotyczącego [uwierzytelniania użytkowników w Aplikacjach interfejsu API](app-service-api-dotnet-user-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="63b47-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

