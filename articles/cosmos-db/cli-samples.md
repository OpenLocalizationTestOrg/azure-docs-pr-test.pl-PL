---
title: "Przykłady interfejsu wiersza polecenia platformy Azure dla platformy Azure rozwiązania Cosmos DB | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="62284-103">Przykładów dla interfejsu wiersza polecenia platformy Azure dla bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="62284-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="62284-104">Poniższa tabela zawiera linki do przykładowe skrypty wiersza polecenia platformy Azure dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="62284-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="62284-105">Odwołanie do strony dla wszystkich poleceń interfejsu wiersza polecenia Azure rozwiązania Cosmos bazy danych są dostępne w [odwołania 2.0 interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="62284-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="62284-106">**Tworzenie konta bazy danych Azure rozwiązania Cosmos, bazy danych i kontenerów**</span><span class="sxs-lookup"><span data-stu-id="62284-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="62284-107">Utwórz konto usługi DocumentDB interfejsu API, wykres lub tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="62284-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="62284-108">Tworzy jednego konta Azure rozwiązania Cosmos DB API, bazy danych i kontener do użycia z usługi DocumentDB, wykres lub interfejsów API tabeli.</span><span class="sxs-lookup"><span data-stu-id="62284-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="62284-109">Tworzenie konta bazy danych MongoDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="62284-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="62284-110">Tworzy jednego interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB konta bazy danych i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="62284-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="62284-111">**Skalować rozwiązania Cosmos Azure DB**</span><span class="sxs-lookup"><span data-stu-id="62284-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="62284-112">Przepływność kontenera skali</span><span class="sxs-lookup"><span data-stu-id="62284-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="62284-113">Zmienia elastycznie througput do kontenera.</span><span class="sxs-lookup"><span data-stu-id="62284-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="62284-114">Replikację bazy danych Azure rozwiązania Cosmos konta bazy danych w wielu regionach i skonfiguruj priorytetów trybu failover</span><span class="sxs-lookup"><span data-stu-id="62284-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="62284-115">Globalny replikuje dane konta w wielu regionach o priorytecie określonego trybu failover.</span><span class="sxs-lookup"><span data-stu-id="62284-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="62284-116">**Zabezpieczanie Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="62284-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="62284-117">Uzyskaj klucze konta</span><span class="sxs-lookup"><span data-stu-id="62284-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="62284-118">Pobiera klucze podstawowe i pomocnicze zapisu głównego i klucze podstawowe i pomocnicze tylko do odczytu dla konta.</span><span class="sxs-lookup"><span data-stu-id="62284-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="62284-119">Pobierz ciąg połączenia bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="62284-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="62284-120">Pobiera parametry połączenia do łączenie aplikacji z bazy danych MongoDB do swojego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="62284-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="62284-121">Wygeneruj ponownie klucze konta</span><span class="sxs-lookup"><span data-stu-id="62284-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="62284-122">Ponowne wygenerowanie klucza głównego lub w trybie tylko do odczytu dla konta.</span><span class="sxs-lookup"><span data-stu-id="62284-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="62284-123">Utworzenie zapory</span><span class="sxs-lookup"><span data-stu-id="62284-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="62284-124">Tworzy przychodzących zasad kontroli dostępu w IP można ograniczyć dostęp do konta z zatwierdzonych zbiór maszyny i/lub usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="62284-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="62284-125">**Wysokiej dostępności, odzyskiwania po awarii, kopia zapasowa i przywracanie**</span><span class="sxs-lookup"><span data-stu-id="62284-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="62284-126">Konfigurowanie zasad trybu failover</span><span class="sxs-lookup"><span data-stu-id="62284-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="62284-127">Ustawia priorytet trybu failover każdego regionu, w którym konta są replikowane.</span><span class="sxs-lookup"><span data-stu-id="62284-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="62284-128">**Łączenie z zasobami Azure DB rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="62284-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="62284-129">Łączenie aplikacji sieci web do bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="62284-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="62284-130">Utwórz i połączenia bazy danych Azure rozwiązania Cosmos bazy danych i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62284-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
