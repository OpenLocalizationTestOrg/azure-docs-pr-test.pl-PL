---
title: "Programowanie JavaScript po stronie aaaServer dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toowrite bazy danych Azure rozwiązania Cosmos toouse procedury składowane, wyzwalacze bazy danych i funkcje zdefiniowane przez użytkownika (UDF) w języku JavaScript. Pobierz porady programing bazy danych i inne."
keywords: "Wyzwalacze bazy danych, procedury składowanej, procedury składowanej, program bazy danych, sproc, documentdb, azure, platformy Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="af1fb-105">Programowanie po stronie serwera w usłudze Azure DB rozwiązania Cosmos: procedury składowane, wyzwalacze bazy danych i funkcji UDF</span><span class="sxs-lookup"><span data-stu-id="af1fb-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="af1fb-106">Dowiedz się, jak zintegrować języka Azure rozwiązania Cosmos DB, transakcyjne wykonywanie kodu JavaScript umożliwia deweloperom pisanie **procedur składowanych**, **wyzwalaczy** i **funkcje zdefiniowane przez użytkownika** natywnie w [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af1fb-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="af1fb-107">Dzięki temu toowrite bazy danych programu aplikacji logiki, które mogą być dostarczane i wykonywane bezpośrednio na powitania bazy danych magazynu partycji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="af1fb-108">Zaleca się wprowadzenie uruchomione przez oglądaniu powitania po wideo, gdzie Andrew Liu zapewnia model programowania po stronie serwera bazy danych tooCosmos krótkie wprowadzenie dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="af1fb-109">Następnie wróć toothis artykułu, w którym poznasz toohello odpowiedzi hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="af1fb-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="af1fb-110">Jak zapisać procedury składowanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika przy użyciu języka JavaScript?</span><span class="sxs-lookup"><span data-stu-id="af1fb-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="af1fb-111">Sposób rozwiązania Cosmos DB zagwarantować kwasu?</span><span class="sxs-lookup"><span data-stu-id="af1fb-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="af1fb-112">Jak działają transakcji w bazie danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="af1fb-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="af1fb-113">Co to są wstępnie wyzwala i jest wyzwalane po i jak jedną zapisać?</span><span class="sxs-lookup"><span data-stu-id="af1fb-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="af1fb-114">Jak zarejestrować i wykonać procedury przechowywanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika w sposób RESTful za pośrednictwem protokołu HTTP?</span><span class="sxs-lookup"><span data-stu-id="af1fb-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="af1fb-115">Co rozwiązania Cosmos SDK bazy danych są dostępne toocreate i wykonywanie przechowywanych procedur, wyzwalaczy i funkcji UDF?</span><span class="sxs-lookup"><span data-stu-id="af1fb-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="af1fb-116">Wprowadzenie tooStored procedury i programowania funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="af1fb-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="af1fb-117">To podejście *"JavaScript jako nowoczesnego dzień T-SQL"* zwalnia deweloperzy aplikacji od złożoności hello niezgodności typu systemu i technologii mapowania relacyjnego obiektu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="af1fb-118">Ponadto wprowadzono szereg korzyści wewnętrzne, które mogą być wykorzystywane toobuild rozbudowanych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="af1fb-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="af1fb-119">**Logika proceduralna:** JavaScript jako wysokiego poziomu języka programowania, zapewnia tooexpress interfejs zaawansowanych, znanych logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="af1fb-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="af1fb-120">Można wykonywać złożonych sekwencji operacji bliżej toohello danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="af1fb-121">**Niepodzielne transakcji:** gwarancje rozwiązania Cosmos bazy danych, które bazy danych operacji wewnątrz jednej procedury składowanej lub wyzwalacza są atomic.</span><span class="sxs-lookup"><span data-stu-id="af1fb-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="af1fb-122">Dzięki temu aplikacja łączy pokrewnych operacje w pojedynczej partii, dzięki czemu wszystkie z nich poprawne albo żadna z nich powiodło się.</span><span class="sxs-lookup"><span data-stu-id="af1fb-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="af1fb-123">**Wydajność:** hello na fakt, że JSON jest system typów języka Javascript leżą zamapowanych toohello i jest również hello podstawowa jednostka przestrzeni dyskowej w bazie danych rozwiązania Cosmos umożliwia kilka optymalizacji, takich jak opóźnieniem materialization o JSON dokumentów w buforze hello Pula i nadawania dostępne toohello na żądanie wykonywanie kodu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="af1fb-124">Istnieje więcej korzyści wydajności związanych z wysyłanie bazy danych toohello logiki biznesowej:</span><span class="sxs-lookup"><span data-stu-id="af1fb-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="af1fb-125">Przetwarzanie wsadowe — deweloperzy mogą grupy operacje, takie jak wstawia i przesyłanie ich zbiorczo.</span><span class="sxs-lookup"><span data-stu-id="af1fb-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="af1fb-126">Opóźnienie ruchu sieci Hello kosztów i zmniejszone hello magazynu narzutów toocreate oddzielne transakcje.</span><span class="sxs-lookup"><span data-stu-id="af1fb-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="af1fb-127">Wstępna kompilacja — rozwiązania Cosmos DB precompiles procedur składowanych, wyzwalaczy i tooavoid funkcje zdefiniowane przez użytkownika koszt kompilacji języka JavaScript dla każdego wywołania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="af1fb-128">Witaj koszty tworzenia kodu bajtowego hello jest logiki procedurach hello amortyzowanego tooa minimalnej wartości.</span><span class="sxs-lookup"><span data-stu-id="af1fb-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="af1fb-129">Sekwencjonowanie — wiele operacji potrzeby efekt uboczny ("wyzwalacza") która potencjalnie obejmuje wykonanie jednej lub wielu operacji dodatkowej magazynu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="af1fb-130">Jako uzupełnienie niepodzielność, to wydajność więcej po przeniesieniu toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="af1fb-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="af1fb-131">**Hermetyzacja:** przechowywane procedury mogą być używane toogroup logiki biznesowej w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="af1fb-132">Daje to dwie następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="af1fb-132">This has two advantages:</span></span>
  * <span data-ttu-id="af1fb-133">Dodaje warstwy abstrakcji na powitania nieprzetworzone dane, co umożliwia ich aplikacji niezależnie od danych hello tooevolve architektów danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="af1fb-134">Jest to szczególnie korzystne w przypadku, gdy dane hello przynależy schematu, powodu toohello łamliwa założeń, które może być konieczne toobe rozszerzania do aplikacji hello, jeśli mają bezpośrednio toodeal z danymi.</span><span class="sxs-lookup"><span data-stu-id="af1fb-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="af1fb-135">Ta warstwa abstrakcji pozwala chronić swoje dane usprawnienie dostępu hello ze skryptów hello przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="af1fb-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="af1fb-136">Witaj tworzenia i uruchamiania wyzwalaczy bazy danych, procedury składowane i operatory zapytań niestandardowych jest obsługiwany za pośrednictwem hello [interfejsu API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), i [zestawówSDKklienta](documentdb-sdk-dotnet.md) na wielu platformach, w tym .NET, Node.js oraz JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af1fb-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="af1fb-137">W tym samouczku używana hello [Node.js SDK z ze zobowiązania Q](http://azure.github.io/azure-documentdb-node-q/) tooillustrate składni i użycia procedur składowanych, wyzwalaczy i funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="af1fb-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="af1fb-138">Procedury składowane</span><span class="sxs-lookup"><span data-stu-id="af1fb-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="af1fb-139">Przykład: Napisać prosty procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="af1fb-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="af1fb-140">Zacznijmy od prostego procedury przechowywanej, która zwraca odpowiedź "Hello World".</span><span class="sxs-lookup"><span data-stu-id="af1fb-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="af1fb-141">Procedury składowane są rejestrowane w jednej kolekcji i może działać na dokumentów i załączników w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="af1fb-142">Hello poniższy fragment kodu przedstawia sposób tooregister hello helloWorld przechowywane procedury z kolekcją.</span><span class="sxs-lookup"><span data-stu-id="af1fb-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="af1fb-143">Po zarejestrowaniu hello przechowywane procedury możemy ją wykonać hello kolekcji i przeczytaj wyniki hello zwrotnego na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="af1fb-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="af1fb-144">Obiekt kontekstu Hello zapewnia dostęp tooall operacje, które można wykonywać w dyskowej rozwiązania Cosmos bazy danych, a także uzyskiwać dostęp do obiektów toohello żądań i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="af1fb-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="af1fb-145">W takim przypadku użyliśmy hello obiektu tooset hello treść odpowiedzi hello odpowiedzi, która została wysłana wstecz toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="af1fb-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="af1fb-146">Aby uzyskać więcej informacji, zobacz toohello [serwera Azure rozwiązania Cosmos DB JavaScript dokumentacji zestawu SDK](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="af1fb-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="af1fb-147">Daj nam rozwiń w tym przykładzie i dodać więcej bazy danych związanych z nimi funkcji toohello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="af1fb-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="af1fb-148">Procedury składowane można tworzenie, aktualizowanie, odczytu, zapytania i usuwać dokumenty i załączniki wewnątrz hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="af1fb-149">Przykład: Napisania toocreate procedury składowanej dokumentu</span><span class="sxs-lookup"><span data-stu-id="af1fb-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="af1fb-150">fragment dalej Hello pokazuje, jak toouse hello toointeract obiektu kontekstu z zasobami DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="af1fb-151">Tę procedurę składowaną przyjmuje jako documentToCreate wejściowych, treści hello toobe dokumentu, utworzone w bieżącej kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="af1fb-152">Wszystkie operacje są asynchroniczne i zależą od wywołania zwrotne funkcji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af1fb-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="af1fb-153">Funkcja wywołania zwrotnego Hello ma dwa parametry: jeden dla obiekt błędu hello w przypadku, gdy operacja hello kończy się niepowodzeniem i jeden dla hello utworzony obiekt.</span><span class="sxs-lookup"><span data-stu-id="af1fb-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="af1fb-154">Wewnątrz wywołania zwrotnego hello użytkowników można obsłużyć wyjątek hello lub zgłosić błąd.</span><span class="sxs-lookup"><span data-stu-id="af1fb-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="af1fb-155">W przypadku, gdy wywołanie zwrotne nie zostanie podana, i występuje błąd, hello Azure DB rozwiązania Cosmos w czasie wykonywania zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="af1fb-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="af1fb-156">W powyższym przykładzie hello wywołania zwrotnego hello zgłasza błąd, jeśli hello operacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="af1fb-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="af1fb-157">W przeciwnym razie Ustawia identyfikator hello hello dokument utworzony jako treść hello hello odpowiedzi toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="af1fb-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="af1fb-158">Oto, jak wykonaniem tej procedury składowanej z parametrami wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="af1fb-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="af1fb-159">Należy pamiętać, że procedurę składowaną można zmodyfikowanych tootake tablicę treści dokumentu jako dane wejściowe i je utworzyć w hello sam przechowywane procedury wykonywania zamiast wielu sieci żądań toocreate ich osobno.</span><span class="sxs-lookup"><span data-stu-id="af1fb-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="af1fb-160">Może to być używane tooimplement importer zbiorczego wydajne rozwiązania Cosmos bazy danych (omówiony w dalszej części tego samouczka).</span><span class="sxs-lookup"><span data-stu-id="af1fb-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="af1fb-161">przykład Witaj opisane przedstawiono, jak toouse procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="af1fb-162">Później w samouczku hello omówimy wyzwalaczy i funkcji zdefiniowanych przez użytkownika (UDF).</span><span class="sxs-lookup"><span data-stu-id="af1fb-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="af1fb-163">Transakcji w bazie danych programu</span><span class="sxs-lookup"><span data-stu-id="af1fb-163">Database program transactions</span></span>
<span data-ttu-id="af1fb-164">Transakcji w typowej bazy danych można zdefiniować jako sekwencja operacji wykonywanych jako pojedyncza jednostka logiczna pracy.</span><span class="sxs-lookup"><span data-stu-id="af1fb-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="af1fb-165">Udostępnia każdą transakcję **ACID gwarancje**.</span><span class="sxs-lookup"><span data-stu-id="af1fb-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="af1fb-166">KWAS jest dobrze znanego akronim, zawiera cztery właściwości — niepodzielność, spójności, izolacji i trwałości.</span><span class="sxs-lookup"><span data-stu-id="af1fb-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="af1fb-167">Krótko mówiąc, niepodzielność gwarantuje, że wszystkie hello pracy wewnątrz transakcji jest traktowany jako pojedyncza jednostka gdzie albo wszystkie dba lub none.</span><span class="sxs-lookup"><span data-stu-id="af1fb-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="af1fb-168">Spójności upewnia się, że hello dane są zawsze w dobrym stanie wewnętrznego na przez transakcje.</span><span class="sxs-lookup"><span data-stu-id="af1fb-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="af1fb-169">Izolacja gwarantuje, że żadne transakcje dwóch koliduje ze sobą — ogólnie rzecz biorąc, większość komercyjnych systemów zapewniają wiele poziomów izolacji, które mogą być używane zgodnie z wymaganiami aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="af1fb-170">Trwałość zapewnia żadnych zmian, które zostaje zatwierdzona w bazie danych hello zawsze będzie obecne.</span><span class="sxs-lookup"><span data-stu-id="af1fb-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="af1fb-171">W bazie danych rozwiązania Cosmos, JavaScript jest hostowana na powitania tej samej przestrzeni pamięci jako hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="af1fb-172">W związku z tym żądań w ramach procedury składowane i wyzwalaczy wykonywany w hello sam zakresem sesji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="af1fb-173">Dzięki temu DB rozwiązania Cosmos tooguarantee kwasu dla wszystkich operacji, które są częścią jednego procedury składowanej/wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="af1fb-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="af1fb-174">Należy wziąć pod uwagę następujące hello przechowywane Definicja procedury:</span><span class="sxs-lookup"><span data-stu-id="af1fb-174">Consider hello following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="af1fb-175">Tę procedurę składowaną używa transakcji w elementach tootrade aplikacji gier, między dwóch graczy w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="af1fb-176">Witaj przechowywane procedury prób tooread dwa dokumenty, które gracz toohello odpowiednie identyfikatory przekazany jako argument.</span><span class="sxs-lookup"><span data-stu-id="af1fb-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="af1fb-177">Jeśli oba dokumenty player zostaną znalezione, następnie hello przechowywane procedury aktualizacji hello dokumentów przez zamianę ich elementów.</span><span class="sxs-lookup"><span data-stu-id="af1fb-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="af1fb-178">Jeśli nie zostaną napotkane błędy wzdłuż sposób hello, zgłasza wyjątek JavaScript, która niejawnie przerywa hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="af1fb-179">Jeśli hello kolekcji hello przechowywane procedury został zarejestrowany przed to kolekcja jednej partycji, a następnie hello transakcji jest zakresem tooall hello dokumentów w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="af1fb-180">Jeśli kolekcja hello jest podzielona na partycje, procedury składowane są wykonywane w zakresie transakcji hello klucza jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="af1fb-181">Każdy składowanych, wykonywanie procedury następnie musi zawierać wartość klucza partycji odpowiedniej toohello zakresu hello transakcji musi być uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="af1fb-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="af1fb-182">Aby uzyskać więcej informacji, zobacz [Azure rozwiązania Cosmos DB partycjonowania](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="af1fb-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="af1fb-183">Przekazywania i wycofywania</span><span class="sxs-lookup"><span data-stu-id="af1fb-183">Commit and rollback</span></span>
<span data-ttu-id="af1fb-184">Transakcje są głęboko i natywnie zintegrowane model programowania JavaScript DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="af1fb-185">Wewnątrz funkcji JavaScript wszystkie operacje są automatycznie zawijany w ramach jednej transakcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="af1fb-186">Jeśli hello JavaScript zostaje ukończona bez żadnych wyjątków, bazy danych toohello operacji hello są zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="af1fb-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="af1fb-187">W efekcie instrukcje "BEGIN TRANSACTION" i "COMMIT TRANSACTION" hello w relacyjnych baz danych są niejawne w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="af1fb-188">W przypadku dowolnego wyjątek, który jest propagowana ze skryptu hello środowiska wykonawczego języka JavaScript DB rozwiązania Cosmos cofnie hello cała transakcja.</span><span class="sxs-lookup"><span data-stu-id="af1fb-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="af1fb-189">Jak pokazano wcześniej hello przykład generowania wyjątku jest skutecznie równoważne tooa "ROLLBACK TRANSACTION" w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="af1fb-190">Spójność danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-190">Data consistency</span></span>
<span data-ttu-id="af1fb-191">Procedury składowane i wyzwalaczy są zawsze wykonywane na hello repliki podstawowej hello Azure DB rozwiązania Cosmos kontenera.</span><span class="sxs-lookup"><span data-stu-id="af1fb-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="af1fb-192">Dzięki temu, że odczyty z wewnątrz przechowywane procedury oferta wysoki poziom spójności.</span><span class="sxs-lookup"><span data-stu-id="af1fb-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="af1fb-193">Zapytania przy użyciu funkcji zdefiniowanych przez użytkownika mogą być wykonywane na powitania podstawowe lub pomocnicze repliki, ale Upewniamy się toomeet hello żądanego poziomu spójności, wybierając odpowiednie repliki hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="af1fb-194">Ograniczonego wykonania</span><span class="sxs-lookup"><span data-stu-id="af1fb-194">Bounded execution</span></span>
<span data-ttu-id="af1fb-195">Wszystkie operacje rozwiązania Cosmos bazy danych należy wykonać w ramach serwera hello określony limit czasu żądania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="af1fb-196">To ograniczenie dotyczy również funkcje tooJavaScript (procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="af1fb-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="af1fb-197">Jeśli operacja nie została zakończona z limitem czasu, hello transakcja zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="af1fb-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="af1fb-198">Funkcje kodu JavaScript musi zakończyć się przed upływem limitu czasu hello, lub zaimplementuj kontynuacji na podstawie modelu toobatch/wznawia wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="af1fb-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="af1fb-199">W kolejności toosimplify programowanie przechowywanych procedur i wyzwalaczy toohandle terminów, wszystkie funkcje w obiekcie kolekcji hello (dla tworzenia, odczytu, zastępowanie i usuwanie dokumentów i załączników) zwracają wartość logiczna, która reprezentuje czy który Operacja zostanie wykonana.</span><span class="sxs-lookup"><span data-stu-id="af1fb-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="af1fb-200">Jeśli ta wartość wynosi false, to wskazanie, że limit czasu hello o tooexpire i tą procedurą hello musi dobiega końca wykonywania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="af1fb-201">Pierwszy operacji magazynu niezaakceptowanych operacji w kolejce toohello wcześniejsze dotrą toocomplete, jeśli procedura przechowywana hello jest przeprowadzany w czasie i więcej żądań w kolejce.</span><span class="sxs-lookup"><span data-stu-id="af1fb-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="af1fb-202">JavaScript — funkcje są również ograniczona zużycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="af1fb-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="af1fb-203">Rozwiązania cosmos DB rezerwuje przepływności na kolekcję na podstawie rozmiaru hello zainicjowano obsługę administracyjną konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="af1fb-204">Przepływność wyrażonych znormalizowane jednostki Procesora, pamięci i wywołać jednostki żądania lub RUs zużycie we/wy.</span><span class="sxs-lookup"><span data-stu-id="af1fb-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="af1fb-205">Funkcje kodu JavaScript potencjalnie może zużywać dużą liczbę RUs w krótkim czasie i mogą zostać ograniczony szybkość po osiągnięciu limitu hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="af1fb-206">Procedury składowane znacznym zasobów może być również dostępność poddane kwarantannie tooensure operacji w bazie danych pierwotnych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="af1fb-207">Przykład: Zbiorcze importowanie danych do programu bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="af1fb-208">Poniżej przedstawiono przykład procedury przechowywanej, która jest zapisywane dokumenty toobulk importu do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="af1fb-209">Uwaga jak hello przechowywane procedury uchwytów ograniczonego wykonania sprawdzając hello Boolean wartość zwracana z createDocument, a następnie używa hello liczbę dokumentów dodaje w każdym wywołaniu hello przechowywane procedury postępu tootrack i Wznów w partiach.</span><span class="sxs-lookup"><span data-stu-id="af1fb-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="af1fb-210"><a id="trigger"></a>Wyzwalacze bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="af1fb-211">Wyzwalacze wstępne bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-211">Database pre-triggers</span></span>
<span data-ttu-id="af1fb-212">Rozwiązania cosmos DB udostępnia wyzwalacze, które są wykonywane lub wyzwolone przez operację na dokument.</span><span class="sxs-lookup"><span data-stu-id="af1fb-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="af1fb-213">Na przykład można określić wstępne wyzwalacza, podczas tworzenia dokumentu — wstępne wyzwalacz zostanie uruchomiony przed utworzeniem hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="af1fb-214">Witaj poniżej przedstawiono przykładowy sposób wstępnego Wyzwalacze mogą być używane toovalidate hello właściwości dokumentu, który jest tworzony:</span><span class="sxs-lookup"><span data-stu-id="af1fb-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="af1fb-215">I hello odpowiadającego kodu Node.js rejestracji po stronie klienta dla wyzwalacza hello:</span><span class="sxs-lookup"><span data-stu-id="af1fb-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="af1fb-216">Wstępne wyzwalaczy nie może mieć parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="af1fb-217">Obiekt żądania Hello może być komunikat żądania hello używane toomanipulate skojarzony z hello operacji.</span><span class="sxs-lookup"><span data-stu-id="af1fb-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="af1fb-218">W tym miejscu wyzwalacza wstępne hello jest uruchamiana z hello tworzenia dokumentu i treści komunikatu żądania hello zawiera toobe dokumentu hello utworzony w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="af1fb-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="af1fb-219">Gdy wyzwalacze są zarejestrowane, użytkownicy mogą określić hello operacje, które można uruchomić z.</span><span class="sxs-lookup"><span data-stu-id="af1fb-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="af1fb-220">Wyzwalacz został utworzony z TriggerOperation.Create, co oznacza, że następujące hello jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="af1fb-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="af1fb-221">Wyzwalacze po bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-221">Database post-triggers</span></span>
<span data-ttu-id="af1fb-222">Po wyzwalaczy, takich jak wstępne wyzwalacze są skojarzone z operacji w dokumencie i nie przyjmuje żadnych parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="af1fb-223">Zakres ich działania **po** hello operacja została zakończona i mają dostęp toohello odpowiedzi wysyłany komunikat toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="af1fb-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="af1fb-224">Hello poniższy przykład przedstawia po Wyzwalacze w akcji:</span><span class="sxs-lookup"><span data-stu-id="af1fb-224">hello following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="af1fb-225">jak pokazano w hello następujące przykładowe można zarejestrować Hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="af1fb-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="af1fb-226">Wyzwalacz wysyła zapytanie hello dokument metadanych i aktualizuje ze szczegółami hello nowo utworzonego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="af1fb-227">Rzecz, istotne hello jest toonote **transakcyjnych** wykonanie wyzwalaczy w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="af1fb-228">Po wyzwalacz uruchamia hello w ramach jednej transakcji, jak tworzenie hello hello oryginalnego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="af1fb-229">W związku z tym jeśli z powitania po wyzwalacza (jeśli są nam dokument metadanych hello tooupdate powiedzieć) firma Microsoft zgłosić wyjątek, cała transakcja hello zakończy się niepowodzeniem i wycofana.</span><span class="sxs-lookup"><span data-stu-id="af1fb-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="af1fb-230">Dokument nie zostanie utworzona i zostanie zwrócony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="af1fb-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="af1fb-231"><a id="udf"></a>Funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="af1fb-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="af1fb-232">Funkcje zdefiniowane przez użytkownika (UDF) są gramatyki języka zapytań SQL usługi DocumentDB interfejsu API hello tooextend używane i implementować niestandardowe reguły biznesowe.</span><span class="sxs-lookup"><span data-stu-id="af1fb-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="af1fb-233">Mogą one wywołać tylko z wewnątrz zapytań.</span><span class="sxs-lookup"><span data-stu-id="af1fb-233">They can only be called from inside queries.</span></span> <span data-ttu-id="af1fb-234">Nie mają obiektu context toohello dostępu i mają toobe używany jako tylko do obliczeń JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af1fb-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="af1fb-235">W związku z tym funkcje UDF może działać w replikach pomocniczych hello usługi DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="af1fb-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="af1fb-236">Hello poniższy przykład tworzy UDF toocalculate podatkowych oparte na szybkości dla różnych nawiasy przychodów, a następnie używa on wewnątrz toofind zapytania wszystkich osób, które płatnej ponad 20 000 $ w podatki.</span><span class="sxs-lookup"><span data-stu-id="af1fb-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="af1fb-237">Witaj UDF później mogą być używane w zapytaniach, podobnie jak w hello następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="af1fb-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="af1fb-238">Zapytanie o języku zintegrowanym JavaScript API</span><span class="sxs-lookup"><span data-stu-id="af1fb-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="af1fb-239">Ponadto tooissuing zapytania przy użyciu gramatyki SQL usługi DocumentDB, hello po stronie serwera SDK pozwala tooperform zoptymalizowanych pod kątem zapytań przy użyciu interfejs fluent JavaScript bez żadnych wiedzy programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af1fb-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="af1fb-240">Hello JavaScript zapytania interfejsu API pozwala tooprogrammatically kompilacji zapytań przez przekazanie funkcji predykatu w funkcji chainable wywołuje built-ins tablicy i popularnych bibliotek JavaScript, takich jak lodash składni znanych tooECMAScript5 firmy.</span><span class="sxs-lookup"><span data-stu-id="af1fb-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="af1fb-241">Zapytania są analizowane przez toobe środowiska wykonawczego języka JavaScript hello wykonywane efektywne wykorzystanie indeksów Azure rozwiązania Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="af1fb-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="af1fb-242">`__`(o podwójnej precyzji podkreślenie) jest zbyt alias`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="af1fb-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="af1fb-243">Innymi słowy, można użyć `__` lub `getContext().getCollection()` tooaccess hello JavaScript API zapytania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="af1fb-244">Obsługiwane funkcje obejmują:</span><span class="sxs-lookup"><span data-stu-id="af1fb-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="af1fb-245">
<b>Chain().... wartość ([wywołania zwrotnego] [, opcje])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-246">Rozpoczyna się value() od łańcuchowa wywołanie, które musi zostać zakończone.</span><span class="sxs-lookup"><span data-stu-id="af1fb-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-247">
<b>Filtr (predicateFunction [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-248">Filtruje hello wejściowych przy użyciu funkcji predykatu, która zwraca wartość PRAWDA/FAŁSZ w kolejności toofilter dokumentów wejściowych we/wy na powitania Wynikowy zestaw.</span><span class="sxs-lookup"><span data-stu-id="af1fb-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="af1fb-249">Działa to podobnie tooa klauzuli WHERE instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="af1fb-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-250">
<b>mapy (transformationFunction [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-251">Stosuje projekcji podane przekształcenia, która mapuje każdego elementu wejściowego tooa JavaScript obiektu lub wartości.</span><span class="sxs-lookup"><span data-stu-id="af1fb-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="af1fb-252">To zachowanie podobne tooa klauzuli SELECT w języku SQL.</span><span class="sxs-lookup"><span data-stu-id="af1fb-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-253">
<b>pluck ([propertyName] [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-254">Jest to skrót do mapy, który wyodrębni hello wartość właściwości jednego z każdego elementu wejściowego.</span><span class="sxs-lookup"><span data-stu-id="af1fb-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-255">
<b>spłaszczanie ([isShallow] [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-256">Łączy i spłaszcza tablic z każdego elementu wejściowego w pojedynczą tablicę tooa.</span><span class="sxs-lookup"><span data-stu-id="af1fb-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="af1fb-257">Podobne tooSelectMany w składniku LINQ to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="af1fb-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-258">
<b>sortBy ([predicate] [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-259">Tworzy nowy zestaw dokumentów, sortując hello dokumentów w strumieniu dokument wejściowy hello rosnąco przy użyciu hello danego predykatu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="af1fb-260">To zachowanie podobne tooa klauzuli ORDER BY w języku SQL.</span><span class="sxs-lookup"><span data-stu-id="af1fb-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="af1fb-261">
<b>sortByDescending ([predicate] [, opcje] [, wywołania zwrotnego])</b>
</span><span class="sxs-lookup"><span data-stu-id="af1fb-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="af1fb-262">Tworzy nowy zestaw dokumentów, sortując hello dokumentów w strumieniu dokument wejściowy hello w kolejności malejącej, używając hello danego predykatu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="af1fb-263">To zachowanie podobne klauzuli ORDER BY x DESC tooa w języku SQL.</span><span class="sxs-lookup"><span data-stu-id="af1fb-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="af1fb-264">Podczas się wewnątrz predykatu lub selektora funkcje, hello następujące konstrukcje JavaScript uzyskać automatycznie zoptymalizowane toorun bezpośrednio na indeksy bazy danych rozwiązania Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="af1fb-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="af1fb-265">Operatory prosty: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="af1fb-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="af1fb-266">Literały, w tym literału obiektu hello: {}</span><span class="sxs-lookup"><span data-stu-id="af1fb-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="af1fb-267">var return</span><span class="sxs-lookup"><span data-stu-id="af1fb-267">var, return</span></span>

<span data-ttu-id="af1fb-268">Witaj, który tworzy następujące JavaScript nie pobrać zoptymalizowane pod kątem indeksy bazy danych Azure rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="af1fb-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="af1fb-269">Przepływ kontroli (np. Jeśli, podczas gdy)</span><span class="sxs-lookup"><span data-stu-id="af1fb-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="af1fb-270">Wywołania funkcji</span><span class="sxs-lookup"><span data-stu-id="af1fb-270">Function calls</span></span>

<span data-ttu-id="af1fb-271">Aby uzyskać więcej informacji, zobacz nasze [JSDocs po stronie serwera](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="af1fb-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="af1fb-272">Przykład: Zapisu przy użyciu interfejsu API zapytania JavaScript hello procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="af1fb-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="af1fb-273">powitania po przykładowy kod jest przykładem sposobu użycia hello JavaScript API zapytania w kontekście hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="af1fb-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="af1fb-274">Witaj procedury składowanej wstawia dokumentu, określonego przez parametr wejściowy i aktualizuje dokument metadanych, przy użyciu hello `__.filter()` metody minSize, maxSize i totalSize ustalane na podstawie właściwości size hello dokument wejściowy.</span><span class="sxs-lookup"><span data-stu-id="af1fb-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="af1fb-275">Arkusz ze wskazówkami dotyczącymi tooJavascript SQL</span><span class="sxs-lookup"><span data-stu-id="af1fb-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="af1fb-276">Witaj poniższej tabeli przedstawiono różne zapytania SQL i hello odpowiednich zapytań języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af1fb-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="af1fb-277">Z kwerendy SQL dokumentu klucze właściwości (np. `doc.id`) jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="af1fb-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="af1fb-278">SQL</span><span class="sxs-lookup"><span data-stu-id="af1fb-278">SQL</span></span>| <span data-ttu-id="af1fb-279">JavaScript zapytania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="af1fb-279">JavaScript Query API</span></span>|<span data-ttu-id="af1fb-280">Poniższy opis</span><span class="sxs-lookup"><span data-stu-id="af1fb-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="af1fb-281">WYBIERZ *</span><span class="sxs-lookup"><span data-stu-id="af1fb-281">SELECT *</span></span><br><span data-ttu-id="af1fb-282">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-282">FROM docs</span></span>| <span data-ttu-id="af1fb-283">__.map(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="af1fb-284">&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc;</span><span class="sxs-lookup"><span data-stu-id="af1fb-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="af1fb-285">});</span><span class="sxs-lookup"><span data-stu-id="af1fb-285">});</span></span>|<span data-ttu-id="af1fb-286">1</span><span class="sxs-lookup"><span data-stu-id="af1fb-286">1</span></span>|
|<span data-ttu-id="af1fb-287">Wybierz docs.id, docs.message jako msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="af1fb-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="af1fb-288">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-288">FROM docs</span></span>|<span data-ttu-id="af1fb-289">__.map(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-289">__.map(function(doc) {</span></span><br><span data-ttu-id="af1fb-290">&nbsp;&nbsp;&nbsp;&nbsp;Zwraca {</span><span class="sxs-lookup"><span data-stu-id="af1fb-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="af1fb-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identyfikator: doc.id,</span><span class="sxs-lookup"><span data-stu-id="af1fb-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="af1fb-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="af1fb-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="af1fb-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions</span><span class="sxs-lookup"><span data-stu-id="af1fb-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="af1fb-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="af1fb-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="af1fb-295">});</span><span class="sxs-lookup"><span data-stu-id="af1fb-295">});</span></span>|<span data-ttu-id="af1fb-296">2</span><span class="sxs-lookup"><span data-stu-id="af1fb-296">2</span></span>|
|<span data-ttu-id="af1fb-297">WYBIERZ *</span><span class="sxs-lookup"><span data-stu-id="af1fb-297">SELECT *</span></span><br><span data-ttu-id="af1fb-298">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-298">FROM docs</span></span><br><span data-ttu-id="af1fb-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="af1fb-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="af1fb-300">__.Filter(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="af1fb-301">&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc.id === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="af1fb-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="af1fb-302">});</span><span class="sxs-lookup"><span data-stu-id="af1fb-302">});</span></span>|<span data-ttu-id="af1fb-303">3</span><span class="sxs-lookup"><span data-stu-id="af1fb-303">3</span></span>|
|<span data-ttu-id="af1fb-304">WYBIERZ *</span><span class="sxs-lookup"><span data-stu-id="af1fb-304">SELECT *</span></span><br><span data-ttu-id="af1fb-305">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-305">FROM docs</span></span><br><span data-ttu-id="af1fb-306">GDZIE ARRAY_CONTAINS (dokumentów. Tagi, 123)</span><span class="sxs-lookup"><span data-stu-id="af1fb-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="af1fb-307">__.Filter(Function(x) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-307">__.filter(function(x) {</span></span><br><span data-ttu-id="af1fb-308">&nbsp;&nbsp;&nbsp;&nbsp;Zwraca x.Tags & & x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="af1fb-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="af1fb-309">});</span><span class="sxs-lookup"><span data-stu-id="af1fb-309">});</span></span>|<span data-ttu-id="af1fb-310">4</span><span class="sxs-lookup"><span data-stu-id="af1fb-310">4</span></span>|
|<span data-ttu-id="af1fb-311">Wybierz docs.id, docs.message jako msg</span><span class="sxs-lookup"><span data-stu-id="af1fb-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="af1fb-312">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-312">FROM docs</span></span><br><span data-ttu-id="af1fb-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="af1fb-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="af1fb-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="af1fb-314">__.chain()</span></span><br><span data-ttu-id="af1fb-315">&nbsp;&nbsp;&nbsp;&nbsp;.Filter(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="af1fb-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc.id === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="af1fb-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="af1fb-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af1fb-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af1fb-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="af1fb-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca {</span><span class="sxs-lookup"><span data-stu-id="af1fb-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="af1fb-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identyfikator: doc.id,</span><span class="sxs-lookup"><span data-stu-id="af1fb-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="af1fb-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="af1fb-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="af1fb-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="af1fb-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="af1fb-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af1fb-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af1fb-324">.Value();</span><span class="sxs-lookup"><span data-stu-id="af1fb-324">.value();</span></span>|<span data-ttu-id="af1fb-325">5</span><span class="sxs-lookup"><span data-stu-id="af1fb-325">5</span></span>|
|<span data-ttu-id="af1fb-326">Wybierz wartość tagu</span><span class="sxs-lookup"><span data-stu-id="af1fb-326">SELECT VALUE tag</span></span><br><span data-ttu-id="af1fb-327">Z dokumentów</span><span class="sxs-lookup"><span data-stu-id="af1fb-327">FROM docs</span></span><br><span data-ttu-id="af1fb-328">Dołącz do dokumentów w tagu. Tagi</span><span class="sxs-lookup"><span data-stu-id="af1fb-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="af1fb-329">Docs._ts ORDER BY</span><span class="sxs-lookup"><span data-stu-id="af1fb-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="af1fb-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="af1fb-330">__.chain()</span></span><br><span data-ttu-id="af1fb-331">&nbsp;&nbsp;&nbsp;&nbsp;.Filter(Function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="af1fb-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwróć dokumentu. Tagi & & Array.IsArray — (dokumentu. Znaczniki);</span><span class="sxs-lookup"><span data-stu-id="af1fb-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="af1fb-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af1fb-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af1fb-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="af1fb-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="af1fb-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zwraca doc._ts;</span><span class="sxs-lookup"><span data-stu-id="af1fb-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="af1fb-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="af1fb-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="af1fb-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="af1fb-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="af1fb-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="af1fb-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="af1fb-339">&nbsp;&nbsp;&nbsp;&nbsp;.Value()</span><span class="sxs-lookup"><span data-stu-id="af1fb-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="af1fb-340">6</span><span class="sxs-lookup"><span data-stu-id="af1fb-340">6</span></span>|

<span data-ttu-id="af1fb-341">Witaj poniższymi opisami wyjaśnić, każdego zapytania w powyższej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="af1fb-342">To powoduje wszystkie dokumenty (podzielony na strony z token kontynuacji) jako.</span><span class="sxs-lookup"><span data-stu-id="af1fb-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="af1fb-343">Identyfikator hello projektów, wiadomości (aliasem toomsg) i akcji z wszystkie dokumenty.</span><span class="sxs-lookup"><span data-stu-id="af1fb-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="af1fb-344">Zapytania dotyczące dokumentów za pomocą predykatu hello: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="af1fb-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="af1fb-345">Zapytania dotyczące dokumentów, których właściwość tagów i tagów jest tablicą zawierającą wartość hello 123.</span><span class="sxs-lookup"><span data-stu-id="af1fb-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="af1fb-346">Zapytania dotyczące dokumentów z predykatem, id = "X998_Y998", a następnie identyfikator hello projektów i komunikatów (aliasem toomsg).</span><span class="sxs-lookup"><span data-stu-id="af1fb-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="af1fb-347">Filtry dla dokumentów, które mają właściwości tablicy, tagi, i sortuje hello wynikowy dokumentów przez właściwość sygnatury czasowej systemu _ts hello i następnie projektów + spłaszcza hello tagi tablicy.</span><span class="sxs-lookup"><span data-stu-id="af1fb-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="af1fb-348">Obsługa środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="af1fb-348">Runtime support</span></span>
<span data-ttu-id="af1fb-349">[Interfejs API po stronie serwera usługi DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) zapewnia obsługę hello większość hello Typowe projektowanie funkcjami języka JavaScript jako standardowych przez [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="af1fb-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="af1fb-350">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="af1fb-350">Security</span></span>
<span data-ttu-id="af1fb-351">Procedury składowane JavaScript i wyzwalacze są w trybie piaskownicy tak, aby hello skutków skrypt nie nastąpił przeciek toohello innych bez pośrednictwa izolacji transakcji snapshot hello na poziomie bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="af1fb-352">środowiska wykonawcze Hello w puli, ale czyszczone kontekstu powitania po każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="af1fb-353">Dlatego jest gwarantowane toobe bezpieczne z dowolnym niezamierzone skutki uboczne od siebie.</span><span class="sxs-lookup"><span data-stu-id="af1fb-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="af1fb-354">Wstępna kompilacja</span><span class="sxs-lookup"><span data-stu-id="af1fb-354">Pre-compilation</span></span>
<span data-ttu-id="af1fb-355">Procedur składowanych, wyzwalaczy i funkcji UDF są niejawnie prekompilowany toohello formatu kodu bajtów w kolejności tooavoid kompilacji koszt w momencie hello każde wywołanie skryptu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="af1fb-356">Dzięki temu wywołań procedury składowane są szybkie i ma niewielki rozmiar.</span><span class="sxs-lookup"><span data-stu-id="af1fb-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="af1fb-357">Obsługa zestawu SDK klienta</span><span class="sxs-lookup"><span data-stu-id="af1fb-357">Client SDK support</span></span>
<span data-ttu-id="af1fb-358">W przypadku dodawania toohello interfejsu API usługi DocumentDB dla [Node.js](documentdb-sdk-node.md) klienta, bazy danych Azure rozwiązania Cosmos jest [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), i [zestawów SDK Python](documentdb-sdk-python.md) dla hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="af1fb-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="af1fb-359">Procedur składowanych, wyzwalaczy i funkcji UDF można tworzyć i wykonywane przy użyciu dowolnej z tych zestawów SDK oraz.</span><span class="sxs-lookup"><span data-stu-id="af1fb-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="af1fb-360">powitania po przykładzie pokazano, jak toocreate i wykonywanie procedury przechowywanej za pomocą powitania klienta .NET.</span><span class="sxs-lookup"><span data-stu-id="af1fb-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="af1fb-361">Należy zauważyć, jak typów .NET hello są przekazywane do hello procedurę składowaną w formacie JSON i odczytywania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="af1fb-362">W tym przykładzie pokazano sposób toouse hello [interfejsu API platformy .NET usługi DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate wstępne wyzwalacza i Utwórz dokument z wyzwalaczem hello włączone.</span><span class="sxs-lookup"><span data-stu-id="af1fb-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="af1fb-363">I hello poniższy przykład przedstawia sposób toocreate użytkownika definiowania funkcji (UDF) i używać go w [zapytań SQL usługi DocumentDB interfejsu API](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="af1fb-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="af1fb-364">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="af1fb-364">REST API</span></span>
<span data-ttu-id="af1fb-365">Wszystkie operacje bazy danych rozwiązania Cosmos Azure mogą być wykonywane w sposób RESTful.</span><span class="sxs-lookup"><span data-stu-id="af1fb-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="af1fb-366">Procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika może być zarejestrowany w kolekcji przy użyciu metody POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="af1fb-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="af1fb-367">Witaj poniżej przedstawiono przykładowy sposób tooregister procedury składowanej:</span><span class="sxs-lookup"><span data-stu-id="af1fb-367">hello following is an example of how tooregister a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="af1fb-368">Witaj procedury składowanej jest zarejestrowany, wykonując przed hello identyfikatora URI żądania POST bazami danych/programu testdb/colls/testColl/sprocs z zawierających treść hello hello toocreate procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="af1fb-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="af1fb-369">Wyzwalaczy i funkcji UDF można zarejestrować podobnie, wysyłając odpowiednio POST przed/wyzwalacze i /udfs.</span><span class="sxs-lookup"><span data-stu-id="af1fb-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="af1fb-370">To przechowywane procedury może następnie być wykonywane przez wystawienie żądania POST przed jego link do zasobu:</span><span class="sxs-lookup"><span data-stu-id="af1fb-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="af1fb-371">W tym miejscu hello toohello wejściowe, przechowywane procedury są przekazywane w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="af1fb-372">Należy pamiętać, że dane wejściowe hello jest przekazywany jako tablica JSON parametrów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="af1fb-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="af1fb-373">Hello pierwszej danej wejściowej procedury przyjmuje hello są przechowywane jako dokument, który jest treść odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="af1fb-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="af1fb-374">Otrzymaliśmy odpowiedzi Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="af1fb-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="af1fb-375">Wyzwalacze, w przeciwieństwie do procedur składowanych, nie można wykonać bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="af1fb-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="af1fb-376">Zamiast tego są one wykonywane w ramach operacji w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="af1fb-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="af1fb-377">Można określić toorun wyzwalaczy hello z żądaniem korzystanie z nagłówków HTTP.</span><span class="sxs-lookup"><span data-stu-id="af1fb-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="af1fb-378">Oto Hello toocreate żądania dokumentu.</span><span class="sxs-lookup"><span data-stu-id="af1fb-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="af1fb-379">Tutaj toobe wstępne wyzwalacza hello Uruchom z żądaniem hello jest określony w nagłówku x-ms-documentdb-pre-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="af1fb-380">Odpowiednio żadne po wyzwalacze są podane w nagłówku x-ms-documentdb-post-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="af1fb-381">Należy pamiętać, że zarówno przed i po wyzwalaczy można określić dla danego żądania.</span><span class="sxs-lookup"><span data-stu-id="af1fb-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="af1fb-382">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="af1fb-382">Sample code</span></span>
<span data-ttu-id="af1fb-383">Można znaleźć więcej przykładów kodu po stronie serwera (w tym [usuwanie zbiorcze](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), i [aktualizacji](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) na naszych [repozytorium GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="af1fb-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="af1fb-384">Chcesz tooshare Twojego świetny procedury składowanej?</span><span class="sxs-lookup"><span data-stu-id="af1fb-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="af1fb-385">Wyślij żądanie ściągnięcia!</span><span class="sxs-lookup"><span data-stu-id="af1fb-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af1fb-386">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af1fb-386">Next steps</span></span>
<span data-ttu-id="af1fb-387">Po utworzeniu jednego lub więcej procedur składowanych, wyzwalaczy i funkcji zdefiniowanych przez użytkownika utworzonych można załadować je i je wyświetlić w portalu Azure za pomocą Eksploratora danych hello.</span><span class="sxs-lookup"><span data-stu-id="af1fb-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="af1fb-388">Można również znaleźć hello następujących odwołań i zasoby przydatne w Twojej więcej informacji na temat programowania po stronie serwera bazy danych Azure rozwiązania Cosmos toolearn ścieżki:</span><span class="sxs-lookup"><span data-stu-id="af1fb-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="af1fb-389">Zestawy SDK Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="af1fb-390">Studio usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="af1fb-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="af1fb-391">JSON</span><span class="sxs-lookup"><span data-stu-id="af1fb-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="af1fb-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="af1fb-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="af1fb-393">Rozszerzalność bezpieczne i przenośnych bazy danych</span><span class="sxs-lookup"><span data-stu-id="af1fb-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="af1fb-394">Architektura bazy danych zorientowane na usługę</span><span class="sxs-lookup"><span data-stu-id="af1fb-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="af1fb-395">Hosting hello środowiska uruchomieniowego .NET programu Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="af1fb-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

