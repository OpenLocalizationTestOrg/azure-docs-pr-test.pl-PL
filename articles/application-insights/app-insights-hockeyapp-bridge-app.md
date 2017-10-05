---
title: "Eksplorowanie danych HockeyApp w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="b49f2-103">Eksplorowanie danych HockeyApp w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="b49f2-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="b49f2-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) jest zalecane platformą monitorowania na żywo wersje desktop i mobile apps.</span><span class="sxs-lookup"><span data-stu-id="b49f2-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="b49f2-105">Z HockeyApp można wysyłać niestandardowych i śledzenia danych telemetrycznych do monitorowania użycia i ułatwić diagnozowanie (oprócz pobierania danych awarii).</span><span class="sxs-lookup"><span data-stu-id="b49f2-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="b49f2-106">Ten strumień danych telemetrycznych można zbadać w zaawansowanym [Analytics](app-insights-analytics.md) funkcji [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b49f2-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b49f2-107">Ponadto można [eksportowanie niestandardowego i dane telemetryczne śledzenia](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b49f2-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="b49f2-108">Aby włączyć te funkcje, należy skonfigurować mostek przekazuje HockeyApp niestandardowe dane do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b49f2-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="b49f2-109">Aplikacji HockeyApp Mostek</span><span class="sxs-lookup"><span data-stu-id="b49f2-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="b49f2-110">Aplikacja Mostek HockeyApp jest funkcja core, która umożliwia dostęp do aplikacji HockeyApp niestandardowych i dane telemetryczne śledzenia w usłudze Application Insights przy użyciu funkcji analizy i eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="b49f2-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="b49f2-111">Niestandardowy i śledzenia zebranych zdarzeń wg HockeyApp po utworzeniu aplikacji HockeyApp mostek będzie dostępny z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b49f2-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="b49f2-112">Zobaczmy, jak ustawić jedną z tych aplikacji mostek.</span><span class="sxs-lookup"><span data-stu-id="b49f2-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="b49f2-113">Otwórz ustawienia konta aplikacji HockeyApp, [tokeny interfejsu API](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="b49f2-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="b49f2-114">Utwórz nowy token, albo ponownie użyć już istniejącego.</span><span class="sxs-lookup"><span data-stu-id="b49f2-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="b49f2-115">Minimalne uprawnienia wymagane są tylko do odczytu"".</span><span class="sxs-lookup"><span data-stu-id="b49f2-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="b49f2-116">Kopiowanie interfejsu API zająć tokenu.</span><span class="sxs-lookup"><span data-stu-id="b49f2-116">Take a copy of the API token.</span></span>

![Pobierz token HockeyApp API](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="b49f2-118">Otwórz portal Microsoft Azure i [utworzyć zasobu usługi Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b49f2-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="b49f2-119">Ustaw typ aplikacji "Platforma HockeyApp Mostek aplikacji":</span><span class="sxs-lookup"><span data-stu-id="b49f2-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![Nowy zasób usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="b49f2-121">Nie należy ustawić nazwę — spowoduje to ustawienie automatycznie na podstawie nazwy aplikacji HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="b49f2-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="b49f2-122">Pola Mostek HockeyApp są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="b49f2-122">The HockeyApp bridge fields appear.</span></span> 

![Wprowadź pola Mostek](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="b49f2-124">Wprowadź token HockeyApp zanotowaną wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b49f2-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="b49f2-125">Ta akcja powoduje wypełnienie menu rozwijanym "Aplikacji HockeyApp" z wszystkich aplikacji HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="b49f2-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="b49f2-126">Wybierz ten, który ma być używany, a następnie ukończ pozostałe pola.</span><span class="sxs-lookup"><span data-stu-id="b49f2-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="b49f2-127">Otwórz nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="b49f2-127">Open the new resource.</span></span> 

<span data-ttu-id="b49f2-128">Należy pamiętać, że dane zajmuje trochę czasu, aby uruchomić przepływy.</span><span class="sxs-lookup"><span data-stu-id="b49f2-128">Note that the data takes a while to start flowing.</span></span>

![Oczekiwanie na dane zasobu usługi Application Insights](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="b49f2-130">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="b49f2-130">That’s it!</span></span> <span data-ttu-id="b49f2-131">Niestandardowy i śledzenia zbieranych danych w aplikacji zinstrumentowane HockeyApp od tego momentu teraz jest również dostępny w funkcji analizy i eksportu ciągłego usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b49f2-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="b49f2-132">Załóżmy krótko przejrzyj każdą z tych funkcji, które są teraz dostępne dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b49f2-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="b49f2-133">Analiza</span><span class="sxs-lookup"><span data-stu-id="b49f2-133">Analytics</span></span>
<span data-ttu-id="b49f2-134">Analytics to narzędzie zaawansowanych zapytań ad hoc danych, co umożliwia diagnozowanie i analizowania telemetrii i szybko odnaleźć główne przyczyny i wzorce.</span><span class="sxs-lookup"><span data-stu-id="b49f2-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analiza](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="b49f2-136">Dowiedz się więcej o analityka</span><span class="sxs-lookup"><span data-stu-id="b49f2-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="b49f2-137">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="b49f2-137">Continuous export</span></span>
<span data-ttu-id="b49f2-138">Eksport ciągły pozwala na wyeksportowanie danych do kontenera magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b49f2-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="b49f2-139">Jest to bardzo przydatne, jeśli chcesz zachować dane przez czas dłuższy niż okres przechowywania obecnie oferowanych przez usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b49f2-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="b49f2-140">Można przechowywać dane w magazynie obiektów blob, przetworzyć go do bazy danych SQL lub preferowany rozwiązań magazynowania danych.</span><span class="sxs-lookup"><span data-stu-id="b49f2-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="b49f2-141">Dowiedz się więcej o eksportu ciągłego</span><span class="sxs-lookup"><span data-stu-id="b49f2-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="b49f2-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b49f2-142">Next steps</span></span>
* [<span data-ttu-id="b49f2-143">Stosowanie Analytics do danych</span><span class="sxs-lookup"><span data-stu-id="b49f2-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)

