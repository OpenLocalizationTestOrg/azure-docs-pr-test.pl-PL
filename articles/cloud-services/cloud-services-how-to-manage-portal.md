---
title: "Typowe zadania zarządzania usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie zarządzania usługami w chmurze w portalu Azure. Te przykłady, użyj portalu Azure."
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="68ad2-104">Jak zarządzać usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="68ad2-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68ad2-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="68ad2-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="68ad2-106">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="68ad2-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="68ad2-107">W **usługi w chmurze (klasyczne)** obszaru Azure portalu, można zaktualizować roli usługi lub wdrożenie, podwyższyć poziom wdrożenia etapowego do środowiska produkcyjnego, połączyć zasoby z usługi w chmurze, tak aby widoczne zależności między zasobami i zasoby są skalowane ze sobą i usunąć usługi w chmurze lub wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68ad2-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="68ad2-108">Więcej informacji na temat skalowania usługi w chmurze [tutaj](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="68ad2-109">Porady: aktualizowanie roli usługi w chmurze lub wdrożenia</span><span class="sxs-lookup"><span data-stu-id="68ad2-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="68ad2-110">Jeśli musisz zaktualizować kod aplikacji dla usługi w chmurze, użyj **aktualizacji** w bloku usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="68ad2-111">Można aktualizować jedną rolę lub wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="68ad2-111">You can update a single role or all roles.</span></span> <span data-ttu-id="68ad2-112">Aby zaktualizować, możesz przekazać pakiet usługi lub pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="68ad2-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="68ad2-113">W [portalu Azure][Azure portal], wybierz usługę w chmurze do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="68ad2-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="68ad2-114">Ten krok powoduje otwarcie bloku wystąpienia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="68ad2-115">W bloku, kliknij **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="68ad2-115">In the blade, click the **Update** button.</span></span>

    ![Przycisk Aktualizuj](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="68ad2-117">Aktualizacja wdrożenia przy użyciu nowego pliku pakietu usługi (cspkg) i pliku konfiguracji usługi (cscfg).</span><span class="sxs-lookup"><span data-stu-id="68ad2-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="68ad2-119">**Opcjonalnie** zaktualizować etykietę wdrożenia i konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="68ad2-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="68ad2-120">Jeśli żadnych ról z tylko jednego wystąpienia roli, wybierz **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** aktualizację kontynuować.</span><span class="sxs-lookup"><span data-stu-id="68ad2-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="68ad2-121">Każda rola ma co najmniej dwa wystąpienia roli (maszyny wirtualne) Azure tylko można gwarantuje dostępność usługi 99,95% podczas aktualizacji usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="68ad2-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="68ad2-122">Dwa wystąpienia roli jednej maszyny wirtualnej przetwarza żądania klientów podczas innych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="68ad2-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="68ad2-123">Sprawdź **rozpocząć wdrażanie** mają zastosowane po zakończeniu przekazywania pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="68ad2-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="68ad2-124">Kliknij przycisk **OK** zacząć aktualizacji usługi.</span><span class="sxs-lookup"><span data-stu-id="68ad2-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="68ad2-125">Porady: Zamień wdrożeń, aby promować przemieszczanego wdrożenia do produkcji</span><span class="sxs-lookup"><span data-stu-id="68ad2-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="68ad2-126">Jeśli zdecydujesz się wdrożyć nową wersję usługi w chmurze, etap i przetestować w środowisku przemieszczania usługi chmury z nową wersją.</span><span class="sxs-lookup"><span data-stu-id="68ad2-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="68ad2-127">Użyj **wymiany** przełączyć adresów URL, które są opisane dwa wdrożenia i wspierania nową wersję w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="68ad2-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="68ad2-128">Można wymienić wdrożenia od **usługi w chmurze** strony lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="68ad2-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="68ad2-129">W [portalu Azure][Azure portal], wybierz usługę w chmurze do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="68ad2-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="68ad2-130">Ten krok powoduje otwarcie bloku wystąpienia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="68ad2-131">W bloku, kliknij **wymiany** przycisku.</span><span class="sxs-lookup"><span data-stu-id="68ad2-131">In the blade, click the **Swap** button.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="68ad2-133">Otwiera następujące monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="68ad2-133">The following confirmation prompt opens.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="68ad2-135">Po sprawdzeniu informacji wdrożenia, kliknij przycisk **OK** można zamienić wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68ad2-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="68ad2-136">Wymiany wdrożenia odbywa się szybko ponieważ jedynym elementem, który zmienia się wirtualne adresy IP (VIP) dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68ad2-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="68ad2-137">W celu ograniczenia kosztów obliczeń, można usunąć tymczasowej wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="68ad2-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="68ad2-138">Często zadawane pytania dotyczące wymiany wdrożenia</span><span class="sxs-lookup"><span data-stu-id="68ad2-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="68ad2-139">**Jakie są wymagania wstępne dotyczące wymiany wdrożenia?**</span><span class="sxs-lookup"><span data-stu-id="68ad2-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="68ad2-140">Istnieją dwa kluczowe wymagania wstępne dotyczące wymiany pomyślne wdrożenie:</span><span class="sxs-lookup"><span data-stu-id="68ad2-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="68ad2-141">Jeśli chcesz użyć statycznego adresu IP dla Twojego miejsca produkcji, należy zarezerwować jeden dla miejsca przemieszczania również.</span><span class="sxs-lookup"><span data-stu-id="68ad2-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="68ad2-142">W przeciwnym razie wymiany nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="68ad2-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="68ad2-143">Wszystkie wystąpienia ról musi być uruchomiona, zanim będzie można wykonać wymiany.</span><span class="sxs-lookup"><span data-stu-id="68ad2-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="68ad2-144">Można sprawdzić stan swoich wystąpień, w bloku omówienie portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="68ad2-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="68ad2-145">Alternatywnie można użyć [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) polecenia w programie Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68ad2-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="68ad2-146">Należy pamiętać, że aktualizacje systemu operacyjnego gościa i naprawianie operacji usługi również może spowodować zamiany wdrażania zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="68ad2-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="68ad2-147">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z wdrażaniem usługi chmury](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="68ad2-148">**Zamiana wpływa negatywnie przestojów w przypadku mojej aplikacji? Jak należy ją obsługuje?**</span><span class="sxs-lookup"><span data-stu-id="68ad2-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="68ad2-149">Zgodnie z opisem w ostatniej sekcji, wymiany wdrożenia jest zazwyczaj szybkie, ponieważ jest on tylko zmiany konfiguracji usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="68ad2-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="68ad2-150">W niektórych przypadkach jednak może potrwać co najmniej 10 sekund i powodować błędy połączeń przejściowej.</span><span class="sxs-lookup"><span data-stu-id="68ad2-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="68ad2-151">Aby ograniczyć wpływ na klientów, rozważ zaimplementowanie [Logika ponawiania klienta](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="68ad2-152">Porady: łączenie zasobu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="68ad2-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="68ad2-153">Azure portal nie łączenie zasobów jak w bieżącym portalu klasycznego Azure.</span><span class="sxs-lookup"><span data-stu-id="68ad2-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="68ad2-154">Zamiast tego należy wdrożyć dodatkowe zasoby do tej samej grupy zasobów, które są używane przez usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="68ad2-155">Porady: usuwanie wdrożeń i usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="68ad2-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="68ad2-156">Aby można było usunąć usługi w chmurze, należy usunąć poszczególnych istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68ad2-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="68ad2-157">W celu ograniczenia kosztów obliczeń, można usunąć tymczasowej wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="68ad2-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="68ad2-158">Rozliczenie jest kosztów obliczeniowe dla wystąpień roli wdrożone, które zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="68ad2-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="68ad2-159">Użyj poniższej procedury można usunąć wdrożenia lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="68ad2-160">W [portalu Azure][Azure portal], wybierz usługę w chmurze do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="68ad2-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="68ad2-161">Ten krok powoduje otwarcie bloku wystąpienia usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68ad2-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="68ad2-162">W bloku, kliknij **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="68ad2-162">In the blade, click the **Delete** button.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="68ad2-164">Można usunąć usługi w chmurze całego sprawdzając **Cloud service i jej wdrożenia** lub wybrać opcję **wdrożenia produkcyjnego** lub **przemieszczania — wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="68ad2-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="68ad2-166">Kliknij przycisk **usunąć** znajdujący się u dołu.</span><span class="sxs-lookup"><span data-stu-id="68ad2-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="68ad2-167">Aby usunąć usługi w chmurze, kliknij przycisk **usługi w chmurze Delete**.</span><span class="sxs-lookup"><span data-stu-id="68ad2-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="68ad2-168">Następnie w oknie monitu o potwierdzenie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="68ad2-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="68ad2-169">Po usunięciu usługi w chmurze, a pełne monitorowania jest skonfigurowana, danych trzeba usunąć ręcznie z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="68ad2-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="68ad2-170">Aby uzyskać informacje o tym, gdzie można znaleźć w tabelach metryki, zobacz [to](cloud-services-how-to-monitor.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="68ad2-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="68ad2-171">Porady: więcej informacji o wdrożeniach nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="68ad2-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="68ad2-172">**Omówienie** bloku ma pasek stanu u góry.</span><span class="sxs-lookup"><span data-stu-id="68ad2-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="68ad2-173">Po kliknięciu przycisku paska otwiera nowy blok i wyświetla informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="68ad2-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="68ad2-174">Jeśli wdrożenie nie zawiera żadnych błędów, blok informacji jest pusta.</span><span class="sxs-lookup"><span data-stu-id="68ad2-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="68ad2-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68ad2-176">Next steps</span></span>
* <span data-ttu-id="68ad2-177">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="68ad2-178">Dowiedz się, jak [wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="68ad2-179">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="68ad2-180">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68ad2-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
