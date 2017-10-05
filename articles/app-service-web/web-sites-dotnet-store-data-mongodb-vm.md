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
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="41a55-103">Tworzenie aplikacji sieci Web na platformie Azure, która łączy się z bazą danych MongoDB uruchomioną na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="41a55-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="41a55-104">Przy użyciu narzędzia Git, można wdrożyć aplikację ASP.NET do aplikacji sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="41a55-105">W tym samouczku utworzysz prosty frontonu ASP.NET MVC aplikację listy zadań, która nawiązuje połączenie z bazą danych MongoDB uruchomione na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="41a55-106">[Bazy danych MongoDB] [ MongoDB] jest popularnych typu open source, bazy danych NoSQL o wysokiej wydajności.</span><span class="sxs-lookup"><span data-stu-id="41a55-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="41a55-107">Po uruchomione i testowania aplikacji programu ASP.NET na komputerze deweloperskim, możesz przekazać aplikację do aplikacji usługi sieci Web aplikacji przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="41a55-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="41a55-108">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="41a55-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="41a55-109">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="41a55-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="41a55-110">Tło wiedzy</span><span class="sxs-lookup"><span data-stu-id="41a55-110">Background knowledge</span></span>
<span data-ttu-id="41a55-111">Znajomość następujące przydaje się w tym samouczku, ale nie wymagane:</span><span class="sxs-lookup"><span data-stu-id="41a55-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="41a55-112">C# sterownik bazy danych mongodb.</span><span class="sxs-lookup"><span data-stu-id="41a55-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="41a55-113">Aby uzyskać więcej informacji dotyczących tworzenia aplikacji C# dla bazy danych MongoDB, zobacz MongoDB [Center języka CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="41a55-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="41a55-114">Platforma aplikacji sieci web ASP .NET.</span><span class="sxs-lookup"><span data-stu-id="41a55-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="41a55-115">Dowiedz się, wszystkie dotyczące go w [witryny sieci Web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="41a55-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="41a55-116">Platforma aplikacji sieci web ASP .NET MVC.</span><span class="sxs-lookup"><span data-stu-id="41a55-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="41a55-117">Dowiedz się, wszystkie dotyczące go w [witryny sieci Web platformy ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="41a55-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="41a55-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-118">Azure.</span></span> <span data-ttu-id="41a55-119">Można rozpocząć odczytywanie na [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="41a55-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a55-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="41a55-120">Prerequisites</span></span>
* <span data-ttu-id="41a55-121">[Program Visual Studio Express 2013 for Web] [ VSEWeb] lub [programu Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="41a55-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="41a55-122">Zestaw Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="41a55-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="41a55-123">Aktywną subskrypcją Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="41a55-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="41a55-124">Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="41a55-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="41a55-125">W tym samouczku założono, że utworzono maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="41a55-126">Po utworzeniu maszyny wirtualnej należy zainstalować bazy danych MongoDB na maszynie wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="41a55-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="41a55-127">Aby utworzyć maszynę wirtualną systemu Windows i zainstaluj bazę danych MongoDB, zobacz [MongoDB zainstalować na maszynie wirtualnej z systemem Windows Server na platformie Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="41a55-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="41a55-128">Po utworzeniu maszyny wirtualnej na platformie Azure i zainstalowane bazy danych MongoDB, należy koniecznie pamiętać nazwy DNS maszyny wirtualnej ("testlinuxvm.cloudapp.net", na przykład) i porcie zewnętrznym bazy danych mongodb, który określono w punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="41a55-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="41a55-129">Należy w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="41a55-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="41a55-130">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="41a55-130">Create the application</span></span>
<span data-ttu-id="41a55-131">W tej sekcji utworzysz aplikację ASP.NET przy użyciu programu Visual Studio o nazwie "My listy zadań" i wykonać początkowe wdrożenie do aplikacji sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="41a55-132">Uruchomisz aplikację lokalnie, ale będzie połączyć się z maszyną wirtualną na platformie Azure i używać utworzone wystąpienie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="41a55-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="41a55-133">W programie Visual Studio, kliknij przycisk **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="41a55-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Nowy projekt strony][StartPageNewProject]
2. <span data-ttu-id="41a55-135">W **nowy projekt** oknie, w okienku po lewej stronie wybierz **Visual C#**, a następnie wybierz **sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="41a55-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="41a55-136">W środkowym okienku wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="41a55-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="41a55-137">Na dole nazwy projektu "MyTaskListApp", a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41a55-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Okno dialogowe Nowy projekt][NewProjectMyTaskListApp]
3. <span data-ttu-id="41a55-139">W **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41a55-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Wybierz szablon MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="41a55-141">Jeśli nie jest już zarejestrowany w Microsoft Azure, pojawi się monit do logowania.</span><span class="sxs-lookup"><span data-stu-id="41a55-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="41a55-142">Postępuj zgodnie z monitami, aby zalogować się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="41a55-143">Gdy użytkownik jest zalogowany, możesz rozpocząć konfigurowanie aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a55-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="41a55-144">Określ **Nazwa aplikacji sieci Web**, **planu usługi aplikacji**, **grupy zasobów**, i **Region**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="41a55-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="41a55-145">Po zakończeniu tworzenia projektu, poczekaj, aż aplikacji sieci web mogą być tworzone w usłudze Azure App Service, jak wskazano w **działanie usługi Azure App Service** okna.</span><span class="sxs-lookup"><span data-stu-id="41a55-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="41a55-146">Następnie kliknij przycisk **MyTaskListApp opublikować tę aplikację sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="41a55-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="41a55-147">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="41a55-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="41a55-148">Po opublikowaniu aplikacji ASP.NET domyślnej aplikacji sieci Web usługi aplikacji Azure zostanie uruchomiona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="41a55-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="41a55-149">Instalacja sterownika bazy danych MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="41a55-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="41a55-150">Bazy danych MongoDB oferuje obsługę po stronie klienta dla aplikacji C# za pośrednictwem sterownika, który należy zainstalować na komputerze deweloperskim lokalnego.</span><span class="sxs-lookup"><span data-stu-id="41a55-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="41a55-151">Sterownik C# jest dostępny za pośrednictwem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="41a55-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="41a55-152">Aby zainstalować sterownik bazy danych MongoDB C#:</span><span class="sxs-lookup"><span data-stu-id="41a55-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="41a55-153">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **MyTaskListApp** projekt i wybierz **Zarządzanie NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="41a55-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Zarządzaj pakietami NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="41a55-155">W **Zarządzaj pakietami NuGet** okna, w okienku po lewej stronie kliknij **Online**.</span><span class="sxs-lookup"><span data-stu-id="41a55-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="41a55-156">W **wyszukiwania Online** polu po prawej stronie, wpisz "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="41a55-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="41a55-157">Kliknij przycisk **zainstalować** do zainstalowania sterownika.</span><span class="sxs-lookup"><span data-stu-id="41a55-157">Click **Install** to install the driver.</span></span>
   
    ![Wyszukaj bazy danych MongoDB C# sterownika][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="41a55-159">Kliknij przycisk **akceptuję** do akceptowania 10gen, Inc. licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="41a55-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="41a55-160">Kliknij przycisk **Zamknij** po sterownik został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="41a55-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="41a55-161">![Bazy danych MongoDB C# sterownik zainstalowany][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="41a55-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="41a55-162">Obecnie jest zainstalowany sterownik bazy danych MongoDB C#.</span><span class="sxs-lookup"><span data-stu-id="41a55-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="41a55-163">Odwołuje się do **MongoDB.Bson**, **MongoDB.Driver**, i **MongoDB.Driver.Core** biblioteki zostały dodane do projektu.</span><span class="sxs-lookup"><span data-stu-id="41a55-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Odwołania do bazy danych MongoDB C# sterownika][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="41a55-165">Dodaj model</span><span class="sxs-lookup"><span data-stu-id="41a55-165">Add a model</span></span>
<span data-ttu-id="41a55-166">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *modele* folderu i **Dodaj** nowy **klasy** i nadaj mu nazwę *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="41a55-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="41a55-167">W *TaskModel.cs*, Zastąp istniejący kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="41a55-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="41a55-168">Dodaj Warstwa dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="41a55-168">Add the data access layer</span></span>
<span data-ttu-id="41a55-169">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *MyTaskListApp* projektu i **Dodaj** **nowy Folder** o nazwie *DAL*.</span><span class="sxs-lookup"><span data-stu-id="41a55-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="41a55-170">Kliknij prawym przyciskiem myszy *DAL* folderu i **Dodaj** nowy **klasy**.</span><span class="sxs-lookup"><span data-stu-id="41a55-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="41a55-171">Nazwa pliku klasy *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="41a55-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="41a55-172">W *Dal.cs*, Zastąp istniejący kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="41a55-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="41a55-173">Dodawanie kontrolera</span><span class="sxs-lookup"><span data-stu-id="41a55-173">Add a controller</span></span>
<span data-ttu-id="41a55-174">Otwórz *Controllers\HomeController.cs* w pliku **Eksploratora rozwiązań** i Zastąp istniejący kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="41a55-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="41a55-175">Ustawianie stylów</span><span class="sxs-lookup"><span data-stu-id="41a55-175">Set up the styles</span></span>
<span data-ttu-id="41a55-176">Aby zmienić tytuł w górnej części strony, otwórz *Views\Shared\\_Layout.cshtml* w pliku **Eksploratora rozwiązań** i zastąp "Nazwa aplikacji" w nagłówku pasek nawigacyjny "Moja aplikacja listy zadań", aby wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="41a55-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="41a55-177">Aby skonfigurować menu listy zadań, należy otworzyć *\Views\Home\Index.cshtml* plików i zastąpić istniejący kod następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="41a55-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="41a55-178">Aby dodać możliwość tworzenia nowego zadania, kliknij prawym przyciskiem myszy *Views\Home\\*  folderu i **Dodaj** **widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a55-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="41a55-179">Nazwa widoku *Utwórz*.</span><span class="sxs-lookup"><span data-stu-id="41a55-179">Name the view *Create*.</span></span> <span data-ttu-id="41a55-180">Zastąp kod z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="41a55-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="41a55-181">**Eksplorator rozwiązań** powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="41a55-181">**Solution Explorer** should look like this:</span></span>

![Eksplorator rozwiązań][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="41a55-183">Ustawianie parametrów połączenia bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="41a55-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="41a55-184">W **Eksploratora rozwiązań**, otwórz *DAL/Dal.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="41a55-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="41a55-185">Znajdź następujący wiersz kodu:</span><span class="sxs-lookup"><span data-stu-id="41a55-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="41a55-186">Zastąp `<vm-dns-name>` o nazwie DNS maszyny wirtualnej uruchomionej bazy danych MongoDB utworzony w [Utwórz maszynę wirtualną i zainstaluj bazę danych MongoDB] [ Create a virtual machine and install MongoDB] kroku w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="41a55-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="41a55-187">Aby znaleźć nazwę DNS maszyny wirtualnej, przejdź do portalu Azure, wybierz **maszyn wirtualnych**i Znajdź **nazwy DNS**.</span><span class="sxs-lookup"><span data-stu-id="41a55-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="41a55-188">Jeśli nazwa DNS maszyny wirtualnej to "testlinuxvm.cloudapp.net" i bazy danych MongoDB nasłuchuje na porcie domyślnym 27017, będzie wyglądać wiersz kodu ciąg połączenia:</span><span class="sxs-lookup"><span data-stu-id="41a55-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="41a55-189">Jeśli punkt końcowy maszyny wirtualnej określa innego portu zewnętrznego bazy danych mongodb, możesz zmiennoprzecinkową portu w parametrach połączenia:</span><span class="sxs-lookup"><span data-stu-id="41a55-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="41a55-190">Aby uzyskać więcej informacji dotyczących parametrów połączenia bazy danych MongoDB, zobacz [połączeń][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="41a55-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="41a55-191">Testowanie wdrożenia lokalnego</span><span class="sxs-lookup"><span data-stu-id="41a55-191">Test the local deployment</span></span>
<span data-ttu-id="41a55-192">Aby uruchomić aplikację na komputerze deweloperskim, zaznacz **Rozpocznij debugowanie** z **debugowania** menu lub naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="41a55-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="41a55-193">Usługi IIS Express uruchamia i przeglądarki zostanie otwarty i uruchamia strony głównej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a55-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="41a55-194">Możesz dodać nowe zadanie, które zostaną dodane do bazy danych MongoDB przeprowadzana na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Moja aplikacja listy zadań][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="41a55-196">Publikowanie aplikacji sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="41a55-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="41a55-197">W tej sekcji zostanie Opublikuj zmiany do aplikacji sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="41a55-198">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MyTaskListApp** ponownie i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="41a55-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="41a55-199">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="41a55-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="41a55-200">Powinna zostać wyświetlona aplikacja sieci web uruchomionych w usłudze Azure App Service i uzyskiwania dostępu do bazy danych MongoDB w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="41a55-201">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="41a55-201">Summary</span></span>
<span data-ttu-id="41a55-202">Teraz zostały pomyślnie wdrożone aplikacje sieci Web usługi aplikacji Azure przez aplikację ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="41a55-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="41a55-203">Aby wyświetlić aplikację sieci web:</span><span class="sxs-lookup"><span data-stu-id="41a55-203">To view the web app:</span></span>

1. <span data-ttu-id="41a55-204">Zaloguj się do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="41a55-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="41a55-205">Kliknij przycisk **Web apps**.</span><span class="sxs-lookup"><span data-stu-id="41a55-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="41a55-206">Wybierz aplikację sieci web w **aplikacje sieci Web** listy.</span><span class="sxs-lookup"><span data-stu-id="41a55-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="41a55-207">Aby uzyskać więcej informacji dotyczących tworzenia aplikacji C# dla bazy danych MongoDB, zobacz [Center języka CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="41a55-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
