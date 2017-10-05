---
title: "Klonowanie aplikacji sieci Web przy użyciu programu PowerShell"
description: "Dowiedz się, jak klonowanie aplikacji sieci Web do nowej aplikacji sieci Web przy użyciu programu PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="b1543-103">Usługa aplikacji Azure aplikacji klonowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1543-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="b1543-104">Wraz z wydaniem programu Microsoft Azure PowerShell w wersji 1.1.0 AzureRMWebApp nowy, która pozwoli uzyskać użytkownika klonowanie istniejącą aplikację sieci Web do aplikacji nowo utworzonej w innym regionie lub w tym samym regionie dodano nową opcję.</span><span class="sxs-lookup"><span data-stu-id="b1543-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="b1543-105">Umożliwi to klienci mogą wdrożyć wiele aplikacji w różnych regionach, szybkie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="b1543-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="b1543-106">Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium.</span><span class="sxs-lookup"><span data-stu-id="b1543-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="b1543-107">Nowa funkcja używa tego samego ograniczenia jako funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b1543-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="b1543-108">Aby dowiedzieć się więcej o korzystaniu z poleceń cmdlet programu Azure PowerShell do zarządzania wyboru Twojej aplikacji sieci Web na podstawie usługi Azure Resource Manager [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b1543-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="b1543-109">Klonowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1543-109">Cloning an existing App</span></span>
<span data-ttu-id="b1543-110">Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, użytkownik chce klonowania zawartości do nowej aplikacji sieci web w regionie północno-środkowe Stany.</span><span class="sxs-lookup"><span data-stu-id="b1543-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="b1543-111">Można to zrobić za pomocą polecenia cmdlet programu PowerShell za pośrednictwem usługi Azure Resource Manager do tworzenia nowej aplikacji sieci web z opcją - SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="b1543-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="b1543-112">Znajomość Nazwa grupy zasobów, która zawiera źródłowej aplikacji sieci web, możemy użyć następującego polecenia programu PowerShell można uzyskać informacji o źródłowej aplikacji sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):</span><span class="sxs-lookup"><span data-stu-id="b1543-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="b1543-113">Aby utworzyć nowy Plan usługi App Service, możemy użyć polecenia New-AzureRmAppServicePlan jak w poniższym przykładzie</span><span class="sxs-lookup"><span data-stu-id="b1543-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="b1543-114">Za pomocą polecenia New-AzureRmWebApp, możemy utworzyć nowej aplikacji sieci web w regionie północno-środkowe Stany i powiązanie jej istniejące warstwy premium planu usługi App Service, Ponadto możemy użyć tej samej grupy zasobów jako źródłowej aplikacji sieci web lub zdefiniuj nową grupę zasobów, pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="b1543-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="b1543-115">Klonowanie istniejącej aplikacji sieci web, w tym wszystkie skojarzone wdrażania gniazd, użytkownik będzie musiał użyć parametru IncludeSourceWebAppSlots następującego polecenia programu PowerShell pokazuje, użyj tego parametru przy użyciu polecenia New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="b1543-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="b1543-116">Można sklonować istniejącą aplikację sieci web w tym samym regionie, użytkownik będzie musiał utworzyć nową grupę zasobów i nowej usługi aplikacji planu w tym samym regionie, a następnie za pomocą następującego polecenia programu PowerShell na potrzeby klonowania aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b1543-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="b1543-117">Klonowanie istniejącej aplikacji do środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1543-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="b1543-118">Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, użytkownik chce klonowania zawartości do nowej aplikacji sieci web do istniejącej aplikacji usługi środowiska (ASE).</span><span class="sxs-lookup"><span data-stu-id="b1543-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="b1543-119">Znajomość Nazwa grupy zasobów, która zawiera źródłowej aplikacji sieci web, możemy użyć następującego polecenia programu PowerShell można uzyskać informacji o źródłowej aplikacji sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):</span><span class="sxs-lookup"><span data-stu-id="b1543-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="b1543-120">Znajomość ASE nazwy i nazwy grupy zasobów, której należy ASE, użytkownik może użyć polecenia New-AzureRmWebApp, aby utworzyć nową aplikację sieci web w istniejącej ASE, pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="b1543-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="b1543-121">Parametr lokalizacja jest wymagana powodu starszej wersji, ale w przypadku tworzenia aplikacji w elemencie ASE zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="b1543-122">Klonowanie istniejącego miejsca aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1543-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="b1543-123">Scenariusz: Użytkownik chce klonowania istniejącego miejsca aplikacji sieci Web albo w nowej aplikacji sieci Web lub nowe miejsce aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b1543-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="b1543-124">W nowej aplikacji sieci Web może być w tym samym regionie co oryginalna miejsca aplikacji sieci Web lub w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="b1543-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="b1543-125">Znajomość Nazwa grupy zasobów, która zawiera źródłowej aplikacji sieci web, możemy użyć następującego polecenia programu PowerShell można uzyskać informacji o miejsca aplikacji sieci web źródła (w tym przypadku o nazwie webappslot źródła) związana z aplikacji sieci Web aplikacji sieci Web źródła:</span><span class="sxs-lookup"><span data-stu-id="b1543-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="b1543-126">Poniżej przedstawiono tworzenie własnego klonu źródłowej aplikacji sieci web nowej aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="b1543-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="b1543-127">Konfigurowanie usługi Traffic Manager podczas klonowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1543-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="b1543-128">Tworzenie aplikacji sieci web w przypadku i konfigurowanie usługi Azure Traffic Manager można kierować ruchem do tych aplikacji sieci web, jest n scenariusza ważne, aby upewnić się, że aplikacje klientów są wysokiej dostępności, w przypadku klonowania istniejącej aplikacji sieci web należy opcję, aby połączyć obie aplikacje sieci web z nowego profilu Menedżera ruchu lub istniejącego - należy pamiętać, że tylko usługi Azure Resource Manager jest obsługiwana wersja usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="b1543-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="b1543-129">Tworzenie nowego profilu Menedżera ruchu podczas klonowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="b1543-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="b1543-130">Scenariusz: Użytkownik chce sklonować aplikacji sieci web do innego regionu, podczas konfigurowania profilu Menedżera ruchu usługi Azure Resource Manager, który obejmuje zarówno aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b1543-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="b1543-131">Poniżej przedstawiono tworzenie własnego klonu źródłowej aplikacji sieci web nowej aplikacji sieci web podczas konfigurowania profilu Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="b1543-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="b1543-132">Dodawanie nowych sklonować aplikacji sieci Web do istniejącego profilu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="b1543-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="b1543-133">Scenariusz: Użytkownik ma już profil Menedżera ruchu usługi Azure Resource Manager, które chciałby, aby dodać obie aplikacje sieci web jako punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b1543-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="b1543-134">Aby to zrobić, najpierw należy utworzyć istniejący identyfikator profilu Menedżera ruchu, są wymagane dla identyfikatora subskrypcji, nazwa grupy zasobów i istniejącej nazwy profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="b1543-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="b1543-135">Po identyfikatorze Menedżera ruchu, poniżej przedstawiono, tworzenie własnego klonu źródłowej aplikacji sieci web nowej aplikacji sieci web podczas dodawania ich do istniejącego profilu Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="b1543-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="b1543-136">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="b1543-136">Current Restrictions</span></span>
<span data-ttu-id="b1543-137">Ta funkcja jest obecnie w przeglądzie, pracujemy, aby dodać nowe funkcje w czasie, poniżej są znane ograniczenia dotyczące bieżącej wersji w klonowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b1543-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="b1543-138">Ustawienia skalowania automatycznego nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="b1543-139">Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="b1543-140">Ustawienia sieci Wirtualnej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="b1543-141">Wgląd w aplikację nie są automatycznie skonfigurowane na docelowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b1543-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="b1543-142">Łatwe ustawienia uwierzytelniania nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="b1543-143">Program kudu rozszerzenia nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="b1543-144">Porada reguły nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="b1543-145">Baza danych zawartości nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="b1543-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="b1543-146">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="b1543-146">References</span></span>
* [<span data-ttu-id="b1543-147">Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="b1543-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="b1543-148">Klonowanie aplikacji sieci Web przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b1543-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="b1543-149">Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b1543-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="b1543-150">Usługa Azure Resource Manager obsługę Azure Traffic Manager w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="b1543-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="b1543-151">Wprowadzenie do usługi App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b1543-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="b1543-152">Używanie programu Azure PowerShell z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1543-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

