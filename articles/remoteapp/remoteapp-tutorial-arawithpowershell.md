---
title: "Użyj polecenia cmdlet programu PowerShell z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać poleceń cmdlet programu Windows PowerShell w usłudze Azure RemoteApp."
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
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="8d81b-103">Użyj polecenia cmdlet programu Windows PowerShell z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8d81b-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d81b-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8d81b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8d81b-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="8d81b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="8d81b-106">Do administrowania i obsługa kolekcji, można użyć poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8d81b-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="8d81b-107">Skorzystaj z poniższych informacji, aby rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="8d81b-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="8d81b-108">Polecenia cmdlet Get</span><span class="sxs-lookup"><span data-stu-id="8d81b-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="8d81b-109">Polecenia cmdlet programu Azure Powershell należy najpierw pobrać [tutaj](http://go.microsoft.com/?linkid=9811175), poleceń cmdlet programu RemoteApp znajdują się w nim.</span><span class="sxs-lookup"><span data-stu-id="8d81b-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="8d81b-110">Zapoznaj się z [pomocy polecenia cmdlet usługi Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="8d81b-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="8d81b-111">Konfigurowanie polecenia cmdlet systemu Azure, aby korzystać z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8d81b-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="8d81b-112">Postępuj zgodnie z [w tym przewodniku](/powershell/azure/overview) dzięki czemu można użyć poleceń cmdlet dla Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81b-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="8d81b-113">Korzystania z tych kroków, aby szybko rozpocząć pracę:</span><span class="sxs-lookup"><span data-stu-id="8d81b-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="8d81b-114">Pobierz i zainstaluj [poleceń cmdlet programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="8d81b-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="8d81b-115">Uruchom program PowerShell platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81b-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="8d81b-116">Uruchom **Add-AzureAccount** do uwierzytelniania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81b-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="8d81b-117">Po wyświetleniu monitu wprowadź tej samej nazwy użytkownika i hasło, którego używasz do logowania do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8d81b-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="8d81b-118">Uruchom **Get-AzureSubscription** na liście subskrypcji skojarzonych z Twoim kontem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d81b-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="8d81b-119">Uruchom **AzureSubscription wybierz — Nazwa subskrypcji &lt;Nazwa subskrypcji&gt;**  lub **AzureSubscription wybierz - SubscriptionId &lt;identyfikator subskrypcji&gt;**  Aby określić subskrypcję do użycia.</span><span class="sxs-lookup"><span data-stu-id="8d81b-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="8d81b-120">Gratulacje, konsola programu Azure PowerShell jest skonfigurowana i gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="8d81b-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="8d81b-121">Należy pamiętać, że konieczne będzie repeate kroki od 2 do 5 w każdym uruchomieniu konsoli programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d81b-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="8d81b-122">Wyświetl listę wszystkich kolekcji</span><span class="sxs-lookup"><span data-stu-id="8d81b-122">List all collections</span></span>
- - -
     <span data-ttu-id="8d81b-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="8d81b-124">Usuwanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="8d81b-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="8d81b-125">Usuń AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="8d81b-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="8d81b-126">Przykład: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="8d81b-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="8d81b-127">Tworzenie kolekcji w chmurze</span><span class="sxs-lookup"><span data-stu-id="8d81b-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="8d81b-128">To proste, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8d81b-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="8d81b-129">Powyższe polecenie automatycznie publikuje aplikacje Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio i Word).</span><span class="sxs-lookup"><span data-stu-id="8d81b-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="8d81b-130">Tworzenie kolekcji może potrwać 30 minut lub dłużej.</span><span class="sxs-lookup"><span data-stu-id="8d81b-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="8d81b-131">Dlatego to polecenie zwraca identyfikator śledzenia, w którym można w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8d81b-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="8d81b-132">Po zakończeniu kolekcji można dodać użytkowników do kolekcji przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8d81b-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="8d81b-133">I gotowe!</span><span class="sxs-lookup"><span data-stu-id="8d81b-133">And you're done!</span></span> <span data-ttu-id="8d81b-134">Ten użytkownik powinien móc połączyć się z aplikacją za pomocą klienta usługi Azure RemoteApp, znaleziono [tutaj](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="8d81b-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="8d81b-135">Dostępne polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="8d81b-135">Available cmdlets</span></span>
<span data-ttu-id="8d81b-136">Istnieje wiele innych poleceń mamy, zostanie wkrótce udostępniona w dokumentacji:</span><span class="sxs-lookup"><span data-stu-id="8d81b-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="8d81b-137">Podstawowe kolekcji usługi RemoteApp poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8d81b-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="8d81b-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="8d81b-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="8d81b-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="8d81b-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="8d81b-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="8d81b-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="8d81b-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="8d81b-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="8d81b-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="8d81b-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="8d81b-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="8d81b-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="8d81b-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="8d81b-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="8d81b-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="8d81b-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="8d81b-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="8d81b-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="8d81b-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="8d81b-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="8d81b-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="8d81b-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="8d81b-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="8d81b-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="8d81b-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="8d81b-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="8d81b-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="8d81b-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="8d81b-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="8d81b-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="8d81b-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="8d81b-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="8d81b-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="8d81b-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="8d81b-157">Polecenia cmdlet sieci wirtualnej usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="8d81b-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="8d81b-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="8d81b-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="8d81b-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="8d81b-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="8d81b-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="8d81b-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="8d81b-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="8d81b-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="8d81b-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="8d81b-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="8d81b-163">Get - AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="8d81b-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="8d81b-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="8d81b-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="8d81b-165">Polecenia cmdlet obrazu szablonu usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="8d81b-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="8d81b-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="8d81b-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="8d81b-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="8d81b-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="8d81b-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="8d81b-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="8d81b-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="8d81b-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="8d81b-170">Inne polecenia cmdlet usługi RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="8d81b-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="8d81b-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="8d81b-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="8d81b-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="8d81b-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="8d81b-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="8d81b-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="8d81b-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="8d81b-174">Get-AzureRemoteAppOperationResult</span></span>

