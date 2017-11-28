---
title: "aaaCreate bazy danych Azure DB rozwiązania Cosmos wykres z językiem Java | Dokumentacja firmy Microsoft"
description: "Przedstawia informacje o liczbie przykładowe dane wykresu zapytania tooand tooconnect można użyć w usłudze Azure DB rozwiązania Cosmos przy użyciu Gremlin kodu języka Java."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="c6dc0-103">Azure DB rozwiązania Cosmos: Tworzenie bazy danych wykresu przy użyciu języka Java i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6dc0-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="c6dc0-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c6dc0-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c6dc0-106">Ta opcja szybkiego startu tworzy wykres bazy danych przy użyciu hello narzędzi portalu platformy Azure dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="c6dc0-107">Ta opcja szybkiego startu przedstawiono również sposób tooquickly Utwórz aplikację konsoli języka Java przy użyciu bazy danych wykresu przy użyciu hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) sterownika.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="c6dc0-108">instrukcje Hello tego przewodnika Szybki Start można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić oprogramowanie Java.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="c6dc0-109">Ta opcja szybkiego startu zaznajomić z tworzenia i modyfikowania zasobów wykresu w hello interfejsu użytkownika lub programowo, nastąpi swoich preferencji.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c6dc0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6dc0-110">Prerequisites</span></span>

* [<span data-ttu-id="c6dc0-111">Zestaw Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="c6dc0-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="c6dc0-112">Uruchom na Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="c6dc0-113">Jest zainstalowanym hello JDK czy tooset hello JAVA_HOME środowiska zmiennej toopoint toohello folder.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="c6dc0-114">[Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="c6dc0-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="c6dc0-115">Na Ubuntu, można uruchomić `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="c6dc0-116">Git</span><span class="sxs-lookup"><span data-stu-id="c6dc0-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="c6dc0-117">Na Ubuntu, można uruchomić `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c6dc0-118">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="c6dc0-118">Create a database account</span></span>

<span data-ttu-id="c6dc0-119">Przed utworzeniem bazy danych wykresu, konieczne jest toocreate Gremlin (wykres) konta bazy danych z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="c6dc0-120">Dodawanie grafu</span><span class="sxs-lookup"><span data-stu-id="c6dc0-120">Add a graph</span></span>

<span data-ttu-id="c6dc0-121">Po wykonaniu użyć narzędzia Eksplorator danych hello w hello Azure toocreate portalu bazy danych wykresu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="c6dc0-122">W portalu Azure, w menu nawigacji po lewej stronie powitania hello kliknij **Eksploratora danych (wersja zapoznawcza)**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="c6dc0-123">W hello **Eksploratora danych (wersja zapoznawcza)** bloku, kliknij przycisk **nowy wykres**, a następnie wypełnij hello strony przy użyciu hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="c6dc0-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Eksplorator danych w hello portalu Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="c6dc0-125">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="c6dc0-125">Setting</span></span>|<span data-ttu-id="c6dc0-126">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="c6dc0-126">Suggested value</span></span>|<span data-ttu-id="c6dc0-127">Opis</span><span class="sxs-lookup"><span data-stu-id="c6dc0-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="c6dc0-128">Identyfikator bazy danych</span><span class="sxs-lookup"><span data-stu-id="c6dc0-128">Database ID</span></span>|<span data-ttu-id="c6dc0-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="c6dc0-129">sample-database</span></span>|<span data-ttu-id="c6dc0-130">Identyfikator Hello nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-130">hello ID for your new database.</span></span> <span data-ttu-id="c6dc0-131">Nazwy baz danych muszą zawierać od 1 do 255 znaków i nie mogą zawierać znaków `/ \ # ?` ani mieć spacji na końcu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="c6dc0-132">Identyfikator grafu</span><span class="sxs-lookup"><span data-stu-id="c6dc0-132">Graph ID</span></span>|<span data-ttu-id="c6dc0-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="c6dc0-133">sample-graph</span></span>|<span data-ttu-id="c6dc0-134">Identyfikator Hello nowego wykresu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-134">hello ID for your new graph.</span></span> <span data-ttu-id="c6dc0-135">Wykres nazwy mają hello wymagania sam znak jako identyfikatory bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="c6dc0-136">Pojemność magazynu</span><span class="sxs-lookup"><span data-stu-id="c6dc0-136">Storage Capacity</span></span>| <span data-ttu-id="c6dc0-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="c6dc0-137">10 GB</span></span>|<span data-ttu-id="c6dc0-138">Pozostaw wartość domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-138">Leave hello default value.</span></span> <span data-ttu-id="c6dc0-139">Jest to hello pojemności hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="c6dc0-140">Przepływność</span><span class="sxs-lookup"><span data-stu-id="c6dc0-140">Throughput</span></span>|<span data-ttu-id="c6dc0-141">400 jednostek żądania</span><span class="sxs-lookup"><span data-stu-id="c6dc0-141">400 RUs</span></span>|<span data-ttu-id="c6dc0-142">Pozostaw wartość domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-142">Leave hello default value.</span></span> <span data-ttu-id="c6dc0-143">Można zwiększać przepływności hello później Chcąc tooreduce opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="c6dc0-144">Klucz partycji</span><span class="sxs-lookup"><span data-stu-id="c6dc0-144">Partition key</span></span>|<span data-ttu-id="c6dc0-145">Pozostaw puste</span><span class="sxs-lookup"><span data-stu-id="c6dc0-145">Leave blank</span></span>|<span data-ttu-id="c6dc0-146">W celu hello tego przewodnika Szybki Start pozostaw puste hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="c6dc0-147">Gdy formularz hello jest wypełniane, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="c6dc0-148">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6dc0-148">Clone hello sample application</span></span>

<span data-ttu-id="c6dc0-149">Teraz załóżmy sklonować aplikacji przez wykres z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="c6dc0-150">Zobacz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="c6dc0-151">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="c6dc0-152">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="c6dc0-153">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="c6dc0-153">Review hello code</span></span>

<span data-ttu-id="c6dc0-154">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="c6dc0-155">Otwórz hello `Program.java` plików z folderu \src\GetStarted hello i Znajdź następujące wiersze kodu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="c6dc0-156">Witaj Gremlin `Client` został zainicjowany z konfiguracji hello w `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="c6dc0-157">Serie kroków Gremlin są wykonywane przy użyciu hello `client.submit` metody.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="c6dc0-158">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="c6dc0-158">Update your connection string</span></span>

1. <span data-ttu-id="c6dc0-159">Otwórz hello src/remote.yaml pliku.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="c6dc0-160">Wypełnij Twojej *hostów*, *username*, i *hasło* wartości hello src/remote.yaml pliku.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="c6dc0-161">pozostałe ustawienia hello Hello nie ma potrzeby toobe zmienione.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="c6dc0-162">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="c6dc0-162">Setting</span></span>|<span data-ttu-id="c6dc0-163">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="c6dc0-163">Suggested value</span></span>|<span data-ttu-id="c6dc0-164">Opis</span><span class="sxs-lookup"><span data-stu-id="c6dc0-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="c6dc0-165">Hosts</span><span class="sxs-lookup"><span data-stu-id="c6dc0-165">Hosts</span></span>|<span data-ttu-id="c6dc0-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="c6dc0-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="c6dc0-167">Zobacz hello zrzut ekranu poniżej tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-167">See hello screenshot following this table.</span></span> <span data-ttu-id="c6dc0-168">Ta wartość jest wartością Gremlin URI hello na stronie Przegląd hello hello portalu Azure w nawiasach kwadratowych spacją hello: 443 / usunięty.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="c6dc0-169">Tę wartość można również pobrać z karty klucze hello, przy użyciu wartości identyfikatora URI hello usuwanie https://, zmieniając toographs dokumentów i usuwanie końcowe hello: 443 /.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="c6dc0-170">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="c6dc0-170">Username</span></span>|<span data-ttu-id="c6dc0-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="c6dc0-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="c6dc0-172">Witaj zasobów formularza hello `/dbs/<db>/colls/<coll>` gdzie `<db>` oznacza nazwę istniejącej bazy danych i `<coll>` jest istniejącą nazwę kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="c6dc0-173">Hasło</span><span class="sxs-lookup"><span data-stu-id="c6dc0-173">Password</span></span>|<span data-ttu-id="c6dc0-174">*Twój podstawowy klucz główny*</span><span class="sxs-lookup"><span data-stu-id="c6dc0-174">*Your primary master key*</span></span>|<span data-ttu-id="c6dc0-175">Zobacz drugi zrzut ekranu hello poniżej tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="c6dc0-176">Ta wartość jest klucz podstawowy, który można pobrać ze strony klucze hello hello portalu Azure, w polu klucza podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="c6dc0-177">Skopiuj wartość hello za pomocą przycisku Kopiuj hello hello prawej strony pola hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="c6dc0-178">Dla wartości hostów hello, skopiuj hello **Gremlin URI** wartość z zakresu od hello **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="c6dc0-179">Jeśli jest pusty, zobacz instrukcje hello hello hostów wiersza w powyższej tabeli o tworzeniu hello Gremlin identyfikatora URI z bloku klucze hello hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="c6dc0-180">![Wyświetlanie i kopiowanie wartość identyfikatora URI Gremlin hello na stronie Przegląd hello hello portalu Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="c6dc0-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="c6dc0-181">W przypadku hello wartość hasła, skopiuj hello **klucza podstawowego** z hello **klucze** bloku: ![wyświetlanie i kopiowanie kluczy primary key w hello portalu Azure, strony](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="c6dc0-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="c6dc0-182">Uruchamianie aplikacji konsoli hello</span><span class="sxs-lookup"><span data-stu-id="c6dc0-182">Run hello console app</span></span>

1. <span data-ttu-id="c6dc0-183">W oknie terminala git hello `cd` toohello azure-cosmos-db-graph-java-getting-started folderu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="c6dc0-184">W oknie terminala git hello, wpisz `mvn package` tooinstall hello wymaganych pakietów języka Java.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="c6dc0-185">W oknie terminala git hello, uruchom `mvn exec:java -D exec.mainClass=GetStarted.Program` w hello toostart okno terminalu aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="c6dc0-186">Okno terminalu Hello Wyświetla wierzchołków hello dodawany toohello wykresu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="c6dc0-187">Po zakończeniu działania programu hello przełącznika wstecz toohello portalu Azure w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="c6dc0-188">Przeglądanie i dodawanie przykładowych danych</span><span class="sxs-lookup"><span data-stu-id="c6dc0-188">Review and add sample data</span></span>

<span data-ttu-id="c6dc0-189">Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz wierzchołków hello dodawane wykres toohello i dodać dodatkowe dane punktów.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="c6dc0-190">W Eksploratorze danych rozwiń hello **bazy danych przykładowych**/**wykres próbki**, kliknij przycisk **wykres**, a następnie kliknij przycisk **Zastosuj filtr**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w hello portalu Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="c6dc0-192">W hello **wyniki** listy, zwróć uwagę, hello nowi użytkownicy dodawani toohello wykresu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="c6dc0-193">Wybierz **ben** i zwróć uwagę, że został on podłączony toorobin.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="c6dc0-194">Można przenosić wierzchołków hello na powitania wykres Eksploratora, powiększać i pomniejszać i rozwiń rozmiar hello hello wykres explorer powierzchni.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Nowe wierzchołków w grafie hello w Eksploratorze danych w hello portalu Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="c6dc0-196">Dodajmy kilka nowy wykres toohello użytkowników przy użyciu hello Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="c6dc0-197">Kliknij przycisk hello **nowy wierzchołek** przycisk tooadd danych tooyour wykresu.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Tworzenie nowych dokumentów w Eksploratorze danych w hello portalu Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="c6dc0-199">Wprowadź etykietę *osoby* wprowadź hello następujące klucze i wartości toocreate hello pierwszym wierzchołku hello wykresie.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="c6dc0-200">Zauważ, że możesz utworzyć unikatowe właściwości dla każdej osoby w grafie.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="c6dc0-201">Tylko hello identyfikator klucz jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-201">Only hello id key is required.</span></span>

    <span data-ttu-id="c6dc0-202">key</span><span class="sxs-lookup"><span data-stu-id="c6dc0-202">key</span></span>|<span data-ttu-id="c6dc0-203">wartość</span><span class="sxs-lookup"><span data-stu-id="c6dc0-203">value</span></span>|<span data-ttu-id="c6dc0-204">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6dc0-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="c6dc0-205">id</span><span class="sxs-lookup"><span data-stu-id="c6dc0-205">id</span></span>|<span data-ttu-id="c6dc0-206">ashley</span><span class="sxs-lookup"><span data-stu-id="c6dc0-206">ashley</span></span>|<span data-ttu-id="c6dc0-207">Unikatowy identyfikator Hello hello wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="c6dc0-208">Jeśli nie określono identyfikatora, zostanie on wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="c6dc0-209">płeć</span><span class="sxs-lookup"><span data-stu-id="c6dc0-209">gender</span></span>|<span data-ttu-id="c6dc0-210">kobieta</span><span class="sxs-lookup"><span data-stu-id="c6dc0-210">female</span></span>| 
    <span data-ttu-id="c6dc0-211">techniczne</span><span class="sxs-lookup"><span data-stu-id="c6dc0-211">tech</span></span> | <span data-ttu-id="c6dc0-212">java</span><span class="sxs-lookup"><span data-stu-id="c6dc0-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="c6dc0-213">W tym przewodniku Szybki start tworzymy kolekcję niepartycjonowaną.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="c6dc0-214">Jednak jeśli tworzysz kolekcję partycjonowaną, określając klucza partycji podczas tworzenia kolekcji hello, następnie należy klucza partycji hello tooinclude jako klucz w każdy wierzchołek nowe.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="c6dc0-215">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-215">Click **OK**.</span></span> <span data-ttu-id="c6dc0-216">Może być konieczne tooexpand Twojego toosee ekranu **OK** na powitania dolnej części ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="c6dc0-217">Kliknij przycisk **Nowy wierzchołek** ponownie i dodaj kolejnego nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="c6dc0-218">Wprowadź etykietę *osoby* następnie wprowadź następujące hello kluczy i wartości:</span><span class="sxs-lookup"><span data-stu-id="c6dc0-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="c6dc0-219">key</span><span class="sxs-lookup"><span data-stu-id="c6dc0-219">key</span></span>|<span data-ttu-id="c6dc0-220">wartość</span><span class="sxs-lookup"><span data-stu-id="c6dc0-220">value</span></span>|<span data-ttu-id="c6dc0-221">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6dc0-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="c6dc0-222">id</span><span class="sxs-lookup"><span data-stu-id="c6dc0-222">id</span></span>|<span data-ttu-id="c6dc0-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="c6dc0-223">rakesh</span></span>|<span data-ttu-id="c6dc0-224">Unikatowy identyfikator Hello hello wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="c6dc0-225">Jeśli nie określono identyfikatora, zostanie on wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="c6dc0-226">płeć</span><span class="sxs-lookup"><span data-stu-id="c6dc0-226">gender</span></span>|<span data-ttu-id="c6dc0-227">mężczyzna</span><span class="sxs-lookup"><span data-stu-id="c6dc0-227">male</span></span>| 
    <span data-ttu-id="c6dc0-228">szkoła</span><span class="sxs-lookup"><span data-stu-id="c6dc0-228">school</span></span>|<span data-ttu-id="c6dc0-229">MIT</span><span class="sxs-lookup"><span data-stu-id="c6dc0-229">MIT</span></span>| 

7. <span data-ttu-id="c6dc0-230">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-230">Click **OK**.</span></span> 

8. <span data-ttu-id="c6dc0-231">Kliknij przycisk **Zastosuj filtr** z domyślnymi hello `g.V()` filtru.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="c6dc0-232">Teraz Pokaż wszystkich użytkowników hello w hello **wyniki** listy.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="c6dc0-233">Dodaj więcej danych, program toolimit filtry wyników.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="c6dc0-234">Domyślnie korzysta z Eksploratora danych `g.V()` tooretrieve wszystkich wierzchołków wykres, ale można zmienić tego tooa różnych [zapytania wykres](tutorial-query-graph.md), takich jak `g.V().count()`, tooreturn liczbę wszystkich wierzchołków hello hello wykresu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="c6dc0-235">Teraz możemy połączyć użytkowników rakesh i ashley.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="c6dc0-236">Upewnij się, **Monika** w wybranym hello **wyniki** listy, a następnie kliknij przycisk Edytuj hello obok zbyt**cele** w prawym dolnym.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="c6dc0-237">Może być konieczne toowiden Twojego hello toosee okna **właściwości** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Zmień docelowe hello wierzchołka na wykresie](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="c6dc0-239">W hello **docelowej** wpisz *rakesh*w hello **etykiety krawędzi** wpisz *zna*, a następnie kliknij pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Dodawanie połączenia między użytkownikami ashley i rakesh w Eksploratorze danych](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="c6dc0-241">Teraz wybierz **rakesh** z listy wyników hello i zobacz, czy Monika i rakesh są połączone.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Dwa wierzchołki połączone w Eksploratorze danych](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="c6dc0-243">Można również użyć Eksploratora danych toocreate przechowywane procedury, funkcje UDF i logiki biznesowej po stronie serwera tooperform wyzwalaczy również jako przepływności skali.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="c6dc0-244">Eksplorator danych udostępnia wszystkie hello wbudowanych programowy dostęp do danych dostępne w hello interfejsów API, ale zapewnia łatwy dostęp do danych tooyour w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="c6dc0-245">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6dc0-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c6dc0-246">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="c6dc0-246">Clean up resources</span></span>

<span data-ttu-id="c6dc0-247">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6dc0-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="c6dc0-248">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="c6dc0-249">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6dc0-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6dc0-250">Next steps</span></span>

<span data-ttu-id="c6dc0-251">W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos utworzyć wykres przy użyciu hello Eksploratora danych i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="c6dc0-252">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="c6dc0-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6dc0-253">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="c6dc0-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

