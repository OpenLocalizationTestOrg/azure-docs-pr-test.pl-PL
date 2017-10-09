---
title: "Parametry połączenia aaaMongoDB konta bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooan aplikacji z bazy danych MongoDB bazy danych Azure rozwiązania Cosmos konta przy użyciu ciągu połączenia bazy danych MongoDB."
keywords: "Parametry połączenia bazy danych mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="d99f9-104">Połączenia bazy danych MongoDB aplikacji tooAzure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="d99f9-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="d99f9-105">Dowiedz się, jak tooconnect tooan aplikacji z bazy danych MongoDB bazy danych Azure rozwiązania Cosmos konta przy użyciu ciągu połączenia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="d99f9-106">Następnie można użyć bazy danych Azure rozwiązania Cosmos bazy danych jako dane hello magazynu dla aplikacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="d99f9-107">Ten samouczek zawiera dwa sposoby tooretrieve ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="d99f9-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="d99f9-108">[Witaj szybki start — metoda](#QuickstartConnection), do użycia z programem .NET, Node.js, powłoka bazy danych MongoDB, Java i Python sterowniki</span><span class="sxs-lookup"><span data-stu-id="d99f9-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="d99f9-109">[Witaj metody ciąg połączenia niestandardowych](#GetCustomConnection), do użycia z innych sterowników</span><span class="sxs-lookup"><span data-stu-id="d99f9-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d99f9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d99f9-110">Prerequisites</span></span>

- <span data-ttu-id="d99f9-111">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d99f9-111">An Azure account.</span></span> <span data-ttu-id="d99f9-112">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/) teraz.</span><span class="sxs-lookup"><span data-stu-id="d99f9-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="d99f9-113">Konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="d99f9-114">Aby uzyskać instrukcje, zobacz [tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z platformą .NET i portalu Azure hello](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d99f9-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="d99f9-115"><a id="QuickstartConnection"></a>Pobierz ciąg połączenia bazy danych MongoDB hello przy użyciu hello szybki start</span><span class="sxs-lookup"><span data-stu-id="d99f9-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="d99f9-116">W przeglądarce internetowej, zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d99f9-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d99f9-117">W hello **bazy danych Azure rozwiązania Cosmos** bloku, wybierz hello API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="d99f9-118">W lewym okienku hello hello konta bloku, kliknij przycisk **szybki start**.</span><span class="sxs-lookup"><span data-stu-id="d99f9-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="d99f9-119">Wybierz platformy (**.NET**, **Node.js**, **powłoki MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="d99f9-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="d99f9-120">Jeśli nie widzisz, Twoje sterownika lub narzędzia na liście, nie martw się — firma Microsoft stale dokumentu więcej wstawki kodu połączenia.</span><span class="sxs-lookup"><span data-stu-id="d99f9-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="d99f9-121">Wprowadź uwagi poniżej na jakie chcesz toosee.</span><span class="sxs-lookup"><span data-stu-id="d99f9-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="d99f9-122">toolearn jak toocraft własne połączenia odczytu [uzyskać informacje o parametrach połączenia konta hello](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="d99f9-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="d99f9-123">Skopiuj i Wklej hello fragment kodu w aplikacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Bloku szybki start](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="d99f9-125"><a id="GetCustomConnection"></a>Pobierz toocustomize ciąg połączenia bazy danych MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="d99f9-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="d99f9-126">W przeglądarce internetowej, zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d99f9-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d99f9-127">W hello **bazy danych Azure rozwiązania Cosmos** bloku, wybierz hello API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="d99f9-128">W lewym okienku hello hello konta bloku, kliknij przycisk **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="d99f9-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="d99f9-129">Witaj **ciąg połączenia** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="d99f9-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="d99f9-130">Ma ona wszystkie hello informacje niezbędne tooconnect toohello konta za pośrednictwem sterownika bazy danych mongodb, w tym ciągu połączenia preconstructed.</span><span class="sxs-lookup"><span data-stu-id="d99f9-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Blok ciągu połączenia](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="d99f9-132">Wymagania dotyczące ciąg połączenia</span><span class="sxs-lookup"><span data-stu-id="d99f9-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="d99f9-133">Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d99f9-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="d99f9-134">Azure konta DB rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem *SSL*.</span><span class="sxs-lookup"><span data-stu-id="d99f9-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="d99f9-135">Azure DB rozwiązania Cosmos obsługuje hello standardowe bazy danych MongoDB format ciągu połączenia identyfikator URI, za pomocą paru specyficznych wymagań: konta bazy danych Azure rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="d99f9-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="d99f9-136">Tak format ciągu połączenia hello jest:</span><span class="sxs-lookup"><span data-stu-id="d99f9-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="d99f9-137">Ten ciąg Hello wartości są dostępne w hello **ciąg połączenia** bloku przedstawiona wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d99f9-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="d99f9-138">Nazwa użytkownika (wymagane): Nazwa konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d99f9-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="d99f9-139">Hasło (wymagane): hasło konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d99f9-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="d99f9-140">Host (wymagane): nazwa FQDN hello konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d99f9-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="d99f9-141">Port (wymagane): 10255.</span><span class="sxs-lookup"><span data-stu-id="d99f9-141">Port (required): 10255.</span></span>
* <span data-ttu-id="d99f9-142">Bazy danych (opcjonalnie): używa bazy danych hello hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="d99f9-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="d99f9-143">Jeśli baza danych jest dostępne, hello domyślna baza danych jest "test".</span><span class="sxs-lookup"><span data-stu-id="d99f9-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="d99f9-144">Protokół SSL = true (wymagane)</span><span class="sxs-lookup"><span data-stu-id="d99f9-144">ssl=true (required)</span></span>

<span data-ttu-id="d99f9-145">Rozważmy na przykład konto hello pokazano hello **ciąg połączenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="d99f9-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="d99f9-146">Jest prawidłowe parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="d99f9-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="d99f9-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d99f9-147">Next steps</span></span>
* <span data-ttu-id="d99f9-148">Dowiedz się, jak za[Użyj MongoChef](mongodb-mongochef.md) z interfejsu API Azure rozwiązania Cosmos bazy danych dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d99f9-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="d99f9-149">Eksploruj hello interfejsu API Azure rozwiązania Cosmos DB bazy danych mongodb, wyświetlając [przykłady](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d99f9-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
