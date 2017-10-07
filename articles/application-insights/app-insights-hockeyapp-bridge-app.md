---
title: "aaaExploring HockeyApp danych w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analizowanie użycia i wydajności aplikacji platformy Azure za pomocą usługi Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="a24a7-103">Eksplorowanie danych HockeyApp w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="a24a7-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="a24a7-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello zaleca platformy monitorowania na żywo wersje desktop i mobile apps.</span><span class="sxs-lookup"><span data-stu-id="a24a7-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="a24a7-105">Z HockeyApp można wysyłać niestandardowych i śledzenia użycia toomonitor telemetrii i ułatwić diagnostyki (w dane awarii toogetting dodanie).</span><span class="sxs-lookup"><span data-stu-id="a24a7-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="a24a7-106">Ten strumień danych telemetrycznych może być badana zaawansowanym hello [Analytics](app-insights-analytics.md) funkcji [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a24a7-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a24a7-107">Ponadto można [wyeksportować hello niestandardowych i dane telemetryczne śledzenia](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="a24a7-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="a24a7-108">tooenable funkcji, należy skonfigurować mostek przekazuje HockeyApp danych niestandardowych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="a24a7-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="a24a7-109">Witaj Mostek HockeyApp aplikacji</span><span class="sxs-lookup"><span data-stu-id="a24a7-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="a24a7-110">HockeyApp Mostek aplikacji Hello jest hello core funkcja umożliwiająca tooaccess HockeyApp niestandardowej, a dane telemetryczne śledzenia w usłudze Application Insights za pośrednictwem hello Analytics i funkcji eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="a24a7-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="a24a7-111">Niestandardowy i śledzenia zebranych zdarzeń wg HockeyApp po utworzeniu hello hello HockeyApp Mostek aplikacji będzie dostępny z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="a24a7-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="a24a7-112">Zobaczmy, jak tooset jednego z tych aplikacji mostek.</span><span class="sxs-lookup"><span data-stu-id="a24a7-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="a24a7-113">Otwórz ustawienia konta aplikacji HockeyApp, [tokeny interfejsu API](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="a24a7-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="a24a7-114">Utwórz nowy token, albo ponownie użyć już istniejącego.</span><span class="sxs-lookup"><span data-stu-id="a24a7-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="a24a7-115">Hello minimalne uprawnienia wymagane są tylko do odczytu"".</span><span class="sxs-lookup"><span data-stu-id="a24a7-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="a24a7-116">Zająć tokenu kopię hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a24a7-116">Take a copy of hello API token.</span></span>

![Pobierz token HockeyApp API](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="a24a7-118">Otwórz hello portalu Microsoft Azure i [utworzyć zasobu usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a24a7-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="a24a7-119">Ustaw typ aplikacji zbyt "Aplikacji HockeyApp Mostek":</span><span class="sxs-lookup"><span data-stu-id="a24a7-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Nowy zasób usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="a24a7-121">Nie ma potrzeby tooset nazwę — spowoduje to ustawienie automatycznie na podstawie nazwy HockeyApp hello.</span><span class="sxs-lookup"><span data-stu-id="a24a7-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="a24a7-122">Witaj HockeyApp Mostek pola są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="a24a7-122">hello HockeyApp bridge fields appear.</span></span> 

![Wprowadź pola Mostek](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="a24a7-124">Wprowadź token HockeyApp hello, zanotowaną wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a24a7-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="a24a7-125">Ta akcja powoduje wypełnienie menu rozwijanym "HockeyApp aplikację" hello z wszystkich aplikacji HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="a24a7-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="a24a7-126">Wybierz hello, co ma toouse i pozostałej pełną hello hello pól.</span><span class="sxs-lookup"><span data-stu-id="a24a7-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="a24a7-127">Otwórz hello nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="a24a7-127">Open hello new resource.</span></span> 

<span data-ttu-id="a24a7-128">Należy pamiętać, że hello danych zajmie trochę czasu toostart przepływu.</span><span class="sxs-lookup"><span data-stu-id="a24a7-128">Note that hello data takes a while toostart flowing.</span></span>

![Oczekiwanie na dane zasobu usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="a24a7-130">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="a24a7-130">That’s it!</span></span> <span data-ttu-id="a24a7-131">Niestandardowy i śledzenia zbieranych danych w aplikacji zinstrumentowane HockeyApp od tego momentu jest teraz również dostępne tooyou w hello Analytics i funkcji eksportu ciągłego usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a24a7-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="a24a7-132">Załóżmy krótko Przejrzyj wszystkie te funkcje tooyou teraz dostępne.</span><span class="sxs-lookup"><span data-stu-id="a24a7-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="a24a7-133">Analiza</span><span class="sxs-lookup"><span data-stu-id="a24a7-133">Analytics</span></span>
<span data-ttu-id="a24a7-134">Analiza jest zaawansowanym narzędziem do ad hoc wykonywania kwerend danych, dzięki czemu toodiagnose i analizowania telemetrii i szybko odnaleźć główne przyczyny i wzorce.</span><span class="sxs-lookup"><span data-stu-id="a24a7-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analiza](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="a24a7-136">Dowiedz się więcej o analityka</span><span class="sxs-lookup"><span data-stu-id="a24a7-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="a24a7-137">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="a24a7-137">Continuous export</span></span>
<span data-ttu-id="a24a7-138">Eksport ciągły umożliwia tooexport danych do kontenera magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a24a7-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="a24a7-139">Jest to bardzo przydatne, jeśli potrzebujesz tookeep danych przez czas dłuższy niż okres przechowywania hello obecnie oferowanych przez usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a24a7-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="a24a7-140">Możesz hello dane są przechowywane w magazynie obiektów blob, przetworzyć go do bazy danych SQL lub preferowany rozwiązań magazynowania danych.</span><span class="sxs-lookup"><span data-stu-id="a24a7-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="a24a7-141">Dowiedz się więcej o eksportu ciągłego</span><span class="sxs-lookup"><span data-stu-id="a24a7-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="a24a7-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a24a7-142">Next steps</span></span>
* [<span data-ttu-id="a24a7-143">Zastosuj dane analityczne tooyour</span><span class="sxs-lookup"><span data-stu-id="a24a7-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

