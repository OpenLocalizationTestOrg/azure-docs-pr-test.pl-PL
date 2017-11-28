---
title: "aaaApplication integracja bramy z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="ca93b-103">Omówienie integracji między bramą aplikacji i Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ca93b-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="ca93b-104">Dowiedz się, jak bramy aplikacji i Centrum zabezpieczeń pomaga chronić zasobów aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ca93b-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="ca93b-105">Zapora aplikacji sieci web dla aplikacji bramy (WAF) integruje się z [Centrum zabezpieczeń](../security-center/security-center-intro.md) tooprovide tooprevent bezproblemowe widoku, wykrywanie i reagowanie aplikacji sieci web toounprotected toothreats w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="ca93b-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="ca93b-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ca93b-106">Overview</span></span>

<span data-ttu-id="ca93b-107">Bramy aplikacji zapory aplikacji sieci Web jest zalecenia w Centrum zabezpieczeń do ochrony aplikacji sieci web z luki w zabezpieczeniach i luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="ca93b-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="ca93b-108">Zasoby sieci Web jest włączona, które nie są chronione przez zapory aplikacji sieci Web są wyświetlane w Centrum zabezpieczeń hello jako zalecenia o wysokim znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="ca93b-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="ca93b-109">Zalecenia dotyczące zapory aplikacji sieci web zostaną wyświetlone na powitania **omówienie** w obszarze **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![Integracja z Centrum zabezpieczeń][1]

<span data-ttu-id="ca93b-111">Kliknięcie żadnych zaleceń dotyczących zapory aplikacji sieci web zostanie otwarty nowy blok zawierającego szczegóły hello hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="ca93b-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="ca93b-112">Dodaj zasób sieci web aplikacji zapory tooan istniejących</span><span class="sxs-lookup"><span data-stu-id="ca93b-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="ca93b-113">Przejdź za**więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na powitania **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="ca93b-114">Na powitania **Centrum zabezpieczeń — aplikacje** bloku hello tabela zawiera listę aplikacji, wykrytych przez Centrum zabezpieczeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplikacje sieci Web][3]

<span data-ttu-id="ca93b-116">Klikając aplikacji sieci web z krytyczny problem, możesz uzyskać hello **kondycja zabezpieczeń aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="ca93b-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="ca93b-117">W poniższym obrazie hello hello aplikacji sieci web, która nie jest chroniona przez zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ca93b-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![zasoby sieci Web, które nie są chronione][2]

<span data-ttu-id="ca93b-119">Kliknij przycisk **Dodawanie zapory aplikacji sieci web** w obszarze **zalecenia** tooopen hello **Dodawanie zapory aplikacji sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="ca93b-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="ca93b-120">Jeśli nie masz istniejącą bramę aplikacji lub mają toocreate nowy, kliknij przycisk **Utwórz nowy** i na powitania **Tworzenie nowej zapory aplikacji sieci Web** bloku, a następnie kliknij przycisk **Microsoft - Brama aplikacji w**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="ca93b-121">Powoduje to przejście przez toocreate kroki hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="ca93b-122">W tym momencie aplikacji sieci web jest dodawany jako zasobu chronionego, Centrum zabezpieczeń teraz śledzi, że ten zasób jest chroniony przez zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ca93b-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="ca93b-123">To nie Dodaj jako członka puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ca93b-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="ca93b-124">Jeśli masz istniejącą bramę aplikacji, można go w **użyć istniejącego rozwiązania**</span><span class="sxs-lookup"><span data-stu-id="ca93b-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Blok dodawania zapory aplikacji sieci Web][4]

<span data-ttu-id="ca93b-126">Dodawanie bramę aplikacji tooan aplikacji sieci web za pomocą Centrum zabezpieczeń nie powoduje dodania hello zasobu jako członka puli wewnętrznej bazy danych, to należy wykonać w zasobu bramy aplikacji hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ca93b-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="ca93b-127">Dodaj zasób tooan istniejących zapory aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ca93b-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="ca93b-128">Przejdź za**więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na powitania **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **rozwiązania partnerskie**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="ca93b-129">Pokaż istniejącej bramy aplikacji obsługującej Centrum zabezpieczeń w hello **rozwiązań partnerskich** bloku.</span><span class="sxs-lookup"><span data-stu-id="ca93b-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![rozwiązania partnerskie][7]

<span data-ttu-id="ca93b-131">Kliknij przycisk **Połącz aplikację** tooopen hello **łączenie aplikacji** bloku, w tym miejscu można skorzystać hello opcje tooselect istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="ca93b-132">Wybierz tooprotect aplikacji hello i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="ca93b-133">Nie dodaje hello puli zaplecza toohello aplikacji sieci web z bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca93b-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="ca93b-134">Ustawia to zasoby hello jako zasobu chronionego, Centrum zabezpieczeń można śledzić.</span><span class="sxs-lookup"><span data-stu-id="ca93b-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="ca93b-135">zasób hello tooadd jako element członkowski puli wewnętrznej bazy danych, należy to zrobić na bramie aplikacji hello, w bieżącym bloku powitania kliknij **Konsola rozwiązań** toobe podjęte zasobu bramy aplikacji toohello umieszczane hello sieci web Pula zaplecza toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![aplikacje rozwiązania partnerskie][6]

## <a name="finalize-configuration"></a><span data-ttu-id="ca93b-137">Finalizowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ca93b-137">Finalize configuration</span></span>

<span data-ttu-id="ca93b-138">Centrum zabezpieczeń ścieżki aplikacji dodany tooan bramy aplikacji jako chronionego zasobu.</span><span class="sxs-lookup"><span data-stu-id="ca93b-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="ca93b-139">Monitoruje kondycję hello tego zasobu i zapewnia, że jest chroniony przez bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="ca93b-140">Witaj następnym krokiem jest tooadd hello prywatnego adresu IP, publiczny adres IP lub kartę interfejsu Sieciowego w puli zaplecza toohello maszyny wirtualnej bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca93b-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="ca93b-141">Dopóki nie jest to dodatkowe zalecenia **Finalizuj ochronę aplikacji** jest wyświetlany dopiero po dodaniu hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="ca93b-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![Blok dodawania zapory aplikacji sieci Web][5]

## <a name="security-alerts"></a><span data-ttu-id="ca93b-143">Alerty zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ca93b-143">Security Alerts</span></span>

<span data-ttu-id="ca93b-144">Centrum zabezpieczeń poruszanie się w obrębie zbyt**wykrywania** > **alerty zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="ca93b-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="ca93b-145">W tym miejscu możesz znaleźć alerty zapory aplikacji sieci Web z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca93b-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="ca93b-146">Alerty są przerwane przez reguły zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ca93b-146">Alerts are broken down by WAF rule.</span></span>

![alerty zabezpieczeń][8]

<span data-ttu-id="ca93b-148">Kliknięcie reguła określi Lista alertów dla tej określonej reguły zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ca93b-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="ca93b-149">Każdy alert zawiera dodatkowe szczegóły znajdowanie hello.</span><span class="sxs-lookup"><span data-stu-id="ca93b-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="ca93b-150">Szczegóły Hello udostępnienia bramy aplikacji toohello łącza.</span><span class="sxs-lookup"><span data-stu-id="ca93b-150">hello details provide a link toohello application gateway.</span></span>
 
![Szczegóły alertu][9]

## <a name="next-steps"></a><span data-ttu-id="ca93b-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca93b-152">Next steps</span></span>

<span data-ttu-id="ca93b-153">jak Zapora aplikacji sieci web tooenable na istniejącą bramę aplikacji, odwiedź stronę toolearn [Tworzenie lub aktualizacja bramy aplikacji Azure z zapory aplikacji sieci web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="ca93b-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png