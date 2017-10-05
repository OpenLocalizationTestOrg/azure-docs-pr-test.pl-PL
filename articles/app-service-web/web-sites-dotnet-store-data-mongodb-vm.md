---
title: "Tworzenie aplikacji sieci Web na platformie Azure, która łączy się z bazą danych MongoDB uruchomioną na maszynie wirtualnej"
description: "Samouczek opisujący wdrażanie aplikacji ASP.NET w usłudze Azure App Service przy użyciu narzędzia Git podłączony do bazy danych MongoDB na maszynie wirtualnej platformy Azure."
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
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a>Tworzenie aplikacji sieci Web na platformie Azure, która łączy się z bazą danych MongoDB uruchomioną na maszynie wirtualnej
Przy użyciu narzędzia Git, można wdrożyć aplikację ASP.NET do aplikacji sieci Web usługi aplikacji Azure. W tym samouczku utworzysz prosty frontonu ASP.NET MVC aplikację listy zadań, która nawiązuje połączenie z bazą danych MongoDB uruchomione na maszynie wirtualnej na platformie Azure.  [Bazy danych MongoDB] [ MongoDB] jest popularnych typu open source, bazy danych NoSQL o wysokiej wydajności. Po uruchomione i testowania aplikacji programu ASP.NET na komputerze deweloperskim, możesz przekazać aplikację do aplikacji usługi sieci Web aplikacji przy użyciu narzędzia Git.

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="background-knowledge"></a>Tło wiedzy
Znajomość następujące przydaje się w tym samouczku, ale nie wymagane:

* C# sterownik bazy danych mongodb. Aby uzyskać więcej informacji dotyczących tworzenia aplikacji C# dla bazy danych MongoDB, zobacz MongoDB [Center języka CSharp][MongoC#LangCenter]. 
* Platforma aplikacji sieci web ASP .NET. Dowiedz się, wszystkie dotyczące go w [witryny sieci Web ASP.net][ASP.NET].
* Platforma aplikacji sieci web ASP .NET MVC. Dowiedz się, wszystkie dotyczące go w [witryny sieci Web platformy ASP.NET MVC][MVCWebSite].
* Azure. Można rozpocząć odczytywanie na [Azure][WindowsAzure].

## <a name="prerequisites"></a>Wymagania wstępne
* [Program Visual Studio Express 2013 for Web] [ VSEWeb] lub [programu Visual Studio 2013][VSUlt]
* [Zestaw Azure SDK dla platformy .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Aktywną subskrypcją Microsoft Azure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB
W tym samouczku założono, że utworzono maszynę wirtualną na platformie Azure. Po utworzeniu maszyny wirtualnej należy zainstalować bazy danych MongoDB na maszynie wirtualnej:

* Aby utworzyć maszynę wirtualną systemu Windows i zainstaluj bazę danych MongoDB, zobacz [MongoDB zainstalować na maszynie wirtualnej z systemem Windows Server na platformie Azure][InstallMongoOnWindowsVM].

Po utworzeniu maszyny wirtualnej na platformie Azure i zainstalowane bazy danych MongoDB, należy koniecznie pamiętać nazwy DNS maszyny wirtualnej ("testlinuxvm.cloudapp.net", na przykład) i porcie zewnętrznym bazy danych mongodb, który określono w punkcie końcowym.  Należy w dalszej części tego samouczka.

<a id="createapp"></a>

## <a name="create-the-application"></a>Tworzenie aplikacji
W tej sekcji utworzysz aplikację ASP.NET przy użyciu programu Visual Studio o nazwie "My listy zadań" i wykonać początkowe wdrożenie do aplikacji sieci Web usługi aplikacji Azure. Uruchomisz aplikację lokalnie, ale będzie połączyć się z maszyną wirtualną na platformie Azure i używać utworzone wystąpienie bazy danych MongoDB.

1. W programie Visual Studio, kliknij przycisk **nowy projekt**.
   
    ![Nowy projekt strony][StartPageNewProject]
2. W **nowy projekt** oknie, w okienku po lewej stronie wybierz **Visual C#**, a następnie wybierz **sieci Web**. W środkowym okienku wybierz **aplikacji sieci Web ASP.NET**. Na dole nazwy projektu "MyTaskListApp", a następnie kliknij przycisk **OK**.
   
    ![Okno dialogowe Nowy projekt][NewProjectMyTaskListApp]
3. W **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC**, a następnie kliknij przycisk **OK**.
   
    ![Wybierz szablon MVC][VS2013SelectMVCTemplate]
4. Jeśli nie jest już zarejestrowany w Microsoft Azure, pojawi się monit do logowania. Postępuj zgodnie z monitami, aby zalogować się do platformy Azure.
5. Gdy użytkownik jest zalogowany, możesz rozpocząć konfigurowanie aplikacji sieci web usługi aplikacji. Określ **Nazwa aplikacji sieci Web**, **planu usługi aplikacji**, **grupy zasobów**, i **Region**, następnie kliknij przycisk **Utwórz**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Po zakończeniu tworzenia projektu, poczekaj, aż aplikacji sieci web mogą być tworzone w usłudze Azure App Service, jak wskazano w **działanie usługi Azure App Service** okna. Następnie kliknij przycisk **MyTaskListApp opublikować tę aplikację sieci Web**.
7. Kliknij przycisk **Opublikuj**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Po opublikowaniu aplikacji ASP.NET domyślnej aplikacji sieci Web usługi aplikacji Azure zostanie uruchomiona w przeglądarce.

## <a name="install-the-mongodb-c-driver"></a>Instalacja sterownika bazy danych MongoDB C#
Bazy danych MongoDB oferuje obsługę po stronie klienta dla aplikacji C# za pośrednictwem sterownika, który należy zainstalować na komputerze deweloperskim lokalnego. Sterownik C# jest dostępny za pośrednictwem pakietu NuGet.

Aby zainstalować sterownik bazy danych MongoDB C#:

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **MyTaskListApp** projekt i wybierz **Zarządzanie NuGetPackages**.
   
    ![Zarządzaj pakietami NuGet][VS2013ManageNuGetPackages]
2. W **Zarządzaj pakietami NuGet** okna, w okienku po lewej stronie kliknij **Online**. W **wyszukiwania Online** polu po prawej stronie, wpisz "mongodb.driver".  Kliknij przycisk **zainstalować** do zainstalowania sterownika.
   
    ![Wyszukaj bazy danych MongoDB C# sterownika][SearchforMongoDBCSharpDriver]
3. Kliknij przycisk **akceptuję** do akceptowania 10gen, Inc. licencyjnych.
4. Kliknij przycisk **Zamknij** po sterownik został zainstalowany.
    ![Bazy danych MongoDB C# sterownik zainstalowany][MongoDBCsharpDriverInstalled]

Obecnie jest zainstalowany sterownik bazy danych MongoDB C#.  Odwołuje się do **MongoDB.Bson**, **MongoDB.Driver**, i **MongoDB.Driver.Core** biblioteki zostały dodane do projektu.

![Odwołania do bazy danych MongoDB C# sterownika][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Dodaj model
W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *modele* folderu i **Dodaj** nowy **klasy** i nadaj mu nazwę *TaskModel.cs*.  W *TaskModel.cs*, Zastąp istniejący kod następującym kodem:

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

## <a name="add-the-data-access-layer"></a>Dodaj Warstwa dostępu do danych
W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *MyTaskListApp* projektu i **Dodaj** **nowy Folder** o nazwie *DAL*.  Kliknij prawym przyciskiem myszy *DAL* folderu i **Dodaj** nowy **klasy**. Nazwa pliku klasy *Dal.cs*.  W *Dal.cs*, Zastąp istniejący kod następującym kodem:

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

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
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

            // Creates a Task and inserts it into the collection in MongoDB.
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
Otwórz *Controllers\HomeController.cs* w pliku **Eksploratora rozwiązań** i Zastąp istniejący kod następującym kodem:

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

## <a name="set-up-the-styles"></a>Ustawianie stylów
Aby zmienić tytuł w górnej części strony, otwórz *Views\Shared\\_Layout.cshtml* w pliku **Eksploratora rozwiązań** i zastąp "Nazwa aplikacji" w nagłówku pasek nawigacyjny "Moja aplikacja listy zadań", aby wygląda następująco:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Aby skonfigurować menu listy zadań, należy otworzyć *\Views\Home\Index.cshtml* plików i zastąpić istniejący kod następującym kodem:

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


Aby dodać możliwość tworzenia nowego zadania, kliknij prawym przyciskiem myszy *Views\Home\\*  folderu i **Dodaj** **widoku**.  Nazwa widoku *Utwórz*. Zastąp kod z następujących czynności:

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

## <a name="set-the-mongodb-connection-string"></a>Ustawianie parametrów połączenia bazy danych MongoDB
W **Eksploratora rozwiązań**, otwórz *DAL/Dal.cs* pliku. Znajdź następujący wiersz kodu:

    private string connectionString = "mongodb://<vm-dns-name>";

Zastąp `<vm-dns-name>` o nazwie DNS maszyny wirtualnej uruchomionej bazy danych MongoDB utworzony w [Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB] [ Create a virtual machine and install MongoDB] kroku w tym samouczku.  Aby znaleźć nazwę DNS maszyny wirtualnej, przejdź do portalu Azure, wybierz **maszyn wirtualnych**i Znajdź **nazwy DNS**.

Jeśli nazwa DNS maszyny wirtualnej to "testlinuxvm.cloudapp.net" i bazy danych MongoDB nasłuchuje na porcie domyślnym 27017, będzie wyglądać wiersz kodu ciąg połączenia:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Jeśli punkt końcowy maszyny wirtualnej określa innego portu zewnętrznego bazy danych mongodb, możesz zmiennoprzecinkową portu w parametrach połączenia:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Aby uzyskać więcej informacji dotyczących parametrów połączenia bazy danych MongoDB, zobacz [połączeń][MongoConnectionStrings].

## <a name="test-the-local-deployment"></a>Testowanie wdrożenia lokalnego
Aby uruchomić aplikację na komputerze deweloperskim, zaznacz **Rozpocznij debugowanie** z **debugowania** menu lub naciśnij klawisz **F5**. Usługi IIS Express uruchamia i przeglądarki zostanie otwarty i uruchamia strony głównej aplikacji.  Możesz dodać nowe zadanie, które zostaną dodane do bazy danych MongoDB przeprowadzana na maszynie wirtualnej na platformie Azure.

![Moja aplikacja listy zadań][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a>Publikowanie aplikacji sieci Web usługi aplikacji Azure
W tej sekcji zostanie Opublikuj zmiany do aplikacji sieci Web usługi aplikacji Azure.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MyTaskListApp** ponownie i kliknij przycisk **publikowania**.
2. Kliknij przycisk **Opublikuj**.
   
    Powinna zostać wyświetlona aplikacja sieci web uruchomionych w usłudze Azure App Service i uzyskiwania dostępu do bazy danych MongoDB w maszynach wirtualnych platformy Azure.

## <a name="summary"></a>Podsumowanie
Teraz zostały pomyślnie wdrożone aplikacje sieci Web usługi aplikacji Azure przez aplikację ASP.NET. Aby wyświetlić aplikację sieci web:

1. Zaloguj się do portalu Azure.
2. Kliknij przycisk **Web apps**. 
3. Wybierz aplikację sieci web w **aplikacje sieci Web** listy.

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
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
