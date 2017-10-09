---
title: tooAzure aaaIntroduction magazynu kolejek | Dokumentacja firmy Microsoft
description: Wprowadzenie tooAzure magazynu kolejek
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="d6687-103">Wprowadzenie tooQueues</span><span class="sxs-lookup"><span data-stu-id="d6687-103">Introduction tooQueues</span></span>

<span data-ttu-id="d6687-104">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d6687-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="d6687-105">Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6687-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="d6687-106">Najczęstsze zastosowania</span><span class="sxs-lookup"><span data-stu-id="d6687-106">Common uses</span></span>

<span data-ttu-id="d6687-107">Najczęstsze zastosowania usługi Queue Storage obejmują:</span><span class="sxs-lookup"><span data-stu-id="d6687-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="d6687-108">Tworzenie zaległości pracy tooprocess asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="d6687-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="d6687-109">Przekazywanie komunikatów z roli procesu roboczego platformy Azure tooan roli sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6687-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="d6687-110">Pojęcia dotyczące usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="d6687-110">Queue service concepts</span></span>

<span data-ttu-id="d6687-111">Hello usługa kolejki zawiera hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="d6687-111">hello Queue service contains hello following components:</span></span>

![Pojęcia dotyczące kolejki](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="d6687-113">**Format adresu URL:** kolejek mają hello następującego formatu adresu URL:</span><span class="sxs-lookup"><span data-stu-id="d6687-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="d6687-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="d6687-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="d6687-115">Witaj następującego adresu URL dotyczy kolejki w diagramie hello:</span><span class="sxs-lookup"><span data-stu-id="d6687-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="d6687-116">**Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6687-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="d6687-117">Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6687-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="d6687-118">**Kolejka:** kolejka zawiera zestaw komunikatów.</span><span class="sxs-lookup"><span data-stu-id="d6687-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="d6687-119">Wszystkie komunikaty muszą być w kolejce.</span><span class="sxs-lookup"><span data-stu-id="d6687-119">All messages must be in a queue.</span></span> <span data-ttu-id="d6687-120">Należy zauważyć, że nazwa kolejki hello musi być tylko małe litery.</span><span class="sxs-lookup"><span data-stu-id="d6687-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="d6687-121">Informacje dotyczące nazewnictwa kolejek można znaleźć w temacie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Nazewnictwo kolejek i metadanych).</span><span class="sxs-lookup"><span data-stu-id="d6687-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="d6687-122">**Komunikat o błędzie:** A komunikatu, w dowolnym formacie z zapasowej too64 KB.</span><span class="sxs-lookup"><span data-stu-id="d6687-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="d6687-123">Witaj maksymalny czas, który komunikatu może pozostawać w kolejce hello wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="d6687-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6687-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6687-124">Next steps</span></span>

* [<span data-ttu-id="d6687-125">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d6687-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="d6687-126">Wprowadzenie do korzystania z kolejki przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d6687-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
