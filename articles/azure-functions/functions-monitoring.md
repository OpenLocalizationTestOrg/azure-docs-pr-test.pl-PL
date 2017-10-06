---
title: "aaaMonitoring usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor funkcji platformy Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="d717e-104">Monitorowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d717e-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="d717e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d717e-105">Overview</span></span> 


<span data-ttu-id="d717e-106">Witaj **Monitor** karcie dla każdej funkcji umożliwia tooreview wykonanie każdej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d717e-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Karta monitor funkcje platformy Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="d717e-108">Kliknięcie wykonywania umożliwia możesz tooreview hello duration, danych wejściowych, błędy i skojarzone pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="d717e-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="d717e-109">Jest to przydatne debugowania i dostrajania funkcji wydajności.</span><span class="sxs-lookup"><span data-stu-id="d717e-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="d717e-110">Korzystając z hello [zużycie plan hostingu](functions-overview.md#pricing) dla usługi Azure Functions hello **monitorowanie** kafelka w bloku Przegląd funkcji aplikacji hello nie wyświetli żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="d717e-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="d717e-111">Jest to spowodowane platformy hello dynamicznie skaluje i zarządza wystąpienia obliczeniowe, więc te metryki nie są przydatne w planie zużycia.</span><span class="sxs-lookup"><span data-stu-id="d717e-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="d717e-112">Użycie hello toomonitor aplikacji funkcji, wskazówki hello należy zamiast tego użyć w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d717e-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="d717e-113">powitania po zrzut ekranu przedstawia przykład:</span><span class="sxs-lookup"><span data-stu-id="d717e-113">hello following screen-shot shows an example:</span></span>
> 
> ![Monitorowanie na powitania bloku zasobów głównego](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="d717e-115">Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d717e-115">Real-time monitoring</span></span>

<span data-ttu-id="d717e-116">Monitorowanie w czasie rzeczywistym będą dostępne po kliknięciu **strumień na żywo zdarzeń** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="d717e-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opcja strumienia zdarzeń na karcie monitorowanie hello na żywo](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="d717e-118">strumień na żywo zdarzeń Hello zostaną wyświetlone na wykresie na nowej karcie przeglądarki w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="d717e-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Przykład strumienia wydarzenia na żywo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="d717e-120">Jest to znany problem, który może powodować Twojej toobe toofail danych wypełnione.</span><span class="sxs-lookup"><span data-stu-id="d717e-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="d717e-121">Jeśli wystąpią, może być konieczne tooclose hello przeglądarki kartę zawierającego hello na żywo strumienia zdarzeń, a następnie kliknij przycisk **strumień na żywo zdarzeń** tooallow ponownie go tooproperly wypełnić danych strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d717e-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="d717e-122">strumień na żywo zdarzeń Hello będzie wykres hello następujące statystyki dla funkcji:</span><span class="sxs-lookup"><span data-stu-id="d717e-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="d717e-123">Wykonaniami uruchomione na sekundę</span><span class="sxs-lookup"><span data-stu-id="d717e-123">Executions started per second</span></span>
* <span data-ttu-id="d717e-124">Wykonaniami wykonywanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="d717e-124">Executions completed per second</span></span>
* <span data-ttu-id="d717e-125">Wykonaniami zakończone niepowodzeniami na sekundę</span><span class="sxs-lookup"><span data-stu-id="d717e-125">Executions failed per second</span></span>
* <span data-ttu-id="d717e-126">Średni czas wykonania (w milisekundach).</span><span class="sxs-lookup"><span data-stu-id="d717e-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="d717e-127">Te statystyki są w czasie rzeczywistym, ale hello rzeczywiste Tworzenie wykresów hello wykonywania danych mogą mieć około 10 sekund opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="d717e-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="d717e-128">Monitorowanie plików dziennika z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d717e-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="d717e-129">Można przesłać strumieniowo sesji wiersza polecenia tooa pliki dziennika na lokalnej stacji roboczej za pomocą hello Azure interfejsu wiersza polecenia (CLI) lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d717e-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="d717e-130">Pliki dziennika aplikacji funkcji monitorowania z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d717e-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="d717e-131">tooget pracę, [zainstalować hello wiersza polecenia platformy Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="d717e-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="d717e-132">Zaloguj się do konta platformy Azure przy użyciu następujących hello polecenia ani żadnych innych opcji, których dotyczy, hello [Zaloguj tooAzure z hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d717e-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="d717e-133">Użyj hello następujące polecenie trybie Azure CLI usługi zarządzania (ASM) tooenable:.</span><span class="sxs-lookup"><span data-stu-id="d717e-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="d717e-134">Jeśli masz wiele subskrypcji, użyj następującego polecenia toolist hello Twojej subskrypcji i zestaw hello bieżącej subskrypcji toohello subskrypcji, która zawiera aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="d717e-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="d717e-135">Witaj następujące polecenie będą przesyłane strumieniowo pliki dziennika hello linii polecenia toohello aplikacji funkcji:</span><span class="sxs-lookup"><span data-stu-id="d717e-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="d717e-136">Pliki dziennika aplikacji funkcji monitorowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d717e-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="d717e-137">Rozpoczęto, tooget [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d717e-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d717e-138">Dodaj konto platformy Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d717e-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="d717e-139">Jeśli masz wiele subskrypcji, możesz podać je według nazwy z powitania po toosee polecenia hello prawidłowa subskrypcja jest hello aktualnie wybrany na podstawie `IsCurrent` właściwości:</span><span class="sxs-lookup"><span data-stu-id="d717e-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="d717e-140">Tooset hello aktywną subskrypcją toohello zawierający aplikację funkcji, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d717e-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="d717e-141">Strumień hello rejestruje tooyour sesji programu PowerShell z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d717e-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="d717e-142">Aby uzyskać więcej informacji można znaleźć zbyt[porady: strumienia dzienników aplikacji sieci web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="d717e-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d717e-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d717e-143">Next steps</span></span>
<span data-ttu-id="d717e-144">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="d717e-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="d717e-145">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="d717e-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="d717e-146">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="d717e-146">Scale a function</span></span>](functions-scale.md)

