---
<span data-ttu-id="e3b1d-101">title: aaa "bazy danych Azure rozwiązania Cosmos: tworzenie aplikacji konsoli API bazy danych MongoDB z Golang i hello portalu Azure | Opis Microsoft Docs": przedstawia przykładowy kod Golang, można użyć tooconnect tooand wykonać kwerendy w usługach Azure rozwiązania Cosmos DB: Autor db rozwiązania cosmos: Durgaprasad Budhwani Menedżera: Edytor jhubbard: mimig1</span><span class="sxs-lookup"><span data-stu-id="e3b1d-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="e3b1d-102">MS.Service: db rozwiązania cosmos ms.topic: artykuł bohater ms.date: ms.author 2017-07/21: mimig</span><span class="sxs-lookup"><span data-stu-id="e3b1d-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="e3b1d-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji konsoli API bazy danych MongoDB z Golang i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e3b1d-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="e3b1d-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e3b1d-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="e3b1d-106">Przedstawiono to szybki start jak toouse istniejące [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) aplikacji napisanych w [Golang](https://golang.org/) i podłącz go bazy danych Azure DB rozwiązania Cosmos tooyour, która obsługuje połączenia klienta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="e3b1d-107">Innymi słowy aplikacja Golang tylko wie, że nawiązuje połączenie tooa bazy danych przy użyciu interfejsów API bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="e3b1d-108">Jest niewidoczne toohello aplikacji hello dane są przechowywane w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3b1d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e3b1d-109">Prerequisites</span></span>

- <span data-ttu-id="e3b1d-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-110">An Azure subscription.</span></span> <span data-ttu-id="e3b1d-111">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="e3b1d-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="e3b1d-112">[Przejdź](https://golang.org/dl/) oraz podstawową wiedzę na temat hello [Przejdź](https://golang.org/) języka.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="e3b1d-113">Środowisko IDE — [Gogland](https://www.jetbrains.com/go/) firmy Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) firmy Microsoft lub [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="e3b1d-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="e3b1d-114">W tym samouczku używam środowiska Goglang.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="e3b1d-115">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="e3b1d-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="e3b1d-116">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3b1d-116">Clone hello sample application</span></span>

<span data-ttu-id="e3b1d-117">Klonowanie hello przykładową aplikację i zainstaluj hello wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="e3b1d-118">Utwórz folder o nazwie CosmosDBSample znajdujące się w folderze GOROOT\src hello, czyli C:\Go\ domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="e3b1d-119">Uruchom następujące polecenia, używając okno terminalu git np. git bash tooclone hello próbki repozytorium do folderu CosmosDBSample hello hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="e3b1d-120">Uruchom następujące polecenie tooget hello mgo pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="e3b1d-121">Hello [mgo](http://labix.org/mgo) sterownika (Wymowa jako *mango*) jest [MongoDB](http://www.mongodb.org/) sterownik hello [Przejdź języka](http://golang.org/) implementuje wzbogaconej i również testowane Wybór funkcji w obszarze bardzo prosty interfejs API następujące standardowe idioms Go.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="e3b1d-122">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="e3b1d-122">Update your connection string</span></span>

<span data-ttu-id="e3b1d-123">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="e3b1d-124">Kliknij przycisk **szybki start** w hello menu nawigacji po lewej stronie, a następnie kliknij przycisk **innych** tooview hello ciągu połączenia wymagane przez hello Przejdź aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="e3b1d-125">W Goglang Otwórz plik main.go hello w katalogu GOROOT\CosmosDBSample hello i zaktualizuj hello następujące wiersze kodu za pomocą hello ciągu połączenia z hello portalu Azure, jak pokazano w powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="e3b1d-126">Nazwa bazy danych Hello jest prefiksem hello hello **hosta** wartość w okienku ciąg połączenia portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="e3b1d-127">Dla konta hello pokazano na poniższym obrazie hello hello Nazwa bazy danych jest szkolić golang.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Szybki start okienku karta inne w hello Azure przedstawiający portalu hello ciągu połączenia](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="e3b1d-129">Zapisz plik main.go hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="e3b1d-130">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="e3b1d-130">Review hello code</span></span>

<span data-ttu-id="e3b1d-131">Upewnijmy szybki przegląd co dzieje się w pliku main.go hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="e3b1d-132">Łączenie hello tooAzure aplikacji przejdź DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="e3b1d-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="e3b1d-133">Azure DB rozwiązania Cosmos obsługuje hello włączony protokół SSL bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="e3b1d-134">tooan tooconnect MongoDB włączony protokół SSL, należy toodefine hello **DialServer** działać w [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)i użycie hello [tls. *Wybierania* ](http://golang.org/pkg/crypto/tls#Dial) funkcji tooperform hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="e3b1d-135">Witaj następującego fragmentu kodu Golang łączy hello aplikacji przejdź z interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="e3b1d-136">Witaj *DialInfo* klasa przechowuje opcje do ustanowienia sesji z klastra bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="e3b1d-137">Witaj **mgo. Dial()** metoda jest używana w przypadku braku połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="e3b1d-138">Dla połączeń SSL, hello **mgo. DialWithInfo()** wymagana jest metoda.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="e3b1d-139">Wystąpienie hello **{} DialWIthInfo** obiekt jest używany toocreate hello sesji.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="e3b1d-140">Po ustanowieniu sesji hello, aby dostęp do kolekcji hello za pomocą następującego fragmentu kodu hello:</span><span class="sxs-lookup"><span data-stu-id="e3b1d-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="e3b1d-141">Tworzenie dokumentu</span><span class="sxs-lookup"><span data-stu-id="e3b1d-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="e3b1d-142">Wykonywanie zapytania o dokument lub jego odczytywanie</span><span class="sxs-lookup"><span data-stu-id="e3b1d-142">Query or read a document</span></span>

<span data-ttu-id="e3b1d-143">Usługa Azure Cosmos DB obsługuje zaawansowane zapytania o dokumenty JSON przechowywane w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="e3b1d-144">Witaj następujący przykładowy kod przedstawia zapytanie, które można uruchomić względem dokumentów hello w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="e3b1d-145">Aktualizowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="e3b1d-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="e3b1d-146">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="e3b1d-146">Delete a document</span></span>

<span data-ttu-id="e3b1d-147">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="e3b1d-148">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e3b1d-148">Run hello app</span></span>

1. <span data-ttu-id="e3b1d-149">W Goglang, upewnij się, że Twoje GOPATH (dostępnych w ramach **pliku**, **ustawienia**, **Przejdź**, **GOPATH**) należą: Lokalizacja hello w których hello gopkg został zainstalowany, która jest USERPROFILE\go domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="e3b1d-150">Komentarz hello wierszy, które usunąć hello dokumentu, linie 91 96, dzięki czemu można wyświetlić dokumentu powitania po uruchomionej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="e3b1d-151">W środowisku Goglang kliknij pozycję **Run** (Uruchom), a następnie kliknij pozycję **Run 'Build main.go and run'** (Uruchom „Skompiluj plik main.go i uruchom”).</span><span class="sxs-lookup"><span data-stu-id="e3b1d-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="e3b1d-152">Aplikacja Hello zakończeniu i wyświetla opis hello dokumentu hello utworzona w [Utwórz dokument](#create-document).</span><span class="sxs-lookup"><span data-stu-id="e3b1d-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang przedstawiający hello dane wyjściowe aplikacji hello](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="e3b1d-154">Przeglądanie dokumentu w Eksploratorze danych</span><span class="sxs-lookup"><span data-stu-id="e3b1d-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="e3b1d-155">Przejdź wstecz toohello toosee portalu Azure w Eksploratorze danych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="e3b1d-156">Kliknij przycisk **Eksploratora danych (wersja zapoznawcza)** w menu nawigacji po lewej stronie powitania, rozwiń węzeł **szkolić golang**, **pakietu**, a następnie kliknij przycisk **dokumenty**.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="e3b1d-157">W hello **dokumenty** , kliknij pozycję hello \_identyfikator toodisplay hello dokumentu w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Dokument hello nowo utworzony przedstawiający Eksploratora danych](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="e3b1d-159">Możesz pracować z wbudowanym dokumentu hello i kliknij przycisk **aktualizacji** toosave go.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="e3b1d-160">Można również usunąć hello dokumentu lub tworzenie nowych dokumentów lub zapytań.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="e3b1d-161">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e3b1d-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e3b1d-162">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="e3b1d-162">Clean up resources</span></span>

<span data-ttu-id="e3b1d-163">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e3b1d-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="e3b1d-164">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="e3b1d-165">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3b1d-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3b1d-166">Next steps</span></span>

<span data-ttu-id="e3b1d-167">W tym szybkiego startu kiedy znasz już jak toocreate konta bazy danych Azure rozwiązania Cosmos i uruchomić aplikację Golang przy użyciu hello interfejsu API dla bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="e3b1d-168">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="e3b1d-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3b1d-169">Importowanie danych do bazy danych Azure rozwiązania Cosmos dla hello API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="e3b1d-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
