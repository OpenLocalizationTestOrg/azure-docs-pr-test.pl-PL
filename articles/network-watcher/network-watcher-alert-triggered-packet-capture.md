---
title: "aktywne toodo przechwytywania pakietów aaaUse sieci, monitorowanie za pomocą alertów i usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate alert wyzwolony przechwytywania pakietów z obserwatora sieciowego Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="0321e-103">Użyj przechwytywania pakietów dla sieci aktywnego monitorowania za pomocą alertów i usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0321e-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="0321e-104">Przechwytywania pakietów obserwatora sieciowego tworzy sesji przechwytywania tootrack ruch do i z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0321e-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="0321e-105">Witaj pliku przechwytywania może mieć zdefiniowany filtr tootrack hello tylko ruchu, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0321e-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="0321e-106">Dane te są następnie przechowywane w obiekcie blob magazynu lub lokalnie na maszynie gościa hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="0321e-107">Ta funkcja może być uruchomiona zdalnie na inne scenariusze automatyzacji, takich jak usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0321e-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="0321e-108">Zapewnia przechwytywania pakietów hello możliwości toorun aktywnego przechwytywania na podstawie zdefiniowanych anomalii sieci.</span><span class="sxs-lookup"><span data-stu-id="0321e-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="0321e-109">Innych celów obejmują zbieranie statystyk sieciowych, pobieranie informacji na temat sieci atakami, debugowania komunikacja klient serwer i inne.</span><span class="sxs-lookup"><span data-stu-id="0321e-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="0321e-110">Zasoby, które są wdrażane na platformie Azure Uruchom 24/7.</span><span class="sxs-lookup"><span data-stu-id="0321e-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="0321e-111">Możesz i pracownicy działu aktywnie nie można monitorować stan hello wszystkich zasobów 24/7.</span><span class="sxs-lookup"><span data-stu-id="0321e-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="0321e-112">Na przykład co się stanie, jeśli wystąpi problem w 2 AM?</span><span class="sxs-lookup"><span data-stu-id="0321e-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="0321e-113">Dzięki użyciu obserwatora sieciowego, alerty i funkcji w ramach hello ekosystemu platformy Azure aktywne mogą odpowiadać hello danych i narzędzia toosolve problemów w sieci.</span><span class="sxs-lookup"><span data-stu-id="0321e-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Scenariusz][scenario]

## <a name="prerequisites"></a><span data-ttu-id="0321e-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0321e-115">Prerequisites</span></span>

* <span data-ttu-id="0321e-116">Witaj najnowszą wersję [programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0321e-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="0321e-117">Istniejące wystąpienie obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="0321e-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="0321e-118">Jeśli nie masz już konto, [utworzyć wystąpienia obserwatora sieciowego](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="0321e-119">Istniejącej maszyny wirtualnej w hello tego samego regionu obserwatora sieciowego z hello [rozszerzenie systemu Windows](../virtual-machines/windows/extensions-nwa.md) lub [rozszerzenie maszyny wirtualnej systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="0321e-120">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="0321e-120">Scenario</span></span>

<span data-ttu-id="0321e-121">W tym przykładzie maszyna wirtualna wysyła więcej segmentów TCP niż zwykle, i chcesz toobe alerty.</span><span class="sxs-lookup"><span data-stu-id="0321e-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="0321e-122">Segmentów TCP są używane jako w tym przykładzie, ale można użyć dowolnego warunku alertu.</span><span class="sxs-lookup"><span data-stu-id="0321e-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="0321e-123">Po wyświetleniu powiadomienia, ma tooreceive toounderstand danych na poziomie pakietów, dlaczego wzrosło komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="0321e-124">Następnie możesz wykonać czynności tooreturn hello maszyny wirtualnej tooregular komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="0321e-125">W tym scenariuszu założono, że istniejące wystąpienie programu obserwatora sieciowego i grupy zasobów z prawidłową maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="0321e-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="0321e-126">następujące listy Hello znajduje się przegląd hello przepływu pracy, który ma miejsce:</span><span class="sxs-lookup"><span data-stu-id="0321e-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="0321e-127">Alert zostanie wywołany na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0321e-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="0321e-128">Hello alert wywołania funkcji platformy Azure za pomocą elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="0321e-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="0321e-129">Funkcja Azure przetwarza hello alert i uruchamia sesję przechwytywania pakietów obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="0321e-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="0321e-130">przechwytywania pakietów Hello jest uruchamiany na powitania maszyny Wirtualnej i zbiera ruchu.</span><span class="sxs-lookup"><span data-stu-id="0321e-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="0321e-131">Witaj pliku przechwytywania pakietów jest przekazywany tooa konta magazynu do przeglądu i diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="0321e-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="0321e-132">tooautomate ten proces, możemy utworzyć i na naszych tootrigger maszyny Wirtualnej połączenie alert, gdy wystąpi zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="0321e-133">Możemy również utworzyć toocall funkcji do obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="0321e-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="0321e-134">W tym scenariuszu hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0321e-134">This scenario does hello following:</span></span>

* <span data-ttu-id="0321e-135">Tworzy funkcję platformy Azure, która rozpoczyna się przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="0321e-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="0321e-136">Tworzy regułę alertu na maszynie wirtualnej i konfiguruje hello reguły alertu toocall hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0321e-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="0321e-137">Tworzenie funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0321e-137">Create an Azure function</span></span>

<span data-ttu-id="0321e-138">pierwszym krokiem Hello toocreate alert hello tooprocess funkcji platformy Azure i utworzyć przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="0321e-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="0321e-139">W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **nowy** > **obliczeniowe** > **aplikacji funkcji**.</span><span class="sxs-lookup"><span data-stu-id="0321e-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Tworzenie aplikacji — funkcja][1-1]

2. <span data-ttu-id="0321e-141">Na powitania **aplikacji funkcji** bloku, wprowadź następujące wartości hello, a następnie wybierz **OK** aplikacji hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="0321e-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="0321e-142">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="0321e-142">**Setting**</span></span> | <span data-ttu-id="0321e-143">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="0321e-143">**Value**</span></span> | <span data-ttu-id="0321e-144">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="0321e-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="0321e-145">**Nazwa aplikacji**</span><span class="sxs-lookup"><span data-stu-id="0321e-145">**App name**</span></span>|<span data-ttu-id="0321e-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="0321e-146">PacketCaptureExample</span></span>|<span data-ttu-id="0321e-147">Nazwa Hello hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="0321e-148">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="0321e-148">**Subscription**</span></span>|<span data-ttu-id="0321e-149">[Subskrypcji] hello subskrypcji dla aplikacji funkcja hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0321e-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="0321e-150">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="0321e-150">**Resource Group**</span></span>|<span data-ttu-id="0321e-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="0321e-151">PacketCaptureRG</span></span>|<span data-ttu-id="0321e-152">Witaj zasobów grupy toocontain hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="0321e-153">**Plan hostingu**</span><span class="sxs-lookup"><span data-stu-id="0321e-153">**Hosting Plan**</span></span>|<span data-ttu-id="0321e-154">Użycie planu</span><span class="sxs-lookup"><span data-stu-id="0321e-154">Consumption Plan</span></span>| <span data-ttu-id="0321e-155">Typ Hello planowanie używany przez funkcję aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="0321e-156">Dostępne opcje to zużycie lub plan usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="0321e-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="0321e-157">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="0321e-157">**Location**</span></span>|<span data-ttu-id="0321e-158">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="0321e-158">Central US</span></span>| <span data-ttu-id="0321e-159">region Hello toocreate hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="0321e-160">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="0321e-160">**Storage Account**</span></span>|<span data-ttu-id="0321e-161">{automatycznie wygenerowaną}</span><span class="sxs-lookup"><span data-stu-id="0321e-161">{autogenerated}</span></span>| <span data-ttu-id="0321e-162">Konto magazynu Hello Azure Functions potrzeb magazynu ogólnego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="0321e-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="0321e-163">Na powitania **aplikacji funkcji PacketCaptureExample** bloku, wybierz opcję **funkcje** > **Niestandardowa funkcja**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="0321e-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="0321e-164">Wybierz **HttpTrigger Powershell**, a następnie wprowadź hello pozostałe informacje.</span><span class="sxs-lookup"><span data-stu-id="0321e-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="0321e-165">Na koniec toocreate hello funkcji, wybierz opcję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0321e-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="0321e-166">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="0321e-166">**Setting**</span></span> | <span data-ttu-id="0321e-167">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="0321e-167">**Value**</span></span> | <span data-ttu-id="0321e-168">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="0321e-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="0321e-169">**Scenariusz**</span><span class="sxs-lookup"><span data-stu-id="0321e-169">**Scenario**</span></span>|<span data-ttu-id="0321e-170">Eksperymentalne</span><span class="sxs-lookup"><span data-stu-id="0321e-170">Experimental</span></span>|<span data-ttu-id="0321e-171">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="0321e-171">Type of scenario</span></span>|
    |<span data-ttu-id="0321e-172">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="0321e-172">**Name your function**</span></span>|<span data-ttu-id="0321e-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="0321e-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="0321e-174">Nazwa funkcji hello</span><span class="sxs-lookup"><span data-stu-id="0321e-174">Name of hello function</span></span>|
    |<span data-ttu-id="0321e-175">**Poziom dostępu**</span><span class="sxs-lookup"><span data-stu-id="0321e-175">**Authorization level**</span></span>|<span data-ttu-id="0321e-176">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0321e-176">Function</span></span>|<span data-ttu-id="0321e-177">Poziom dostępu dla hello — funkcja</span><span class="sxs-lookup"><span data-stu-id="0321e-177">Authorization level for hello function</span></span>|

![Przykład funkcji][functions1]

> [!NOTE]
> <span data-ttu-id="0321e-179">Szablon programu PowerShell Hello jest eksperymentalna i nie ma pełnej obsługi.</span><span class="sxs-lookup"><span data-stu-id="0321e-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="0321e-180">Dostosowania są wymagane w ramach tego przykładu i opisano szczegółowo w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="0321e-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="0321e-181">Dodawanie modułów</span><span class="sxs-lookup"><span data-stu-id="0321e-181">Add modules</span></span>

<span data-ttu-id="0321e-182">toouse poleceń cmdlet programu PowerShell obserwatora sieciowego, przekazać hello najnowsze PowerShell modułu toohello funkcja aplikację.</span><span class="sxs-lookup"><span data-stu-id="0321e-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="0321e-183">Na komputerze lokalnym hello zainstalowane najnowsze modułów programu Azure PowerShell uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="0321e-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="0321e-184">Dzięki temu przykład Witaj ścieżki lokalnej z modułów programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0321e-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="0321e-185">Te foldery są używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="0321e-185">These folders are used in a later step.</span></span> <span data-ttu-id="0321e-186">Moduły Hello, które są używane w tym scenariuszu są:</span><span class="sxs-lookup"><span data-stu-id="0321e-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="0321e-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="0321e-187">AzureRM.Network</span></span>

    * <span data-ttu-id="0321e-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="0321e-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="0321e-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="0321e-189">AzureRM.Resources</span></span>

    ![Foldery programu PowerShell][functions5]

1. <span data-ttu-id="0321e-191">Wybierz **funkcji ustawienia aplikacji** > **Przejdź tooApp Edytor usługi**.</span><span class="sxs-lookup"><span data-stu-id="0321e-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Ustawienia aplikacji — funkcja][functions2]

1. <span data-ttu-id="0321e-193">Kliknij prawym przyciskiem myszy hello **AlertPacketCapturePowershell** folder, a następnie utwórz folder o nazwie **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="0321e-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="0321e-194">Utwórz podfolder dla poszczególnych modułów, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="0321e-194">Create a subfolder for each module that you need.</span></span>

    ![Folderze i jego podfolderach][functions3]

    * <span data-ttu-id="0321e-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="0321e-196">AzureRM.Network</span></span>

    * <span data-ttu-id="0321e-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="0321e-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="0321e-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="0321e-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="0321e-199">Kliknij prawym przyciskiem myszy hello **AzureRM.Network** podfolder, a następnie wybierz **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="0321e-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="0321e-200">Przejdź tooyour Azure modułów.</span><span class="sxs-lookup"><span data-stu-id="0321e-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="0321e-201">W lokalnej hello **AzureRM.Network** folderu, wybierz wszystkie pliki hello w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="0321e-202">Następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="0321e-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="0321e-203">Powtórz te kroki dla **AzureRM.Profile** i **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="0321e-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Przekazywanie plików][functions6]

1. <span data-ttu-id="0321e-205">Po zakończeniu, każdy folder powinien mieć hello pliki modułu programu PowerShell z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0321e-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Pliki środowiska PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="0321e-207">Authentication</span><span class="sxs-lookup"><span data-stu-id="0321e-207">Authentication</span></span>

<span data-ttu-id="0321e-208">polecenia cmdlet programu PowerShell hello toouse, wymagane jest uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="0321e-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="0321e-209">Możesz skonfigurować uwierzytelnianie w hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="0321e-210">tooconfigure uwierzytelniania, należy skonfigurować zmienne środowiskowe i przekazać aplikację funkcja toohello zaszyfrowanego pliku klucza.</span><span class="sxs-lookup"><span data-stu-id="0321e-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="0321e-211">Ten scenariusz zawiera tylko jeden przykład jak tooimplement uwierzytelniania za pomocą usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0321e-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="0321e-212">Istnieją inne sposoby toodo to.</span><span class="sxs-lookup"><span data-stu-id="0321e-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="0321e-213">Zaszyfrowane poświadczenia</span><span class="sxs-lookup"><span data-stu-id="0321e-213">Encrypted credentials</span></span>

<span data-ttu-id="0321e-214">Witaj następującego skryptu programu PowerShell tworzy plik klucza o nazwie **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="0321e-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="0321e-215">Umożliwia także zaszyfrowana wersja hello hasła, które jest dostarczone.</span><span class="sxs-lookup"><span data-stu-id="0321e-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="0321e-216">To hasło jest hello tego samego hasła, który jest zdefiniowany dla aplikacji usługi Azure Active Directory hello, który jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0321e-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="0321e-217">W hello Edytor usług aplikacji hello funkcji aplikacji, Utwórz folder o nazwie **klucze** w obszarze **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0321e-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="0321e-218">Następnie przekaż hello **PassEncryptKey.key** pliku, który został utworzony w hello powyższego przykładu środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0321e-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Funkcje klucza][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="0321e-220">Pobieranie wartości zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="0321e-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="0321e-221">wymaganie końcowego Hello jest tooset się hello zmiennych środowiskowych, które są niezbędne tooaccess hello wartości dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0321e-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="0321e-222">Witaj poniższej liście przedstawiono hello zmiennych środowiskowych, które są tworzone:</span><span class="sxs-lookup"><span data-stu-id="0321e-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="0321e-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="0321e-223">AzureClientID</span></span>

* <span data-ttu-id="0321e-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="0321e-224">AzureTenant</span></span>

* <span data-ttu-id="0321e-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="0321e-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="0321e-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="0321e-226">AzureClientID</span></span>

<span data-ttu-id="0321e-227">Identyfikator klienta Hello jest hello identyfikator aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0321e-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="0321e-228">Jeśli nie masz jeszcze toouse aplikacji, należy uruchomić powitania po toocreate przykład aplikację.</span><span class="sxs-lookup"><span data-stu-id="0321e-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="0321e-229">hasło Hello, który jest używany podczas tworzenia aplikacji hello powinna być hello tego samego hasła utworzonego wcześniej podczas zapisywania pliku klucza hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="0321e-230">Hello portalu Azure, wybierz **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="0321e-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="0321e-231">Wybierz hello toouse subskrypcji, a następnie wybierz **(IAM) kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="0321e-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![Funkcje IAM][functions9]

1. <span data-ttu-id="0321e-233">Wybierz hello toouse konta, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0321e-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="0321e-234">Skopiuj hello identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-234">Copy hello Application ID.</span></span>

    ![Identyfikator aplikacji funkcji][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="0321e-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="0321e-236">AzureTenant</span></span>

<span data-ttu-id="0321e-237">Uzyskaj identyfikator dzierżawcy hello uruchamiając hello następujące przykładowe środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0321e-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="0321e-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="0321e-238">AzureCredPassword</span></span>

<span data-ttu-id="0321e-239">Witaj wartości zmiennej środowiskowej AzureCredPassword hello jest wartość hello, który można pobrać z systemem hello następujące przykładowe programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0321e-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="0321e-240">W tym przykładzie jest hello sam, co przedstawiono w poprzednim hello **zaszyfrowane poświadczenia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0321e-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="0321e-241">Witaj wartość, która jest potrzebna jest wyjściem hello hello `$Encryptedpassword` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="0321e-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="0321e-242">To jest hello usługi głównej hasło szyfrowane przy użyciu skryptu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="0321e-243">Zmienne środowiskowe hello magazynu</span><span class="sxs-lookup"><span data-stu-id="0321e-243">Store hello environment variables</span></span>

1. <span data-ttu-id="0321e-244">Przejdź toohello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-244">Go toohello function app.</span></span> <span data-ttu-id="0321e-245">Następnie wybierz **funkcji ustawienia aplikacji** > **Konfiguruj ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="0321e-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Konfigurowanie ustawień aplikacji][functions11]

1. <span data-ttu-id="0321e-247">Dodaj hello zmienne środowiskowe i ich ustawienia aplikacji toohello wartości, a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="0321e-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Ustawienia aplikacji][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="0321e-249">Dodawanie funkcji toohello programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0321e-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="0321e-250">Jest teraz toomake czasu wywołuje obserwatora sieciowego z wewnątrz hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0321e-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="0321e-251">W zależności od wymagań hello hello stosowania tej funkcji może się różnić.</span><span class="sxs-lookup"><span data-stu-id="0321e-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="0321e-252">Jednak hello ogólny przebieg kodu hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="0321e-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="0321e-253">Parametry wejściowe procesu.</span><span class="sxs-lookup"><span data-stu-id="0321e-253">Process input parameters.</span></span>
2. <span data-ttu-id="0321e-254">Istniejący pakiet kwerendy przechwytuje limity tooverify i rozwiązać konflikty nazw.</span><span class="sxs-lookup"><span data-stu-id="0321e-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="0321e-255">Utwórz przechwytywania pakietów z odpowiednimi parametrami.</span><span class="sxs-lookup"><span data-stu-id="0321e-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="0321e-256">Przechwytywania pakietów sondowania okresowo czasu jego ukończenia.</span><span class="sxs-lookup"><span data-stu-id="0321e-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="0321e-257">Powiadomienie użytkownika hello, że sesja przechwytywania pakietów hello jest pełny.</span><span class="sxs-lookup"><span data-stu-id="0321e-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="0321e-258">Witaj poniższym przykładzie jest kod programu PowerShell, który może być używana w funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="0321e-259">Brak wartości, które wymagają toobe zastąpione dla **subscriptionId**, **resourceGroupName**, i **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="0321e-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="0321e-260">Pobierz adres URL funkcji hello</span><span class="sxs-lookup"><span data-stu-id="0321e-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="0321e-261">Po utworzeniu funkcji, należy skonfigurować adres URL hello alertu toocall skojarzoną z hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="0321e-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="0321e-262">tooget tę wartość, adres URL funkcji hello kopiowania z funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0321e-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Znajdowanie hello adres URL funkcji][functions13]

2. <span data-ttu-id="0321e-264">Skopiuj adres URL funkcji hello aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="0321e-264">Copy hello function URL for your function app.</span></span>

    ![Kopiowanie hello adres URL funkcji][2]

<span data-ttu-id="0321e-266">Jeśli potrzebujesz właściwości niestandardowe w ładunku żądania POST webhook hello hello odwoływać się za[skonfigurować elementu webhook na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="0321e-267">Konfigurowanie alertu dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0321e-267">Configure an alert on a VM</span></span>

<span data-ttu-id="0321e-268">Alerty, które mogą zostać skonfigurowane toonotify osób po określonej metryki przekracza wartość progową, który jest przypisany tooit.</span><span class="sxs-lookup"><span data-stu-id="0321e-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="0321e-269">W tym przykładzie hello alertu znajduje się na powitania segmentów TCP, które są wysyłane, ale hello alertu można wywoływać dla innych metryk.</span><span class="sxs-lookup"><span data-stu-id="0321e-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="0321e-270">W tym przykładzie alert jest skonfigurowany toocall funkcji hello toocall elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="0321e-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="0321e-271">Utwórz regułę alertu hello</span><span class="sxs-lookup"><span data-stu-id="0321e-271">Create hello alert rule</span></span>

<span data-ttu-id="0321e-272">Przejdź tooan istniejącej maszyny wirtualnej, a następnie dodaj regułę alertu.</span><span class="sxs-lookup"><span data-stu-id="0321e-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="0321e-273">Bardziej szczegółowa dokumentacja na temat konfigurowania alertów można znaleźć w folderze [w monitorze Azure tworzyć alerty dla usług Azure - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="0321e-274">Wprowadź następujące wartości w hello hello **reguły alertu** bloku, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="0321e-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="0321e-275">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="0321e-275">**Setting**</span></span> | <span data-ttu-id="0321e-276">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="0321e-276">**Value**</span></span> | <span data-ttu-id="0321e-277">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="0321e-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="0321e-278">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="0321e-278">**Name**</span></span>|<span data-ttu-id="0321e-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="0321e-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="0321e-280">Nazwa reguły alertów hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="0321e-281">**Opis**</span><span class="sxs-lookup"><span data-stu-id="0321e-281">**Description**</span></span>|<span data-ttu-id="0321e-282">Przekroczono próg wysyłane segmentów TCP</span><span class="sxs-lookup"><span data-stu-id="0321e-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="0321e-283">Opis Hello hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="0321e-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="0321e-284">**Metryka**</span><span class="sxs-lookup"><span data-stu-id="0321e-284">**Metric**</span></span>|<span data-ttu-id="0321e-285">Wysłane segmenty protokołu TCP</span><span class="sxs-lookup"><span data-stu-id="0321e-285">TCP segments sent</span></span>| <span data-ttu-id="0321e-286">Witaj metryki toouse tootrigger hello alert.</span><span class="sxs-lookup"><span data-stu-id="0321e-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="0321e-287">**Warunek**</span><span class="sxs-lookup"><span data-stu-id="0321e-287">**Condition**</span></span>|<span data-ttu-id="0321e-288">Więcej niż</span><span class="sxs-lookup"><span data-stu-id="0321e-288">Greater than</span></span>| <span data-ttu-id="0321e-289">toouse warunek Hello podczas obliczania metryki hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="0321e-290">**Próg**</span><span class="sxs-lookup"><span data-stu-id="0321e-290">**Threshold**</span></span>|<span data-ttu-id="0321e-291">100</span><span class="sxs-lookup"><span data-stu-id="0321e-291">100</span></span>| <span data-ttu-id="0321e-292">wartość Hello hello metryki, które wyzwala hello alert.</span><span class="sxs-lookup"><span data-stu-id="0321e-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="0321e-293">Ta wartość musi być ustawiona tooa prawidłową wartość dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="0321e-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="0321e-294">**Okres**</span><span class="sxs-lookup"><span data-stu-id="0321e-294">**Period**</span></span>|<span data-ttu-id="0321e-295">Za pośrednictwem hello ostatnich pięciu minut</span><span class="sxs-lookup"><span data-stu-id="0321e-295">Over hello last five minutes</span></span>| <span data-ttu-id="0321e-296">Określa okres hello w których toolook próg hello na powitania metryki.</span><span class="sxs-lookup"><span data-stu-id="0321e-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="0321e-297">**Element Webhook**</span><span class="sxs-lookup"><span data-stu-id="0321e-297">**Webhook**</span></span>|<span data-ttu-id="0321e-298">[adres URL elementu webhook z funkcji aplikacji]</span><span class="sxs-lookup"><span data-stu-id="0321e-298">[webhook URL from function app]</span></span>| <span data-ttu-id="0321e-299">adres URL elementu webhook Hello z hello funkcji aplikacji, który został utworzony w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="0321e-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="0321e-300">Metryka segmentów TCP Hello nie jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="0321e-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="0321e-301">Dowiedz się więcej na temat tooenable dodatkowe metryki, odwiedzając [włączania monitorowania i diagnostyki](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="0321e-302">Przejrzyj wyniki hello</span><span class="sxs-lookup"><span data-stu-id="0321e-302">Review hello results</span></span>

<span data-ttu-id="0321e-303">Po hello kryteria alertu wyzwalaczy hello jest tworzony przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="0321e-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="0321e-304">Przejdź tooNetwork obserwatora, a następnie wybierz **przechwytywania pakietów**.</span><span class="sxs-lookup"><span data-stu-id="0321e-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="0321e-305">Na tej stronie możesz wybrać hello pakietów przechwytywania pliku łącza toodownload hello pakietów przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="0321e-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Widok przechwytywania pakietów][functions14]

<span data-ttu-id="0321e-307">Jeśli plik przechwytywania hello jest przechowywany lokalnie, można je pobrać, logując się toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0321e-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="0321e-308">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu Azure, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="0321e-309">Kolejnym narzędziem służy jest [Eksploratora usługi Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0321e-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="0321e-310">Po pobraniu programu przechwytywania można wyświetlić go przy użyciu dowolnego narzędzia, który może odczytywać **CAP** pliku.</span><span class="sxs-lookup"><span data-stu-id="0321e-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="0321e-311">Poniżej podano linki tootwo tych narzędzi:</span><span class="sxs-lookup"><span data-stu-id="0321e-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="0321e-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="0321e-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="0321e-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="0321e-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="0321e-314">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0321e-314">Next steps</span></span>

<span data-ttu-id="0321e-315">Dowiedz się, jak tooview Twojego pakietów przechwytuje odwiedzając [analizy przechwytywania pakietu z programu Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="0321e-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
