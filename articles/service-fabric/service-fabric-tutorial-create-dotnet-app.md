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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Tworzenie i wdrażanie aplikacji przy użyciu interfejsu API platformy ASP.NET Core sieci Web usługi frontonu i usługi stanowej zaplecza
W tym samouczku wchodzi w jednej serii.  Dowiesz się jak toocreate aplikacji sieci szkieletowej usług Azure z przodu interfejsu API platformy ASP.NET Core sieci Web zakończenie i toostore usługi stanowej zaplecza danych. Po zakończeniu, masz aplikację do głosowania z frontonu, który zapisuje wyniki głosowania stanowe usługi zaplecza w klastrze hello sieci web platformy ASP.NET Core. Jeśli nie chcesz toomanually utworzyć hello głosowania aplikacji, możesz [pobrać kodu źródłowego hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) dla hello ukończone aplikacji i przejść od razu zbyt[Przewodnik po głosowanie w przykładowej aplikacji hello](#walkthrough_anchor).

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

W części jednej serii hello, możesz dowiedzieć się, jak:

> [!div class="checklist"]
> * Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej
> * Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych
> * Witaj toocommunicate zwrotnego serwera proxy za pomocą usługi stanowej hello

W tym samouczku dowiesz się, jak:
> [!div class="checklist"]
> * Tworzenie aplikacji sieci szkieletowej usług .NET
> * [Wdrażanie klastra zdalnego tooa aplikacji hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka:
- Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) i zainstaluj hello **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.
- [Zainstaluj hello zestawu SDK sieci szkieletowej usług](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Tworzenie usługi dla składnika ASP.NET Web API jako niezawodnej usługi
Najpierw utwórz hello sieci web frontonu z hello głosowania aplikacji przy użyciu platformy ASP.NET Core. Platformy ASP.NET Core to platforma programistyczna lekka międzyplatformowa sieci web można używać nowoczesnych toocreate interfejsu użytkownika sieci web i interfejsów API sieci web. tooget pełną wiedzę na temat sposobu platformy ASP.NET Core integruje się z sieci szkieletowej usług, zalecamy przeczytanie za pośrednictwem hello [platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md) artykułu. Teraz można wykonać tego samouczka tooget szybko rozpocząć pracę. toolearn więcej informacji na temat platformy ASP.NET Core, zobacz hello [platformy ASP.NET Core dokumentacji](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> W tym samouczku jest oparta na powitania [platformy ASP.NET Core narzędzi dla programu Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). już trwa aktualizowanie Hello .NET Core tools dla programu Visual Studio 2015.

1. Uruchom program Visual Studio jako **administrator**.

2. Tworzenie projektu z **pliku**->**nowy**->**projektu**

3. W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.

4. Nadaj nazwę aplikacji hello **głosowania** i naciśnij klawisz **OK**.

   ![Okno dialogowe nowego projektu w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Na powitania **Nowa usługa sieci szkieletowej usług** wybierz pozycję **bezstanowych platformy ASP.NET Core**i nadaj nazwę usługi **VotingWeb**.
   
   ![Wybieranie usługi sieci web ASP.NET w oknie dialogowym hello nowej usługi](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu. W tym samouczku, wybierz **aplikacji sieci Web**. 
   
   ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio tworzy aplikację oraz projekt usługi i wyświetla je w Eksploratorze rozwiązań.

   ![Eksplorator rozwiązań po utworzeniu aplikacji z platformy ASP.NET core usługi interfejsu API sieci Web]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Dodaj usługę VotingWeb toohello AngularJS
Dodaj [AngularJS](http://angularjs.org/) tooyour usługi przy użyciu wbudowanych hello [Bower Obsługa](/aspnet/core/client-side/bower). Otwórz *bower.json* i Dodaj pozycje kątowego i kąta początkowego, a następnie zapisz zmiany.

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
Podczas zapisywania hello *bower.json* Twojego projektu zainstalowano plik, kątową *wwwroot/lib* folderu. Ponadto ta opcja jest wyświetlana w ramach hello *zależności/Bower* folderu.

### <a name="update-hello-sitejs-file"></a>Plik site.js hello aktualizacji
Otwórz hello *wwwroot/js/site.js* pliku.  Zastąp jego zawartość hello JavaScript używane przez widoki głównej hello:

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

### <a name="update-hello-indexcshtml-file"></a>Plik Index.cshtml hello aktualizacji
Otwórz hello *Views/Home/Index.cshtml* plik, określonym kontrolerem głównej toohello hello widoku.  Zastąp jego zawartość następujących hello, a następnie zapisz zmiany.

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

### <a name="update-hello-layoutcshtml-file"></a>Plik _Layout.cshtml hello aktualizacji
Otwórz hello *Views/Shared/_Layout.cshtml* plik, układ domyślny hello hello aplikacji ASP.NET.  Zastąp jego zawartość następujących hello, a następnie zapisz zmiany.

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

### <a name="update-hello-votingwebcs-file"></a>Plik VotingWeb.cs hello aktualizacji
Otwórz hello *VotingWeb.cs* pliku, który tworzy hello hosta sieci Web platformy ASP.NET Core wewnątrz usługi bezstanowej hello przy użyciu serwera sieci web WebListener hello.  Dodaj hello `using System.Net.Http;` początku dyrektywy toohello hello pliku.  Zastąp hello `CreateServiceInstanceListeners()` działać z hello poniżej, a następnie zapisz zmiany.

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

### <a name="add-hello-votescontrollercs-file"></a>Dodaj plik VotesController.cs hello
Dodaj kontroler, który definiuje akcje głosu. Kliknij prawym przyciskiem myszy na powitania **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**.  Nadaj nazwę plikowi hello "VotesController.cs", a następnie kliknij przycisk **Dodaj**.  Zastąp zawartość pliku hello hello poniżej, a następnie zapisz zmiany.  W dalszej [pliku VotesController.cs hello aktualizacji](#updatevotecontroller_anchor), ten plik zostanie zmodyfikowane tooread i zapisywania danych głosowania z hello usługi zaplecza.  Obecnie kontrolera hello zwraca ciąg statycznych danych toohello widoku.

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



### <a name="deploy-and-run-hello-application-locally"></a>Wdrażanie i uruchamianie aplikacji hello lokalnie
Możesz teraz Przejdź dalej i uruchamianie aplikacji hello. W programie Visual Studio, naciśnij klawisz `F5` toodeploy hello aplikację do debugowania. `F5`kończy się niepowodzeniem, jeśli wcześniej nie został otwarty program Visual Studio jako **administratora**.

> [!NOTE]
> Witaj pierwszego uruchomienia i wdrażanie aplikacji hello lokalnie, Visual Studio tworzy lokalny klaster na potrzeby debugowania.  Tworzenie klastra może zająć trochę czasu. Stan tworzenia klastra Hello jest wyświetlany w oknie danych wyjściowych programu Visual Studio hello.

W tym momencie aplikacji sieci web powinien wyglądać następująco:

![Platformy ASP.NET Core frontonu](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

debugowanie aplikacji hello toostop wrócić do poprzedniej strony tooVisual Studio i naciśnij klawisz **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Dodaj aplikację tooyour usługi stanowej zaplecza
Teraz, gdy mamy Usługa interfejsu API sieci Web platformy ASP.NET w naszej aplikacji jest uruchomiona, spróbuj teraz i Dodaj toostore niezawodnej usługi stanowej niektóre dane w naszej aplikacji.

Sieć szkieletowa usług pozwala tooconsistently i niezawodne przechowywanie dane bezpośrednio w usłudze przy użyciu niezawodnych kolekcji. Niezawodne kolekcje są zestaw klas wysokiej dostępności i niezawodne kolekcji, które są znane tooanyone, który został użyty kolekcje C#.

W tym samouczku utworzysz usługę, która przechowuje wartość licznika w niezawodnej kolekcji.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **usług** poziomu projekt aplikacji hello i wybierz polecenie **Dodaj > Nowa usługa sieci szkieletowej usług**.
   
    ![Dodawanie nowej usługi tooan istniejącej aplikacji](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. W hello **Nowa usługa sieci szkieletowej usług** okno dialogowe, wybierz **Stateful platformy ASP.NET Core**i usługa hello nazw **VotingData** i naciśnij klawisz **OK**.

    ![Okno dialogowe nowej usługi w programie Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Po utworzeniu projektu usługi dostępne są dwie usługi w aplikacji. Kontynuując toobuild aplikacji, można dodać więcej usług w hello tak samo. Każdy może być niezależnie określonej wersji, jak i uaktualnionych.

3. Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu. W tym samouczku, wybierz **interfejsu API sieci Web**.

    ![Wybierz typ projektu programu ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio tworzy projekt usługi i wyświetla je w Eksploratorze rozwiązań.

    ![Eksplorator rozwiązań](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Dodaj plik VoteDataController.cs hello

W hello **VotingData** kliknij prawym przyciskiem myszy projekt na powitania **kontrolerów** folderu, następnie wybierz **Dodaj -> Nowy element -> klasy**. Nadaj nazwę plikowi hello "VoteDataController.cs", a następnie kliknij przycisk **Dodaj**. Zastąp zawartość pliku hello hello poniżej, a następnie zapisz zmiany.

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


## <a name="connect-hello-services"></a>Połączenie usług hello
W następnym kroku firma Microsoft będzie połączyć z hello dwóch usług i wprowadzić hello frontonu sieci Web aplikacji elementu get i set głosowania informacji z usługi zaplecza hello.

Sieć szkieletowa usług oferuje pełną elastyczność w sposób komunikowania się z usługami reliable services. Wewnątrz aplikacji konieczne może być usług, które są dostępne za pośrednictwem protokołu TCP. Inne usługi, które mogą być dostępne za pośrednictwem interfejsu API REST protokołu HTTP i innych usług może być dostępny za pośrednictwem gniazda sieci web. W tle na dostępne opcje hello oraz kompromisy hello zaangażowany, zobacz [komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md).

W tym samouczku używamy [Web API platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Plik VotesController.cs hello aktualizacji
W hello **VotingWeb** projektu, otwórz hello *Controllers/VotesController.cs* pliku.  Zastąp hello `VotesController` zawartość definicji hello następujące klasy, a następnie zapisz zmiany.

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

## <a name="walk-through-hello-voting-sample-application"></a>Przewodnik po głosowanie w przykładowej aplikacji hello
głosowania aplikacji Hello składa się z dwóch usług:
- Usługa frontonu (VotingWeb) sieci Web — platformy ASP.NET Core usługi frontonu, która służy hello strony sieci web i ujawnia sieci web API toocommunicate hello usługi wewnętrznej bazy danych.
- Usługi zaplecza (VotingData) — usługi sieci web platformy ASP.NET Core, która ujawnia interfejsu API toostore hello głos powoduje niezawodnej słownika utrwalony na dysku.

![Diagram aplikacji](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Po głosowanie w hello aplikacji hello następującego wystąpienia zdarzeń:
1. JavaScript wysyła hello głos żądanie toohello interfejsu API sieci web usługi frontonu sieci web hello jako żądanie HTTP PUT.

2. Usługa frontonu sieci web Hello używa toolocate serwera proxy i przesyła usługi zaplecza HTTP PUT toohello żądania.

3. usługi zaplecza Hello przyjmuje hello żądania przychodzącego, a hello magazynów zaktualizowany wynik w niezawodnej słownik, który pobiera replikowanych toomultiple węzłów w klastrze hello i utrwalony na dysku. Dane wszystkich aplikacji hello są przechowywane w klastrze hello, więc nie bazy danych nie jest wymagane.

## <a name="debug-in-visual-studio"></a>Debugowanie w programie Visual Studio
Podczas debugowania aplikacji w programie Visual Studio, czy używasz klastra lokalnego Projektowanie sieci szkieletowej usług. Masz hello tooadjust opcji debugowania scenariusz tooyour środowisko. W tej aplikacji są przechowywane dane w naszej usługi zaplecza przy użyciu niezawodnych słownika. Po zatrzymaniu debugera hello programu Visual Studio spowoduje usunięcie aplikacji hello na domyślne. Usunięcie aplikacji hello powoduje hello danych w wewnętrznej hello tooalso usługi można usunąć. toopersist hello danych między sesji debugowania, możesz zmienić hello **tryb debugowania aplikacji** jako właściwość hello **głosowania** projektu programu Visual Studio.

toolook na co się stanie w kodzie hello, pełną hello następujące kroki:
1. Otwórz hello **VotesController.cs** pliku i ustaw punkt przerwania w składniku web API hello **Put** — metoda (linii 47) — możesz wyszukać plik hello w hello Eksploratora rozwiązań w programie Visual Studio.

2. Otwórz hello **VoteDataController.cs** pliku i ustaw punkt przerwania w tym składnika web API **Put** — metoda (wiersz 50).

3. Przejść toohello przeglądarki i kliknij opcję głosu lub dodać nową opcję głosu. Naciśniesz hello pierwszy punkt przerwania hello web przodu end w kontrolerze interfejsu api.
    
    1. Jest to, gdzie hello JavaScript w przeglądarce hello wysyła kontrolera interfejsu API sieci web toohello żądania w hello usługi frontonu.
    
    ![Dodawanie usługi frontonu głosu](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Najpierw możemy utworzyć hello adresu URL toohello ReverseProxy dla naszej usługi zaplecza **(1)**.
    3. Następnie możemy wysłać hello HTTP PUT żądanie toohello ReverseProxy **(2)**.
    4. Na koniec hello zostanie zwrócona odpowiedź hello z klienta toohello usługi zaplecza hello **(3)**.

4. Naciśnij klawisz **F5** toocontinue
    1. Jesteś teraz w punkcie przerwania hello hello usługi zaplecza.
    
    ![Dodawania usługi zaplecza głosu](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. W hello pierwszego wiersza w metodzie hello **(1)** używamy hello `StateManager` tooget lub dodać słownika niezawodnej o nazwie `counts`.
    3. Wszystkie interakcje z wartości w słowniku niezawodnej wymagają transakcji, za pomocą tej instrukcji **(2)** tworzy tej transakcji.
    4. W transakcji hello modyfikacjom następnie hello wartość hello odpowiedniego klucza hello głosowania opcji i zatwierdzeń hello operacji **(3)**. Po zatwierdzić hello metoda zwróci wartość, hello danych jest aktualizowany w słowniku hello i replikowane tooother węzłów w klastrze hello. dane Hello teraz są bezpiecznie przechowywane w hello klastra, a usługi zaplecza hello może przełączyć się węzłów tooother zachowaniu hello dostępnych danych.
5. Naciśnij klawisz **F5** toocontinue

hello toostop sesję, naciśnij klawisz debugowania **Shift + F5**.


## <a name="next-steps"></a>Następne kroki
W tej części samouczka hello przedstawiono sposób:

> [!div class="checklist"]
> * Tworzenie usługi interfejsu API platformy ASP.NET Core sieci Web jako usługa stanowa niezawodnej
> * Tworzenie usługi dla aplikacji sieci Web platformy ASP.NET Core jako usługę sieci web bezstanowych
> * Witaj toocommunicate zwrotnego serwera proxy za pomocą usługi stanowej hello

Następny samouczek toohello wyprzedzeniem:
> [!div class="nextstepaction"]
> [Wdrażanie tooAzure aplikacji hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
