---
title: "Monitorowanie kondycji zasobów Azure CDN | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie monitorowania kondycji zasobów platformy Azure CDN przy użyciu kondycja zasobów Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="987a2-103">Monitorowanie kondycji zasobów Azure CDN</span><span class="sxs-lookup"><span data-stu-id="987a2-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="987a2-104">Kondycja zasobów sieci CDN w warstwie Azure jest podzbiorem [kondycji zasobów platformy Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="987a2-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="987a2-105">Kondycja zasobów Azure służy do monitorowania kondycji zasobów w sieci CDN i odbierania możliwością wskazówki dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="987a2-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="987a2-106">Kondycja zasobów usługi Azure CDN tylko aktualnie kont kondycji globalne dostarczania CDN i funkcje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="987a2-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="987a2-107">Kondycja zasobów usługi Azure CDN nie weryfikuje poszczególnych punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="987a2-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="987a2-108">Sygnalizuje, że źródła danych usługi Azure CDN kondycja zasobów mogą być opóźnione do 15 minut.</span><span class="sxs-lookup"><span data-stu-id="987a2-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="987a2-109">Jak znaleźć kondycja zasobów Azure CDN</span><span class="sxs-lookup"><span data-stu-id="987a2-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="987a2-110">W [portalu Azure](https://portal.azure.com), przejdź do swojego profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="987a2-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="987a2-111">Kliknij przycisk **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="987a2-111">Click the **Settings** button.</span></span>

    ![Przycisk ustawień](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="987a2-113">W obszarze *pomocy technicznej i rozwiązywania problemów*, kliknij przycisk **kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="987a2-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Kondycja zasobów w sieci CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="987a2-115">Możesz również znaleźć CDN zasobów wymienionych w *kondycja zasobów* kafelka w *Pomoc i obsługa techniczna* bloku.</span><span class="sxs-lookup"><span data-stu-id="987a2-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="987a2-116">Szybki dostęp do *Pomoc i obsługa techniczna* klikając kółku **?**</span><span class="sxs-lookup"><span data-stu-id="987a2-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="987a2-117">w prawym górnym rogu portalu.</span><span class="sxs-lookup"><span data-stu-id="987a2-117">in the upper right corner of the portal.</span></span>
>
> ![Pomoc i obsługa techniczna](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="987a2-119">Azure CDN specyficzne wiadomości</span><span class="sxs-lookup"><span data-stu-id="987a2-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="987a2-120">Stany związane z usługi Azure CDN kondycja zasobów znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="987a2-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="987a2-121">Komunikat</span><span class="sxs-lookup"><span data-stu-id="987a2-121">Message</span></span> | <span data-ttu-id="987a2-122">Zalecane działanie</span><span class="sxs-lookup"><span data-stu-id="987a2-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="987a2-123">Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN</span><span class="sxs-lookup"><span data-stu-id="987a2-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="987a2-124">Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN.</span><span class="sxs-lookup"><span data-stu-id="987a2-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="987a2-125">Niestety, Usługa zarządzania CDN jest obecnie niedostępna</span><span class="sxs-lookup"><span data-stu-id="987a2-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="987a2-126">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie występował po w oczekiwanym czasie rozpoznania, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="987a2-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="987a2-127">Niestety, punktami końcowymi CDN może mieć wpływ bieżących problemów niektóre z naszych dostawców usługi CDN</span><span class="sxs-lookup"><span data-stu-id="987a2-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="987a2-128">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Użyj narzędzia do rozwiązywania problemów, aby dowiedzieć się jak przetestować punkt początkowy i punkt końcowy CDN; Jeśli problem będzie występował po w oczekiwanym czasie rozpoznania, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="987a2-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="987a2-129">Niestety, zmiany w konfiguracji punktu końcowego CDN występują opóźnienia w przepłynie</span><span class="sxs-lookup"><span data-stu-id="987a2-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="987a2-130">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Zmiany w konfiguracji nie są w pełni propagowane w oczekiwanym czasie, należy się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="987a2-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="987a2-131">Niestety, wystąpiły problemy podczas ładowania dodatkowego portalu</span><span class="sxs-lookup"><span data-stu-id="987a2-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="987a2-132">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie występował po w oczekiwanym czasie rozpoznania, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="987a2-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="987a2-133">Niestety, wystąpiły problemy z niektórych naszych dostawców sieci CDN</span><span class="sxs-lookup"><span data-stu-id="987a2-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="987a2-134">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie występował po w oczekiwanym czasie rozpoznania, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="987a2-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="987a2-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="987a2-135">Next steps</span></span>

- [<span data-ttu-id="987a2-136">Zapoznanie się z informacjami o kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="987a2-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="987a2-137">Rozwiązywanie problemów z sieci CDN kompresji</span><span class="sxs-lookup"><span data-stu-id="987a2-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="987a2-138">Rozwiązywanie problemów z błędami 404</span><span class="sxs-lookup"><span data-stu-id="987a2-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)