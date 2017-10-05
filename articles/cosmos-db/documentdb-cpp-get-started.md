---
title: "Samouczek języka C++ dla usługi Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="f69ca-104">Azure Cosmos DB: samouczek aplikacji w języku C++ dla interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f69ca-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f69ca-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f69ca-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f69ca-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f69ca-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f69ca-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="f69ca-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f69ca-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="f69ca-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f69ca-109">Java</span><span class="sxs-lookup"><span data-stu-id="f69ca-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f69ca-110">C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="f69ca-111">Witamy w samouczku języka C++ dla zatwierdzonego dla interfejsu API DocumentDB usługi Azure Cosmos DB zestawu SDK języka C++!</span><span class="sxs-lookup"><span data-stu-id="f69ca-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="f69ca-112">W ramach tego samouczka utworzysz aplikację konsolową, która tworzy zasoby usługi Azure Cosmos DB, w tym bazę danych w języku C++, oraz wykonuje względem nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="f69ca-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="f69ca-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f69ca-113">We'll cover:</span></span>

* <span data-ttu-id="f69ca-114">Tworzenie konta usługi Azure Cosmos DB i łączenie się z nim</span><span class="sxs-lookup"><span data-stu-id="f69ca-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="f69ca-115">Instalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f69ca-115">Setting up your application</span></span>
* <span data-ttu-id="f69ca-116">Tworzenie bazy danych usługi Azure Cosmos DB dla języka C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="f69ca-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="f69ca-117">Creating a collection</span></span>
* <span data-ttu-id="f69ca-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="f69ca-118">Creating JSON documents</span></span>
* <span data-ttu-id="f69ca-119">Wykonywanie zapytań względem kolekcji</span><span class="sxs-lookup"><span data-stu-id="f69ca-119">Querying the collection</span></span>
* <span data-ttu-id="f69ca-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f69ca-120">Replacing a document</span></span>
* <span data-ttu-id="f69ca-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f69ca-121">Deleting a document</span></span>
* <span data-ttu-id="f69ca-122">Usuwanie bazy danych usługi Azure Cosmos DB dla języka C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="f69ca-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="f69ca-123">Don't have time?</span></span> <span data-ttu-id="f69ca-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="f69ca-124">Don't worry!</span></span> <span data-ttu-id="f69ca-125">Kompletne rozwiązanie jest dostępne w witrynie [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="f69ca-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="f69ca-126">Przejdź do sekcji [Pobieranie kompletnego rozwiązania](#GetSolution), aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="f69ca-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f69ca-127">Po ukończeniu samouczka języka C++ użyj przycisków głosowania u dołu tej strony, aby przesłać nam swoją opinię.</span><span class="sxs-lookup"><span data-stu-id="f69ca-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="f69ca-128">Jeśli chcesz, abyśmy skontaktowali się z Tobą bezpośrednio, możesz w komentarzach podać swój adres e-mail lub [skontaktować się z nami tutaj](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="f69ca-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="f69ca-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="f69ca-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="f69ca-130">Wymagania wstępne dla samouczka języka C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="f69ca-131">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="f69ca-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="f69ca-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f69ca-132">An active Azure account.</span></span> <span data-ttu-id="f69ca-133">Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f69ca-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f69ca-134">Program [Visual Studio](https://www.visualstudio.com/downloads/) z zainstalowanymi składnikami języka C++.</span><span class="sxs-lookup"><span data-stu-id="f69ca-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f69ca-135">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f69ca-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f69ca-136">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f69ca-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f69ca-137">Jeśli masz już konto, którego chcesz użyć, możesz przejść od razu do kroku [Konfigurowanie aplikacji języka C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f69ca-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f69ca-138"><a id="SetupC++"></a>Krok 2. Konfigurowanie aplikacji języka C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="f69ca-139">Otwórz program Visual Studio, w menu **Plik** kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="f69ca-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="f69ca-140">W oknie **Nowy projekt** w okienku **Zainstalowane** rozwiń węzeł **Visual C++**, kliknij pozycję **Win32**, a następnie kliknij pozycję **Aplikacja konsolowa Win32**.</span><span class="sxs-lookup"><span data-stu-id="f69ca-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="f69ca-141">Nadaj projektowi nazwę hellodocumentdb, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f69ca-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Zrzut ekranu przedstawiający kreatora nowego projektu](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="f69ca-143">Po uruchomieniu Kreatora aplikacji Win32 kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f69ca-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="f69ca-144">Po utworzeniu projektu otwórz Menedżera pakietów NuGet, klikając prawym przyciskiem myszy projekt **hellodocumentdb** w **Eksploratorze rozwiązań**, a następnie klikając pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f69ca-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Zrzut ekranu przedstawiający pozycję Zarządzaj pakietami NuGet w menu projektu](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="f69ca-146">Na karcie **NuGet: hellodocumentdb** kliknij pozycję **Przeglądaj**, a następnie wyszukaj ciąg *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="f69ca-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="f69ca-147">W wynikach wybierz pozycję DocumentDbCPP, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="f69ca-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="f69ca-148">Ten pakiet instaluje odwołania do zestawu SDK REST języka C++, który jest zależnością dla pakietu DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="f69ca-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Zrzut ekranu przedstawiający wyróżniony pakiet DocumentDbCpp](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="f69ca-150">Gdy pakiety zostaną dodane do projektu, będziemy gotowi do rozpoczęcia pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="f69ca-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="f69ca-151"><a id="Config"></a>Krok 3. Kopiowanie szczegółów połączenia z witryny Azure Portal dla bazy danych Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f69ca-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="f69ca-152">Wywołaj witrynę [Azure Portal](https://portal.azure.com) i przejdź do utworzonego konta bazy danych Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f69ca-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="f69ca-153">W następnym kroku identyfikator URI i klucz podstawowy z witryny Azure Portal będą nam potrzebne do nawiązania połączenia z naszych fragmentów kodu w języku C++.</span><span class="sxs-lookup"><span data-stu-id="f69ca-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Identyfikator URI usługi Azure Cosmos DB i klucze w witrynie Azure Portal](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="f69ca-155"><a id="Connect"></a>Krok 4. Łączenie się z kontem usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f69ca-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="f69ca-156">Po wierszu `#include "stdafx.h"` dodaj następujące nagłówki i przestrzenie nazw do kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="f69ca-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="f69ca-157">Następnie dodaj następujący kod do funkcji main oraz zastąp konfigurację konta i klucz podstawowy, aby dopasować ustawienia usługi Azure Cosmos DB z kroku 3.</span><span class="sxs-lookup"><span data-stu-id="f69ca-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="f69ca-158">Teraz, gdy masz kod do zainicjowania klienta documentdb, przyjrzyjmy się pracy z zasobami usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f69ca-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="f69ca-159"><a id="CreateDBColl"></a>Krok 5. Tworzenie bazy danych i kolekcji w języku C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="f69ca-160">Zanim wykonamy ten krok, zajmijmy się sposobem interakcji bazy danych, kolekcji i dokumentów dla osób, które zaczynają korzystanie z usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f69ca-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="f69ca-161">[Baza danych](documentdb-resources.md#databases) jest kontenerem logicznym magazynu dokumentów podzielonym na kolekcje.</span><span class="sxs-lookup"><span data-stu-id="f69ca-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="f69ca-162">[Kolekcja](documentdb-resources.md#collections) jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f69ca-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="f69ca-163">Więcej informacji o modelu zasobów hierarchicznych i pojęciach usługi Azure Cosmos DB znajduje się w temacie [Pojęcia i hierarchiczny model zasobów bazy danych Azure Cosmos DB](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f69ca-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="f69ca-164">Aby utworzyć bazę danych i odpowiednią kolekcję, dodaj następujący kod na końcu Twojej funkcji main.</span><span class="sxs-lookup"><span data-stu-id="f69ca-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="f69ca-165">Spowoduje to utworzenie bazy danych o nazwie „FamilyRegistry” i kolekcji o nazwie „FamilyCollection” przy użyciu konfiguracji klienta zadeklarowanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="f69ca-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="f69ca-166"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f69ca-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="f69ca-167">[Dokumenty](documentdb-resources.md#documents) są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="f69ca-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f69ca-168">Teraz można wstawić dokument do usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f69ca-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="f69ca-169">Dokument można utworzyć, kopiując następujący kod i wklejając go na końcu funkcji main.</span><span class="sxs-lookup"><span data-stu-id="f69ca-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="f69ca-170">Podsumowując, ten kod tworzy bazę danych, kolekcję i dokumenty usługi Azure Cosmos DB, do których można tworzyć zapytania w Eksploratorze dokumentów w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f69ca-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Samouczek języka C++ — diagram pokazujący hierarchiczną relację między kontem, bazą danych, kolekcją i dokumentami](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="f69ca-172"><a id="QueryDB"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f69ca-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f69ca-173">Usługa Azure Cosmos DB obsługuje [zaawansowane zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f69ca-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="f69ca-174">Następujący przykładowy kod przedstawia zapytanie wykonywane przy użyciu składni SQL, które możesz uruchomić względem dokumentów utworzonych w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="f69ca-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="f69ca-175">Funkcja przyjmuje jako argumenty unikatowy identyfikator lub identyfikator zasobu dla bazy danych i kolekcji wraz z klientem dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f69ca-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="f69ca-176">Dodaj następujący kod przed funkcją main.</span><span class="sxs-lookup"><span data-stu-id="f69ca-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="f69ca-177"><a id="Replace"></a>Krok 8. Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f69ca-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="f69ca-178">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="f69ca-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="f69ca-179">Dodaj ten kod po funkcji executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="f69ca-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="f69ca-180"><a id="Delete"></a>Krok 9. Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="f69ca-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="f69ca-181">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON. W tym celu możesz skopiować następujący kod i wkleić go po funkcji replacedocument.</span><span class="sxs-lookup"><span data-stu-id="f69ca-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="f69ca-182"><a id="DeleteDB"></a>Krok 10. Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="f69ca-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="f69ca-183">Usunięcie utworzonej bazy danych usunie bazę danych i wszystkie zasoby podrzędne (kolekcje, dokumenty itd.).</span><span class="sxs-lookup"><span data-stu-id="f69ca-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f69ca-184">Skopiuj poniższy fragment kodu (funkcja cleanup) i wklej go po funkcji deletedocument, aby usunąć bazę danych i wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="f69ca-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="f69ca-185"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji w języku C++!</span><span class="sxs-lookup"><span data-stu-id="f69ca-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="f69ca-186">Dodaliśmy kod do tworzenia, modyfikowania i usuwania różnych zasobów usługi Azure Cosmos DB oraz do wykonywania względem nich zapytań.</span><span class="sxs-lookup"><span data-stu-id="f69ca-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="f69ca-187">Połączmy to teraz ze sobą, dodając wywołania tych różnych funkcji w naszej funkcji main w pliku hellodocumentdb.cpp wraz z pewnymi komunikatami diagnostycznymi.</span><span class="sxs-lookup"><span data-stu-id="f69ca-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="f69ca-188">Możesz to zrobić, zastępując funkcję main Twojej aplikacji poniższym kodem.</span><span class="sxs-lookup"><span data-stu-id="f69ca-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="f69ca-189">Nadpisuje to parametry account_configuration_uri i primary_key, które zostały skopiowane do kodu w kroku 3, więc zapisz ten wiersz lub ponownie skopiuj wartości z portalu.</span><span class="sxs-lookup"><span data-stu-id="f69ca-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="f69ca-190">Teraz powinna być możliwość skompilowania i uruchomienia kodu w programie Visual Studio po naciśnięciu klawisza F5 lub alternatywnie w oknie terminala, lokalizując aplikację, a następnie uruchamiając plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="f69ca-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="f69ca-191">Powinny zostać wyświetlone dane wyjściowe aplikacji rozpoczynania pracy.</span><span class="sxs-lookup"><span data-stu-id="f69ca-191">You should see the output of your get started app.</span></span> <span data-ttu-id="f69ca-192">Dane wyjściowe powinny odpowiadać poniższemu zrzutowi ekranu.</span><span class="sxs-lookup"><span data-stu-id="f69ca-192">The output should match the following screenshot.</span></span>

![Dane wyjściowe aplikacji usługi Azure Cosmos DB w języku C++](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="f69ca-194">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f69ca-194">Congratulations!</span></span> <span data-ttu-id="f69ca-195">Udało Ci się ukończyć samouczek języka C++ i utworzyć swoją pierwszą aplikację konsolową usługi Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="f69ca-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="f69ca-196"><a id="GetSolution"></a>Pobieranie kompletnego rozwiązania samouczka języka C++</span><span class="sxs-lookup"><span data-stu-id="f69ca-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="f69ca-197">Aby skompilować rozwiązanie GetStarted, które zawiera wszystkie przykłady z tego artykułu, będą potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f69ca-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="f69ca-198">[Konto usługi Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="f69ca-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="f69ca-199">Rozwiązanie [GetStarted](https://github.com/stalker314314/DocumentDBCpp) dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f69ca-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f69ca-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f69ca-200">Next steps</span></span>
* <span data-ttu-id="f69ca-201">Dowiedz się, jak [monitorować konto usługi Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f69ca-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f69ca-202">Uruchom zapytania względem naszego przykładowego zestawu danych na [placu zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f69ca-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f69ca-203">Dowiedz się więcej o modelu programowania w sekcji Dla deweloperów [strony dokumentacji usługi Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f69ca-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


