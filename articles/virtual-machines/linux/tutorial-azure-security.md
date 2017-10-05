---
title: "Maszyny wirtualne w Centrum zabezpieczeń Azure i systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zabezpieczeń dla maszyny wirtualnej systemu Linux platformy Azure z Centrum zabezpieczeń Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7f76da8cd5f4299c64c6e99d0521829c454d8c6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="3d67a-103">Monitorowanie zabezpieczeń maszyny wirtualnej przy użyciu Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="3d67a-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="3d67a-104">Centrum zabezpieczeń Azure ułatwia wgląd we Azure zasobu rozwiązania w zakresie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="3d67a-105">Centrum zabezpieczeń zapewnia zintegrowane zabezpieczenia monitorowania.</span><span class="sxs-lookup"><span data-stu-id="3d67a-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="3d67a-106">Można wykryć zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone.</span><span class="sxs-lookup"><span data-stu-id="3d67a-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="3d67a-107">Z tego samouczka, dowiesz się o Centrum zabezpieczeń Azure i jak:</span><span class="sxs-lookup"><span data-stu-id="3d67a-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="3d67a-108">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="3d67a-108">Set up data collection</span></span>
> * <span data-ttu-id="3d67a-109">Ustawianie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-109">Set up security policies</span></span>
> * <span data-ttu-id="3d67a-110">Wyświetl i rozwiąż problemy z konfiguracją kondycji</span><span class="sxs-lookup"><span data-stu-id="3d67a-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="3d67a-111">Przejrzyj wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="3d67a-112">Omówienie Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-112">Security Center overview</span></span>

<span data-ttu-id="3d67a-113">Centrum zabezpieczeń identyfikuje potencjalne problemy z konfiguracją maszyny wirtualnej (VM), a Ustawianie zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="3d67a-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="3d67a-114">Mogą one obejmować maszyn wirtualnych, których brakuje grup zabezpieczeń sieci niezaszyfrowane dyski i atakami siłowymi protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="3d67a-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="3d67a-115">Informacje są wyświetlane na pulpicie nawigacyjnym Centrum zabezpieczeń na wykresach łatwe do odczytania.</span><span class="sxs-lookup"><span data-stu-id="3d67a-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="3d67a-116">Aby uzyskać dostępu do pulpitu nawigacyjnego Centrum zabezpieczeń w portalu Azure, w menu wybierz **Centrum zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="3d67a-117">Na pulpicie nawigacyjnym można sprawdzić kondycję zabezpieczeń w środowisku platformy Azure, Znajdź liczbę zalecanych rozwiązań i wyświetlić bieżący stan alertów zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="3d67a-118">Można rozwinąć każdego wysokiego poziomu wykresie, aby zobaczyć więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3d67a-118">You can expand each high-level chart to see more detail.</span></span>

![Pulpit nawigacyjny Centrum zabezpieczeń](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="3d67a-120">Centrum zabezpieczeń wykracza poza podano zalecenia dotyczące problemów wykrytych danych odnajdywania.</span><span class="sxs-lookup"><span data-stu-id="3d67a-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="3d67a-121">Na przykład jeśli maszyna wirtualna została wdrożona bez dołączonego sieciowej grupy zabezpieczeń, Centrum zabezpieczeń wyświetla zalecenia, korygowania prostych kroków, które można wykonać.</span><span class="sxs-lookup"><span data-stu-id="3d67a-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="3d67a-122">Otrzymasz automatycznego korygowania bez opuszczania kontekstu Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![Zalecenia](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="3d67a-124">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="3d67a-124">Set up data collection</span></span>

<span data-ttu-id="3d67a-125">Przed uzyskaniem widoczność w konfiguracjach zabezpieczeń maszyny Wirtualnej, należy skonfigurować zbierania danych Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="3d67a-126">Obejmuje to włączenie funkcji zbierania danych i tworzenie konta magazynu Azure do przechowywania zebranych danych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="3d67a-127">Na pulpicie nawigacyjnym Centrum zabezpieczeń, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="3d67a-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="3d67a-128">Aby uzyskać **zbierania danych**, wybierz pozycję **na**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="3d67a-129">Aby utworzyć konto magazynu, wybierz **wybierz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="3d67a-130">Następnie wybierz opcję **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="3d67a-131">Na **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="3d67a-132">Agenta zbierania danych Centrum zabezpieczeń jest instalowany na wszystkich maszynach wirtualnych, a rozpoczęciem zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="3d67a-133">Skonfiguruj zasady zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-133">Set up a security policy</span></span>

<span data-ttu-id="3d67a-134">Zasady zabezpieczeń są używane do zdefiniowania elementów, dla których Centrum zabezpieczeń służy do zbierania danych i podano zalecenia.</span><span class="sxs-lookup"><span data-stu-id="3d67a-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="3d67a-135">Zasady zabezpieczeń można stosować do różnych grup zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d67a-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="3d67a-136">Mimo że domyślnie zasobów platformy Azure są sprawdzane dla wszystkich elementów zasad, można wyłączyć elementy poszczególnych zasad dla wszystkich zasobów platformy Azure lub dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d67a-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="3d67a-137">Aby uzyskać szczegółowe informacje na temat zasad zabezpieczeń Centrum zabezpieczeń, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3d67a-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="3d67a-138">Aby skonfigurować zasady zabezpieczeń dla wszystkich zasobów systemu Azure:</span><span class="sxs-lookup"><span data-stu-id="3d67a-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="3d67a-139">Na pulpicie nawigacyjnym Centrum zabezpieczeń, wybierz **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="3d67a-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="3d67a-140">Wybierz **zasady zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="3d67a-141">Włącz lub Wyłącz zasady elementów, które chcesz zastosować do wszystkich zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d67a-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="3d67a-142">Po wybraniu ustawienia, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="3d67a-143">Na **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="3d67a-144">Aby skonfigurować zasady dla określonej grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="3d67a-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="3d67a-145">Na pulpicie nawigacyjnym Centrum zabezpieczeń, wybierz **zasady zabezpieczeń**, a następnie wybierz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d67a-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="3d67a-146">Wybierz **zasady zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="3d67a-147">Włącz lub Wyłącz zasady elementów, które chcesz zastosować do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d67a-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="3d67a-148">W obszarze **dziedziczenia**, wybierz pozycję **Unique**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="3d67a-149">Po wybraniu ustawienia, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="3d67a-150">Na **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="3d67a-151">Ponadto można wyłączyć zbieranie danych dla określonej grupy zasobów na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="3d67a-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="3d67a-152">W poniższym przykładzie utworzono unikatowe zasady dla grupy zasobów o nazwie *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="3d67a-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="3d67a-153">W tej zasadzie dysku szyfrowanie i sieci web aplikacji zapory zalecenia są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="3d67a-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Unikatowe zasady](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="3d67a-155">Wyświetl kondycję konfiguracji maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3d67a-155">View VM configuration health</span></span>

<span data-ttu-id="3d67a-156">Po utworzeniu włączone zbieranie danych i ustaw zasadę zabezpieczeń, alertów i zalecenia rozpoczyna się Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="3d67a-157">Podczas wdrażania maszyn wirtualnych, zainstalowano agenta zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="3d67a-158">Centrum zabezpieczeń jest następnie wypełniane przy użyciu danych dla nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="3d67a-159">Aby uzyskać szczegółowe informacje o kondycji konfiguracji maszyny Wirtualnej, zobacz [ochrony maszyn wirtualnych w Centrum zabezpieczeń](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="3d67a-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="3d67a-160">Ponieważ dane są zbierane, kondycja zasobów dla każdej maszyny Wirtualnej i powiązanych zasobów platformy Azure są agregowane.</span><span class="sxs-lookup"><span data-stu-id="3d67a-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="3d67a-161">Informacje są wyświetlane na wykresie łatwe do odczytania.</span><span class="sxs-lookup"><span data-stu-id="3d67a-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="3d67a-162">Aby wyświetlić kondycję zasobu:</span><span class="sxs-lookup"><span data-stu-id="3d67a-162">To view resource health:</span></span>

1.  <span data-ttu-id="3d67a-163">Na zabezpieczenia Centrum pulpitu nawigacyjnego, w obszarze **kondycja zabezpieczeń zasobów**, wybierz pozycję **obliczeniowe**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="3d67a-164">Na **obliczeniowe** bloku, wybierz opcję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="3d67a-165">Ten widok zawiera podsumowanie stanu konfiguracji dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![Obliczenia bazy danych kondycji](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="3d67a-167">Aby wyświetlić wszystkie zalecenia dotyczące maszyny Wirtualnej, wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3d67a-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="3d67a-168">Zalecenia i korekty są opisane bardziej szczegółowo w następnej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="3d67a-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="3d67a-169">Korygowanie problemów z konfiguracją</span><span class="sxs-lookup"><span data-stu-id="3d67a-169">Remediate configuration issues</span></span>

<span data-ttu-id="3d67a-170">Po rozpoczęciu Centrum zabezpieczeń do wypełnienia z danymi konfiguracji zalecenia są wykonywane na podstawie skonfigurowanych zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="3d67a-171">Na przykład jeśli maszyna wirtualna została skonfigurowana bez skojarzonej sieciowej grupy zabezpieczeń, zalecenia dotyczące utworzyć.</span><span class="sxs-lookup"><span data-stu-id="3d67a-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="3d67a-172">Aby wyświetlić listę wszystkich zaleceń:</span><span class="sxs-lookup"><span data-stu-id="3d67a-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="3d67a-173">Na pulpicie nawigacyjnym Centrum zabezpieczeń, wybierz **zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="3d67a-174">Wybierz określonego zalecenia.</span><span class="sxs-lookup"><span data-stu-id="3d67a-174">Select a specific recommendation.</span></span> <span data-ttu-id="3d67a-175">Zostanie wyświetlona lista wszystkich zasobów, dla którego stosuje zalecenia.</span><span class="sxs-lookup"><span data-stu-id="3d67a-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="3d67a-176">Aby zastosować zalecenie, wybierz określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3d67a-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="3d67a-177">Postępuj zgodnie z instrukcjami dotyczącymi czynności korygujące.</span><span class="sxs-lookup"><span data-stu-id="3d67a-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="3d67a-178">W wielu przypadkach Centrum zabezpieczeń zapewnia można wykonać kroki, które można podjąć w celu rozwiązania zalecenie bez opuszczania Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="3d67a-179">W poniższym przykładzie Centrum zabezpieczeń wykryje grupy zabezpieczeń sieci, która ma nieograniczony reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="3d67a-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="3d67a-180">Na stronie zalecenia, można wybrać **edytowanie reguły ruchu przychodzącego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d67a-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="3d67a-181">Zostanie wyświetlony interfejs użytkownika, który jest wymagane do zmodyfikowania reguły.</span><span class="sxs-lookup"><span data-stu-id="3d67a-181">The UI that is needed to modify the rule appears.</span></span> 

![Zalecenia](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="3d67a-183">Zgodnie z zaleceniami zostaną rozwiązane, są one oznaczone jako rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="3d67a-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="3d67a-184">Wyświetl wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-184">View detected threats</span></span>

<span data-ttu-id="3d67a-185">Oprócz zalecenia dotyczące konfiguracji zasobów Centrum zabezpieczeń wyświetla alertów wykrywania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="3d67a-186">Funkcja alerty zabezpieczeń agreguje dane zbierane z każdej maszyny Wirtualnej Azure dzienniki sieci i połączonych rozwiązań partnerskich do wykrywania zagrożeń względem zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d67a-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="3d67a-187">Aby uzyskać szczegółowe informacje o funkcji wykrywania zagrożeń Centrum zabezpieczeń, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="3d67a-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="3d67a-188">Funkcja alerty zabezpieczeń wymaga Centrum zabezpieczeń warstwy cenowej zostać zwiększona z *wolne* do *standardowe*.</span><span class="sxs-lookup"><span data-stu-id="3d67a-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="3d67a-189">30-dniowej **bezpłatnej wersji próbnej** jest dostępne po przejściu do tego wyższej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="3d67a-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="3d67a-190">Aby zmienić warstwę cenową:</span><span class="sxs-lookup"><span data-stu-id="3d67a-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="3d67a-191">Na pulpicie nawigacyjnym Centrum zabezpieczeń, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="3d67a-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="3d67a-192">Wybierz **warstwa cenowa**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="3d67a-193">Wybierz nową warstwę, a następnie wybierz **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="3d67a-194">Na **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3d67a-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="3d67a-195">Po zmianie warstwy cenowej, wykres alerty zabezpieczeń rozpoczyna się do wypełnienia jako zabezpieczeń, które zostały wykryte zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="3d67a-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![Alerty zabezpieczeń](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="3d67a-197">Wybierz alert, aby wyświetlić informacje.</span><span class="sxs-lookup"><span data-stu-id="3d67a-197">Select an alert to view information.</span></span> <span data-ttu-id="3d67a-198">Na przykład można wyświetlić opis to zagrożenie, czas wykrycia wszystkie próby zagrożeń i zalecanych czynności naprawczych.</span><span class="sxs-lookup"><span data-stu-id="3d67a-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="3d67a-199">W poniższym przykładzie ataków siłowych RDP wykryto z 294 nieudanych prób RDP.</span><span class="sxs-lookup"><span data-stu-id="3d67a-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="3d67a-200">Zalecane rozwiązanie jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="3d67a-200">A recommended resolution is provided.</span></span>

![Atak protokołu RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="3d67a-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d67a-202">Next steps</span></span>
<span data-ttu-id="3d67a-203">W tym samouczku Konfigurowanie Centrum zabezpieczeń Azure, a następnie przejrzeć maszyn wirtualnych w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3d67a-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="3d67a-204">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="3d67a-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3d67a-205">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="3d67a-205">Set up data collection</span></span>
> * <span data-ttu-id="3d67a-206">Ustawianie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-206">Set up security policies</span></span>
> * <span data-ttu-id="3d67a-207">Wyświetl i rozwiąż problemy z konfiguracją kondycji</span><span class="sxs-lookup"><span data-stu-id="3d67a-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="3d67a-208">Przejrzyj wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3d67a-208">Review detected threats</span></span>

<span data-ttu-id="3d67a-209">Przejdź do następnego samouczkiem, aby dowiedzieć się więcej o tworzeniu potoku CI/CD z Wpięć, GitHub i Docker.</span><span class="sxs-lookup"><span data-stu-id="3d67a-209">Advance to the next tutorial to learn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3d67a-210">Tworzenie elementu konfiguracji/CD infrastruktury z Wpięć, GitHub i Docker</span><span class="sxs-lookup"><span data-stu-id="3d67a-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

