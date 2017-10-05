---
title: "Dodawanie zapory aplikacji sieci web w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera implementowania zaleceń Centrum zabezpieczeń Azure ** Dodaj sieci web aplikacji zapory ** i ** finalizowanie ochrony aplikacji **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: d04a07237029953d8a9b20704d85e852ce45d867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="aeb8d-103">Dodawanie zapory aplikacji sieci web w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="aeb8d-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="aeb8d-104">Centrum zabezpieczeń Azure może zalecić Dodawanie zapory aplikacji sieci web (WAF) z partnerem firmy Microsoft w celu zabezpieczenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="aeb8d-105">Ten dokument przeprowadzi Cię przez przykładem zastosowania tego zalecenia.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="aeb8d-106">Wszelkie publicznego połączonej adresu IP (IP poziomie wystąpienia lub IP równoważenia obciążenia) zawierający sieciową grupę zabezpieczeń skojarzoną z portami Otwórz przychodzący sieci web (80,443) jest wyświetlane zalecenie zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="aeb8d-107">Centrum zabezpieczeń zaleca się zainicjowanie obsługi zapory aplikacji sieci Web pomagających chronić przed atakami przeznaczonych dla aplikacji sieci web na maszynach wirtualnych i środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="aeb8d-108">Środowisko aplikacji (ASE) jest [Premium](https://azure.microsoft.com/pricing/details/app-service/) opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi App service.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="aeb8d-109">Aby dowiedzieć się więcej na temat ASE, zobacz [dokumentację środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="aeb8d-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aeb8d-110">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="aeb8d-111">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="aeb8d-112">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="aeb8d-112">Implement the recommendation</span></span>
1. <span data-ttu-id="aeb8d-113">W **zalecenia** bloku, wybierz opcję **zabezpieczenia aplikacji sieci web za pomocą zapory aplikacji sieci web**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="aeb8d-114">![Zabezpieczanie aplikacji sieci web][1]</span><span class="sxs-lookup"><span data-stu-id="aeb8d-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="aeb8d-115">W **zabezpieczenia aplikacji sieci web za pomocą zapory aplikacji sieci web** bloku, wybierz aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="aeb8d-116">**Dodawanie zapory aplikacji sieci Web** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="aeb8d-117">![Dodawanie zapory aplikacji sieci Web][2]</span><span class="sxs-lookup"><span data-stu-id="aeb8d-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="aeb8d-118">Możesz użyć istniejących zapory aplikacji sieci web, jeśli jest dostępny, lub można utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="aeb8d-119">W tym przykładzie nie dostępnych żadnych istniejących WAFs, utworzymy zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="aeb8d-120">Aby utworzyć zapory aplikacji sieci Web, należy wybrać z listy partnerów zintegrowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="aeb8d-121">W tym przykładzie mamy wybierz **zapory aplikacji sieci Web Barracuda**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="aeb8d-122">**Zapory aplikacji sieci Web Barracuda** zostanie otwarty blok informacjami o rozwiązaniem partnerskim.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="aeb8d-123">Wybierz **Utwórz** w bloku informacji.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-123">Select **Create** in the information blade.</span></span>

   ![Blok informacji zapory][3]

6. <span data-ttu-id="aeb8d-125">**Nowa Zapora aplikacji sieci Web** zostanie otwarty blok, których można wykonywać **konfiguracji maszyny Wirtualnej** kroki i podaj **informacji zapory aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="aeb8d-126">Wybierz **konfiguracji maszyny Wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="aeb8d-127">W **konfiguracji maszyny Wirtualnej** bloku, wprowadź informacje wymagane do aż maszynę wirtualną, która uruchamia zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="aeb8d-128">![Konfiguracja maszyny Wirtualnej][4]</span><span class="sxs-lookup"><span data-stu-id="aeb8d-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="aeb8d-129">Wróć do **Nowa Zapora aplikacji sieci Web** bloku, a następnie wybierz **informacji zapory aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="aeb8d-130">W **informacji zapory aplikacji sieci Web** bloku, należy skonfigurować zapory aplikacji sieci Web, sama.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="aeb8d-131">Krok 7 można skonfigurować maszyny wirtualnej, na którym działa zapory aplikacji sieci Web i krok 8 umożliwia udostępnianie zapory aplikacji sieci Web, sama.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="aeb8d-132">Finalizuj ochronę aplikacji</span><span class="sxs-lookup"><span data-stu-id="aeb8d-132">Finalize application protection</span></span>
1. <span data-ttu-id="aeb8d-133">Wróć do **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="aeb8d-134">Wygenerowano nowy wpis po utworzeniu zapory aplikacji sieci Web, nazywany **Finalizuj ochronę aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="aeb8d-135">Ten wpis informuje o tym, trzeba wykonać proces faktycznie Podłączanie zapory aplikacji sieci Web w sieci wirtualnej platformy Azure, dzięki czemu można chronić aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>

   ![Finalizuj ochronę aplikacji][5]

2. <span data-ttu-id="aeb8d-137">Wybierz **Finalizuj ochronę aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="aeb8d-138">Zostanie otwarty nowy blok.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-138">A new blade opens.</span></span> <span data-ttu-id="aeb8d-139">Widać, czy istnieje aplikacja sieci web, która musi mieć ruch przekierowane.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="aeb8d-140">Wybierz aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-140">Select the web application.</span></span> <span data-ttu-id="aeb8d-141">Zostanie otwarty blok zawierający kroki dla finalizowanie konfiguracji zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="aeb8d-142">Wykonaj kroki, a następnie wybierz **ograniczania ruchu**.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="aeb8d-143">Centrum zabezpieczeń następnie wykonuje w górę okablowania.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-143">Security Center then does the wiring-up for you.</span></span>

   ![Ograniczanie ruchu][6]

> [!NOTE]
> <span data-ttu-id="aeb8d-145">Wiele aplikacji sieci web w Centrum zabezpieczeń można chronić, dodając te aplikacje do istniejących wdrożeń zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="aeb8d-146">Dzienniki z tym zapory aplikacji sieci Web teraz są w pełni zintegrowane.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="aeb8d-147">Centrum zabezpieczeń można uruchomić automatycznie zbierania i analizowania dzienników, aby go powierzchni alerty zabezpieczeń ważnych dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb8d-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aeb8d-148">Next steps</span></span>
<span data-ttu-id="aeb8d-149">Ten dokument pokazano sposób wykonania zalecenia Centrum zabezpieczeń "Dodaj aplikację sieci web".</span><span class="sxs-lookup"><span data-stu-id="aeb8d-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="aeb8d-150">Aby dowiedzieć się więcej o konfigurowaniu zapory aplikacji sieci web, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="aeb8d-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="aeb8d-151">Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="aeb8d-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="aeb8d-152">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="aeb8d-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="aeb8d-153">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="aeb8d-154">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="aeb8d-155">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="aeb8d-156">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="aeb8d-157">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="aeb8d-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="aeb8d-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
