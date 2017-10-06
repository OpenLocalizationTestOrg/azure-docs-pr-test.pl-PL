---
title: "Samouczek usługi Azure Cosmos DB: Tworzenie, wykonywanie zapytań i przechodzenie w konsoli Apache TinkerPops Gremlin | Microsoft Docs"
description: "Toocreates Szybki Start Azure DB rozwiązania Cosmos wierzchołków, krawędzie i zapytań przy użyciu hello DB Azure rozwiązania Cosmos interfejsu API programu Graph."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="859b7-103">Azure rozwiązania Cosmos bazy danych: Utwórz zapytanie i przechodzić między nimi wykres w konsoli Gremlin hello</span><span class="sxs-lookup"><span data-stu-id="859b7-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="859b7-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="859b7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="859b7-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="859b7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="859b7-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazy danych i wykres (kontener) przy użyciu hello portalu Azure, a następnie użyj hello [konsoli Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) z [Apache TinkerPop](http://tinkerpop.apache.org) toowork z Wykres danych interfejsu API (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="859b7-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="859b7-107">W tym samouczku Utwórz i zapytania wierzchołków i krawędzi, aktualizowanie właściwości wierzchołków zapytania wierzchołków, przechodzenie przez wykres hello i upuść wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="859b7-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![Azure DB rozwiązania Cosmos z hello Apache Gremlin konsoli](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="859b7-109">Konsola Gremlin Hello jest Groovy/Java i działa w systemie Linux, Mac i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="859b7-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="859b7-110">Można go pobrać ze hello [lokacji Apache TinkerPop](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="859b7-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="859b7-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="859b7-111">Prerequisites</span></span>

<span data-ttu-id="859b7-112">Toohave toocreate subskrypcji platformy Azure, konto bazy danych Azure rozwiązania Cosmos jest wymagane dla tego przewodnika Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="859b7-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="859b7-113">Należy również tooinstall hello [konsoli Gremlin](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="859b7-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="859b7-114">Użyj wersji 3.2.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="859b7-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="859b7-115">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="859b7-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="859b7-116">Dodawanie grafu</span><span class="sxs-lookup"><span data-stu-id="859b7-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="859b7-117"><a id="ConnectAppService"></a>Połącz tooyour usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="859b7-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="859b7-118">Przed rozpoczęciem hello Gremlin konsoli, Utwórz lub zmodyfikuj plik konfiguracji zdalnego secure.yaml hello w katalogu apache-tinkerpop-gremlin-console-3.2.5/conf hello.</span><span class="sxs-lookup"><span data-stu-id="859b7-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="859b7-119">Wypełnij ustawienia konfiguracji *host*, *port*, *username*, *password*, *connectionPool* i *serializer*:</span><span class="sxs-lookup"><span data-stu-id="859b7-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="859b7-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="859b7-120">Setting</span></span>|<span data-ttu-id="859b7-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="859b7-121">Suggested value</span></span>|<span data-ttu-id="859b7-122">Opis</span><span class="sxs-lookup"><span data-stu-id="859b7-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="859b7-123">hosty</span><span class="sxs-lookup"><span data-stu-id="859b7-123">hosts</span></span>|<span data-ttu-id="859b7-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="859b7-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="859b7-125">Zobacz poniższy zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="859b7-125">See screenshot below.</span></span> <span data-ttu-id="859b7-126">Jest to wartość identyfikatora URI Gremlin hello na stronie Przegląd hello hello portalu Azure w nawiasach kwadratowych spacją hello: 443 / usunięty.</span><span class="sxs-lookup"><span data-stu-id="859b7-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="859b7-127">Tę wartość można również pobrać z karty klucze hello, przy użyciu wartości identyfikatora URI hello usuwanie https://, zmieniając toographs dokumentów i usuwanie końcowe hello: 443 /.</span><span class="sxs-lookup"><span data-stu-id="859b7-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="859b7-128">port</span><span class="sxs-lookup"><span data-stu-id="859b7-128">port</span></span>|<span data-ttu-id="859b7-129">443</span><span class="sxs-lookup"><span data-stu-id="859b7-129">443</span></span>|<span data-ttu-id="859b7-130">Ustaw too443.</span><span class="sxs-lookup"><span data-stu-id="859b7-130">Set too443.</span></span>
    <span data-ttu-id="859b7-131">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="859b7-131">username</span></span>|<span data-ttu-id="859b7-132">*Twoja nazwa użytkownika*</span><span class="sxs-lookup"><span data-stu-id="859b7-132">*Your username*</span></span>|<span data-ttu-id="859b7-133">Witaj zasobów formularza hello `/dbs/<db>/colls/<coll>` gdzie `<db>` jest nazwa bazy danych i `<coll>` oznacza nazwę kolekcji.</span><span class="sxs-lookup"><span data-stu-id="859b7-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="859b7-134">hasło</span><span class="sxs-lookup"><span data-stu-id="859b7-134">password</span></span>|<span data-ttu-id="859b7-135">*Twój klucz podstawowy*</span><span class="sxs-lookup"><span data-stu-id="859b7-135">*Your primary key*</span></span>| <span data-ttu-id="859b7-136">Zobacz drugi zrzut ekranu poniżej.</span><span class="sxs-lookup"><span data-stu-id="859b7-136">See second screenshot below.</span></span> <span data-ttu-id="859b7-137">Jest to klucz podstawowy, który można pobrać ze strony klucze hello hello portalu Azure, w polu klucza podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="859b7-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="859b7-138">Użyj przycisku Kopiuj hello po lewej stronie powitania hello pole toocopy hello wartość.</span><span class="sxs-lookup"><span data-stu-id="859b7-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="859b7-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="859b7-139">connectionPool</span></span>|<span data-ttu-id="859b7-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="859b7-140">{enableSsl: true}</span></span>|<span data-ttu-id="859b7-141">Ustawienie puli połączeń protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="859b7-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="859b7-142">serializer</span><span class="sxs-lookup"><span data-stu-id="859b7-142">serializer</span></span>|<span data-ttu-id="859b7-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="859b7-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="859b7-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="859b7-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="859b7-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="859b7-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="859b7-146">Ustaw wartość toothis i usunięcie wszystkich `\n` podziały podczas wklejania hello wartości.</span><span class="sxs-lookup"><span data-stu-id="859b7-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="859b7-147">Dla wartości hostów hello, skopiuj hello **Gremlin URI** wartość z zakresu od hello **omówienie** strony: ![wyświetlanie i kopiowanie wartość identyfikatora URI Gremlin hello na stronie Przegląd hello hello portalu Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="859b7-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="859b7-148">W przypadku wartości hasła hello, skopiuj hello **klucza podstawowego** z hello **klucze** strony: ![wyświetlanie i kopiowanie kluczy primary key w hello portalu Azure, strony](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="859b7-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="859b7-149">W terminalu, uruchom `bin/gremlin.bat` lub `bin/gremlin.sh` toostart hello [konsoli Gremlin](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="859b7-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="859b7-150">W terminalu, uruchom `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="859b7-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="859b7-151">Jeśli wystąpi błąd hello `No appenders could be found for logger` upewnij się, zaktualizowano hello serializator wartość w pliku zdalnego secure.yaml hello, zgodnie z opisem w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="859b7-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="859b7-152">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="859b7-152">Great!</span></span> <span data-ttu-id="859b7-153">Teraz, gdy zakończeniu hello instalacji, Zacznijmy niektóre polecenia konsoli.</span><span class="sxs-lookup"><span data-stu-id="859b7-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="859b7-154">Wypróbujmy proste polecenie count().</span><span class="sxs-lookup"><span data-stu-id="859b7-154">Let's try a simple count() command.</span></span> <span data-ttu-id="859b7-155">Wpisz następujące hello do konsoli hello w wierszu hello:</span><span class="sxs-lookup"><span data-stu-id="859b7-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="859b7-156">Powiadomienie hello `:>` czy poprzedza hello `g.V().count()` tekst?</span><span class="sxs-lookup"><span data-stu-id="859b7-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="859b7-157">Jest to część polecenia hello potrzebne tootype.</span><span class="sxs-lookup"><span data-stu-id="859b7-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="859b7-158">Jest ważne podczas korzystania z bazy danych Azure rozwiązania Cosmos hello Gremlin konsoli.</span><span class="sxs-lookup"><span data-stu-id="859b7-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="859b7-159">Pominięcie to `:>` prefiks nakazuje hello tooexecute hello polecenie konsoli lokalnie, często względem wykresu w pamięci.</span><span class="sxs-lookup"><span data-stu-id="859b7-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="859b7-160">Za pomocą tej `:>` informuje tooexecute konsoli hello polecenia zdalnego, w tym przypadku przed DB rozwiązania Cosmos (albo emulatora localhost hello, lub > wystąpienia platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="859b7-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="859b7-161">Tworzenie wierzchołków i krawędzi</span><span class="sxs-lookup"><span data-stu-id="859b7-161">Create vertices and edges</span></span>

<span data-ttu-id="859b7-162">Zacznijmy od dodania wierzchołków dla pięciu osób: *Thomas*, *Mary Kay*, *Robin*, *Ben* i *Jack*.</span><span class="sxs-lookup"><span data-stu-id="859b7-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="859b7-163">Dane wejściowe (Thomas):</span><span class="sxs-lookup"><span data-stu-id="859b7-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="859b7-164">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="859b7-165">Dane wejściowe (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="859b7-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="859b7-166">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="859b7-167">Dane wejściowe (Robin):</span><span class="sxs-lookup"><span data-stu-id="859b7-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="859b7-168">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="859b7-169">Dane wejściowe (Ben):</span><span class="sxs-lookup"><span data-stu-id="859b7-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="859b7-170">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="859b7-171">Dane wejściowe (Jack):</span><span class="sxs-lookup"><span data-stu-id="859b7-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="859b7-172">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="859b7-173">Następnie dodajmy krawędzie dla relacji między tymi osobami.</span><span class="sxs-lookup"><span data-stu-id="859b7-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="859b7-174">Dane wejściowe (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="859b7-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="859b7-175">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="859b7-176">Dane wejściowe (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="859b7-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="859b7-177">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="859b7-178">Dane wejściowe (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="859b7-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="859b7-179">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="859b7-180">Aktualizowanie wierzchołka</span><span class="sxs-lookup"><span data-stu-id="859b7-180">Update a vertex</span></span>

<span data-ttu-id="859b7-181">Ta funkcja pozwala zaktualizować hello *blogu Thomasa* wierzchołka z nowego wiek *45*.</span><span class="sxs-lookup"><span data-stu-id="859b7-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="859b7-182">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="859b7-183">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="859b7-184">Wykonywanie zapytania względem grafu</span><span class="sxs-lookup"><span data-stu-id="859b7-184">Query your graph</span></span>

<span data-ttu-id="859b7-185">Teraz uruchommy różne zapytania względem grafu.</span><span class="sxs-lookup"><span data-stu-id="859b7-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="859b7-186">Po pierwsze spróbujmy zapytania z filtru tooreturn tylko osoby, które są starsze niż 40 lat.</span><span class="sxs-lookup"><span data-stu-id="859b7-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="859b7-187">Dane wejściowe (zapytanie filtru):</span><span class="sxs-lookup"><span data-stu-id="859b7-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="859b7-188">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="859b7-189">Następnie Załóżmy projekt hello imię osoby hello, które są starsze niż 40 lat.</span><span class="sxs-lookup"><span data-stu-id="859b7-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="859b7-190">Dane wejściowe (zapytanie filtru i projekcji):</span><span class="sxs-lookup"><span data-stu-id="859b7-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="859b7-191">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="859b7-192">Przechodzenie grafu</span><span class="sxs-lookup"><span data-stu-id="859b7-192">Traverse your graph</span></span>

<span data-ttu-id="859b7-193">Umożliwia przenoszenie hello wykres tooreturn wszystkie w blogu Thomasa znajomych.</span><span class="sxs-lookup"><span data-stu-id="859b7-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="859b7-194">Dane wejściowe (znajomi Thomasa):</span><span class="sxs-lookup"><span data-stu-id="859b7-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="859b7-195">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="859b7-196">Następnie zaloguj się hello warstwy następnym wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="859b7-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="859b7-197">Przenoszenie wszystkich hello znajomych przyjaciół w blogu Thomasa hello tooreturn wykresu.</span><span class="sxs-lookup"><span data-stu-id="859b7-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="859b7-198">Dane wejściowe (znajomi znajomych Thomasa):</span><span class="sxs-lookup"><span data-stu-id="859b7-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="859b7-199">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="859b7-200">Usuwanie wierzchołka</span><span class="sxs-lookup"><span data-stu-id="859b7-200">Drop a vertex</span></span>

<span data-ttu-id="859b7-201">Umożliwia teraz usunąć wierzchołek z bazy danych wykresu hello.</span><span class="sxs-lookup"><span data-stu-id="859b7-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="859b7-202">Dane wejściowe (usunięcie wierzchołka Jacka):</span><span class="sxs-lookup"><span data-stu-id="859b7-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="859b7-203">Czyszczenie grafu</span><span class="sxs-lookup"><span data-stu-id="859b7-203">Clear your graph</span></span>

<span data-ttu-id="859b7-204">Na koniec Przyjrzyjmy Wyczyść bazę danych hello wszystkich wierzchołków i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="859b7-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="859b7-205">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="859b7-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="859b7-206">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="859b7-206">Congratulations!</span></span> <span data-ttu-id="859b7-207">Pomyślnie ukończono samouczek interfejsu API programu Graph w usłudze Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="859b7-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="859b7-208">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="859b7-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="859b7-209">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="859b7-209">Clean up resources</span></span>

<span data-ttu-id="859b7-210">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="859b7-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="859b7-211">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="859b7-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="859b7-212">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="859b7-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859b7-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="859b7-213">Next steps</span></span>

<span data-ttu-id="859b7-214">W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos utworzyć wykres przy użyciu hello Eksploratora danych, tworzyć wierzchołki i krawędzi i przechodzić między nimi przy użyciu konsoli Gremlin hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="859b7-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="859b7-215">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="859b7-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="859b7-216">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="859b7-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
