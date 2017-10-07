---
title: "Przykłady środowiska PowerShell dla bazy danych Azure rozwiązania Cosmos aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure PowerShell próbki — toohelp skryptów tworzenia i zarządzania nimi konta bazy danych Azure rozwiązania Cosmos."
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
ms.openlocfilehash: 8815e775f720226e98cc8dcf7743e481c213272b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="25886-103">Przykładów dla platformy Azure środowiska PowerShell dla bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="25886-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="25886-104">Witaj Poniższa tabela zawiera linki toosample programu Azure PowerShell skryptów dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="25886-104">hello following table includes links toosample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="25886-105">**Tworzenie konta bazy danych Azure rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="25886-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="25886-106">Utwórz konto usługi DocumentDB interfejsu API</span><span class="sxs-lookup"><span data-stu-id="25886-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="25886-107">Tworzy pojedynczy toouse konta bazy danych Azure rozwiązania Cosmos hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="25886-107">Creates a single Azure Cosmos DB account toouse with hello DocumentDB API.</span></span> |
|<span data-ttu-id="25886-108">**Skalować rozwiązania Cosmos Azure DB**</span><span class="sxs-lookup"><span data-stu-id="25886-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="25886-109">Replikację bazy danych Azure rozwiązania Cosmos konta w wielu regionach i skonfiguruj priorytetów trybu failover</span><span class="sxs-lookup"><span data-stu-id="25886-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="25886-110">Globalny replikuje dane konta w wielu regionach o priorytecie określonego trybu failover.</span><span class="sxs-lookup"><span data-stu-id="25886-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="25886-111">**Zabezpieczanie Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="25886-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="25886-112">Uzyskaj klucze konta</span><span class="sxs-lookup"><span data-stu-id="25886-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="25886-113">Pobiera klucze podstawowe i pomocnicze zapisu wzorca hello i klucze podstawowe i pomocnicze tylko do odczytu dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="25886-113">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="25886-114">Pobierz ciąg połączenia bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="25886-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="25886-115">Pobiera tooconnect ciąg połączenia hello tooyour aplikacji z bazy danych MongoDB konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="25886-115">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="25886-116">Wygeneruj ponownie klucze konta</span><span class="sxs-lookup"><span data-stu-id="25886-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="25886-117">Generuje ponownie wzorca hello lub tylko do odczytu klucza dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="25886-117">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="25886-118">Utworzenie zapory</span><span class="sxs-lookup"><span data-stu-id="25886-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="25886-119">Tworzy przychodzących IP dostępu kontroli zasad toolimit toohello konto dostępu z zatwierdzonych zbiór maszyny i/lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="25886-119">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="25886-120">**Wysokiej dostępności, odzyskiwania po awarii, kopia zapasowa i przywracanie**</span><span class="sxs-lookup"><span data-stu-id="25886-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="25886-121">Konfigurowanie zasad trybu failover</span><span class="sxs-lookup"><span data-stu-id="25886-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="25886-122">Ustawia hello każdego regionu, w której są replikowane konta hello priorytet trybu failover.</span><span class="sxs-lookup"><span data-stu-id="25886-122">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|||