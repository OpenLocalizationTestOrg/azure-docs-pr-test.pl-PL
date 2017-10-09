---
title: "aaaMonitor hello kondycji zasobów Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure CDN przy użyciu kondycja zasobów Azure."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="1fd31-103">Monitorowanie kondycji hello zasobów Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1fd31-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="1fd31-104">Kondycja zasobów sieci CDN w warstwie Azure jest podzbiorem [kondycji zasobów platformy Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fd31-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="1fd31-105">Można używać zasobów platformy Azure kondycji toomonitor hello kondycji zasobów w sieci CDN i odbierać wskazówki można wykonać tootroubleshoot problemów.</span><span class="sxs-lookup"><span data-stu-id="1fd31-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="1fd31-106">Kondycja zasobów usługi Azure CDN tylko aktualnie kont kondycji hello globalne dostarczania CDN i funkcje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1fd31-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="1fd31-107">Kondycja zasobów usługi Azure CDN nie weryfikuje poszczególnych punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="1fd31-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="1fd31-108">Witaj sygnalizuje, że źródła danych usługi Azure CDN kondycja zasobów może być aktywne minut too15 opóźnione.</span><span class="sxs-lookup"><span data-stu-id="1fd31-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="1fd31-109">Jak toofind kondycja zasobów Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1fd31-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="1fd31-110">W hello [portalu Azure](https://portal.azure.com), Przeglądaj tooyour profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="1fd31-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="1fd31-111">Kliknij przycisk hello **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1fd31-111">Click hello **Settings** button.</span></span>

    ![Przycisk ustawień](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="1fd31-113">W obszarze *pomocy technicznej i rozwiązywania problemów*, kliknij przycisk **kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="1fd31-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Kondycja zasobów w sieci CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="1fd31-115">Możesz również znaleźć CDN zasobów wymienionych w hello *kondycja zasobów* kafelka w hello *Pomoc i obsługa techniczna* bloku.</span><span class="sxs-lookup"><span data-stu-id="1fd31-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="1fd31-116">Szybki dostęp zbyt*Pomoc i obsługa techniczna* klikając hello kółku **?**</span><span class="sxs-lookup"><span data-stu-id="1fd31-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="1fd31-117">w hello prawym górnym rogu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="1fd31-117">in hello upper right corner of hello portal.</span></span>
>
> ![Pomoc i obsługa techniczna](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="1fd31-119">Azure CDN specyficzne wiadomości</span><span class="sxs-lookup"><span data-stu-id="1fd31-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="1fd31-120">Kondycja zasobów w sieci CDN tooAzure powiązane stany znajdują się poniżej.</span><span class="sxs-lookup"><span data-stu-id="1fd31-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="1fd31-121">Komunikat</span><span class="sxs-lookup"><span data-stu-id="1fd31-121">Message</span></span> | <span data-ttu-id="1fd31-122">Zalecane działanie</span><span class="sxs-lookup"><span data-stu-id="1fd31-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="1fd31-123">Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN</span><span class="sxs-lookup"><span data-stu-id="1fd31-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="1fd31-124">Użytkownik może mieć zatrzymana, usunięte lub błędnie skonfigurowane co najmniej jednego z punktami końcowymi CDN.</span><span class="sxs-lookup"><span data-stu-id="1fd31-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="1fd31-125">Niestety, hello CDN Usługa zarządzania jest obecnie niedostępna</span><span class="sxs-lookup"><span data-stu-id="1fd31-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="1fd31-126">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1fd31-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="1fd31-127">Niestety, punktami końcowymi CDN może mieć wpływ bieżących problemów niektóre z naszych dostawców usługi CDN</span><span class="sxs-lookup"><span data-stu-id="1fd31-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="1fd31-128">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jak używać hello rozwiązywanie narzędzie toolearn tootest Twojego punkt początkowy i punkt końcowy CDN; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1fd31-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="1fd31-129">Niestety, zmiany w konfiguracji punktu końcowego CDN występują opóźnienia w przepłynie</span><span class="sxs-lookup"><span data-stu-id="1fd31-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="1fd31-130">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Zmiany w konfiguracji nie są w pełni propagowane w hello oczekiwany czas, należy się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1fd31-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="1fd31-131">Niestety, wystąpiły problemy podczas ładowania portalu dodatkowym hello</span><span class="sxs-lookup"><span data-stu-id="1fd31-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="1fd31-132">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1fd31-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="1fd31-133">Niestety, wystąpiły problemy z niektórych naszych dostawców sieci CDN</span><span class="sxs-lookup"><span data-stu-id="1fd31-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="1fd31-134">Zaglądaj tu, aby zobaczyć aktualizacje stanu; Jeśli problem będzie nadal występować po hello oczekiwany czas rozpoznawania nazw, skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1fd31-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1fd31-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fd31-135">Next steps</span></span>

- [<span data-ttu-id="1fd31-136">Zapoznanie się z informacjami o kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1fd31-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="1fd31-137">Rozwiązywanie problemów z sieci CDN kompresji</span><span class="sxs-lookup"><span data-stu-id="1fd31-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="1fd31-138">Rozwiązywanie problemów z błędami 404</span><span class="sxs-lookup"><span data-stu-id="1fd31-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)