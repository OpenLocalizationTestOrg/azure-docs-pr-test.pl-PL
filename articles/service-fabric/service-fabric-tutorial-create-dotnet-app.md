---
title: "Tworzenie aplikacji .NET dla usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia aplikacji platformy ASP.NET Core frontonu i niezawodnej usługi stanowej zaplecza i wdrażanie aplikacji do klastra."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/17/2018
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: f4b3c766ee46233cd4ec2d195e39d0b68516952f
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Tworzenie i wdrażanie aplikacji przy użyciu interfejsu API platformy ASP.NET Core sieci Web usługi frontonu i usługi stanowej zaplecza
W tym samouczku wchodzi w jednej serii.  Zostanie sposób tworzenia aplikacji sieci szkieletowej usług Azure z interfejsu API platformy ASP.NET Core sieci Web frontonu i stanowe usługi zaplecza do przechowywania danych. Po zakończeniu będziesz mieć aplikację do głosowania z usługą internetową frontonu ASP.NET Core, która zapisuje wyniki głosowania w stanowej usłudze zaplecza w klastrze. Jeśli nie chcesz ręcznie utworzyć aplikację do głosowania, możesz [pobrać kodu źródłowego](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) dla ukończona aplikacja i przejść od razu do [przeprowadzenie głosowania przykładowej aplikacji](#walkthrough_anchor).

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

W części jednej serii, możesz dowiedzieć się, jak:

> [!div class="checklist"]
> * Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej
> * Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych
> * Użyć zwrotnego serwera proxy do komunikacji z usługą stanową

W tym samouczku dowiesz się, jak:
> [!div class="checklist"]
> * Tworzenie aplikacji sieci szkieletowej usług .NET
> * [Wdrażanie aplikacji do zdalnego klastra](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)
> * [Konfigurowanie monitorowania i diagnostyki dla aplikacji](service-fabric-tutorial-monitoring-aspnet.md)

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka:
- Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) wersji 15.3 lub nowszym z **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.
- [Zainstaluj zestaw SDK sieci szkieletowej usług](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Tworzenie usługi dla składnika ASP.NET Web API jako niezawodnej usługi
Najpierw utwórz głosowania aplikacji za pomocą platformy ASP.NET Core frontonu sieci web. Platformy ASP.NET Core to platforma programistyczna lekka międzyplatformowa sieci web, który służy do tworzenia nowoczesnych witryn sieci web interfejsu użytkownika i interfejsów API sieci web. Aby uzyskać pełne zrozumienie sposobu platformy ASP.NET Core integruje się z sieci szkieletowej usług, zalecamy przeczytanie za pośrednictwem [platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md) artykułu. Obecnie można wykonać w tym samouczku, aby szybko rozpocząć pracę. Aby dowiedzieć się więcej na temat platformy ASP.NET Core, zobacz [platformy ASP.NET Core dokumentacji](https://docs.microsoft.com/aspnet/core/).

1. Uruchom program Visual Studio jako **administrator**.

2. Tworzenie projektu z **pliku**->**nowy**->**projektu**

3. W oknie dialogowym **Nowy projekt** wybierz kolejno pozycje **Chmura > Aplikacja usługi Service Fabric**.

4. Nazwa aplikacji **głosowania** i naciśnij klawisz **OK**.

   ![Okno dialogowe nowego projektu w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Na **Nowa usługa sieci szkieletowej usług** wybierz pozycję **bezstanowych platformy ASP.NET Core**i nadaj nazwę usługi **VotingWeb**.
   
   ![Wybieranie usługi sieci web ASP.NET w oknie dialogowym Nowy usługi](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. Następna strona zawiera zestaw platformy ASP.NET Core szablonów projektu. W tym samouczku, wybierz **aplikacji sieci Web (Model-View-Controller)**. 
   
   ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio tworzy aplikację oraz projekt usługi i wyświetla je w Eksploratorze rozwiązań.

   ![Eksplorator rozwiązań po utworzeniu aplikacji z platformy ASP.NET core usługi interfejsu API sieci Web]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a>Dodaj AngularJS do usługi VotingWeb
Dodaj [AngularJS](http://angularjs.org/) przy użyciu usługi [Bower Obsługa](/aspnet/core/client-side/bower). Najpierw dodaj plik konfiguracji Bower do projektu.  W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **VotingWeb** i wybierz **Dodaj -> Nowy element**. Wybierz **Web** , a następnie **Bower w pliku konfiguracji**.  *Bower.json* tworzony jest plik.

Otwórz *bower.json* i Dodaj pozycje kątowego i kąta początkowego, a następnie zapisz zmiany.

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "3.2.1",
    "jquery-validation": "1.16.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.8",
    "angular-bootstrap": "v1.1.0"
  }
}
```
Po zapisaniu *bower.json* Twojego projektu zainstalowano plik, kątową *wwwroot/lib* folderu. Ponadto ta opcja jest wyświetlana w ramach *zależności/Bower* folderu.

### <a name="update-the-sitejs-file"></a>Zaktualizuj plik site.js
Otwórz *wwwroot/js/site.js* pliku.  Zastąp jego zawartość JavaScript używane przez widoki głównej:

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

### <a name="update-the-indexcshtml-file"></a>Zaktualizuj plik Index.cshtml
Otwórz *Views/Home/Index.cshtml* pliku specyficzne dla kontrolera głównej widoku.  Zastąp jego zawartość następujące, a następnie zapisz zmiany.

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
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item"/>
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr/>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click to vote
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

### <a name="update-the-layoutcshtml-file"></a>Zaktualizuj plik _Layout.cshtml
Otwórz *Views/Shared/_Layout.cshtml* plik domyślny układ dla aplikacji ASP.NET.  Zastąp jego zawartość następujące, a następnie zapisz zmiany.

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet"/>
    <link href="~/css/site.css" rel="stylesheet"/>

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

### <a name="update-the-votingwebcs-file"></a>Zaktualizuj plik VotingWeb.cs
Otwórz *VotingWeb.cs* pliku, który tworzy platformy ASP.NET Core hostem sieci Web wewnątrz usługi bezstanowej, przy użyciu WebListener serwera sieci web.  

Dodaj `using System.Net.Http;` dyrektywy na początku pliku.  

Zastąp `CreateServiceInstanceListeners()` działać z następujących czynności, a następnie zapisz zmiany.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(
            serviceContext =>
                new KestrelCommunicationListener(
                    serviceContext,
                    "ServiceEndpoint",
                    (url, listener) =>
                    {
                        ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting Kestrel on {url}");

                        return new WebHostBuilder()
                            .UseKestrel()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<HttpClient>(new HttpClient())
                                    .AddSingleton<FabricClient>(new FabricClient())
                                    .AddSingleton<StatelessServiceContext>(serviceContext))
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
                    }))
    };
}
```

Dodaj również `GetVotingDataServiceName` metody, która zwraca nazwę usługi podczas sondowania:

```csharp
internal static Uri GetVotingDataServiceName(ServiceContext context)
{
    return new Uri($"{context.CodePackageActivationContext.ApplicationName}/VotingData");
}
```

### <a name="add-the-votescontrollercs-file"></a>Dodaj plik VotesController.cs
Dodaj kontroler, który definiuje akcje głosu. Kliknij prawym przyciskiem myszy **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**.  Nazwa pliku "VotesController.cs", a następnie kliknij przycisk **Dodaj**.  

Zastąp zawartość pliku z następującym, a następnie zapisz zmiany.  W dalszej [zaktualizować pliku VotesController.cs](#updatevotecontroller_anchor), ten plik został zmodyfikowany na odczytywanie i zapisywanie danych głosowania z usługi zaplecza.  Obecnie kontrolera zwraca ciąg statycznych danych do widoku.

```csharp
namespace VotingWeb.Controllers
{
    using System;
    using System.Collections.Generic;
    using System.Fabric;
    using System.Fabric.Query;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Newtonsoft.Json;

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

### <a name="configure-the-listening-port"></a>Skonfiguruj port nasłuchujący
Po utworzeniu usługi frontonu VotingWeb Visual Studio losowo wybiera port dla usługi do nasłuchiwania.  Usługa VotingWeb działa jako frontonu dla tej aplikacji i akceptuje ruch zewnętrzny, więc warto powiązać ustalonego tej usługi i także znać port.  [Manifestu usługi](service-fabric-application-and-service-manifests.md) deklaruje punktów końcowych usługi. W Eksploratorze rozwiązań Otwórz *VotingWeb/PackageRoot/ServiceManifest.xml*.  Znajdź **punktu końcowego** zasobu w **zasobów** sekcji i zmień **portu** wartość 80, lub do innego portu. Aby wdrożyć i uruchomić aplikację lokalnie, port nasłuchujący aplikacji musi być otwartego i dostępnego na komputerze.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Również zaktualizować wartość właściwości adresu URL aplikacji w projekcie głosowania, więc w przeglądarce sieci web zostanie otwarty do właściwego portu podczas debugowania za pomocą "F5".  W Eksploratorze rozwiązań wybierz **głosowania** projektu i zaktualizuj **adres URL aplikacji** właściwości.

![Adres URL aplikacji](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

### <a name="deploy-and-run-the-application-locally"></a>Wdrażanie i uruchamianie aplikacji lokalnie
Możesz teraz Przejdź dalej i uruchomić aplikację. W programie Visual Studio naciśnij klawisz `F5`, aby wdrożyć aplikację do debugowania. `F5`kończy się niepowodzeniem, jeśli wcześniej nie został otwarty program Visual Studio jako **administratora**.

> [!NOTE]
> Przy pierwszym uruchamianiu i wdrażaniu aplikacji w środowisku lokalnym program Visual Studio tworzy lokalny klaster na potrzeby debugowania.  Tworzenie klastra może zająć trochę czasu. Stan tworzenia klastra jest wyświetlany w oknie danych wyjściowych programu Visual Studio.

W tym momencie aplikacji sieci web powinien wyglądać następująco:

![Platformy ASP.NET Core frontonu](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

Aby zatrzymać debugowanie aplikacji, wróć do programu Visual Studio i naciśnij klawisz **Shift + F5**.

## <a name="add-a-stateful-back-end-service-to-your-application"></a>Dodaj stanowe usługi zaplecza do aplikacji
Teraz, gdy Usługa interfejsu API sieci Web platformy ASP.NET jest uruchomiona w aplikacji, przejdź dalej i dodać stanowe niezawodnej usługi do przechowywania niektóre dane w aplikacji.

Sieć szkieletowa usług pozwala na spójne i niezawodne przechowywanie dane bezpośrednio w usłudze przy użyciu niezawodnych kolekcje. Niezawodne kolekcje są zestawem klasy kolekcji wysokiej dostępności i niezawodne, które są znane dla każdego, kto został użyty kolekcje C#.

W tym samouczku utworzysz usługę, która przechowuje wartość licznika w niezawodnej kolekcji.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **usług** aplikacji projekt i wybierz pozycję **Dodaj > Nowa usługa sieci szkieletowej usług**.
    
2. W **Nowa usługa sieci szkieletowej usług** okno dialogowe, wybierz **Stateful platformy ASP.NET Core**i nadaj nazwę usługi **VotingData** i naciśnij klawisz **OK**.

    ![Okno dialogowe nowej usługi w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Po utworzeniu projektu usługi dostępne są dwie usługi w aplikacji. Jak można kontynuować tworzenie aplikacji, można dodać więcej usług w taki sam sposób. Każdy może być niezależnie określonej wersji, jak i uaktualnionych.

3. Następna strona zawiera zestaw platformy ASP.NET Core szablonów projektu. W tym samouczku, wybierz **interfejsu API sieci Web**.

    ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio tworzy projekt usługi i wyświetla je w Eksploratorze rozwiązań.

    ![Eksplorator rozwiązań](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-webapi-service.png)

### <a name="add-the-votedatacontrollercs-file"></a>Dodaj plik VoteDataController.cs

W **VotingData** projektu kliknij prawym przyciskiem myszy **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**. Nazwa pliku "VoteDataController.cs", a następnie kliknij przycisk **Dodaj**. Zastąp zawartość pliku z następującym, a następnie zapisz zmiany.

```csharp
// ------------------------------------------------------------
//  Copyright (c) Microsoft Corporation.  All rights reserved.
//  Licensed under the MIT License (MIT). See License.txt in the repo root for license information.
// ------------------------------------------------------------

namespace VotingData.Controllers
{
    using System.Collections.Generic;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.ServiceFabric.Data;
    using Microsoft.ServiceFabric.Data.Collections;

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
            CancellationToken ct = new CancellationToken();

            IReliableDictionary<string, int> votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                IAsyncEnumerable<KeyValuePair<string, int>> list = await votesDictionary.CreateEnumerableAsync(tx);

                IAsyncEnumerator<KeyValuePair<string, int>> enumerator = list.GetAsyncEnumerator();

                List<KeyValuePair<string, int>> result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return this.Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            IReliableDictionary<string, int> votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

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
            IReliableDictionary<string, int> votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

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


## <a name="connect-the-services"></a>Połączenie usługi
W następnym kroku należy połączyć z dwóch usług i wprowadzić frontonu sieci Web aplikacji elementu get i set głosowania informacji z usługi zaplecza.

Sieć szkieletowa usług oferuje pełną elastyczność w sposób komunikowania się z usługami reliable services. Wewnątrz aplikacji konieczne może być usług, które są dostępne za pośrednictwem protokołu TCP. Inne usługi, które mogą być dostępne za pośrednictwem interfejsu API REST protokołu HTTP i innych usług może być dostępny za pośrednictwem gniazda sieci web. W tle na dostępne opcje oraz zaangażowanych skutków ubocznych, zobacz [komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md).

W tym samouczku, użyj [Web API platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a>Zaktualizuj plik VotesController.cs
W **VotingWeb** otwarciu projektu *Controllers/VotesController.cs* pliku.  Zastąp `VotesController` klasy definicji zawartość następującym kodem, a następnie zapisz zmiany.

```csharp
public class VotesController : Controller
{
    private readonly HttpClient httpClient;
    private readonly FabricClient fabricClient;
    private readonly StatelessServiceContext serviceContext;

    public VotesController(HttpClient httpClient, StatelessServiceContext context, FabricClient fabricClient)
    {
        this.fabricClient = fabricClient;
        this.httpClient = httpClient;
        this.serviceContext = context;
    }

    // GET: api/Votes
    [HttpGet("")]
    public async Task<IActionResult> Get()
    {
        Uri serviceName = VotingWeb.GetVotingDataServiceName(this.serviceContext);
        Uri proxyAddress = this.GetProxyAddress(serviceName);

        ServicePartitionList partitions = await this.fabricClient.QueryManager.GetPartitionListAsync(serviceName);

        List<KeyValuePair<string, int>> result = new List<KeyValuePair<string, int>>();

        foreach (Partition partition in partitions)
        {
            string proxyUrl =
                $"{proxyAddress}/api/VoteData?PartitionKey={((Int64RangePartitionInformation) partition.PartitionInformation).LowKey}&PartitionKind=Int64Range";

            using (HttpResponseMessage response = await this.httpClient.GetAsync(proxyUrl))
            {
                if (response.StatusCode != System.Net.HttpStatusCode.OK)
                {
                    continue;
                }

                result.AddRange(JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync()));
            }
        }

        return this.Json(result);
    }

    // PUT: api/Votes/name
    [HttpPut("{name}")]
    public async Task<IActionResult> Put(string name)
    {
        Uri serviceName = VotingWeb.GetVotingDataServiceName(this.serviceContext);
        Uri proxyAddress = this.GetProxyAddress(serviceName);
        long partitionKey = this.GetPartitionKey(name);
        string proxyUrl = $"{proxyAddress}/api/VoteData/{name}?PartitionKey={partitionKey}&PartitionKind=Int64Range";

        StringContent putContent = new StringContent($"{{ 'name' : '{name}' }}", Encoding.UTF8, "application/json");
        putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

        using (HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent))
        {
            return new ContentResult()
            {
                StatusCode = (int) response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }
    }

    // DELETE: api/Votes/name
    [HttpDelete("{name}")]
    public async Task<IActionResult> Delete(string name)
    {
        Uri serviceName = VotingWeb.GetVotingDataServiceName(this.serviceContext);
        Uri proxyAddress = this.GetProxyAddress(serviceName);
        long partitionKey = this.GetPartitionKey(name);
        string proxyUrl = $"{proxyAddress}/api/VoteData/{name}?PartitionKey={partitionKey}&PartitionKind=Int64Range";

        using (HttpResponseMessage response = await this.httpClient.DeleteAsync(proxyUrl))
        {
            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int) response.StatusCode);
            }
        }

        return new OkResult();
    }


    /// <summary>
    /// Constructs a reverse proxy URL for a given service.
    /// Example: http://localhost:19081/VotingApplication/VotingData/
    /// </summary>
    /// <param name="serviceName"></param>
    /// <returns></returns>
    private Uri GetProxyAddress(Uri serviceName)
    {
        return new Uri($"http://localhost:19081{serviceName.AbsolutePath}");
    }

    /// <summary>
    /// Creates a partition key from the given name.
    /// Uses the zero-based numeric position in the alphabet of the first letter of the name (0-25).
    /// </summary>
    /// <param name="name"></param>
    /// <returns></returns>
    private long GetPartitionKey(string name)
    {
        return Char.ToUpper(name.First()) - 'A';
    }
}
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-the-voting-sample-application"></a>Szczegółowe omówienie przykładowej aplikacji do głosowania
Aplikacja do głosowania składa się z dwóch usług:
- Usługa internetowa frontonu (VotingWeb) — usługa internetowa frontonu platformy ASP.NET Core, obsługująca stronę internetową i ujawniająca interfejsy API sieci Web na potrzeby komunikacji z usługą zaplecza.
- Usługi zaplecza (VotingData) — usługa internetowa platformy ASP.NET Core, która uwidacznia interfejs API do przechowywania wyników głosowania w niezawodnym słowniku utrwalonym na dysku.

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Podczas głosowania w aplikacji występują następujące zdarzenia:
1. Plik JavaScript wysyła żądanie głosowania do internetowego interfejsu API w usłudze internetowej frontonu jako żądanie HTTP PUT.

2. Usługa internetowa frontonu używa serwera proxy w celu zlokalizowania i przesłania żądania HTTP PUT do usługi zaplecza.

3. Usługa zaplecza przyjmuje żądanie przychodzące i przechowuje zaktualizowany wynik w niezawodnym słowniku, który jest replikowany do wielu węzłów w klastrze i utrwalany na dysku. Wszystkie dane aplikacji są przechowywane w klastrze, więc baza danych nie jest wymagana.

## <a name="debug-in-visual-studio"></a>Debugowanie w programie Visual Studio
Podczas debugowania aplikacji w programie Visual Studio używany jest lokalny klaster projektowy usługi Service Fabric. Możesz opcjonalnie dostosować środowisko debugowania do danego scenariusza. W tej aplikacji przechowywanie danych w usłudze zaplecza przy użyciu niezawodnych słownika. Program Visual Studio domyślnie usuwa aplikację po zatrzymaniu debugera. Usunięcie aplikacji spowoduje, że dane w usłudze zaplecza także zostaną usunięte. Aby zachować dane między sesjami debugowania, możesz zmienić **Tryb debugowania aplikacji** jako właściwość w projekcie **Voting (Głosowanie)** w programie Visual Studio.

Aby zobaczyć, co się stanie w kodzie, wykonaj następujące kroki:
1. Otwórz **VotesController.cs** pliku i ustaw punkt przerwania w sieci web interfejsu API **Put** — metoda (linii 63) — możesz wyszukać plik w Eksploratorze rozwiązań w programie Visual Studio.

2. Otwórz **VoteDataController.cs** pliku i ustaw punkt przerwania w tym składnika web API **Put** — metoda (wiersz 53).

3. Wróć do przeglądarki i kliknij opcję głosowania lub dodaj nową opcję głosowania. Zostanie trafiony pierwszy punkt przerwania w kontrolerze interfejsu API frontonu internetowego.
    
    1. Jest to punkt, w którym skrypt JavaScript w przeglądarce wysyła żądanie do kontrolera internetowego interfejsu API w usłudze frontonu.
    
    ![Dodawanie usługi frontonu Vote (Głosowanie)](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Najpierw utworzyć adres URL, który ReverseProxy usługi zaplecza **(1)**.
    3. Następnie wysłać umieść żądanie HTTP do ReverseProxy **(2)**.
    4. Na koniec zwracany do klienta odpowiedź z usługi zaplecza **(3)**.

4. Naciśnij klawisz **F5**, aby kontynuować
    1. Jesteś teraz w punkcie przerwania w usłudze zaplecza.
    
    ![Dodawanie usługi zaplecza Vote](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. W pierwszym wierszu w metodzie **(1)** użyj `StateManager` do pobrania lub dodać słownika niezawodnej o nazwie `counts`.
    3. Wszystkie interakcje z wartościami w niezawodnym słowniku wymagają transakcji — ta instrukcja using **(2)** tworzy tę transakcję.
    4. W transakcji, zaktualizuj tę wartość klucza odpowiednich opcji głosu i zatwierdza operacji **(3)**. Po powrocie z metody zatwierdzania dane są aktualizowane w słowniku i replikowane do innych węzłów w klastrze. Dane są bezpiecznie przechowywane w klastrze, a usługa zaplecza może zostać przełączona w tryb failover do innych węzłów, które nadal mają dostępne dane.
5. Naciśnij klawisz **F5**, aby kontynuować

Aby zatrzymać sesję debugowania, naciśnij klawisze **Shift+F5**.


## <a name="next-steps"></a>Kolejne kroki
W tej części samouczka przedstawiono sposób:

> [!div class="checklist"]
> * Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej
> * Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych
> * Użyć zwrotnego serwera proxy do komunikacji z usługą stanową

Przejdź do następnego samouczek:
> [!div class="nextstepaction"]
> [Wdrażanie aplikacji na platformie Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md)
