---
title: "Interfejs API DB aaaUse Azure rozwiązania Cosmos dla bazy danych MongoDB toobuild aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Samouczek bazy danych Azure rozwiązania Cosmos, który tworzy aplikacji sieci web bazy danych w trybie online za pomocą interfejsu API hello bazy danych mongodb."
keywords: "Przykłady bazy danych mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="b4f5a-104">Azure DB rozwiązania Cosmos: Łączenie aplikacji bazy danych MongoDB tooa przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b4f5a-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="b4f5a-105">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b4f5a-106">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b4f5a-107">Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure i sposobu hello toocreate bazy danych i kolekcji toostore danych za pomocą [API bazy danych MongoDB](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4f5a-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="b4f5a-108">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b4f5a-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4f5a-109">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b4f5a-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="b4f5a-110">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="b4f5a-110">Update your connection string</span></span>
> * <span data-ttu-id="b4f5a-111">Tworzenie aplikacji bazy danych MongoDB na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b4f5a-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="b4f5a-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="b4f5a-112">Create a database account</span></span>

<span data-ttu-id="b4f5a-113">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="b4f5a-114">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="b4f5a-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="b4f5a-115">Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="b4f5a-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="b4f5a-116">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="b4f5a-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="b4f5a-117">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b4f5a-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="b4f5a-118">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b4f5a-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="b4f5a-119">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="b4f5a-119">Update your connection string</span></span>

1. <span data-ttu-id="b4f5a-120">W portalu Azure w hello hello **bazy danych Azure rozwiązania Cosmos** wybierz hello API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="b4f5a-121">Na pasku po lewej stronie powitania hello konta bloku, kliknij przycisk **szybki start**.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="b4f5a-122">Wybierz platformy (*sterownik .NET*, *sterownika Node.js*, *powłoki MongoDB*, *sterownika Java*, *Python sterownik*).</span><span class="sxs-lookup"><span data-stu-id="b4f5a-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="b4f5a-123">Jeśli nie widzisz z sterownika lub narzędzia wymienione, nie martw się, firma Microsoft stale dokumentu więcej wstawki kodu połączenia.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="b4f5a-124">Skopiuj i Wklej hello fragment kodu w aplikacji bazy danych MongoDB, i są gotowe toogo.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="b4f5a-125">Konfigurowanie aplikacji bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="b4f5a-125">Set up your MongoDB app</span></span>

<span data-ttu-id="b4f5a-126">Można użyć hello [tworzenie aplikacji sieci web na platformie Azure, łączącego tooMongoDB uruchomione na maszynie wirtualnej](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) samouczek z minimalnym modyfikacji, tooquickly instalacji aplikacji bazy danych MongoDB (albo lokalnie lub tooan opublikowanej aplikacji sieci web platformy Azure) który łączy z interfejsu API tooan dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="b4f5a-127">Czynności opisane w samouczku hello, z jedną modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="b4f5a-128">Zastąp kod Dal.cs hello to:</span><span class="sxs-lookup"><span data-stu-id="b4f5a-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
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
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
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
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="b4f5a-129">Modyfikowanie hello następujące zmienne w pliku Dal.cs hello na ustawienia konta ze strony klucze hello w hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="b4f5a-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="b4f5a-130">Użycie aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b4f5a-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="b4f5a-131">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="b4f5a-131">Clean up resources</span></span>

<span data-ttu-id="b4f5a-132">Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="b4f5a-133">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b4f5a-134">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4f5a-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4f5a-135">Next steps</span></span>

<span data-ttu-id="b4f5a-136">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b4f5a-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4f5a-137">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b4f5a-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="b4f5a-138">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="b4f5a-138">Update your connection string</span></span>
> * <span data-ttu-id="b4f5a-139">Tworzenie aplikacji bazy danych MongoDB na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b4f5a-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="b4f5a-140">Można kontynuować toohello następny samouczek i zaimportować tooAzure danych z bazy danych MongoDB DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b4f5a-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4f5a-141">Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b4f5a-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

