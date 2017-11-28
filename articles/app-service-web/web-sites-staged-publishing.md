---
title: "aaaSet się przemieszczania środowiska dla aplikacji sieci web w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse przemieszczane publikowania dla aplikacji sieci web w usłudze Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="07084-103">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="07084-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="07084-104">Podczas wdrażania aplikację sieci web, aplikacji sieci web w systemie Linux, przenośne zaplecza i aplikacji interfejsu API za[usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714), można wdrożyć miejsce wdrożenia oddzielnych tooa zamiast miejsca produkcji domyślne hello podczas uruchamiania w hello **Standard**lub **Premium** tryb planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="07084-105">Miejsca wdrożenia są faktycznie na żywo aplikacji za pomocą ich własnych nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="07084-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="07084-106">Elementy zawartości i konfiguracji aplikacji może być zamieniona między dwóch miejsc wdrożenia, w tym hello miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="07084-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="07084-107">Wdrażanie przedział czasu wdrożenia tooa aplikacji ma hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="07084-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="07084-108">Zmiany przemieszczania miejsce wdrożenia aplikacji może sprawdzać przed zamienienie go z miejscem produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="07084-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="07084-109">Najpierw wdrażania miejsca tooa aplikacji i zamienienie go w środowisku produkcyjnym gwarantuje, że wszystkie wystąpienia miejsca hello są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="07084-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="07084-110">Eliminuje to czas przestoju, podczas wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="07084-111">przekierowywanie ruchu Hello jest łatwego i żadne żądania są usuwane w wyniku operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="07084-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="07084-112">Ta całego przepływu pracy można zautomatyzować poprzez skonfigurowanie [automatycznej wymiany](#Auto-Swap) podczas weryfikacji przed wymiany nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="07084-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="07084-113">Po wymiany hello gniazda z wcześniej przygotowanych aplikacji ma hello poprzedniej aplikacji produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="07084-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="07084-114">Jeśli zmiany hello miejscami do miejsca produkcji hello są niezgodne z oczekiwaniami, możesz wykonać powitalne sam zamiana natychmiast utworzyć kopię tooget "ostatniej znanej dobrej witryny".</span><span class="sxs-lookup"><span data-stu-id="07084-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="07084-115">Każdego trybu planu usługi aplikacji obsługuje różne liczby miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="07084-116">obsługuje tryb aplikacji toofind hello liczbę miejsc, zobacz [App Service — ceny](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="07084-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="07084-117">Gdy aplikacja ma wiele miejsc, nie można zmienić trybu hello.</span><span class="sxs-lookup"><span data-stu-id="07084-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="07084-118">Skalowanie jest niedostępna dla gniazda nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="07084-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="07084-119">Zarządzanie połączonego zasobu nie jest obsługiwane dla gniazda nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="07084-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="07084-120">W hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) , można uniknąć ten potencjalny wpływ na gnieździe produkcyjnym przenosząc tymczasowo hello miejsca nieprodukcyjnych tooa różnych aplikacji planu tryb usługi.</span><span class="sxs-lookup"><span data-stu-id="07084-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="07084-121">Uwaga gniazdo nieprodukcyjnych hello ponownie udostępnić hello tego samego trybu z miejscem produkcyjnym hello przed można zamienić miejsc hello dwa.</span><span class="sxs-lookup"><span data-stu-id="07084-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="07084-122">Dodaj miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-122">Add a deployment slot</span></span>
<span data-ttu-id="07084-123">Aplikacja Hello musi być uruchomiona w hello **standardowe** lub **Premium** trybu w kolejności dla tooenable możesz wielu miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="07084-124">W hello [Azure Portal](https://portal.azure.com/), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="07084-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="07084-125">Wybierz hello **miejsc wdrożenia** opcji, a następnie kliknij przycisk **Dodaj miejsce**.</span><span class="sxs-lookup"><span data-stu-id="07084-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Dodaj nowe miejsce wdrożenia][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="07084-127">Jeśli aplikacja hello nie jest już hello **standardowe** lub **Premium** tryb, zostanie wyświetlony komunikat informujący o włączenie publikowania przemieszczanego tryby hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="07084-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="07084-128">W tym momencie masz hello opcja tooselect **uaktualnienia** i przejdź toohello **skali** kartę aplikacji przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="07084-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="07084-129">W hello **dodać gniazdo** bloku, nadaj nazwę hello miejsca i wybierz czy tooclone konfiguracji aplikacji z innego istniejącego miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="07084-130">Kliknij przycisk hello toocontinue znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="07084-130">Click hello check mark toocontinue.</span></span>
   
    ![Źródło konfiguracji][ConfigurationSource1]
   
    <span data-ttu-id="07084-132">Hello po raz pierwszy Dodaj miejsce, będziesz korzystać tylko z dwóch opcji: klonowania konfiguracji z gniazda domyślne hello w środowisku produkcyjnym lub w ogóle.</span><span class="sxs-lookup"><span data-stu-id="07084-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="07084-133">Po utworzeniu miejsc kilka będą mogli tooclone konfiguracji z miejsca niż jeden hello w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="07084-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Konfiguracja źródła][MultipleConfigurationSources]
4. <span data-ttu-id="07084-135">W bloku zasobów aplikacji, kliknij przycisk **miejsc wdrożenia**, kliknij przycisk tooopen miejsca wdrożenia bloku zasobów z miejsca, przy użyciu zestawu metryki i konfiguracji, tak jak każda inna aplikacja.</span><span class="sxs-lookup"><span data-stu-id="07084-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="07084-136">Hello nazwa miejsca hello jest wyświetlany u góry hello tooremind bloku hello możesz przeglądanym hello miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Tytuł miejsca wdrożenia][StagingTitle]
5. <span data-ttu-id="07084-138">Kliknij adres URL aplikacji hello w bloku hello miejsca.</span><span class="sxs-lookup"><span data-stu-id="07084-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="07084-139">Miejsce wdrożenia hello powiadomienie ma własną nazwę hosta i jest również aktywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="07084-140">miejsce wdrożenia toohello dostępu publicznego toolimit, zobacz [aplikacji sieci Web usługi aplikacji — miejsc wdrożenia produkcyjnego toonon dostępu do sieci web bloku](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="07084-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="07084-141">Brak zawartości po utworzeniu miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="07084-142">Można wdrożyć toohello gniazda z gałęzi repozytorium różnych lub całkowicie innego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="07084-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="07084-143">Można również zmienić konfiguracji hello miejsca.</span><span class="sxs-lookup"><span data-stu-id="07084-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="07084-144">Użyj hello publikowania profilu lub wdrożenia poświadczeń skojarzonych z hello miejsce wdrożenia aktualizacji zawartości.</span><span class="sxs-lookup"><span data-stu-id="07084-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="07084-145">Można na przykład [Opublikuj gnieździe toothis za pomocą narzędzia git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="07084-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="07084-146">Konfiguracja dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-146">Configuration for deployment slots</span></span>
<span data-ttu-id="07084-147">Gdy Klonuj konfiguracji z innego miejsca wdrożenia, konfiguracja sklonowany hello jest można edytować.</span><span class="sxs-lookup"><span data-stu-id="07084-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="07084-148">Ponadto niektóre elementy konfiguracji będzie śledzić hello zawartości między swap (nie gniazdo określonych), podczas gdy inne elementy konfiguracji, pozostanie na powitania sam gniazdo po swap (gniazdo określonych).</span><span class="sxs-lookup"><span data-stu-id="07084-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="07084-149">Witaj następujące przedstawiono konfigurację hello ulegnie zmianie po zamienić miejsc.</span><span class="sxs-lookup"><span data-stu-id="07084-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="07084-150">**Ustawienia, które są zamienione**:</span><span class="sxs-lookup"><span data-stu-id="07084-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="07084-151">Ustawienia ogólne — takie jak gniazda sieci Web 32/64-bitowych wersji framework</span><span class="sxs-lookup"><span data-stu-id="07084-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="07084-152">Ustawienia aplikacji (może być skonfigurowany toostick tooa miejsca)</span><span class="sxs-lookup"><span data-stu-id="07084-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="07084-153">Parametry połączenia (może być skonfigurowany toostick tooa miejsca)</span><span class="sxs-lookup"><span data-stu-id="07084-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="07084-154">Mapowania programu obsługi</span><span class="sxs-lookup"><span data-stu-id="07084-154">Handler mappings</span></span>
* <span data-ttu-id="07084-155">Ustawienia monitorowania i diagnostyki</span><span class="sxs-lookup"><span data-stu-id="07084-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="07084-156">Zawartość zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="07084-156">WebJobs content</span></span>

<span data-ttu-id="07084-157">**Ustawienia, które nie są zamienione**:</span><span class="sxs-lookup"><span data-stu-id="07084-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="07084-158">Publikowanie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="07084-158">Publishing endpoints</span></span>
* <span data-ttu-id="07084-159">Niestandardowa nazwa domeny</span><span class="sxs-lookup"><span data-stu-id="07084-159">Custom Domain Names</span></span>
* <span data-ttu-id="07084-160">Certyfikaty SSL i powiązań</span><span class="sxs-lookup"><span data-stu-id="07084-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="07084-161">Ustawienia skali</span><span class="sxs-lookup"><span data-stu-id="07084-161">Scale settings</span></span>
* <span data-ttu-id="07084-162">Planiści zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="07084-162">WebJobs schedulers</span></span>

<span data-ttu-id="07084-163">tooconfigure połączenie lub ustawienie ciągu toostick tooa miejsca aplikacji (nie miejscami), dostęp hello **ustawienia aplikacji** bloku do określonego miejsca, a następnie wybierz hello **ustawienie miejsca** pole hello elementy konfiguracji, które powinny trzymaj hello miejsca.</span><span class="sxs-lookup"><span data-stu-id="07084-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="07084-164">Należy pamiętać, że oznaczenie element konfiguracji jako miejsca określonego ma wpływ hello ustanowienie tego elementu jako nie swappable wszystkich miejsc wdrożenia hello skojarzone z aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="07084-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Ustawienia gniazda][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="07084-166">Zamienić miejsc wdrażania</span><span class="sxs-lookup"><span data-stu-id="07084-166">Swap deployment slots</span></span> 
<span data-ttu-id="07084-167">Można zamienić miejsc wdrożenia w hello **omówienie** lub **miejsc wdrożenia** widok bloku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07084-168">Przed możesz zamienić aplikację z miejsce wdrożenia do środowiska produkcyjnego, upewnij się, że wszystkie z systemem innym niż miejsce określone ustawienia są skonfigurowane zgodnie z oczekiwaniami toohave go w celu wymiany hello.</span><span class="sxs-lookup"><span data-stu-id="07084-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="07084-169">tooswap miejsc wdrożenia, kliknij przycisk hello **wymiany** przycisk na pasku poleceń hello aplikacji hello lub na pasku poleceń hello miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Przycisk wymiany][SwapButtonBar]

2. <span data-ttu-id="07084-171">Upewnij się, że kierowanych źródła i wymiany wymiany hello są poprawnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="07084-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="07084-172">Zazwyczaj obiekt docelowy wymiany hello jest hello miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="07084-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="07084-173">Kliknij przycisk **OK** toocomplete hello operacji.</span><span class="sxs-lookup"><span data-stu-id="07084-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="07084-174">Po zakończeniu działania hello zostały zamieniono hello miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Ukończ zamianę](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="07084-176">Dla hello **zamiany z podglądem** wymiany typu, zobacz [zamiany z podglądem (faza wielu wymiany)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="07084-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="07084-177">Zamiana z podglądem (faza wielu wymiany)</span><span class="sxs-lookup"><span data-stu-id="07084-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="07084-178">Zamiany z podglądem lub wielu faza wymiany uprościć weryfikacji konfiguracji specyficznych dla miejsca elementów, takich jak parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="07084-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="07084-179">W przypadku obciążeń krytycznym mają toovalidate, która aplikacja hello działa zgodnie z oczekiwaniami, po zastosowaniu konfiguracji gniazda produkcyjnego hello i należy wykonać takie weryfikacji *przed* aplikacji hello jest zamieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="07084-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="07084-180">Zamiany z podglądem jest, co jest potrzebne.</span><span class="sxs-lookup"><span data-stu-id="07084-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="07084-181">Zamiany z podglądem jest nieobsługiwana w aplikacjach sieci web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="07084-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="07084-182">Jeśli używasz hello **zamiana z podglądem** opcji (zobacz [zamienić miejsc wdrożenia](#Swap)), usługi aplikacji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="07084-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="07084-183">Nie ma wpływu na przechowuje hello docelowego miejsca niezmienione tak istniejących obciążenie gniazdo (np. produkcja).</span><span class="sxs-lookup"><span data-stu-id="07084-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="07084-184">Dotyczy elementów konfiguracji hello hello miejsca toohello źródła miejsca docelowego, w tym parametry połączenia specyficzne dla miejsca hello i ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="07084-185">Uruchamia ponownie hello procesów roboczych na powitania miejsca źródłowego przy użyciu tych elementów konfiguracji wyżej.</span><span class="sxs-lookup"><span data-stu-id="07084-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="07084-186">Po zakończeniu wymiany hello: miejsca źródłowego wstępnie przygotowany warmed up hello przenosi do miejsca docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="07084-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="07084-187">miejsca docelowego Hello jest przenoszony do miejsca źródłowego hello jak ręczne wymiany.</span><span class="sxs-lookup"><span data-stu-id="07084-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="07084-188">Jeśli anulujesz wymiany hello: ponowne zastosowanie hello elementy konfiguracji z miejsca źródłowego toohello hello źródła miejsca.</span><span class="sxs-lookup"><span data-stu-id="07084-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="07084-189">Można przejrzeć, dokładnie tak jak aplikacji hello będzie się odbywać z konfiguracją hello z miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="07084-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="07084-190">Po ukończeniu sprawdzania poprawności zakończeniu wymiany hello w osobnym kroku.</span><span class="sxs-lookup"><span data-stu-id="07084-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="07084-191">Ten krok ma hello dodatkową zaletę hello jest już przygotowaniu miejsca źródłowego z odpowiednią konfiguracją hello, czy klienci nie będzie działać z żadnych przestojów.</span><span class="sxs-lookup"><span data-stu-id="07084-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="07084-192">Przykłady dotyczące hello poleceń cmdlet programu Azure PowerShell dostępne dla wielu faza wymiany znajdują się w hello poleceń cmdlet programu PowerShell systemu Azure dla sekcji miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="07084-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="07084-193">Konfigurowanie automatycznej wymiany (MB)</span><span class="sxs-lookup"><span data-stu-id="07084-193">Configure Auto Swap</span></span>
<span data-ttu-id="07084-194">Automatycznej wymiany usprawnia DevOps scenariuszy, w którym ma toocontinuously wdrażania aplikacji za pomocą zero zimny start i przestojów dla klientów końcowych aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="07084-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="07084-195">Jeśli miejsce wdrożenia jest skonfigurowany do automatycznej wymiany do produkcji, zawsze push Twoje miejsce toothat aktualizacji kodu, usługi aplikacji — automatycznie wymiany aplikacji hello w środowisku produkcyjnym po już ma przygotowaniu miejsca w gnieździe hello.</span><span class="sxs-lookup"><span data-stu-id="07084-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07084-196">Po włączeniu automatycznej wymiany dla miejsca, upewnij się, że konfiguracja miejsca hello jest dokładnie hello konfiguracji przeznaczonych dla miejsca docelowego hello (zazwyczaj hello gniazda produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="07084-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="07084-197">Automatycznej wymiany nie jest obsługiwana w aplikacjach sieci web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="07084-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="07084-198">Konfigurowanie automatycznej wymiany gnieździe jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="07084-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="07084-199">Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="07084-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="07084-200">W **miejsc wdrożenia**, a następnie wybierz gniazdo nieprodukcyjnych i wybierz **ustawienia aplikacji** w bloku zasobów z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="07084-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="07084-201">Wybierz **na** dla **automatycznej wymiany**, wybierz pozycję gniazda docelowy hello **automatycznej wymiany miejsca**i kliknij przycisk **zapisać** na pasku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="07084-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="07084-202">Upewnij się, że konfiguracja miejsca hello jest dokładnie hello konfiguracji przeznaczonych dla miejsca docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="07084-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="07084-203">Witaj **powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="07084-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="07084-204">tootest automatycznej wymiany dla aplikacji, należy najpierw zaznaczyć gnieździe docelowym nieprodukcyjnych **automatycznej wymiany miejsca** toobecome zapoznać się z funkcją hello.</span><span class="sxs-lookup"><span data-stu-id="07084-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="07084-205">Wykonanie miejsca wdrożenia toothat wypychania kodu.</span><span class="sxs-lookup"><span data-stu-id="07084-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="07084-206">Automatycznej wymiany nastąpi po pewnym czasie, a aktualizacja hello zostaną odzwierciedlone pod adresem URL z miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="07084-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="07084-207">toorollback aplikacji produkcyjnej po wymiany</span><span class="sxs-lookup"><span data-stu-id="07084-207">toorollback a production app after swap</span></span>
<span data-ttu-id="07084-208">Jeśli błędy są identyfikowane w środowisku produkcyjnym po zakończeniu wymiany gniazd, wdrażanie miejsc hello stanów wstępne wymiany tootheir wstecz przez zamianę natychmiast hello tego samego dwóch miejsc.</span><span class="sxs-lookup"><span data-stu-id="07084-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="07084-209">Niestandardowe rozgrzewania przed wymiany</span><span class="sxs-lookup"><span data-stu-id="07084-209">Custom warm-up before swap</span></span>
<span data-ttu-id="07084-210">Niektóre aplikacje mogą wymagać akcje niestandardowe rozgrzewania.</span><span class="sxs-lookup"><span data-stu-id="07084-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="07084-211">Witaj `applicationInitialization` umożliwia element konfiguracji w pliku web.config można toospecify niestandardową inicjalizację akcje toobe wykonać zanim żądanie zostanie odebrane.</span><span class="sxs-lookup"><span data-stu-id="07084-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="07084-212">Operacja zamiany Hello będzie oczekiwał na ten toocomplete rozgrzewania niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="07084-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="07084-213">Oto przykładowe fragment pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="07084-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="07084-214">toodelete miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-214">toodelete a deployment slot</span></span>
<span data-ttu-id="07084-215">W bloku hello miejsce wdrożenia, miejsce wdrożenia Otwórz hello bloku, kliknij przycisk **omówienie** (hello domyślnej strony) i kliknij przycisk **usunąć** na pasku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="07084-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Usuń miejsce wdrożenia][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="07084-217">Polecenia cmdlet programu PowerShell systemu Azure dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="07084-218">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą środowiska Windows PowerShell, włącznie z obsługą zarządzania miejsc wdrożenia w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="07084-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="07084-219">Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, a na uwierzytelniania programu Azure PowerShell z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07084-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="07084-220">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="07084-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="07084-221">Tworzenie miejsca wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="07084-222">Zainicjuj wymiany z przeglądem (faza wielu wymiany) i zastosować gniazda toosource konfiguracji miejsca docelowego</span><span class="sxs-lookup"><span data-stu-id="07084-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="07084-223">Anuluj oczekująca zamiana (obszar wymiany z przeglądem) i przywracanie konfiguracji miejsca źródłowego</span><span class="sxs-lookup"><span data-stu-id="07084-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="07084-224">Zamienić miejsc wdrażania</span><span class="sxs-lookup"><span data-stu-id="07084-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="07084-225">Usuń miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="07084-226">Azure polecenia interfejsu wiersza polecenia (Azure CLI) dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07084-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="07084-227">Hello interfejsu wiersza polecenia Azure udostępnia polecenia i platform do pracy z platformą Azure, w tym obsługę zarządzania miejsc wdrożenia usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07084-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="07084-228">Aby uzyskać instrukcje dotyczące instalowania i konfigurowania hello Azure CLI, wraz z informacjami na temat tooconnect interfejsu wiersza polecenia Azure tooyour subskrypcji platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07084-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="07084-229">Wywołanie polecenia hello toolist dostępne dla usługi Azure App Service w hello Azure CLI `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="07084-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="07084-230">Dla [Azure CLI 2.0](https://github.com/Azure/azure-cli) poleceń dla miejsc wdrożenia, zobacz [miejsce wdrożenia sieci web appservice az](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="07084-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="07084-231">Lista witryn platformy Azure</span><span class="sxs-lookup"><span data-stu-id="07084-231">azure site list</span></span>
<span data-ttu-id="07084-232">Informacje o aplikacji hello w bieżącej subskrypcji hello, można wywołać **listy witryn azure**w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="07084-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="07084-233">Tworzenie usługi Azure site</span><span class="sxs-lookup"><span data-stu-id="07084-233">azure site create</span></span>
<span data-ttu-id="07084-234">Wywołanie toocreate miejsce wdrożenia, **Tworzenie usługi azure site** i określ nazwę istniejącej aplikacji hello oraz nazwę hello hello toocreate miejsca, tak jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="07084-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="07084-235">tooenable kontroli źródła dla hello nowe miejsce, użyj hello **— git** opcja tak jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="07084-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="07084-236">usługi Azure site wymiany (MB)</span><span class="sxs-lookup"><span data-stu-id="07084-236">azure site swap</span></span>
<span data-ttu-id="07084-237">toomake hello aplikacji produkcyjnej hello miejsca wdrażania aktualizacji, użyj hello **wymiany usługi azure site** tooperform polecenia operację zamiany, tak jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="07084-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="07084-238">aplikacji produkcyjnej Hello nie będą występować dowolne czas przestoju, nie zostaną poddane zimny start.</span><span class="sxs-lookup"><span data-stu-id="07084-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="07084-239">Usuwanie witryny platformy Azure</span><span class="sxs-lookup"><span data-stu-id="07084-239">azure site delete</span></span>
<span data-ttu-id="07084-240">toodelete miejsce wdrożenia, która nie jest już konieczne Użyj hello **usuwanie witryny azure** poleceń, tak jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="07084-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="07084-241">Zobacz działającą aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="07084-241">See a web app in action.</span></span> <span data-ttu-id="07084-242">[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) natychmiast i tej utworzyć początkową aplikację — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="07084-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="07084-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07084-243">Next Steps</span></span>
<span data-ttu-id="07084-244">[Usługa Azure App Service aplikacji sieci Web — Blokuj miejsc wdrożenia produkcyjnego toonon dostępu do sieci web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp wprowadzenie usługi w systemie Linux](./app-service-linux-intro.md)
[bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="07084-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

