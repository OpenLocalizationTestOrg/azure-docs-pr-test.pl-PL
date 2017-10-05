---
title: "Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji Azure"
description: "Więcej informacji na temat tworzenia i używania środowiska usługi aplikacji Azure izolowane internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="bb91f-103">Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="bb91f-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="bb91f-104">Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="bb91f-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="bb91f-105">Istnieją dwa sposoby wdrożenia środowiska usługi App Service (ASE):</span><span class="sxs-lookup"><span data-stu-id="bb91f-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="bb91f-106">Z adresów VIP na zewnętrzny adres IP często nazywane ASE zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="bb91f-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="bb91f-107">Z adresów VIP na wewnętrzny adres IP często nazywane ASE ILB, ponieważ wewnętrzny punkt końcowy jest wewnętrzny moduł równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="bb91f-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="bb91f-108">W tym artykule przedstawiono sposób tworzenia ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="bb91f-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="bb91f-109">Omówienie ASE, zobacz [wprowadzenie do środowiska usługi aplikacji][Intro].</span><span class="sxs-lookup"><span data-stu-id="bb91f-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="bb91f-110">Aby dowiedzieć się, jak utworzyć ASE zewnętrznych, zobacz [Tworzenie zewnętrznych ASE][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="bb91f-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="bb91f-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bb91f-111">Overview</span></span> ##

<span data-ttu-id="bb91f-112">Można wdrożyć ASE z punktem końcowym dostęp do Internetu lub adres IP w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb91f-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="bb91f-113">Aby ustawić adres IP adresów sieci wirtualnej, należy wdrożyć ASE z ILB.</span><span class="sxs-lookup"><span data-stu-id="bb91f-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="bb91f-114">Podczas wdrażania sieci ASE z ILB, należy podać:</span><span class="sxs-lookup"><span data-stu-id="bb91f-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="bb91f-115">Własnej domeny, który jest używany podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="bb91f-116">Certyfikat używany do obsługi protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="bb91f-117">Zarządzanie systemem DNS dla domeny.</span><span class="sxs-lookup"><span data-stu-id="bb91f-117">DNS management for your domain.</span></span>

<span data-ttu-id="bb91f-118">W zamian można wykonać czynności takich jak:</span><span class="sxs-lookup"><span data-stu-id="bb91f-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="bb91f-119">Host aplikacji intranetowych bezpiecznie w chmurze, które dostępne za pośrednictwem sieci VPN platformy Azure ExpressRoute lub lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="bb91f-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="bb91f-120">Aplikacje hosta w chmurze, które nie są wymienione w publicznych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="bb91f-121">Utwórz izolowaną internet zaplecza aplikacji, które frontonu aplikacji bezpiecznego można zintegrować z.</span><span class="sxs-lookup"><span data-stu-id="bb91f-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="bb91f-122">Funkcje wyłączone</span><span class="sxs-lookup"><span data-stu-id="bb91f-122">Disabled functionality</span></span> ###

<span data-ttu-id="bb91f-123">Istnieje kilka kwestii, które nie można wykonać, gdy używasz ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="bb91f-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="bb91f-124">Użyj opartych na protokole SSL.</span><span class="sxs-lookup"><span data-stu-id="bb91f-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="bb91f-125">Przypisz adresy IP do określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="bb91f-126">Kup i korzystać z certyfikatu z aplikacji za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="bb91f-127">Można uzyskać certyfikatów bezpośrednio od urzędu certyfikacji i używać ich z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="bb91f-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="bb91f-128">Nie można je uzyskać za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="bb91f-129">Utwórz ILB ASE</span><span class="sxs-lookup"><span data-stu-id="bb91f-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="bb91f-130">Aby utworzyć ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="bb91f-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="bb91f-131">W portalu Azure wybierz **nowy** > **sieci Web i mobilność** > **środowiska usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="bb91f-132">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="bb91f-132">Select your subscription.</span></span>

3. <span data-ttu-id="bb91f-133">Wybierz lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb91f-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="bb91f-134">Wybierz lub Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="bb91f-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="bb91f-135">W przypadku wybrania istniejącej sieci wirtualnej, należy utworzyć podsieci do przechowywania ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="bb91f-136">Upewnij się, że ustawiony rozmiar podsieci, wystarczająco duże, aby pomieścić przyszłego rozwoju Twojej ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="bb91f-137">Firma Microsoft zaleca o rozmiarze `/25`, który 128 adresów i może obsłużyć ASE rozmiar maksymalny.</span><span class="sxs-lookup"><span data-stu-id="bb91f-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="bb91f-138">Możesz wybrać rozmiar minimalny to `/28`.</span><span class="sxs-lookup"><span data-stu-id="bb91f-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="bb91f-139">Po wymaga infrastruktury, ten rozmiar mogą być skalowane do maksymalnie 11 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="bb91f-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="bb91f-140">Przekraczają maksymalną liczbą wystąpień 100 domyślną w planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="bb91f-141">Skalowanie bliskie 100, ale także z bardziej szybkie skalowanie frontonu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="bb91f-142">Wybierz **wirtualnego lokalizacji** > **konfiguracji sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="bb91f-143">Ustaw **typu VIP** do **wewnętrzny**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="bb91f-144">Wprowadź nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="bb91f-144">Enter a domain name.</span></span> <span data-ttu-id="bb91f-145">Ta domena jest używany w przypadku aplikacji utworzone w tym ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="bb91f-146">Istnieją pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="bb91f-146">There are some restrictions.</span></span> <span data-ttu-id="bb91f-147">Nie można go:</span><span class="sxs-lookup"><span data-stu-id="bb91f-147">It can't be:</span></span>

    * <span data-ttu-id="bb91f-148">NET</span><span class="sxs-lookup"><span data-stu-id="bb91f-148">net</span></span>   

    * <span data-ttu-id="bb91f-149">azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="bb91f-149">azurewebsites.net</span></span>

    * <span data-ttu-id="bb91f-150">p.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="bb91f-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="bb91f-151">&lt;asename&gt;. p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="bb91f-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="bb91f-152">Niestandardowa nazwa domeny używane do aplikacji i nazwy domeny używane przez użytkownika ASE nie mogą się nakładać.</span><span class="sxs-lookup"><span data-stu-id="bb91f-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="bb91f-153">Dla ASE ILB z nazwą domeny _contoso.com_, nie można użyć niestandardowych nazw domen dla twojej aplikacji, takich jak:</span><span class="sxs-lookup"><span data-stu-id="bb91f-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="bb91f-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="bb91f-154">www.contoso.com</span></span>

    * <span data-ttu-id="bb91f-155">Abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="bb91f-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="bb91f-156">Abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="bb91f-156">abcd.contoso.com</span></span>

   <span data-ttu-id="bb91f-157">Jeśli znasz nazwy domeny niestandardowej dla aplikacji, należy wybrać domenę dla ASE ILB, który nie występuje konflikt z tymi nazwami domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="bb91f-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="bb91f-158">W tym przykładzie, można użyć przypominać *contoso internal.com* dla domeny Twojej ASE ponieważ nie będących w konflikcie z nazwami domen niestandardowych, które kończą się *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="bb91f-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="bb91f-159">Wybierz **OK**, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-159">Select **OK**, and then select **Create**.</span></span>

    ![Tworzenie środowiska ASE][1]

<span data-ttu-id="bb91f-161">Na **sieci wirtualnej** bloku jest **konfiguracja sieci wirtualnej** opcji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="bb91f-162">Służy on do wybierania zewnętrznego adresu VIP lub wewnętrznego adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="bb91f-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="bb91f-163">Wartość domyślna to **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-163">The default is **External**.</span></span> <span data-ttu-id="bb91f-164">W przypadku wybrania **zewnętrznych**, Twoje ASE używa VIP dostępny z Internetu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="bb91f-165">W przypadku wybrania **wewnętrzne**, Twoje ASE skonfigurowano ILB na adres IP w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb91f-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="bb91f-166">Po wybraniu **wewnętrzne**, możliwość dodawania więcej adresów IP do sieci ASE zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="bb91f-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="bb91f-167">Zamiast tego należy podać domenę ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="bb91f-168">W elemencie ASE z zewnętrznego wirtualnego adresu IP nazwę ASE służy w domenie aplikacji utworzone w tym ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="bb91f-169">Jeśli ustawisz **typu VIP** do **wewnętrzne**, nazwę ASE nie jest używany w domenie dla ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="bb91f-170">Jawnie określ domenę.</span><span class="sxs-lookup"><span data-stu-id="bb91f-170">You specify the domain explicitly.</span></span> <span data-ttu-id="bb91f-171">Jeśli Twoja domena to *contoso.corp.net* i utworzyć aplikację, w tym o nazwie ASE *timereporting*, adres URL dla tej aplikacji jest timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="bb91f-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="bb91f-172">Utwórz aplikację w elemencie ASE ILB</span><span class="sxs-lookup"><span data-stu-id="bb91f-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="bb91f-173">Tworzenie aplikacji w elemencie ASE ILB odbywa się w taki sam sposób tworzenia aplikacji w elemencie ASE normalnie.</span><span class="sxs-lookup"><span data-stu-id="bb91f-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="bb91f-174">W portalu Azure wybierz **nowy** > **sieci Web i mobilność** > **Web** lub **Mobile** lub **interfejsu API Aplikacja**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="bb91f-175">Wprowadź nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="bb91f-176">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="bb91f-176">Select the subscription.</span></span>

4. <span data-ttu-id="bb91f-177">Wybierz lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb91f-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="bb91f-178">Wybierz lub Utwórz plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-178">Select or create an App Service plan.</span></span> <span data-ttu-id="bb91f-179">Jeśli chcesz utworzyć nowy plan usługi aplikacji, wybierz użytkownika ASE jako lokalizację.</span><span class="sxs-lookup"><span data-stu-id="bb91f-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="bb91f-180">Wybierz puli procesów roboczych, w którym ma swój plan usługi aplikacji ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="bb91f-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="bb91f-181">Po utworzeniu planu usługi aplikacji, wybierz Twoje ASE jako lokalizację i puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="bb91f-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="bb91f-182">Po określeniu nazwy aplikacji domeny pod nazwą aplikacji zostało zastąpione przez domenę dla Twojego ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="bb91f-183">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-183">Select **Create**.</span></span> <span data-ttu-id="bb91f-184">Aplikacji są wyświetlane na pulpicie nawigacyjnym, zaznacz **Przypnij do pulpitu nawigacyjnego** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="bb91f-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![Tworzenie planu usługi aplikacji][2]

    <span data-ttu-id="bb91f-186">W obszarze **Nazwa aplikacji**, nazwa domeny jest zaktualizowana w celu odzwierciedlenia domeny Twojej ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="bb91f-187">Sprawdzanie poprawności tworzenia POST ILB ASE</span><span class="sxs-lookup"><span data-stu-id="bb91f-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="bb91f-188">ASE ILB są nieco inne niż z systemem innym niż - ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="bb91f-189">Jak już zanotowane trzeba zarządzać własną DNS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="bb91f-190">Należy również podać swój własny certyfikat dla połączeń HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="bb91f-191">Po utworzeniu sieci ASE, nazwa domeny zawiera określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="bb91f-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="bb91f-192">Nowy element jest wyświetlany w **ustawienie** menu o nazwie **certyfikatu ILB**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="bb91f-193">ASE jest tworzony przy użyciu certyfikatu, który nie określa domeny ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="bb91f-194">Użycie ASE z tego certyfikatu, przeglądarki informuje, że jest on nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="bb91f-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="bb91f-195">Ten certyfikat ułatwia testowanie HTTPS, ale należy przekazać swój własny certyfikat, który jest powiązany z własną domeną ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="bb91f-196">Ten krok jest niezbędny, niezależnie od tego, czy certyfikat z podpisem własnym, czy otrzymanego od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Nazwa domeny ILB ASE][3]

<span data-ttu-id="bb91f-198">Twoje ASE ILB musi mieć prawidłowy certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="bb91f-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="bb91f-199">Użyj certyfikatu wewnętrznego urzędów, kupić certyfikat od zewnętrznego wystawcy lub Użyj certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="bb91f-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="bb91f-200">Niezależnie od źródła certyfikatu SSL, należy poprawnie skonfigurowane następujące atrybuty certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="bb91f-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="bb91f-201">**Temat**: ten atrybut musi mieć ustawioną *.your głównego domeny tutaj.</span><span class="sxs-lookup"><span data-stu-id="bb91f-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="bb91f-202">**Alternatywna nazwa podmiotu**: ten atrybut musi zawierać zarówno **.your głównego domeny tutaj* i **.scm.your-głównego-domeny — w tym miejscu*.</span><span class="sxs-lookup"><span data-stu-id="bb91f-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="bb91f-203">Połączenia SSL do witryny SCM/Kudu skojarzone z każdej aplikacji używać adresu w postaci *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="bb91f-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="bb91f-204">Konwertuj/Zapisz certyfikat jako plik pfx.</span><span class="sxs-lookup"><span data-stu-id="bb91f-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="bb91f-205">Plik PFX musi obejmować wszystkie pośrednie i certyfikaty główne.</span><span class="sxs-lookup"><span data-stu-id="bb91f-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="bb91f-206">Zabezpiecz ją przy użyciu hasła.</span><span class="sxs-lookup"><span data-stu-id="bb91f-206">Secure it with a password.</span></span>

<span data-ttu-id="bb91f-207">Jeśli chcesz utworzyć certyfikat z podpisem własnym, w tym miejscu można użyć poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb91f-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="bb91f-208">Należy użyć nazwy domeny ILB ASE zamiast *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="bb91f-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="bb91f-209">Certyfikat, który generowanie tych poleceń programu PowerShell oflagowane przez przeglądarki, ponieważ certyfikat nie został utworzony przez urząd certyfikacji, który znajduje się w łańcuch zaufania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bb91f-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="bb91f-210">Aby uzyskać certyfikat, któremu ufa przeglądarki, należy przygotować od urzędu certyfikacji komercyjnych w łańcuchu zaufania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bb91f-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Zestaw ILB certyfikatu][4]

<span data-ttu-id="bb91f-212">Aby przekazać własne certyfikaty i testowanie dostępu:</span><span class="sxs-lookup"><span data-stu-id="bb91f-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="bb91f-213">Po utworzeniu ASE, przejdź do ASE interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb91f-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="bb91f-214">Wybierz **ASE** > **ustawienia** > **certyfikatu ILB**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="bb91f-215">Aby ustawić certyfikat ILB, wybierz plik certyfikatu PFX, a następnie wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="bb91f-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="bb91f-216">Ten krok zajmuje trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-216">This step takes some time to process.</span></span> <span data-ttu-id="bb91f-217">Pojawi się komunikat z informacją, że operacja przekazywania jest w toku.</span><span class="sxs-lookup"><span data-stu-id="bb91f-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="bb91f-218">Pobierz adres ILB dla Twojego ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="bb91f-219">Wybierz **ASE** > **właściwości** > **wirtualny adres IP**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="bb91f-220">Tworzenie aplikacji sieci web w sieci ASE po utworzeniu ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="bb91f-221">Tworzenie maszyny Wirtualnej, jeśli nie istnieje w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb91f-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb91f-222">Nie należy próbować utworzyć tej maszyny Wirtualnej w tej samej podsieci co ASE, ponieważ będzie zakończyć się niepowodzeniem lub spowodować problemy.</span><span class="sxs-lookup"><span data-stu-id="bb91f-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="bb91f-223">Ustaw DNS dla domeny ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="bb91f-224">Za pomocą symbolu wieloznacznego i domeny w systemie DNS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="bb91f-225">Proste testy w celu edytowania pliku hosts na maszynie Wirtualnej można ustawić nazwy aplikacji sieci web do adresu VIP IP:</span><span class="sxs-lookup"><span data-stu-id="bb91f-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="bb91f-226">a.</span><span class="sxs-lookup"><span data-stu-id="bb91f-226">a.</span></span> <span data-ttu-id="bb91f-227">Jeśli Twoje ASE ma nazwę domeny _. ilbase.com_ i utworzysz aplikację sieci web o nazwie _mytestapp_, jest skierowana na _mytestapp.ilbase.com_. Następnie ustaw _mytestapp.ilbase.com_ do rozpoznawania adresów ILB.</span><span class="sxs-lookup"><span data-stu-id="bb91f-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="bb91f-228">(W systemie Windows, w pliku hosts wynosi _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="bb91f-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="bb91f-229">b.</span><span class="sxs-lookup"><span data-stu-id="bb91f-229">b.</span></span> <span data-ttu-id="bb91f-230">Aby przetestować wdrożenie publikowania w sieci web lub dostęp do zaawansowanych konsoli, należy utworzyć rekord dla _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="bb91f-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="bb91f-231">Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do http://mytestapp.ilbase.com. (Lub przejdź do niezależnie od Twoja nazwa aplikacji sieci web jest z domeną.)</span><span class="sxs-lookup"><span data-stu-id="bb91f-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="bb91f-232">Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do https://mytestapp.ilbase.com. Jeśli używasz certyfikatu z podpisem własnym, należy zaakceptować braku zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bb91f-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="bb91f-233">Adres IP dla sieci ILB znajduje się w obszarze **adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="bb91f-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="bb91f-234">Ta lista zawiera również adresy IP używane przez zewnętrznych adresów VIP oraz dla ruchu przychodzącego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="bb91f-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![Adres ILB IP][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="bb91f-236">Zadania Web Job, funkcje i ILB ASE</span><span class="sxs-lookup"><span data-stu-id="bb91f-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="bb91f-237">Zarówno funkcje i zadania sieci web są obsługiwane w elemencie ASE ILB, ale portalu pracować z nimi, musi mieć dostęp do sieci do lokacji SCM.</span><span class="sxs-lookup"><span data-stu-id="bb91f-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="bb91f-238">Oznacza to, że przeglądarka musi być na hoście, który jest albo podłączone do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb91f-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="bb91f-239">Gdy używasz usługi Azure Functions w elemencie ASE ILB, może pobrać komunikat o błędzie stwierdzający "nie możemy teraz pobrać funkcji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="bb91f-240">Spróbuj ponownie później."</span><span class="sxs-lookup"><span data-stu-id="bb91f-240">Please try again later."</span></span> <span data-ttu-id="bb91f-241">Ten błąd występuje, ponieważ interfejs użytkownika funkcji wykorzystuje lokacji SCM za pośrednictwem protokołu HTTPS i certyfikatu głównego nie jest w przeglądarce łańcuch zaufania.</span><span class="sxs-lookup"><span data-stu-id="bb91f-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="bb91f-242">Zadania Web Job ma podobny problem.</span><span class="sxs-lookup"><span data-stu-id="bb91f-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="bb91f-243">Aby uniknąć tego problemu, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="bb91f-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="bb91f-244">Dodaj certyfikat do magazynu zaufanych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="bb91f-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="bb91f-245">Odblokowuje to Edge i przeglądarki Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="bb91f-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="bb91f-246">Użyj przeglądarki Chrome i przejdź do witryny SCM najpierw, Zaakceptuj niezaufany certyfikat, a następnie przejdź do portalu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="bb91f-247">Użyj komercyjnych certyfikat w łańcuchu zaufania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bb91f-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="bb91f-248">Jest to najlepsze rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="bb91f-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="bb91f-249">Konfiguracja DNS</span><span class="sxs-lookup"><span data-stu-id="bb91f-249">DNS configuration</span></span> ##

<span data-ttu-id="bb91f-250">Gdy używasz zewnętrznego adresu VIP DNS jest zarządzana przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="bb91f-251">Wszystkich aplikacji utworzonych w Twojej ASE jest automatycznie dodawany do usługi Azure DNS, który jest publicznym systemie DNS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="bb91f-252">W elemencie ASE ILB możesz zarządzać własną DNS.</span><span class="sxs-lookup"><span data-stu-id="bb91f-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="bb91f-253">Dla danej domeny, takie jak _contoso.net_, należy utworzyć rekordy A systemu DNS w systemie DNS, wskazujące na adres ILB dla:</span><span class="sxs-lookup"><span data-stu-id="bb91f-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="bb91f-254">*. contoso.net</span><span class="sxs-lookup"><span data-stu-id="bb91f-254">*.contoso.net</span></span>
- <span data-ttu-id="bb91f-255">*. scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="bb91f-255">*.scm.contoso.net</span></span>

<span data-ttu-id="bb91f-256">Jeśli domenę ILB ASE jest używany dla wielu elementów poza tym ASE, może być konieczne zarządzanie DNS na podstawie ciągu app-name.</span><span class="sxs-lookup"><span data-stu-id="bb91f-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="bb91f-257">Ta metoda może być trudne, ponieważ konieczne jest dodanie nowej nazwy aplikacji w systemie DNS, podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="bb91f-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="bb91f-258">Z tego powodu zaleca się użycie dedykowanych domeny.</span><span class="sxs-lookup"><span data-stu-id="bb91f-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="bb91f-259">Publikowanie za pomocą ILB ASE</span><span class="sxs-lookup"><span data-stu-id="bb91f-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="bb91f-260">Każda aplikacja, która zostanie utworzona są dwa punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="bb91f-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="bb91f-261">W elemencie ASE ILB masz  *&lt;Nazwa aplikacji >.&lt; Domeny ASE ILB >* i  *&lt;Nazwa aplikacji > .scm.&lt; Domeny ASE ILB >*.</span><span class="sxs-lookup"><span data-stu-id="bb91f-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="bb91f-262">Nazwa witryny SCM umożliwia przejście do konsoli Kudu, nazywanym **portal zaawansowane**, w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="bb91f-263">Konsola Kudu umożliwia wyświetlanie zmiennych środowiskowych, eksplorowania dysku, użyj konsoli i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="bb91f-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="bb91f-264">Aby uzyskać więcej informacji, zobacz [konsoli Kudu dla usługi Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="bb91f-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="bb91f-265">W wielodostępnej usługi aplikacji i zewnętrznego ASE Brak rejestracji jednokrotnej między konsoli Kudu i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="bb91f-266">Dla ASE ILB jednak należy do korzystania z poświadczeń publikowania do logowania się do konsoli Kudu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="bb91f-267">Internetowych systemów elementu konfiguracji, takich jak GitHub i Visual Studio Team Services nie działają z ASE ILB, ponieważ punkt końcowy publikowania nie jest dostępny internet.</span><span class="sxs-lookup"><span data-stu-id="bb91f-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="bb91f-268">Zamiast tego należy użyć systemu elementu konfiguracji, który wykorzystuje model ściągania, takich jak Dropbox.</span><span class="sxs-lookup"><span data-stu-id="bb91f-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="bb91f-269">Publikowanie punktów końcowych dla aplikacji w elemencie ASE ILB Użyj domeny, która została utworzona ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="bb91f-270">Ta domena jest wyświetlany w profilu publikowania aplikacji i w bloku portalu aplikacji (**omówienie** > **Essentials** , a także **właściwości**).</span><span class="sxs-lookup"><span data-stu-id="bb91f-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="bb91f-271">Jeśli masz ASE ILB z poddomeny *contoso.net* i aplikację o nazwie *test*, użyj *mytest.contoso.net* dla FTP i *mytest.scm.contoso.net* wdrożenia sieci web.</span><span class="sxs-lookup"><span data-stu-id="bb91f-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="bb91f-272">Połączenie ASE ILB z urządzenia zapory aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="bb91f-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="bb91f-273">Usługa aplikacji Azure udostępnia wiele środki bezpieczeństwa, które zapewniają ochronę systemu.</span><span class="sxs-lookup"><span data-stu-id="bb91f-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="bb91f-274">Ułatwiają również określić, czy zostało zaatakowane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb91f-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="bb91f-275">Ochrona najlepsze dla aplikacji sieci web jest połączenie Platforma macierzysta, takich jak usługi Azure App Service za pomocą zapory aplikacji sieci web (WAF).</span><span class="sxs-lookup"><span data-stu-id="bb91f-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="bb91f-276">Ponieważ ILB ASE ma punkt końcowy aplikacji izolowane sieci, jest odpowiednie do takiego użycia.</span><span class="sxs-lookup"><span data-stu-id="bb91f-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="bb91f-277">Aby dowiedzieć się więcej na temat sposobu konfigurowania sieci ASE ILB z urządzenia zapory aplikacji sieci Web, zobacz [Konfigurowanie zapory aplikacji sieci web ze środowiskiem usługi aplikacji][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="bb91f-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="bb91f-278">W tym artykule przedstawiono sposób Barracuda urządzenia wirtualnego za pomocą programu ASE.</span><span class="sxs-lookup"><span data-stu-id="bb91f-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="bb91f-279">Innym rozwiązaniem jest używać bramy aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="bb91f-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="bb91f-280">Brama aplikacji w używa reguł core OWASP do zabezpieczania aplikacji umieszczony za nią.</span><span class="sxs-lookup"><span data-stu-id="bb91f-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="bb91f-281">Aby uzyskać więcej informacji na temat bramy aplikacji, zobacz [wprowadzenie do zapory aplikacji sieci web platformy Azure][AppGW].</span><span class="sxs-lookup"><span data-stu-id="bb91f-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="bb91f-282">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="bb91f-282">Get started</span></span> ##

<span data-ttu-id="bb91f-283">Wszystkie artykuły i dokładne instrukcje dla ASEs są dostępne w [Plik README dla środowiska usługi aplikacji][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="bb91f-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="bb91f-284">Aby rozpocząć pracę z ASEs, zobacz [wprowadzenie do środowiska usługi aplikacji][Intro].</span><span class="sxs-lookup"><span data-stu-id="bb91f-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="bb91f-285">Aby uzyskać więcej informacji o platformie Azure App Service, zobacz temat [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="bb91f-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
