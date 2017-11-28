---
title: "Samouczek aaaC ++ dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Samouczek języka C++, który pokazuje tworzenie bazy danych w języku C++ i aplikacji konsolowej przy użyciu zatwierdzonego dla usługi Azure Cosmos DB zestawu SDK języka C++. Azure Cosmos DB to skalowana w skali globalnej usługa bazy danych."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="36ccf-104">Azure DB rozwiązania Cosmos: Samouczek aplikacji konsoli C++ dla hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="36ccf-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36ccf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="36ccf-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="36ccf-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="36ccf-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="36ccf-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="36ccf-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="36ccf-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="36ccf-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="36ccf-109">Java</span><span class="sxs-lookup"><span data-stu-id="36ccf-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="36ccf-110">C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="36ccf-111">Zapraszamy toohello C++ samouczek dotyczący hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB zatwierdzone zestawu SDK dla języka C++!</span><span class="sxs-lookup"><span data-stu-id="36ccf-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="36ccf-112">W ramach tego samouczka utworzysz aplikację konsolową, która tworzy zasoby usługi Azure Cosmos DB, w tym bazę danych w języku C++, oraz wykonuje względem nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="36ccf-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="36ccf-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36ccf-113">We'll cover:</span></span>

* <span data-ttu-id="36ccf-114">Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="36ccf-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="36ccf-115">Instalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="36ccf-115">Setting up your application</span></span>
* <span data-ttu-id="36ccf-116">Tworzenie bazy danych usługi Azure Cosmos DB dla języka C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="36ccf-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="36ccf-117">Creating a collection</span></span>
* <span data-ttu-id="36ccf-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="36ccf-118">Creating JSON documents</span></span>
* <span data-ttu-id="36ccf-119">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="36ccf-119">Querying hello collection</span></span>
* <span data-ttu-id="36ccf-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="36ccf-120">Replacing a document</span></span>
* <span data-ttu-id="36ccf-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="36ccf-121">Deleting a document</span></span>
* <span data-ttu-id="36ccf-122">Usuwanie bazy danych DB rozwiązania Cosmos Azure C++ hello</span><span class="sxs-lookup"><span data-stu-id="36ccf-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="36ccf-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="36ccf-123">Don't have time?</span></span> <span data-ttu-id="36ccf-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="36ccf-124">Don't worry!</span></span> <span data-ttu-id="36ccf-125">Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="36ccf-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="36ccf-126">Zobacz [uzyskać kompletne rozwiązanie hello](#GetSolution) Aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="36ccf-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="36ccf-127">Po ukończeniu samouczka C++ hello, proszę Użyj hello przyciski do głosowania u dołu tej strony toogive hello nam opinii.</span><span class="sxs-lookup"><span data-stu-id="36ccf-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="36ccf-128">Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach lub [dotrzeć tutaj toous](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="36ccf-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="36ccf-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="36ccf-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="36ccf-130">Wymagania wstępne dotyczące samouczka hello C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="36ccf-131">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="36ccf-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="36ccf-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ccf-132">An active Azure account.</span></span> <span data-ttu-id="36ccf-133">Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36ccf-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="36ccf-134">[Visual Studio](https://www.visualstudio.com/downloads/), z zainstalowanymi składnikami języka hello C++.</span><span class="sxs-lookup"><span data-stu-id="36ccf-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="36ccf-135">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36ccf-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="36ccf-136">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="36ccf-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="36ccf-137">Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[instalowanie aplikacji C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="36ccf-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="36ccf-138"><a id="SetupC++"></a>Krok 2. Konfigurowanie aplikacji języka C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="36ccf-139">Otwórz program Visual Studio, a następnie na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="36ccf-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="36ccf-140">W hello **nowy projekt** okna na powitania **zainstalowana** okienku rozwiń **Visual C++**, kliknij przycisk **Win32**, a następnie kliknij przycisk  **Aplikacji konsoli Win32**.</span><span class="sxs-lookup"><span data-stu-id="36ccf-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="36ccf-141">Nazwa hello hellodocumentdb projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="36ccf-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Zrzut ekranu przedstawiający Kreator nowego projektu hello](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="36ccf-143">Po uruchomieniu hello Kreator aplikacji Win32, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="36ccf-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="36ccf-144">Po utworzeniu projektu hello, otwórz Menedżera pakietów NuGet hello, klikając prawym przyciskiem myszy hello **hellodocumentdb** projektu w **Eksploratora rozwiązań** i klikając **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="36ccf-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Zrzut ekranu przedstawiający menu Projekt hello Zarządzanie pakietem NuGet](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="36ccf-146">W hello **NuGet: hellodocumentdb** , kliknij pozycję **Przeglądaj**, a następnie wyszukaj *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="36ccf-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="36ccf-147">W wynikach hello wybierz DocumentDbCPP, jak pokazano w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="36ccf-148">Ten pakiet instaluje odwołania tooC c++ REST SDK, który jest zależność hello DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="36ccf-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Zrzut ekranu przedstawiający hello DocumentDbCpp pakietu, wyróżniony](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="36ccf-150">Po dodaniu pakietów hello tooyour projektu, możemy wszystkie toostart zestaw pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="36ccf-151"><a id="Config"></a>Krok 3. Kopiowanie szczegółów połączenia z witryny Azure Portal dla bazy danych Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36ccf-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="36ccf-152">Wywołaj [portalu Azure](https://portal.azure.com) i przechodzić między nimi utworzonego konta bazy danych dla bazy danych Azure rozwiązania Cosmos toohello.</span><span class="sxs-lookup"><span data-stu-id="36ccf-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="36ccf-153">Wkrótce skontaktujemy hello URI oraz primary key hello z portalu Azure w hello następny krok tooestablish połączenie z naszych fragment kodu w języku C++.</span><span class="sxs-lookup"><span data-stu-id="36ccf-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure rozwiązania Cosmos DB URI i klucze w hello portalu Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="36ccf-155"><a id="Connect"></a>Krok 4: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="36ccf-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="36ccf-156">Dodaj hello następującego kodu źródłowego tooyour nagłówki i przestrzenie nazw, po `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="36ccf-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="36ccf-157">Następnie dodać hello następujący kod tooyour main — funkcja i zastąpienie hello konfiguracji konta i toomatch klucza podstawowego ustawień bazy danych Azure rozwiązania Cosmos w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="36ccf-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="36ccf-158">Teraz, gdy masz klienta usługi documentdb hello tooinitialize kodu hello Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="36ccf-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="36ccf-159"><a id="CreateDBColl"></a>Krok 5. Tworzenie bazy danych i kolekcji w języku C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="36ccf-160">Zanim możemy wykonać ten krok, przejdź na interakcje bazy danych, kolekcji i dokumentów dla osób, które kim są nowe tooAzure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="36ccf-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="36ccf-161">[Baza danych](documentdb-resources.md#databases) jest kontenerem logicznym magazynu dokumentów podzielonym na kolekcje.</span><span class="sxs-lookup"><span data-stu-id="36ccf-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="36ccf-162">A [kolekcji](documentdb-resources.md#collections) jest kontenerem dokumentów JSON i hello skojarzone logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="36ccf-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="36ccf-163">Aby dowiedzieć się więcej o hello Azure DB rozwiązania Cosmos hierarchiczna pojęcia i model zasobów w [pojęcia i model zasobów hierarchiczna bazy danych Azure rozwiązania Cosmos](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="36ccf-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="36ccf-164">toocreate a bazy danych i odpowiedniej kolekcji dodać hello kod zakończenia toohello funkcji main.</span><span class="sxs-lookup"><span data-stu-id="36ccf-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="36ccf-165">Spowoduje to utworzenie bazy danych o nazwie "FamilyRegistry" i kolekcję o nazwie "FamilyCollection" przy użyciu konfiguracji klienta hello zadeklarowany w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="36ccf-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="36ccf-166"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentu</span><span class="sxs-lookup"><span data-stu-id="36ccf-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="36ccf-167">[Dokumenty](documentdb-resources.md#documents) są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="36ccf-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="36ccf-168">Teraz można wstawić dokument do usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="36ccf-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="36ccf-169">Można utworzyć dokumentu, kopiując powitania po kod na końcu hello hello main — funkcja.</span><span class="sxs-lookup"><span data-stu-id="36ccf-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="36ccf-170">toosummarize, ten kod tworzy bazy danych Azure rozwiązania Cosmos bazy danych, kolekcji i dokumentów, które można zbadać w Eksploratora dokumentów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36ccf-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Samouczek C++ — Diagram pokazujący hello hierarchiczną relację między hello konta, hello bazy danych, kolekcji hello i hello dokumentów](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="36ccf-172"><a id="QueryDB"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="36ccf-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="36ccf-173">Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="36ccf-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="36ccf-174">Witaj następujący przykładowy kod przedstawia zapytanie zostało nawiązane przy użyciu składni SQL, który można uruchomić względem dokumentów hello utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="36ccf-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="36ccf-175">Funkcja Hello przyjmuje jako argumenty hello unikatowego identyfikatora lub identyfikator zasobu hello bazy danych i kolekcji hello wraz z powitania klienta dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="36ccf-176">Dodaj następujący kod przed funkcją main.</span><span class="sxs-lookup"><span data-stu-id="36ccf-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="36ccf-177"><a id="Replace"></a>Krok 8. Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="36ccf-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="36ccf-178">Azure DB rozwiązania Cosmos obsługuje zastępowanie dokumentów JSON, jak pokazano w hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="36ccf-179">Dodaj ten kod po hello executesimplequery funkcji.</span><span class="sxs-lookup"><span data-stu-id="36ccf-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="36ccf-180"><a id="Delete"></a>Krok 9. Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="36ccf-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="36ccf-181">Azure DB rozwiązania Cosmos obsługuje usuwanie dokumentów JSON, możesz to zrobić przez kopiowanie i wklejanie hello następującego kodu po hello replacedocument funkcji.</span><span class="sxs-lookup"><span data-stu-id="36ccf-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="36ccf-182"><a id="DeleteDB"></a>Krok 10. Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="36ccf-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="36ccf-183">Trwa usuwanie hello utworzone bazy danych usuwa hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="36ccf-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="36ccf-184">Skopiuj i Wklej hello następującego fragmentu kodu (Funkcja oczyszczania) po bazy danych hello deletedocument funkcja tooremove hello i wszystkie zasoby podrzędne hello.</span><span class="sxs-lookup"><span data-stu-id="36ccf-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="36ccf-185"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji w języku C++!</span><span class="sxs-lookup"><span data-stu-id="36ccf-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="36ccf-186">Firma Microsoft zostało dodane toocreate kodu, zapytania, modyfikowanie i usuwanie różnymi zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="36ccf-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="36ccf-187">Poinformuj nas teraz okablować to się przez dodanie wywołania toothese różne funkcje z naszym głównym funkcji w hellodocumentdb.cpp oraz niektóre komunikaty diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="36ccf-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="36ccf-188">Można to zrobić, zastępując hello główną funkcją aplikacji hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="36ccf-189">Ten zapisy za pośrednictwem hello account_configuration_uri i primary_key skopiowane do kodu hello w kroku 3, więc tej wartości hello wiersza lub kopiowanie w ponownie zapisać hello portalu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="36ccf-190">Powinny teraz toobuild może być i uruchamianie kodu w programie Visual Studio, naciskając klawisz F5 lub też w hello okno terminalu lokalizowania aplikacji hello i uruchamiając hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="36ccf-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="36ccf-191">Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy hello.</span><span class="sxs-lookup"><span data-stu-id="36ccf-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="36ccf-192">Witaj dane wyjściowe powinny odpowiadać hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="36ccf-192">hello output should match hello following screenshot.</span></span>

![Dane wyjściowe aplikacji usługi Azure Cosmos DB w języku C++](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="36ccf-194">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="36ccf-194">Congratulations!</span></span> <span data-ttu-id="36ccf-195">Po ukończeniu samouczka C++ hello i ma swoją pierwszą aplikację konsoli bazy danych rozwiązania Cosmos Azure!</span><span class="sxs-lookup"><span data-stu-id="36ccf-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="36ccf-196"><a id="GetSolution"></a>Pobierz kompletnego rozwiązania samouczka hello C++</span><span class="sxs-lookup"><span data-stu-id="36ccf-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="36ccf-197">rozwiązania GetStarted hello toobuild, który zawiera wszystkie przykłady hello w tym artykule, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="36ccf-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="36ccf-198">[Konto usługi Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="36ccf-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="36ccf-199">Witaj [GetStarted](https://github.com/stalker314314/DocumentDBCpp) rozwiązanie jest dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="36ccf-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36ccf-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36ccf-200">Next steps</span></span>
* <span data-ttu-id="36ccf-201">Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="36ccf-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="36ccf-202">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="36ccf-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="36ccf-203">Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="36ccf-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


