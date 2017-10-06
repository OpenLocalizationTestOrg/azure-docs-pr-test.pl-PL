---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello interfejsu API programu Graph w .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
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
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="cdce0-103">Azure DB rozwiązania Cosmos: Opracowywania hello interfejsu API programu Graph w .NET</span><span class="sxs-lookup"><span data-stu-id="cdce0-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="cdce0-104">Azure DB rozwiązania Cosmos jest usługa globalnie rozproszone wielu modelu bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cdce0-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="cdce0-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdce0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cdce0-106">Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure i jak toocreate wykres bazy danych i kontenera.</span><span class="sxs-lookup"><span data-stu-id="cdce0-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="cdce0-107">następnie aplikacja Hello tworzy prosty sieci społecznościowych cztery osoby korzystające z hello [interfejsu API programu Graph](graph-sdk-dotnet.md) (wersja zapoznawcza), a następnie przechodzi przez i zapytanie hello wykresu przy użyciu Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="cdce0-108">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="cdce0-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdce0-109">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cdce0-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="cdce0-110">Tworzenie bazy danych wykresu i kontenera</span><span class="sxs-lookup"><span data-stu-id="cdce0-110">Create a graph database and container</span></span>
> * <span data-ttu-id="cdce0-111">Serializować obiektów too.NET wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="cdce0-112">Dodaj wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-112">Add vertices and edges</span></span>
> * <span data-ttu-id="cdce0-113">Wykres hello zapytania przy użyciu Gremlin</span><span class="sxs-lookup"><span data-stu-id="cdce0-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="cdce0-114">Wykresy w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="cdce0-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="cdce0-115">Można użyć bazy danych Azure rozwiązania Cosmos toocreate, aktualizacji i wykresy zapytania przy użyciu hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="cdce0-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="cdce0-116">Biblioteka Microsoft.Azure.Graph Hello udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` na powitania `DocumentClient` klasy tooexecute Gremlin zapytania.</span><span class="sxs-lookup"><span data-stu-id="cdce0-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="cdce0-117">Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML).</span><span class="sxs-lookup"><span data-stu-id="cdce0-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="cdce0-118">Firma Microsoft obejmuje kilka przykładów w tym artykule tooget Twojego uruchomiony z Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="cdce0-119">Zobacz [zapytania Gremlin](gremlin-support.md) Aby uzyskać szczegółowe wskazówki Gremlin funkcji dostępnych w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdce0-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cdce0-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cdce0-120">Prerequisites</span></span>
<span data-ttu-id="cdce0-121">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="cdce0-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="cdce0-122">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cdce0-122">An active Azure account.</span></span> <span data-ttu-id="cdce0-123">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cdce0-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="cdce0-124">Alternatywnie można użyć hello [emulatora usługi Azure DocumentDB](local-emulator.md) w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="cdce0-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="cdce0-125">Program [Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="cdce0-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="cdce0-126">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="cdce0-126">Create database account</span></span>

<span data-ttu-id="cdce0-127">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cdce0-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="cdce0-128">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="cdce0-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="cdce0-129">Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="cdce0-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="cdce0-130">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="cdce0-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="cdce0-131">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cdce0-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="cdce0-132">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cdce0-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="cdce0-133"><a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdce0-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="cdce0-134">Otwórz program **Visual Studio** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="cdce0-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="cdce0-135">Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="cdce0-136">W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)**, nazwy projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="cdce0-137">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="cdce0-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="cdce0-138">W hello **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **Microsoft.Azure.Graphs** w polu wyszukiwania hello a hello wyboru **obejmują wersje wstępne**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="cdce0-139">W wynikach hello znaleźć **Microsoft.Azure.Graphs** i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="cdce0-140">Jeśli zostanie wyświetlony komunikat o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="cdce0-141">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="cdce0-142">Witaj `Microsoft.Azure.Graphs` Biblioteka udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` do wykonywania operacji Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="cdce0-143">Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML).</span><span class="sxs-lookup"><span data-stu-id="cdce0-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="cdce0-144">Firma Microsoft obejmuje kilka przykładów w tym artykule tooget Twojego uruchomiony z Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="cdce0-145">[Zapytania gremlin](gremlin-support.md) ma szczegółowy przewodnik na temat możliwości Gremlin w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdce0-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="cdce0-146"><a id="add-references"></a>Łączenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cdce0-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="cdce0-147">Dodaj te dwie stałe i *klienta* zmiennej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdce0-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="cdce0-148">Następnie head kopii toohello [portalu Azure](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="cdce0-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="cdce0-149">adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdce0-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="cdce0-150">W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="cdce0-151">Skopiuj hello identyfikatora URI z portalu hello i wklej go za pośrednictwem `Endpoint` we właściwości punktu końcowego hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="cdce0-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="cdce0-152">Następnie kopiowania hello klucza podstawowego z portalu hello i wklej go do hello `AuthKey` właściwości powyżej.</span><span class="sxs-lookup"><span data-stu-id="cdce0-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="cdce0-153">! [Zrzut ekranu przedstawiający hello Azure portal używany przez samouczek toocreate hello aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="cdce0-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="cdce0-154">Pokazuje hello konta bazy danych Azure rozwiązania Cosmos, przyciskiem KLUCZE wyróżnionym w hello Azure DB rozwiązania Cosmos nawigacji i wartości URI oraz PRIMARY KEY hello wyróżnione na powitania bloku klucze] [klucze]</span><span class="sxs-lookup"><span data-stu-id="cdce0-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="cdce0-155"><a id="instantiate"></a>Utwórz wystąpienie hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="cdce0-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="cdce0-156">Następnie utwórz nowe wystąpienie klasy hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="cdce0-157"><a id="create-database"></a>Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="cdce0-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="cdce0-158">Teraz Utwórz bazę danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello  **DocumentClient** klasy z hello [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cdce0-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="cdce0-159">Tworzenie wykresu.</span><span class="sxs-lookup"><span data-stu-id="cdce0-159">Create a graph</span></span> 

<span data-ttu-id="cdce0-160">Następnie należy utworzyć kontener wykresu przy użyciu hello przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient**  klasy.</span><span class="sxs-lookup"><span data-stu-id="cdce0-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="cdce0-161">Kolekcja jest kontenerem jednostek wykresu.</span><span class="sxs-lookup"><span data-stu-id="cdce0-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="cdce0-162"><a id="serializing"></a>Serializować obiektów too.NET wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="cdce0-163">Azure DB rozwiązania Cosmos używa hello [formacie łańcuchowym GraphSON](gremlin-support.md), który definiuje schematu JSON dla wierzchołków, krawędzie i właściwości.</span><span class="sxs-lookup"><span data-stu-id="cdce0-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="cdce0-164">Hello Azure rozwiązania Cosmos DB .NET SDK zawiera struktury JSON.NET jako zależność, a to pozwala nam tooserialize/deserializacji GraphSON na obiekty .NET, które firma Microsoft może współpracować w kodzie.</span><span class="sxs-lookup"><span data-stu-id="cdce0-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="cdce0-165">Na przykład załóżmy współpracować z prostego sieci społecznościowych z czterech osób.</span><span class="sxs-lookup"><span data-stu-id="cdce0-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="cdce0-166">Opisano, jak toocreate `Person` wierzchołków, Dodaj `Knows` relacji między nimi, a następnie zapytania i przechodzić między nimi hello wykres toofind "friend friend" relacji.</span><span class="sxs-lookup"><span data-stu-id="cdce0-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="cdce0-167">Witaj `Microsoft.Azure.Graphs.Elements` przestrzeń nazw zawiera `Vertex`, `Edge`, `Property` i `VertexProperty` klasy do deserializacji obiektów zdefiniowanych przez toowell .NET programu GraphSON odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="cdce0-168">Uruchom przy użyciu CreateGremlinQuery Gremlin</span><span class="sxs-lookup"><span data-stu-id="cdce0-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="cdce0-169">Gremlin, takiego jak SQL, obsługuje odczytu, zapisu i operacje zapytań.</span><span class="sxs-lookup"><span data-stu-id="cdce0-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="cdce0-170">Na przykład hello poniższy fragment kodu przedstawia sposób toocreate wierzchołków, krawędzi, wykonać niektóre przykładowe zapytania przy użyciu `CreateGremlinQuery<T>`i asynchronicznie iterację te wyniki za pomocą `ExecuteNextAsync` i "HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="cdce0-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="cdce0-171">Dodaj wierzchołki i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-171">Add vertices and edges</span></span>

<span data-ttu-id="cdce0-172">Oto instrukcje Gremlin hello pokazano w powyższej sekcji hello więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="cdce0-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="cdce0-173">Pierwszy możemy niektórych wierzchołków przy użyciu jego Gremlin `addV` metody.</span><span class="sxs-lookup"><span data-stu-id="cdce0-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="cdce0-174">Na przykład hello następujący fragment kodu tworzy wierzchołek "Blogu Thomasa Andersen" typu "Osoba" z właściwości imię i nazwisko, wiek.</span><span class="sxs-lookup"><span data-stu-id="cdce0-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="cdce0-175">Następnie utworzymy niektórych krawędzi między te wierzchołków przy użyciu jego Gremlin `addE` metody.</span><span class="sxs-lookup"><span data-stu-id="cdce0-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="cdce0-176">Możemy zaktualizować istniejące wierzchołków przy użyciu `properties` krok w Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="cdce0-177">Firma Microsoft pominąć hello wywołania tooexecute hello zapytanie przy użyciu `HasMoreResults` i `ExecuteNextAsync` hello pozostałej części hello przykłady.</span><span class="sxs-lookup"><span data-stu-id="cdce0-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="cdce0-178">Można usunąć krawędzi oraz wierzchołków przy użyciu jego Gremlin `drop` kroku.</span><span class="sxs-lookup"><span data-stu-id="cdce0-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="cdce0-179">Oto fragment kodu, który pokazuje sposób toodelete a wierzchołka i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="cdce0-180">Należy pamiętać, że porzucenie wierzchołek wykonuje kaskadowych usunięcie hello skojarzone krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="cdce0-181">Wykres hello zapytania</span><span class="sxs-lookup"><span data-stu-id="cdce0-181">Query hello graph</span></span>

<span data-ttu-id="cdce0-182">Można wykonać zapytania, a także za pomocą Gremlin traversals.</span><span class="sxs-lookup"><span data-stu-id="cdce0-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="cdce0-183">Na przykład powitania po fragment kodu przedstawia, jak toocount hello liczbę wierzchołków w grafie hello:</span><span class="sxs-lookup"><span data-stu-id="cdce0-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="cdce0-184">Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` toobuild bardziej złożone filtry:</span><span class="sxs-lookup"><span data-stu-id="cdce0-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="cdce0-185">Niektóre właściwości hello wyników zapytania za pomocą hello można projektu `values` krok:</span><span class="sxs-lookup"><span data-stu-id="cdce0-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="cdce0-186">Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cdce0-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="cdce0-187">Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy potrzebujesz toonavigate toorelated krawędzi oraz wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="cdce0-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="cdce0-188">Spróbujmy wszystkich znajomych blogu Thomasa.</span><span class="sxs-lookup"><span data-stu-id="cdce0-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="cdce0-189">Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok toofind wszystkie hello wyjściowego krawędzi z blogu Thomasa, a następnie przechodzenie toohello w wierzchołki z tych krawędzi przy użyciu jego Gremlin `inV` krok:</span><span class="sxs-lookup"><span data-stu-id="cdce0-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="cdce0-190">Zapytanie dalej Hello wykonuje dwie toofind przeskoków wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy.</span><span class="sxs-lookup"><span data-stu-id="cdce0-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="cdce0-191">Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, takie jak filtr mieszania hello wyrażenia wykonywania pętli przy użyciu `loop` krok i implementujący nawigacji warunkowego przy użyciu hello `choose` kroku.</span><span class="sxs-lookup"><span data-stu-id="cdce0-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="cdce0-192">Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="cdce0-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="cdce0-193">To wszystko, ten samouczek bazy danych Azure rozwiązania Cosmos została zakończona!</span><span class="sxs-lookup"><span data-stu-id="cdce0-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="cdce0-194">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="cdce0-194">Clean up resources</span></span>

<span data-ttu-id="cdce0-195">Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cdce0-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="cdce0-196">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="cdce0-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="cdce0-197">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="cdce0-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdce0-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdce0-198">Next Steps</span></span>

<span data-ttu-id="cdce0-199">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cdce0-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdce0-200">Utworzone konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="cdce0-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="cdce0-201">Utworzony wykres bazy danych i kontener</span><span class="sxs-lookup"><span data-stu-id="cdce0-201">Created a graph database and container</span></span>
> * <span data-ttu-id="cdce0-202">Obiekty too.NET zserializowane wierzchołków i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="cdce0-203">Dodano wierzchołków i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="cdce0-203">Added vertices and edges</span></span>
> * <span data-ttu-id="cdce0-204">Przy użyciu Gremlin wykresu, którego dotyczy kwerenda hello</span><span class="sxs-lookup"><span data-stu-id="cdce0-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="cdce0-205">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cdce0-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cdce0-206">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="cdce0-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
