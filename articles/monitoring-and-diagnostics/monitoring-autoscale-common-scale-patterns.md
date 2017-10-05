---
title: "Omówienie typowe wzorce skalowania automatycznego | Dokumentacja firmy Microsoft"
description: "Dowiedz się, niektóre typowe wzorce do automatycznego skalowania zasobu na platformie Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="966f8-103">Omówienie typowe wzorce skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="966f8-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="966f8-104">W tym artykule opisano niektóre typowe wzorce skalowania zasobu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="966f8-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="966f8-105">Azure automatyczne skalowanie monitora dotyczy tylko zestawów skali maszyny wirtualnej (VMSS), usługi w chmurze, planów usługi aplikacji i środowiska usługi app service.</span><span class="sxs-lookup"><span data-stu-id="966f8-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="966f8-106">Umożliwia wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="966f8-106">Lets get started</span></span>

<span data-ttu-id="966f8-107">W tym artykule przyjęto założenie, że czytelnik zna automatyczne skalowanie.</span><span class="sxs-lookup"><span data-stu-id="966f8-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="966f8-108">Możesz [tutaj wprowadzenie do skalowania zasobu][1].</span><span class="sxs-lookup"><span data-stu-id="966f8-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="966f8-109">Poniżej przedstawiono niektóre typowe wzorce skali.</span><span class="sxs-lookup"><span data-stu-id="966f8-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="966f8-110">Oparte na Procesorze skali</span><span class="sxs-lookup"><span data-stu-id="966f8-110">Scale based on CPU</span></span>

<span data-ttu-id="966f8-111">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="966f8-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="966f8-112">Aby skalowania w poziomie/skali w na podstawie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="966f8-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="966f8-113">Ponadto chcesz upewnij się, że minimalna liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="966f8-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="966f8-114">Ponadto chcesz zapewnić ustawienie limitu maksymalnej liczby wystąpień, które można skalować.</span><span class="sxs-lookup"><span data-stu-id="966f8-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Oparte na Procesorze skali][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="966f8-116">Skalowanie inaczej w weekendy vs dni tygodnia</span><span class="sxs-lookup"><span data-stu-id="966f8-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="966f8-117">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="966f8-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="966f8-118">Ma domyślnie wystąpień 3 (w dni robocze)</span><span class="sxs-lookup"><span data-stu-id="966f8-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="966f8-119">Nieoczekiwanie ruchu w weekendy, i dlatego ma być skalowana do 1 wystąpienie w weekendy.</span><span class="sxs-lookup"><span data-stu-id="966f8-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Skalowanie inaczej w weekendy vs dni tygodnia][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="966f8-121">Skalowanie inaczej w dni wolne</span><span class="sxs-lookup"><span data-stu-id="966f8-121">Scale differently during holidays</span></span>

<span data-ttu-id="966f8-122">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="966f8-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="966f8-123">Chcesz skalować w górę/dół oparte na użycie procesora CPU domyślnie</span><span class="sxs-lookup"><span data-stu-id="966f8-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="966f8-124">Jednak podczas świąt (lub określone dni, które są ważne dla biznesu) chcesz zastąpić wartości domyślne i mieć większej pojemności do Twojej dyspozycji.</span><span class="sxs-lookup"><span data-stu-id="966f8-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Święta inaczej w skali][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="966f8-126">Skalowanie w oparciu metryki niestandardowe</span><span class="sxs-lookup"><span data-stu-id="966f8-126">Scale based on custom metric</span></span>

<span data-ttu-id="966f8-127">Masz frontonu sieci web i warstwy interfejsu API, który komunikuje się z wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="966f8-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="966f8-128">Aby skalować warstwę interfejsu API na podstawie niestandardowych zdarzeń frontonu (przykład: chcesz skalować procesu wyewidencjonowania na podstawie liczby elementów w koszyku)</span><span class="sxs-lookup"><span data-stu-id="966f8-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Skalowanie w oparciu metryki niestandardowe][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png