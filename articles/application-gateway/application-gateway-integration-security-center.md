---
title: "Integracja bramy aplikacji z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera informacje dotyczące integracji brama aplikacji w Centrum zabezpieczeń Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="22961-103">Omówienie integracji między bramą aplikacji i Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="22961-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="22961-104">Dowiedz się, jak bramy aplikacji i Centrum zabezpieczeń pomaga chronić zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="22961-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="22961-105">Zapora aplikacji sieci web dla aplikacji bramy (WAF) integruje się z [Centrum zabezpieczeń](../security-center/security-center-intro.md) w celu zapewnienia bezproblemowego przeglądu zapobiegające, wykrywania i reagowania na zagrożenia do aplikacji sieci web niechronione w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="22961-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="22961-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="22961-106">Overview</span></span>

<span data-ttu-id="22961-107">Bramy aplikacji zapory aplikacji sieci Web jest zalecenia w Centrum zabezpieczeń do ochrony aplikacji sieci web z luki w zabezpieczeniach i luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="22961-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="22961-108">Zasoby sieci Web jest włączona, które nie są chronione przez zapory aplikacji sieci Web są wyświetlane w Centrum zabezpieczeń jako zalecenia o wysokim znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="22961-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="22961-109">Zalecenia dotyczące zapory aplikacji sieci web zostaną wyświetlone na **omówienie** w obszarze **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="22961-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![Integracja z Centrum zabezpieczeń][1]

<span data-ttu-id="22961-111">Klikając przycisk żadnych zaleceń dotyczących zapory aplikacji sieci web są otwierane w nowym bloku zawierającego szczegóły zalecenia.</span><span class="sxs-lookup"><span data-stu-id="22961-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="22961-112">Dodawanie zapory aplikacji sieci web do istniejącego zasobu</span><span class="sxs-lookup"><span data-stu-id="22961-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="22961-113">Przejdź do **więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="22961-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="22961-114">Na **Centrum zabezpieczeń — aplikacje** bloku, tabela zawiera listę aplikacji, wykrytych przez Centrum zabezpieczeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22961-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplikacje sieci Web][3]

<span data-ttu-id="22961-116">Klikając aplikacji sieci web z krytyczny problem, możesz uzyskać **kondycja zabezpieczeń aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="22961-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="22961-117">Na poniższej ilustracji, aplikacji sieci web, która nie jest chroniony przez zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="22961-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![zasoby sieci Web, które nie są chronione][2]

<span data-ttu-id="22961-119">Kliknij przycisk **Dodawanie zapory aplikacji sieci web** w obszarze **zalecenia** otworzyć **Dodawanie zapory aplikacji sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="22961-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="22961-120">Jeśli nie masz istniejącą bramę aplikacji lub chcesz utworzyć nową, kliknij przycisk **Utwórz nowy** i na **Tworzenie nowej zapory aplikacji sieci Web** bloku, a następnie kliknij przycisk **Microsoft - aplikacji Brama**.</span><span class="sxs-lookup"><span data-stu-id="22961-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="22961-121">Powoduje to przejście kroki, aby utworzyć bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="22961-122">W tym momencie aplikacji sieci web jest dodawany jako zasobu chronionego, Centrum zabezpieczeń teraz śledzi, że ten zasób jest chroniony przez zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="22961-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="22961-123">To nie Dodaj jako członka puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="22961-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="22961-124">Jeśli masz istniejącą bramę aplikacji, można go w **użyć istniejącego rozwiązania**</span><span class="sxs-lookup"><span data-stu-id="22961-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Blok dodawania zapory aplikacji sieci Web][4]

<span data-ttu-id="22961-126">Dodawanie aplikacji sieci web do bramy aplikacji za pomocą Centrum zabezpieczeń nie powoduje dodania zasobu jako członka puli wewnętrznej bazy danych, to należy wykonać w zasobu bramy aplikacji bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="22961-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="22961-127">Dodaj zasób do istniejących zapory aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="22961-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="22961-128">Przejdź do **więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **rozwiązania partnerskie**.</span><span class="sxs-lookup"><span data-stu-id="22961-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="22961-129">Pokaż istniejącej bramy aplikacji obsługującej Centrum zabezpieczeń w **rozwiązań partnerskich** bloku.</span><span class="sxs-lookup"><span data-stu-id="22961-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![rozwiązania partnerskie][7]

<span data-ttu-id="22961-131">Kliknij przycisk **Połącz aplikację** otworzyć **łączenie aplikacji** bloku, w tym miejscu można skorzystać opcji, aby wybrać istniejące aplikacje.</span><span class="sxs-lookup"><span data-stu-id="22961-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="22961-132">Wybierz aplikacje do ochrony i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="22961-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="22961-133">Nie dodaje aplikacji sieci web do puli zaplecza bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="22961-134">Zasoby to ustawienie jako chroniony zasób, Centrum zabezpieczeń można śledzić.</span><span class="sxs-lookup"><span data-stu-id="22961-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="22961-135">Aby dodać zasobu jako członka puli wewnętrznej bazy danych, należy to zrobić na bramie aplikacji w bieżącym bloku można kliknąć **Konsola rozwiązań** podjąć w celu zasobu bramy aplikacji, którym można dodać aplikacji sieci web Pula zaplecza.</span><span class="sxs-lookup"><span data-stu-id="22961-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![aplikacje rozwiązania partnerskie][6]

## <a name="finalize-configuration"></a><span data-ttu-id="22961-137">Finalizowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="22961-137">Finalize configuration</span></span>

<span data-ttu-id="22961-138">Centrum zabezpieczeń śledzi aplikacji dodanych do bramy aplikacji jako chronionego zasobu.</span><span class="sxs-lookup"><span data-stu-id="22961-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="22961-139">Monitoruje kondycję tego zasobu i zapewnia, że jest chroniony przez bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="22961-140">Następnym krokiem jest dodawanie prywatnego adresu IP, publiczny adres IP lub karty Sieciowej maszyny wirtualnej do puli zaplecza bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="22961-141">Dopóki nie jest to dodatkowe zalecenia **Finalizuj ochronę aplikacji** jest wyświetlany, dopóki zasób nie zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="22961-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![Blok dodawania zapory aplikacji sieci Web][5]

## <a name="security-alerts"></a><span data-ttu-id="22961-143">Alerty zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="22961-143">Security Alerts</span></span>

<span data-ttu-id="22961-144">W Centrum zabezpieczeń, przejdź do **wykrywania** > **alerty zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="22961-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="22961-145">W tym miejscu możesz znaleźć alerty zapory aplikacji sieci Web z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="22961-146">Alerty są przerwane przez reguły zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="22961-146">Alerts are broken down by WAF rule.</span></span>

![alerty zabezpieczeń][8]

<span data-ttu-id="22961-148">Kliknięcie reguła określi Lista alertów dla tej określonej reguły zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="22961-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="22961-149">Każdy alert zawiera dodatkowe szczegóły niezgodności.</span><span class="sxs-lookup"><span data-stu-id="22961-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="22961-150">Szczegóły zawierają łącza do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22961-150">The details provide a link to the application gateway.</span></span>
 
![Szczegóły alertu][9]

## <a name="next-steps"></a><span data-ttu-id="22961-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22961-152">Next steps</span></span>

<span data-ttu-id="22961-153">Aby dowiedzieć się, jak włączyć zapory aplikacji sieci web na istniejącą bramę aplikacji, odwiedź stronę [Tworzenie lub aktualizacja bramy aplikacji Azure z zapory aplikacji sieci web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="22961-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png