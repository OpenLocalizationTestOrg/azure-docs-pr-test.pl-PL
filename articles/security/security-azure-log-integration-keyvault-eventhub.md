---
title: "Integracja dzienniki z usługi Azure Key Vault za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Samouczek, który zawiera kroki niezbędne do udostępnienia dzienników usługi Key Vault SIEM za pomocą integracji dziennika Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="68495-103">Samouczek usługi Azure integracji dziennika: zdarzeń procesu usługi Azure Key Vault za pomocą usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="68495-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="68495-104">Integracja dziennika Azure służy do pobierania zarejestrowane zdarzenia i udostępnić je do systemu zarządzania (SIEM) informacje i zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="68495-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="68495-105">W tym samouczku przedstawiono sposób integracji dziennika Azure może służyć do przetworzenia dzienniki, które zostały zakupione w ramach usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="68495-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="68495-106">Użyj tego samouczka, aby poznać sposób integracji dziennika Azure i usługi Event Hubs współpracują ze sobą następujące przykładowe kroki i zrozumienie, jak każdy krok obsługuje rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="68495-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="68495-107">Następnie może potrwać co kiedy znasz już w tym miejscu można utworzyć własne kroki, aby obsługiwać unikatowe wymagania firmy.</span><span class="sxs-lookup"><span data-stu-id="68495-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="68495-108">Kroków i poleceń, w tym samouczku nie mają zostać skopiowane i wklejone.</span><span class="sxs-lookup"><span data-stu-id="68495-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="68495-109">Są one tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="68495-109">They're examples only.</span></span> <span data-ttu-id="68495-110">Nie należy używać poleceń programu PowerShell "w jakim jest" w środowisku na żywo.</span><span class="sxs-lookup"><span data-stu-id="68495-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="68495-111">Należy dostosować oparte na środowisku unikatowy.</span><span class="sxs-lookup"><span data-stu-id="68495-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="68495-112">Ten samouczek przeprowadzi Cię przez proces podejmowania działania usługi Azure Key Vault zalogowany do Centrum zdarzeń i udostępniając ją jako pliki w formacie JSON SIEM system.</span><span class="sxs-lookup"><span data-stu-id="68495-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="68495-113">Następnie można skonfigurować system SIEM do przetworzenia plików JSON.</span><span class="sxs-lookup"><span data-stu-id="68495-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="68495-114">Większość czynności w tym samouczku obejmują konfigurowanie magazynów kluczy konta magazynu i usługi event hubs.</span><span class="sxs-lookup"><span data-stu-id="68495-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="68495-115">Kolejne kroki integracji dziennika Azure znajdują się na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="68495-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="68495-116">Nie należy wykonywać następujące czynności w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="68495-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="68495-117">Są one przeznaczone dla środowiska laboratoryjnego.</span><span class="sxs-lookup"><span data-stu-id="68495-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="68495-118">Należy dostosować kroki przed ich użyciem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="68495-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="68495-119">Informacje podane na bieżąco pomaga w zrozumieniu przyczynami każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="68495-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="68495-120">Łącza do innych artykułów nadaj bardziej szczegółowo w pewnych tematów.</span><span class="sxs-lookup"><span data-stu-id="68495-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="68495-121">Aby uzyskać więcej informacji dotyczących usług, które wymienia tego samouczka zobacz:</span><span class="sxs-lookup"><span data-stu-id="68495-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="68495-122">Usługa Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="68495-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="68495-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="68495-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="68495-124">Integracja z dzienników Azure</span><span class="sxs-lookup"><span data-stu-id="68495-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="68495-125">Początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="68495-125">Initial setup</span></span>

<span data-ttu-id="68495-126">Aby móc zakończyć kroki opisane w tym artykule, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="68495-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="68495-127">Subskrypcja platformy Azure i konta dla tej subskrypcji z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="68495-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="68495-128">Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="68495-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="68495-129">System z dostępem do Internetu, który spełnia wymagania dotyczące instalowania integracji dziennika Azure.</span><span class="sxs-lookup"><span data-stu-id="68495-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="68495-130">System może znajdować się na usługi w chmurze lub obsługiwanego lokalnie.</span><span class="sxs-lookup"><span data-stu-id="68495-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="68495-131">[Integracja z usługą Azure dziennika](https://www.microsoft.com/download/details.aspx?id=53324) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="68495-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="68495-132">Aby zainstalować go:</span><span class="sxs-lookup"><span data-stu-id="68495-132">To install it:</span></span>

   <span data-ttu-id="68495-133">a.</span><span class="sxs-lookup"><span data-stu-id="68495-133">a.</span></span> <span data-ttu-id="68495-134">Podłącz do sieci wspomnianego w kroku 2 za pomocą pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="68495-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="68495-135">b.</span><span class="sxs-lookup"><span data-stu-id="68495-135">b.</span></span> <span data-ttu-id="68495-136">Skopiuj Instalatora integracji dziennika Azure do systemu.</span><span class="sxs-lookup"><span data-stu-id="68495-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="68495-137">Możesz [pobierane pliki instalacyjne](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="68495-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="68495-138">c.</span><span class="sxs-lookup"><span data-stu-id="68495-138">c.</span></span> <span data-ttu-id="68495-139">Uruchamianie Instalatora i zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68495-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="68495-140">d.</span><span class="sxs-lookup"><span data-stu-id="68495-140">d.</span></span> <span data-ttu-id="68495-141">Jeśli będzie zawierał informacje telemetryczne, pozostaw zaznaczone pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="68495-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="68495-142">Jeśli użytkownik nie wysłać informacje o użyciu do firmy Microsoft, wyczyść pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="68495-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="68495-143">Aby uzyskać więcej informacji na temat integracji dziennika Azure i sposobu jego instalacji, zobacz [Azure dziennika Integracja z usługą rejestrowania diagnostyki Azure i funkcji przekazywania zdarzeń systemu Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68495-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="68495-144">Najnowsza wersja programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68495-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="68495-145">Jeśli masz zainstalowany program Windows Server 2016, musisz mieć co najmniej PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="68495-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="68495-146">Jeśli używasz wersji systemu Windows Server może być starsza wersja programu PowerShell jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="68495-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="68495-147">Sprawdź wersję, wprowadzając ```get-host``` w oknie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68495-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="68495-148">Jeśli nie masz programu PowerShell 5.0 zainstalowany, możesz [go pobrać](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="68495-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="68495-149">Po utworzeniu co najmniej PowerShell 5.0, możesz przejść do zainstalowania najnowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="68495-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="68495-150">a.</span><span class="sxs-lookup"><span data-stu-id="68495-150">a.</span></span> <span data-ttu-id="68495-151">W oknie programu PowerShell, wprowadź ```Install-Module Azure``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="68495-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="68495-152">Wykonaj kroki instalacji.</span><span class="sxs-lookup"><span data-stu-id="68495-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="68495-153">b.</span><span class="sxs-lookup"><span data-stu-id="68495-153">b.</span></span> <span data-ttu-id="68495-154">Wprowadź ```Install-Module AzureRM``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="68495-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="68495-155">Wykonaj kroki instalacji.</span><span class="sxs-lookup"><span data-stu-id="68495-155">Complete the installation steps.</span></span>

   <span data-ttu-id="68495-156">Aby uzyskać więcej informacji, zobacz [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="68495-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="68495-157">Utwórz elementy infrastruktury obsługi</span><span class="sxs-lookup"><span data-stu-id="68495-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="68495-158">Otwórz okno programu PowerShell z podwyższonym poziomem uprawnień i przejdź do **C:\Program Files\Microsoft Azure dziennika integracji**.</span><span class="sxs-lookup"><span data-stu-id="68495-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="68495-159">Zaimportuj polecenia cmdlet AzLog przez uruchomienie skryptu LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="68495-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="68495-160">Wprowadź `.\LoadAzLogModule.ps1` polecenia.</span><span class="sxs-lookup"><span data-stu-id="68495-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="68495-161">(Uwaga ". \" w tym poleceniu.) Powinny zostać wyświetlone informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="68495-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Listę załadowanych modułów](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="68495-163">Wprowadź `Login-AzureRmAccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="68495-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="68495-164">W oknie logowania wprowadź informacji o poświadczeniach dla subskrypcji, która będzie używana w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="68495-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="68495-165">Jeśli po raz pierwszy jest logowanie do platformy Azure z tego komputera, pojawi się komunikat o Microsoft do zbierania danych użycia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68495-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="68495-166">Firma Microsoft zaleca włączyć tej kolekcji danych, ponieważ będzie służyć do poprawienia programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68495-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="68495-167">Po pomyślnym uwierzytelnieniu użytkownik zalogował się i pojawi się informacja na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="68495-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="68495-168">Zanotuj identyfikator subskrypcji i Nazwa subskrypcji, ponieważ konieczne będzie ich zakończenie kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="68495-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![Okno programu PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="68495-170">Utwórz zmienne do przechowywania wartości, które będą używane później.</span><span class="sxs-lookup"><span data-stu-id="68495-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="68495-171">Wprowadź każdy z poniższych wierszy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68495-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="68495-172">Może być konieczne dostosowanie wartości do danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="68495-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="68495-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Nazwa Twojej subskrypcji mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="68495-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="68495-174">Można to sprawdzić w ramach danych wyjściowych poprzednie polecenie.)</span><span class="sxs-lookup"><span data-stu-id="68495-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="68495-175">```$location = 'West US'```(Ta zmienna będzie służyć do przekazywania lokalizacji, w którym ma zostać utworzony zasobów.</span><span class="sxs-lookup"><span data-stu-id="68495-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="68495-176">Można zmienić tej zmiennej można w dowolnej lokalizacji wybrane.)</span><span class="sxs-lookup"><span data-stu-id="68495-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="68495-177">``` $name = 'azlogtest' + $random```(Nazwa może być dowolna, ale powinien zawierać tylko małe litery i cyfry).</span><span class="sxs-lookup"><span data-stu-id="68495-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="68495-178">``` $storageName = $name```(Ta zmienna będzie można używać nazwy konta magazynu).</span><span class="sxs-lookup"><span data-stu-id="68495-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="68495-179">```$rgname = $name ```(Ta zmienna będzie służyć do nazwy grupy zasobów.)</span><span class="sxs-lookup"><span data-stu-id="68495-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="68495-180">``` $eventHubNameSpaceName = $name```(To jest nazwa przestrzeni nazw Centrum zdarzeń).</span><span class="sxs-lookup"><span data-stu-id="68495-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="68495-181">Określ subskrypcję, która będzie działać z:</span><span class="sxs-lookup"><span data-stu-id="68495-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="68495-182">Utwórz grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="68495-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="68495-183">Po wprowadzeniu `$rg` w tym momencie powinny być widoczne dane wyjściowe podobne do tego zrzutu ekranu:</span><span class="sxs-lookup"><span data-stu-id="68495-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Dane wyjściowe po utworzeniu grupy zasobów](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="68495-185">Utwórz konto magazynu, która będzie służyć do śledzenia informacji o stanie:</span><span class="sxs-lookup"><span data-stu-id="68495-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="68495-186">Tworzenie przestrzeni nazw Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68495-186">Create the event hub namespace.</span></span> <span data-ttu-id="68495-187">Jest to wymagane do tworzenia Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="68495-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="68495-188">Pobierz identyfikator reguły, który będzie używany z dostawcą insights:</span><span class="sxs-lookup"><span data-stu-id="68495-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="68495-189">Pobierz wszystkie możliwe lokalizacji platformy Azure i Dodaj nazwy do zmiennej używanej w kolejnym kroku:</span><span class="sxs-lookup"><span data-stu-id="68495-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="68495-190">a.</span><span class="sxs-lookup"><span data-stu-id="68495-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="68495-191">b.</span><span class="sxs-lookup"><span data-stu-id="68495-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="68495-192">Po wprowadzeniu `$locations` w tym momencie wyświetlić nazwy lokalizacji bez dodatkowych informacji zwrócony przez Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="68495-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="68495-193">Utwórz profil usługi Azure Resource Manager dziennika:</span><span class="sxs-lookup"><span data-stu-id="68495-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="68495-194">Aby uzyskać więcej informacji o profilu dzienników Azure, zobacz [Omówienie dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="68495-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="68495-195">Podczas próby utworzenia profilu dziennika, może być wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="68495-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="68495-196">Następnie zapoznanie się z dokumentacją Get AzureRmLogProfile i Usuń AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="68495-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="68495-197">Po uruchomieniu Get AzureRmLogProfile zobaczysz informacje o profilu dziennika.</span><span class="sxs-lookup"><span data-stu-id="68495-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="68495-198">Można usunąć istniejącego profilu dziennika wprowadzając ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="68495-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Błąd profilu usługi Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="68495-200">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="68495-200">Create a key vault</span></span>

1. <span data-ttu-id="68495-201">Tworzenie magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="68495-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="68495-202">Konfiguruj rejestrowanie dla magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="68495-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="68495-203">Wygenerować dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="68495-203">Generate log activity</span></span>

<span data-ttu-id="68495-204">Żądania należy wysłać do magazynu kluczy można wygenerować dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="68495-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="68495-205">Generowania kluczy, przechowywanie kluczy tajnych, takie jak akcje lub odczytu klucze tajne z magazynu kluczy zostanie utworzona wpisy dziennika.</span><span class="sxs-lookup"><span data-stu-id="68495-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="68495-206">Wyświetl bieżące klucze magazynu:</span><span class="sxs-lookup"><span data-stu-id="68495-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="68495-207">Generuj nową **klucz2**:</span><span class="sxs-lookup"><span data-stu-id="68495-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="68495-208">Wyświetlaj ponownie klucze i zobacz, który **klucz2** zawiera inną wartość:</span><span class="sxs-lookup"><span data-stu-id="68495-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="68495-209">Ustaw i klucz tajny, aby wygenerować wpisy dziennika dodatkowych do odczytu:</span><span class="sxs-lookup"><span data-stu-id="68495-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="68495-210">a.</span><span class="sxs-lookup"><span data-stu-id="68495-210">a.</span></span> <span data-ttu-id="68495-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="68495-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Zwrócony tajny](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="68495-213">Konfigurowanie integracji dzienników Azure</span><span class="sxs-lookup"><span data-stu-id="68495-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="68495-214">Teraz, gdy skonfigurowano wszystkie wymagane elementy mają Key Vault logowania do Centrum zdarzeń, należy skonfigurować integrację dziennika Azure:</span><span class="sxs-lookup"><span data-stu-id="68495-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="68495-215">Uruchom polecenie AzLog dla każdego Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="68495-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="68495-216">Po minucie lub sposób uruchamiania poleceń, ostatnie dwa powinna zostać wyświetlona generowaną pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="68495-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="68495-217">Możesz sprawdzić, który przez monitorowanie katalogu **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="68495-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68495-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68495-218">Next steps</span></span>

- [<span data-ttu-id="68495-219">Integracja dzienników Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="68495-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="68495-220">Wprowadzenie do integracji dziennika Azure</span><span class="sxs-lookup"><span data-stu-id="68495-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="68495-221">Integrowanie dzienników z zasobów platformy Azure z systemów SIEM</span><span class="sxs-lookup"><span data-stu-id="68495-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
