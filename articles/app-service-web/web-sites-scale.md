---
title: "Skalowanie w górę aplikacji na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować aplikację w usłudze Azure App Service, aby dodać pojemności i funkcje."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="dff63-103">Skalowanie w górę aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dff63-103">Scale up an app in Azure</span></span>
<span data-ttu-id="dff63-104">W tym artykule przedstawiono sposób skalowania aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="dff63-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="dff63-105">Istnieją dwa przepływy pracy do skalowania, skalowania w górę i skalowania w poziomie i w tym artykule opisano skalowania w górę przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="dff63-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="dff63-106">[Skalowanie w górę](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Pobierz więcej Procesora, pamięci, miejsca na dysku i dodatkowych funkcji, takich jak dedykowanych maszynach wirtualnych (VM), niestandardowe domeny i certyfikaty, przemieszczania miejsc, skalowanie automatyczne i inne.</span><span class="sxs-lookup"><span data-stu-id="dff63-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="dff63-107">Skalowanie w górę, zmieniając warstwę cenową planu usługi aplikacji — należącego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dff63-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="dff63-108">[Skalowanie w poziomie](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Zwiększ liczbę wystąpień maszyn wirtualnych, które Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="dff63-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="dff63-109">Możesz skalować w poziomie do maksymalnie 20 wystąpień, w zależności od warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="dff63-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="dff63-110">[Środowiska usługi App Service](../app-service/app-service-app-service-environments-readme.md) w **Premium** warstwy będzie kontynuowany liczba skalowalnego w poziomie do 50 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="dff63-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="dff63-111">Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="dff63-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="dff63-112">Można znaleźć informacje o tym, jak używać Skalowanie automatyczne, który jest skalowanie liczby wystąpień automatycznie na podstawie wstępnie zdefiniowanych reguł i harmonogramy.</span><span class="sxs-lookup"><span data-stu-id="dff63-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="dff63-113">Ustawienia skalowania trwać tylko sekund, stosowanie i wpływają na wszystkie aplikacje w sieci [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dff63-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="dff63-114">Nie wymagają zmiany kodu lub ponownego wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dff63-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="dff63-115">Aby uzyskać informacje o cenach i funkcje poszczególnych planów usługi aplikacji, zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="dff63-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="dff63-116">Przed przejściem plan usługi aplikacji z **wolne** warstwy, należy najpierw usunąć [limitów wydatków](https://azure.microsoft.com/pricing/spending-limits/) w miejscu dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dff63-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="dff63-117">Aby wyświetlić lub zmienić opcje dla Twojej subskrypcji Microsoft Azure App Service, zobacz [subskrypcji platformy Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="dff63-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="dff63-118">Skalowanie w górę warstwę cenową</span><span class="sxs-lookup"><span data-stu-id="dff63-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="dff63-119">W przeglądarce otwórz [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="dff63-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="dff63-120">W bloku aplikacji kliknij **wszystkie ustawienia**, a następnie kliknij przycisk **Skaluj w górę**.</span><span class="sxs-lookup"><span data-stu-id="dff63-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Przejdź do skalować aplikację platformy Azure.][ChooseWHP]
3. <span data-ttu-id="dff63-122">Wybierz warstwę, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="dff63-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="dff63-123">**Powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="dff63-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="dff63-124">Powiązane zasoby są skalowane</span><span class="sxs-lookup"><span data-stu-id="dff63-124">Scale related resources</span></span>
<span data-ttu-id="dff63-125">Jeśli aplikacja jest zależny od innych usług, takich jak bazy danych SQL Azure lub usługi Azure Storage, można również skalować tych zasobów na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="dff63-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="dff63-126">Te zasoby nie mogą być skalowane z planu usługi aplikacji i musi być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="dff63-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="dff63-127">W **Essentials**, kliknij przycisk **grupy zasobów** łącza.</span><span class="sxs-lookup"><span data-stu-id="dff63-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Skalowanie w górę powiązane zasoby aplikacji Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="dff63-129">W **Podsumowanie** częścią **grupy zasobów** bloku, kliknij zasób, który ma być skalowana.</span><span class="sxs-lookup"><span data-stu-id="dff63-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="dff63-130">Poniższy zrzut ekranu przedstawia zasobów bazy danych SQL i zasobów magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="dff63-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Przejdź do bloku grupy zasobów, aby skalować aplikację Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="dff63-132">Dla zasobów bazy danych SQL, kliknij przycisk **ustawienia** > **warstwa cenowa** skalowania warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="dff63-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Skalowanie w górę zaplecza bazy danych SQL dla aplikacji Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="dff63-134">Można też włączyć [— replikacja geograficzna](../sql-database/sql-database-geo-replication-overview.md) dla swojego wystąpienia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="dff63-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="dff63-135">Dla zasobu usługi Magazyn Azure, kliknij przycisk **ustawienia** > **konfiguracji** na skalowanie w górę opcje magazynu.</span><span class="sxs-lookup"><span data-stu-id="dff63-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Skalowanie w górę konta usługi Magazyn Azure używany przez aplikację Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="dff63-137">Dowiedz się więcej o funkcje programistyczne</span><span class="sxs-lookup"><span data-stu-id="dff63-137">Learn about developer features</span></span>
<span data-ttu-id="dff63-138">W zależności od warstwy cenowej są dostępne następujące funkcje ukierunkowane developer:</span><span class="sxs-lookup"><span data-stu-id="dff63-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="dff63-139">Liczba bitów</span><span class="sxs-lookup"><span data-stu-id="dff63-139">Bitness</span></span>
* <span data-ttu-id="dff63-140">**Podstawowe**, **standardowe**, i **Premium** warstwy obsługi aplikacji 64-bitowe i 32-bitowych.</span><span class="sxs-lookup"><span data-stu-id="dff63-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="dff63-141">**Wolne** i **Shared** planu warstwami obsługuje wyłącznie aplikacje 32-bitowe.</span><span class="sxs-lookup"><span data-stu-id="dff63-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="dff63-142">Obsługa debugera</span><span class="sxs-lookup"><span data-stu-id="dff63-142">Debugger support</span></span>
* <span data-ttu-id="dff63-143">Obsługa debugera jest dostępna dla **wolne**, **Shared**, i **podstawowe** tryby w jedno połączenie dla danego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dff63-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="dff63-144">Obsługa debugera jest dostępna dla **standardowe** i **Premium** tryby na pięć równoczesnych połączeń na plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dff63-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="dff63-145">Dowiedz się więcej o innych funkcjach</span><span class="sxs-lookup"><span data-stu-id="dff63-145">Learn about other features</span></span>
* <span data-ttu-id="dff63-146">Aby uzyskać szczegółowe informacje o wszystkich pozostałych funkcji w usłudze App Service planów cenowych w tym i funkcje przydatne dla wszystkich użytkowników (w tym deweloperzy), zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="dff63-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="dff63-147">Jeśli chcesz rozpocząć pracę z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="dff63-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="dff63-148">Bez kart kredytowych są wymagane i nie bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="dff63-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="dff63-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dff63-149">Next steps</span></span>
* <span data-ttu-id="dff63-150">Aby rozpocząć pracę z platformą Azure, zobacz [bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dff63-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dff63-151">Informacje o cenach, pomocy technicznej i umowy dotyczącej poziomu usług można znaleźć w poniższych łączy.</span><span class="sxs-lookup"><span data-stu-id="dff63-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="dff63-152">Informacje o cenach transferu danych</span><span class="sxs-lookup"><span data-stu-id="dff63-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="dff63-153">Plany pomocy technicznej platformy Azure firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="dff63-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="dff63-154">Umowy dotyczące poziomu usług</span><span class="sxs-lookup"><span data-stu-id="dff63-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="dff63-155">Szczegóły cennika bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="dff63-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="dff63-156">[Maszyny wirtualnej i rozmiary usługi chmury Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="dff63-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="dff63-157">Szczegóły cennika usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="dff63-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="dff63-158">Usługi aplikacji — cennik szczegóły - połączeń SSL</span><span class="sxs-lookup"><span data-stu-id="dff63-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="dff63-159">Informacje o usłudze Azure App Service najlepszych rozwiązań, w tym tworzenie skalowalnych i elastyczne architektury, zobacz [najlepsze rozwiązania: aplikacje sieci Web usługi aplikacji Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="dff63-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="dff63-160">Dla plików wideo na temat skalowania aplikacji usługi App Service zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="dff63-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="dff63-161">Kiedy skalować witryn sieci Web Azure - o Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="dff63-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="dff63-162">Automatyczne skalowanie witryn sieci Web Azure, procesora CPU lub zaplanowane — z Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="dff63-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="dff63-163">Jak Azure skalowalność witryn sieci Web - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="dff63-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
