---
title: "Parametry połączenia bazy danych MongoDB dla konta bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łączenie aplikacji z bazy danych MongoDB konta bazy danych rozwiązania Cosmos Azure przy użyciu ciągu połączenia bazy danych MongoDB."
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
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="ad8db-104">Łączenie aplikacji bazy danych MongoDB, do bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ad8db-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="ad8db-105">Dowiedz się, jak łączenie aplikacji z bazy danych MongoDB konta bazy danych rozwiązania Cosmos Azure przy użyciu ciągu połączenia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="ad8db-106">Następnie można użyć bazy danych Azure rozwiązania Cosmos bazy danych jako dane magazynu dla aplikacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="ad8db-107">Ten samouczek zawiera można pobrać ciągu połączenia na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="ad8db-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="ad8db-108">[Szybki start — metoda](#QuickstartConnection), do użycia z programem .NET, Node.js, powłoka bazy danych MongoDB, Java i Python sterowniki</span><span class="sxs-lookup"><span data-stu-id="ad8db-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="ad8db-109">[Metoda ciąg połączenia niestandardowe](#GetCustomConnection), do użycia z innych sterowników</span><span class="sxs-lookup"><span data-stu-id="ad8db-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad8db-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad8db-110">Prerequisites</span></span>

- <span data-ttu-id="ad8db-111">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad8db-111">An Azure account.</span></span> <span data-ttu-id="ad8db-112">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/) teraz.</span><span class="sxs-lookup"><span data-stu-id="ad8db-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="ad8db-113">Konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="ad8db-114">Aby uzyskać instrukcje, zobacz [tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z usług .NET i portalu Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ad8db-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="ad8db-115"><a id="QuickstartConnection"></a>Pobierz ciąg połączenia bazy danych MongoDB przy użyciu szybki start</span><span class="sxs-lookup"><span data-stu-id="ad8db-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="ad8db-116">W przeglądarce internetowej, zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad8db-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad8db-117">W **bazy danych Azure rozwiązania Cosmos** bloku, wybierz interfejsu API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="ad8db-118">W lewym okienku blok konta, kliknij przycisk **szybki start**.</span><span class="sxs-lookup"><span data-stu-id="ad8db-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="ad8db-119">Wybierz platformy (**.NET**, **Node.js**, **powłoki MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="ad8db-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="ad8db-120">Jeśli nie widzisz, Twoje sterownika lub narzędzia na liście, nie martw się — firma Microsoft stale dokumentu więcej wstawki kodu połączenia.</span><span class="sxs-lookup"><span data-stu-id="ad8db-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="ad8db-121">Skomentuj poniżej na chcesz zobaczyć.</span><span class="sxs-lookup"><span data-stu-id="ad8db-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="ad8db-122">Aby dowiedzieć się, jak sformułować własne połączenia, przeczytaj [uzyskać informacje o parametrach połączenia dla konta](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="ad8db-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="ad8db-123">Skopiuj i Wklej fragmentu kodu w aplikacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Bloku szybki start](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="ad8db-125"><a id="GetCustomConnection"></a>Pobierz ciąg połączenia bazy danych MongoDB do dostosowania</span><span class="sxs-lookup"><span data-stu-id="ad8db-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="ad8db-126">W przeglądarce internetowej, zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad8db-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad8db-127">W **bazy danych Azure rozwiązania Cosmos** bloku, wybierz interfejsu API dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="ad8db-128">W lewym okienku blok konta, kliknij przycisk **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="ad8db-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="ad8db-129">**Ciąg połączenia** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="ad8db-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="ad8db-130">Ma wszystkie informacje wymagane do nawiązania konta za pośrednictwem sterownika bazy danych mongodb, w tym ciągu połączenia preconstructed.</span><span class="sxs-lookup"><span data-stu-id="ad8db-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Blok ciągu połączenia](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="ad8db-132">Wymagania dotyczące ciąg połączenia</span><span class="sxs-lookup"><span data-stu-id="ad8db-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="ad8db-133">Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ad8db-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="ad8db-134">Azure konta DB rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem *SSL*.</span><span class="sxs-lookup"><span data-stu-id="ad8db-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="ad8db-135">Azure DB rozwiązania Cosmos obsługuje standardowe bazy danych MongoDB format ciągu połączenia identyfikator URI, za pomocą paru specyficznych wymagań: konta bazy danych Azure rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="ad8db-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="ad8db-136">Tak format ciągu połączenia jest:</span><span class="sxs-lookup"><span data-stu-id="ad8db-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="ad8db-137">Wartości te parametry są dostępne w **ciąg połączenia** bloku przedstawiona wcześniej:</span><span class="sxs-lookup"><span data-stu-id="ad8db-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="ad8db-138">Nazwa użytkownika (wymagane): Nazwa konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ad8db-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="ad8db-139">Hasło (wymagane): hasło konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ad8db-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="ad8db-140">Host (wymagane): nazwa FQDN konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ad8db-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="ad8db-141">Port (wymagane): 10255.</span><span class="sxs-lookup"><span data-stu-id="ad8db-141">Port (required): 10255.</span></span>
* <span data-ttu-id="ad8db-142">Bazy danych (opcjonalnie): połączenie korzysta z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ad8db-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="ad8db-143">Jeśli baza danych jest dostępne, domyślna baza danych jest "test".</span><span class="sxs-lookup"><span data-stu-id="ad8db-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="ad8db-144">Protokół SSL = true (wymagane)</span><span class="sxs-lookup"><span data-stu-id="ad8db-144">ssl=true (required)</span></span>

<span data-ttu-id="ad8db-145">Rozważmy na przykład konto pokazano **ciąg połączenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="ad8db-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="ad8db-146">Jest prawidłowe parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="ad8db-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="ad8db-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad8db-147">Next steps</span></span>
* <span data-ttu-id="ad8db-148">Dowiedz się, jak [Użyj MongoChef](mongodb-mongochef.md) z interfejsu API Azure rozwiązania Cosmos bazy danych dla konta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad8db-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="ad8db-149">Eksploruj interfejsu API Azure rozwiązania Cosmos bazy danych dla bazy danych MongoDB, przeglądając [przykłady](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ad8db-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
