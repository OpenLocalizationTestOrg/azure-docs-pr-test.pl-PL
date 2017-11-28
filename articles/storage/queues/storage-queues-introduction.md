---
title: Wprowadzenie do magazynu kolejek Azure | Dokumentacja firmy Microsoft
description: Wprowadzenie do magazynu kolejek Azure
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="ea916-103">Wprowadzenie do kolejek</span><span class="sxs-lookup"><span data-stu-id="ea916-103">Introduction to Queues</span></span>

<span data-ttu-id="ea916-104">Azure Queue Storage to usługa do przechowywania dużej liczby komunikatów, do której można uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ea916-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="ea916-105">Pojedynczy komunikat z kolejki nie może przekraczać 64 KB, a kolejka może zawierać miliony komunikatów — maksymalnie liczbę nieprzekraczającą całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea916-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="ea916-106">Najczęstsze zastosowania</span><span class="sxs-lookup"><span data-stu-id="ea916-106">Common uses</span></span>

<span data-ttu-id="ea916-107">Najczęstsze zastosowania usługi Queue Storage obejmują:</span><span class="sxs-lookup"><span data-stu-id="ea916-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="ea916-108">Tworzenie zaległości pracy do przetwarzania asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="ea916-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="ea916-109">Przekazywanie komunikatów z roli sieci Web platformy Azure do roli procesu roboczego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea916-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="ea916-110">Pojęcia dotyczące usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="ea916-110">Queue service concepts</span></span>

<span data-ttu-id="ea916-111">Usługa kolejki zawiera następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="ea916-111">The Queue service contains the following components:</span></span>

![Pojęcia dotyczące kolejki](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="ea916-113">**Format adresu URL:** adresy URL kolejek mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="ea916-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="ea916-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="ea916-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="ea916-115">Następujący adres URL dotyczy kolejki w schemacie:</span><span class="sxs-lookup"><span data-stu-id="ea916-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="ea916-116">**Konto magazynu:** dostęp do usługi Azure Storage odbywa się za pośrednictwem konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea916-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="ea916-117">Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea916-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="ea916-118">**Kolejka:** kolejka zawiera zestaw komunikatów.</span><span class="sxs-lookup"><span data-stu-id="ea916-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="ea916-119">Wszystkie komunikaty muszą być w kolejce.</span><span class="sxs-lookup"><span data-stu-id="ea916-119">All messages must be in a queue.</span></span> <span data-ttu-id="ea916-120">Pamiętaj, że nazwa kolejki może zawierać tylko małe litery.</span><span class="sxs-lookup"><span data-stu-id="ea916-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="ea916-121">Informacje dotyczące nazewnictwa kolejek można znaleźć w temacie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Nazewnictwo kolejek i metadanych).</span><span class="sxs-lookup"><span data-stu-id="ea916-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="ea916-122">**Komunikat**: komunikat w dowolnym formacie, o maksymalnym rozmiarze 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ea916-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="ea916-123">Maksymalny czas, który komunikatu może pozostawać w kolejce wynosi siedem dni.</span><span class="sxs-lookup"><span data-stu-id="ea916-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea916-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ea916-124">Next steps</span></span>

* [<span data-ttu-id="ea916-125">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="ea916-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="ea916-126">Wprowadzenie do korzystania z kolejki przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="ea916-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
