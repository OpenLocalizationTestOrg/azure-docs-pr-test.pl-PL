---
title: "Co robić w przypadku platformy Azure usługa przerw w działaniu, który ma wpływ na usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co należy zrobić w przypadku Azure zakłócenia, który ma wpływ na usługi Azure Key Vault."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="ee18f-103">Usługa Azure Key Vault dostępność i nadmiarowość</span><span class="sxs-lookup"><span data-stu-id="ee18f-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="ee18f-104">Usługa Azure Key Vault funkcjami wielu warstw nadmiarowość, aby upewnić się, że kluczy i kluczy tajnych pozostają dostępne dla aplikacji nawet w przypadku awarii poszczególnych składników usługi.</span><span class="sxs-lookup"><span data-stu-id="ee18f-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="ee18f-105">Zawartość magazynu kluczy są replikowane w regionie i w regionie pomocniczym co najmniej 150 mil optymalizacji, ale w tej samej lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="ee18f-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="ee18f-106">Zapewnia to dostępność wysoką trwałością kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="ee18f-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="ee18f-107">Zobacz [Azure łączyć regionów](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) dokumentu szczegółowe informacje dotyczące konkretnego regionu pary.</span><span class="sxs-lookup"><span data-stu-id="ee18f-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="ee18f-108">W przypadku awarii pojedynczych składników w usłudze magazyn kluczy, alternatywne składniki w regionie kroku obsługiwać Twoje żądanie, aby upewnić się, że nie jest bez spadku funkcji.</span><span class="sxs-lookup"><span data-stu-id="ee18f-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="ee18f-109">Nie trzeba wykonywać żadnych czynności w celu wyzwolenia to.</span><span class="sxs-lookup"><span data-stu-id="ee18f-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="ee18f-110">Odbywa się automatycznie, a ma być przezroczysty dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ee18f-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="ee18f-111">W rzadkich niedostępności całego regionu Azure, automatycznie są kierowane żądań, które należy z usługi Azure Key Vault w tym regionie (*przejścia w tryb failover*) w regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="ee18f-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="ee18f-112">Gdy ponownie jest dostępna w regionie podstawowym, żądania są kierowane Wstecz (*nie powiodło się wstecz*) w regionie podstawowym.</span><span class="sxs-lookup"><span data-stu-id="ee18f-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="ee18f-113">Ponownie nie ma potrzeby podejmować żadnych działań, ponieważ jest to wykonywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ee18f-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="ee18f-114">Istnieje kilka ostrzeżenia pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="ee18f-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="ee18f-115">W przypadku trybu failover regionu może upłynąć kilka minut, aż usługi do pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="ee18f-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="ee18f-116">Żądania, które zostały wprowadzone w tym czasie może zakończyć się niepowodzeniem, dopóki nie zakończy pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="ee18f-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="ee18f-117">Po zakończeniu pracy w trybie failover magazynu kluczy jest w trybie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ee18f-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="ee18f-118">Żądania, które są obsługiwane w tym trybie są:</span><span class="sxs-lookup"><span data-stu-id="ee18f-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="ee18f-119">Lista magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="ee18f-119">List key vaults</span></span>
  * <span data-ttu-id="ee18f-120">Pobierz właściwości magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="ee18f-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="ee18f-121">Utwórz listę kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="ee18f-121">List secrets</span></span>
  * <span data-ttu-id="ee18f-122">Pobierz kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="ee18f-122">Get secrets</span></span>
  * <span data-ttu-id="ee18f-123">Lista kluczy</span><span class="sxs-lookup"><span data-stu-id="ee18f-123">List keys</span></span>
  * <span data-ttu-id="ee18f-124">Pobieranie kluczy (właściwości)</span><span class="sxs-lookup"><span data-stu-id="ee18f-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="ee18f-125">Szyfrowanie</span><span class="sxs-lookup"><span data-stu-id="ee18f-125">Encrypt</span></span>
  * <span data-ttu-id="ee18f-126">Odszyfrowywanie</span><span class="sxs-lookup"><span data-stu-id="ee18f-126">Decrypt</span></span>
  * <span data-ttu-id="ee18f-127">Zawijaj</span><span class="sxs-lookup"><span data-stu-id="ee18f-127">Wrap</span></span>
  * <span data-ttu-id="ee18f-128">Dekodowanie</span><span class="sxs-lookup"><span data-stu-id="ee18f-128">Unwrap</span></span>
  * <span data-ttu-id="ee18f-129">Weryfikuj</span><span class="sxs-lookup"><span data-stu-id="ee18f-129">Verify</span></span>
  * <span data-ttu-id="ee18f-130">Zaloguj się</span><span class="sxs-lookup"><span data-stu-id="ee18f-130">Sign</span></span>
  * <span data-ttu-id="ee18f-131">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ee18f-131">Backup</span></span>
* <span data-ttu-id="ee18f-132">Po przejściu w tryb failover nie jest ponownie, wszystkie żądania typy (w tym odczytu *i* żądań zapisu) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="ee18f-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

