---
title: "aaaMonitor i zarządzanie nimi zadania usługi analiza strumienia przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toomonitor programu Azure PowerShell i polecenia cmdlet zadania usługi analiza strumienia i zarządzać nimi."
keywords: "Program Azure powershell, poleceń cmdlet programu azure powershell, polecenia programu powershell skryptów środowiska powershell"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="42e64-104">Monitorowanie i zarządzanie nimi zadania usługi analiza strumienia za pomocą poleceń cmdlet programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="42e64-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="42e64-105">Dowiedz się, jak toomonitor i zarządzanie zasobami usługi Stream Analytics za pomocą poleceń cmdlet programu Azure PowerShell i skryptów programu powershell, które wykonywać podstawowe zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="42e64-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="42e64-106">Wymagania wstępne dotyczące uruchamiania poleceń cmdlet programu Azure PowerShell dla usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="42e64-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="42e64-107">Utwórz grupy zasobów platformy Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="42e64-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="42e64-108">Witaj poniżej znajduje się przykładowy skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="42e64-109">Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="42e64-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="42e64-110">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="42e64-111">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="42e64-112">Zadania usługi analiza strumienia utworzone programowo monitorowania, domyślnie nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="42e64-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="42e64-113">Można ręcznie włączyć monitorowanie hello portalu Azure, przechodząc na stronę Monitor toohello zadania i kliknięcie przycisku Włącz hello, lub możesz to zrobić programowo, wykonując kroki hello znajdujący się w [Azure Stream Analytics — Monitor strumienia Analiza zadania programowo](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="42e64-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="42e64-114">Azure poleceń cmdlet programu PowerShell dla usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="42e64-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="42e64-115">Hello następującego polecenia cmdlet programu Azure PowerShell można toomonitor używane i zarządzanie zadania usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="42e64-116">Należy pamiętać, że programu Azure PowerShell ma różne wersje.</span><span class="sxs-lookup"><span data-stu-id="42e64-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="42e64-117">**W przykładach hello pierwsze polecenie wymienionych hello jest przeznaczony dla programu Azure PowerShell 0.9.8 hello drugie polecenie jest Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="42e64-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="42e64-118">polecenia Hello Azure PowerShell 1.0 zawsze będą mieć "AzureRM" hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="42e64-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="42e64-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="42e64-120">Wyświetla listę wszystkich zadań usługi Stream Analytics zdefiniowanej w hello subskrypcji platformy Azure lub określonej grupy zasobów lub pobiera informacje o zadaniu o konkretnym zadaniu w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="42e64-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="42e64-121">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-121">**Example 1**</span></span>

<span data-ttu-id="42e64-122">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="42e64-123">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="42e64-124">To polecenie programu PowerShell zwraca informacje o wszystkich zadań usługi Stream Analytics hello w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="42e64-125">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-125">**Example 2**</span></span>

<span data-ttu-id="42e64-126">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="42e64-127">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="42e64-128">To polecenie programu PowerShell zwraca informacje o wszystkich zadań usługi Stream Analytics hello w grupie zasobów hello StreamAnalytics domyślne-centralnego-US.</span><span class="sxs-lookup"><span data-stu-id="42e64-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="42e64-129">**Przykład 3**</span><span class="sxs-lookup"><span data-stu-id="42e64-129">**Example 3**</span></span>

<span data-ttu-id="42e64-130">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="42e64-131">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="42e64-132">To polecenie programu PowerShell zwraca informacje o zadaniu Stream Analytics hello StreamingJob w grupie zasobów hello StreamAnalytics domyślne-centralnego-US.</span><span class="sxs-lookup"><span data-stu-id="42e64-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="42e64-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="42e64-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="42e64-134">Wyświetla listę wszystkich danych wejściowych hello, które są zdefiniowane w określonym zadaniu Stream Analytics lub pobiera informacje o określone dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="42e64-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="42e64-135">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-135">**Example 1**</span></span>

<span data-ttu-id="42e64-136">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="42e64-137">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="42e64-138">To polecenie programu PowerShell zwraca informacje o wszystkich zdefiniowanych w zadaniu hello StreamingJob danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="42e64-139">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-139">**Example 2**</span></span>

<span data-ttu-id="42e64-140">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="42e64-141">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="42e64-142">To polecenie programu PowerShell zwraca informacje o hello danych wejściowych o nazwie EntryStream zdefiniowane w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="42e64-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="42e64-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="42e64-144">Wyświetla listę wszystkich hello dane wyjściowe, które są zdefiniowane w określonym zadaniu Stream Analytics lub pobiera informacje o określonych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="42e64-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="42e64-145">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-145">**Example 1**</span></span>

<span data-ttu-id="42e64-146">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="42e64-147">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="42e64-148">To polecenie programu PowerShell zwraca informacje o danych wyjściowych hello zdefiniowane w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="42e64-149">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-149">**Example 2**</span></span>

<span data-ttu-id="42e64-150">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="42e64-151">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="42e64-152">To polecenie programu PowerShell zwraca informacje o danych wyjściowych hello o nazwie zdefiniowane w zadaniu hello StreamingJob danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="42e64-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="42e64-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="42e64-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="42e64-154">Pobiera informacje o przydziału hello przesyłania strumieniowego jednostki w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="42e64-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="42e64-155">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-155">**Example 1**</span></span>

<span data-ttu-id="42e64-156">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="42e64-157">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="42e64-158">Tego polecenia programu PowerShell zwraca informacje o hello przydziału i użycia jednostek przesyłania strumieniowego w regionie środkowe stany USA hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="42e64-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="42e64-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="42e64-160">Pobiera informacje o określonych przekształcenia zdefiniowane w zadaniu Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="42e64-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="42e64-161">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-161">**Example 1**</span></span>

<span data-ttu-id="42e64-162">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="42e64-163">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="42e64-164">To polecenie programu PowerShell zwraca informacje o transformacji hello o nazwie StreamingJob w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="42e64-165">Nowe AzureStreamAnalyticsInput | Nowe AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="42e64-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="42e64-166">Tworzy nowe dane wejściowe w zadaniu Stream Analytics, lub aktualizuje istniejące określone dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="42e64-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="42e64-167">Witaj danych wejściowych hello można określić w pliku JSON hello lub hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="42e64-168">Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="42e64-169">Jeśli Określ dane wejściowe, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="42e64-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="42e64-170">Jeśli określisz hello — parametru Force i określ istniejącą wprowadź nazwę, wprowadzania hello zostaną zastąpione bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="42e64-171">Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [Tworzenie danych wejściowych (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] sekcji hello [interfejs API REST zarządzania usługi analiza strumienia Odwołanie do biblioteki][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="42e64-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="42e64-172">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-172">**Example 1**</span></span>

<span data-ttu-id="42e64-173">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="42e64-174">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="42e64-175">To polecenie programu PowerShell tworzy nowe dane wejściowe z hello pliku Input.json.</span><span class="sxs-lookup"><span data-stu-id="42e64-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="42e64-176">Jeśli istniejące dane wejściowe o nazwie hello określony w pliku definicji wejściowych hello jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.</span><span class="sxs-lookup"><span data-stu-id="42e64-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="42e64-177">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-177">**Example 2**</span></span>

<span data-ttu-id="42e64-178">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="42e64-179">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="42e64-180">To polecenie programu PowerShell tworzy nowe dane wejściowe w zadaniu hello o nazwie EntryStream.</span><span class="sxs-lookup"><span data-stu-id="42e64-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="42e64-181">Jeśli istniejące dane wejściowe o tej nazwie jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.</span><span class="sxs-lookup"><span data-stu-id="42e64-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="42e64-182">**Przykład 3**</span><span class="sxs-lookup"><span data-stu-id="42e64-182">**Example 3**</span></span>

<span data-ttu-id="42e64-183">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="42e64-184">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="42e64-185">To polecenie programu PowerShell zastępuje definicji hello hello istniejącego źródła danych wejściowych o nazwie EntryStream z hello definicję z pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="42e64-186">Nowe AzureStreamAnalyticsJob | Nowe AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="42e64-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="42e64-187">Tworzy nowe zadanie usługi analiza strumienia w Microsoft Azure lub aktualizacji definicji hello istniejących określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="42e64-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="42e64-188">Witaj hello zadania można określić w pliku JSON hello lub hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="42e64-189">Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="42e64-190">Jeśli Określ nazwę zadania, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejącego zadania.</span><span class="sxs-lookup"><span data-stu-id="42e64-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="42e64-191">Jeśli określisz hello — parametru Force, a następnie określ nazwę istniejącego zadania, hello definicji zadania zostaną zastąpione bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="42e64-192">Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [utworzyć zadania usługi analiza strumienia] [ msdn-rest-api-create-stream-analytics-job] sekcji hello [dokumentacja interfejsu API REST zarządzania usługi analiza strumienia Biblioteka][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="42e64-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="42e64-193">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-193">**Example 1**</span></span>

<span data-ttu-id="42e64-194">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="42e64-195">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="42e64-196">To polecenie programu PowerShell tworzy nowe zadanie z definicji hello w JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="42e64-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="42e64-197">Jeśli istniejące zadanie o nazwie hello określony w pliku definicji zadania hello jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.</span><span class="sxs-lookup"><span data-stu-id="42e64-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="42e64-198">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-198">**Example 2**</span></span>

<span data-ttu-id="42e64-199">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="42e64-200">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="42e64-201">To polecenie programu PowerShell zastępuje hello definicji zadania dla StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="42e64-202">Nowe AzureStreamAnalyticsOutput | Nowe AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="42e64-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="42e64-203">Tworzy nowe dane wyjściowe w zadaniu Stream Analytics, lub aktualizuje istniejące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="42e64-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="42e64-204">Witaj hello danych wyjściowych można określić w pliku JSON hello lub hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="42e64-205">Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="42e64-206">Jeśli Określ wyjścia, który już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="42e64-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="42e64-207">Jeśli określisz hello — parametru Force i określ istniejącą output nazwy, hello dane wyjściowe zostaną zastąpione bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="42e64-208">Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [Tworzenie danych wyjściowych (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] sekcji hello [interfejs API REST zarządzania usługi analiza strumienia Odwołanie do biblioteki][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="42e64-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="42e64-209">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-209">**Example 1**</span></span>

<span data-ttu-id="42e64-210">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="42e64-211">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="42e64-212">To polecenie programu PowerShell tworzy nowe dane wyjściowe w zadaniu hello StreamingJob o nazwie "wyjściowej".</span><span class="sxs-lookup"><span data-stu-id="42e64-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="42e64-213">Jeśli istniejące dane wyjściowe o tej nazwie jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.</span><span class="sxs-lookup"><span data-stu-id="42e64-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="42e64-214">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-214">**Example 2**</span></span>

<span data-ttu-id="42e64-215">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="42e64-216">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="42e64-217">To polecenie programu PowerShell zastępuje hello definicji do "wyjściowej" w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="42e64-218">Nowe AzureStreamAnalyticsTransformation | Nowe AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="42e64-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="42e64-219">Tworzy nowy transformacji w zadaniu Stream Analytics lub aktualizuje hello istniejących transformacji.</span><span class="sxs-lookup"><span data-stu-id="42e64-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="42e64-220">Witaj transformacji hello można określić w pliku JSON hello lub hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="42e64-221">Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="42e64-222">Jeśli Określ transformację, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących transformacji.</span><span class="sxs-lookup"><span data-stu-id="42e64-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="42e64-223">Jeśli określisz hello — parametru Force i określ istniejącą nazwę przekształcania, przekształcania hello zostaną zastąpione bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="42e64-224">Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [utworzyć transformacji (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] sekcji hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="42e64-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="42e64-225">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-225">**Example 1**</span></span>

<span data-ttu-id="42e64-226">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="42e64-227">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="42e64-228">To polecenie programu PowerShell tworzy nowy przekształcenia o nazwie StreamingJobTransform w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="42e64-229">Jeśli istniejące transformacji jest już zdefiniowany o tej nazwie, polecenia cmdlet hello zapyta, czy tooreplace go.</span><span class="sxs-lookup"><span data-stu-id="42e64-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="42e64-230">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="42e64-230">**Example 2**</span></span>

<span data-ttu-id="42e64-231">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="42e64-232">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="42e64-233">To polecenie programu PowerShell zastępuje hello definicji StreamingJobTransform w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="42e64-234">Usuń AzureStreamAnalyticsInput | Usuń AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="42e64-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="42e64-235">Asynchronicznie usuwa określone dane wejściowe z zadania usługi analiza strumienia w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="42e64-236">Jeśli określisz hello — parametru Force, hello danych wejściowych zostaną usunięte bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="42e64-237">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-237">**Example 1**</span></span>

<span data-ttu-id="42e64-238">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="42e64-239">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="42e64-240">Tego polecenia programu PowerShell, usuwa hello wejściowych EventStream w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="42e64-241">Usuń AzureStreamAnalyticsJob | Usuń AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="42e64-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="42e64-242">Asynchronicznie usuwa określonego zadania usługi analiza strumienia w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="42e64-243">Jeśli określisz hello — parametru Force, hello zadania zostaną usunięte bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="42e64-244">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-244">**Example 1**</span></span>

<span data-ttu-id="42e64-245">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="42e64-246">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="42e64-247">To polecenie programu PowerShell usuwa zadanie hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="42e64-248">Usuń AzureStreamAnalyticsOutput | Usuń AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="42e64-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="42e64-249">Asynchronicznie usuwa określone dane wyjściowe z zadania usługi analiza strumienia w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="42e64-250">Jeśli określisz hello — parametru Force, hello dane wyjściowe będą usunięte bez potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="42e64-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="42e64-251">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-251">**Example 1**</span></span>

<span data-ttu-id="42e64-252">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="42e64-253">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="42e64-254">Dane wyjściowe dane wyjściowe tego hello usuwa polecenia programu PowerShell w zadaniu hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="42e64-255">Start AzureStreamAnalyticsJob | Start AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="42e64-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="42e64-256">Asynchronicznie wdraża i uruchamia zadanie usługi analiza strumienia w Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42e64-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="42e64-257">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-257">**Example 1**</span></span>

<span data-ttu-id="42e64-258">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="42e64-259">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="42e64-260">To polecenie programu PowerShell uruchamia hello zadania StreamingJob danych wyjściowych niestandardowego czas rozpoczęcia ustawić tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="42e64-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="42e64-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="42e64-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="42e64-262">Asynchronicznie Zatrzymuje zadanie usługi analiza strumienia, w programie Microsoft Azure i zwalnia zasoby, które były, które były używane.</span><span class="sxs-lookup"><span data-stu-id="42e64-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="42e64-263">Witaj definicji zadania i metadanych pozostaną dostępne w ramach subskrypcji za pośrednictwem hello portalu Azure i zarządzanie interfejsów API, tak, aby hello zadania mogą edytować i ponownie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="42e64-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="42e64-264">Nie zostanie obciążona dla zadania w stanie hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="42e64-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="42e64-265">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-265">**Example 1**</span></span>

<span data-ttu-id="42e64-266">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="42e64-267">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="42e64-268">To polecenie programu PowerShell Zatrzymuje zadanie hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="42e64-269">Test AzureStreamAnalyticsInput | AzureRMStreamAnalyticsInput testu</span><span class="sxs-lookup"><span data-stu-id="42e64-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="42e64-270">Zdolność hello testy tooa tooconnect Stream Analytics określone dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="42e64-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="42e64-271">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-271">**Example 1**</span></span>

<span data-ttu-id="42e64-272">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="42e64-273">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="42e64-274">Tego programu PowerShell polecenie testy hello status połączenia hello wejściowych EntryStream w StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="42e64-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="42e64-275">Test AzureStreamAnalyticsOutput | AzureRMStreamAnalyticsOutput testu</span><span class="sxs-lookup"><span data-stu-id="42e64-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="42e64-276">Zdolność hello testy tooa tooconnect Stream Analytics określone dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="42e64-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="42e64-277">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="42e64-277">**Example 1**</span></span>

<span data-ttu-id="42e64-278">Program Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="42e64-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="42e64-279">Program Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="42e64-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="42e64-280">Dane wyjściowe w StreamingJob dane wyjściowe tego środowiska PowerShell polecenie testy hello status połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="42e64-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="42e64-281">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="42e64-281">Get support</span></span>
<span data-ttu-id="42e64-282">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="42e64-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="42e64-283">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42e64-283">Next steps</span></span>
* [<span data-ttu-id="42e64-284">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="42e64-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="42e64-285">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="42e64-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="42e64-286">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="42e64-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="42e64-287">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="42e64-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="42e64-288">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="42e64-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

