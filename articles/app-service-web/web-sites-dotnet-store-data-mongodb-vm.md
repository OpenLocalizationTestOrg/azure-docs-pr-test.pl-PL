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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="66721-103">Tworzenie aplikacji sieci web na platformie Azure, łączącego tooMongoDB uruchomione na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="66721-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="66721-104">Przy użyciu narzędzia Git, można wdrożyć tooAzure aplikacji ASP.NET aplikacji usługi sieci Web aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66721-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="66721-105">W tym samouczku utworzysz prosty frontonu ASP.NET MVC aplikacji listy zadań, która łączy bazy danych MongoDB tooa uruchomione na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="66721-106">[Bazy danych MongoDB] [ MongoDB] jest popularnych typu open source, bazy danych NoSQL o wysokiej wydajności.</span><span class="sxs-lookup"><span data-stu-id="66721-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="66721-107">Po uruchomione i testowanie aplikacji ASP.NET hello na komputerze deweloperskim, przekaże tooApp aplikacji hello usługi aplikacje sieci Web przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="66721-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="66721-108">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="66721-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="66721-109">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="66721-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="66721-110">Tło wiedzy</span><span class="sxs-lookup"><span data-stu-id="66721-110">Background knowledge</span></span>
<span data-ttu-id="66721-111">Wiedzę na temat następujących hello jest przydatne w tym samouczku, ale nie wymagane:</span><span class="sxs-lookup"><span data-stu-id="66721-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="66721-112">Sterownik Hello C# dla bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="66721-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="66721-113">Aby uzyskać więcej informacji na temat tworzenia aplikacji C# dla bazy danych MongoDB, zobacz hello bazy danych MongoDB [Center języka CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="66721-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="66721-114">Witaj platforma aplikacji sieci web ASP .NET.</span><span class="sxs-lookup"><span data-stu-id="66721-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="66721-115">Dowiedz się, wszystkie dotyczące go na powitania [witryny sieci Web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="66721-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="66721-116">platforma aplikacji sieci web ASP .NET MVC Hello.</span><span class="sxs-lookup"><span data-stu-id="66721-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="66721-117">Dowiedz się, wszystkie dotyczące go na powitania [witryny sieci Web platformy ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="66721-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="66721-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-118">Azure.</span></span> <span data-ttu-id="66721-119">Można rozpocząć odczytywanie na [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="66721-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66721-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="66721-120">Prerequisites</span></span>
* <span data-ttu-id="66721-121">[Program Visual Studio Express 2013 for Web] [ VSEWeb] lub [programu Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="66721-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="66721-122">Zestaw Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="66721-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="66721-123">Aktywną subskrypcją Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="66721-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="66721-124">Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="66721-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="66721-125">W tym samouczku założono, że utworzono maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="66721-126">Po utworzeniu maszyny wirtualnej hello należy tooinstall bazy danych MongoDB na maszynie wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="66721-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="66721-127">toocreate maszyny wirtualnej systemu Windows i Instalacja bazy danych MongoDB, zobacz [MongoDB zainstalować na maszynie wirtualnej z systemem Windows Server na platformie Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="66721-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="66721-128">Po utworzeniu maszyny wirtualnej hello na platformie Azure i zainstalowane bazy danych MongoDB, być czy tooremember hello nazwą DNS hello maszyny wirtualnej ("testlinuxvm.cloudapp.net", na przykład) i porcie zewnętrznym hello bazy danych mongodb, określona w hello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="66721-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="66721-129">Należy w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="66721-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="66721-130">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="66721-130">Create hello application</span></span>
<span data-ttu-id="66721-131">W tej sekcji utworzysz aplikację ASP.NET przy użyciu programu Visual Studio o nazwie "My listy zadań" i wykonać tooAzure początkowe wdrożenie aplikacji usługi sieci Web aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66721-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="66721-132">Aplikacja hello zostaną uruchomione lokalnie, ale zostanie połączyć tooyour maszyny wirtualnej na platformie Azure i używać utworzone wystąpienie bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="66721-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="66721-133">W programie Visual Studio, kliknij przycisk **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="66721-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Nowy projekt strony][StartPageNewProject]
2. <span data-ttu-id="66721-135">W hello **nowy projekt** oknie w lewym okienku hello, wybierz opcję **Visual C#**, a następnie wybierz **sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="66721-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="66721-136">W środkowym okienku hello, wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="66721-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="66721-137">U dołu hello nazwy projektu "MyTaskListApp", a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="66721-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Okno dialogowe Nowy projekt][NewProjectMyTaskListApp]
3. <span data-ttu-id="66721-139">W hello **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="66721-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Wybierz szablon MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="66721-141">Jeśli nie jest już zarejestrowany w Microsoft Azure, będzie zostanie wyświetlony monit o toosign w.</span><span class="sxs-lookup"><span data-stu-id="66721-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="66721-142">Wykonaj toosign monity hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="66721-143">Gdy użytkownik jest zalogowany, możesz rozpocząć konfigurowanie aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66721-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="66721-144">Określ hello **Nazwa aplikacji sieci Web**, **planu usługi aplikacji**, **grupy zasobów**, i **Region**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="66721-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="66721-145">Po zakończeniu tworzenia projektu hello, poczekaj, aż toobe aplikacji sieci web hello utworzone w usłudze Azure App Service, wskazane hello **działanie usługi Azure App Service** okna.</span><span class="sxs-lookup"><span data-stu-id="66721-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="66721-146">Następnie kliknij przycisk **teraz opublikować MyTaskListApp toothis aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="66721-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="66721-147">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="66721-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="66721-148">Gdy domyślnej aplikacji ASP.NET jest tooAzure opublikowanej aplikacji usługi sieci Web aplikacji, zostanie uruchomiony w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="66721-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="66721-149">Zainstaluj hello sterownik bazy danych MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="66721-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="66721-150">Bazy danych MongoDB oferuje obsługę po stronie klienta dla aplikacji C# za pośrednictwem sterownika, który należy tooinstall na komputerze deweloperskim lokalnego.</span><span class="sxs-lookup"><span data-stu-id="66721-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="66721-151">Witaj C# sterownik jest dostępny za pośrednictwem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="66721-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="66721-152">Witaj tooinstall sterownik bazy danych MongoDB C#:</span><span class="sxs-lookup"><span data-stu-id="66721-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="66721-153">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **MyTaskListApp** projekt i wybierz **Zarządzanie NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="66721-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Zarządzaj pakietami NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="66721-155">W hello **Zarządzaj pakietami NuGet** okna, w okienku po lewej stronie powitania kliknij **Online**.</span><span class="sxs-lookup"><span data-stu-id="66721-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="66721-156">W hello **wyszukiwania Online** pole na powitania prawo, wpisz "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="66721-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="66721-157">Kliknij przycisk **zainstalować** tooinstall hello sterownika.</span><span class="sxs-lookup"><span data-stu-id="66721-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Wyszukaj bazy danych MongoDB C# sterownika][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="66721-159">Kliknij przycisk **akceptuję** tooaccept hello 10gen, Inc. postanowienia licencyjne.</span><span class="sxs-lookup"><span data-stu-id="66721-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="66721-160">Kliknij przycisk **Zamknij** po hello sterownik został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="66721-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="66721-161">![Bazy danych MongoDB C# sterownik zainstalowany][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="66721-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="66721-162">Witaj sterownik bazy danych MongoDB C# jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="66721-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="66721-163">Odwołania toohello **MongoDB.Bson**, **MongoDB.Driver**, i **MongoDB.Driver.Core** biblioteki zostały dodane toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="66721-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Odwołania do bazy danych MongoDB C# sterownika][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="66721-165">Dodaj model</span><span class="sxs-lookup"><span data-stu-id="66721-165">Add a model</span></span>
<span data-ttu-id="66721-166">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy *modele* folderu i **Dodaj** nowy **klasy** i nadaj mu nazwę *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="66721-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="66721-167">W *TaskModel.cs*, Zamień istniejący kod hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="66721-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="66721-168">Dodaj Warstwa dostępu do danych hello</span><span class="sxs-lookup"><span data-stu-id="66721-168">Add hello data access layer</span></span>
<span data-ttu-id="66721-169">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello *MyTaskListApp* projektu i **Dodaj** **nowy Folder** o nazwie *DAL*.</span><span class="sxs-lookup"><span data-stu-id="66721-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="66721-170">Kliknij prawym przyciskiem myszy hello *DAL* folderu i **Dodaj** nowy **klasy**.</span><span class="sxs-lookup"><span data-stu-id="66721-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="66721-171">Nazwa pliku klasy hello *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="66721-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="66721-172">W *Dal.cs*, Zamień istniejący kod hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="66721-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="66721-173">Dodawanie kontrolera</span><span class="sxs-lookup"><span data-stu-id="66721-173">Add a controller</span></span>
<span data-ttu-id="66721-174">Otwórz hello *Controllers\HomeController.cs* w pliku **Eksploratora rozwiązań** i Zastąp istniejący kod hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="66721-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="66721-175">Ustawianie stylów hello</span><span class="sxs-lookup"><span data-stu-id="66721-175">Set up hello styles</span></span>
<span data-ttu-id="66721-176">toochange hello tytuł u góry hello hello strony, otwórz hello *Views\Shared\\_Layout.cshtml* w pliku **Eksploratora rozwiązań** i zastąp "Nazwa aplikacji" w nagłówku pasek nawigacyjny hello "Moje zadania Lista aplikacji", aby wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="66721-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="66721-177">W kolejności tooset hello listy zadań menu, otwórz hello *\Views\Home\Index.cshtml* plików i Zastąp istniejący kod hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="66721-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="66721-178">tooadd hello możliwości toocreate nowe zadanie, kliknij prawym przyciskiem myszy hello *Views\Home\\*  folderu i **Dodaj** **widoku**.</span><span class="sxs-lookup"><span data-stu-id="66721-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="66721-179">Nazwa widoku hello *Utwórz*.</span><span class="sxs-lookup"><span data-stu-id="66721-179">Name hello view *Create*.</span></span> <span data-ttu-id="66721-180">Zastąp kod hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="66721-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="66721-181">**Eksplorator rozwiązań** powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="66721-181">**Solution Explorer** should look like this:</span></span>

![Eksplorator rozwiązań][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="66721-183">Ustawianie parametrów połączenia bazy danych MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="66721-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="66721-184">W **Eksploratora rozwiązań**, otwórz hello *DAL/Dal.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="66721-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="66721-185">Znajdź hello po wierszu kodu:</span><span class="sxs-lookup"><span data-stu-id="66721-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="66721-186">Zastąp `<vm-dns-name>` o nazwie DNS hello hello maszynę wirtualną działającą bazy danych MongoDB utworzony w hello [Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB] [ Create a virtual machine and install MongoDB] kroku w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="66721-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="66721-187">Nazwa DNS hello toofind maszynę wirtualną, przejdź toohello portalu Azure, wybierz **maszyn wirtualnych**i Znajdź **nazwy DNS**.</span><span class="sxs-lookup"><span data-stu-id="66721-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="66721-188">Jeśli nazwa DNS hello hello maszyny wirtualnej to "testlinuxvm.cloudapp.net" i bazy danych MongoDB nasłuchuje na porcie domyślnym hello 27017, będzie wyglądać hello połączenia ciąg wiersz kodu:</span><span class="sxs-lookup"><span data-stu-id="66721-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="66721-189">Jeśli hello punktu końcowego maszyny wirtualnej określa innego portu zewnętrznego bazy danych mongodb, możesz zmiennoprzecinkową hello portu w parametrach połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="66721-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="66721-190">Aby uzyskać więcej informacji dotyczących parametrów połączenia bazy danych MongoDB, zobacz [połączeń][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="66721-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="66721-191">Testowanie wdrażania lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="66721-191">Test hello local deployment</span></span>
<span data-ttu-id="66721-192">Wybierz aplikację na komputerze deweloperskim toorun **Rozpocznij debugowanie** z hello **debugowania** menu lub naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="66721-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="66721-193">Usługi IIS Express uruchamia i przeglądarki zostanie otwarty i uruchamia strony głównej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="66721-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="66721-194">Możesz dodać nowe zadanie, którego będzie można dodać bazy danych MongoDB toohello uruchomione na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Moja aplikacja listy zadań][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="66721-196">Publikowanie aplikacji sieci Web usługi aplikacji tooAzure</span><span class="sxs-lookup"><span data-stu-id="66721-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="66721-197">W tej sekcji zostanie opublikowany tooAzure Twojego zmian aplikacji sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="66721-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="66721-198">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MyTaskListApp** ponownie i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="66721-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="66721-199">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="66721-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="66721-200">Powinna zostać wyświetlona aplikacja sieci web uruchomionych w usłudze Azure App Service i uzyskiwania dostępu do bazy danych MongoDB hello w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="66721-201">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="66721-201">Summary</span></span>
<span data-ttu-id="66721-202">TooAzure aplikacji programu ASP.NET aplikacji usługi sieci Web aplikacji teraz zostały pomyślnie wdrożone.</span><span class="sxs-lookup"><span data-stu-id="66721-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="66721-203">tooview hello aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="66721-203">tooview hello web app:</span></span>

1. <span data-ttu-id="66721-204">Zaloguj się do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="66721-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="66721-205">Kliknij przycisk **Web apps**.</span><span class="sxs-lookup"><span data-stu-id="66721-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="66721-206">Wybierz aplikację sieci web w hello **aplikacje sieci Web** listy.</span><span class="sxs-lookup"><span data-stu-id="66721-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="66721-207">Aby uzyskać więcej informacji dotyczących tworzenia aplikacji C# dla bazy danych MongoDB, zobacz [Center języka CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="66721-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
