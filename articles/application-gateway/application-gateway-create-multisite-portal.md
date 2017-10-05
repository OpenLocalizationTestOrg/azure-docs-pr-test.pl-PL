---
title: Kilka witryn z bramy aplikacji Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera instrukcje dotyczące konfigurowania istniejącą bramę aplikacji Azure do obsługi wielu aplikacji sieci web na tej samej bramy z portalu Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="54af5-103">Skonfigurować istniejącą bramę aplikacji do obsługi wielu aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="54af5-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54af5-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="54af5-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="54af5-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="54af5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="54af5-106">Obsługujący wiele lokacji umożliwia wdrożenie więcej niż jednej aplikacji sieci web na tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54af5-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="54af5-107">Opiera się na obecność nagłówek hosta w przychodzące żądanie HTTP, aby określić, które odbiornika będzie odbierać dane.</span><span class="sxs-lookup"><span data-stu-id="54af5-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="54af5-108">Odbiornik następnie kieruje ruch do puli zaplecza odpowiednie zgodnie z konfiguracją w definicji reguły bramy.</span><span class="sxs-lookup"><span data-stu-id="54af5-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="54af5-109">Brama aplikacji w aplikacji sieci web z włączonym protokołem SSL, opiera się rozszerzenia oznaczenia nazwy serwera (SNI), aby wybrać poprawny odbiornika dla ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="54af5-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="54af5-110">Zazwyczaj do obsługi wielu lokacji jest używane w celu zrównoważenia obciążenia żądaniami dla domen z innej witryny sieci web do innego serwera zaplecza pul.</span><span class="sxs-lookup"><span data-stu-id="54af5-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="54af5-111">Podobnie wielu domen podrzędnych tej samej domeny katalogu głównego może być hostowana na tę samą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54af5-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="54af5-112">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="54af5-112">Scenario</span></span>

<span data-ttu-id="54af5-113">W poniższym przykładzie brama aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam.</span><span class="sxs-lookup"><span data-stu-id="54af5-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="54af5-114">Podobnych konfiguracji może posłużyć do hosta poddomen, takich jak app.contoso.com i blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="54af5-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![Scenariusz w wielu lokacjach][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="54af5-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="54af5-116">Before you begin</span></span>

<span data-ttu-id="54af5-117">W tym scenariuszu dodaje obsługę wielu lokacji do istniejącej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54af5-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="54af5-118">Aby ukończyć ten scenariusz, istniejącą bramę aplikacji musi być dostępna do skonfigurowania.</span><span class="sxs-lookup"><span data-stu-id="54af5-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="54af5-119">Odwiedź stronę [Utwórz bramę aplikacji przy użyciu portalu](application-gateway-create-gateway-portal.md) informacje na temat tworzenia aplikacji w warstwie podstawowa bramy w portalu.</span><span class="sxs-lookup"><span data-stu-id="54af5-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="54af5-120">Poniżej przedstawiono kroki niezbędne do zaktualizuj bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="54af5-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="54af5-121">Tworzenie pul zaplecza dla każdej witryny.</span><span class="sxs-lookup"><span data-stu-id="54af5-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="54af5-122">Utwórz odbiornik dla każdej lokacji obsługuje bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54af5-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="54af5-123">Utwórz reguły mapowania każdego odbiornik mający odpowiednie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="54af5-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="54af5-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="54af5-124">Requirements</span></span>

* <span data-ttu-id="54af5-125">**Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="54af5-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="54af5-126">Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.</span><span class="sxs-lookup"><span data-stu-id="54af5-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="54af5-127">Można także nazwę FQDN.</span><span class="sxs-lookup"><span data-stu-id="54af5-127">FQDN can also be used.</span></span>
* <span data-ttu-id="54af5-128">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="54af5-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="54af5-129">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="54af5-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="54af5-130">**Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54af5-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="54af5-131">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="54af5-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="54af5-132">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="54af5-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="54af5-133">Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.</span><span class="sxs-lookup"><span data-stu-id="54af5-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="54af5-134">**Reguła:** reguły wiąże odbiornika puli serwera zaplecza i definiuje puli serwera zaplecza, których ruch powinny być kierowane do, gdy trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="54af5-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="54af5-135">Reguły są przetwarzane w kolejności, w jakiej występują, a ruch zostanie skierowany przez pierwszą regułę odpowiadającą niezależnie od szczegółowością.</span><span class="sxs-lookup"><span data-stu-id="54af5-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="54af5-136">Na przykład jeśli utworzono regułę przy użyciu odbiornika podstawowe i regułę przy użyciu odbiornika obejmujący wiele lokacji zarówno w tym samym porcie, reguły z wieloma lokacjami odbiornika musi być wymieniona przed regułę przy użyciu podstawowego odbiornika w kolejności reguły obejmujący wiele lokacji, aby działać zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="54af5-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="54af5-137">**Certyfikaty:** każdego odbiornika wymaga unikatowego certyfikatu, w tym przykładzie 2 odbiorników są tworzone dla wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="54af5-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="54af5-138">Dwa certyfikaty PFX oraz hasła dla nich muszą zostać utworzone.</span><span class="sxs-lookup"><span data-stu-id="54af5-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="54af5-139">Tworzenie pul zaplecza dla każdej lokacji</span><span class="sxs-lookup"><span data-stu-id="54af5-139">Create back-end pools for each site</span></span>

<span data-ttu-id="54af5-140">Dla każdej lokacji puli zaplecza, że aplikacja obsługuje bramy jest potrzebne, w tym przypadku 2 są można utworzyć, jeden dla contoso11.com i jeden dla fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="54af5-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="54af5-141">Krok 1</span><span class="sxs-lookup"><span data-stu-id="54af5-141">Step 1</span></span>

<span data-ttu-id="54af5-142">Przejdź do istniejącej bramy aplikacji w portalu Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54af5-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="54af5-143">Wybierz **pul zaplecza** i kliknij przycisk **Dodaj**</span><span class="sxs-lookup"><span data-stu-id="54af5-143">Select **Backend pools** and click **Add**</span></span>

![Dodawanie pul zaplecza][7]

### <a name="step-2"></a><span data-ttu-id="54af5-145">Krok 2</span><span class="sxs-lookup"><span data-stu-id="54af5-145">Step 2</span></span>

<span data-ttu-id="54af5-146">Wprowadź informacje dla tej puli zaplecza **pool1**, dodawanie adresów ip lub nazwy FQDN dla serwerów zaplecza i kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="54af5-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![Ustawienia pool1 puli wewnętrznej bazy danych][8]

### <a name="step-3"></a><span data-ttu-id="54af5-148">Krok 3</span><span class="sxs-lookup"><span data-stu-id="54af5-148">Step 3</span></span>

<span data-ttu-id="54af5-149">W bloku pul zaplecza kliknij **Dodaj** można dodać dodatkowe puli zaplecza **pool2**, dodawanie adresów ip lub nazwy FQDN dla serwerów zaplecza i kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="54af5-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![Ustawienia pool2 puli wewnętrznej bazy danych][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="54af5-151">Tworzenie odbiorników dla każdego zaplecza</span><span class="sxs-lookup"><span data-stu-id="54af5-151">Create listeners for each back-end</span></span>

<span data-ttu-id="54af5-152">Usługa Application Gateway bazuje na nagłówkach hosta HTTP 1.1 w celu hostowania więcej niż jednej witryny sieci Web na tym samym publicznym adresie IP i porcie.</span><span class="sxs-lookup"><span data-stu-id="54af5-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="54af5-153">Podstawowe odbiornika utworzone w portalu nie zawiera tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="54af5-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="54af5-154">Krok 1</span><span class="sxs-lookup"><span data-stu-id="54af5-154">Step 1</span></span>

<span data-ttu-id="54af5-155">Kliknij przycisk **odbiorników** na istniejące bramy aplikacji i kliknij przycisk **obejmujący wiele lokacji** do dodania pierwszego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="54af5-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![obiekty nasłuchujące bloku — omówienie][1]

### <a name="step-2"></a><span data-ttu-id="54af5-157">Krok 2</span><span class="sxs-lookup"><span data-stu-id="54af5-157">Step 2</span></span>

<span data-ttu-id="54af5-158">Wprowadź informacje dla odbiornika.</span><span class="sxs-lookup"><span data-stu-id="54af5-158">Fill out the information for the listener.</span></span> <span data-ttu-id="54af5-159">W tym przykładzie protokół SSL jest skonfigurowany zakończenia, Utwórz nowy port serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="54af5-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="54af5-160">Przekaż certyfikat PFX, który ma być używany dla zakończenia połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="54af5-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="54af5-161">Jedyną różnicą w tym bloku w porównaniu do bloku standardowe odbiornika podstawowe jest nazwą hosta.</span><span class="sxs-lookup"><span data-stu-id="54af5-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![odbiornik bloku właściwości][2]

### <a name="step-3"></a><span data-ttu-id="54af5-163">Krok 3</span><span class="sxs-lookup"><span data-stu-id="54af5-163">Step 3</span></span>

<span data-ttu-id="54af5-164">Kliknij przycisk **obejmujący wiele lokacji** i utwórz inny odbiornik, zgodnie z opisem w poprzednim kroku dla drugiej witryny.</span><span class="sxs-lookup"><span data-stu-id="54af5-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="54af5-165">Upewnij się używała innego certyfikatu dla drugiego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="54af5-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="54af5-166">Jedyną różnicą w tym bloku w porównaniu do bloku standardowe odbiornika podstawowe jest nazwą hosta.</span><span class="sxs-lookup"><span data-stu-id="54af5-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="54af5-167">Wypełnij informacje odbiornika i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="54af5-167">Fill out the information for the listener and click **OK**.</span></span>

![odbiornik bloku właściwości][3]

> [!NOTE]
> <span data-ttu-id="54af5-169">Tworzenie odbiorników w portalu Azure dla aplikacji bramy jest długotrwałych zadań, może upłynąć trochę czasu, aby utworzyć dwa odbiorniki w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="54af5-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="54af5-170">Po zakończeniu Pokaż odbiorników w portalu, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="54af5-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![odbiornik — omówienie][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="54af5-172">Tworzenie reguł do mapowania odbiorników pul zaplecza</span><span class="sxs-lookup"><span data-stu-id="54af5-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="54af5-173">Krok 1</span><span class="sxs-lookup"><span data-stu-id="54af5-173">Step 1</span></span>

<span data-ttu-id="54af5-174">Przejdź do istniejącej bramy aplikacji w portalu Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54af5-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="54af5-175">Wybierz **reguły** i wybrać istniejącą regułę domyślną **rule1** i kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="54af5-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="54af5-176">Krok 2</span><span class="sxs-lookup"><span data-stu-id="54af5-176">Step 2</span></span>

<span data-ttu-id="54af5-177">Wypełnij bloku reguł, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="54af5-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="54af5-178">Wybieranie pierwszy odbiornika i pierwszej puli, a następnie klikając polecenie **zapisać** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="54af5-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![Edytuj istniejącą regułę][6]

### <a name="step-3"></a><span data-ttu-id="54af5-180">Krok 3</span><span class="sxs-lookup"><span data-stu-id="54af5-180">Step 3</span></span>

<span data-ttu-id="54af5-181">Kliknij przycisk **podstawowe reguły** utworzyć drugą regułę.</span><span class="sxs-lookup"><span data-stu-id="54af5-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="54af5-182">Wypełnij formularz drugi odbiornika, a drugie puli wewnętrznej bazy danych, a następnie kliknij przycisk **OK** do zapisania.</span><span class="sxs-lookup"><span data-stu-id="54af5-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![Dodawanie bloku podstawowe reguły][10]

<span data-ttu-id="54af5-184">W tym scenariuszu kończy się konfigurowanie istniejącą bramę aplikacji z obsługą wielu lokacji za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="54af5-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54af5-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54af5-185">Next steps</span></span>

<span data-ttu-id="54af5-186">Dowiedz się, jak chronić witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="54af5-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
