---
title: "Przykłady programu Azure PowerShell dotyczące rozwiązania Cosmos Azure DB | Dokumentacja firmy Microsoft"
description: "Azure PowerShell próbki — skryptów ułatwiających tworzenie i zarządzanie kontami bazy danych Azure rozwiązania Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="56a83-103">Przykładów dla platformy Azure środowiska PowerShell dla bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="56a83-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="56a83-104">Poniższa tabela zawiera linki do przykładowe skrypty programu PowerShell systemu Azure dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="56a83-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="56a83-105">**Tworzenie konta bazy danych Azure rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="56a83-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="56a83-106">Utwórz konto usługi DocumentDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="56a83-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="56a83-107">Tworzy jednego konta Azure rozwiązania Cosmos DB do użycia przy użyciu interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="56a83-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="56a83-108">**Skalować rozwiązania Cosmos Azure DB**</span><span class="sxs-lookup"><span data-stu-id="56a83-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="56a83-109">Replikację bazy danych Azure rozwiązania Cosmos konta w wielu regionach i skonfiguruj priorytetów trybu failover</span><span class="sxs-lookup"><span data-stu-id="56a83-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="56a83-110">Globalny replikuje dane konta w wielu regionach o priorytecie określonego trybu failover.</span><span class="sxs-lookup"><span data-stu-id="56a83-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="56a83-111">**Zabezpieczanie Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="56a83-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="56a83-112">Uzyskaj klucze konta</span><span class="sxs-lookup"><span data-stu-id="56a83-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="56a83-113">Pobiera klucze podstawowe i pomocnicze zapisu głównego i klucze podstawowe i pomocnicze tylko do odczytu dla konta.</span><span class="sxs-lookup"><span data-stu-id="56a83-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="56a83-114">Pobierz ciąg połączenia bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="56a83-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="56a83-115">Pobiera parametry połączenia do łączenie aplikacji z bazy danych MongoDB do swojego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="56a83-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="56a83-116">Wygeneruj ponownie klucze konta</span><span class="sxs-lookup"><span data-stu-id="56a83-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="56a83-117">Ponowne wygenerowanie klucza głównego lub w trybie tylko do odczytu dla konta.</span><span class="sxs-lookup"><span data-stu-id="56a83-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="56a83-118">Utworzenie zapory</span><span class="sxs-lookup"><span data-stu-id="56a83-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="56a83-119">Tworzy przychodzących zasad kontroli dostępu w IP można ograniczyć dostęp do konta z zatwierdzonych zbiór maszyny i/lub usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="56a83-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="56a83-120">**Wysokiej dostępności, odzyskiwania po awarii, kopia zapasowa i przywracanie**</span><span class="sxs-lookup"><span data-stu-id="56a83-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="56a83-121">Konfigurowanie zasad trybu failover</span><span class="sxs-lookup"><span data-stu-id="56a83-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="56a83-122">Ustawia priorytet trybu failover każdego regionu, w którym konta są replikowane.</span><span class="sxs-lookup"><span data-stu-id="56a83-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||