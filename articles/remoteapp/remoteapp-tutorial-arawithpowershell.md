---
title: "aaaUse poleceń cmdlet programu PowerShell z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse poleceń cmdlet programu Windows PowerShell w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="6ed5c-103">Użyj polecenia cmdlet programu Windows PowerShell z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6ed5c-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6ed5c-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6ed5c-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="6ed5c-106">Można użyć tooadminister poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp hello i obsługa kolekcji.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="6ed5c-107">Użyj hello następujące informacje tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="6ed5c-108">Pobierz hello poleceń cmdlet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="6ed5c-109">Należy najpierw pobrać poleceń cmdlet programu Azure Powershell hello [tutaj](http://go.microsoft.com/?linkid=9811175), poleceń cmdlet funkcji RemoteApp hello znajdują się w nim.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="6ed5c-110">Zapoznaj się z hello [pomocy polecenia cmdlet usługi Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="6ed5c-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="6ed5c-111">Skonfiguruj subskrypcję toouse poleceń cmdlet systemu Azure</span><span class="sxs-lookup"><span data-stu-id="6ed5c-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="6ed5c-112">Postępuj zgodnie z [w tym przewodniku](/powershell/azure/overview) dzięki czemu można użyć poleceń cmdlet hello względem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="6ed5c-113">Możesz użyć tych tooget kroki szybko rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="6ed5c-114">Pobierz i zainstaluj hello [poleceń cmdlet programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="6ed5c-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="6ed5c-115">Uruchom program PowerShell platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="6ed5c-116">Uruchom **Add-AzureAccount** tooyour tooauthenticate subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="6ed5c-117">Po wyświetleniu monitu wprowadź hello tej samej nazwy użytkownika i hasła, użyj toosign w portalu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="6ed5c-118">Uruchom **Get-AzureSubscription** toolist hello subskrypcji skojarzonych z Twoim kontem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="6ed5c-119">Uruchom **AzureSubscription wybierz — Nazwa subskrypcji &lt;Nazwa subskrypcji&gt;**  lub **AzureSubscription wybierz - SubscriptionId &lt;identyfikator subskrypcji&gt;**  toospecify hello subskrypcji toouse.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="6ed5c-120">Gratulacje, konsola programu Azure PowerShell jest skonfigurowany i gotowy toouse.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="6ed5c-121">Należy pamiętać, że musisz mieć toorepeate kroki od 2 do 5 w każdym uruchomieniu konsoli programu Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="6ed5c-122">Wyświetl listę wszystkich kolekcji</span><span class="sxs-lookup"><span data-stu-id="6ed5c-122">List all collections</span></span>
- - -
     <span data-ttu-id="6ed5c-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="6ed5c-124">Usuwanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="6ed5c-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="6ed5c-125">Usuń AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="6ed5c-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="6ed5c-126">Przykład: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="6ed5c-127">Tworzenie kolekcji w chmurze</span><span class="sxs-lookup"><span data-stu-id="6ed5c-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="6ed5c-128">To proste, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="6ed5c-129">Witaj powyżej polecenie automatycznie publikuje aplikacje Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio i Word).</span><span class="sxs-lookup"><span data-stu-id="6ed5c-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="6ed5c-130">Tworzenie kolekcji może potrwać 30 minut lub dłużej toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6ed5c-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="6ed5c-131">Dlatego to polecenie zwraca identyfikator śledzenia, w którym można w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="6ed5c-132">Po wykonaniu czynności hello kolekcji można dodać kolekcji toohello użytkowników z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="6ed5c-133">I gotowe!</span><span class="sxs-lookup"><span data-stu-id="6ed5c-133">And you're done!</span></span> <span data-ttu-id="6ed5c-134">Ten użytkownik powinien być stanie tooconnect toohello aplikacji za pomocą klienta usługi Azure RemoteApp hello znaleziono [tutaj](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ed5c-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="6ed5c-135">Dostępne polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-135">Available cmdlets</span></span>
<span data-ttu-id="6ed5c-136">Istnieje wiele innych poleceń mamy, zostanie udostępniona wkrótce hello dokumentacji dla nich:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="6ed5c-137">Podstawowe kolekcji usługi RemoteApp poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="6ed5c-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="6ed5c-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="6ed5c-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="6ed5c-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="6ed5c-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="6ed5c-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="6ed5c-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="6ed5c-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="6ed5c-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="6ed5c-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="6ed5c-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="6ed5c-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="6ed5c-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="6ed5c-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="6ed5c-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="6ed5c-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="6ed5c-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="6ed5c-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="6ed5c-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="6ed5c-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="6ed5c-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="6ed5c-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="6ed5c-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="6ed5c-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="6ed5c-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="6ed5c-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="6ed5c-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="6ed5c-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="6ed5c-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="6ed5c-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="6ed5c-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="6ed5c-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="6ed5c-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="6ed5c-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="6ed5c-157">Polecenia cmdlet sieci wirtualnej usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="6ed5c-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="6ed5c-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="6ed5c-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="6ed5c-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="6ed5c-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="6ed5c-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="6ed5c-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="6ed5c-163">Get - AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="6ed5c-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="6ed5c-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="6ed5c-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="6ed5c-165">Polecenia cmdlet obrazu szablonu usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="6ed5c-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="6ed5c-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="6ed5c-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="6ed5c-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="6ed5c-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="6ed5c-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="6ed5c-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="6ed5c-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="6ed5c-170">Inne polecenia cmdlet usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="6ed5c-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="6ed5c-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="6ed5c-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="6ed5c-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="6ed5c-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="6ed5c-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="6ed5c-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="6ed5c-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="6ed5c-174">Get-AzureRemoteAppOperationResult</span></span>

