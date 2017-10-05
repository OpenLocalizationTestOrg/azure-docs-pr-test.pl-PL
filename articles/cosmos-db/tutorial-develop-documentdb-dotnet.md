---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie za pomocą usługi DocumentDB interfejsu API programu .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzyć aplikacje za pomocą interfejsu API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="16f4d-103">Azure CosmosDB: Tworzenie za pomocą interfejsu API usługi DocumentDB w .NET</span><span class="sxs-lookup"><span data-stu-id="16f4d-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="16f4d-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16f4d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="16f4d-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="16f4d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="16f4d-106">Ten samouczek pokazuje, jak utworzyć konto bazy danych rozwiązania Cosmos Azure przy użyciu portalu Azure, a następnie utwórz bazą danych dokumentów i kolekcji z [klucza partycji](documentdb-partition-data.md#partition-keys) przy użyciu [interfejsu API platformy .NET usługi DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16f4d-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="16f4d-107">Definiując klucza partycji podczas tworzenia kolekcji, aplikacja jest przygotowana do łatwego skalowania wraz z rozwojem danych.</span><span class="sxs-lookup"><span data-stu-id="16f4d-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="16f4d-108">Ten samouczek obejmuje następujące zadania za pomocą [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="16f4d-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16f4d-109">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="16f4d-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="16f4d-110">Tworzenie bazy danych i kolekcji z użyciem klucza partycji</span><span class="sxs-lookup"><span data-stu-id="16f4d-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="16f4d-111">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="16f4d-111">Create JSON documents</span></span>
> * <span data-ttu-id="16f4d-112">Aktualizowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="16f4d-112">Update a document</span></span>
> * <span data-ttu-id="16f4d-113">Zapytanie względem kolekcji podzielone na partycje</span><span class="sxs-lookup"><span data-stu-id="16f4d-113">Query partitioned collections</span></span>
> * <span data-ttu-id="16f4d-114">Uruchamianie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="16f4d-114">Run stored procedures</span></span>
> * <span data-ttu-id="16f4d-115">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="16f4d-115">Delete a document</span></span>
> * <span data-ttu-id="16f4d-116">Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16f4d-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16f4d-117">Prerequisites</span></span>
<span data-ttu-id="16f4d-118">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="16f4d-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="16f4d-119">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16f4d-119">An active Azure account.</span></span> <span data-ttu-id="16f4d-120">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="16f4d-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="16f4d-121">Alternatywnie można użyć [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku, jeśli chcesz użyć lokalnego środowiska, które emuluje usługi Azure DocumentDB do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="16f4d-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="16f4d-122">Program [Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="16f4d-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="16f4d-123">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="16f4d-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="16f4d-124">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="16f4d-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="16f4d-125">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="16f4d-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="16f4d-126">Jeśli tak, przejdź do [konfigurowanie rozwiązania Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="16f4d-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="16f4d-127">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="16f4d-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="16f4d-128">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu do [konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="16f4d-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="16f4d-129">Jeśli używasz emulatora usługi Azure rozwiązania Cosmos bazy danych, wykonaj kroki opisane w temacie [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) skonfigurować emulatora i przejść od razu do [konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="16f4d-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="16f4d-130"><a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16f4d-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="16f4d-131">Otwórz program **Visual Studio** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="16f4d-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="16f4d-132">W menu **Plik** wybierz polecenie **Nowy**, a następnie wybierz pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="16f4d-133">W **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)** , nazwę projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="16f4d-134">![Zrzut ekranu przedstawiający okno Nowy projekt](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="16f4d-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="16f4d-135">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w ramach rozwiązania Visual Studio, a następnie kliknij pozycję **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="16f4d-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Zrzut ekranu przedstawiający menu projektu kliknięte prawym przyciskiem myszy](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="16f4d-137">W **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **documentdb** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="16f4d-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="16f4d-138">W wynikach znajdź pozycję **Microsoft.Azure.DocumentDB** i kliknij przycisk **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="16f4d-139">Identyfikator pakietu dla biblioteki klienta usługi Azure rozwiązania Cosmos bazy danych jest [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="16f4d-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="16f4d-140">![Zrzut ekranu przedstawiający NuGet Menu do znajdowania zestawu SDK klienta usługi Azure rozwiązania Cosmos bazy danych](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="16f4d-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="16f4d-141">Jeśli zostanie wyświetlony komunikat dotyczący przejrzenia zmian wprowadzonych w rozwiązaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="16f4d-142">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="16f4d-143"><a id="Connect"></a>Dodaj odwołania do projektu</span><span class="sxs-lookup"><span data-stu-id="16f4d-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="16f4d-144">Pozostałe kroki w tym samouczku Podaj wstawki kodu interfejsu API usługi DocumentDB, które są wymagane do tworzenia i aktualizacji bazy danych Azure rozwiązania Cosmos zasobów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="16f4d-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="16f4d-145">Najpierw dodaj te odwołania do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="16f4d-146"><a id="add-references"></a>Łączenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="16f4d-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="16f4d-147">Następnie dodaj te dwie stałe i *klienta* zmiennej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="16f4d-148">Następnie, head z powrotem do [portalu Azure](https://portal.azure.com) można pobrać adresu URL punktu końcowego, a klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="16f4d-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="16f4d-149">Adres URL punktu końcowego i klucz podstawowy są niezbędne, aby aplikacja wiedziała, z jakim elementem ma się połączyć, oraz aby usługa Azure Cosmos DB ufała połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="16f4d-150">W portalu Azure, przejdź do swojego konta bazy danych rozwiązania Cosmos platformy Azure, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="16f4d-151">Skopiuj identyfikator URI z portalu i wklej go za pośrednictwem `<your endpoint URL>` w pliku program.cs.</span><span class="sxs-lookup"><span data-stu-id="16f4d-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="16f4d-152">Następnie skopiuj podstawowy klucz z portalu i wklej go za pośrednictwem `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="16f4d-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="16f4d-153">Należy usunąć `<` i `>` z własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="16f4d-153">Be sure to remove the `<` and `>` from your values.</span></span>

![Zrzut ekranu przedstawiający portal Azure używany przez samouczek NoSQL do tworzenia aplikacji konsolowej C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="16f4d-156"><a id="instantiate"></a>Utwórz wystąpienie obiektu DocumentClient</span><span class="sxs-lookup"><span data-stu-id="16f4d-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="16f4d-157">Teraz, Utwórz nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="16f4d-158"><a id="create-database"></a>Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="16f4d-159">Następnie należy utworzyć bazy danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) za pomocą [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody  **DocumentClient** klasę z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="16f4d-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="16f4d-160">Baza danych jest kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="16f4d-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="16f4d-161">Podejmowanie decyzji o klucza partycji</span><span class="sxs-lookup"><span data-stu-id="16f4d-161">Decide on a partition key</span></span> 

<span data-ttu-id="16f4d-162">Kolekcje są kontenerami do przechowywania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="16f4d-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="16f4d-163">Zasoby logiczne i można je [obejmować co najmniej jednej partycji fizycznej](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="16f4d-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="16f4d-164">A [klucza partycji](documentdb-partition-data.md) jest właściwość (lub ścieżki) w dokumencie, które jest używane do rozpowszechniania danych między serwerami lub partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="16f4d-165">Wszystkie dokumenty z tym samym kluczem partycji są przechowywane w tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="16f4d-166">Określanie klucza partycji jest ważne decyzja podejmowana przed utworzeniem kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="16f4d-167">Klucze partycji są właściwości (lub ścieżki) w dokumentach używane przez bazy danych Azure rozwiązania Cosmos w dystrybucji danych między wieloma serwerami lub partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="16f4d-168">Rozwiązania cosmos DB skróty wartość klucza partycji i używa skrótu wynik w celu określenia partycji, w której ma zostać zapisany dokument.</span><span class="sxs-lookup"><span data-stu-id="16f4d-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="16f4d-169">Wszystkie dokumenty z tym samym kluczem partycji są przechowywane w tej samej partycji, a klucze partycji nie można zmienić po utworzeniu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="16f4d-170">W tym samouczku, chcemy się wartość klucza partycji `/deviceId` tak, aby wszystkie dane na jednym urządzeniu są przechowywane w jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="16f4d-171">Chcesz wybrać klucza partycji, który ma wiele wartości, z których każdy są używane na temat taką samą częstotliwością do upewnij się, że rozwiązania Cosmos DB może równoważyć obciążenie danych rozwoju lub osiągnięcia pełnej przepływności kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="16f4d-172">Aby uzyskać więcej informacji na temat partycjonowania, zobacz [partycji i skali w usłudze Azure DB rozwiązania Cosmos?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="16f4d-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="16f4d-173"><a id="CreateColl"></a>Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="16f4d-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="16f4d-174">Teraz, wiemy naszych klucza partycji `/deviceId`, umożliwia tworzenie [kolekcji](documentdb-resources.md#collections) za pomocą [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [CreateDocumentCollectionIfNotExistsAsync ](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="16f4d-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="16f4d-175">Kolekcja jest kontenerem dokumentów JSON i wszelkie skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="16f4d-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="16f4d-176">Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla aplikacji do komunikowania się z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="16f4d-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="16f4d-177">Aby uzyskać więcej informacji, odwiedź stronę naszych [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="16f4d-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="16f4d-178">Ta metoda powoduje, że wywołanie bazy danych Azure rozwiązania Cosmos i przepisy usługi liczba partycji na podstawie przepływności żądanego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="16f4d-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="16f4d-179">Można zmienić przepływność kolekcji, ponieważ wydajność potrzebuje rozwija przy użyciu zestawu SDK lub [portalu Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="16f4d-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="16f4d-180"><a id="CreateDoc"></a>Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="16f4d-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="16f4d-181">Teraz można wstawić niektórych dokumentów JSON do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="16f4d-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="16f4d-182">[Dokument](documentdb-resources.md#documents) można utworzyć za pomocą metody [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="16f4d-183">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="16f4d-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="16f4d-184">Ta klasa przykładowe zawiera urządzenia odczytywania i wywołanie CreateDocumentAsync Wstaw nowe urządzenie odczytu do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="16f4d-185">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-185">Read data</span></span>

<span data-ttu-id="16f4d-186">Załóżmy odczytu dokumentu przez klucz partycji i identyfikator przy użyciu metody ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="16f4d-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="16f4d-187">Należy pamiętać, że odczyty obejmują wartość PartitionKey (odpowiadający `x-ms-documentdb-partitionkey` nagłówek żądania w interfejsie API REST).</span><span class="sxs-lookup"><span data-stu-id="16f4d-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="16f4d-188">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-188">Update data</span></span>

<span data-ttu-id="16f4d-189">Teraz załóżmy zaktualizować niektóre dane przy użyciu metody ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="16f4d-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="16f4d-190">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-190">Delete data</span></span>

<span data-ttu-id="16f4d-191">Umożliwia teraz usunąć przy użyciu metody DeleteDocumentAsync dokumentu przez klucz partycji i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="16f4d-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="16f4d-192">Zapytanie względem kolekcji podzielone na partycje</span><span class="sxs-lookup"><span data-stu-id="16f4d-192">Query partitioned collections</span></span>

<span data-ttu-id="16f4d-193">Kwerendy danych w kolekcjach podzielonym na partycje, bazy danych Azure rozwiązania Cosmos automatycznie rozsyła kwerendy do partycji odpowiadający wartości klucza partycji podana w filtrze (jeśli istnieją).</span><span class="sxs-lookup"><span data-stu-id="16f4d-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="16f4d-194">Na przykład to zapytanie jest kierowany do właśnie partycji zawierającej klucz partycji "XMS 0001".</span><span class="sxs-lookup"><span data-stu-id="16f4d-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="16f4d-195">Następujące zapytanie nie ma filtr klucza partycji (DeviceId) i jest rozwiniętym do wszystkich partycji, w którym jest przeprowadzana z partycji indeksu.</span><span class="sxs-lookup"><span data-stu-id="16f4d-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="16f4d-196">Należy pamiętać, że trzeba określić EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` w interfejsie API REST) ma zestaw SDK, aby wykonać zapytania na partycje.</span><span class="sxs-lookup"><span data-stu-id="16f4d-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="16f4d-197">Równoległego wykonywania zapytań</span><span class="sxs-lookup"><span data-stu-id="16f4d-197">Parallel query execution</span></span>
<span data-ttu-id="16f4d-198">Zestawów DocumentDB SDK DB rozwiązania Cosmos Azure 1.9.0 i powyżej opcje wykonywania zapytania równoległe pomocy technicznej, które umożliwiają wykonywanie zapytań o małych opóźnieniach dotyczących kolekcji partycjonowanych nawet wtedy, gdy konieczne jest touch dużą liczbę partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="16f4d-199">Na przykład następujące zapytanie jest skonfigurowany do uruchomienia równoległego na partycje.</span><span class="sxs-lookup"><span data-stu-id="16f4d-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="16f4d-200">Możesz zarządzać równoległego wykonywania zapytań przez dostrajanie następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="16f4d-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="16f4d-201">Przez ustawienie `MaxDegreeOfParallelism`, można kontrolować stopień równoległości tj., maksymalną liczbę równoczesnych połączeń sieciowych do partycji w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="16f4d-202">Jeśli ustawisz to-1, stopień równoległości jest zarządzany przez zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="16f4d-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="16f4d-203">Jeśli `MaxDegreeOfParallelism` nie jest określony lub ustawiona na 0, co jest to wartość domyślna, będzie jednego połączenia sieciowego z partycjami kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="16f4d-204">Przez ustawienie `MaxBufferedItemCount`, można kompromis wykorzystanie pamięci zapytania opóźnienia i po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="16f4d-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="16f4d-205">Jeśli ten parametr lub ustaw tę wartość-1, liczba elementów buforowane podczas równoległego wykonywania zapytań jest zarządzany przez zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="16f4d-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="16f4d-206">Podana takim samym stanie kolekcji, zapytań równoległych zwróci wyniki w tej samej kolejności jak wykonanie szeregowego.</span><span class="sxs-lookup"><span data-stu-id="16f4d-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="16f4d-207">Podczas wykonywania kwerendy między partycji zawierającej, sortowanie (ORDER BY i/lub góry), zestaw SDK usługi DocumentDB wystawia zapytania równolegle na partycje i scala częściowo sortowane wyniki w po stronie klienta, aby wygenerować globalnie uporządkowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="16f4d-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="16f4d-208">Wykonanie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="16f4d-208">Execute stored procedures</span></span>
<span data-ttu-id="16f4d-209">Ponadto można wykonywać transakcje atomic względem dokumentów mających taki sam identyfikator urządzenia, np. Jeśli wartości zagregowanych lub najnowszy stan urządzeń w jednym dokumencie jest obsługa przez dodanie poniższego kodu do projektu.</span><span class="sxs-lookup"><span data-stu-id="16f4d-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="16f4d-210">I to już wszystko!</span><span class="sxs-lookup"><span data-stu-id="16f4d-210">And that's it!</span></span> <span data-ttu-id="16f4d-211">to są głównymi składnikami aplikacji bazy danych rozwiązania Cosmos platformy Azure, która używa klucza partycji wydajne skalowanie dystrybucji danych na partycji.</span><span class="sxs-lookup"><span data-stu-id="16f4d-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="16f4d-212">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="16f4d-212">Clean up resources</span></span>

<span data-ttu-id="16f4d-213">Jeśli nie zamierzasz nadal korzystać z tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego samouczka w portalu Azure następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="16f4d-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="16f4d-214">Z menu po lewej stronie w portalu Azure kliknij **grup zasobów** a następnie kliknij przycisk unikatową nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="16f4d-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="16f4d-215">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="16f4d-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16f4d-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16f4d-216">Next steps</span></span>

<span data-ttu-id="16f4d-217">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="16f4d-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="16f4d-218">Utworzone konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="16f4d-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="16f4d-219">Utworzony z użyciem klucza partycji bazy danych i kolekcji</span><span class="sxs-lookup"><span data-stu-id="16f4d-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="16f4d-220">Utworzony dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="16f4d-220">Created JSON documents</span></span>
> * <span data-ttu-id="16f4d-221">Zaktualizowano dokumentu</span><span class="sxs-lookup"><span data-stu-id="16f4d-221">Updated a document</span></span>
> * <span data-ttu-id="16f4d-222">Zapytanie kolekcji partycjonowanych</span><span class="sxs-lookup"><span data-stu-id="16f4d-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="16f4d-223">Uruchomiono procedurę składowaną</span><span class="sxs-lookup"><span data-stu-id="16f4d-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="16f4d-224">Usunąć dokumentu</span><span class="sxs-lookup"><span data-stu-id="16f4d-224">Deleted a document</span></span>
> * <span data-ttu-id="16f4d-225">Usunięte z bazy danych</span><span class="sxs-lookup"><span data-stu-id="16f4d-225">Deleted a database</span></span>

<span data-ttu-id="16f4d-226">Można teraz przejść do następnego samouczek i zaimportuj dane dodatkowe do swojego konta DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="16f4d-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="16f4d-227">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="16f4d-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
