---
title: "aaaAzure wewnętrzne niezawodnej Menedżer stanu usługi sieci szkieletowej i niezawodne kolekcji | Dokumentacja firmy Microsoft"
description: "Nowości dotyczące pojęć niezawodnej kolekcji i Projekt w sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="2900c-103">Menedżer stanu niezawodny sieci szkieletowej usług Azure i niezawodne kolekcji wewnętrzne</span><span class="sxs-lookup"><span data-stu-id="2900c-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="2900c-104">Ten dokument delves wewnątrz niezawodnej Menedżer stanu i niezawodne kolekcji toosee działanie podstawowe składniki tle hello.</span><span class="sxs-lookup"><span data-stu-id="2900c-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="2900c-105">Ten dokument jest w toku.</span><span class="sxs-lookup"><span data-stu-id="2900c-105">This document is work in-progress.</span></span> <span data-ttu-id="2900c-106">Dodaj komentarz toothis artykuł tootell nam tematu, które chcesz toolearn więcej informacji na temat.</span><span class="sxs-lookup"><span data-stu-id="2900c-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="2900c-107">Model trwałości lokalnego: dziennika i punktu kontrolnego</span><span class="sxs-lookup"><span data-stu-id="2900c-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="2900c-108">Hello niezawodnej Menedżer stanu i niezawodne kolekcje wykonaj modelu trwałości, który jest nazywany dziennika i punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="2900c-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="2900c-109">W tym modelu każdej zmiany stanu jest rejestrowane jako pierwsze na dysku, a następnie stosowane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="2900c-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="2900c-110">Stan ukończenia Hello sam jest trwały sporadycznie ()</span><span class="sxs-lookup"><span data-stu-id="2900c-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="2900c-111">Punkt kontrolny).</span><span class="sxs-lookup"><span data-stu-id="2900c-111">Checkpoint).</span></span>
<span data-ttu-id="2900c-112">Hello korzyścią jest to, że wystąpiły są przekształcane w sekwencyjnych zapisów tylko Dołącz na dysku dla lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="2900c-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="2900c-113">toobetter zrozumieć hello dziennika i modelu punkt kontrolny, najpierw Przyjrzyjmy się hello nieskończone dysku scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2900c-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="2900c-114">Witaj niezawodnej Menedżer stanu rejestruje każdej operacji przed ich replikacji.</span><span class="sxs-lookup"><span data-stu-id="2900c-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="2900c-115">Rejestrowanie umożliwia hello niezawodnej kolekcje tooapply hello operacji tylko w pamięci.</span><span class="sxs-lookup"><span data-stu-id="2900c-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="2900c-116">Ponieważ dzienniki są trwałe, nawet wtedy, gdy replika hello nie powiedzie się i wymaga ponownego uruchomienia, toobe hello niezawodnej Menedżer stanu ma za mało informacji w jej tooreplay dziennika wszystkie operacje hello, który utracił hello repliki.</span><span class="sxs-lookup"><span data-stu-id="2900c-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="2900c-117">Dysk hello jest nieograniczony, rekordów dziennika nigdy nie należy usunąć toobe i hello niezawodnej kolekcji musi toomanage tylko hello stan w pamięci.</span><span class="sxs-lookup"><span data-stu-id="2900c-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="2900c-118">Teraz Przyjrzyjmy się hello skończoną dysku scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2900c-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="2900c-119">Jak accumulate rekordów dziennika, uruchomić hello niezawodnej Menedżer stanu mało miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="2900c-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="2900c-120">Przed tak się stanie, hello niezawodnej Menedżer stanu musi tootruncate jego miejsca toomake dziennika hello nowszej rekordów.</span><span class="sxs-lookup"><span data-stu-id="2900c-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="2900c-121">Żądania menedżera stanu niezawodny hello toocheckpoint niezawodnej kolekcje toodisk ich stan w pamięci.</span><span class="sxs-lookup"><span data-stu-id="2900c-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="2900c-122">W tym momencie hello niezawodnej kolekcje czy utrwalić stanu w pamięci.</span><span class="sxs-lookup"><span data-stu-id="2900c-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="2900c-123">Po kolekcje niezawodnej hello ukończyć ich punkty kontrolne, hello niezawodnej menedżera stanu można obciąć hello dziennika toofree miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="2900c-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="2900c-124">Gdy repliki hello musi ponownie uruchomić toobe, niezawodne kolekcje odzyskać ich użyciu stan, a hello niezawodnej Menedżer stanu odzyskuje i odtwarza wszystkie zmiany stanu hello, które od czasu ostatniego punktu kontrolnego hello.</span><span class="sxs-lookup"><span data-stu-id="2900c-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="2900c-125">Dodaj inną wartość z procesu tworzenia punktów kontrolnych jest zwiększa czasy odzyskiwania w typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2900c-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="2900c-126">Dziennik zawiera wszystkie operacje, które miały miejsce od czasu ostatniego punktu kontrolnego hello.</span><span class="sxs-lookup"><span data-stu-id="2900c-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="2900c-127">Dlatego może zawierać wiele wersji elementu, takich jak wiele wartości dla danego wiersza w słowniku niezawodne.</span><span class="sxs-lookup"><span data-stu-id="2900c-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="2900c-128">Z kolei niezawodnej kolekcji punktów kontrolnych hello tylko najnowszą wersję każdej wartości dla klucza.</span><span class="sxs-lookup"><span data-stu-id="2900c-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2900c-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2900c-129">Next steps</span></span>
* [<span data-ttu-id="2900c-130">Transakcje i blokad</span><span class="sxs-lookup"><span data-stu-id="2900c-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

