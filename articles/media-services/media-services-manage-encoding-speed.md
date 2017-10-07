---
title: "szybkość Zarządzaj aaa i współbieżność kodowania usłudze Azure Media Services | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera krótkie omówienie sposobu zarządzania szybkość i współbieżność kodowania zadań/zadań z usługi Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="4fcf7-103">Zarządzanie szybkość i współbieżności z kodowaniem</span><span class="sxs-lookup"><span data-stu-id="4fcf7-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="4fcf7-104">Ten artykuł zawiera krótkie omówienie sposobu zarządzania szybkość i współbieżność zadań/zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="4fcf7-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4fcf7-105">Overview</span></span>

<span data-ttu-id="4fcf7-106">W usłudze Media Services **typ jednostki zarezerwowane** określa szybkość hello przetwarzania zadania przetwarzania multimediów.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="4fcf7-107">Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="4fcf7-108">Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="4fcf7-109">Witaj [skalowania jednostki kodowania](media-services-scale-media-processing-overview.md) tematu zawiera tabelę, która ułatwia podjęcie decyzji, wybierając między różnych szybkościach kodowania.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="4fcf7-110">Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision Twojego konta z **jednostki zarezerwowanego**.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="4fcf7-111">Liczba Hello elastycznie jednostki zarezerwowanego określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="4fcf7-112">Na przykład jeśli konto ma pięć jednostki zarezerwowanego, następnie nośnika pięć zadań będą uruchomione jednocześnie tak długo, jak istnieją toobe zadania przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="4fcf7-113">Witaj pozostałych zadań będzie czekać w kolejce hello i zostanie pobrana uzyskać przetwarzania sekwencyjnie, po zakończeniu uruchomione zadanie.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="4fcf7-114">Jeśli konto nie ma żadnych jednostek zarezerwowanego zainicjowano obsługę administracyjną, następnie zadania będą pobierane po kolei.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="4fcf7-115">W takim przypadku hello czas oczekiwania między jeden Kończenie zadań i hello uruchomienie kolejnej będzie zależeć od hello dostępność zasobów w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="4fcf7-116">Aby uzyskać szczegółowe informacje i przykłady przedstawiające tooscale jednostki kodowania, zobacz temat [to](media-services-scale-media-processing-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="4fcf7-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="4fcf7-117">Następny krok</span><span class="sxs-lookup"><span data-stu-id="4fcf7-117">Next step</span></span>

[<span data-ttu-id="4fcf7-118">Kodowania jednostki skalowania</span><span class="sxs-lookup"><span data-stu-id="4fcf7-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="4fcf7-119">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="4fcf7-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fcf7-120">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="4fcf7-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

