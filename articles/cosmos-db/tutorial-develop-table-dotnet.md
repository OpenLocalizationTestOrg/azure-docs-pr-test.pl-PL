---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello tabeli interfejs API .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API tabeli DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="8aa3c-103">Azure DB rozwiązania Cosmos: Opracowywania hello tabeli interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="8aa3c-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="8aa3c-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8aa3c-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="8aa3c-106">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="8aa3c-107">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8aa3c-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="8aa3c-108">Włączanie funkcji w pliku app.config hello</span><span class="sxs-lookup"><span data-stu-id="8aa3c-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="8aa3c-109">Utwórz tabelę przy użyciu hello [API tabeli](table-introduction.md) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8aa3c-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="8aa3c-110">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="8aa3c-111">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="8aa3c-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="8aa3c-112">Pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="8aa3c-113">Przy użyciu automatycznego indeksów pomocniczych podmiotów zapytania</span><span class="sxs-lookup"><span data-stu-id="8aa3c-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="8aa3c-114">Zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-114">Replace an entity</span></span> 
> * <span data-ttu-id="8aa3c-115">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-115">Delete an entity</span></span> 
> * <span data-ttu-id="8aa3c-116">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="8aa3c-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="8aa3c-117">Tabele Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="8aa3c-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="8aa3c-118">Azure DB rozwiązania Cosmos zapewnia hello [API tabeli](table-introduction.md) (wersja zapoznawcza) dla aplikacji, które muszą magazyn kluczy i wartości, z projektem bez schematu.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="8aa3c-119">[Magazyn tabel Azure](../storage/common/storage-introduction.md) zestawy SDK i interfejsów API REST mogą być używane toowork z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="8aa3c-120">Wymagania wysokiej przepływności, mogą używać bazy danych Azure rozwiązania Cosmos toocreate tabel.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="8aa3c-121">Usługa Azure Cosmos DB obsługuje tabele o zoptymalizowanej przepływności (nazywane nieformalnie „tabelami premium”), dostępne obecnie w publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="8aa3c-122">Można kontynuować toouse magazynu tabel Azure dla tabel z magazynu wysokiej i niższe wymagania przepływności.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="8aa3c-123">Azure DB rozwiązania Cosmos wprowadzi pomocy technicznej dla tabel zoptymalizowanych pod kątem pamięci masowej w przyszłej aktualizacji, i istniejących i nowych tabel Azure, konta magazynu będzie można bezproblemowo uaktualnić tooAzure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="8aa3c-124">Jeśli obecnie używasz magazynu tabel Azure, uzyskasz następujące korzyści z wersji zapoznawczej "Tabela premium" hello hello:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="8aa3c-125">Gotowe [globalne dystrybucji](distribute-data-globally.md) z wielu i [automatycznej i ręcznej pracy awaryjnej.](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8aa3c-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="8aa3c-126">Obsługa automatycznego schematu niezwiązane z żadnym indeksowania względem wszystkich właściwości ("indeksów pomocniczych") i szybkie zapytań</span><span class="sxs-lookup"><span data-stu-id="8aa3c-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="8aa3c-127">Obsługa [niezależne skalowanie pamięci masowej i przepływność](partition-data.md), przez dowolną liczbę regionów</span><span class="sxs-lookup"><span data-stu-id="8aa3c-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="8aa3c-128">Obsługa [dedykowanych przepływności na tabelę](request-units.md) mogą być skalowane z setkami toomillions żądań na sekundę</span><span class="sxs-lookup"><span data-stu-id="8aa3c-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="8aa3c-129">Obsługa [pięć dostosowywalne poziomy spójności](consistency-levels.md) tootrade poza dostępności, opóźnienia i spójności w oparciu wymagań aplikacji</span><span class="sxs-lookup"><span data-stu-id="8aa3c-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="8aa3c-130">dostępność 99,99% w pojedynczym regionie i możliwości tooadd więcej regionów potrzeby wyższej dostępności i [SLA kompleksowe branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/) w ogólnodostępnej</span><span class="sxs-lookup"><span data-stu-id="8aa3c-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="8aa3c-131">Praca z istniejącego magazynu Azure hello zestawu .NET SDK i żadna aplikacja tooyour zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="8aa3c-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="8aa3c-132">Witaj wersji zapoznawczej obsługuje bazy danych Azure rozwiązania Cosmos hello tabeli interfejsu API przy użyciu zestawu .NET SDK hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="8aa3c-133">Możesz pobrać hello [zestawu SDK w wersji zapoznawczej usługi Magazyn Azure](https://aka.ms/premiumtablenuget) z pakietu NuGet, która ma hello tej samej klasy i metody podpisy jako hello [zestawu SDK usługi Magazyn Azure](https://www.nuget.org/packages/WindowsAzure.Storage), ale także podłączyć tooAzure DB rozwiązania Cosmos kont przy użyciu hello Tabela interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="8aa3c-134">toolearn więcej informacji na temat skomplikowanych zadaniach magazynu tabel Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="8aa3c-135">Wprowadzenie tooAzure DB rozwiązania Cosmos: Tabela interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8aa3c-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="8aa3c-136">Witaj dokumentację referencyjną usługi tabel, aby uzyskać szczegółowe informacje o dostępnych interfejsach API [biblioteki klienta usługi Storage dla platformy .NET odwołania](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="8aa3c-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="8aa3c-137">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="8aa3c-137">About this tutorial</span></span>
<span data-ttu-id="8aa3c-138">W tym samouczku jest dla deweloperów, którzy są zaznajomieni z programem hello magazynu tabel Azure SDK i chcesz toouse hello premium funkcje dostępne przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="8aa3c-139">Jest on oparty na [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](table-storage-how-to-use-dotnet.md) i pokazuje, jak tootake korzystać z dodatkowych funkcji, takich jak indeksów pomocniczych, udostępnionej przepływności i wielu.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="8aa3c-140">Firma Microsoft opisano, jak toouse hello Azure toocreate portalu konta usługi Azure DB rozwiązania Cosmos, a następnie tworzenie i wdrażanie aplikacji tabeli.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="8aa3c-141">Przeprowadzenie możemy również przykłady .NET do tworzenia i usuwania tabeli, wstawianie, aktualizowanie, usuwanie i przeszukiwaniem danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="8aa3c-142">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="8aa3c-143">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="8aa3c-144">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="8aa3c-144">Create a database account</span></span>

<span data-ttu-id="8aa3c-145">Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="8aa3c-146">Masz już konto bazy danych rozwiązania Cosmos Azure?</span><span class="sxs-lookup"><span data-stu-id="8aa3c-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="8aa3c-147">Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="8aa3c-148">Czy miał konto usługi Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="8aa3c-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="8aa3c-149">Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="8aa3c-150">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="8aa3c-151">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8aa3c-151">Clone hello sample application</span></span>

<span data-ttu-id="8aa3c-152">Teraz załóżmy sklonować aplikacji przez tabelę z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="8aa3c-153">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="8aa3c-154">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="8aa3c-155">Następnie otwórz plik rozwiązania hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="8aa3c-156">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="8aa3c-156">Update your connection string</span></span>

<span data-ttu-id="8aa3c-157">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="8aa3c-158">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="8aa3c-159">Użyjesz przyciski Kopia hello po prawej stronie powitania ciąg hello ekranu toocopy hello połączenia w pliku app.config hello hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="8aa3c-160">W programie Visual Studio Otwórz plik app.config hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="8aa3c-161">Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość klucz konta hello w pliku app.config. Użyj nazwy konta hello utworzony wcześniej dla nazwy konta w pliku app.config.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="8aa3c-162">toouse tę aplikację z magazynem tabel Azure standardowe, należy w ciągu połączenia hello toochange `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="8aa3c-163">Użyj nazwy konta hello jako nazwa tabeli konta i klucz jako klucz podstawowy magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="8aa3c-164">Tworzenie i wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="8aa3c-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="8aa3c-165">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="8aa3c-166">W hello NuGet **Przeglądaj** wpisz ***WindowsAzure.Storage PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="8aa3c-167">Sprawdź **obejmują wersje wstępne**.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="8aa3c-168">Wyniki hello zainstalować hello **WindowsAzure.Storage PremiumTable** i wybierz polecenie kompilacji w wersji zapoznawczej hello `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="8aa3c-169">Ta akcja instaluje pakiet magazynu tabel Azure hello oraz wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="8aa3c-170">Kliknij polecenie CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="8aa3c-171">Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracować z danymi w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="8aa3c-172">toouse tę aplikację w emulatorze Azure rozwiązania Cosmos bazy danych, możesz po prostu wymagane w ciągu połączenia hello toochange `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="8aa3c-173">Użyj hello poniżej wartości dla emulatora.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="8aa3c-174">Możliwości platformy Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="8aa3c-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="8aa3c-175">Azure DB rozwiązania Cosmos obsługuje wiele funkcji, które nie są dostępne w hello magazynu tabel Azure interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="8aa3c-176">Witaj nową funkcję można włączyć za pomocą następujących hello `appSettings` wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="8aa3c-177">Nie wprowadzeniu wszelkie nowe sygnatury przeciążenia toohello podglądu lub zestawu SDK usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="8aa3c-178">Dzięki temu można tooconnect tooboth standard i premium tabel i pracy z innymi usługami Azure Storage, takich jak obiekty BLOB i kolejki.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="8aa3c-179">Klucz</span><span class="sxs-lookup"><span data-stu-id="8aa3c-179">Key</span></span> | <span data-ttu-id="8aa3c-180">Opis</span><span class="sxs-lookup"><span data-stu-id="8aa3c-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa3c-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="8aa3c-181">TableConnectionMode</span></span>  | <span data-ttu-id="8aa3c-182">Azure DB rozwiązania Cosmos obsługuje dwa tryby łączności.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="8aa3c-183">W `Gateway` tryb, żądania są zawsze wykonywane toohello bazy danych Azure rozwiązania Cosmos bramy, który przekazuje on toohello odpowiednich danych partycji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="8aa3c-184">W `Direct` tryb łączności powitania klienta pobiera mapowanie hello toopartitions tabel i żądań bezpośrednio przed partycji danych.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="8aa3c-185">Firma Microsoft zaleca `Direct`, hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="8aa3c-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="8aa3c-186">TableConnectionProtocol</span></span> | <span data-ttu-id="8aa3c-187">Azure DB rozwiązania Cosmos obsługuje dwa protokoły połączenia - `Https` i `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="8aa3c-188">`Tcp`jest domyślną hello i zalecane, ponieważ jest bardziej lightweight.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="8aa3c-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="8aa3c-189">TablePreferredLocations</span></span> | <span data-ttu-id="8aa3c-190">Rozdzielaną przecinkami listę preferowanych (podłączonej do wielu sieci) lokalizacji odczytów.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="8aa3c-191">Każde konto bazy danych rozwiązania Cosmos Azure może być skojarzony z 1-30 + regionów.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="8aa3c-192">Każde wystąpienie klienta można określić podzbiór tych regionów hello preferowane aby odczyty małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="8aa3c-193">regiony Hello muszą nosić przy użyciu ich [wyświetlane nazwy](https://msdn.microsoft.com/library/azure/gg441293.aspx), na przykład `West US`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="8aa3c-194">Zobacz też [wielu interfejsów API](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="8aa3c-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="8aa3c-195">TableConsistencyLevel</span></span> | <span data-ttu-id="8aa3c-196">Można kompromis między dostępności opóźnienia, spójność i wybierając pięć dobrze zdefiniowane poziomy spójności: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, i `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="8aa3c-197">Domyślnie jest `Session`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-197">Default is `Session`.</span></span> <span data-ttu-id="8aa3c-198">Wybór Hello poziomu spójności sprawia, że różnica znaczących wydajności w konfiguracji w przypadku.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="8aa3c-199">Zobacz [poziomy spójności](consistency-levels.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="8aa3c-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="8aa3c-200">TableThroughput</span></span> | <span data-ttu-id="8aa3c-201">Zarezerwowaną przepływnością dla tabeli hello wyrażona w jednostkach żądań (RU) na sekundę.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="8aa3c-202">Tabele pojedynczego może obsługiwać miliony 100s RU/s.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="8aa3c-203">Zobacz [jednostek żądania](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="8aa3c-204">Domyślnie`400`</span><span class="sxs-lookup"><span data-stu-id="8aa3c-204">Default is `400`</span></span> |
| <span data-ttu-id="8aa3c-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="8aa3c-205">TableIndexingPolicy</span></span> | <span data-ttu-id="8aa3c-206">Spójne i automatyczne dodatkowej indeksowania wszystkie kolumny w tabeli</span><span class="sxs-lookup"><span data-stu-id="8aa3c-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="8aa3c-207">JSON ciąg zgodnych toohello indeksowania specyfikacji zasad.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="8aa3c-208">Zobacz [zasady indeksowania](indexing-policies.md) toosee sposób zmiany indeksowania zasad tooinclude/wykluczania określonych kolumn.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="8aa3c-209">Automatyczne indeksowanie wszystkich właściwości (skrót ciągi), a zakres numerów</span><span class="sxs-lookup"><span data-stu-id="8aa3c-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="8aa3c-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="8aa3c-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="8aa3c-211">Skonfiguruj maksymalną liczbę elementów zwróconych dla tabeli kwerendy w jednym cyklu hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="8aa3c-212">Domyślnie jest `-1`, który umożliwia Azure DB rozwiązania Cosmos dynamiczne określanie wartości hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="8aa3c-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="8aa3c-213">TableQueryEnableScan</span></span> | <span data-ttu-id="8aa3c-214">Jeśli zapytanie hello nie można użyć hello indeksu dla dowolny filtr, uruchom ją mimo to za pomocą skanowania.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="8aa3c-215">Domyślnie jest `false`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-215">Default is `false`.</span></span>|
| <span data-ttu-id="8aa3c-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="8aa3c-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="8aa3c-217">Witaj stopień równoległości do wykonania zapytania różnych partycji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="8aa3c-218">`0`jest szeregowe z nie pobierania, `1` jest szeregowe z pobierania i wyższe wartości wzrostu hello stopień równoległości.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="8aa3c-219">Domyślnie jest `-1`, który umożliwia Azure DB rozwiązania Cosmos dynamiczne określanie wartości hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="8aa3c-220">Wartość domyślna hello toochange, otwórz hello `app.config` plików w Eksploratorze rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="8aa3c-221">Dodaj zawartość hello hello `<appSettings>` widocznego poniżej.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="8aa3c-222">Zastąp `account-name` hello nazwą konta magazynu i `account-key` kluczem dostępu do konta.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="8aa3c-223">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="8aa3c-224">Otwórz hello `Program.cs` plików i można znaleźć, te wiersze kodu utworzyć hello tabeli zasobów.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="8aa3c-225">Utwórz powitania klienta tabeli</span><span class="sxs-lookup"><span data-stu-id="8aa3c-225">Create hello table client</span></span>
<span data-ttu-id="8aa3c-226">Możesz zainicjować `CloudTableClient` tooconnect toohello tabeli konta.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="8aa3c-227">Ten klient został zainicjowany przy użyciu hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, i `TablePreferredLocations` wartości konfiguracji, jeśli określony w ustawieniach aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="8aa3c-228">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="8aa3c-228">Create a table</span></span>
<span data-ttu-id="8aa3c-229">Następnie można utworzyć tabeli za pomocą `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="8aa3c-230">Tabele w bazie danych rozwiązania Cosmos Azure mogą być skalowane niezależnie pod względem pamięci masowej i przepływność i podziału na partycje odbywa się automatycznie przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="8aa3c-231">Azure DB rozwiązania Cosmos obsługuje zarówno o stałym rozmiarze i nieograniczoną liczbę tabel.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="8aa3c-232">Zobacz [partycjonowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="8aa3c-233">Brak istotną różnicą w sposób tworzenia tabel.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="8aa3c-234">Azure DB rozwiązania Cosmos rezerwuje przepływności, w przeciwieństwie do magazynu Azure na podstawie zużycia modelu dla transakcji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="8aa3c-235">model rezerwacji Hello ma dwie kluczowe korzyści:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="8aa3c-236">Przepustowość sieci jest w wersji dedykowanej/zarezerwowana, więc można nigdy nie pobrać ograniczany Jeśli częstotliwość żądania jest poziomie lub poniżej z udostępnionej przepływności</span><span class="sxs-lookup"><span data-stu-id="8aa3c-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="8aa3c-237">model rezerwacji Hello jest więcej [ekonomiczne w przypadku obciążeń intensywnie przepływności](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="8aa3c-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="8aa3c-238">Można skonfigurować przepływności domyślne hello przez skonfigurowanie ustawienia hello dla `TableThroughput` pod względem RU (jednostki żądania) na sekundę.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="8aa3c-239">Odczyt jednostki 1 KB jest znormalizowany jako 1 RU i inne operacje są znormalizowane tooa stałej wartości RU oparte na ich użycie procesora CPU, pamięci i IOPS.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="8aa3c-240">Dowiedz się więcej o [jednostek w usłudze Azure DB rozwiązania Cosmos żądania](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="8aa3c-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8aa3c-241">Podczas gdy magazyn tabel zestawu SDK nie obsługuje obecnie modyfikowanie przepływności, można zmienić przepływności hello natychmiast w dowolnym momencie przy użyciu hello portalu Azure lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="8aa3c-242">Następnie możemy przeprowadzenie odczytu prostego powitania i zapisu (CRUD) przy użyciu magazynu tabel Azure hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="8aa3c-243">W tym samouczku przedstawiono przewidywalną niski milisekund jednocyfrowej opóźnienia i szybkie zapytania pochodzącymi z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8aa3c-244">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-244">Add an entity tooa table</span></span>
<span data-ttu-id="8aa3c-245">Jednostki w magazynie tabel Azure rozszerza z hello `TableEntity` klasy i musi mieć `PartitionKey` i `RowKey` właściwości.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="8aa3c-246">Oto przykład definicji jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="8aa3c-247">powitania po fragment kodu przedstawia, jak tooinsert jednostki z hello magazynu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="8aa3c-248">Azure DB rozwiązania Cosmos jest przeznaczona dla gwarantowane małe opóźnienia w dowolnej skali między hello world.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="8aa3c-249">Ukończenie operacji zapisu < 15 ms p99 i ms ~ 6 w p50 aplikacji uruchomionych na hello tego samego regionu hello konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="8aa3c-250">I ten czas trwania kont faktu hello, który zapisuje są wstecz toohello klienta dopiero po ich są synchronicznie replikowane, trwale zatwierdzone, i całą jego zawartość jest indeksowana.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="8aa3c-251">Witaj API tabeli dla bazy danych Azure rozwiązania Cosmos jest w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="8aa3c-252">Ogólnie gwarancje opóźnienia p99 hello bazują na umów SLA, takich jak innych interfejsów API Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8aa3c-253">Zbiorcze wstawianie jednostek</span><span class="sxs-lookup"><span data-stu-id="8aa3c-253">Insert a batch of entities</span></span>
<span data-ttu-id="8aa3c-254">Azure tabeli magazynu obsługuje interfejs API operacji partii, który umożliwia łączenie aktualizowanie i usuwanie, i wstawia w hello tego samego pojedynczej operacji zbiorczej.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="8aa3c-255">Azure DB rozwiązania Cosmos nie ma niektórych ograniczeń hello na interfejsu API partii hello jako magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="8aa3c-256">Na przykład można wykonywać wielu odczytów w partii, można wykonywać wiele toohello zapisy tej samej jednostki w partii, a nie ma żadnego limitu na 100 operacje na partię.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="8aa3c-257">Pobieranie pojedynczej jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-257">Retrieve a single entity</span></span>
<span data-ttu-id="8aa3c-258">Pobiera (pobiera) w usłudze Azure DB rozwiązania Cosmos pełną < 10 ms p99 i ~ 1 ms na p50 w hello tego samego regionu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="8aa3c-259">Dodaj tyle konta tooyour regiony dla odczytów małe opóźnienia i wdrożyć aplikacje tooread z ich lokalnego regionu ("wieloadresowej") przez ustawienie `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="8aa3c-260">Można pobrać pojedynczą jednostką przy użyciu następującego fragmentu hello:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="8aa3c-261">Dowiedz się więcej o wielu interfejsów API w [programowania z użyciem wielu regionów](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="8aa3c-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="8aa3c-262">Przy użyciu automatycznego indeksów pomocniczych podmiotów zapytania</span><span class="sxs-lookup"><span data-stu-id="8aa3c-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="8aa3c-263">Tabele mogą być przeszukiwane przy użyciu hello `TableQuery` klasy.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="8aa3c-264">Azure DB rozwiązania Cosmos ma aparat zoptymalizowanych pod kątem zapisu bazy danych, który automatycznie indeksuje wszystkie kolumny w tabeli.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="8aa3c-265">Indeksowanie w usłudze Azure DB rozwiązania Cosmos jest niezależny tooschema.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="8aa3c-266">W związku z tym nawet jeśli schemat różni się od wierszy lub schematu hello rozwoju wraz z upływem czasu, jest automatycznie indeksowane.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="8aa3c-267">Ponieważ bazy danych rozwiązania Cosmos Azure obsługuje automatyczne indeksów pomocniczych, zapytań dotyczących dowolnej właściwości można użyć indeksu hello i obsłużona wydajnie.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="8aa3c-268">Podgląd bazy danych rozwiązania Cosmos Azure obsługuje hello zapytania takie same funkcje co magazyn tabel Azure dla hello tabeli interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="8aa3c-269">Azure DB rozwiązania Cosmos obsługuje również sortowanie, agregacje, dane geograficzne zapytania hierarchii i szeroki zakres funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="8aa3c-270">dodatkowe funkcje Hello zostanie podany w hello tabeli interfejsu API w przyszłej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="8aa3c-271">Zobacz [kwerendy bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md) omówienie tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="8aa3c-272">Zastępowanie jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-272">Replace an entity</span></span>
<span data-ttu-id="8aa3c-273">tooupdate jednostki, pobrać hello usługi tabel, zmodyfikuj obiekt jednostki hello i następnie zapisz zmiany hello ponownie toohello usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="8aa3c-274">Witaj poniższy kod zmienia numer telefonu istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="8aa3c-275">Podobnie można wykonywać `InsertOrMerge` lub `Merge` operacji.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="8aa3c-276">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-276">Delete an entity</span></span>
<span data-ttu-id="8aa3c-277">Można z łatwością usunąć jednostkę po jej pobraniu przy użyciu hello tego samego wzorca co w przypadku aktualizowania jednostki.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="8aa3c-278">powitania po kod umożliwia pobranie i usunięcie jednostki klienta.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="8aa3c-279">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="8aa3c-279">Delete a table</span></span>
<span data-ttu-id="8aa3c-280">Na koniec hello poniższy przykład kodu usuwa tabelę z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="8aa3c-281">Możesz usunąć i ponownie utwórz tabelę bezpośrednio z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="8aa3c-282">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="8aa3c-282">Clean up resources</span></span> 

<span data-ttu-id="8aa3c-283">Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="8aa3c-284">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="8aa3c-285">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8aa3c-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-286">Next steps</span></span>

<span data-ttu-id="8aa3c-287">W tym samouczku objętych firma Microsoft, jak tooget uruchamiane przy użyciu bazy danych Azure rozwiązania Cosmos z hello tabeli interfejsu API i wykonaniu następujących hello:</span><span class="sxs-lookup"><span data-stu-id="8aa3c-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="8aa3c-288">Utworzone konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="8aa3c-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="8aa3c-289">Funkcje włączone w pliku app.config hello</span><span class="sxs-lookup"><span data-stu-id="8aa3c-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="8aa3c-290">Utworzyć tabelę</span><span class="sxs-lookup"><span data-stu-id="8aa3c-290">Created a table</span></span> 
> * <span data-ttu-id="8aa3c-291">Dodano tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="8aa3c-292">Wstawić partię jednostek</span><span class="sxs-lookup"><span data-stu-id="8aa3c-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="8aa3c-293">Pobrać pojedynczą jednostką</span><span class="sxs-lookup"><span data-stu-id="8aa3c-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="8aa3c-294">Jednostki, którego dotyczy kwerenda przy użyciu automatycznego indeksów pomocniczych</span><span class="sxs-lookup"><span data-stu-id="8aa3c-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="8aa3c-295">Zastąpione jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-295">Replaced an entity</span></span> 
> * <span data-ttu-id="8aa3c-296">Usunięte jednostki</span><span class="sxs-lookup"><span data-stu-id="8aa3c-296">Deleted an entity</span></span> 
> * <span data-ttu-id="8aa3c-297">Usunięto tabelę</span><span class="sxs-lookup"><span data-stu-id="8aa3c-297">Deleted a table</span></span>  

<span data-ttu-id="8aa3c-298">Można teraz kontynuować toohello następny samouczek i Dowiedz się więcej o przeszukiwaniem danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="8aa3c-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8aa3c-299">Zapytanie z hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8aa3c-299">Query with hello Table API</span></span>](tutorial-query-table.md)
