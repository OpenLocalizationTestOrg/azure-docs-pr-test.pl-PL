---
title: "Azure rozwiązania Cosmos bazy danych: Interfejs API Graph w .NET opracowywania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzyć aplikacje za pomocą interfejsu API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: eeaa0c4f84a408815371742334d2ba7ce600b72f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-develop-with-the-graph-api-in-net"></a><span data-ttu-id="6cafd-103">Azure rozwiązania Cosmos bazy danych: Interfejs API Graph w .NET opracowywania</span><span class="sxs-lookup"><span data-stu-id="6cafd-103">Azure Cosmos DB: Develop with the Graph API in .NET</span></span>
<span data-ttu-id="6cafd-104">Azure DB rozwiązania Cosmos jest usługa globalnie rozproszone wielu modelu bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6cafd-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="6cafd-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="6cafd-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6cafd-106">W tym samouczku przedstawiono tworzenie konta bazy danych rozwiązania Cosmos Azure przy użyciu portalu Azure oraz do tworzenia bazy danych wykresu i kontenera.</span><span class="sxs-lookup"><span data-stu-id="6cafd-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal and how to create a graph database and container.</span></span> <span data-ttu-id="6cafd-107">Następnie aplikacja tworzy prosty sieci społecznościowych cztery osoby korzystające z [interfejsu API programu Graph](graph-sdk-dotnet.md) (wersja zapoznawcza), a następnie przechodzi przez i zapytanie przy użyciu Gremlin wykresu.</span><span class="sxs-lookup"><span data-stu-id="6cafd-107">The application then creates a simple social network with four people using the [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries the graph using Gremlin.</span></span>

<span data-ttu-id="6cafd-108">Ten samouczek obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6cafd-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6cafd-109">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6cafd-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6cafd-110">Tworzenie bazy danych wykresu i kontenera</span><span class="sxs-lookup"><span data-stu-id="6cafd-110">Create a graph database and container</span></span>
> * <span data-ttu-id="6cafd-111">Serializować wierzchołki i krawędzi obiekty .NET</span><span class="sxs-lookup"><span data-stu-id="6cafd-111">Serialize vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="6cafd-112">Dodaj wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="6cafd-112">Add vertices and edges</span></span>
> * <span data-ttu-id="6cafd-113">Wykres przy użyciu Gremlin zapytania</span><span class="sxs-lookup"><span data-stu-id="6cafd-113">Query the graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="6cafd-114">Wykresy w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="6cafd-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="6cafd-115">Bazy danych rozwiązania Cosmos Azure umożliwia tworzenie, aktualizowanie i zapytania przy użyciu wykresów [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="6cafd-115">You can use Azure Cosmos DB to create, update, and query graphs using the [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="6cafd-116">Biblioteka Microsoft.Azure.Graph udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` nad `DocumentClient` klasy na wykonanie kwerend Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-116">The Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of the `DocumentClient` class to execute Gremlin queries.</span></span>

<span data-ttu-id="6cafd-117">Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML).</span><span class="sxs-lookup"><span data-stu-id="6cafd-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="6cafd-118">Firma Microsoft obejmuje kilka przykładów w tym artykule można pobrać z wprowadzeniem z Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-118">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="6cafd-119">Zobacz [zapytania Gremlin](gremlin-support.md) Aby uzyskać szczegółowe wskazówki Gremlin funkcji dostępnych w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6cafd-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6cafd-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6cafd-120">Prerequisites</span></span>
<span data-ttu-id="6cafd-121">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="6cafd-121">Please make sure you have the following:</span></span>

* <span data-ttu-id="6cafd-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cafd-122">An active Azure account.</span></span> <span data-ttu-id="6cafd-123">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6cafd-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="6cafd-124">Na potrzeby tego samouczka możesz także użyć [emulatora usługi Azure DocumentDB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6cafd-124">Alternatively, you can use the [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="6cafd-125">Program [Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6cafd-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="6cafd-126">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="6cafd-126">Create database account</span></span>

<span data-ttu-id="6cafd-127">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6cafd-127">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="6cafd-128">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="6cafd-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="6cafd-129">Jeśli tak, przejdź do [konfigurowanie rozwiązania Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="6cafd-129">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="6cafd-130">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="6cafd-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="6cafd-131">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu do [konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6cafd-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="6cafd-132">Jeśli używasz emulatora usługi Azure rozwiązania Cosmos bazy danych, wykonaj kroki opisane w temacie [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) skonfigurować emulatora i przejść od razu do [konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="6cafd-132">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="6cafd-133"><a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cafd-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="6cafd-134">Otwórz program **Visual Studio** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="6cafd-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="6cafd-135">W menu **Plik** wybierz polecenie **Nowy**, a następnie wybierz pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-135">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="6cafd-136">W **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)** , nazwę projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-136">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="6cafd-137">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w ramach rozwiązania Visual Studio, a następnie kliknij pozycję **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="6cafd-137">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="6cafd-138">W **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **Microsoft.Azure.Graphs** w polu wyszukiwania, a także sprawdź **obejmują wersje wstępne**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-138">In the **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in the search box, and check the **Include prerelease versions**.</span></span>
6. <span data-ttu-id="6cafd-139">W wynikach, Znajdź **Microsoft.Azure.Graphs** i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-139">Within the results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="6cafd-140">Jeśli zostanie wyświetlony komunikat dotyczący przejrzenia zmian wprowadzonych w rozwiązaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-140">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="6cafd-141">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="6cafd-142">`Microsoft.Azure.Graphs` Biblioteka udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` do wykonywania operacji Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-142">The `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="6cafd-143">Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML).</span><span class="sxs-lookup"><span data-stu-id="6cafd-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="6cafd-144">Firma Microsoft obejmuje kilka przykładów w tym artykule można pobrać z wprowadzeniem z Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-144">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="6cafd-145">[Zapytania gremlin](gremlin-support.md) ma szczegółowy przewodnik na temat możliwości Gremlin w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6cafd-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="6cafd-146"><a id="add-references"></a>Łączenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="6cafd-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="6cafd-147">Dodaj te dwie stałe i *klienta* zmiennej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cafd-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="6cafd-148">Następnie z powrotem do head [portalu Azure](https://portal.azure.com) można pobrać adresu URL punktu końcowego, a klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6cafd-148">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="6cafd-149">Adres URL punktu końcowego i klucz podstawowy są niezbędne, aby aplikacja wiedziała, z jakim elementem ma się połączyć, oraz aby usługa Azure Cosmos DB ufała połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6cafd-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> 

<span data-ttu-id="6cafd-150">W portalu Azure, przejdź do swojego konta bazy danych rozwiązania Cosmos platformy Azure, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="6cafd-151">Skopiuj identyfikator URI z portalu i wklej go za pośrednictwem `Endpoint` we właściwości punktu końcowego powyżej.</span><span class="sxs-lookup"><span data-stu-id="6cafd-151">Copy the URI from the portal and paste it over `Endpoint` in the endpoint property above.</span></span> <span data-ttu-id="6cafd-152">Następnie skopiuj podstawowy klucz z portalu i wklej ją do `AuthKey` właściwości powyżej.</span><span class="sxs-lookup"><span data-stu-id="6cafd-152">Then copy the PRIMARY KEY from the portal and paste it into the `AuthKey` property above.</span></span> 

<span data-ttu-id="6cafd-153">! [Zrzut ekranu przedstawiający portal Azure używany przez samouczek tworzenia aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="6cafd-153">![Screen shot of the Azure portal used by the tutorial to create a C# application.</span></span> <span data-ttu-id="6cafd-154">Pokazuje bazy danych Azure rozwiązania Cosmos konta, przyciskiem KLUCZE wyróżnionym w nawigacji bazy danych Azure rozwiązania Cosmos i wartości URI oraz PRIMARY KEY wyróżnionym w bloku klucze] [klucze]</span><span class="sxs-lookup"><span data-stu-id="6cafd-154">Shows an Azure Cosmos DB account the KEYS button highlighted on the Azure Cosmos DB navigation , and the URI and PRIMARY KEY values highlighted on the Keys blade][keys]</span></span> 
 
## <span data-ttu-id="6cafd-155"><a id="instantiate"></a>Utwórz wystąpienie obiektu DocumentClient</span><span class="sxs-lookup"><span data-stu-id="6cafd-155"><a id="instantiate"></a>Instantiate the DocumentClient</span></span> 
<span data-ttu-id="6cafd-156">Następnie utwórz nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-156">Next, create a new instance of the **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="6cafd-157"><a id="create-database"></a>Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="6cafd-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="6cafd-158">Teraz Utwórz bazę danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) za pomocą [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody  **DocumentClient** klasę z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6cafd-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="6cafd-159">Tworzenie wykresu.</span><span class="sxs-lookup"><span data-stu-id="6cafd-159">Create a graph</span></span> 

<span data-ttu-id="6cafd-160">Następnie należy utworzyć kontener wykresu przy użyciu przy użyciu [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="6cafd-160">Next, create a graph container by using the using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="6cafd-161">Kolekcja jest kontenerem jednostek wykresu.</span><span class="sxs-lookup"><span data-stu-id="6cafd-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="6cafd-162"><a id="serializing"></a>Serializować wierzchołki i krawędzi obiekty .NET</span><span class="sxs-lookup"><span data-stu-id="6cafd-162"><a id="serializing"></a>Serialize vertices and edges to .NET objects</span></span>
<span data-ttu-id="6cafd-163">Używa Azure DB rozwiązania Cosmos [formacie łańcuchowym GraphSON](gremlin-support.md), który definiuje schematu JSON dla wierzchołków, krawędzie i właściwości.</span><span class="sxs-lookup"><span data-stu-id="6cafd-163">Azure Cosmos DB uses the [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="6cafd-164">Zestaw .NET SDK usługi Azure rozwiązania Cosmos DB zawiera struktury JSON.NET jako zależność i pozwala na serializacji/deserializacji GraphSON na obiekty .NET, które firma Microsoft może współpracować w kodzie.</span><span class="sxs-lookup"><span data-stu-id="6cafd-164">The Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us to serialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="6cafd-165">Na przykład załóżmy współpracować z prostego sieci społecznościowych z czterech osób.</span><span class="sxs-lookup"><span data-stu-id="6cafd-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="6cafd-166">Opisano, jak utworzyć `Person` wierzchołków, Dodaj `Knows` relacji między nimi, a następnie zapytań i przechodzenia wykres można znaleźć relacji "friend friend".</span><span class="sxs-lookup"><span data-stu-id="6cafd-166">We look at how to create `Person` vertices, add `Knows` relationships between them, then query and traverse the graph to find "friend of friend" relationships.</span></span> 

<span data-ttu-id="6cafd-167">`Microsoft.Azure.Graphs.Elements` Przestrzeń nazw zawiera `Vertex`, `Edge`, `Property` i `VertexProperty` klasy do deserializacji odpowiedzi GraphSON dobrze zdefiniowany obiekty .NET.</span><span class="sxs-lookup"><span data-stu-id="6cafd-167">The `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses to well-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="6cafd-168">Uruchom przy użyciu CreateGremlinQuery Gremlin</span><span class="sxs-lookup"><span data-stu-id="6cafd-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="6cafd-169">Gremlin, takiego jak SQL, obsługuje odczytu, zapisu i operacje zapytań.</span><span class="sxs-lookup"><span data-stu-id="6cafd-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="6cafd-170">Na przykład poniższy fragment kodu przedstawia sposób tworzenia wierzchołków, krawędzi, wykonać niektóre przykładowe zapytania przy użyciu `CreateGremlinQuery<T>`i asynchronicznie iterację te wyniki za pomocą `ExecuteNextAsync` i "HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="6cafd-170">For example, the following snippet shows how to create vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="6cafd-171">Dodaj wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="6cafd-171">Add vertices and edges</span></span>

<span data-ttu-id="6cafd-172">Oto instrukcje Gremlin wyświetlany w poprzedniej sekcji więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="6cafd-172">Let's look at the Gremlin statements shown in the preceding section more detail.</span></span> <span data-ttu-id="6cafd-173">Pierwszy możemy niektórych wierzchołków przy użyciu jego Gremlin `addV` metody.</span><span class="sxs-lookup"><span data-stu-id="6cafd-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="6cafd-174">Na przykład poniższy fragment kodu tworzy wierzchołek "Blogu Thomasa Andersen" typu "Osoba" z właściwości imię i nazwisko, wiek.</span><span class="sxs-lookup"><span data-stu-id="6cafd-174">For example, the following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="6cafd-175">Następnie utworzymy niektórych krawędzi między te wierzchołków przy użyciu jego Gremlin `addE` metody.</span><span class="sxs-lookup"><span data-stu-id="6cafd-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="6cafd-176">Możemy zaktualizować istniejące wierzchołków przy użyciu `properties` krok w Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="6cafd-177">Firma Microsoft pominąć wywołania do wykonania zapytania za pomocą `HasMoreResults` i `ExecuteNextAsync` dla pozostałych przykładach.</span><span class="sxs-lookup"><span data-stu-id="6cafd-177">We skip the call to execute the query via `HasMoreResults` and `ExecuteNextAsync` for the rest of the examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="6cafd-178">Można usunąć krawędzi oraz wierzchołków przy użyciu jego Gremlin `drop` kroku.</span><span class="sxs-lookup"><span data-stu-id="6cafd-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="6cafd-179">Oto fragment, pokazujący sposób usuwania wierzchołek i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="6cafd-179">Here's a snippet that shows how to delete a vertex and an edge.</span></span> <span data-ttu-id="6cafd-180">Należy pamiętać, że porzucenie wierzchołek wykonuje kaskadowych Usuń skojarzone krawędzi.</span><span class="sxs-lookup"><span data-stu-id="6cafd-180">Note that dropping a vertex performs a cascading delete of the associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-the-graph"></a><span data-ttu-id="6cafd-181">Zapytanie wykresu</span><span class="sxs-lookup"><span data-stu-id="6cafd-181">Query the graph</span></span>

<span data-ttu-id="6cafd-182">Można wykonać zapytania, a także za pomocą Gremlin traversals.</span><span class="sxs-lookup"><span data-stu-id="6cafd-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="6cafd-183">Na przykład poniższy fragment kodu przedstawia sposób liczbę wierzchołki na wykresie:</span><span class="sxs-lookup"><span data-stu-id="6cafd-183">For example, the following snippet shows how to count the number of vertices in the graph:</span></span>

```cs
// Run a query to count vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="6cafd-184">Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` do tworzenia bardziej złożonych filtrów:</span><span class="sxs-lookup"><span data-stu-id="6cafd-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="6cafd-185">Niektóre właściwości wyników zapytania za pomocą można projektu `values` krok:</span><span class="sxs-lookup"><span data-stu-id="6cafd-185">You can project certain properties in the query results using the `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="6cafd-186">Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6cafd-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="6cafd-187">Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy musisz przejść do krawędzi pokrewne i wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="6cafd-187">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="6cafd-188">Spróbujmy wszystkich znajomych blogu Thomasa.</span><span class="sxs-lookup"><span data-stu-id="6cafd-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="6cafd-189">Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok, aby znaleźć wszystkie wyjściowego krawędzi blogu Thomasa, a następnie przechodzenie do wierzchołków w z tych krawędzi przy użyciu jego Gremlin `inV` krok:</span><span class="sxs-lookup"><span data-stu-id="6cafd-189">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="6cafd-190">Zapytanie dalej wykonuje dwie przeskoków w celu znalezienia wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy.</span><span class="sxs-lookup"><span data-stu-id="6cafd-190">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="6cafd-191">Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, tym wyrażeniach filtru mieszanie wykonywania pętli przy użyciu `loop` krok i wykonawcze przy użyciu warunkowego nawigacji `choose` kroku.</span><span class="sxs-lookup"><span data-stu-id="6cafd-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="6cafd-192">Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="6cafd-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="6cafd-193">To wszystko, ten samouczek bazy danych Azure rozwiązania Cosmos została zakończona!</span><span class="sxs-lookup"><span data-stu-id="6cafd-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="6cafd-194">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="6cafd-194">Clean up resources</span></span>

<span data-ttu-id="6cafd-195">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="6cafd-195">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>  

1. <span data-ttu-id="6cafd-196">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6cafd-196">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="6cafd-197">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="6cafd-197">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cafd-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cafd-198">Next Steps</span></span>

<span data-ttu-id="6cafd-199">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6cafd-199">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6cafd-200">Utworzone konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="6cafd-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="6cafd-201">Utworzony wykres bazy danych i kontener</span><span class="sxs-lookup"><span data-stu-id="6cafd-201">Created a graph database and container</span></span>
> * <span data-ttu-id="6cafd-202">Zserializowany wierzchołki i krawędzi obiekty .NET</span><span class="sxs-lookup"><span data-stu-id="6cafd-202">Serialized vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="6cafd-203">Dodano wierzchołków i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="6cafd-203">Added vertices and edges</span></span>
> * <span data-ttu-id="6cafd-204">Zapytanie wykresu przy użyciu Gremlin</span><span class="sxs-lookup"><span data-stu-id="6cafd-204">Queried the graph using Gremlin</span></span>

<span data-ttu-id="6cafd-205">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="6cafd-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cafd-206">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="6cafd-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
