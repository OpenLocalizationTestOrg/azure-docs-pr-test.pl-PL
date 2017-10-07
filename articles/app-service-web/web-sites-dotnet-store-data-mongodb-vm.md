---
title: "aaaCreate aplikacji sieci web na platformie Azure, łączącego tooMongoDB uruchomione na maszynie wirtualnej"
description: "Samouczek opisujący sposób toouse Git toodeploy tooAzure aplikacji ASP.NET usługi aplikacji połączenia tooMongoDB na maszynie wirtualnej platformy Azure."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Tworzenie aplikacji sieci web na platformie Azure, łączącego tooMongoDB uruchomione na maszynie wirtualnej
Przy użyciu narzędzia Git, można wdrożyć tooAzure aplikacji ASP.NET aplikacji usługi sieci Web aplikacji. W tym samouczku utworzysz prosty frontonu ASP.NET MVC aplikacji listy zadań, która łączy bazy danych MongoDB tooa uruchomione na maszynie wirtualnej na platformie Azure.  [Bazy danych MongoDB] [ MongoDB] jest popularnych typu open source, bazy danych NoSQL o wysokiej wydajności. Po uruchomione i testowanie aplikacji ASP.NET hello na komputerze deweloperskim, przekaże tooApp aplikacji hello usługi aplikacje sieci Web przy użyciu narzędzia Git.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="background-knowledge"></a>Tło wiedzy
Wiedzę na temat następujących hello jest przydatne w tym samouczku, ale nie wymagane:

* Sterownik Hello C# dla bazy danych MongoDB. Aby uzyskać więcej informacji na temat tworzenia aplikacji C# dla bazy danych MongoDB, zobacz hello bazy danych MongoDB [Center języka CSharp][MongoC#LangCenter]. 
* Witaj platforma aplikacji sieci web ASP .NET. Dowiedz się, wszystkie dotyczące go na powitania [witryny sieci Web ASP.net][ASP.NET].
* platforma aplikacji sieci web ASP .NET MVC Hello. Dowiedz się, wszystkie dotyczące go na powitania [witryny sieci Web platformy ASP.NET MVC][MVCWebSite].
* Azure. Można rozpocząć odczytywanie na [Azure][WindowsAzure].

## <a name="prerequisites"></a>Wymagania wstępne
* [Program Visual Studio Express 2013 for Web] [ VSEWeb] lub [programu Visual Studio 2013][VSUlt]
* [Zestaw Azure SDK dla platformy .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Aktywną subskrypcją Microsoft Azure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB
W tym samouczku założono, że utworzono maszynę wirtualną na platformie Azure. Po utworzeniu maszyny wirtualnej hello należy tooinstall bazy danych MongoDB na maszynie wirtualnej hello:

* toocreate maszyny wirtualnej systemu Windows i Instalacja bazy danych MongoDB, zobacz [MongoDB zainstalować na maszynie wirtualnej z systemem Windows Server na platformie Azure][InstallMongoOnWindowsVM].

Po utworzeniu maszyny wirtualnej hello na platformie Azure i zainstalowane bazy danych MongoDB, być czy tooremember hello nazwą DNS hello maszyny wirtualnej ("testlinuxvm.cloudapp.net", na przykład) i porcie zewnętrznym hello bazy danych mongodb, określona w hello punktu końcowego.  Należy w dalszej części samouczka hello.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
W tej sekcji utworzysz aplikację ASP.NET przy użyciu programu Visual Studio o nazwie "My listy zadań" i wykonać tooAzure początkowe wdrożenie aplikacji usługi sieci Web aplikacji. Aplikacja hello zostaną uruchomione lokalnie, ale zostanie połączyć tooyour maszyny wirtualnej na platformie Azure i używać utworzone wystąpienie bazy danych MongoDB hello.

1. W programie Visual Studio, kliknij przycisk **nowy projekt**.
   
    ![Nowy projekt strony][StartPageNewProject]
2. W hello **nowy projekt** oknie w lewym okienku hello, wybierz opcję **Visual C#**, a następnie wybierz **sieci Web**. W środkowym okienku hello, wybierz **aplikacji sieci Web ASP.NET**. U dołu hello nazwy projektu "MyTaskListApp", a następnie kliknij przycisk **OK**.
   
    ![Okno dialogowe Nowy projekt][NewProjectMyTaskListApp]
3. W hello **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC**, a następnie kliknij przycisk **OK**.
   
    ![Wybierz szablon MVC][VS2013SelectMVCTemplate]
4. Jeśli nie jest już zarejestrowany w Microsoft Azure, będzie zostanie wyświetlony monit o toosign w. Wykonaj toosign monity hello na platformie Azure.
5. Gdy użytkownik jest zalogowany, możesz rozpocząć konfigurowanie aplikacji sieci web usługi aplikacji. Określ hello **Nazwa aplikacji sieci Web**, **planu usługi aplikacji**, **grupy zasobów**, i **Region**, następnie kliknij przycisk **Utwórz**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Po zakończeniu tworzenia projektu hello, poczekaj, aż toobe aplikacji sieci web hello utworzone w usłudze Azure App Service, wskazane hello **działanie usługi Azure App Service** okna. Następnie kliknij przycisk **teraz opublikować MyTaskListApp toothis aplikacji sieci Web**.
7. Kliknij przycisk **Opublikuj**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Gdy domyślnej aplikacji ASP.NET jest tooAzure opublikowanej aplikacji usługi sieci Web aplikacji, zostanie uruchomiony w przeglądarce hello.

## <a name="install-hello-mongodb-c-driver"></a>Zainstaluj hello sterownik bazy danych MongoDB C#
Bazy danych MongoDB oferuje obsługę po stronie klienta dla aplikacji C# za pośrednictwem sterownika, który należy tooinstall na komputerze deweloperskim lokalnego. Witaj C# sterownik jest dostępny za pośrednictwem pakietu NuGet.

Witaj tooinstall sterownik bazy danych MongoDB C#:

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **MyTaskListApp** projekt i wybierz **Zarządzanie NuGetPackages**.
   
    ![Zarządzaj pakietami NuGet][VS2013ManageNuGetPackages]
2. W hello **Zarządzaj pakietami NuGet** okna, w okienku po lewej stronie powitania kliknij **Online**. W hello **wyszukiwania Online** pole na powitania prawo, wpisz "mongodb.driver".  Kliknij przycisk **zainstalować** tooinstall hello sterownika.
   
    ![Wyszukaj bazy danych MongoDB C# sterownika][SearchforMongoDBCSharpDriver]
3. Kliknij przycisk **akceptuję** tooaccept hello 10gen, Inc. postanowienia licencyjne.
4. Kliknij przycisk **Zamknij** po hello sterownik został zainstalowany.
    ![Bazy danych MongoDB C# sterownik zainstalowany][MongoDBCsharpDriverInstalled]

Witaj sterownik bazy danych MongoDB C# jest zainstalowany.  Odwołania toohello **MongoDB.Bson**, **MongoDB.Driver**, i **MongoDB.Driver.Core** biblioteki zostały dodane toohello projektu.

![Odwołania do bazy danych MongoDB C# sterownika][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Dodaj model
W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy *modele* folderu i **Dodaj** nowy **klasy** i nadaj mu nazwę *TaskModel.cs* .  W *TaskModel.cs*, Zamień istniejący kod hello hello następującego kodu:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a>Dodaj Warstwa dostępu do danych hello
W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello *MyTaskListApp* projektu i **Dodaj** **nowy Folder** o nazwie *DAL*.  Kliknij prawym przyciskiem myszy hello *DAL* folderu i **Dodaj** nowy **klasy**. Nazwa pliku klasy hello *Dal.cs*.  W *Dal.cs*, Zamień istniejący kod hello hello następującego kodu:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>Dodawanie kontrolera
Otwórz hello *Controllers\HomeController.cs* w pliku **Eksploratora rozwiązań** i Zastąp istniejący kod hello hello poniżej:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a>Ustawianie stylów hello
toochange hello tytuł u góry hello hello strony, otwórz hello *Views\Shared\\_Layout.cshtml* w pliku **Eksploratora rozwiązań** i zastąp "Nazwa aplikacji" w nagłówku pasek nawigacyjny hello "Moje zadania Lista aplikacji", aby wygląda następująco:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

W kolejności tooset hello listy zadań menu, otwórz hello *\Views\Home\Index.cshtml* plików i Zastąp istniejący kod hello hello następującego kodu:

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


tooadd hello możliwości toocreate nowe zadanie, kliknij prawym przyciskiem myszy hello *Views\Home\\*  folderu i **Dodaj** **widoku**.  Nazwa widoku hello *Utwórz*. Zastąp kod hello hello następujące czynności:

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Eksplorator rozwiązań** powinna wyglądać następująco:

![Eksplorator rozwiązań][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>Ustawianie parametrów połączenia bazy danych MongoDB hello
W **Eksploratora rozwiązań**, otwórz hello *DAL/Dal.cs* pliku. Znajdź hello po wierszu kodu:

    private string connectionString = "mongodb://<vm-dns-name>";

Zastąp `<vm-dns-name>` o nazwie DNS hello hello maszynę wirtualną działającą bazy danych MongoDB utworzony w hello [Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB] [ Create a virtual machine and install MongoDB] kroku w tym samouczku.  Nazwa DNS hello toofind maszynę wirtualną, przejdź toohello portalu Azure, wybierz **maszyn wirtualnych**i Znajdź **nazwy DNS**.

Jeśli nazwa DNS hello hello maszyny wirtualnej to "testlinuxvm.cloudapp.net" i bazy danych MongoDB nasłuchuje na porcie domyślnym hello 27017, będzie wyglądać hello połączenia ciąg wiersz kodu:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Jeśli hello punktu końcowego maszyny wirtualnej określa innego portu zewnętrznego bazy danych mongodb, możesz zmiennoprzecinkową hello portu w parametrach połączenia hello:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Aby uzyskać więcej informacji dotyczących parametrów połączenia bazy danych MongoDB, zobacz [połączeń][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Testowanie wdrażania lokalne powitania
Wybierz aplikację na komputerze deweloperskim toorun **Rozpocznij debugowanie** z hello **debugowania** menu lub naciśnij klawisz **F5**. Usługi IIS Express uruchamia i przeglądarki zostanie otwarty i uruchamia strony głównej aplikacji hello.  Możesz dodać nowe zadanie, którego będzie można dodać bazy danych MongoDB toohello uruchomione na maszynie wirtualnej na platformie Azure.

![Moja aplikacja listy zadań][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Publikowanie aplikacji sieci Web usługi aplikacji tooAzure
W tej sekcji zostanie opublikowany tooAzure Twojego zmian aplikacji sieci Web usługi aplikacji.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MyTaskListApp** ponownie i kliknij przycisk **publikowania**.
2. Kliknij przycisk **Opublikuj**.
   
    Powinna zostać wyświetlona aplikacja sieci web uruchomionych w usłudze Azure App Service i uzyskiwania dostępu do bazy danych MongoDB hello w maszynach wirtualnych platformy Azure.

## <a name="summary"></a>Podsumowanie
TooAzure aplikacji programu ASP.NET aplikacji usługi sieci Web aplikacji teraz zostały pomyślnie wdrożone. tooview hello aplikacji sieci web:

1. Zaloguj się do hello portalu Azure.
2. Kliknij przycisk **Web apps**. 
3. Wybierz aplikację sieci web w hello **aplikacje sieci Web** listy.

Aby uzyskać więcej informacji dotyczących tworzenia aplikacji C# dla bazy danych MongoDB, zobacz [Center języka CSharp][MongoC#LangCenter]. 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
