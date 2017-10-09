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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure DB rozwiązania Cosmos: Łączenie aplikacji bazy danych MongoDB tooa przy użyciu platformy .NET

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure i sposobu hello toocreate bazy danych i kolekcji toostore danych za pomocą [API bazy danych MongoDB](mongodb-introduction.md). 

Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Cosmos DB 
> * Aktualizowanie parametrów połączenia
> * Tworzenie aplikacji bazy danych MongoDB na maszynie wirtualnej 


## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.  

> [!TIP]
> * Masz już konto bazy danych rozwiązania Cosmos Azure? Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)
> * Czy miał konto usługi Azure DocumentDB? Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).  
> * Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

1. W portalu Azure w hello hello **bazy danych Azure rozwiązania Cosmos** wybierz hello API dla konta bazy danych MongoDB. 
2. Na pasku po lewej stronie powitania hello konta bloku, kliknij przycisk **szybki start**. 
3. Wybierz platformy (*sterownik .NET*, *sterownika Node.js*, *powłoki MongoDB*, *sterownika Java*, *Python sterownik*). Jeśli nie widzisz z sterownika lub narzędzia wymienione, nie martw się, firma Microsoft stale dokumentu więcej wstawki kodu połączenia. 
4. Skopiuj i Wklej hello fragment kodu w aplikacji bazy danych MongoDB, i są gotowe toogo.

## <a name="set-up-your-mongodb-app"></a>Konfigurowanie aplikacji bazy danych MongoDB

Można użyć hello [tworzenie aplikacji sieci web na platformie Azure, łączącego tooMongoDB uruchomione na maszynie wirtualnej](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) samouczek z minimalnym modyfikacji, tooquickly instalacji aplikacji bazy danych MongoDB (albo lokalnie lub tooan opublikowanej aplikacji sieci web platformy Azure) który łączy z interfejsu API tooan dla konta bazy danych MongoDB.  

1. Czynności opisane w samouczku hello, z jedną modyfikacji.  Zastąp kod Dal.cs hello to:

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

2. Modyfikowanie hello następujące zmienne w pliku Dal.cs hello na ustawienia konta ze strony klucze hello w hello portalu Azure:

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Użycie aplikacji hello!

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure. 

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Cosmos DB 
> * Aktualizowanie parametrów połączenia
> * Tworzenie aplikacji bazy danych MongoDB na maszynie wirtualnej

Można kontynuować toohello następny samouczek i zaimportować tooAzure danych z bazy danych MongoDB DB rozwiązania Cosmos.  

> [!div class="nextstepaction"]
> [Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB](mongodb-migrate.md)

