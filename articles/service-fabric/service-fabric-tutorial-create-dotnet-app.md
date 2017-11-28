---
title: "aaaCreate aplikacji .NET dla usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikacji przy użyciu platformy ASP.NET Core frontonu i niezawodne usługi stanowej zaplecza i wdrożenie klastra tooa aplikacji hello."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="76deb-103">Tworzenie i wdrażanie aplikacji przy użyciu interfejsu API platformy ASP.NET Core sieci Web usługi frontonu i usługi stanowej zaplecza</span><span class="sxs-lookup"><span data-stu-id="76deb-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="76deb-104">W tym samouczku wchodzi w jednej serii.</span><span class="sxs-lookup"><span data-stu-id="76deb-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="76deb-105">Dowiesz się jak toocreate aplikacji sieci szkieletowej usług Azure z przodu interfejsu API platformy ASP.NET Core sieci Web zakończenie i toostore usługi stanowej zaplecza danych.</span><span class="sxs-lookup"><span data-stu-id="76deb-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="76deb-106">Po zakończeniu, masz aplikację do głosowania z frontonu, który zapisuje wyniki głosowania stanowe usługi zaplecza w klastrze hello sieci web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="76deb-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="76deb-107">Jeśli nie chcesz toomanually utworzyć hello głosowania aplikacji, możesz [pobrać kodu źródłowego hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) dla hello ukończone aplikacji i przejść od razu zbyt[Przewodnik po głosowanie w przykładowej aplikacji hello](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="76deb-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="76deb-109">W części jednej serii hello, możesz dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="76deb-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76deb-110">Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej</span><span class="sxs-lookup"><span data-stu-id="76deb-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="76deb-111">Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych</span><span class="sxs-lookup"><span data-stu-id="76deb-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="76deb-112">Witaj toocommunicate zwrotnego serwera proxy za pomocą usługi stanowej hello</span><span class="sxs-lookup"><span data-stu-id="76deb-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="76deb-113">W tym samouczku dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="76deb-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="76deb-114">Tworzenie aplikacji sieci szkieletowej usług .NET</span><span class="sxs-lookup"><span data-stu-id="76deb-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="76deb-115">Wdrażanie klastra zdalnego tooa aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="76deb-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="76deb-116">Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="76deb-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="76deb-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="76deb-117">Prerequisites</span></span>
<span data-ttu-id="76deb-118">Przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="76deb-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="76deb-119">Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="76deb-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="76deb-120">[Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) i zainstaluj hello **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.</span><span class="sxs-lookup"><span data-stu-id="76deb-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="76deb-121">Zainstaluj hello zestawu SDK sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="76deb-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="76deb-122">Tworzenie usługi dla składnika ASP.NET Web API jako niezawodnej usługi</span><span class="sxs-lookup"><span data-stu-id="76deb-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="76deb-123">Najpierw utwórz hello sieci web frontonu z hello głosowania aplikacji przy użyciu platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="76deb-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="76deb-124">Platformy ASP.NET Core to platforma programistyczna lekka międzyplatformowa sieci web można używać nowoczesnych toocreate interfejsu użytkownika sieci web i interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="76deb-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="76deb-125">tooget pełną wiedzę na temat sposobu platformy ASP.NET Core integruje się z sieci szkieletowej usług, zalecamy przeczytanie za pośrednictwem hello [platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="76deb-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="76deb-126">Teraz można wykonać tego samouczka tooget szybko rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="76deb-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="76deb-127">toolearn więcej informacji na temat platformy ASP.NET Core, zobacz hello [platformy ASP.NET Core dokumentacji](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="76deb-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="76deb-128">W tym samouczku jest oparta na powitania [platformy ASP.NET Core narzędzi dla programu Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="76deb-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="76deb-129">już trwa aktualizowanie Hello .NET Core tools dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="76deb-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="76deb-130">Uruchom program Visual Studio jako **administrator**.</span><span class="sxs-lookup"><span data-stu-id="76deb-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="76deb-131">Tworzenie projektu z **pliku**->**nowy**->**projektu**</span><span class="sxs-lookup"><span data-stu-id="76deb-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="76deb-132">W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="76deb-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="76deb-133">Nadaj nazwę aplikacji hello **głosowania** i naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="76deb-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Okno dialogowe nowego projektu w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="76deb-135">Na powitania **Nowa usługa sieci szkieletowej usług** wybierz pozycję **bezstanowych platformy ASP.NET Core**i nadaj nazwę usługi **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="76deb-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Wybieranie usługi sieci web ASP.NET w oknie dialogowym hello nowej usługi](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="76deb-137">Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu.</span><span class="sxs-lookup"><span data-stu-id="76deb-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="76deb-138">W tym samouczku, wybierz **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="76deb-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="76deb-140">Visual Studio tworzy aplikację oraz projekt usługi i wyświetla je w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="76deb-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Eksplorator rozwiązań po utworzeniu aplikacji z platformy ASP.NET core usługi interfejsu API sieci Web]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="76deb-142">Dodaj usługę VotingWeb toohello AngularJS</span><span class="sxs-lookup"><span data-stu-id="76deb-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="76deb-143">Dodaj [AngularJS](http://angularjs.org/) tooyour usługi przy użyciu wbudowanych hello [Bower Obsługa](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="76deb-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="76deb-144">Otwórz *bower.json* i Dodaj pozycje kątowego i kąta początkowego, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="76deb-145">Podczas zapisywania hello *bower.json* Twojego projektu zainstalowano plik, kątową *wwwroot/lib* folderu.</span><span class="sxs-lookup"><span data-stu-id="76deb-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="76deb-146">Ponadto ta opcja jest wyświetlana w ramach hello *zależności/Bower* folderu.</span><span class="sxs-lookup"><span data-stu-id="76deb-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="76deb-147">Plik site.js hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="76deb-147">Update hello site.js file</span></span>
<span data-ttu-id="76deb-148">Otwórz hello *wwwroot/js/site.js* pliku.</span><span class="sxs-lookup"><span data-stu-id="76deb-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="76deb-149">Zastąp jego zawartość hello JavaScript używane przez widoki głównej hello:</span><span class="sxs-lookup"><span data-stu-id="76deb-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="76deb-150">Plik Index.cshtml hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="76deb-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="76deb-151">Otwórz hello *Views/Home/Index.cshtml* plik, określonym kontrolerem głównej toohello hello widoku.</span><span class="sxs-lookup"><span data-stu-id="76deb-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="76deb-152">Zastąp jego zawartość następujących hello, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-152">Replace its contents with hello following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="76deb-153">Plik _Layout.cshtml hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="76deb-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="76deb-154">Otwórz hello *Views/Shared/_Layout.cshtml* plik, układ domyślny hello hello aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="76deb-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="76deb-155">Zastąp jego zawartość następujących hello, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-155">Replace its contents with hello following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="76deb-156">Plik VotingWeb.cs hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="76deb-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="76deb-157">Otwórz hello *VotingWeb.cs* pliku, który tworzy hello hosta sieci Web platformy ASP.NET Core wewnątrz usługi bezstanowej hello przy użyciu serwera sieci web WebListener hello.</span><span class="sxs-lookup"><span data-stu-id="76deb-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="76deb-158">Dodaj hello `using System.Net.Http;` początku dyrektywy toohello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="76deb-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="76deb-159">Zastąp hello `CreateServiceInstanceListeners()` działać z hello poniżej, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="76deb-160">Dodaj plik VotesController.cs hello</span><span class="sxs-lookup"><span data-stu-id="76deb-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="76deb-161">Dodaj kontroler, który definiuje akcje głosu.</span><span class="sxs-lookup"><span data-stu-id="76deb-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="76deb-162">Kliknij prawym przyciskiem myszy na powitania **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**.</span><span class="sxs-lookup"><span data-stu-id="76deb-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="76deb-163">Nadaj nazwę plikowi hello "VotesController.cs", a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="76deb-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="76deb-164">Zastąp zawartość pliku hello hello poniżej, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="76deb-165">W dalszej [pliku VotesController.cs hello aktualizacji](#updatevotecontroller_anchor), ten plik zostanie zmodyfikowane tooread i zapisywania danych głosowania z hello usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="76deb-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="76deb-166">Obecnie kontrolera hello zwraca ciąg statycznych danych toohello widoku.</span><span class="sxs-lookup"><span data-stu-id="76deb-166">For now, hello controller returns static string data toohello view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="76deb-167">Wdrażanie i uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="76deb-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="76deb-168">Możesz teraz Przejdź dalej i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="76deb-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="76deb-169">W programie Visual Studio, naciśnij klawisz `F5` toodeploy hello aplikację do debugowania.</span><span class="sxs-lookup"><span data-stu-id="76deb-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="76deb-170">`F5`kończy się niepowodzeniem, jeśli wcześniej nie został otwarty program Visual Studio jako **administratora**.</span><span class="sxs-lookup"><span data-stu-id="76deb-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="76deb-171">Witaj pierwszego uruchomienia i wdrażanie aplikacji hello lokalnie, Visual Studio tworzy lokalny klaster na potrzeby debugowania.</span><span class="sxs-lookup"><span data-stu-id="76deb-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="76deb-172">Tworzenie klastra może zająć trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="76deb-172">Cluster creation may take some time.</span></span> <span data-ttu-id="76deb-173">Stan tworzenia klastra Hello jest wyświetlany w oknie danych wyjściowych programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="76deb-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="76deb-174">W tym momencie aplikacji sieci web powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="76deb-174">At this point, your web app should look like this:</span></span>

![Platformy ASP.NET Core frontonu](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="76deb-176">debugowanie aplikacji hello toostop wrócić do poprzedniej strony tooVisual Studio i naciśnij klawisz **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="76deb-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="76deb-177">Dodaj aplikację tooyour usługi stanowej zaplecza</span><span class="sxs-lookup"><span data-stu-id="76deb-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="76deb-178">Teraz, gdy mamy Usługa interfejsu API sieci Web platformy ASP.NET w naszej aplikacji jest uruchomiona, spróbuj teraz i Dodaj toostore niezawodnej usługi stanowej niektóre dane w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76deb-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="76deb-179">Sieć szkieletowa usług pozwala tooconsistently i niezawodne przechowywanie dane bezpośrednio w usłudze przy użyciu niezawodnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="76deb-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="76deb-180">Niezawodne kolekcje są zestaw klas wysokiej dostępności i niezawodne kolekcji, które są znane tooanyone, który został użyty kolekcje C#.</span><span class="sxs-lookup"><span data-stu-id="76deb-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="76deb-181">W tym samouczku utworzysz usługę, która przechowuje wartość licznika w niezawodnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="76deb-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="76deb-182">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **usług** poziomu projekt aplikacji hello i wybierz polecenie **Dodaj > Nowa usługa sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="76deb-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Dodawanie nowej usługi tooan istniejącej aplikacji](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="76deb-184">W hello **Nowa usługa sieci szkieletowej usług** okno dialogowe, wybierz **Stateful platformy ASP.NET Core**i usługa hello nazw **VotingData** i naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="76deb-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Okno dialogowe nowej usługi w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="76deb-186">Po utworzeniu projektu usługi dostępne są dwie usługi w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76deb-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="76deb-187">Kontynuując toobuild aplikacji, można dodać więcej usług w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="76deb-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="76deb-188">Każdy może być niezależnie określonej wersji, jak i uaktualnionych.</span><span class="sxs-lookup"><span data-stu-id="76deb-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="76deb-189">Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu.</span><span class="sxs-lookup"><span data-stu-id="76deb-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="76deb-190">W tym samouczku, wybierz **interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="76deb-190">For this tutorial, choose **Web API**.</span></span>

    ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="76deb-192">Visual Studio tworzy projekt usługi i wyświetla je w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="76deb-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Eksplorator rozwiązań](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="76deb-194">Dodaj plik VoteDataController.cs hello</span><span class="sxs-lookup"><span data-stu-id="76deb-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="76deb-195">W hello **VotingData** kliknij prawym przyciskiem myszy projekt na powitania **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**.</span><span class="sxs-lookup"><span data-stu-id="76deb-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="76deb-196">Nadaj nazwę plikowi hello "VoteDataController.cs", a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="76deb-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="76deb-197">Zastąp zawartość pliku hello hello poniżej, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-197">Replace hello file contents with hello following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a><span data-ttu-id="76deb-198">Połączenie usług hello</span><span class="sxs-lookup"><span data-stu-id="76deb-198">Connect hello services</span></span>
<span data-ttu-id="76deb-199">W następnym kroku firma Microsoft będzie połączyć z hello dwóch usług i wprowadzić hello frontonu sieci Web aplikacji elementu get i set głosowania informacji z usługi zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="76deb-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="76deb-200">Sieć szkieletowa usług oferuje pełną elastyczność w sposób komunikowania się z usługami reliable services.</span><span class="sxs-lookup"><span data-stu-id="76deb-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="76deb-201">Wewnątrz aplikacji konieczne może być usług, które są dostępne za pośrednictwem protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="76deb-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="76deb-202">Inne usługi, które mogą być dostępne za pośrednictwem interfejsu API REST protokołu HTTP i innych usług może być dostępny za pośrednictwem gniazda sieci web.</span><span class="sxs-lookup"><span data-stu-id="76deb-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="76deb-203">W tle na dostępne opcje hello oraz kompromisy hello zaangażowany, zobacz [komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="76deb-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="76deb-204">W tym samouczku używamy [Web API platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="76deb-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="76deb-205">Plik VotesController.cs hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="76deb-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="76deb-206">W hello **VotingWeb** projektu, otwórz hello *Controllers/VotesController.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="76deb-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="76deb-207">Zastąp hello `VotesController` zawartość definicji hello następujące klasy, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="76deb-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="76deb-208">Przewodnik po głosowanie w przykładowej aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="76deb-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="76deb-209">głosowania aplikacji Hello składa się z dwóch usług:</span><span class="sxs-lookup"><span data-stu-id="76deb-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="76deb-210">Usługa frontonu (VotingWeb) sieci Web — platformy ASP.NET Core usługi frontonu, która służy hello strony sieci web i ujawnia sieci web API toocommunicate hello usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="76deb-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="76deb-211">Usługi zaplecza (VotingData) — usługi sieci web platformy ASP.NET Core, która ujawnia interfejsu API toostore hello głos powoduje niezawodnej słownika utrwalony na dysku.</span><span class="sxs-lookup"><span data-stu-id="76deb-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="76deb-213">Po głosowanie w hello aplikacji hello następującego wystąpienia zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="76deb-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="76deb-214">JavaScript wysyła hello głos żądanie toohello interfejsu API sieci web usługi frontonu sieci web hello jako żądanie HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="76deb-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="76deb-215">Usługa frontonu sieci web Hello używa toolocate serwera proxy i przesyła usługi zaplecza HTTP PUT toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="76deb-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="76deb-216">usługi zaplecza Hello przyjmuje hello żądania przychodzącego, a hello magazynów zaktualizowany wynik w niezawodnej słownik, który pobiera replikowanych toomultiple węzłów w klastrze hello i utrwalony na dysku.</span><span class="sxs-lookup"><span data-stu-id="76deb-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="76deb-217">Dane wszystkich aplikacji hello są przechowywane w klastrze hello, więc nie bazy danych nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="76deb-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="76deb-218">Debugowanie w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="76deb-218">Debug in Visual Studio</span></span>
<span data-ttu-id="76deb-219">Podczas debugowania aplikacji w programie Visual Studio, czy używasz klastra lokalnego Projektowanie sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="76deb-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="76deb-220">Masz hello tooadjust opcji debugowania scenariusz tooyour środowisko.</span><span class="sxs-lookup"><span data-stu-id="76deb-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="76deb-221">W tej aplikacji są przechowywane dane w naszej usługi zaplecza przy użyciu niezawodnych słownika.</span><span class="sxs-lookup"><span data-stu-id="76deb-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="76deb-222">Po zatrzymaniu debugera hello programu Visual Studio spowoduje usunięcie aplikacji hello na domyślne.</span><span class="sxs-lookup"><span data-stu-id="76deb-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="76deb-223">Usunięcie aplikacji hello powoduje hello danych w wewnętrznej hello tooalso usługi można usunąć.</span><span class="sxs-lookup"><span data-stu-id="76deb-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="76deb-224">toopersist hello danych między sesji debugowania, możesz zmienić hello **tryb debugowania aplikacji** jako właściwość hello **głosowania** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76deb-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="76deb-225">toolook na co się stanie w kodzie hello, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="76deb-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="76deb-226">Otwórz hello **VotesController.cs** pliku i ustaw punkt przerwania w składniku web API hello **Put** — metoda (linii 47) — możesz wyszukać plik hello w hello Eksploratora rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76deb-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="76deb-227">Otwórz hello **VoteDataController.cs** pliku i ustaw punkt przerwania w tym składnika web API **Put** — metoda (wiersz 50).</span><span class="sxs-lookup"><span data-stu-id="76deb-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="76deb-228">Przejść toohello przeglądarki i kliknij opcję głosu lub dodać nową opcję głosu.</span><span class="sxs-lookup"><span data-stu-id="76deb-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="76deb-229">Naciśniesz hello pierwszy punkt przerwania hello web przodu end w kontrolerze interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="76deb-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="76deb-230">Jest to, gdzie hello JavaScript w przeglądarce hello wysyła kontrolera interfejsu API sieci web toohello żądania w hello usługi frontonu.</span><span class="sxs-lookup"><span data-stu-id="76deb-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Dodawanie usługi frontonu głosu](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="76deb-232">Najpierw możemy utworzyć hello adresu URL toohello ReverseProxy dla naszej usługi zaplecza **(1)**.</span><span class="sxs-lookup"><span data-stu-id="76deb-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="76deb-233">Następnie możemy wysłać hello HTTP PUT żądanie toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="76deb-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="76deb-234">Na koniec hello zostanie zwrócona odpowiedź hello z klienta toohello usługi zaplecza hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="76deb-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="76deb-235">Naciśnij klawisz **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="76deb-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="76deb-236">Jesteś teraz w punkcie przerwania hello hello usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="76deb-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Dodawania usługi zaplecza głosu](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="76deb-238">W hello pierwszego wiersza w metodzie hello **(1)** używamy hello `StateManager` tooget lub dodać słownika niezawodnej o nazwie `counts`.</span><span class="sxs-lookup"><span data-stu-id="76deb-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="76deb-239">Wszystkie interakcje z wartości w słowniku niezawodnej wymagają transakcji, za pomocą tej instrukcji **(2)** tworzy tej transakcji.</span><span class="sxs-lookup"><span data-stu-id="76deb-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="76deb-240">W transakcji hello modyfikacjom następnie hello wartość hello odpowiedniego klucza hello głosowania opcji i zatwierdzeń hello operacji **(3)**.</span><span class="sxs-lookup"><span data-stu-id="76deb-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="76deb-241">Po zatwierdzić hello metoda zwróci wartość, hello danych jest aktualizowany w słowniku hello i replikowane tooother węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="76deb-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="76deb-242">dane Hello teraz są bezpiecznie przechowywane w hello klastra, a usługi zaplecza hello może przełączyć się węzłów tooother zachowaniu hello dostępnych danych.</span><span class="sxs-lookup"><span data-stu-id="76deb-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="76deb-243">Naciśnij klawisz **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="76deb-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="76deb-244">hello toostop sesję, naciśnij klawisz debugowania **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="76deb-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="76deb-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76deb-245">Next steps</span></span>
<span data-ttu-id="76deb-246">W tej części samouczka hello przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="76deb-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76deb-247">Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej</span><span class="sxs-lookup"><span data-stu-id="76deb-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="76deb-248">Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych</span><span class="sxs-lookup"><span data-stu-id="76deb-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="76deb-249">Witaj toocommunicate zwrotnego serwera proxy za pomocą usługi stanowej hello</span><span class="sxs-lookup"><span data-stu-id="76deb-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="76deb-250">Następny samouczek toohello wyprzedzeniem:</span><span class="sxs-lookup"><span data-stu-id="76deb-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="76deb-251">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="76deb-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
