---
title: "Przykłady interfejsu wiersza polecenia dla bazy danych Azure rozwiązania Cosmos aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładów dla interfejsu wiersza polecenia platformy Azure — tworzenie i zarządzanie kontami, baz danych, kontenerów, regiony i zapory bazy danych Azure rozwiązania Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="c3a68-103">Przykładów dla interfejsu wiersza polecenia platformy Azure dla bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c3a68-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="c3a68-104">Witaj Poniższa tabela zawiera linki toosample interfejsu wiersza polecenia Azure skryptów dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c3a68-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="c3a68-105">Odwołanie do strony dla wszystkich poleceń interfejsu wiersza polecenia Azure rozwiązania Cosmos bazy danych są dostępne w hello [odwołania 2.0 interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="c3a68-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="c3a68-106">**Tworzenie konta bazy danych Azure rozwiązania Cosmos, bazy danych i kontenerów**</span><span class="sxs-lookup"><span data-stu-id="c3a68-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="c3a68-107">Utwórz konto usługi DocumentDB interfejsu API, wykres lub tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c3a68-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="c3a68-108">Tworzy pojedynczy konto interfejsu API Azure rozwiązania Cosmos bazy danych, bazę danych i kontener do użycia z hello usługi DocumentDB, wykres lub interfejsów API tabeli.</span><span class="sxs-lookup"><span data-stu-id="c3a68-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="c3a68-109">Tworzenie konta bazy danych MongoDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c3a68-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c3a68-110">Tworzy jednego interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB konta bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c3a68-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="c3a68-111">**Skalować rozwiązania Cosmos Azure DB**</span><span class="sxs-lookup"><span data-stu-id="c3a68-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="c3a68-112">Przepływność kontenera skali</span><span class="sxs-lookup"><span data-stu-id="c3a68-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c3a68-113">Zmiany hello zainicjowana througput do kontenera.</span><span class="sxs-lookup"><span data-stu-id="c3a68-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="c3a68-114">Replikację bazy danych Azure rozwiązania Cosmos konta bazy danych w wielu regionach i skonfiguruj priorytetów trybu failover</span><span class="sxs-lookup"><span data-stu-id="c3a68-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c3a68-115">Globalny replikuje dane konta w wielu regionach o priorytecie określonego trybu failover.</span><span class="sxs-lookup"><span data-stu-id="c3a68-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="c3a68-116">**Zabezpieczanie Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="c3a68-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="c3a68-117">Uzyskaj klucze konta</span><span class="sxs-lookup"><span data-stu-id="c3a68-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c3a68-118">Pobiera klucze podstawowe i pomocnicze zapisu wzorca hello i klucze podstawowe i pomocnicze tylko do odczytu dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="c3a68-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="c3a68-119">Pobierz ciąg połączenia bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="c3a68-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c3a68-120">Pobiera tooconnect ciąg połączenia hello tooyour aplikacji z bazy danych MongoDB konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c3a68-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="c3a68-121">Wygeneruj ponownie klucze konta</span><span class="sxs-lookup"><span data-stu-id="c3a68-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c3a68-122">Generuje ponownie wzorca hello lub tylko do odczytu klucza dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="c3a68-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="c3a68-123">Utworzenie zapory</span><span class="sxs-lookup"><span data-stu-id="c3a68-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="c3a68-124">Tworzy przychodzących IP dostępu kontroli zasad toolimit toohello konto dostępu z zatwierdzonych zbiór maszyny i/lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c3a68-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="c3a68-125">**Wysokiej dostępności, odzyskiwania po awarii, kopia zapasowa i przywracanie**</span><span class="sxs-lookup"><span data-stu-id="c3a68-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="c3a68-126">Konfigurowanie zasad trybu failover</span><span class="sxs-lookup"><span data-stu-id="c3a68-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c3a68-127">Ustawia hello każdego regionu, w której są replikowane konta hello priorytet trybu failover.</span><span class="sxs-lookup"><span data-stu-id="c3a68-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="c3a68-128">**Łączenie z zasobami Azure DB rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="c3a68-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="c3a68-129">Połącz tooAzure aplikacji sieci web DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c3a68-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="c3a68-130">Utwórz i połączenia bazy danych Azure rozwiązania Cosmos bazy danych i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a68-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
