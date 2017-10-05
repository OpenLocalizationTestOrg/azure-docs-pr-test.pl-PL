---
title: "Użyj środowiska usługi aplikacji Azure"
description: "Jak tworzenie, publikowanie i skalowanie aplikacji w środowisku usługi aplikacji Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 279951d40b7780120d0b94e183f06e00ccece016
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="83da3-103">Użyj środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="83da3-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="83da3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="83da3-104">Overview</span></span> ##

<span data-ttu-id="83da3-105">Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure klienta.</span><span class="sxs-lookup"><span data-stu-id="83da3-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="83da3-106">Składa się z:</span><span class="sxs-lookup"><span data-stu-id="83da3-106">It consists of:</span></span>

- <span data-ttu-id="83da3-107">**Zakończenia przód**: front końce są, gdzie HTTP/HTTPS kończy się w środowisku usługi aplikacji (ASE).</span><span class="sxs-lookup"><span data-stu-id="83da3-107">**Front ends**: The front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="83da3-108">**Pracownicy**: pracownicy są zasoby, które hosta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-108">**Workers**: The workers are the resources that host your apps.</span></span>
- <span data-ttu-id="83da3-109">**Baza danych**: bazy danych zawiera informacje określające środowiska.</span><span class="sxs-lookup"><span data-stu-id="83da3-109">**Database**: The database holds information that defines the environment.</span></span>
- <span data-ttu-id="83da3-110">**Magazyn**: Magazyn jest używany na potrzeby hostowania aplikacji publikowanych przez klienta.</span><span class="sxs-lookup"><span data-stu-id="83da3-110">**Storage**: The storage is used to host the customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="83da3-111">Istnieją dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2.</span><span class="sxs-lookup"><span data-stu-id="83da3-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="83da3-112">Przed ich użyciem w ASEv1, możesz zarządzać zasobami.</span><span class="sxs-lookup"><span data-stu-id="83da3-112">In ASEv1, you must manage the resources before you can use them.</span></span> <span data-ttu-id="83da3-113">Aby uzyskać informacje o konfigurowaniu i zarządzaniu nimi ASEv1, zobacz [skonfigurować v1 środowiska usługi aplikacji][ConfigureASEv1].</span><span class="sxs-lookup"><span data-stu-id="83da3-113">To learn how to configure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="83da3-114">Pozostała część ten artykuł koncentruje się na ASEv2.</span><span class="sxs-lookup"><span data-stu-id="83da3-114">The rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="83da3-115">ASE (ASEv1 i ASEv2) można wdrożyć z zewnętrznym lub wewnętrznym adresu VIP do uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="83da3-116">Wdrożenia z zewnętrznego adresu VIP jest popularnie określany ASE zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="83da3-116">The deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="83da3-117">Wersja wewnętrznej jest nazywana ILB ASE, ponieważ używa wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="83da3-117">The internal version is called the ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="83da3-118">Aby dowiedzieć się więcej na temat ILB ASE, zobacz [tworzenie i używanie ASE ILB][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="83da3-118">To learn more about the ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="83da3-119">Tworzenie aplikacji sieci web w elemencie ASE</span><span class="sxs-lookup"><span data-stu-id="83da3-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="83da3-120">Aby utworzyć aplikację sieci web w elemencie ASE, należy użyć te same czynności co zwykle tworzenia, jednak z kilku niewielkie różnice.</span><span class="sxs-lookup"><span data-stu-id="83da3-120">To create a web app in an ASE, you use the same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="83da3-121">Podczas tworzenia nowego planu usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="83da3-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="83da3-122">Zamiast wybierać lokalizację geograficzną, w której chcesz wdrożyć aplikację, wybierz polecenie ASE jako lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-122">Instead of choosing a geographic location in which to deploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="83da3-123">Wszystkich utworzonych w elemencie ASE planów usługi aplikacji musi być izolowany warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="83da3-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="83da3-124">Jeśli nie masz ASE, możesz utworzyć jedną zgodnie z instrukcjami w [tworzenie środowiska usługi aplikacji][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="83da3-124">If you don't have an ASE, you can create one by following the instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="83da3-125">Aby utworzyć aplikację sieci web w elemencie ASE:</span><span class="sxs-lookup"><span data-stu-id="83da3-125">To create a web app in an ASE:</span></span>

1. <span data-ttu-id="83da3-126">Wybierz **nowe** > **sieci Web i mobilność** > **sieci Web aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="83da3-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="83da3-127">Wprowadź nazwę dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="83da3-127">Enter a name for the web app.</span></span> <span data-ttu-id="83da3-128">Jeśli plan usługi aplikacji jest już wybrana w elemencie ASE, nazwę domeny dla aplikacji odzwierciedla ASE nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="83da3-128">If you already selected an App Service plan in an ASE, the domain name for the app reflects the domain name of the ASE.</span></span>

    ![Wybór nazwy aplikacji sieci Web][1]

3. <span data-ttu-id="83da3-130">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="83da3-130">Select a subscription.</span></span>

4. <span data-ttu-id="83da3-131">Wprowadź nazwę nowej grupy zasobów lub wybierz **Użyj istniejącego** i wybierz z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="83da3-131">Enter a name for a new resource group, or select **Use existing** and select one from the drop-down list.</span></span>

5. <span data-ttu-id="83da3-132">Wybierz istniejący plan usługi aplikacji w Twojej ASE lub Utwórz nową, wykonując następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="83da3-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="83da3-133">a.</span><span class="sxs-lookup"><span data-stu-id="83da3-133">a.</span></span> <span data-ttu-id="83da3-134">Wybierz **tworzenia nowych**.</span><span class="sxs-lookup"><span data-stu-id="83da3-134">Select **Create New**.</span></span>

    <span data-ttu-id="83da3-135">b.</span><span class="sxs-lookup"><span data-stu-id="83da3-135">b.</span></span> <span data-ttu-id="83da3-136">Wprowadź nazwę planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-136">Enter the name for your App Service plan.</span></span>

    <span data-ttu-id="83da3-137">c.</span><span class="sxs-lookup"><span data-stu-id="83da3-137">c.</span></span> <span data-ttu-id="83da3-138">Wybierz użytkownika ASE w **lokalizacji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="83da3-138">Select your ASE in the **Location** drop-down list.</span></span>

    <span data-ttu-id="83da3-139">d.</span><span class="sxs-lookup"><span data-stu-id="83da3-139">d.</span></span> <span data-ttu-id="83da3-140">Wybierz **izolowany** warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="83da3-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="83da3-141">Wybierz **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="83da3-141">Select **Select**.</span></span>

    <span data-ttu-id="83da3-142">e.</span><span class="sxs-lookup"><span data-stu-id="83da3-142">e.</span></span> <span data-ttu-id="83da3-143">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="83da3-143">Select **OK**.</span></span>
    
    ![Izolowane warstw cenowych][2]

6. <span data-ttu-id="83da3-145">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83da3-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="83da3-146">Jak skalować działa</span><span class="sxs-lookup"><span data-stu-id="83da3-146">How scale works</span></span> ##

<span data-ttu-id="83da3-147">Każda aplikacja usługi aplikacji jest uruchamiany w plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="83da3-148">Model kontenera jest środowisk przytrzymaj planów usługi App Service i planów usługi App Service przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-148">The container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="83da3-149">Skalowanie aplikacji należy skalowanie planu usługi aplikacji i w związku z tym wszystkie aplikacje w tym samym planie.</span><span class="sxs-lookup"><span data-stu-id="83da3-149">When you scale an app, you scale the App Service plan and thus scale all the apps in the same plan.</span></span>

<span data-ttu-id="83da3-150">W ASEv2 skalowanie planu usługi App Service, infrastruktura wymagana jest automatycznie dodawany.</span><span class="sxs-lookup"><span data-stu-id="83da3-150">In ASEv2, when you scale an App Service plan, the needed infrastructure is automatically added.</span></span> <span data-ttu-id="83da3-151">Podczas dodawania jest infrastruktura istnieje opóźnienie operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="83da3-151">There is a time delay to scale operations while the infrastructure is added.</span></span> <span data-ttu-id="83da3-152">ASEv1 wymagane infrastruktury muszą zostać dodane przed utworzeniem lub skalowanie planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-152">In ASEv1, the needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="83da3-153">W wielodostępnej usługi aplikacji skalowanie jest zwykle bezpośredniego, ponieważ pula zasobów jest łatwo dostępna do jego obsługi.</span><span class="sxs-lookup"><span data-stu-id="83da3-153">In the multitenant App Service, scaling is usually immediate because a pool of resources is readily available to support it.</span></span> <span data-ttu-id="83da3-154">W elemencie ASE istnieje takie buforu i zasoby są przydzielane na potrzeby.</span><span class="sxs-lookup"><span data-stu-id="83da3-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="83da3-155">W elemencie ASE można skalować wystąpień do 100.</span><span class="sxs-lookup"><span data-stu-id="83da3-155">In an ASE, you can scale up to 100 instances.</span></span> <span data-ttu-id="83da3-156">Te wystąpienia, 100 może być wszystko w jednym jednego planu usługi aplikacji lub rozproszone na wielu planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="83da3-157">Adresy IP</span><span class="sxs-lookup"><span data-stu-id="83da3-157">IP addresses</span></span> ##

<span data-ttu-id="83da3-158">Usługa App Service oferuje możliwość przydzielony dedykowany adres IP do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-158">App Service has the ability to allocate a dedicated IP address to an app.</span></span> <span data-ttu-id="83da3-159">Ta funkcja jest dostępna po skonfigurowaniu opartych na protokole SSL, zgodnie z opisem w [Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci web platformy Azure][ConfigureSSL].</span><span class="sxs-lookup"><span data-stu-id="83da3-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate to Azure web apps][ConfigureSSL].</span></span> <span data-ttu-id="83da3-160">W elemencie ASE istnieje jednak zauważalne wyjątku.</span><span class="sxs-lookup"><span data-stu-id="83da3-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="83da3-161">Nie można dodać dodatkowe adresy IP stosowaną do opartych na protokole SSL w elemencie ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="83da3-161">You can't add additional IP addresses to be used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="83da3-162">W ASEv1 należy przydzielić adresy IP jako zasoby przed ich użyciem.</span><span class="sxs-lookup"><span data-stu-id="83da3-162">In ASEv1, you need to allocate the IP addresses as resources before you can use them.</span></span> <span data-ttu-id="83da3-163">W ASEv2 można ich używać z aplikacji tak samo jak w wielodostępnej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-163">In ASEv2, you use them from your app just as you do in the multitenant App Service.</span></span> <span data-ttu-id="83da3-164">Istnieje jeden adres zapasowe w ASEv2 maksymalnie 30 adresów IP.</span><span class="sxs-lookup"><span data-stu-id="83da3-164">There is always one spare address in ASEv2 up to 30 IP addresses.</span></span> <span data-ttu-id="83da3-165">Zawsze używany jest jeden, inny są dodawane, że adres zawsze jest gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="83da3-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="83da3-166">Czas opóźnienia należy przydzielić inny adres IP, co uniemożliwia dodanie adresu IP adresów szybkie naciśnięcie.</span><span class="sxs-lookup"><span data-stu-id="83da3-166">A time delay is required to allocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="83da3-167">Skalowanie frontonu</span><span class="sxs-lookup"><span data-stu-id="83da3-167">Front-end scaling</span></span> ##

<span data-ttu-id="83da3-168">W ASEv2 gdy skalowanie planów usługi aplikacji pracowników są automatycznie dodawane do ich obsługi.</span><span class="sxs-lookup"><span data-stu-id="83da3-168">In ASEv2, when you scale out your App Service plans, workers are automatically added to support them.</span></span> <span data-ttu-id="83da3-169">Co ASE jest tworzony z przodu punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="83da3-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="83da3-170">Ponadto przodu kończy się automatycznie skalowania w poziomie z szybkością co frontonu dla każdego wystąpienia 15 w planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-170">In addition, the front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="83da3-171">Na przykład jeśli masz wystąpień 15 masz trzy front kończy się.</span><span class="sxs-lookup"><span data-stu-id="83da3-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="83da3-172">Jeśli można skalować do 30 wystąpień, użytkownik ma cztery zakończenia przód i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="83da3-172">If you scale to 30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="83da3-173">Ten numer interfejsy powinny być to wystarczająca liczba dla większości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="83da3-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="83da3-174">Jednak można skalować w poziomie szybsze.</span><span class="sxs-lookup"><span data-stu-id="83da3-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="83da3-175">Możesz zmienić stosunek jako jeden z przodu niski zakończyć co pięć wystąpień.</span><span class="sxs-lookup"><span data-stu-id="83da3-175">You can change the ratio to as low as one front end for every five instances.</span></span> <span data-ttu-id="83da3-176">Opłata za zmianę stosunek nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="83da3-176">There is a charge for changing the ratio.</span></span> <span data-ttu-id="83da3-177">Aby uzyskać więcej informacji, zobacz [cennik usługi aplikacji Azure][Pricing].</span><span class="sxs-lookup"><span data-stu-id="83da3-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="83da3-178">Frontonu zasoby są ASE punktu końcowego HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83da3-178">Front-end resources are the HTTP/HTTPS endpoint for the ASE.</span></span> <span data-ttu-id="83da3-179">Z domyślnej konfiguracji frontonu użycie pamięci na fronton jest stale około 60 procent.</span><span class="sxs-lookup"><span data-stu-id="83da3-179">With the default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="83da3-180">Obciążeń klientów nie działają na fronton.</span><span class="sxs-lookup"><span data-stu-id="83da3-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="83da3-181">Kluczowe znaczenie dla frontonu w odniesieniu do skalowania jest Procesora, który jest wymuszany głównie przez ruchu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83da3-181">The key factor for a front end with respect to scale is the CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="83da3-182">Dostęp do aplikacji</span><span class="sxs-lookup"><span data-stu-id="83da3-182">App access</span></span> ##

<span data-ttu-id="83da3-183">W elemencie ASE zewnętrznych domeny, który jest używany podczas tworzenia aplikacji różni się od wielodostępnej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-183">In an External ASE, the domain that's used when you create apps is different from the multitenant App Service.</span></span> <span data-ttu-id="83da3-184">Zawiera nazwę ASE.</span><span class="sxs-lookup"><span data-stu-id="83da3-184">It includes the name of the ASE.</span></span> <span data-ttu-id="83da3-185">Aby uzyskać więcej informacji na temat tworzenia ASE zewnętrznych, zobacz [tworzenie środowiska usługi aplikacji][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="83da3-185">For more information on how to create an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="83da3-186">Nazwa domeny w elemencie ASE zewnętrznych wygląda następująco: *.&lt; asename&gt;. p.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="83da3-186">The domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="83da3-187">Na przykład, jeśli nosi nazwę Twojej ASE _ase zewnętrzne_ i hosta aplikacji o nazwie _contoso_ w tym ASE, możesz uzyskać do niej dostęp w następujących adresów URL:</span><span class="sxs-lookup"><span data-stu-id="83da3-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at the following URLs:</span></span>

- <span data-ttu-id="83da3-188">contoso.external ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="83da3-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="83da3-189">contoso.SCM.external ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="83da3-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="83da3-190">Adres URL contoso.scm.external-ase.p.azurewebsites.net umożliwia dostęp do konsoli Kudu lub do publikowania aplikacji za pomocą sieci web deploy.</span><span class="sxs-lookup"><span data-stu-id="83da3-190">The URL contoso.scm.external-ase.p.azurewebsites.net is used to access the Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="83da3-191">Informacje w konsoli Kudu, zobacz [konsoli Kudu dla usługi Azure App Service][Kudu].</span><span class="sxs-lookup"><span data-stu-id="83da3-191">For information on the Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="83da3-192">Konsoli Kudu zapewnia interfejsu użytkownika sieci web dla debugowania przekazywania plików, edytowanie plików i wiele innych.</span><span class="sxs-lookup"><span data-stu-id="83da3-192">The Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="83da3-193">W elemencie ASE ILB należy określić domeny, w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="83da3-193">In an ILB ASE, you determine the domain at deployment time.</span></span> <span data-ttu-id="83da3-194">Aby uzyskać więcej informacji na temat tworzenia ASE ILB, zobacz [tworzenie i używanie ASE ILB][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="83da3-194">For more information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="83da3-195">Jeśli określisz nazwy domeny _ilb ase.info_, aplikacji, w tym ASE korzystania z tej domeny podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-195">If you specify the domain name _ilb-ase.info_, the apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="83da3-196">Dla aplikacji o nazwie _contoso_, adresy URL są:</span><span class="sxs-lookup"><span data-stu-id="83da3-196">For the app named _contoso_, the URLs are:</span></span>

- <span data-ttu-id="83da3-197">contoso.ilb ase.info</span><span class="sxs-lookup"><span data-stu-id="83da3-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="83da3-198">contoso.SCM.ilb ase.info</span><span class="sxs-lookup"><span data-stu-id="83da3-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="83da3-199">Publikowanie</span><span class="sxs-lookup"><span data-stu-id="83da3-199">Publishing</span></span> ##

<span data-ttu-id="83da3-200">Podobnie jak w przypadku wielodostępnej App Service w elemencie ASE można opublikować z:</span><span class="sxs-lookup"><span data-stu-id="83da3-200">As with the multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="83da3-201">Wdrażanie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="83da3-201">Web deployment.</span></span>
- <span data-ttu-id="83da3-202">FTP.</span><span class="sxs-lookup"><span data-stu-id="83da3-202">FTP.</span></span>
- <span data-ttu-id="83da3-203">Ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="83da3-203">Continuous integration.</span></span>
- <span data-ttu-id="83da3-204">Przeciągnij i upuść w konsoli Kudu.</span><span class="sxs-lookup"><span data-stu-id="83da3-204">Drag and drop in the Kudu console.</span></span>
- <span data-ttu-id="83da3-205">IDE, takie jak Visual Studio, Eclipse lub IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="83da3-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="83da3-206">Z zewnętrznego ASE te opcje publikowania wszystkich działają tak samo.</span><span class="sxs-lookup"><span data-stu-id="83da3-206">With an External ASE, these publishing options all behave the same.</span></span> <span data-ttu-id="83da3-207">Aby uzyskać więcej informacji, zobacz [wdrożenia w usłudze Azure App Service][AppDeploy].</span><span class="sxs-lookup"><span data-stu-id="83da3-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="83da3-208">Główna różnica z publikowaniem są względem ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="83da3-208">The major difference with publishing is with respect to an ILB ASE.</span></span> <span data-ttu-id="83da3-209">Z ASE ILB publikowania punktów końcowych, które są dostępne tylko za pośrednictwem ILB.</span><span class="sxs-lookup"><span data-stu-id="83da3-209">With an ILB ASE, the publishing endpoints are all available only through the ILB.</span></span> <span data-ttu-id="83da3-210">ILB znajduje się na prywatnego adresu IP w podsieci ASE w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83da3-210">The ILB is on a private IP in the ASE subnet in the virtual network.</span></span> <span data-ttu-id="83da3-211">Jeśli nie masz dostępu do sieci do ILB, nie można opublikować żadnej aplikacji na tym ASE.</span><span class="sxs-lookup"><span data-stu-id="83da3-211">If you don’t have network access to the ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="83da3-212">Jak wspomniano w [tworzenie i używanie ASE ILB][MakeILBASE], należy skonfigurować usługę DNS dla aplikacji w systemie.</span><span class="sxs-lookup"><span data-stu-id="83da3-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need to configure DNS for the apps in the system.</span></span> <span data-ttu-id="83da3-213">Która zawiera punkt końcowy SCM.</span><span class="sxs-lookup"><span data-stu-id="83da3-213">That includes the SCM endpoint.</span></span> <span data-ttu-id="83da3-214">Jeśli nie są prawidłowo zdefiniowane, nie można opublikować.</span><span class="sxs-lookup"><span data-stu-id="83da3-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="83da3-215">IDEs Twojego muszą mieć dostęp sieciowy do ILB, aby opublikować bezpośrednio do niego.</span><span class="sxs-lookup"><span data-stu-id="83da3-215">Your IDEs also need to have network access to the ILB in order to publish directly to it.</span></span>

<span data-ttu-id="83da3-216">Internetowych systemów elementu konfiguracji, takich jak GitHub i Visual Studio Team Services nie działają z ASE ILB, ponieważ punkt końcowy publikowania nie jest dostępny Internet.</span><span class="sxs-lookup"><span data-stu-id="83da3-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="83da3-217">Zamiast tego należy użyć systemu elementu konfiguracji, który wykorzystuje model ściągania, takich jak Dropbox.</span><span class="sxs-lookup"><span data-stu-id="83da3-217">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="83da3-218">Publikowanie punktów końcowych dla aplikacji w elemencie ASE ILB Użyj domeny, która została utworzona ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="83da3-218">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="83da3-219">Można to sprawdzić w profilu publikowania aplikacji i w bloku portalu aplikacji (w **omówienie** > **Essentials** oraz w **właściwości**).</span><span class="sxs-lookup"><span data-stu-id="83da3-219">You can see it in the app's publishing profile and in the app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="83da3-220">Cennik</span><span class="sxs-lookup"><span data-stu-id="83da3-220">Pricing</span></span> ##

<span data-ttu-id="83da3-221">Cennik SKU o nazwie **izolowany** został utworzony do użytku z ASEv2.</span><span class="sxs-lookup"><span data-stu-id="83da3-221">The pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="83da3-222">Wszystkie plany usługi aplikacji, które znajdują się w ASEv2 znajdują się w izolowany cennik jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="83da3-222">All App Service plans that are hosted in ASEv2 are in the Isolated pricing SKU.</span></span> <span data-ttu-id="83da3-223">Izolowane stawki planu usługi aplikacji może się różnić dla regionu.</span><span class="sxs-lookup"><span data-stu-id="83da3-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="83da3-224">Oprócz ceny dla planów usługi aplikacji istnieje szybkość płaski ASE samej siebie.</span><span class="sxs-lookup"><span data-stu-id="83da3-224">In addition to the price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="83da3-225">Szybkość płaski nie zmienia się rozmiar Twojej ASE i płaci infrastruktury ASE na domyślny skalowanie szybkość 1 dodatkowe frontonu dla każdego 15 wystąpieniach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-225">The flat rate doesn't change with the size of your ASE and pays for the ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="83da3-226">Jeśli domyślna stawka skali 1 frontonu dla każdego 15 wystąpieniach planu usługi aplikacji nie jest wystarczająca, można dostosować stosunek w której przodu kończy się zostaną dodane lub rozmiaru zakończenia przód.</span><span class="sxs-lookup"><span data-stu-id="83da3-226">If the default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust the ratio at which front-ends are added or the size of the front-ends.</span></span>  <span data-ttu-id="83da3-227">Po zmodyfikowaniu stosunek lub rozmiar płacisz za rdzeni frontonu, które nie zostanie dodany domyślnie.</span><span class="sxs-lookup"><span data-stu-id="83da3-227">When you adjust the ratio or size, you pay for the front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="83da3-228">Na przykład jeśli współczynnik skali, do 10, fronton jest dodawany do co 10 wystąpień w planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-228">For example, if you adjust the scale ratio to 10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="83da3-229">Stałe opłaty obejmuje współczynnika skalowania jeden frontonu dla każdego wystąpienia 15.</span><span class="sxs-lookup"><span data-stu-id="83da3-229">The flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="83da3-230">O stosunku skali 10 opłaty opłacać trzeci fronton, który jest dodawany do 10 wystąpieniach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83da3-230">With a scale ratio of 10, you pay a fee for the third front end that's added for the 10 App Service plan instances.</span></span> <span data-ttu-id="83da3-231">Nie trzeba płacić za go po osiągnięciu 15 wystąpienia, ponieważ zostało dodane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="83da3-231">You don't need to pay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="83da3-232">Jeśli dostosować rozmiar zakończenia przód 2 rdzenie, ale nie ustawiaj stosunek następnie na zapłacenie za dodatkowe rdzenie.</span><span class="sxs-lookup"><span data-stu-id="83da3-232">If you adjusted the size of the front-ends to 2 cores but do not adjust the ratio then you pay for the extra cores.</span></span>  <span data-ttu-id="83da3-233">ASE jest tworzony z 2 przodu zakończenia, dlatego nawet progu automatycznego skalowania będzie na zapłacenie za 2 dodatkowe rdzenie, jeśli zwiększyć rozmiar do 2 rdzenie przodu zakończenia.</span><span class="sxs-lookup"><span data-stu-id="83da3-233">An ASE is created with 2 front-ends, so even below the automatic scaling threshold you would pay for 2 extra cores if you increased the size to 2 core front-ends.</span></span>

<span data-ttu-id="83da3-234">Aby uzyskać więcej informacji, zobacz [cennik usługi aplikacji Azure][Pricing].</span><span class="sxs-lookup"><span data-stu-id="83da3-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="83da3-235">Usuń ASE</span><span class="sxs-lookup"><span data-stu-id="83da3-235">Delete an ASE</span></span> ##

<span data-ttu-id="83da3-236">Aby usunąć ASE:</span><span class="sxs-lookup"><span data-stu-id="83da3-236">To delete an ASE:</span></span> 

1. <span data-ttu-id="83da3-237">Użyj **usunąć** w górnej części **środowiska usługi aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="83da3-237">Use **Delete** at the top of the **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="83da3-238">Wprowadź nazwę użytkownika ASE, aby potwierdzić, czy chcesz go usunąć.</span><span class="sxs-lookup"><span data-stu-id="83da3-238">Enter the name of your ASE to confirm that you want to delete it.</span></span> <span data-ttu-id="83da3-239">Po usunięciu ASE usunąć całą zawartość w niej również.</span><span class="sxs-lookup"><span data-stu-id="83da3-239">When you delete an ASE, you delete all of the content within it as well.</span></span> 

    ![Usuwanie ASE][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
