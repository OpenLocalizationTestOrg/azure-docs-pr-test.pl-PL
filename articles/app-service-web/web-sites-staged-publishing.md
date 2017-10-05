---
title: "Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użyć przemieszczanego publikowania aplikacji sieci web w usłudze Azure App Service."
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
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="a0695-103">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="a0695-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="a0695-104">Podczas wdrażania aplikację sieci web, aplikacji sieci web w systemie Linux, przenośne zaplecza i aplikacji interfejsu API [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714), można wdrożyć na miejsce wdrożenia oddzielne zamiast domyślnego gniazda produkcyjnego podczas uruchamiania **standardowe** lub **Premium** tryb planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="a0695-105">Miejsca wdrożenia są faktycznie na żywo aplikacji za pomocą ich własnych nazwy hostów.</span><span class="sxs-lookup"><span data-stu-id="a0695-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="a0695-106">Elementy zawartości i konfiguracji aplikacji może być zamieniona między dwóch miejsc wdrożenia, w tym miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="a0695-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="a0695-107">Wdrażanie aplikacji w miejscu wdrożenia ma następujące zalety:</span><span class="sxs-lookup"><span data-stu-id="a0695-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="a0695-108">Zmiany przemieszczania miejsce wdrożenia aplikacji może sprawdzać przed zamienienie go z miejscem produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a0695-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="a0695-109">Wdrażanie aplikacji na gnieździe najpierw i zamienienie go w środowisku produkcyjnym gwarantuje, że wszystkie wystąpienia gniazda są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a0695-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="a0695-110">Eliminuje to czas przestoju, podczas wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="a0695-111">Przekierowywanie ruchu jest łatwego i żadne żądania są usuwane w wyniku operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="a0695-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="a0695-112">Ta całego przepływu pracy można zautomatyzować poprzez skonfigurowanie [automatycznej wymiany](#Auto-Swap) podczas weryfikacji przed wymiany nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="a0695-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="a0695-113">Po wymiany gniazda z wcześniej przygotowanych aplikacji ma poprzedniej aplikacji produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="a0695-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="a0695-114">Jeśli zmiany miejscami do miejsca produkcji są niezgodne z oczekiwaniami, można wykonać tego samego wymiany od razu do pobrania "ostatniej znanej dobrej witryny" ponownie.</span><span class="sxs-lookup"><span data-stu-id="a0695-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="a0695-115">Każdego trybu planu usługi aplikacji obsługuje różne liczby miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="a0695-116">Aby dowiedzieć się, liczba gniazd obsługuje tryb aplikacji, zobacz [App Service — ceny](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a0695-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="a0695-117">Gdy aplikacja ma wiele miejsc, nie można zmienić trybu.</span><span class="sxs-lookup"><span data-stu-id="a0695-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="a0695-118">Skalowanie jest niedostępna dla gniazda nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="a0695-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="a0695-119">Zarządzanie połączonego zasobu nie jest obsługiwane dla gniazda nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="a0695-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="a0695-120">W [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) , można uniknąć ten potencjalny wpływ na gnieździe produkcyjnym przenosząc tymczasowo nieprodukcyjnych miejsca do innego trybu planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="a0695-121">Należy pamiętać, że gniazdo nieprodukcyjnych ponownie muszą współdzielić ten sam tryb z miejscem produkcyjnym, przed można wymienić dwóch miejsc.</span><span class="sxs-lookup"><span data-stu-id="a0695-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="a0695-122">Dodaj miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-122">Add a deployment slot</span></span>
<span data-ttu-id="a0695-123">Aplikacja musi być uruchomiona **standardowe** lub **Premium** trybu w kolejności, aby włączyć wielu miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="a0695-124">W [Azure Portal](https://portal.azure.com/), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="a0695-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="a0695-125">Wybierz **miejsc wdrożenia** opcji, a następnie kliknij przycisk **Dodaj miejsce**.</span><span class="sxs-lookup"><span data-stu-id="a0695-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Dodaj nowe miejsce wdrożenia][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="a0695-127">Jeśli aplikacja nie jest już w **standardowe** lub **Premium** tryb, zostanie wyświetlony komunikat informujący o obsługiwanych trybów umożliwiających publikowanie przemieszczane.</span><span class="sxs-lookup"><span data-stu-id="a0695-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="a0695-128">W tym momencie masz możliwość wybrania **uaktualnienia** i przejdź do **skali** kartę aplikacji przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="a0695-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="a0695-129">W **dodać gniazdo** bloku, nazwę miejsca i wybierz, czy Klonuj konfiguracji aplikacji z innego istniejącego miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="a0695-130">Kliknij znacznik wyboru, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="a0695-130">Click the check mark to continue.</span></span>
   
    ![Źródło konfiguracji][ConfigurationSource1]
   
    <span data-ttu-id="a0695-132">Pierwsze dodać gniazdo, będziesz korzystać tylko z dwóch opcji: klonowania konfiguracji z miejsca domyślne w środowisku produkcyjnym lub w ogóle.</span><span class="sxs-lookup"><span data-stu-id="a0695-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="a0695-133">Po utworzeniu kilka miejsc, można Klonuj konfiguracji z miejsca innego niż ten, w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="a0695-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Konfiguracja źródła][MultipleConfigurationSources]
4. <span data-ttu-id="a0695-135">W bloku zasobów aplikacji, kliknij przycisk **miejsc wdrożenia**, następnie kliknij przycisk miejsce wdrożenia, aby otworzyć blok zasobów z miejsca, przy użyciu zestawu metryki i konfiguracji, tak jak każda inna aplikacja.</span><span class="sxs-lookup"><span data-stu-id="a0695-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="a0695-136">Nazwa miejsca jest wyświetlany w górnej części bloku celu odnotowania, że miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Tytuł miejsca wdrożenia][StagingTitle]
5. <span data-ttu-id="a0695-138">Kliknij adres URL aplikacji w bloku tego gniazda.</span><span class="sxs-lookup"><span data-stu-id="a0695-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="a0695-139">Zwróć uwagę, miejsce wdrożenia ma własną nazwę hosta i jest również aktywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="a0695-140">Aby ograniczyć publiczny dostęp do miejsca wdrożenia, zobacz [aplikacji sieci Web usługi aplikacji — Blokuj dostęp w sieci web do miejsc wdrożenia nieprodukcyjnych](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="a0695-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="a0695-141">Brak zawartości po utworzeniu miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="a0695-142">Można wdrożyć do gniazda z gałęzi repozytorium różnych lub całkowicie innego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a0695-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="a0695-143">Można również zmienić konfigurację tego gniazda.</span><span class="sxs-lookup"><span data-stu-id="a0695-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="a0695-144">Użyj poświadczeń profilu lub wdrożenia publikowania skojarzone z miejscem wdrożenia aktualizacji zawartości.</span><span class="sxs-lookup"><span data-stu-id="a0695-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="a0695-145">Można na przykład [publikowanie do tego miejsca za pomocą narzędzia git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="a0695-146">Konfiguracja dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-146">Configuration for deployment slots</span></span>
<span data-ttu-id="a0695-147">Klonuj konfiguracji z innego miejsca wdrożenia, sklonowany konfiguracji po edycji.</span><span class="sxs-lookup"><span data-stu-id="a0695-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="a0695-148">Ponadto niektóre elementy konfiguracji będzie śledzić zawartości między swap (nie gniazdo określonych), podczas gdy inne elementy konfiguracji, pozostanie w tym samym miejscu po swap (gniazdo określone).</span><span class="sxs-lookup"><span data-stu-id="a0695-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="a0695-149">Konfiguracja ulegnie zmianie po zamienić miejsc przedstawiono.</span><span class="sxs-lookup"><span data-stu-id="a0695-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="a0695-150">**Ustawienia, które są zamienione**:</span><span class="sxs-lookup"><span data-stu-id="a0695-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="a0695-151">Ustawienia ogólne — takie jak gniazda sieci Web 32/64-bitowych wersji framework</span><span class="sxs-lookup"><span data-stu-id="a0695-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="a0695-152">Ustawienia aplikacji (może być skonfigurowana do osadzania miejsca)</span><span class="sxs-lookup"><span data-stu-id="a0695-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="a0695-153">Parametry połączenia (można skonfigurować w celu osadzania miejsca)</span><span class="sxs-lookup"><span data-stu-id="a0695-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="a0695-154">Mapowania programu obsługi</span><span class="sxs-lookup"><span data-stu-id="a0695-154">Handler mappings</span></span>
* <span data-ttu-id="a0695-155">Ustawienia monitorowania i diagnostyki</span><span class="sxs-lookup"><span data-stu-id="a0695-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="a0695-156">Zawartość zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="a0695-156">WebJobs content</span></span>

<span data-ttu-id="a0695-157">**Ustawienia, które nie są zamienione**:</span><span class="sxs-lookup"><span data-stu-id="a0695-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="a0695-158">Publikowanie punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="a0695-158">Publishing endpoints</span></span>
* <span data-ttu-id="a0695-159">Niestandardowa nazwa domeny</span><span class="sxs-lookup"><span data-stu-id="a0695-159">Custom Domain Names</span></span>
* <span data-ttu-id="a0695-160">Certyfikaty SSL i powiązań</span><span class="sxs-lookup"><span data-stu-id="a0695-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="a0695-161">Ustawienia skali</span><span class="sxs-lookup"><span data-stu-id="a0695-161">Scale settings</span></span>
* <span data-ttu-id="a0695-162">Planiści zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="a0695-162">WebJobs schedulers</span></span>

<span data-ttu-id="a0695-163">Aby skonfigurować aplikację ustawienie lub parametry połączenia trzymać miejsca (nie miejscami), dostęp do **ustawienia aplikacji** bloku do określonego miejsca, następnie wybierz **ustawienie miejsca** pola konfiguracji elementy, które powinny trzymaj gniazda.</span><span class="sxs-lookup"><span data-stu-id="a0695-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="a0695-164">Należy pamiętać, że oznaczenie element konfiguracji zgodnie z miejsca określonego powoduje ustanowienie tego elementu jako nie swappable wszystkich miejsc wdrożenia skojarzone z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a0695-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Ustawienia gniazda][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="a0695-166">Zamienić miejsc wdrażania</span><span class="sxs-lookup"><span data-stu-id="a0695-166">Swap deployment slots</span></span> 
<span data-ttu-id="a0695-167">Można zamienić miejsc wdrożenia w **omówienie** lub **miejsc wdrożenia** widok bloku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0695-168">Przed możesz zamienić aplikację z miejsce wdrożenia do środowiska produkcyjnego, upewnij się, że wszystkie z systemem innym niż miejsce określone ustawienia są skonfigurowane zgodnie z oczekiwaniami go w celu wymiany.</span><span class="sxs-lookup"><span data-stu-id="a0695-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="a0695-169">Aby zamienić miejsc wdrożenia, kliknij przycisk **wymiany** przycisku w pasku poleceń, aplikacji lub na pasku poleceń w miejscu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Przycisk wymiany][SwapButtonBar]

2. <span data-ttu-id="a0695-171">Upewnij się, czy wymiany źródłowych i docelowych wymiany są poprawnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="a0695-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="a0695-172">Zazwyczaj obiekt docelowy wymiany jest miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="a0695-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="a0695-173">Kliknij przycisk **OK** do ukończenia tej operacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="a0695-174">Po zakończeniu operacji, zostały zamieniono miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Ukończ zamianę](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="a0695-176">Dla **zamiany z podglądem** wymiany typu, zobacz [zamiany z podglądem (faza wielu wymiany)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="a0695-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="a0695-177">Zamiana z podglądem (faza wielu wymiany)</span><span class="sxs-lookup"><span data-stu-id="a0695-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="a0695-178">Zamiany z podglądem lub wielu faza wymiany uprościć weryfikacji konfiguracji specyficznych dla miejsca elementów, takich jak parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="a0695-179">W przypadku obciążeń krytycznym chcesz zweryfikować których aplikacja działa zgodnie z oczekiwaniami, po zastosowaniu konfiguracji miejsca produkcyjnego i należy wykonać takie weryfikacji *przed* aplikacji jest zamieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a0695-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="a0695-180">Zamiany z podglądem jest, co jest potrzebne.</span><span class="sxs-lookup"><span data-stu-id="a0695-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="a0695-181">Zamiany z podglądem jest nieobsługiwana w aplikacjach sieci web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a0695-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="a0695-182">Jeśli używasz **zamiana z podglądem** opcji (zobacz [zamienić miejsc wdrożenia](#Swap)), usługi aplikacji — wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a0695-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="a0695-183">Przechowuje miejsca docelowego bez zmian, więc nie ma wpływu na istniejące obciążenia na gniazdo (np. produkcja).</span><span class="sxs-lookup"><span data-stu-id="a0695-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="a0695-184">Dotyczy elementów konfiguracji z miejsca docelowego do miejsca źródłowego, w tym parametry połączenia specyficzne dla miejsca i ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="a0695-185">Uruchamia ponownie procesów roboczych na miejsca źródłowego przy użyciu tych elementów konfiguracji wyżej.</span><span class="sxs-lookup"><span data-stu-id="a0695-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="a0695-186">Po zakończeniu wymiany: Przenosi miejsca źródłowego wstępnie przygotowany warmed up do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="a0695-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="a0695-187">Miejscem docelowym jest przenoszony do miejsca źródłowego, jak ręcznie wymiany.</span><span class="sxs-lookup"><span data-stu-id="a0695-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="a0695-188">Jeśli anulujesz wymiany: ponowne zastosowanie elementy konfiguracji z miejsca źródłowego do miejsca źródłowego.</span><span class="sxs-lookup"><span data-stu-id="a0695-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="a0695-189">Można wyświetlić podgląd dokładnie jak aplikacja będzie się odbywać z konfiguracji z miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="a0695-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="a0695-190">Po ukończeniu sprawdzania poprawności zakończeniu wymiany w osobnym kroku.</span><span class="sxs-lookup"><span data-stu-id="a0695-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="a0695-191">Ten krok ma dodatkową zaletę, który jest już przygotowaniu miejsca źródłowego z odpowiednią konfigurację, a klienci nie będzie działać z żadnych przestojów.</span><span class="sxs-lookup"><span data-stu-id="a0695-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="a0695-192">Przykłady dla poleceń cmdlet programu Azure PowerShell, dostępna dla wielu faza wymiany znajdują się w poleceniach cmdlet programu PowerShell systemu Azure dla sekcji miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="a0695-193">Konfigurowanie automatycznej wymiany (MB)</span><span class="sxs-lookup"><span data-stu-id="a0695-193">Configure Auto Swap</span></span>
<span data-ttu-id="a0695-194">Automatycznej wymiany usprawnia scenariuszy opracowywania oprogramowania miejscu stale wdrażania aplikacji za pomocą zero zimny start i przestojów dla klientów końcowych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="a0695-195">Jeśli miejsce wdrożenia jest skonfigurowany do automatycznej wymiany do produkcji, zawsze wypychania aktualizacji kodu do tego miejsca, usługi aplikacji — automatycznie wymiany aplikacji w środowisku produkcyjnym po już ma przygotowaniu miejsca w miejscu.</span><span class="sxs-lookup"><span data-stu-id="a0695-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0695-196">Po włączeniu automatycznej wymiany dla miejsca, upewnij się, że konfiguracja miejsca jest dokładnie konfiguracji przeznaczonych dla miejsca docelowego (zazwyczaj gniazda produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="a0695-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="a0695-197">Automatycznej wymiany nie jest obsługiwana w aplikacjach sieci web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a0695-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="a0695-198">Konfigurowanie automatycznej wymiany gnieździe jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="a0695-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="a0695-199">Wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="a0695-199">Follow the steps below:</span></span>

1. <span data-ttu-id="a0695-200">W **miejsc wdrożenia**, a następnie wybierz gniazdo nieprodukcyjnych i wybierz **ustawienia aplikacji** w bloku zasobów z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="a0695-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="a0695-201">Wybierz **na** dla **automatycznej wymiany**, wybierz gniazdo docelowy w **automatycznej wymiany miejsca**i kliknij przycisk **zapisać** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="a0695-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="a0695-202">Upewnij się, że konfiguracja gniazda jest dokładnie konfiguracji przeznaczonych dla miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="a0695-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="a0695-203">**Powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="a0695-204">Aby przetestować automatycznej wymiany dla aplikacji, najpierw wybrać gnieździe docelowym nieprodukcyjnych **automatycznej wymiany miejsca** zapoznać się z funkcji.</span><span class="sxs-lookup"><span data-stu-id="a0695-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="a0695-205">Wykonanie kodu wypychania do tego miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="a0695-206">Automatycznej wymiany nastąpi po pewnym czasie i aktualizacji zostaną odzwierciedlone w adresie URL z miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="a0695-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="a0695-207">Aby wycofać aplikacji produkcyjnej po wymiany</span><span class="sxs-lookup"><span data-stu-id="a0695-207">To rollback a production app after swap</span></span>
<span data-ttu-id="a0695-208">Jeśli wszystkie błędy są identyfikowane w środowisku produkcyjnym po zakończeniu wymiany gniazd, wycofywanie gniazdach do stanu przed wymiany natychmiast wymiany tego samego dwa gniazda.</span><span class="sxs-lookup"><span data-stu-id="a0695-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="a0695-209">Niestandardowe rozgrzewania przed wymiany</span><span class="sxs-lookup"><span data-stu-id="a0695-209">Custom warm-up before swap</span></span>
<span data-ttu-id="a0695-210">Niektóre aplikacje mogą wymagać akcje niestandardowe rozgrzewania.</span><span class="sxs-lookup"><span data-stu-id="a0695-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="a0695-211">`applicationInitialization` Element konfiguracji w pliku web.config można określić niestandardową inicjalizację akcje można wykonać, zanim żądanie zostanie odebrane.</span><span class="sxs-lookup"><span data-stu-id="a0695-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="a0695-212">Operacja zamiany będzie oczekiwał na ten niestandardowe zwiększanie gotowości do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="a0695-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="a0695-213">Oto przykładowe fragment pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="a0695-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="a0695-214">Aby usunąć miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-214">To delete a deployment slot</span></span>
<span data-ttu-id="a0695-215">W bloku dla miejsca wdrożenia, otwórz blok miejsce wdrożenia, kliknij pozycję **omówienie** (domyślna strona) i kliknij przycisk **usunąć** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="a0695-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Usuń miejsce wdrożenia][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="a0695-217">Polecenia cmdlet programu PowerShell systemu Azure dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="a0695-218">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell, włącznie z obsługą zarządzania miejsc wdrożenia w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a0695-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="a0695-219">Aby uzyskać informacje na temat instalowania i konfigurowania programu Azure PowerShell, a na uwierzytelniania programu Azure PowerShell z subskrypcją platformy Azure, zobacz [jak instalowanie i konfigurowanie programu Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0695-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="a0695-220">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a0695-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="a0695-221">Tworzenie miejsca wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="a0695-222">Zainicjuj wymiany z przeglądem (faza wielu wymiany) i zastosować konfiguracji miejsca docelowego do miejsca źródłowego</span><span class="sxs-lookup"><span data-stu-id="a0695-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="a0695-223">Anuluj oczekująca zamiana (obszar wymiany z przeglądem) i przywracanie konfiguracji miejsca źródłowego</span><span class="sxs-lookup"><span data-stu-id="a0695-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="a0695-224">Zamienić miejsc wdrażania</span><span class="sxs-lookup"><span data-stu-id="a0695-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="a0695-225">Usuń miejsce wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="a0695-226">Azure polecenia interfejsu wiersza polecenia (Azure CLI) dla miejsc wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0695-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="a0695-227">Interfejsu wiersza polecenia Azure udostępnia polecenia i platform do pracy z platformą Azure, w tym obsługę zarządzania miejsc wdrożenia usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0695-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="a0695-228">Aby uzyskać instrukcje dotyczące instalowania i konfigurowania wiersza polecenia platformy Azure, w tym informacje na temat nawiązywania połączenia z subskrypcją platformy Azure, Azure CLI zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a0695-229">Aby wyświetlić listę dostępnych poleceń dla usługi Azure App Service w wiersza polecenia platformy Azure, należy wywołać `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="a0695-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a0695-230">Dla [Azure CLI 2.0](https://github.com/Azure/azure-cli) poleceń dla miejsc wdrożenia, zobacz [miejsce wdrożenia sieci web appservice az](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="a0695-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="a0695-231">Lista witryn platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0695-231">azure site list</span></span>
<span data-ttu-id="a0695-232">Informacje o aplikacji w bieżącej subskrypcji, należy wywołać **listy witryn azure**, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a0695-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="a0695-233">Tworzenie usługi Azure site</span><span class="sxs-lookup"><span data-stu-id="a0695-233">azure site create</span></span>
<span data-ttu-id="a0695-234">Aby utworzyć miejsce wdrożenia, należy wywołać **Tworzenie usługi azure site** i określ nazwę istniejącej aplikacji oraz nazwę gniazda, aby utworzyć, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a0695-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="a0695-235">Aby włączyć kontrolę źródła dla nowego miejsca, za pomocą **— git** opcji, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a0695-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="a0695-236">usługi Azure site wymiany (MB)</span><span class="sxs-lookup"><span data-stu-id="a0695-236">azure site swap</span></span>
<span data-ttu-id="a0695-237">Aby wdrażania aktualizacji gniazdo aplikacji produkcyjnej, użyj **wymiany usługi azure site** polecenie, aby wykonać operację zamiany, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a0695-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="a0695-238">Aplikacji produkcyjnej nie będą występować dowolne czas przestoju, nie zostaną poddane zimny start.</span><span class="sxs-lookup"><span data-stu-id="a0695-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="a0695-239">Usuwanie witryny platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a0695-239">azure site delete</span></span>
<span data-ttu-id="a0695-240">Aby usunąć miejsce wdrożenia, który nie jest już potrzebny, należy użyć **usuwanie witryny azure** polecenia, jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a0695-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="a0695-241">Zobacz działającą aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a0695-241">See a web app in action.</span></span> <span data-ttu-id="a0695-242">[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) natychmiast i tej utworzyć początkową aplikację — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="a0695-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a0695-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0695-243">Next Steps</span></span>
<span data-ttu-id="a0695-244">[Azure App Service aplikacji sieci Web — Blokuj dostęp w sieci web do miejsc wdrożenia nieprodukcyjnych](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[wprowadzenie do usługi App Service w systemie Linux](./app-service-linux-intro.md)
[bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="a0695-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
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

