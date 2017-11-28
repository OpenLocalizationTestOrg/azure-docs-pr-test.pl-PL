---
title: "aaaAzure pakiet IoT — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące Pakietu IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="e3593-103">Często zadawane pytania dotyczące Pakietu IoT</span><span class="sxs-lookup"><span data-stu-id="e3593-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="e3593-104">Zobacz też określonych połączonych fabryki hello [— często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="e3593-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="e3593-105">Gdzie znaleźć kodu źródłowego hello hello wstępnie rozwiązań?</span><span class="sxs-lookup"><span data-stu-id="e3593-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="e3593-106">Kod źródłowy Hello są przechowywane w powitania po repozytoriów GitHub:</span><span class="sxs-lookup"><span data-stu-id="e3593-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="e3593-107">[Zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="e3593-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="e3593-108">[Rozwiązanie do konserwacji predykcyjnej wstępnie][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="e3593-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="e3593-109">Fabryka połączonych wstępnie skonfigurowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e3593-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="e3593-110">Jak zaktualizować toohello najnowszą wersję hello zdalnego monitorowania wstępnie skonfigurowane rozwiązanie czy używa hello funkcje zarządzania urządzeniami Centrum IoT?</span><span class="sxs-lookup"><span data-stu-id="e3593-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="e3593-111">Jeśli wdrożono wstępnie skonfigurowane rozwiązanie z witryny https://www.azureiotsuite.com/ hello zawsze wdraża nowe wystąpienie klasy hello najnowsza wersja rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="e3593-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="e3593-112">W przypadku wdrożenia przy użyciu wiersza polecenia hello wstępnie skonfigurowane rozwiązanie, należy zaktualizować istniejące wdrożenie o nowy kod.</span><span class="sxs-lookup"><span data-stu-id="e3593-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="e3593-113">Zobacz [wdrożenie w chmurze] [ lnk-cloud-deployment] w hello GitHub [repozytorium][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="e3593-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e3593-114">Jak dodać obsługę nowych toohello — metoda urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="e3593-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="e3593-115">Zobacz sekcję hello [obsługę nowych symulatora toohello — metoda] [ lnk-add-method] w hello [dostosować wstępnie skonfigurowane rozwiązanie] [ lnk-customize] artykułu.</span><span class="sxs-lookup"><span data-stu-id="e3593-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="e3593-116">Symulowane urządzenie Hello ignoruje zmiany żądanej właściwości, dlaczego?</span><span class="sxs-lookup"><span data-stu-id="e3593-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="e3593-117">W hello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie, hello symulowane urządzenie kod używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** żądanego właściwości Witaj tooupdate zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="e3593-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="e3593-118">Wszystkie inne żądanej właściwości żądania zmiany są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="e3593-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="e3593-119">Urządzenie nie ma hello listy urządzeń na pulpicie nawigacyjnym rozwiązania hello, dlaczego?</span><span class="sxs-lookup"><span data-stu-id="e3593-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="e3593-120">Witaj listy urządzeń na pulpicie nawigacyjnym rozwiązania hello używa zapytania tooreturn hello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e3593-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="e3593-121">Obecnie kwerendy nie może zwrócić więcej niż 10 tys urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e3593-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="e3593-122">Spróbuj bardziej restrykcyjne hello kryteria wyszukiwania dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="e3593-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="e3593-123">Jaka jest różnica hello usunięcie grupy zasobów w hello Azure portalu i klikając przycisk Usuń na wstępnie skonfigurowane rozwiązanie w azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="e3593-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="e3593-124">Jeśli usuniesz hello wstępnie skonfigurowane rozwiązanie w [azureiotsuite.com][lnk-azureiotsuite], należy usunąć wszystkie zasoby hello, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e3593-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="e3593-125">Jeśli dodano grupę zasobów toohello dodatkowe zasoby, te zasoby są także usuwane.</span><span class="sxs-lookup"><span data-stu-id="e3593-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="e3593-126">Usunięcie grupy zasobów hello w hello [portalu Azure][lnk-azure-portal], zostaną usunięte tylko hello zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3593-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="e3593-127">Należy również aplikacji usługi Azure Active Directory hello toodelete skojarzonej z hello wstępnie skonfigurowane rozwiązanie w hello [klasycznego portalu Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="e3593-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="e3593-128">Jak wiele wystąpień Centrum IoT można udostępnić w ramach subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="e3593-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="e3593-129">Domyślnie można udostępnić [10 centra IoT na subskrypcję][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="e3593-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="e3593-130">Można utworzyć [biletu pomocy technicznej platformy Azure] [ link-azuresupportticket] tooraise ten limit.</span><span class="sxs-lookup"><span data-stu-id="e3593-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="e3593-131">W rezultacie od każdego przepisy wstępnie skonfigurowane rozwiązanie z nowym Centrum IoT można tylko należy się too10 wstępnie rozwiązań w ramach danej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e3593-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="e3593-132">Jak wiele wystąpień bazy danych Azure rozwiązania Cosmos można udostępnić w ramach subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="e3593-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="e3593-133">50.</span><span class="sxs-lookup"><span data-stu-id="e3593-133">Fifty.</span></span> <span data-ttu-id="e3593-134">Można utworzyć [biletu pomocy technicznej platformy Azure] [ link-azuresupportticket] tooraise to ograniczenie, ale domyślnie umożliwia tylko obsługę 50 wystąpień rozwiązania Cosmos bazy danych na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e3593-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="e3593-135">Ile bezpłatnych interfejsów API usługi Mapy Bing można aprowizować w ramach subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="e3593-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="e3593-136">Dwa.</span><span class="sxs-lookup"><span data-stu-id="e3593-136">Two.</span></span> <span data-ttu-id="e3593-137">W subskrypcji platformy Azure można utworzyć tylko dwa wewnętrzne transakcje poziom 1 mapy Bing dla planów organizacji.</span><span class="sxs-lookup"><span data-stu-id="e3593-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="e3593-138">rozwiązanie monitorowania zdalnego Hello jest udostępniana domyślnie z planem hello wewnętrzny poziom 1 transakcji.</span><span class="sxs-lookup"><span data-stu-id="e3593-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="e3593-139">W związku z tym umożliwia tylko obsługę tootwo zdalnego monitorowanie rozwiązań w ramach subskrypcji, bez żadnych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="e3593-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="e3593-140">Mam wdrożone rozwiązanie do monitorowania zdalnego z mapą statyczną. Jak dodać interaktywną mapę Bing?</span><span class="sxs-lookup"><span data-stu-id="e3593-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="e3593-141">Pobierz interfejsu API map Bing dla QueryKey przedsiębiorstwa z [portalu Azure][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="e3593-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="e3593-142">Przejdź toohello grupy zasobów, w przypadku interfejsu API map Bing dla przedsiębiorstwa hello [portalu Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e3593-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="e3593-143">Kliknij przycisk **wszystkie ustawienia**, następnie **zarządzanie kluczami**.</span><span class="sxs-lookup"><span data-stu-id="e3593-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="e3593-144">Można zobaczyć dwa klucze: **umożliwia** i **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="e3593-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="e3593-145">Skopiuj wartość hello **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="e3593-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e3593-146">Nie masz konta interfejsu API usługi Mapy Bing dla przedsiębiorstw?</span><span class="sxs-lookup"><span data-stu-id="e3593-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="e3593-147">Utworzyć w hello [portalu Azure] [ lnk-azure-portal] klikając + nowe wyszukiwanie interfejsu API map Bing dla przedsiębiorstwa i wykonaj monituje toocreate.</span><span class="sxs-lookup"><span data-stu-id="e3593-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="e3593-148">Rozwiń hello najnowsze kod z hello [Azure IoT — zdalnego-monitorowania][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="e3593-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="e3593-149">Uruchom lokalnie lub w chmurze po hello dotyczące wdrażania wiersza polecenia w folderze /docs/ hello w repozytorium hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e3593-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="e3593-150">Po uruchomiono na komputerze lokalnym lub w chmurze, wdrażania, poszukać w folderze głównym dla hello *. plików user.config utworzonych podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e3593-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="e3593-151">Otwórz ten plik w edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="e3593-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="e3593-152">Zmień hello następująca linia wartość hello tooinclude skopiowany z Twojej **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="e3593-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="e3593-153">Czy można utworzyć wstępnie skonfigurowane rozwiązanie w przypadku korzystania z platformy Microsoft Azure dla programu DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="e3593-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="e3593-154">Obecnie nie można utworzyć wstępnie skonfigurowane rozwiązanie o [Microsoft Azure dla programu DreamSpark] [ lnk-dreamspark] konta.</span><span class="sxs-lookup"><span data-stu-id="e3593-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="e3593-155">Można jednak utworzyć [bezpłatnego konta wersji próbnej platformy Azure] [ lnk-30daytrial] w zaledwie kilka minut, umożliwiająca tworzenie wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3593-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="e3593-156">Jeśli subskrypcja Cloud Solution Provider (CSP) można utworzyć wstępnie skonfigurowane rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="e3593-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="e3593-157">Obecnie nie można utworzyć wstępnie skonfigurowane rozwiązanie z subskrypcją Cloud Solution Provider (CSP).</span><span class="sxs-lookup"><span data-stu-id="e3593-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="e3593-158">Można jednak utworzyć [bezpłatnego konta wersji próbnej platformy Azure] [ lnk-30daytrial] w zaledwie kilka minut, umożliwiająca tworzenie wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3593-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="e3593-159">Jak usunąć dzierżawę usługi AAD?</span><span class="sxs-lookup"><span data-stu-id="e3593-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="e3593-160">Zobacz Golpe marek blogu [wskazówki usunięcia dzierżawy usługi Azure AD][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="e3593-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="e3593-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3593-161">Next steps</span></span>

<span data-ttu-id="e3593-162">Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:</span><span class="sxs-lookup"><span data-stu-id="e3593-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="e3593-163">[Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="e3593-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="e3593-164">Fabryka połączonych wstępnie Omówienie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e3593-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="e3593-165">[Zabezpieczenia IoT z hello tła w][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="e3593-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
