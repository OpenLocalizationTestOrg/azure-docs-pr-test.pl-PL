---
title: "zadania zarządzania usługi chmury aaaCommon | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze toomanage w hello portalu Azure. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="14a34-104">W jaki sposób tooManage usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="14a34-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14a34-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14a34-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="14a34-106">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14a34-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="14a34-107">W hello **usługi w chmurze (klasyczne)** obszaru hello Azure portalu, można zaktualizować roli usługi lub wdrożenie, podwyższyć poziom tooproduction wdrożenia etapowego, Połącz usługi w chmurze tooyour zasobów widać hello zasobów zależności skali razem hello zasobów i usunąć usługi w chmurze lub wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="14a34-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="14a34-108">Więcej informacji na temat sposobu tooscale usługi w chmurze jest dostępna [tutaj](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="14a34-109">Porady: aktualizowanie roli usługi w chmurze lub wdrożenia</span><span class="sxs-lookup"><span data-stu-id="14a34-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="14a34-110">Jeśli potrzebujesz kodu aplikacji hello tooupdate dla usługi w chmurze użyj **aktualizacji** na powitania chmury usługi bloku.</span><span class="sxs-lookup"><span data-stu-id="14a34-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="14a34-111">Można aktualizować jedną rolę lub wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="14a34-111">You can update a single role or all roles.</span></span> <span data-ttu-id="14a34-112">tooupdate, możesz przekazać pakiet usługi lub pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="14a34-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="14a34-113">W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma tooupdate.</span><span class="sxs-lookup"><span data-stu-id="14a34-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="14a34-114">Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="14a34-115">W bloku powitania kliknij hello **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a34-115">In hello blade, click hello **Update** button.</span></span>

    ![Przycisk Aktualizuj](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="14a34-117">Zaktualizuj hello wdrożenia przy użyciu nowego pliku pakietu usługi (cspkg) i pliku konfiguracji usługi (cscfg).</span><span class="sxs-lookup"><span data-stu-id="14a34-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="14a34-119">**Opcjonalnie** hello etykieta wdrożenia i konto magazynu hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="14a34-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="14a34-120">W przypadku ról tylko jedno wystąpienie roli, należy wybrać hello **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** tooenable hello uaktualnienia tooproceed.</span><span class="sxs-lookup"><span data-stu-id="14a34-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="14a34-121">Każda rola ma co najmniej dwa wystąpienia roli (maszyny wirtualne) Azure tylko można gwarantuje dostępność usługi 99,95% podczas aktualizacji usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="14a34-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="14a34-122">Dwa wystąpienia roli jednej maszyny wirtualnej przetwarza żądania klientów podczas aktualizowania jest hello innych.</span><span class="sxs-lookup"><span data-stu-id="14a34-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="14a34-123">Sprawdź **rozpocząć wdrażanie** aktualizacji hello toohave stosowane po zakończeniu przekazywania hello hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="14a34-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="14a34-124">Kliknij przycisk **OK** toobegin aktualizacji hello usługi.</span><span class="sxs-lookup"><span data-stu-id="14a34-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="14a34-125">Porady: Zamień toopromote wdrożeń tooproduction wdrożenia etapowego</span><span class="sxs-lookup"><span data-stu-id="14a34-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="14a34-126">Po zdecydować toodeploy nową wersję usługi w chmurze, etap i przetestować w środowisku przemieszczania usługi chmury z nową wersją.</span><span class="sxs-lookup"><span data-stu-id="14a34-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="14a34-127">Użyj **wymiany** adresy URL hello tooswitch przez które hello dwa wdrożenia są opisane i promowania nowego tooproduction wersji.</span><span class="sxs-lookup"><span data-stu-id="14a34-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="14a34-128">Można wymienić wdrożenia od hello **usługi w chmurze** strony lub hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="14a34-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="14a34-129">W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma tooupdate.</span><span class="sxs-lookup"><span data-stu-id="14a34-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="14a34-130">Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="14a34-131">W bloku powitania kliknij hello **wymiany** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a34-131">In hello blade, click hello **Swap** button.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="14a34-133">Witaj następujące monit o potwierdzenie zostanie otwarty.</span><span class="sxs-lookup"><span data-stu-id="14a34-133">hello following confirmation prompt opens.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="14a34-135">Po sprawdzeniu informacji o wdrożeniu powitania kliknij **OK** tooswap hello wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="14a34-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="14a34-136">wymiany wdrożenia Hello odbywa się szybko ponieważ hello jedynym elementem, który zmienia hello wirtualnych adresów IP (VIP) w przypadku wdrożeń hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="14a34-137">toosave obliczeń kosztów, możesz usunąć hello przemieszczania wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="14a34-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="14a34-138">Często zadawane pytania dotyczące wymiany wdrożenia</span><span class="sxs-lookup"><span data-stu-id="14a34-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="14a34-139">**Jakie są wymagania wstępne hello na wymiany wdrożenia?**</span><span class="sxs-lookup"><span data-stu-id="14a34-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="14a34-140">Istnieją dwa kluczowe wymagania wstępne dotyczące wymiany pomyślne wdrożenie:</span><span class="sxs-lookup"><span data-stu-id="14a34-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="14a34-141">Jeśli chcesz toouse statycznego adresu IP dla Twojego miejsca produkcji, musi zarezerwować jeden dla miejsca przemieszczania również.</span><span class="sxs-lookup"><span data-stu-id="14a34-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="14a34-142">W przeciwnym razie wymiany hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="14a34-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="14a34-143">Wszystkie wystąpienia ról musi być uruchomiona, zanim będzie można wykonać hello wymiany.</span><span class="sxs-lookup"><span data-stu-id="14a34-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="14a34-144">Możliwość sprawdzenia stanu hello swoich wystąpień, w bloku omówienie hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="14a34-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="14a34-145">Alternatywnie można użyć hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) polecenia w programie Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14a34-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="14a34-146">Aktualizacje systemu operacyjnego gościa i naprawianie operacji usługi może również spowodować wdrożenia zamienia toofail.</span><span class="sxs-lookup"><span data-stu-id="14a34-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="14a34-147">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z wdrażaniem usługi chmury](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="14a34-148">**Zamiana wpływa negatywnie przestojów w przypadku mojej aplikacji? Jak należy ją obsługuje?**</span><span class="sxs-lookup"><span data-stu-id="14a34-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="14a34-149">Zgodnie z opisem w ostatniej sekcji hello, wymiany wdrożenia jest zazwyczaj szybkie, ponieważ jest on tylko zmiany konfiguracji usługi równoważenia obciążenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="14a34-150">W niektórych przypadkach jednak może potrwać co najmniej 10 sekund i powodować błędy połączeń przejściowej.</span><span class="sxs-lookup"><span data-stu-id="14a34-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="14a34-151">toolimit wpływ tooyour klientów, rozważ zaimplementowanie [Logika ponawiania klienta](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="14a34-152">Porady: łączenie usługi w chmurze tooa zasobów</span><span class="sxs-lookup"><span data-stu-id="14a34-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="14a34-153">Witaj portalu Azure nie łączy zasobów ze sobą, jak jest hello bieżącego klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="14a34-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="14a34-154">Zamiast tego należy wdrożyć dodatkowe zasoby toohello tej samej grupie zasobów używanych przez hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="14a34-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="14a34-155">Porady: usuwanie wdrożeń i usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="14a34-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="14a34-156">Aby można było usunąć usługi w chmurze, należy usunąć poszczególnych istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="14a34-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="14a34-157">toosave obliczeń kosztów, możesz usunąć hello przemieszczania wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="14a34-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="14a34-158">Rozliczenie jest kosztów obliczeniowe dla wystąpień roli wdrożone, które zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="14a34-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="14a34-159">Za pomocą następującej procedury toodelete hello wdrożenia lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="14a34-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="14a34-160">W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="14a34-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="14a34-161">Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="14a34-162">W bloku powitania kliknij hello **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a34-162">In hello blade, click hello **Delete** button.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="14a34-164">Można usunąć usługi w chmurze całego hello sprawdzając **Cloud service i jej wdrożenia** lub wybierz albo hello **wdrożenia produkcyjnego** lub hello **przemieszczania — wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="14a34-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="14a34-166">Kliknij przycisk hello **usunąć** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="14a34-167">usługi w chmurze hello toodelete kliknij **usługi w chmurze Delete**.</span><span class="sxs-lookup"><span data-stu-id="14a34-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="14a34-168">Następnie na powitania monit o potwierdzenie, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="14a34-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="14a34-169">Po usunięciu usługi w chmurze, skonfigurowano pełnego monitorowania, należy usunąć dane hello ręcznie z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="14a34-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="14a34-170">Informacje o którym toofind hello metryki tabel, zobacz [to](cloud-services-how-to-monitor.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="14a34-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="14a34-171">Porady: więcej informacji o wdrożeniach nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="14a34-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="14a34-172">Witaj **omówienie** bloku ma pasek stanu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="14a34-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="14a34-173">Po kliknięciu przycisku paska hello nowy blok otwiera i wyświetla informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="14a34-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="14a34-174">Jeśli wdrożenie hello nie zawiera żadnych błędów, blok informacji hello jest pusta.</span><span class="sxs-lookup"><span data-stu-id="14a34-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="14a34-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14a34-176">Next steps</span></span>
* <span data-ttu-id="14a34-177">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="14a34-178">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="14a34-179">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="14a34-180">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14a34-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
