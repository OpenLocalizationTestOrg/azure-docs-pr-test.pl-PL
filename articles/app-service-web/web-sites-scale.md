---
title: "aaaScale się aplikacji na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale zapasowej aplikacji w usłudze Azure App Service tooadd pojemności i funkcje."
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
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="d5c7f-103">Skalowanie w górę aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d5c7f-103">Scale up an app in Azure</span></span>
<span data-ttu-id="d5c7f-104">W tym artykule opisano sposób tooscale aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="d5c7f-105">Istnieją dwa przepływy pracy do skalowania, skalowania w górę i skalowania w poziomie i w tym artykule opisano hello skalowania w górę przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="d5c7f-106">[Skalowanie w górę](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Pobierz więcej Procesora, pamięci, miejsca na dysku i dodatkowych funkcji, takich jak dedykowanych maszynach wirtualnych (VM), niestandardowe domeny i certyfikaty, przemieszczania miejsc, skalowanie automatyczne i inne.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="d5c7f-107">Skalowanie w górę, zmieniając hello cenowym planu usługi aplikacji — należącego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="d5c7f-108">[Skalowanie w poziomie](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Zwiększ hello liczba wystąpień maszyn wirtualnych, których uruchamianie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="d5c7f-109">Możesz skalować w poziomie tooas wiele jako 20 wystąpień, w zależności od warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="d5c7f-110">[Środowiska usługi App Service](../app-service/app-service-app-service-environments-readme.md) w **Premium** warstwy będzie zwiększyć swoich wystąpień too50 liczba skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="d5c7f-111">Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="d5c7f-112">Można znaleźć poza jak toouse Skalowanie automatyczne, który jest automatycznie tooscale liczba wystąpień na podstawie wstępnie zdefiniowanych reguł i harmonogramy.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="d5c7f-113">Witaj skali ustawienia zajmuje tylko sekund tooapply i wpływają na wszystkie aplikacje w sieci [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="d5c7f-114">Nie wymagają możesz toochange kodu lub ponownego wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="d5c7f-115">Uzyskać informacje o cenach hello i funkcjach poszczególnych planów usługi aplikacji, zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="d5c7f-116">Przed przejściem plan usługi aplikacji z hello **wolne** warstwy, należy najpierw usunąć hello [limitów wydatków](https://azure.microsoft.com/pricing/spending-limits/) w miejscu dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="d5c7f-117">tooview lub zmień opcje subskrypcji Microsoft Azure App Service, zobacz [subskrypcji platformy Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="d5c7f-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="d5c7f-118">Skalowanie w górę warstwę cenową</span><span class="sxs-lookup"><span data-stu-id="d5c7f-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="d5c7f-119">W przeglądarce otwórz hello [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d5c7f-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="d5c7f-120">W bloku aplikacji kliknij **wszystkie ustawienia**, a następnie kliknij przycisk **Skaluj w górę**.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Przejdź tooscale zapasowej swojej aplikacji Azure.][ChooseWHP]
3. <span data-ttu-id="d5c7f-122">Wybierz warstwę, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="d5c7f-123">Witaj **powiadomienia** kartę będzie flash zielona **Powodzenie** po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="d5c7f-124">Powiązane zasoby są skalowane</span><span class="sxs-lookup"><span data-stu-id="d5c7f-124">Scale related resources</span></span>
<span data-ttu-id="d5c7f-125">Jeśli aplikacja jest zależny od innych usług, takich jak bazy danych SQL Azure lub usługi Azure Storage, można również skalować tych zasobów na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="d5c7f-126">Te zasoby nie mogą być skalowane z hello planu usługi aplikacji i musi być skalowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="d5c7f-127">W **Essentials**, kliknij przycisk hello **grupy zasobów** łącza.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Skalowanie w górę powiązane zasoby aplikacji Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="d5c7f-129">W hello **Podsumowanie** częścią hello **grupy zasobów** bloku, kliknij zasobów, które mają tooscale.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="d5c7f-130">powitania po zrzut ekranu przedstawia zasobów bazy danych SQL i zasobów magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Przejdź tooscale bloku grupy tooresource zapasowej swojej aplikacji Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="d5c7f-132">Dla zasobów bazy danych SQL, kliknij przycisk **ustawienia** > **warstwa cenowa** hello tooscale warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Skalowanie w górę hello bazy danych SQL wewnętrznej bazy danych dla aplikacji Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="d5c7f-134">Można też włączyć [— replikacja geograficzna](../sql-database/sql-database-geo-replication-overview.md) dla swojego wystąpienia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="d5c7f-135">Dla zasobu usługi Magazyn Azure, kliknij przycisk **ustawienia** > **konfiguracji** tooscale Twojego opcji magazynu.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Skalowanie w górę hello Azure Storage konto używane przez aplikację Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="d5c7f-137">Dowiedz się więcej o funkcje programistyczne</span><span class="sxs-lookup"><span data-stu-id="d5c7f-137">Learn about developer features</span></span>
<span data-ttu-id="d5c7f-138">W zależności od warstwy cenowej hello hello zorientowane na developer są dostępne następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="d5c7f-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="d5c7f-139">Liczba bitów</span><span class="sxs-lookup"><span data-stu-id="d5c7f-139">Bitness</span></span>
* <span data-ttu-id="d5c7f-140">Hello **podstawowe**, **standardowe**, i **Premium** warstwy obsługi aplikacji 64-bitowe i 32-bitowych.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="d5c7f-141">Witaj **wolne** i **Shared** planu warstwami obsługuje tylko 32-bitowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="d5c7f-142">Obsługa debugera</span><span class="sxs-lookup"><span data-stu-id="d5c7f-142">Debugger support</span></span>
* <span data-ttu-id="d5c7f-143">Obsługa debugera jest dostępna dla hello **wolne**, **Shared**, i **podstawowe** tryby w jedno połączenie dla danego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="d5c7f-144">Obsługa debugera jest dostępna dla hello **standardowe** i **Premium** tryby na pięć równoczesnych połączeń na plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="d5c7f-145">Dowiedz się więcej o innych funkcjach</span><span class="sxs-lookup"><span data-stu-id="d5c7f-145">Learn about other features</span></span>
* <span data-ttu-id="d5c7f-146">Aby uzyskać szczegółowe informacje o wszystkich pozostałych funkcji w hello usługi aplikacji hello planów, włącznie z ceny i funkcje zainteresowania użytkowników tooall (w tym deweloperzy), zobacz [szczegóły cennika usługi App](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="d5c7f-147">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/) gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d5c7f-148">Bez kart kredytowych są wymagane i nie bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="d5c7f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5c7f-149">Next steps</span></span>
* <span data-ttu-id="d5c7f-150">tooget korzystać z platformy Azure, zobacz [bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d5c7f-151">Aby uzyskać informacje o cenach pomocy technicznej i umowy dotyczącej poziomu usług, odwiedź hello następującego łącza.</span><span class="sxs-lookup"><span data-stu-id="d5c7f-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="d5c7f-152">Informacje o cenach transferu danych</span><span class="sxs-lookup"><span data-stu-id="d5c7f-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="d5c7f-153">Plany pomocy technicznej platformy Azure firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="d5c7f-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="d5c7f-154">Umowy dotyczące poziomu usług</span><span class="sxs-lookup"><span data-stu-id="d5c7f-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="d5c7f-155">Szczegóły cennika bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="d5c7f-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="d5c7f-156">[Maszyny wirtualnej i rozmiary usługi chmury Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="d5c7f-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="d5c7f-157">Szczegóły cennika usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5c7f-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="d5c7f-158">Usługi aplikacji — cennik szczegóły - połączeń SSL</span><span class="sxs-lookup"><span data-stu-id="d5c7f-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="d5c7f-159">Informacje o usłudze Azure App Service najlepszych rozwiązań, w tym tworzenie skalowalnych i elastyczne architektury, zobacz [najlepsze rozwiązania: aplikacje sieci Web usługi aplikacji Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5c7f-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="d5c7f-160">Temat skalowania aplikacji usługi App Service można obejrzeć hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="d5c7f-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="d5c7f-161">Gdy tooScale Azure Websites — Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="d5c7f-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="d5c7f-162">Automatyczne skalowanie witryn sieci Web Azure, procesora CPU lub zaplanowane — z Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="d5c7f-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="d5c7f-163">Jak Azure skalowalność witryn sieci Web - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="d5c7f-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
