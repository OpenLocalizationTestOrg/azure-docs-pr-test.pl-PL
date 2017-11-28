---
title: "Dzienniki aaaIntegrate z usługi Azure Key Vault za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Samouczek, który udostępnia hello niezbędne kroki toomake Key Vault dzienniki dostępne tooa SIEM za pomocą integracji dziennika Azure"
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
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="58684-103">Samouczek usługi Azure integracji dziennika: zdarzeń procesu usługi Azure Key Vault za pomocą usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="58684-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="58684-104">Można użyć zdarzenia rejestrowane tooretrieve integracji dziennika Azure i były dostępne tooyour zabezpieczeń systemu informacji i zdarzeń zarządzania (SIEM).</span><span class="sxs-lookup"><span data-stu-id="58684-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="58684-105">W tym samouczku przedstawiono sposób integracji dziennika Azure może być używane tooprocess dzienniki, które zostały zakupione w ramach usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="58684-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="58684-106">Użyj tego samouczka tooget zapoznanie się z sposób integracji dziennika Azure i usługi Event Hubs pracy ze sobą następuje hello przykładowe kroki i zrozumienie, jak każdy krok obsługuje hello rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="58684-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="58684-107">Następnie należy wykonać co znasz tutaj toocreate własne toosupport kroki unikatowe wymagania firmy.</span><span class="sxs-lookup"><span data-stu-id="58684-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="58684-108">Witaj kroków i poleceń, w tym samouczku nie są zamierzone toobe skopiowane i wklejone.</span><span class="sxs-lookup"><span data-stu-id="58684-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="58684-109">Są one tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="58684-109">They're examples only.</span></span> <span data-ttu-id="58684-110">Nie należy używać poleceń programu PowerShell hello "w jakim jest" w środowisku na żywo.</span><span class="sxs-lookup"><span data-stu-id="58684-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="58684-111">Należy dostosować oparte na środowisku unikatowy.</span><span class="sxs-lookup"><span data-stu-id="58684-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="58684-112">Ten samouczek przeprowadzi Cię przez proces hello Centrum zdarzeń zarejestrowanych tooan działania usługi Azure Key Vault pobieranie oraz udostępnianie go jako system SIEM tooyour pliki JSON.</span><span class="sxs-lookup"><span data-stu-id="58684-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="58684-113">Następnie można skonfigurować pliki JSON hello tooprocess system SIEM.</span><span class="sxs-lookup"><span data-stu-id="58684-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="58684-114">Większość hello kroków w tym samouczku obejmują konfigurowanie magazynów kluczy konta magazynu i usługi event hubs.</span><span class="sxs-lookup"><span data-stu-id="58684-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="58684-115">określone kroki integracji dziennika Azure Hello są hello na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="58684-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="58684-116">Nie należy wykonywać następujące czynności w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="58684-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="58684-117">Są one przeznaczone dla środowiska laboratoryjnego.</span><span class="sxs-lookup"><span data-stu-id="58684-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="58684-118">Należy dostosować hello kroki przed ich użyciem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="58684-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="58684-119">Informacje udostępniane wzdłuż hello sposób pomaga się, że rozumiesz hello przyczynami każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="58684-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="58684-120">Artykuły tooother łącza umożliwiają bardziej szczegółowo na niektóre tematy.</span><span class="sxs-lookup"><span data-stu-id="58684-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="58684-121">Aby uzyskać więcej informacji o usługach hello, które w tym samouczku uwagi zobacz:</span><span class="sxs-lookup"><span data-stu-id="58684-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="58684-122">Usługa Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="58684-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="58684-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="58684-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="58684-124">Integracja z dzienników Azure</span><span class="sxs-lookup"><span data-stu-id="58684-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="58684-125">Początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="58684-125">Initial setup</span></span>

<span data-ttu-id="58684-126">Przed ukończeniem hello opisanych w tym artykule, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="58684-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="58684-127">Subskrypcja platformy Azure i konta dla tej subskrypcji z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="58684-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="58684-128">Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="58684-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="58684-129">System z toohello dostęp do Internetu, który spełnia wymagania hello Azure integracji dziennika instalacji.</span><span class="sxs-lookup"><span data-stu-id="58684-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="58684-130">Hello system może znajdować się na usługi w chmurze lub obsługiwanego lokalnie.</span><span class="sxs-lookup"><span data-stu-id="58684-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="58684-131">[Integracja z usługą Azure dziennika](https://www.microsoft.com/download/details.aspx?id=53324) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="58684-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="58684-132">tooinstall go:</span><span class="sxs-lookup"><span data-stu-id="58684-132">tooinstall it:</span></span>

   <span data-ttu-id="58684-133">a.</span><span class="sxs-lookup"><span data-stu-id="58684-133">a.</span></span> <span data-ttu-id="58684-134">Należy używać systemu toohello tooconnect pulpitu zdalnego wspomnianego w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="58684-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="58684-135">b.</span><span class="sxs-lookup"><span data-stu-id="58684-135">b.</span></span> <span data-ttu-id="58684-136">Skopiuj hello Azure integracji dziennika Instalatora toohello systemu.</span><span class="sxs-lookup"><span data-stu-id="58684-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="58684-137">Możesz [pobierane pliki instalacyjne hello](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="58684-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="58684-138">c.</span><span class="sxs-lookup"><span data-stu-id="58684-138">c.</span></span> <span data-ttu-id="58684-139">Uruchom Instalator hello i zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="58684-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="58684-140">d.</span><span class="sxs-lookup"><span data-stu-id="58684-140">d.</span></span> <span data-ttu-id="58684-141">Jeśli będzie zawierał informacje telemetryczne, pozostaw zaznaczone pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="58684-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="58684-142">Jeśli użytkownik nie wysłać tooMicrosoft informacji użycia, wyczyść pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="58684-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="58684-143">Aby uzyskać więcej informacji o integracji z dziennika Azure i w jaki sposób tooinstall, zobacz [Azure dziennika Integracja z usługą rejestrowania diagnostyki Azure i funkcji przekazywania zdarzeń systemu Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58684-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="58684-144">Witaj najnowsza wersja programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58684-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="58684-145">Jeśli masz zainstalowany program Windows Server 2016, musisz mieć co najmniej PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="58684-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="58684-146">Jeśli używasz wersji systemu Windows Server może być starsza wersja programu PowerShell jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="58684-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="58684-147">Można sprawdzić wersji hello wprowadzając ```get-host``` w oknie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58684-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="58684-148">Jeśli nie masz programu PowerShell 5.0 zainstalowany, możesz [go pobrać](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="58684-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="58684-149">Po utworzeniu co najmniej PowerShell 5.0, możesz przejść tooinstall hello najnowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="58684-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="58684-150">a.</span><span class="sxs-lookup"><span data-stu-id="58684-150">a.</span></span> <span data-ttu-id="58684-151">W oknie programu PowerShell, wprowadź hello ```Install-Module Azure``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="58684-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="58684-152">Wykonaj kroki instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="58684-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="58684-153">b.</span><span class="sxs-lookup"><span data-stu-id="58684-153">b.</span></span> <span data-ttu-id="58684-154">Wprowadź hello ```Install-Module AzureRM``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="58684-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="58684-155">Wykonaj kroki instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="58684-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="58684-156">Aby uzyskać więcej informacji, zobacz [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="58684-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="58684-157">Utwórz elementy infrastruktury obsługi</span><span class="sxs-lookup"><span data-stu-id="58684-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="58684-158">Otwórz okno programu PowerShell z podwyższonym poziomem uprawnień i przejdź zbyt**C:\Program Files\Microsoft Azure dziennika integracji**.</span><span class="sxs-lookup"><span data-stu-id="58684-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="58684-159">Zaimportuj polecenia cmdlet AzLog hello przez uruchomienie skryptu hello LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="58684-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="58684-160">Wprowadź hello `.\LoadAzLogModule.ps1` polecenia.</span><span class="sxs-lookup"><span data-stu-id="58684-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="58684-161">(Uwaga hello ". \" w tym poleceniu.) Powinny zostać wyświetlone informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="58684-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Listę załadowanych modułów](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="58684-163">Wprowadź hello `Login-AzureRmAccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="58684-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="58684-164">Okno logowania hello wprowadzanie informacji o poświadczeniach hello hello subskrypcji, która będzie używana w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="58684-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="58684-165">Jeśli jest to hello jest rejestrowanie w tooAzure z tego komputera po raz pierwszy, zobaczysz komunikat o dane użycia programu PowerShell toocollect firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58684-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="58684-166">Firma Microsoft zaleca włączyć tej kolekcji danych, ponieważ będzie ona używana tooimprove programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58684-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="58684-167">Po pomyślnym uwierzytelnieniu użytkownik zalogował się i pojawi się informacja hello w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="58684-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="58684-168">Zanotuj nazwę subskrypcji hello identyfikator i subskrypcji, ponieważ konieczne będzie ich toocomplete później kroków.</span><span class="sxs-lookup"><span data-stu-id="58684-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Okno programu PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="58684-170">Utwórz zmienne toostore wartości, które będą używane później.</span><span class="sxs-lookup"><span data-stu-id="58684-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="58684-171">Wprowadź każdy hello następujące wiersze programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58684-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="58684-172">Może być konieczne tooadjust hello wartości toomatch środowiska.</span><span class="sxs-lookup"><span data-stu-id="58684-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="58684-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Nazwa Twojej subskrypcji mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="58684-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="58684-174">Można to sprawdzić jako część hello dane wyjściowe poprzedniego polecenia hello.)</span><span class="sxs-lookup"><span data-stu-id="58684-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="58684-175">```$location = 'West US'```(Ta zmienna będzie toopass używane hello lokalizacji, gdzie utworzone zasoby.</span><span class="sxs-lookup"><span data-stu-id="58684-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="58684-176">Można zmienić tej zmiennej toobe dowolnej lokalizacji wybrane.)</span><span class="sxs-lookup"><span data-stu-id="58684-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="58684-177">``` $name = 'azlogtest' + $random```(nazwa hello może być dowolna, ale powinien zawierać tylko małe litery i cyfry).</span><span class="sxs-lookup"><span data-stu-id="58684-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="58684-178">``` $storageName = $name```(Ta zmienna będzie można używać nazwy konta magazynu hello).</span><span class="sxs-lookup"><span data-stu-id="58684-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="58684-179">```$rgname = $name ```(Ta zmienna będzie służyć do nazwy grupy zasobów hello.)</span><span class="sxs-lookup"><span data-stu-id="58684-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="58684-180">``` $eventHubNameSpaceName = $name```(Jest hello nazwę przestrzeni nazw Centrum zdarzeń hello).</span><span class="sxs-lookup"><span data-stu-id="58684-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="58684-181">Określ hello subskrypcji, która będzie działać z:</span><span class="sxs-lookup"><span data-stu-id="58684-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="58684-182">Utwórz grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="58684-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="58684-183">Po wprowadzeniu `$rg` w tym momencie powinny być widoczne dane wyjściowe podobne toothis w zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="58684-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Dane wyjściowe po utworzeniu grupy zasobów](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="58684-185">Utwórz konto magazynu, które będzie używane tookeep śledzenie informacji o stanie:</span><span class="sxs-lookup"><span data-stu-id="58684-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="58684-186">Utwórz hello przestrzeni nazw z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="58684-186">Create hello event hub namespace.</span></span> <span data-ttu-id="58684-187">Jest to wymagane toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="58684-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="58684-188">Pobierz identyfikator reguły hello, który będzie używany z dostawcą insights hello:</span><span class="sxs-lookup"><span data-stu-id="58684-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="58684-189">Pobierz wszystkie możliwe lokalizacji platformy Azure i Dodaj hello nazwy tooa zmiennej, która może być używany w kolejnym kroku:</span><span class="sxs-lookup"><span data-stu-id="58684-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="58684-190">a.</span><span class="sxs-lookup"><span data-stu-id="58684-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="58684-191">b.</span><span class="sxs-lookup"><span data-stu-id="58684-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="58684-192">Po wprowadzeniu `$locations` w tym momencie wyświetlić nazwy lokalizacji hello bez dodatkowych informacji hello zwrócony przez Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="58684-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="58684-193">Utwórz profil usługi Azure Resource Manager dziennika:</span><span class="sxs-lookup"><span data-stu-id="58684-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="58684-194">Aby uzyskać więcej informacji na temat hello profilu dzienników Azure, zobacz [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="58684-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58684-195">Podczas próby toocreate profilu dziennika, może być wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="58684-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="58684-196">Można następnie przejrzyj dokumentację hello Get AzureRmLogProfile i Usuń AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="58684-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="58684-197">Po uruchomieniu Get-AzureRmLogProfile pojawi się informacja o hello dziennika profilu.</span><span class="sxs-lookup"><span data-stu-id="58684-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="58684-198">Można usunąć istniejącego profilu dziennika hello wprowadzając hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="58684-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Błąd profilu usługi Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="58684-200">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="58684-200">Create a key vault</span></span>

1. <span data-ttu-id="58684-201">Utwórz magazyn kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="58684-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="58684-202">Konfiguruj rejestrowanie dla magazynu kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="58684-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="58684-203">Wygenerować dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="58684-203">Generate log activity</span></span>

<span data-ttu-id="58684-204">Żądania muszą toobe wysyłane tooKey magazynu toogenerate dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="58684-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="58684-205">Generowania kluczy, przechowywanie kluczy tajnych, takie jak akcje lub odczytu klucze tajne z magazynu kluczy zostanie utworzona wpisy dziennika.</span><span class="sxs-lookup"><span data-stu-id="58684-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="58684-206">Wyświetl hello bieżącego magazynu kluczy:</span><span class="sxs-lookup"><span data-stu-id="58684-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="58684-207">Generuj nową **klucz2**:</span><span class="sxs-lookup"><span data-stu-id="58684-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="58684-208">Ponownie wyświetlić hello kluczy i zobacz, który **klucz2** zawiera inną wartość:</span><span class="sxs-lookup"><span data-stu-id="58684-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="58684-209">Ustaw i odczytu tajny toogenerate wpisy dziennika dodatkowe:</span><span class="sxs-lookup"><span data-stu-id="58684-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="58684-210">a.</span><span class="sxs-lookup"><span data-stu-id="58684-210">a.</span></span> <span data-ttu-id="58684-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="58684-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Zwrócony tajny](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="58684-213">Konfigurowanie integracji dzienników Azure</span><span class="sxs-lookup"><span data-stu-id="58684-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="58684-214">Skonfigurowano wszystkie hello wymaganych elementów toohave rejestrowania usługi Key Vault tooan zdarzenia koncentratora, trzeba tooconfigure Azure dziennika integracji:</span><span class="sxs-lookup"><span data-stu-id="58684-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="58684-215">Uruchom polecenie AzLog powitania dla każdego Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="58684-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="58684-216">Po minucie lub sposób uruchamiania hello ostatnich dwóch poleceń powinna zostać wyświetlona generowaną pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="58684-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="58684-217">Użytkownik może upewnij się, że przez monitorowanie katalogu hello **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="58684-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58684-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58684-218">Next steps</span></span>

- [<span data-ttu-id="58684-219">Integracja dzienników Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="58684-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="58684-220">Wprowadzenie do integracji dziennika Azure</span><span class="sxs-lookup"><span data-stu-id="58684-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="58684-221">Integrowanie dzienników z zasobów platformy Azure z systemów SIEM</span><span class="sxs-lookup"><span data-stu-id="58684-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
