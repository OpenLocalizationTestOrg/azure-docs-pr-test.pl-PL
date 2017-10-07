---
title: "toodo aaaWhat w przypadku hello Azure zakłócenia, który ma wpływ na usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie toodo w przypadku hello Azure zakłócenia, który ma wpływ na usługi Azure Key Vault."
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="c5958-103">Usługa Azure Key Vault dostępność i nadmiarowość</span><span class="sxs-lookup"><span data-stu-id="c5958-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="c5958-104">Usługa Azure Key Vault funkcjami wielu warstw nadmiarowość toomake się, że Twoje klucze i klucze tajne nadal dostępne tooyour aplikacji, nawet jeśli pojedynczych składników hello usług kończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c5958-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="c5958-105">Witaj zawartość magazynu kluczy są replikowane w obrębie regionu hello i region pomocniczy tooa co najmniej 150 mil optymalizacji, ale w hello tej samej lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="c5958-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="c5958-106">Zapewnia to dostępność wysoką trwałością kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="c5958-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="c5958-107">Zobacz hello [Azure łączyć regionów](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) dokumentu szczegółowe informacje dotyczące konkretnego regionu pary.</span><span class="sxs-lookup"><span data-stu-id="c5958-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="c5958-108">Jeśli pojedynczych składników w ramach usługi Magazyn kluczy hello zakończą się niepowodzeniem, alternatywne składniki w obrębie regionu hello kroku w tooserve Twojego żądania toomake się, że nie jest bez spadku funkcji.</span><span class="sxs-lookup"><span data-stu-id="c5958-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="c5958-109">Nie trzeba tootake tootrigger żadnych akcji to.</span><span class="sxs-lookup"><span data-stu-id="c5958-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="c5958-110">On odbywa się automatycznie i będzie tooyou przezroczysty.</span><span class="sxs-lookup"><span data-stu-id="c5958-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="c5958-111">W przypadku rzadkich hello niedostępności całego regionu Azure, żądania hello, wprowadzone z usługi Azure Key Vault w tym regionie automatycznie są kierowane (*przejścia w tryb failover*) tooa regionie pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="c5958-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="c5958-112">Gdy regionu podstawowego hello jest ponownie dostępny, żądania są kierowane Wstecz (*nie powiodło się wstecz*) toohello regionu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="c5958-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="c5958-113">Ponownie nie trzeba tootake żadnych akcji, ponieważ jest to wykonywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c5958-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="c5958-114">Znane są kilka toobe ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="c5958-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="c5958-115">W przypadku hello Failover region może potrwać kilka minut, aż hello toofail usługi za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="c5958-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="c5958-116">Żądania, które zostały wprowadzone w tym czasie może zakończyć się niepowodzeniem, dopóki nie zakończy pracy awaryjnej hello.</span><span class="sxs-lookup"><span data-stu-id="c5958-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="c5958-117">Po zakończeniu pracy w trybie failover magazynu kluczy jest w trybie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="c5958-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="c5958-118">Żądania, które są obsługiwane w tym trybie są:</span><span class="sxs-lookup"><span data-stu-id="c5958-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="c5958-119">Lista magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="c5958-119">List key vaults</span></span>
  * <span data-ttu-id="c5958-120">Pobierz właściwości magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="c5958-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="c5958-121">Utwórz listę kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="c5958-121">List secrets</span></span>
  * <span data-ttu-id="c5958-122">Pobierz kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="c5958-122">Get secrets</span></span>
  * <span data-ttu-id="c5958-123">Lista kluczy</span><span class="sxs-lookup"><span data-stu-id="c5958-123">List keys</span></span>
  * <span data-ttu-id="c5958-124">Pobieranie kluczy (właściwości)</span><span class="sxs-lookup"><span data-stu-id="c5958-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="c5958-125">Szyfrowanie</span><span class="sxs-lookup"><span data-stu-id="c5958-125">Encrypt</span></span>
  * <span data-ttu-id="c5958-126">Odszyfrowywanie</span><span class="sxs-lookup"><span data-stu-id="c5958-126">Decrypt</span></span>
  * <span data-ttu-id="c5958-127">Zawijaj</span><span class="sxs-lookup"><span data-stu-id="c5958-127">Wrap</span></span>
  * <span data-ttu-id="c5958-128">Dekodowanie</span><span class="sxs-lookup"><span data-stu-id="c5958-128">Unwrap</span></span>
  * <span data-ttu-id="c5958-129">Weryfikuj</span><span class="sxs-lookup"><span data-stu-id="c5958-129">Verify</span></span>
  * <span data-ttu-id="c5958-130">Zaloguj się</span><span class="sxs-lookup"><span data-stu-id="c5958-130">Sign</span></span>
  * <span data-ttu-id="c5958-131">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="c5958-131">Backup</span></span>
* <span data-ttu-id="c5958-132">Po przejściu w tryb failover nie jest ponownie, wszystkie żądania typy (w tym odczytu *i* żądań zapisu) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="c5958-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

