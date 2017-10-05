---
title: "Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** Zainstaluj program Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="36088-103">Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="36088-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="36088-104">Centrum zabezpieczeń Azure zaleca się, zainstaluj program endpoint protection na maszynach wirtualnych Azure (maszyny wirtualne), jeśli program endpoint protection nie jest już włączona.</span><span class="sxs-lookup"><span data-stu-id="36088-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="36088-105">To zalecenie dotyczy tylko maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36088-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="36088-106">To Przykładowe wdrożenie używa Antimalware firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36088-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="36088-107">Zobacz [integracji partnerskich w Centrum zabezpieczeń Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) lista partnerów zintegrowana z Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="36088-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="36088-108">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="36088-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="36088-109">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="36088-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="36088-110">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="36088-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="36088-111">W **zalecenia** bloku, wybierz opcję **Zainstaluj program Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="36088-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="36088-112">![Wybierz Zainstaluj program Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="36088-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="36088-113">**Zainstaluj program Endpoint Protection** zostanie otwarty blok zawierający listę maszyn wirtualnych bez ochrony punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="36088-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="36088-114">Wybierz z listy maszyn wirtualnych, które chcesz zainstalować program endpoint protection na, a następnie kliknij przycisk **zainstalować na maszynach wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="36088-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="36088-115">![Wybierz maszyny wirtualne, aby zainstalować program Endpoint Protection na][2]</span><span class="sxs-lookup"><span data-stu-id="36088-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="36088-116">**Wybierz program Endpoint Protection** zostanie otwarty blok, aby umożliwić wybranie funkcji ochrony punktów końcowych, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="36088-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="36088-117">W tym przykładzie załóżmy wybierz **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="36088-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="36088-118">![Wybierz program Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="36088-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="36088-119">Dodatkowe informacje dotyczące funkcji ochrony punktów końcowych są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="36088-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="36088-120">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="36088-120">Select **Create**.</span></span>
   <span data-ttu-id="36088-121">![Tworzenie rozwiązania do ochrony przed złośliwym oprogramowaniem][4]</span><span class="sxs-lookup"><span data-stu-id="36088-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="36088-122">Wprowadź ustawienia konfiguracji na **dodać rozszerzenie** bloku, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="36088-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="36088-123">Aby dowiedzieć się więcej o ustawieniach konfiguracji, zobacz [domyślnej i niestandardowej konfiguracji ochrony przed złośliwym kodem](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="36088-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="36088-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) jest teraz aktywny na wybranych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="36088-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="36088-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="36088-125">See also</span></span>
<span data-ttu-id="36088-126">W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń "Zainstaluj program Endpoint Protection".</span><span class="sxs-lookup"><span data-stu-id="36088-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="36088-127">Aby dowiedzieć się więcej na temat włączania Antimalware firmy Microsoft na platformie Azure, zobacz następujący dokument:</span><span class="sxs-lookup"><span data-stu-id="36088-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="36088-128">[Antimalware firmy Microsoft dla usługi w chmurze i maszyn wirtualnych](../security/azure-security-antimalware.md) — Dowiedz się, jak wdrożyć Antimalware firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36088-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="36088-129">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="36088-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="36088-130">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="36088-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="36088-131">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36088-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="36088-132">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36088-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="36088-133">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="36088-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="36088-134">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="36088-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="36088-135">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="36088-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="36088-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="36088-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
