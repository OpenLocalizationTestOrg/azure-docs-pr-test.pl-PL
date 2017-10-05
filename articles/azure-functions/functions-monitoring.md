---
title: "Monitorowanie usługę Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorować funkcji platformy Azure."
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="b6180-104">Monitorowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b6180-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="b6180-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b6180-105">Overview</span></span> 


<span data-ttu-id="b6180-106">**Monitor** karcie dla każdej funkcji umożliwia przeglądanie wykonanie każdej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b6180-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Karta monitor funkcje platformy Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="b6180-108">Kliknięcie przycisku wykonywania umożliwia przeglądanie czas trwania, danych wejściowych, błędy i skojarzone pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="b6180-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="b6180-109">Jest to przydatne debugowania i dostrajania funkcji wydajności.</span><span class="sxs-lookup"><span data-stu-id="b6180-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="b6180-110">Korzystając z [zużycie plan hostingu](functions-overview.md#pricing) dla usługi Azure Functions **monitorowanie** kafelka w bloku Przegląd funkcji aplikacji nie wyświetli żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="b6180-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="b6180-111">Jest to spowodowane platformę dynamicznie skaluje i zarządza wystąpienia obliczeniowe, więc te metryki nie są przydatne w planie zużycia.</span><span class="sxs-lookup"><span data-stu-id="b6180-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="b6180-112">Do monitorowania użycia aplikacji funkcji, należy zamiast tego użyj wskazówek w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b6180-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="b6180-113">Poniższy zrzut ekranu przedstawia przykład:</span><span class="sxs-lookup"><span data-stu-id="b6180-113">The following screen-shot shows an example:</span></span>
> 
> ![Monitorowanie w bloku zasobów głównego](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="b6180-115">Monitorowanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="b6180-115">Real-time monitoring</span></span>

<span data-ttu-id="b6180-116">Monitorowanie w czasie rzeczywistym będą dostępne po kliknięciu **strumień na żywo zdarzeń** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b6180-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opcja strumień wydarzenia na żywo na karcie monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="b6180-118">Strumień na żywo zdarzeń zostaną wyświetlone na wykresie na nowej karcie przeglądarki w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="b6180-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Przykład strumienia wydarzenia na żywo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="b6180-120">Jest to znany problem, który może powodować danych nie można wypełnić.</span><span class="sxs-lookup"><span data-stu-id="b6180-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="b6180-121">Jeśli wystąpią, konieczne może być zamknąć kartę przeglądarki zawierająca strumień wydarzenia na żywo, a następnie kliknij przycisk **strumień na żywo zdarzeń** ponownie, aby zezwalała na poprawnie wypełnić danych strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b6180-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="b6180-122">Strumień na żywo zdarzeń będzie wykres następujące statystyki dla funkcji:</span><span class="sxs-lookup"><span data-stu-id="b6180-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="b6180-123">Wykonaniami uruchomione na sekundę</span><span class="sxs-lookup"><span data-stu-id="b6180-123">Executions started per second</span></span>
* <span data-ttu-id="b6180-124">Wykonaniami wykonywanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="b6180-124">Executions completed per second</span></span>
* <span data-ttu-id="b6180-125">Wykonaniami zakończone niepowodzeniami na sekundę</span><span class="sxs-lookup"><span data-stu-id="b6180-125">Executions failed per second</span></span>
* <span data-ttu-id="b6180-126">Średni czas wykonania (w milisekundach).</span><span class="sxs-lookup"><span data-stu-id="b6180-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="b6180-127">Te statystyki są w czasie rzeczywistym, ale rzeczywisty Tworzenie wykresów danych wykonawczych mogą mieć około 10 sekund opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="b6180-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="b6180-128">Monitorowanie plików dziennika z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b6180-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="b6180-129">Można przesłać strumieniowo pliki dziennika do sesji wiersza polecenia na lokalnej stacji roboczej za pomocą usługi Azure interfejsu wiersza polecenia (CLI) lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6180-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="b6180-130">Pliki dziennika aplikacji funkcji monitorowania z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b6180-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="b6180-131">Aby rozpocząć, [zainstaluj interfejs wiersza polecenia platformy Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="b6180-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="b6180-132">Zaloguj się do konta platformy Azure przy użyciu następującego polecenia lub inne opcje objęte, [logowanie do platformy Azure z wiersza polecenia platformy Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b6180-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="b6180-133">Użyj następującego polecenia, aby włączyć tryb Azure CLI usługi zarządzania (ASM):.</span><span class="sxs-lookup"><span data-stu-id="b6180-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="b6180-134">Jeśli masz wiele subskrypcji, użyj następujących poleceń listy subskrypcji i ustawić bieżącej subskrypcji na subskrypcję, która zawiera aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="b6180-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="b6180-135">Polecenie będą przesyłane strumieniowo pliki dziennika aplikacji funkcji w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="b6180-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="b6180-136">Pliki dziennika aplikacji funkcji monitorowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6180-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="b6180-137">Aby rozpocząć, [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6180-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b6180-138">Dodaj konto platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b6180-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="b6180-139">Jeśli masz wiele subskrypcji, możesz podać je według nazwy przy użyciu następującego polecenia, aby sprawdzić, czy prawidłowa subskrypcja jest aktualnie wybrany na podstawie `IsCurrent` właściwości:</span><span class="sxs-lookup"><span data-stu-id="b6180-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="b6180-140">Jeśli musisz ustawić aktywną subskrypcją dysk zawierający aplikację funkcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b6180-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="b6180-141">Strumienia dzienników do sesji programu PowerShell przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b6180-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="b6180-142">Więcej informacji można znaleźć w [porady: strumienia dzienników aplikacji sieci web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="b6180-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b6180-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6180-143">Next steps</span></span>
<span data-ttu-id="b6180-144">Więcej informacji zawierają następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="b6180-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="b6180-145">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="b6180-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="b6180-146">Skalowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="b6180-146">Scale a function</span></span>](functions-scale.md)

