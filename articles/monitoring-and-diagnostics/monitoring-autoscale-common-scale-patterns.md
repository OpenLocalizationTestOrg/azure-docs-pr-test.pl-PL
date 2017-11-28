---
title: aaaOverview typowe wzorce skalowania automatycznego | Dokumentacja firmy Microsoft
description: "Dowiedz się, że niektóre hello typowe wzorce tooauto skalowania zasobu na platformie Azure."
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="9df93-103">Omówienie typowe wzorce skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="9df93-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="9df93-104">W tym artykule opisano niektóre typowe tooscale wzorce hello zasobu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9df93-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="9df93-105">Azure automatyczne skalowanie monitora dotyczy tylko tooVirtual zestawy skalowania maszyny (VMSS), usługi w chmurze, planów usługi aplikacji i środowiska usługi app service.</span><span class="sxs-lookup"><span data-stu-id="9df93-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="9df93-106">Umożliwia wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="9df93-106">Lets get started</span></span>

<span data-ttu-id="9df93-107">W tym artykule przyjęto założenie, że czytelnik zna automatyczne skalowanie.</span><span class="sxs-lookup"><span data-stu-id="9df93-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="9df93-108">Możesz [Pobierz wprowadzenie tooscale tutaj zasobu][1].</span><span class="sxs-lookup"><span data-stu-id="9df93-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="9df93-109">Witaj poniżej przedstawiono niektóre typowe wzorce skali hello.</span><span class="sxs-lookup"><span data-stu-id="9df93-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="9df93-110">Oparte na Procesorze skali</span><span class="sxs-lookup"><span data-stu-id="9df93-110">Scale based on CPU</span></span>

<span data-ttu-id="9df93-111">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="9df93-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="9df93-112">Ma tooscale poza/skali w na podstawie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="9df93-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="9df93-113">Ponadto chcesz tooensure jest minimalna liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="9df93-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="9df93-114">Ponadto chcesz tooensure ustawioną maksymalny limit toohello liczba wystąpień, które można skalować.</span><span class="sxs-lookup"><span data-stu-id="9df93-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Oparte na Procesorze skali][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="9df93-116">Skalowanie inaczej w weekendy vs dni tygodnia</span><span class="sxs-lookup"><span data-stu-id="9df93-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="9df93-117">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="9df93-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="9df93-118">Ma domyślnie wystąpień 3 (w dni robocze)</span><span class="sxs-lookup"><span data-stu-id="9df93-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="9df93-119">Nieoczekiwanie ruchu w weekendy, i dlatego należy tooscale dół too1 wystąpienia w weekendy.</span><span class="sxs-lookup"><span data-stu-id="9df93-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Skalowanie inaczej w weekendy vs dni tygodnia][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="9df93-121">Skalowanie inaczej w dni wolne</span><span class="sxs-lookup"><span data-stu-id="9df93-121">Scale differently during holidays</span></span>

<span data-ttu-id="9df93-122">Aplikacja sieci web (/ VMSS/chmury usługi roli) i</span><span class="sxs-lookup"><span data-stu-id="9df93-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="9df93-123">Ma tooscale góra/dół oparte na użycie procesora CPU domyślnie</span><span class="sxs-lookup"><span data-stu-id="9df93-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="9df93-124">Jednak podczas świąt (lub określone dni, które są ważne dla biznesu) ma domyślne hello toooverride i mieć większej pojemności do Twojej dyspozycji.</span><span class="sxs-lookup"><span data-stu-id="9df93-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Święta inaczej w skali][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="9df93-126">Skalowanie w oparciu metryki niestandardowe</span><span class="sxs-lookup"><span data-stu-id="9df93-126">Scale based on custom metric</span></span>

<span data-ttu-id="9df93-127">Masz frontonu sieci web i warstwy interfejsu API, który komunikuje się z hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9df93-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="9df93-128">Ma tooscale hello interfejsu API warstwy na podstawie zdarzeń niestandardowych w frontonu hello (przykład: chcesz tooscale procesu wyewidencjonowania na podstawie hello liczby elementów w koszyku hello)</span><span class="sxs-lookup"><span data-stu-id="9df93-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Skalowanie w oparciu metryki niestandardowe][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png