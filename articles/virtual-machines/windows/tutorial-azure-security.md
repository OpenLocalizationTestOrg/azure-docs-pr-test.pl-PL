---
title: "aaaAzure Centrum zabezpieczeń i systemu Windows maszyny wirtualne na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zabezpieczeń dla maszyny wirtualnej systemu Windows Azure z Centrum zabezpieczeń Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="2d9ad-103">Monitorowanie zabezpieczeń maszyny wirtualnej przy użyciu Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2d9ad-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="2d9ad-104">Centrum zabezpieczeń Azure ułatwia wgląd we Azure zasobu rozwiązania w zakresie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="2d9ad-105">Centrum zabezpieczeń zapewnia zintegrowane zabezpieczenia monitorowania.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="2d9ad-106">Można wykryć zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="2d9ad-107">Z tego samouczka, dowiesz się o Centrum zabezpieczeń Azure i jak:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="2d9ad-108">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="2d9ad-108">Set up data collection</span></span>
> * <span data-ttu-id="2d9ad-109">Ustawianie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-109">Set up security policies</span></span>
> * <span data-ttu-id="2d9ad-110">Wyświetl i rozwiąż problemy z konfiguracją kondycji</span><span class="sxs-lookup"><span data-stu-id="2d9ad-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="2d9ad-111">Przejrzyj wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="2d9ad-112">Omówienie Centrum zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-112">Security Center overview</span></span>

<span data-ttu-id="2d9ad-113">Centrum zabezpieczeń identyfikuje potencjalne problemy z konfiguracją maszyny wirtualnej (VM), a Ustawianie zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="2d9ad-114">Mogą one obejmować maszyn wirtualnych, których brakuje grup zabezpieczeń sieci niezaszyfrowane dyski i atakami siłowymi protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="2d9ad-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="2d9ad-115">Witaj informacje są wyświetlane na pulpicie nawigacyjnym Centrum zabezpieczeń hello na wykresach łatwe do odczytania.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="2d9ad-116">pulpit nawigacyjny Centrum zabezpieczeń w hello portalu Azure, w menu hello, wybierz hello tooaccess **Centrum zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="2d9ad-117">Na pulpicie nawigacyjnym hello można wyświetlić hello kondycji zabezpieczeń środowiska Azure, Znajdź liczbę zalecanych rozwiązań i wyświetlić bieżący stan hello alertów zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="2d9ad-118">Każdy toosee wysokiego poziomu wykresu można rozwinąć więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-118">You can expand each high-level chart toosee more detail.</span></span>

![Pulpit nawigacyjny Centrum zabezpieczeń](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="2d9ad-120">Centrum zabezpieczeń wykracza poza danych odnajdywania tooprovide zalecenia dotyczące problemów, które wykryje.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="2d9ad-121">Na przykład jeśli maszyna wirtualna została wdrożona bez dołączonego sieciowej grupy zabezpieczeń, Centrum zabezpieczeń wyświetla zalecenia, korygowania prostych kroków, które można wykonać.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="2d9ad-122">Otrzymasz automatycznego korygowania bez opuszczania kontekstu hello Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Zalecenia](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="2d9ad-124">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="2d9ad-124">Set up data collection</span></span>

<span data-ttu-id="2d9ad-125">Zanim będzie mógł pobrać widoczność w konfiguracjach zabezpieczeń maszyny Wirtualnej, należy tooset się zbieranie danych Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="2d9ad-126">Obejmuje to włączenie funkcji zbierania danych i tworzenie toohold zbierane dane konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="2d9ad-127">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="2d9ad-128">Aby uzyskać **zbierania danych**, wybierz pozycję **na**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="2d9ad-129">Wybierz konto magazynu toocreate **wybierz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="2d9ad-130">Następnie wybierz opcję **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="2d9ad-131">Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="2d9ad-132">agenta zbierania danych Centrum zabezpieczeń Hello jest instalowany na wszystkich maszynach wirtualnych, a rozpoczęciem zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="2d9ad-133">Skonfiguruj zasady zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-133">Set up a security policy</span></span>

<span data-ttu-id="2d9ad-134">Zasady zabezpieczeń są toodefine używane hello elementy, dla których Centrum zabezpieczeń służy do zbierania danych i podano zalecenia.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="2d9ad-135">Można zastosować zasady zabezpieczeń toodifferent zestawy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="2d9ad-136">Mimo że domyślnie zasobów platformy Azure są sprawdzane dla wszystkich elementów zasad, można wyłączyć elementy poszczególnych zasad dla wszystkich zasobów platformy Azure lub dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="2d9ad-137">Aby uzyskać szczegółowe informacje na temat zasad zabezpieczeń Centrum zabezpieczeń, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="2d9ad-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="2d9ad-138">tooset się zasady zabezpieczeń dla wszystkich zasobów systemu Azure:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="2d9ad-139">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="2d9ad-140">Wybierz **zasady zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="2d9ad-141">Włącz lub Wyłącz zasady elementów, które mają tooapply tooall zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="2d9ad-142">Po wybraniu ustawienia, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="2d9ad-143">Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="2d9ad-144">tooset politykę dla określonej grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="2d9ad-145">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zasady zabezpieczeń**, a następnie wybierz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="2d9ad-146">Wybierz **zasady zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="2d9ad-147">Włącz lub wyłącz elementów zasad czy chcesz, aby grupa zasobów toohello tooapply.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="2d9ad-148">W obszarze **dziedziczenia**, wybierz pozycję **Unique**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="2d9ad-149">Po wybraniu ustawienia, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="2d9ad-150">Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="2d9ad-151">Ponadto można wyłączyć zbieranie danych dla określonej grupy zasobów na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="2d9ad-152">W hello poniższy przykład, zostało utworzone unikatowe zasady dla grupy zasobów o nazwie *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="2d9ad-153">W tej zasadzie dysku szyfrowanie i sieci web aplikacji zapory zalecenia są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Unikatowe zasady](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="2d9ad-155">Wyświetl kondycję konfiguracji maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2d9ad-155">View VM configuration health</span></span>

<span data-ttu-id="2d9ad-156">Po utworzeniu włączone zbieranie danych i ustaw zasadę zabezpieczeń, Centrum zabezpieczeń rozpoczyna tooprovide alertów i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="2d9ad-157">Podczas wdrażania maszyn wirtualnych, hello danych kolekcji agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="2d9ad-158">Centrum zabezpieczeń jest następnie wypełniane przy użyciu danych hello nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="2d9ad-159">Aby uzyskać szczegółowe informacje o kondycji konfiguracji maszyny Wirtualnej, zobacz [ochrony maszyn wirtualnych w Centrum zabezpieczeń](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="2d9ad-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="2d9ad-160">Ponieważ dane są zbierane, są agregowane hello kondycja zasobów dla każdej maszyny Wirtualnej i powiązanych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="2d9ad-161">Witaj informacje są wyświetlane na wykresie łatwe do odczytania.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="2d9ad-162">Kondycja zasobów tooview:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-162">tooview resource health:</span></span>

1.  <span data-ttu-id="2d9ad-163">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello w obszarze **kondycja zabezpieczeń zasobów**, wybierz pozycję **obliczeniowe**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="2d9ad-164">Na powitania **obliczeniowe** bloku, wybierz opcję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="2d9ad-165">Ten widok zawiera podsumowanie hello stanu konfiguracji dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Obliczenia bazy danych kondycji](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="2d9ad-167">toosee wszystkie zalecenia dotyczące maszyny Wirtualnej, wybierz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="2d9ad-168">Zalecenia i korygowania są opisane bardziej szczegółowo w następnej sekcji hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="2d9ad-169">Korygowanie problemów z konfiguracją</span><span class="sxs-lookup"><span data-stu-id="2d9ad-169">Remediate configuration issues</span></span>

<span data-ttu-id="2d9ad-170">Po rozpoczęciu toopopulate z danymi konfiguracji Centrum zabezpieczeń zalecenia są wykonywane na podstawie zasad zabezpieczeń hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="2d9ad-171">Na przykład jeśli maszyna wirtualna została skonfigurowana bez skojarzonej sieciowej grupy zabezpieczeń, tworzone są zalecenia toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="2d9ad-172">Lista wszystkich zaleceń wymienionych toosee:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="2d9ad-173">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, wybierz **zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="2d9ad-174">Wybierz określonego zalecenia.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-174">Select a specific recommendation.</span></span> <span data-ttu-id="2d9ad-175">Zostanie wyświetlona lista wszystkich zasobów, dla których ma zastosowanie hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="2d9ad-176">tooapply zalecenie, wybierz określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="2d9ad-177">Wykonaj instrukcje hello czynności korygujące.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="2d9ad-178">W wielu przypadkach Centrum zabezpieczeń zapewnia można wykonać kroki można wykonać tooaddress zalecenie bez opuszczania Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="2d9ad-179">W hello poniższy przykład Centrum zabezpieczeń wykryje grupy zabezpieczeń sieci, która ma nieograniczony reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="2d9ad-180">Na stronie zalecenie hello, można wybrać hello **edytowanie reguły ruchu przychodzącego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="2d9ad-181">zostanie wyświetlone Hello interfejsu użytkownika, która jest wymagana toomodify hello reguły.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Zalecenia](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="2d9ad-183">Zgodnie z zaleceniami zostaną rozwiązane, są one oznaczone jako rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="2d9ad-184">Wyświetl wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-184">View detected threats</span></span>

<span data-ttu-id="2d9ad-185">Ponadto tooresource konfiguracji zaleceń Centrum zabezpieczeń wyświetla alertów wykrywania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="2d9ad-186">Funkcja alerty zabezpieczeń Hello agreguje dane zbierane z każdej maszyny Wirtualnej Azure dzienniki sieci i zagrożenia bezpieczeństwa toodetect rozwiązań partnerskich połączonych względem zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="2d9ad-187">Aby uzyskać szczegółowe informacje o funkcji wykrywania zagrożeń Centrum zabezpieczeń, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="2d9ad-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="2d9ad-188">Funkcja alerty zabezpieczeń Hello wymaga cennik toobe warstwy zwiększyło się z Centrum zabezpieczeń hello *wolne* za*standardowe*.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="2d9ad-189">30-dniowej **bezpłatnej wersji próbnej** jest dostępna w przypadku przenoszenia toothis wyższej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="2d9ad-190">Warstwa cenowa hello toochange:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="2d9ad-191">Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, kliknij przycisk **zasady zabezpieczeń**, a następnie wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="2d9ad-192">Wybierz **warstwa cenowa**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="2d9ad-193">Wybierz hello nową warstwę, a następnie wybierz **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="2d9ad-194">Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="2d9ad-195">Po zmianie hello warstwy cenowej, wykres alerty zabezpieczeń hello rozpoczyna toopopulate wykryciu zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Alerty zabezpieczeń](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="2d9ad-197">Wybierz informacje tooview alertu.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-197">Select an alert tooview information.</span></span> <span data-ttu-id="2d9ad-198">Na przykład możesz wyświetlić opis hello zagrożeń, czas wykrycia hello, wszystkie próby zagrożeń i hello zalecanych czynności naprawczych.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="2d9ad-199">W hello poniższy przykład ataków siłowych RDP wykryto z 294 nieudanych prób RDP.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="2d9ad-200">Zalecane rozwiązanie jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-200">A recommended resolution is provided.</span></span>

![Atak protokołu RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="2d9ad-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d9ad-202">Next steps</span></span>
<span data-ttu-id="2d9ad-203">W tym samouczku Konfigurowanie Centrum zabezpieczeń Azure, a następnie przejrzeć maszyn wirtualnych w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="2d9ad-204">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="2d9ad-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d9ad-205">Konfigurowanie zbierania danych</span><span class="sxs-lookup"><span data-stu-id="2d9ad-205">Set up data collection</span></span>
> * <span data-ttu-id="2d9ad-206">Ustawianie zasad zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-206">Set up security policies</span></span>
> * <span data-ttu-id="2d9ad-207">Wyświetl i rozwiąż problemy z konfiguracją kondycji</span><span class="sxs-lookup"><span data-stu-id="2d9ad-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="2d9ad-208">Przejrzyj wykrytych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2d9ad-208">Review detected threats</span></span>

<span data-ttu-id="2d9ad-209">Następny samouczek toolearn toohello należy poprawić, jak toocreate CI/CD potoku z Visual Studio Team Services i maszyny Wirtualnej systemu Windows usług IIS.</span><span class="sxs-lookup"><span data-stu-id="2d9ad-209">Advance toohello next tutorial toolearn how toocreate a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d9ad-210">Visual Studio Team Services CI/CD potoku</span><span class="sxs-lookup"><span data-stu-id="2d9ad-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
