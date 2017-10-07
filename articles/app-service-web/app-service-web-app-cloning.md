---
title: "aaaWeb aplikacji klonowania przy użyciu programu PowerShell"
description: "Dowiedz się, jak tooclone aplikacje sieci Web toonew aplikacji sieci Web przy użyciu programu PowerShell."
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
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="5044e-103">Usługa aplikacji Azure aplikacji klonowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5044e-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="5044e-104">Hello wersji programu Microsoft Azure PowerShell z wersji 1.1.0 nową opcję został dodany AzureRMWebApp tooNew, która pozwoli uzyskać hello użytkownika hello możliwości tooclone istniejącej aplikacji tooa nowo utworzona aplikacja sieci Web w innym regionie lub hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="5044e-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="5044e-105">Spowoduje to włączenie toodeploy klientów liczba aplikacji w różnych regionach, szybkie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="5044e-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="5044e-106">Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium.</span><span class="sxs-lookup"><span data-stu-id="5044e-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="5044e-107">Hello nowej używa funkcji hello takie same ograniczenia co funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="5044e-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="5044e-108">toolearn dotyczące korzystania z usługi Azure Resource Manager toomanage poleceń cmdlet programu PowerShell systemu Azure na podstawie wyboru Twojej aplikacji sieci Web [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="5044e-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="5044e-109">Klonowanie istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5044e-109">Cloning an existing App</span></span>
<span data-ttu-id="5044e-110">Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, hello użytkownika ma zostać tooclone hello zawartość tooa nowej aplikacji sieci web w regionie północno-środkowe Stany.</span><span class="sxs-lookup"><span data-stu-id="5044e-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="5044e-111">Można to zrobić przy użyciu wersji usługi Azure Resource Manager hello toocreate polecenia cmdlet programu PowerShell hello nowej aplikacji sieci web z opcją - SourceWebApp hello.</span><span class="sxs-lookup"><span data-stu-id="5044e-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="5044e-112">Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć hello następujące informacje o aplikacji programu PowerShell polecenie tooget hello źródła sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):</span><span class="sxs-lookup"><span data-stu-id="5044e-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="5044e-113">toocreate planu usługi aplikacji, możemy użyć polecenia New-AzureRmAppServicePlan jak hello poniższy przykład</span><span class="sxs-lookup"><span data-stu-id="5044e-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="5044e-114">Za pomocą polecenia hello AzureRmWebApp nowy, możemy Utwórz nową aplikację sieci web hello w hello północno-środkowe Stany i powiązanie jej tooan istniejące warstwy premium planu usługi App Service, Ponadto możemy użyć hello zasobów w tej samej grupy jako hello źródłowej aplikacji sieci web lub zdefiniuj nową grupę zasobów , następujące hello wykaże, że:</span><span class="sxs-lookup"><span data-stu-id="5044e-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="5044e-115">tooclone istniejącą aplikację sieci web w tym wszystkich miejsc wdrożenia skojarzony, hello użytkownik będzie musiał toouse hello parametru IncludeSourceWebAppSlots, hello następującego polecenia programu PowerShell pokazuje hello Użyj tego parametru z hello polecenia New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="5044e-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="5044e-116">tooclone istniejącą aplikację sieci web w obrębie hello tego samego regionu hello użytkownik będzie musiał toocreate plan w hello nową grupę zasobów i nowej usługi aplikacji tego samego regionu, a następnie za pomocą hello następujących aplikacji sieci web hello tooclone polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5044e-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="5044e-117">Klonowanie tooan aplikacji istniejącego środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="5044e-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="5044e-118">Scenariusz: Istniejącej aplikacji sieci web w regionie południowo-środkowe stany, hello użytkownika ma zostać tooclone hello zawartość tooa nowej sieci web aplikacji tooan istniejącego środowiska usługi aplikacji (ASE).</span><span class="sxs-lookup"><span data-stu-id="5044e-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="5044e-119">Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć hello następujące informacje o aplikacji programu PowerShell polecenie tooget hello źródła sieci web (w tym przypadku o nazwie aplikacji sieci Web źródła):</span><span class="sxs-lookup"><span data-stu-id="5044e-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="5044e-120">Wiedzy o nazwie hello ASE oraz nazwa grupy zasobów hello hello ASE należącą do, hello użytkownik może użyć polecenia hello nowy AzureRmWebApp toocreate hello nowej aplikacji sieci web w hello istniejących ASE powitania po wykaże, że:</span><span class="sxs-lookup"><span data-stu-id="5044e-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="5044e-121">Parametr lokalizacja Hello jest wymagany powodu Przyczyna toolegacy, ale w przypadku tworzenia aplikacji w elemencie ASE hello zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="5044e-122">Klonowanie istniejącego miejsca aplikacji</span><span class="sxs-lookup"><span data-stu-id="5044e-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="5044e-123">Scenariusz: hello użytkownika ma zostać tooclone istniejących tooeither miejsca aplikacji sieci Web nowej aplikacji sieci Web lub nowe miejsce aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5044e-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="5044e-124">Hello w hello nowej aplikacji sieci Web może być tym samym regionie jako hello oryginalnego miejsca aplikacji sieci Web lub w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="5044e-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="5044e-125">Znajomość hello zasobów nazwy grupy, która zawiera hello źródłowej aplikacji sieci web, możemy użyć następującego polecenia programu PowerShell informacji tooget hello źródła miejsca aplikacji sieci web firmy (w tym przypadku o nazwie webappslot źródła) powiązane tooWeb aplikacji źródła-aplikacji sieci Web hello:</span><span class="sxs-lookup"><span data-stu-id="5044e-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="5044e-126">Hello poniżej przedstawiono utworzenie klona hello źródła sieci web aplikacji tooa nowej aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="5044e-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="5044e-127">Konfigurowanie usługi Traffic Manager podczas klonowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="5044e-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="5044e-128">Tworzenie aplikacji sieci web w przypadku i konfigurowanie usługi Azure Traffic Manager tooroute ruchu tooall tych aplikacji sieci web, jest tooinsure n ważne, będące aplikacji klientów wysokiej dostępności w przypadku klonowania istniejącej aplikacji sieci web, do których masz hello tooconnect opcji zarówno w sieci web aplikacje tooeither nowego profilu Menedżera ruchu lub istniejącego — Pamiętaj, że tylko wersja usługi Azure Resource Manager z Menedżera ruchu jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="5044e-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="5044e-129">Tworzenie nowego profilu Menedżera ruchu podczas klonowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="5044e-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="5044e-130">Scenariusz: hello użytkownika ma zostać tooclone tooanother region aplikacji sieci web podczas konfigurowania profilu Menedżera ruchu usługi Azure Resource Manager, który obejmuje zarówno aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5044e-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="5044e-131">Hello poniżej przedstawiono tworzenie Sklonowanie hello źródła sieci web aplikacji tooa nowej aplikacji sieci web podczas konfigurowania profilu Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="5044e-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="5044e-132">Dodawanie nowych sklonowany aplikacji sieci Web tooan istniejącego profilu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="5044e-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="5044e-133">Scenariusz: hello użytkownik ma już profil Menedżera ruchu usługi Azure Resource Manager czy chciałby tooadd zarówno w sieci web aplikacji jako punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="5044e-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="5044e-134">toodo tak, najpierw musimy tooassemble hello istniejący identyfikator profilu Menedżera ruchu, potrzebujemy hello identyfikator subskrypcji, nazwa grupy zasobów i nazwa profilu Menedżera ruchu hello istniejących.</span><span class="sxs-lookup"><span data-stu-id="5044e-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="5044e-135">Po identyfikatorze Menedżera ruchu hello, hello poniżej przedstawiono tworzenia klonu hello źródła sieci web aplikacji tooa nowej aplikacji sieci web podczas dodawania ich tooan istniejącego profilu Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="5044e-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="5044e-136">Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="5044e-136">Current Restrictions</span></span>
<span data-ttu-id="5044e-137">Ta funkcja jest obecnie w wersji zapoznawczej, pracujemy nad tooadd nowe funkcje w czasie, następujące listy hello są hello znane ograniczenia dotyczące hello bieżącej wersji w klonowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5044e-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="5044e-138">Ustawienia skalowania automatycznego nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="5044e-139">Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="5044e-140">Ustawienia sieci Wirtualnej nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="5044e-141">Wgląd w aplikację nie są automatycznie skonfigurowane w aplikacji sieci web docelowym hello</span><span class="sxs-lookup"><span data-stu-id="5044e-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="5044e-142">Łatwe ustawienia uwierzytelniania nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="5044e-143">Program kudu rozszerzenia nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="5044e-144">Porada reguły nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="5044e-145">Baza danych zawartości nie są klonowane.</span><span class="sxs-lookup"><span data-stu-id="5044e-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="5044e-146">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="5044e-146">References</span></span>
* [<span data-ttu-id="5044e-147">Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="5044e-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="5044e-148">Klonowanie aplikacji sieci Web przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5044e-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="5044e-149">Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5044e-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="5044e-150">Usługa Azure Resource Manager obsługę Azure Traffic Manager w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="5044e-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="5044e-151">Wprowadzenie tooApp środowiska usługi</span><span class="sxs-lookup"><span data-stu-id="5044e-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="5044e-152">Używanie programu Azure PowerShell z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5044e-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

