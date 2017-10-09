---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello interfejs API .NET usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
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
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="2895b-103">Azure CosmosDB: Opracowywania hello interfejsu API usługi DocumentDB w .NET</span><span class="sxs-lookup"><span data-stu-id="2895b-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="2895b-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2895b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2895b-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2895b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2895b-106">Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure, a następnie utwórz bazą danych dokumentów i kolekcji z [klucza partycji](documentdb-partition-data.md#partition-keys) przy użyciu hello [interfejsu API platformy .NET usługi DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2895b-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="2895b-107">Definiując klucza partycji podczas tworzenia kolekcji, aplikacja jest przygotowana tooscale wysiłku, wraz z rozwojem danych.</span><span class="sxs-lookup"><span data-stu-id="2895b-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="2895b-108">Ten samouczek obejmuje hello następujące zadania za pomocą hello [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="2895b-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2895b-109">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2895b-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="2895b-110">Tworzenie bazy danych i kolekcji z użyciem klucza partycji</span><span class="sxs-lookup"><span data-stu-id="2895b-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="2895b-111">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="2895b-111">Create JSON documents</span></span>
> * <span data-ttu-id="2895b-112">Aktualizowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="2895b-112">Update a document</span></span>
> * <span data-ttu-id="2895b-113">Zapytanie względem kolekcji podzielone na partycje</span><span class="sxs-lookup"><span data-stu-id="2895b-113">Query partitioned collections</span></span>
> * <span data-ttu-id="2895b-114">Uruchamianie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="2895b-114">Run stored procedures</span></span>
> * <span data-ttu-id="2895b-115">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="2895b-115">Delete a document</span></span>
> * <span data-ttu-id="2895b-116">Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="2895b-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2895b-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2895b-117">Prerequisites</span></span>
<span data-ttu-id="2895b-118">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2895b-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="2895b-119">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2895b-119">An active Azure account.</span></span> <span data-ttu-id="2895b-120">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2895b-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="2895b-121">Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku, jeśli chcesz toouse środowisko lokalne, które emuluje hello usługi Azure DocumentDB do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="2895b-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="2895b-122">Program [Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="2895b-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="2895b-123">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2895b-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="2895b-124">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2895b-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="2895b-125">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="2895b-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="2895b-126">Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="2895b-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="2895b-127">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="2895b-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="2895b-128">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2895b-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="2895b-129">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2895b-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2895b-130"><a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2895b-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="2895b-131">Otwórz program **Visual Studio** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="2895b-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="2895b-132">Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.</span><span class="sxs-lookup"><span data-stu-id="2895b-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="2895b-133">W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)**, nazwy projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2895b-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="2895b-134">![Zrzut ekranu okna nowy projekt hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="2895b-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="2895b-135">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="2895b-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="2895b-137">W hello **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **documentdb** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2895b-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="2895b-138">W wynikach hello znaleźć **Microsoft.Azure.DocumentDB** i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="2895b-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="2895b-139">Identyfikator pakietu Hello hello biblioteki klienta usługi Azure rozwiązania Cosmos bazy danych jest [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="2895b-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="2895b-140">![Zrzut ekranu przedstawiający hello NuGet Menu do znajdowania zestawu SDK klienta usługi Azure rozwiązania Cosmos bazy danych](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="2895b-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="2895b-141">Jeśli zostanie wyświetlony komunikat o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2895b-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="2895b-142">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="2895b-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="2895b-143"><a id="Connect"></a>Dodawanie odwołań do projektu tooyour</span><span class="sxs-lookup"><span data-stu-id="2895b-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="2895b-144">Witaj pozostałych czynnościach w ramach tego samouczka Podaj hello interfejsu API usługi DocumentDB kodu wstawki wymaganych toocreate i aktualizacji bazy danych Azure rozwiązania Cosmos zasobów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2895b-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="2895b-145">Najpierw dodaj te odwołania tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2895b-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="2895b-146"><a id="add-references"></a>Łączenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="2895b-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="2895b-147">Następnie dodaj te dwie stałe i *klienta* zmiennej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2895b-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="2895b-148">Następnie, head ponownie toohello [portalu Azure](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="2895b-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="2895b-149">adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2895b-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="2895b-150">W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="2895b-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="2895b-151">Skopiuj hello identyfikatora URI z portalu hello i wklej go za pośrednictwem `<your endpoint URL>` w pliku program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="2895b-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="2895b-152">Następnie kopiowania hello klucza podstawowego z portalu hello i wklej go za pośrednictwem `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="2895b-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="2895b-153">Należy się hello tooremove `<` i `>` z własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="2895b-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Zrzut ekranu przedstawiający hello Azure portal używany przez toocreate samouczka NoSQL hello aplikacji konsolowej C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="2895b-156"><a id="instantiate"></a>Utwórz wystąpienie hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="2895b-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="2895b-157">Teraz, Utwórz nowe wystąpienie klasy hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2895b-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="2895b-158"><a id="create-database"></a>Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="2895b-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="2895b-159">Następnie należy utworzyć bazy danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello  **DocumentClient** klasy z hello [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2895b-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2895b-160">Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="2895b-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="2895b-161">Podejmowanie decyzji o klucza partycji</span><span class="sxs-lookup"><span data-stu-id="2895b-161">Decide on a partition key</span></span> 

<span data-ttu-id="2895b-162">Kolekcje są kontenerami do przechowywania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2895b-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="2895b-163">Zasoby logiczne i można je [obejmować co najmniej jednej partycji fizycznej](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="2895b-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="2895b-164">A [klucza partycji](documentdb-partition-data.md) jest właściwość (lub ścieżki) w dokumencie, które jest używane toodistribute danych między serwerami hello lub partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="2895b-165">Wszystkie dokumenty z hello tego samego klucza partycji są przechowywane w hello tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="2895b-166">Określania klucza partycji jest toomake bardzo ważne, aby utworzyć kolekcję.</span><span class="sxs-lookup"><span data-stu-id="2895b-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="2895b-167">Klucze partycji są właściwości (lub ścieżki) w dokumencie, które mogą być używane przez toodistribute bazy danych Azure rozwiązania Cosmos danych między wieloma serwerami lub partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="2895b-168">Rozwiązania cosmos DB skróty hello wartość klucza partycji i używa hello mieszany wynik toodetermine hello partycji w toostore hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2895b-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="2895b-169">Wszystkie dokumenty z hello tego samego klucza partycji są przechowywane w hello tej samej partycji, a klucze partycji nie można zmienić po utworzeniu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2895b-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="2895b-170">W tym samouczku zamierzamy klucza partycji hello tooset zbyt`/deviceId` tak że hello wszystkie dane hello na jednym urządzeniu są przechowywane w jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="2895b-171">Ma toochoose klucza partycji, który ma wiele wartości, które są używane w o hello tooensure częstotliwości tego samego rozwiązania Cosmos DB może równoważyć obciążenie danych rozwoju lub osiągnięcia pełnej przepływności hello hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2895b-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="2895b-172">Aby uzyskać więcej informacji na temat partycjonowania, zobacz [jak toopartition i skali w usłudze Azure DB rozwiązania Cosmos?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="2895b-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="2895b-173"><a id="CreateColl"></a>Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="2895b-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="2895b-174">Teraz, wiemy naszych klucza partycji `/deviceId`, umożliwia tworzenie [kolekcji](documentdb-resources.md#collections) przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="2895b-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2895b-175">Kolekcja jest kontenerem dokumentów JSON i wszelkie skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2895b-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="2895b-176">Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla toocommunicate aplikacji hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2895b-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="2895b-177">Aby uzyskać więcej informacji, odwiedź stronę naszych [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="2895b-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="2895b-178">To sprawia, że metoda interfejsu API REST wywołać tooAzure DB rozwiązania Cosmos i hello liczba partycji na podstawie przepływności żądanego hello przepisów dotyczących usług.</span><span class="sxs-lookup"><span data-stu-id="2895b-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="2895b-179">W razie rozwoju, przy użyciu zestawu SDK hello lub hello potrzeb wydajność można zmienić hello przepływność kolekcji [portalu Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="2895b-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="2895b-180"><a id="CreateDoc"></a>Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="2895b-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="2895b-181">Teraz można wstawić niektórych dokumentów JSON do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2895b-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="2895b-182">A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="2895b-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2895b-183">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="2895b-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2895b-184">Ta klasa próbki zawiera odczytu urządzenia i tooinsert tooCreateDocumentAsync wywołania nowe urządzenie odczytu do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2895b-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a><span data-ttu-id="2895b-185">Odczyt danych</span><span class="sxs-lookup"><span data-stu-id="2895b-185">Read data</span></span>

<span data-ttu-id="2895b-186">Załóżmy odczytu dokumentu hello przez klucz partycji i identyfikator przy użyciu metody ReadDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="2895b-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="2895b-187">Należy pamiętać, że odczyty hello zawierają wartość PartitionKey (odpowiedniego toohello `x-ms-documentdb-partitionkey` nagłówek żądania w hello interfejsu API REST).</span><span class="sxs-lookup"><span data-stu-id="2895b-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="2895b-188">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="2895b-188">Update data</span></span>

<span data-ttu-id="2895b-189">Teraz załóżmy zaktualizować niektóre dane przy użyciu metody ReplaceDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="2895b-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="2895b-190">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="2895b-190">Delete data</span></span>

<span data-ttu-id="2895b-191">Umożliwia teraz usunąć przy użyciu metody DeleteDocumentAsync hello dokumentu przez klucz partycji i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="2895b-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="2895b-192">Zapytanie względem kolekcji podzielone na partycje</span><span class="sxs-lookup"><span data-stu-id="2895b-192">Query partitioned collections</span></span>

<span data-ttu-id="2895b-193">Automatycznie kwerendy danych w kolekcjach podzielonym na partycje, bazy danych Azure rozwiązania Cosmos trasy hello partycji toohello zapytań odpowiadającą wartości klucza partycji toohello określony w filtrze hello (jeśli istnieją).</span><span class="sxs-lookup"><span data-stu-id="2895b-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="2895b-194">Na przykład to zapytanie jest kierowany toojust hello partycji zawierającego hello klucza partycji "XMS 0001".</span><span class="sxs-lookup"><span data-stu-id="2895b-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="2895b-195">Witaj następujące zapytanie nie ma filtr klucza partycji hello (DeviceId) i jest rozwiniętym tooall partycji, którym jest wykonywany przed hello partycjonowania indeksu.</span><span class="sxs-lookup"><span data-stu-id="2895b-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="2895b-196">Należy pamiętać, że program toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` w hello interfejsu API REST) toohave hello SDK tooexecute zapytania na partycje.</span><span class="sxs-lookup"><span data-stu-id="2895b-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="2895b-197">Równoległego wykonywania zapytań</span><span class="sxs-lookup"><span data-stu-id="2895b-197">Parallel query execution</span></span>
<span data-ttu-id="2895b-198">Hello Azure rozwiązania Cosmos bazy danych DocumentDB SDK 1.9.0 i powyżej Obsługa opcje wykonywania zapytania równoległe, umożliwiających tooperform małe opóźnienia zapytanie względem kolekcji partycjonowanych, nawet wtedy, gdy potrzebna jest tootouch dużą liczbę partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="2895b-199">Na przykład hello następującego zapytania jest skonfigurowany toorun równolegle na partycje.</span><span class="sxs-lookup"><span data-stu-id="2895b-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="2895b-200">Możesz zarządzać równoległego wykonywania zapytań przez dostrajanie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2895b-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="2895b-201">Przez ustawienie `MaxDegreeOfParallelism`, można kontrolować hello stopień równoległości, tj. Data hello maksymalną liczbę kolekcji sieci równoczesnych połączeń toohello partycji.</span><span class="sxs-lookup"><span data-stu-id="2895b-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="2895b-202">Jeśli ustawisz to zbyt-1, hello stopień równoległości jest zarządzana przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2895b-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="2895b-203">Jeśli hello `MaxDegreeOfParallelism` nie jest określony lub ustaw too0, która jest wartością domyślną hello, będzie partycje jednej sieci połączenia toohello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2895b-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="2895b-204">Przez ustawienie `MaxBufferedItemCount`, można kompromis wykorzystanie pamięci zapytania opóźnienia i po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="2895b-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="2895b-205">Jeśli ten parametr lub ustaw tę wartość za 1 hello liczbę elementów buforowane podczas równoległego wykonywania zapytań jest zarządzana przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2895b-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="2895b-206">Podane hello niezmienionym hello kolekcji, równoległe zapytania zostanie zwracają wyniki w hello kolejność takie same jak wykonanie szeregowego.</span><span class="sxs-lookup"><span data-stu-id="2895b-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="2895b-207">Podczas wykonywania kwerendy między partycji zawierającej, sortowanie (ORDER BY i/lub góry), hello zestawu SDK usługi DocumentDB wystawia hello zapytania równolegle na partycje i scala częściowo sortowane wyniki w tooproduce po stronie klienta hello globalnie uporządkowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="2895b-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="2895b-208">Wykonanie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="2895b-208">Execute stored procedures</span></span>
<span data-ttu-id="2895b-209">Ponadto można wykonywać transakcje atomic względem dokumentów za pomocą hello tego samego Identyfikatora urządzenia, np. Jeśli jest utrzymanie agreguje lub hello najnowszy stan urządzeń w jednym dokumencie przez dodanie hello następującego projektu tooyour kodu.</span><span class="sxs-lookup"><span data-stu-id="2895b-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="2895b-210">I to już wszystko!</span><span class="sxs-lookup"><span data-stu-id="2895b-210">And that's it!</span></span> <span data-ttu-id="2895b-211">są to hello głównymi składnikami aplikacji bazy danych Azure rozwiązania Cosmos, która używa dystrybucji danych skali tooefficiently klucza partycji na partycje.</span><span class="sxs-lookup"><span data-stu-id="2895b-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="2895b-212">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="2895b-212">Clean up resources</span></span>

<span data-ttu-id="2895b-213">Jeśli nie ma toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego samouczka w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2895b-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="2895b-214">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij przycisk hello unikatową nazwę zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="2895b-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="2895b-215">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2895b-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2895b-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2895b-216">Next steps</span></span>

<span data-ttu-id="2895b-217">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2895b-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2895b-218">Utworzone konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="2895b-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="2895b-219">Utworzony z użyciem klucza partycji bazy danych i kolekcji</span><span class="sxs-lookup"><span data-stu-id="2895b-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="2895b-220">Utworzony dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="2895b-220">Created JSON documents</span></span>
> * <span data-ttu-id="2895b-221">Zaktualizowano dokumentu</span><span class="sxs-lookup"><span data-stu-id="2895b-221">Updated a document</span></span>
> * <span data-ttu-id="2895b-222">Zapytanie kolekcji partycjonowanych</span><span class="sxs-lookup"><span data-stu-id="2895b-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="2895b-223">Uruchomiono procedurę składowaną</span><span class="sxs-lookup"><span data-stu-id="2895b-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="2895b-224">Usunąć dokumentu</span><span class="sxs-lookup"><span data-stu-id="2895b-224">Deleted a document</span></span>
> * <span data-ttu-id="2895b-225">Usunięte z bazy danych</span><span class="sxs-lookup"><span data-stu-id="2895b-225">Deleted a database</span></span>

<span data-ttu-id="2895b-226">Można teraz kontynuować toohello następny samouczek i zaimportować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="2895b-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2895b-227">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2895b-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
