---
title: "aaaCreate i użyj wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji Azure"
description: "Więcej informacji na temat toocreate i korzystania ze środowiska usługi aplikacji Azure izolowane internet"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="525e2-103">Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="525e2-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="525e2-104">Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="525e2-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="525e2-105">Istnieją dwa sposoby toodeploy środowiska usługi App Service (ASE):</span><span class="sxs-lookup"><span data-stu-id="525e2-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="525e2-106">Z adresów VIP na zewnętrzny adres IP często nazywane ASE zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="525e2-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="525e2-107">Z adresów VIP na wewnętrzny adres IP często nazywane ASE ILB, ponieważ hello wewnętrzny punkt końcowy jest wewnętrzny moduł równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="525e2-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="525e2-108">W tym artykule opisano sposób toocreate ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="525e2-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="525e2-109">Omówienie hello ASE, zobacz [środowiska usługi tooApp wprowadzenie][Intro].</span><span class="sxs-lookup"><span data-stu-id="525e2-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="525e2-110">toolearn toocreate ASE zewnętrznych, zobacz temat [Tworzenie zewnętrznych ASE][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="525e2-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="525e2-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="525e2-111">Overview</span></span> ##

<span data-ttu-id="525e2-112">Można wdrożyć ASE z punktem końcowym dostęp do Internetu lub adres IP w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="525e2-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="525e2-113">tooset tooa adresów sieci wirtualnej, powitalne ASE muszą być wdrażane z ILB adresów hello IP.</span><span class="sxs-lookup"><span data-stu-id="525e2-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="525e2-114">Podczas wdrażania sieci ASE z ILB, należy podać:</span><span class="sxs-lookup"><span data-stu-id="525e2-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="525e2-115">Własnej domeny, który jest używany podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="525e2-116">Witaj certyfikat używany do obsługi protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="525e2-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="525e2-117">Zarządzanie systemem DNS dla domeny.</span><span class="sxs-lookup"><span data-stu-id="525e2-117">DNS management for your domain.</span></span>

<span data-ttu-id="525e2-118">W zamian można wykonać czynności takich jak:</span><span class="sxs-lookup"><span data-stu-id="525e2-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="525e2-119">Host aplikacji intranetowych bezpiecznie w chmurze hello dostęp za pośrednictwem sieci VPN platformy Azure ExpressRoute lub lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="525e2-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="525e2-120">Aplikacje hosta w chmurze hello, które nie są wymienione w publicznych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="525e2-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="525e2-121">Utwórz izolowaną internet zaplecza aplikacji, które frontonu aplikacji bezpiecznego można zintegrować z.</span><span class="sxs-lookup"><span data-stu-id="525e2-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="525e2-122">Funkcje wyłączone</span><span class="sxs-lookup"><span data-stu-id="525e2-122">Disabled functionality</span></span> ###

<span data-ttu-id="525e2-123">Istnieje kilka kwestii, które nie można wykonać, gdy używasz ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="525e2-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="525e2-124">Użyj opartych na protokole SSL.</span><span class="sxs-lookup"><span data-stu-id="525e2-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="525e2-125">Przypisz adresy IP toospecific aplikacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="525e2-126">Kup i korzystać z certyfikatu z aplikacji za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="525e2-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="525e2-127">Można uzyskać certyfikatów bezpośrednio od urzędu certyfikacji i używać ich z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="525e2-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="525e2-128">Nie można uzyskać je za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="525e2-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="525e2-129">Utwórz ILB ASE</span><span class="sxs-lookup"><span data-stu-id="525e2-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="525e2-130">toocreate ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="525e2-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="525e2-131">Hello portalu Azure, wybierz **nowy** > **sieci Web i mobilność** > **środowiska usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="525e2-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="525e2-132">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="525e2-132">Select your subscription.</span></span>

3. <span data-ttu-id="525e2-133">Wybierz lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="525e2-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="525e2-134">Wybierz lub Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="525e2-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="525e2-135">W przypadku wybrania istniejącej sieci wirtualnej, należy toocreate hello toohold podsieci ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="525e2-136">Upewnij się, tooset podsieci rozmiaru tooaccommodate wystarczająco duży przyszłego rozwoju ASE sieci.</span><span class="sxs-lookup"><span data-stu-id="525e2-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="525e2-137">Firma Microsoft zaleca o rozmiarze `/25`, który 128 adresów i może obsłużyć ASE rozmiar maksymalny.</span><span class="sxs-lookup"><span data-stu-id="525e2-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="525e2-138">Minimalny rozmiar Hello można wybrać jest `/28`.</span><span class="sxs-lookup"><span data-stu-id="525e2-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="525e2-139">Po wymaga infrastruktury, ten rozmiar może być skalowana tooa maksymalna liczba wystąpień 11.</span><span class="sxs-lookup"><span data-stu-id="525e2-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="525e2-140">Wykracza poza hello domyślne maksymalnie 100 wystąpieniami w planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="525e2-141">Skalowanie bliskie 100, ale także z bardziej szybkie skalowanie frontonu.</span><span class="sxs-lookup"><span data-stu-id="525e2-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="525e2-142">Wybierz **wirtualnego lokalizacji** > **konfiguracji sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="525e2-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="525e2-143">Zestaw hello **typu VIP** za**wewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="525e2-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="525e2-144">Wprowadź nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="525e2-144">Enter a domain name.</span></span> <span data-ttu-id="525e2-145">Ta domena jest hello używane jako aplikacje utworzone w tym ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="525e2-146">Istnieją pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="525e2-146">There are some restrictions.</span></span> <span data-ttu-id="525e2-147">Nie można go:</span><span class="sxs-lookup"><span data-stu-id="525e2-147">It can't be:</span></span>

    * <span data-ttu-id="525e2-148">NET</span><span class="sxs-lookup"><span data-stu-id="525e2-148">net</span></span>   

    * <span data-ttu-id="525e2-149">azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="525e2-149">azurewebsites.net</span></span>

    * <span data-ttu-id="525e2-150">p.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="525e2-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="525e2-151">&lt;asename&gt;. p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="525e2-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="525e2-152">Hello niestandardowej nazwy domeny używane do aplikacji i nazwy domeny hello używany przez Twoje ASE nie może nakładać się.</span><span class="sxs-lookup"><span data-stu-id="525e2-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="525e2-153">Dla ASE ILB z nazwą domeny hello _contoso.com_, nie można użyć niestandardowych nazw domen dla twojej aplikacji, takich jak:</span><span class="sxs-lookup"><span data-stu-id="525e2-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="525e2-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="525e2-154">www.contoso.com</span></span>

    * <span data-ttu-id="525e2-155">Abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="525e2-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="525e2-156">Abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="525e2-156">abcd.contoso.com</span></span>

   <span data-ttu-id="525e2-157">Jeśli znasz hello niestandardowych nazw domen dla aplikacji, wybierz domenę dla hello ASE ILB, który nie występuje konflikt z tymi nazwami domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="525e2-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="525e2-158">W tym przykładzie, można użyć przypominać *contoso internal.com* dla domeny Twojej ASE hello ponieważ nie będących w konflikcie z nazwami domen niestandardowych, które kończą się *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="525e2-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="525e2-159">Wybierz **OK**, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="525e2-159">Select **OK**, and then select **Create**.</span></span>

    ![Tworzenie środowiska ASE][1]

<span data-ttu-id="525e2-161">Na powitania **sieci wirtualnej** bloku jest **konfiguracja sieci wirtualnej** opcji.</span><span class="sxs-lookup"><span data-stu-id="525e2-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="525e2-162">Służy on tooselect zewnętrznego adresu VIP lub jako wewnętrzny adres VIP.</span><span class="sxs-lookup"><span data-stu-id="525e2-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="525e2-163">Domyślnie Hello **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="525e2-163">hello default is **External**.</span></span> <span data-ttu-id="525e2-164">W przypadku wybrania **zewnętrznych**, Twoje ASE używa VIP dostępny z Internetu.</span><span class="sxs-lookup"><span data-stu-id="525e2-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="525e2-165">W przypadku wybrania **wewnętrzne**, Twoje ASE skonfigurowano ILB na adres IP w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="525e2-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="525e2-166">Po wybraniu **wewnętrzne**, tooadd możliwości hello więcej adresów IP tooyour ASE zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="525e2-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="525e2-167">Zamiast tego należy tooprovide domeny hello hello ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="525e2-168">W elemencie ASE z zewnętrznego adresu VIP hello nazwa hello ASE jest używany w domenie hello aplikacji utworzone w tym ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="525e2-169">Jeśli ustawisz **typu VIP** za**wewnętrzne**, nazwę ASE nie jest używany w domenie hello na powitania ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="525e2-170">Należy jawnie określić domenę hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="525e2-171">Jeśli Twoja domena to *contoso.corp.net* i utworzyć aplikację, w tym o nazwie ASE *timereporting*, hello adres URL dla tej aplikacji jest timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="525e2-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="525e2-172">Utwórz aplikację w elemencie ASE ILB</span><span class="sxs-lookup"><span data-stu-id="525e2-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="525e2-173">Utwórz aplikację w elemencie ASE ILB w hello samo tworzenie aplikacji w elemencie ASE normalnie.</span><span class="sxs-lookup"><span data-stu-id="525e2-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="525e2-174">Hello portalu Azure, wybierz **nowy** > **sieci Web i mobilność** > **Web** lub **Mobile** lub  **Aplikacja interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="525e2-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="525e2-175">Wprowadź nazwę aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="525e2-176">Wybierz subskrypcję hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-176">Select hello subscription.</span></span>

4. <span data-ttu-id="525e2-177">Wybierz lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="525e2-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="525e2-178">Wybierz lub Utwórz plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-178">Select or create an App Service plan.</span></span> <span data-ttu-id="525e2-179">Toocreate nowy plan usługi aplikacji, wybierz opcję sieci ASE jako hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="525e2-180">Wybierz miejsce Twojego toobe planu usługi aplikacji utworzone puli procesów roboczych hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="525e2-181">Po utworzeniu planu usługi aplikacji hello wybierz Twoje ASE jako lokalizacji hello i hello puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="525e2-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="525e2-182">Po określeniu nazwy hello aplikacji hello domeny hello pod nazwą aplikacji zastępuje hello domeny dla Twojego ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="525e2-183">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="525e2-183">Select **Create**.</span></span> <span data-ttu-id="525e2-184">Tooappear aplikacji hello na pulpicie nawigacyjnym, zaznacz **toodashboard numeru Pin** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="525e2-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![Tworzenie planu usługi aplikacji][2]

    <span data-ttu-id="525e2-186">W obszarze **Nazwa aplikacji**, nazwa domeny hello jest domeny hello zaktualizowane tooreflect Twojego ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="525e2-187">Sprawdzanie poprawności tworzenia POST ILB ASE</span><span class="sxs-lookup"><span data-stu-id="525e2-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="525e2-188">ASE ILB są nieco inne niż hello nie - ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="525e2-189">Jak już zanotowane należy toomanage własne DNS.</span><span class="sxs-lookup"><span data-stu-id="525e2-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="525e2-190">Masz również tooprovide swój własny certyfikat dla połączeń HTTPS.</span><span class="sxs-lookup"><span data-stu-id="525e2-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="525e2-191">Po utworzeniu sieci ASE hello nazwa domeny zawiera hello określonej domeny.</span><span class="sxs-lookup"><span data-stu-id="525e2-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="525e2-192">Nowy element jest wyświetlany w **ustawienie** menu o nazwie **certyfikatu ILB**.</span><span class="sxs-lookup"><span data-stu-id="525e2-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="525e2-193">Witaj ASE jest tworzony przy użyciu certyfikatu, który nie określa domeny ILB ASE hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="525e2-194">Korzystając z tego certyfikatu hello ASE, przeglądarki informuje, czy jest on nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="525e2-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="525e2-195">Ten certyfikat umożliwia łatwiejsze tootest HTTPS, ale należy tooupload własnego certyfikatu, który jest wiązana tooyour ILB ASE domeny.</span><span class="sxs-lookup"><span data-stu-id="525e2-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="525e2-196">Ten krok jest niezbędny, niezależnie od tego, czy certyfikat z podpisem własnym, czy otrzymanego od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="525e2-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Nazwa domeny ILB ASE][3]

<span data-ttu-id="525e2-198">Twoje ASE ILB musi mieć prawidłowy certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="525e2-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="525e2-199">Użyj certyfikatu wewnętrznego urzędów, kupić certyfikat od zewnętrznego wystawcy lub Użyj certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="525e2-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="525e2-200">Niezależnie od źródła hello hello certyfikatu SSL hello następujące atrybuty certyfikatu należy toobe prawidłowo skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="525e2-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="525e2-201">**Temat**: ten atrybut musi być ustawiony too*.your głównego domeny tutaj.</span><span class="sxs-lookup"><span data-stu-id="525e2-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="525e2-202">**Alternatywna nazwa podmiotu**: ten atrybut musi zawierać zarówno **.your głównego domeny tutaj* i **.scm.your-głównego-domeny — w tym miejscu*.</span><span class="sxs-lookup"><span data-stu-id="525e2-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="525e2-203">Toohello połączenia SSL SCM/Kudu lokacji skojarzone z każdej aplikacji używać adresu formularza hello *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="525e2-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="525e2-204">Konwertuj/Zapisz certyfikat SSL hello jako plik pfx.</span><span class="sxs-lookup"><span data-stu-id="525e2-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="525e2-205">plik PFX Hello musi obejmować wszystkie pośrednie i certyfikaty główne.</span><span class="sxs-lookup"><span data-stu-id="525e2-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="525e2-206">Zabezpiecz ją przy użyciu hasła.</span><span class="sxs-lookup"><span data-stu-id="525e2-206">Secure it with a password.</span></span>

<span data-ttu-id="525e2-207">Jeśli chcesz toocreate certyfikatu z podpisem własnym, można użyć poleceń programu PowerShell hello tutaj.</span><span class="sxs-lookup"><span data-stu-id="525e2-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="525e2-208">Można toouse czy nazwy domeny ILB ASE zamiast *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="525e2-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="525e2-209">certyfikat Hello generowanie tych poleceń programu PowerShell oflagowane przez przeglądarki, ponieważ hello certyfikat nie został utworzony przez urząd certyfikacji, który znajduje się w łańcuch zaufania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="525e2-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="525e2-210">tooget certyfikatu, który ufa przeglądarkę, uzyskaj od urzędu certyfikacji komercyjnych w łańcuchu zaufania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="525e2-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Zestaw ILB certyfikatu][4]

<span data-ttu-id="525e2-212">tooupload własne certyfikaty i test dostępu:</span><span class="sxs-lookup"><span data-stu-id="525e2-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="525e2-213">Po utworzeniu hello ASE Przejdź toohello ASE interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="525e2-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="525e2-214">Wybierz **ASE** > **ustawienia** > **certyfikatu ILB**.</span><span class="sxs-lookup"><span data-stu-id="525e2-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="525e2-215">tooset hello ILB certyfikat, wybierz plik .pfx certyfikatu hello i podaj hasło hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="525e2-216">Ten krok zajmuje kilka tooprocess czas.</span><span class="sxs-lookup"><span data-stu-id="525e2-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="525e2-217">Pojawi się komunikat z informacją, że operacja przekazywania jest w toku.</span><span class="sxs-lookup"><span data-stu-id="525e2-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="525e2-218">Pobierz adres ILB hello Twojej ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="525e2-219">Wybierz **ASE** > **właściwości** > **wirtualny adres IP**.</span><span class="sxs-lookup"><span data-stu-id="525e2-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="525e2-220">Tworzenie aplikacji sieci web w sieci ASE po utworzeniu hello ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="525e2-221">Tworzenie maszyny Wirtualnej, jeśli nie istnieje w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="525e2-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="525e2-222">Nie próbuj toocreate tej maszyny Wirtualnej w tej samej podsieci Witaj, jak hello ASE, ponieważ będzie zakończyć się niepowodzeniem lub spowodować problemy.</span><span class="sxs-lookup"><span data-stu-id="525e2-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="525e2-223">Ustaw hello DNS dla domeny ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="525e2-224">Za pomocą symbolu wieloznacznego i domeny w systemie DNS.</span><span class="sxs-lookup"><span data-stu-id="525e2-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="525e2-225">toodo prostych testów, Edytuj plik hosts hello na Twojej maszyny Wirtualnej tooset hello sieci web aplikacji Nazwa toohello adres VIP:</span><span class="sxs-lookup"><span data-stu-id="525e2-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="525e2-226">a.</span><span class="sxs-lookup"><span data-stu-id="525e2-226">a.</span></span> <span data-ttu-id="525e2-227">Jeśli Twoje ASE ma nazwę domeny hello _. ilbase.com_ i utworzysz aplikację sieci web hello o nazwie _mytestapp_, jest skierowana na _mytestapp.ilbase.com_. Następnie ustaw _mytestapp.ilbase.com_ tooresolve toohello ILB adresu.</span><span class="sxs-lookup"><span data-stu-id="525e2-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="525e2-228">(W systemie Windows, plik hosts hello jest na _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="525e2-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="525e2-229">b.</span><span class="sxs-lookup"><span data-stu-id="525e2-229">b.</span></span> <span data-ttu-id="525e2-230">tootest sieci web wdrożenia publikowania lub dostęp toohello zaawansowane konsoli, Utwórz rekord _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="525e2-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="525e2-231">Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do http://mytestapp.ilbase.com. (Lub przejdź toowhatever, którego nazwę aplikacji sieci web z domeną.)</span><span class="sxs-lookup"><span data-stu-id="525e2-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="525e2-232">Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do https://mytestapp.ilbase.com. Jeśli używasz certyfikatu z podpisem własnym, należy zaakceptować hello braku zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="525e2-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="525e2-233">adres IP Twojego ILB Hello jest wyświetlana w obszarze **adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="525e2-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="525e2-234">Ta lista zawiera również hello adresy IP używane przez zewnętrznych adresów VIP hello i ruchu przychodzącego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="525e2-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![Adres ILB IP][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="525e2-236">Sieci Web zadania, funkcje i hello ILB ASE</span><span class="sxs-lookup"><span data-stu-id="525e2-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="525e2-237">Zarówno funkcje i zadania sieci web są obsługiwane w elemencie ASE ILB, ale hello portalu toowork z nimi, musisz mieć lokacji SCM toohello dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="525e2-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="525e2-238">Oznacza to, że na hoście, który jest albo połączenia wirtualnej sieci toohello musi być przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="525e2-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="525e2-239">Gdy używasz usługi Azure Functions w elemencie ASE ILB, może pobrać komunikat o błędzie stwierdzający "nie jesteśmy w stanie tooretrieve funkcji w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="525e2-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="525e2-240">Spróbuj ponownie później."</span><span class="sxs-lookup"><span data-stu-id="525e2-240">Please try again later."</span></span> <span data-ttu-id="525e2-241">Ten błąd występuje, ponieważ hello interfejsu użytkownika funkcji wykorzystuje hello SCM lokacji za pośrednictwem protokołu HTTPS i certyfikatu głównego hello nie znajduje się w przeglądarce hello łańcuch zaufania.</span><span class="sxs-lookup"><span data-stu-id="525e2-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="525e2-242">Zadania Web Job ma podobny problem.</span><span class="sxs-lookup"><span data-stu-id="525e2-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="525e2-243">tooavoid ten problem, można wykonać jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="525e2-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="525e2-244">Dodawanie magazynu zaufanych certyfikatów tooyour certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="525e2-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="525e2-245">Odblokowuje to Edge i przeglądarki Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="525e2-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="525e2-246">Użyj Chrome i odwiedź witrynę SCM toohello najpierw, Zaakceptuj hello niezaufany certyfikat, a następnie przejdź toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="525e2-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="525e2-247">Użyj komercyjnych certyfikat w łańcuchu zaufania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="525e2-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="525e2-248">Jest to hello najlepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="525e2-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="525e2-249">Konfiguracja DNS</span><span class="sxs-lookup"><span data-stu-id="525e2-249">DNS configuration</span></span> ##

<span data-ttu-id="525e2-250">Gdy używasz zewnętrznego adresu VIP hello DNS jest zarządzana przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="525e2-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="525e2-251">Wszystkich aplikacji utworzonych w Twojej ASE jest automatycznie dodawany tooAzure DNS, który jest publicznym systemie DNS.</span><span class="sxs-lookup"><span data-stu-id="525e2-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="525e2-252">W elemencie ASE ILB możesz zarządzać własną DNS.</span><span class="sxs-lookup"><span data-stu-id="525e2-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="525e2-253">Dla danej domeny, takie jak _contoso.net_, należy toocreate A systemu DNS są rejestrowane w systemie DNS tego adresu ILB tooyour punktu dla:</span><span class="sxs-lookup"><span data-stu-id="525e2-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="525e2-254">*. contoso.net</span><span class="sxs-lookup"><span data-stu-id="525e2-254">*.contoso.net</span></span>
- <span data-ttu-id="525e2-255">*. scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="525e2-255">*.scm.contoso.net</span></span>

<span data-ttu-id="525e2-256">Jeśli domenę ILB ASE jest używany dla wielu elementów poza tym ASE, może być konieczne toomanage DNS na podstawie ciągu app-name.</span><span class="sxs-lookup"><span data-stu-id="525e2-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="525e2-257">Ta metoda może być trudne, ponieważ potrzebna tooadd każdej nowej nazwy aplikacji w systemie DNS podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="525e2-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="525e2-258">Z tego powodu zaleca się użycie dedykowanych domeny.</span><span class="sxs-lookup"><span data-stu-id="525e2-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="525e2-259">Publikowanie za pomocą ILB ASE</span><span class="sxs-lookup"><span data-stu-id="525e2-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="525e2-260">Każda aplikacja, która zostanie utworzona są dwa punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="525e2-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="525e2-261">W elemencie ASE ILB masz  *&lt;Nazwa aplikacji >.&lt; Domeny ASE ILB >* i  *&lt;Nazwa aplikacji > .scm.&lt; Domeny ASE ILB >*.</span><span class="sxs-lookup"><span data-stu-id="525e2-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="525e2-262">Nazwa witryny SCM Hello przyjmuje konsoli Kudu toohello, nazywanym hello **portal zaawansowane**, poziomu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="525e2-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="525e2-263">Konsola Kudu Hello umożliwia wyświetlanie zmiennych środowiskowych, Eksploruj hello dysku, użyj konsoli i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="525e2-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="525e2-264">Aby uzyskać więcej informacji, zobacz [konsoli Kudu dla usługi Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="525e2-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="525e2-265">W wielodostępnej hello usługi aplikacji i zewnętrznego ASE Brak rejestracji jednokrotnej między hello portalu Azure i hello Kudu konsoli.</span><span class="sxs-lookup"><span data-stu-id="525e2-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="525e2-266">Dla hello ILB ASE jednak należy toouse Twojego publikowania toosign poświadczeń do hello Kudu konsoli.</span><span class="sxs-lookup"><span data-stu-id="525e2-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="525e2-267">Internetowych systemów elementu konfiguracji, takich jak GitHub i Visual Studio Team Services nie działają z ASE ILB, ponieważ hello punkt końcowy publikowania nie jest dostępny internet.</span><span class="sxs-lookup"><span data-stu-id="525e2-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="525e2-268">Zamiast tego należy toouse systemu elementu konfiguracji, który wykorzystuje model ściągania, takich jak Dropbox.</span><span class="sxs-lookup"><span data-stu-id="525e2-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="525e2-269">Witaj publikowania punktów końcowych dla aplikacji w elemencie ASE ILB korzystania z domeny hello tego hello ILB ASE została utworzona z.</span><span class="sxs-lookup"><span data-stu-id="525e2-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="525e2-270">Ta domena jest wyświetlany w profilu publikowania aplikacji hello i w bloku portalu aplikacji hello (**omówienie** > **Essentials** , a także **właściwości**).</span><span class="sxs-lookup"><span data-stu-id="525e2-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="525e2-271">Jeśli masz ASE ILB z poddomeny hello *contoso.net* i aplikację o nazwie *test*, użyj *mytest.contoso.net* dla FTP i *mytest.scm.contoso.net*  wdrożenia sieci web.</span><span class="sxs-lookup"><span data-stu-id="525e2-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="525e2-272">Połączenie ASE ILB z urządzenia zapory aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="525e2-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="525e2-273">Usługa aplikacji Azure udostępnia wiele środki bezpieczeństwa, które ochrona powitalnych systemu.</span><span class="sxs-lookup"><span data-stu-id="525e2-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="525e2-274">Ułatwiają również toodetermine czy aplikacji zostało zaatakowane.</span><span class="sxs-lookup"><span data-stu-id="525e2-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="525e2-275">Witaj ochrony najlepsze dla aplikacji sieci web jest toocouple hostingu platformie, takich jak usługi Azure App Service za pomocą zapory aplikacji sieci web (WAF).</span><span class="sxs-lookup"><span data-stu-id="525e2-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="525e2-276">Ponieważ hello ILB ASE ma punkt końcowy aplikacji izolowane sieci, jest odpowiednie do takiego użycia.</span><span class="sxs-lookup"><span data-stu-id="525e2-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="525e2-277">więcej informacji na temat tooconfigure Twojego ASE ILB z urządzenia zapory aplikacji sieci Web, zobacz temat toolearn [Konfigurowanie zapory aplikacji sieci web ze środowiskiem usługi aplikacji][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="525e2-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="525e2-278">W tym artykule przedstawiono sposób toouse Barracuda urządzenie wirtualne z Twojej ASE.</span><span class="sxs-lookup"><span data-stu-id="525e2-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="525e2-279">Innym rozwiązaniem jest toouse Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="525e2-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="525e2-280">Brama aplikacji w używa hello OWASP podstawowe reguły toosecure umieścić wszystkie aplikacje za nią.</span><span class="sxs-lookup"><span data-stu-id="525e2-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="525e2-281">Aby uzyskać więcej informacji na temat bramy aplikacji, zobacz [zapory aplikacji sieci web platformy Azure toohello wprowadzenie][AppGW].</span><span class="sxs-lookup"><span data-stu-id="525e2-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="525e2-282">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="525e2-282">Get started</span></span> ##

<span data-ttu-id="525e2-283">Wszystkie artykuły i jak tooinstructions dla ASEs są dostępne w [Plik README dla środowiska usługi aplikacji][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="525e2-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="525e2-284">tooget wprowadzenie ASEs, zobacz [środowiska usługi tooApp wprowadzenie][Intro].</span><span class="sxs-lookup"><span data-stu-id="525e2-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="525e2-285">Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="525e2-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
