---
title: "Zwróć uwagę, wycofywanie 1 rodziny aaaGuest systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Zawiera informacje na temat sposobu i sytuacji wystąpił wycofania hello 1 rodziny systemu operacyjnego gościa Azure toodetermine, jeśli ma wpływ"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="75ac1-103">Powiadomienie wycofanie 1 rodziny systemu operacyjnego gościa</span><span class="sxs-lookup"><span data-stu-id="75ac1-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="75ac1-104">najpierw ogłoszono Hello wycofanie 1 rodziny systemu operacyjnego na 1 czerwca 2013.</span><span class="sxs-lookup"><span data-stu-id="75ac1-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="75ac1-105">**2 września 2014** hello systemu operacyjnego gościa Azure (systemu operacyjnego gościa) rodziny 1.x, które jest oparte na systemie operacyjnym hello systemu Windows Server 2008, oficjalnie została wycofana.</span><span class="sxs-lookup"><span data-stu-id="75ac1-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="75ac1-106">Wszystkie próby toodeploy nowych usług lub uaktualniania istniejących usług przy użyciu 1 rodziny zakończy się niepowodzeniem z komunikatem o błędzie informujący, że hello się, że 1 rodziny systemu operacyjnego gościa został wycofany.</span><span class="sxs-lookup"><span data-stu-id="75ac1-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="75ac1-107">**3 listopada 2014 r.** zakończone rozszerzoną obsługę 1 rodziny systemu operacyjnego gościa i jest w pełni wycofane.</span><span class="sxs-lookup"><span data-stu-id="75ac1-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="75ac1-108">Wpłynie na wszystkie usługi nadal na 1 rodziny.</span><span class="sxs-lookup"><span data-stu-id="75ac1-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="75ac1-109">Może zatrzymać tych usług w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="75ac1-109">We may stop those services at any time.</span></span> <span data-ttu-id="75ac1-110">Nie ma żadnej gwarancji, że usługi będą nadal toorun, chyba że należy ręcznie uaktualnić je samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="75ac1-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="75ac1-111">Jeśli masz dodatkowe pytania, odwiedź stronę hello [fora usługi w chmurze](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) lub [skontaktuj się z pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="75ac1-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="75ac1-112">Możesz dotyczy?</span><span class="sxs-lookup"><span data-stu-id="75ac1-112">Are you affected?</span></span>
<span data-ttu-id="75ac1-113">Usługi w chmurze są uwzględnione w przypadku jednego z następujących hello warunków:</span><span class="sxs-lookup"><span data-stu-id="75ac1-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="75ac1-114">Ma wartość "rodziny systemów operacyjnych ="1"jawnie określone w pliku pliku ServiceConfiguration.cscfg powitania dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="75ac1-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="75ac1-115">Nie masz wartość dla rodziny systemów operacyjnych jawnie określone w pliku pliku ServiceConfiguration.cscfg powitania dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="75ac1-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="75ac1-116">Obecnie hello system używa hello domyślna wartość "1" w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="75ac1-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="75ac1-117">Witaj portalu Azure zawiera wartość rodziny System operacyjny gościa jako "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="75ac1-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="75ac1-118">toofind, które usługi w chmurze są uruchomione rodziny systemów operacyjnych, które można uruchomić hello następującego skryptu programu Azure PowerShell, ale należy [Konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) pierwszy.</span><span class="sxs-lookup"><span data-stu-id="75ac1-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="75ac1-119">Aby uzyskać więcej informacji na powitania skryptu, zobacz [Azure gościa systemu operacyjnego rodziny 1 End życia: czerwca 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="75ac1-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="75ac1-120">Usługi w chmurze wpłyną wycofanie 1 rodziny systemu operacyjnego, jeśli kolumna rodziny systemów operacyjnych hello w danych wyjściowych skryptu hello jest pusta lub zawiera wartość "1".</span><span class="sxs-lookup"><span data-stu-id="75ac1-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="75ac1-121">Zalecenia, jeśli ma wpływ</span><span class="sxs-lookup"><span data-stu-id="75ac1-121">Recommendations if you are affected</span></span>
<span data-ttu-id="75ac1-122">Firma Microsoft zaleca się, że migracja z tooone ról usługi w chmurze rodzin systemu operacyjnego gościa hello obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="75ac1-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="75ac1-123">**System operacyjny gościa rodziny 4.x** -Windows Server 2012 R2 *(zalecane)*</span><span class="sxs-lookup"><span data-stu-id="75ac1-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="75ac1-124">Upewnij się, że aplikacja korzysta z zestawu SDK 2.1 lub nowszej platformy .NET framework 4.0, 4.5 i 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="75ac1-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="75ac1-125">Witaj rodziny systemów operacyjnych atrybutu zbyt "4" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="75ac1-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="75ac1-126">**System operacyjny gościa rodziny 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="75ac1-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="75ac1-127">Upewnij się, że aplikacja korzysta z zestawu SDK 1,8 lub nowszej platformy .NET framework 4.0 lub 4.5.</span><span class="sxs-lookup"><span data-stu-id="75ac1-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="75ac1-128">Witaj rodziny systemów operacyjnych atrybutu zbyt "3" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="75ac1-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="75ac1-129">**System operacyjny gościa rodziny 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="75ac1-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="75ac1-130">Upewnij się, że aplikacja korzysta z zestawu SDK 1.3 i powyżej platformy .NET framework w wersji 3.5 lub 4.0.</span><span class="sxs-lookup"><span data-stu-id="75ac1-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="75ac1-131">Witaj rodziny systemów operacyjnych atrybutu zbyt "2" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="75ac1-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="75ac1-132">Rozszerzona obsługa 1 rodziny systemu operacyjnego gościa zakończył 3 listopada 2014 r.</span><span class="sxs-lookup"><span data-stu-id="75ac1-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="75ac1-133">Usługi w chmurze rodziny systemów operacyjnych gościa 1 nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="75ac1-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="75ac1-134">Migrowanie wyłączone rodziny 1, jak przerw w działaniu usługi tooavoid możliwe.</span><span class="sxs-lookup"><span data-stu-id="75ac1-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="75ac1-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="75ac1-135">Next steps</span></span>
<span data-ttu-id="75ac1-136">Przejrzyj hello najnowszych [wersje systemu operacyjnego gościa](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="75ac1-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
