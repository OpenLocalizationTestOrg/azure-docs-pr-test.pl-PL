---
title: "aaaAdd odwołanie do zestawu danych tooyour Azure czas serii Insights środowiska | Dokumentacja firmy Microsoft"
description: "W tym samouczku Dodaj odwołanie do zestawu danych tooyour Insights serii czasu środowiska"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="60d8e-103">Tworzenie zestawu danych odwołania dla danego środowiska Insights serii czasu za pomocą portalu Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="60d8e-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="60d8e-104">Odwołanie do zestawu danych jest kolekcją elementów, które zostały rozszerzone przy użyciu hello zdarzenia ze źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="60d8e-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="60d8e-105">Aparat transferu danych przychodzących usługi Time Series Insights łączy zdarzenie ze źródła zdarzenia z elementem w zestawie danych referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="60d8e-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="60d8e-106">To rozszerzone zdarzenie jest następnie dostępne dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="60d8e-106">This augmented event is then available for query.</span></span> <span data-ttu-id="60d8e-107">Tego sprzężenia jest oparta na powitania kluczy zdefiniowane w zestawie danych odwołania.</span><span class="sxs-lookup"><span data-stu-id="60d8e-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="60d8e-108">Kroki tooadd środowisku tooyour odwołanie do zestawu danych</span><span class="sxs-lookup"><span data-stu-id="60d8e-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="60d8e-109">Zaloguj się toohello [portalu Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60d8e-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="60d8e-110">Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie portalu Ibiza hello hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="60d8e-111">Wybierz środowisko usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="60d8e-111">Select your Time Series Insights environment.</span></span>

    ![Utworzenie zestawu danych odwołania Insights serii czasu hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="60d8e-113">Wybierz opcję „Zestawy danych referencyjnych”, kliknij przycisk „+ Dodaj”.</span><span class="sxs-lookup"><span data-stu-id="60d8e-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Utworzenie zestawu danych hello czasu serii Insights odwołanie - szczegóły](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="60d8e-115">Określ nazwę zestawu danych odwołania hello hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="60d8e-116">Określ nazwę klucza hello i jego typu.</span><span class="sxs-lookup"><span data-stu-id="60d8e-116">Specify hello key name and its type.</span></span> <span data-ttu-id="60d8e-117">Ta nazwa i typ jest używane toopick hello prawidłowe właściwości ze zdarzenia hello w źródle zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="60d8e-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="60d8e-118">Na przykład jeśli podasz nazwę klucza jako "DeviceId" i typu "String" hello czasu Insights serii wejściowych aparat wyszukuje właściwości o nazwie hello "DeviceId" typu "String" hello zdarzenia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="60d8e-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="60d8e-119">Musisz podać więcej niż jednego klucza toojoin ze zdarzeniem hello.</span><span class="sxs-lookup"><span data-stu-id="60d8e-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="60d8e-120">Właściwość Hello musi odpowiadać nazwie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="60d8e-120">hello property name match is case-sensitive.</span></span>

     ![Utworzenie zestawu danych hello czasu serii Insights odwołanie - szczegóły](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="60d8e-122">Kliknij przycisk „Utwórz”.</span><span class="sxs-lookup"><span data-stu-id="60d8e-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="60d8e-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60d8e-123">Next steps</span></span>

* <span data-ttu-id="60d8e-124">[Zarządzanie danymi referencyjnymi](time-series-insights-manage-reference-data-csharp.md) na drodze programowej.</span><span class="sxs-lookup"><span data-stu-id="60d8e-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="60d8e-125">Aby hello pełną dokumentację interfejsu API, zobacz [odwołania API danych](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="60d8e-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
