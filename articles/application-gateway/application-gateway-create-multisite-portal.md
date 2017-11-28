---
title: aaaHost wiele lokacji z bramy aplikacji Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera instrukcje tooconfigure istniejącą bramę aplikacji Azure do obsługi wielu aplikacji sieci web na powitania tej samej bramy z hello portalu Azure."
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
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="14a5a-103">Skonfigurować istniejącą bramę aplikacji do obsługi wielu aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="14a5a-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="14a5a-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14a5a-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="14a5a-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="14a5a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="14a5a-106">Obsługa wielu lokacji pozwala toodeploy więcej niż jednej aplikacji sieci web na powitania tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14a5a-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="14a5a-107">Opiera się na obecność nagłówek hosta w hello przychodzące żądanie HTTP, toodetermine odbiornika, które będzie odbierać dane.</span><span class="sxs-lookup"><span data-stu-id="14a5a-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="14a5a-108">odbiornik Hello następnie kieruje ruch puli zaplecza tooappropriate zgodnie z konfiguracją w definicji reguły hello hello bramy.</span><span class="sxs-lookup"><span data-stu-id="14a5a-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="14a5a-109">W aplikacji sieci web z włączonym protokołem SSL bramy aplikacji polega na powitania oznaczenia nazwy serwera (SNI) rozszerzenia toochoose hello poprawne odbiornika dla ruchu w sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="14a5a-110">Zazwyczaj jest używane, do obsługi wielu lokacji tooload równoważenie żądań dla pul serwerów zaplecza toodifferent domeny innej witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="14a5a-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="14a5a-111">Podobnie wielu poddomen powitalne tej samej domeny katalogu głównego może być również obsługiwane na hello tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14a5a-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="14a5a-112">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="14a5a-112">Scenario</span></span>

<span data-ttu-id="14a5a-113">W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam.</span><span class="sxs-lookup"><span data-stu-id="14a5a-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="14a5a-114">Podobne instalacja może być poddomeny używane toohost jak app.contoso.com i blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="14a5a-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![Scenariusz w wielu lokacjach][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="14a5a-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="14a5a-116">Before you begin</span></span>

<span data-ttu-id="14a5a-117">W tym scenariuszu dodaje obsługę wielu lokacji tooan istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14a5a-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="14a5a-118">toocomplete ten scenariusz istniejącą bramę aplikacji wymaga toobe tooconfigure dostępne.</span><span class="sxs-lookup"><span data-stu-id="14a5a-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="14a5a-119">Odwiedź stronę [utworzyć bramę aplikacji przy użyciu portalu hello](application-gateway-create-gateway-portal.md) toolearn jak toocreate brama aplikacji w warstwie podstawowa w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="14a5a-120">Brama aplikacji hello tooupdate wymagane czynności hello to Hello następujące:</span><span class="sxs-lookup"><span data-stu-id="14a5a-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="14a5a-121">Tworzenie pul zaplecza toouse dla każdej lokacji.</span><span class="sxs-lookup"><span data-stu-id="14a5a-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="14a5a-122">Utwórz odbiornik dla każdej lokacji obsługuje bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14a5a-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="14a5a-123">Utwórz toomap reguły każdego odbiornika z hello odpowiednie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="14a5a-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="14a5a-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="14a5a-124">Requirements</span></span>

* <span data-ttu-id="14a5a-125">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="14a5a-126">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="14a5a-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="14a5a-127">Można także nazwę FQDN.</span><span class="sxs-lookup"><span data-stu-id="14a5a-127">FQDN can also be used.</span></span>
* <span data-ttu-id="14a5a-128">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="14a5a-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="14a5a-129">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="14a5a-130">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="14a5a-131">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="14a5a-132">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="14a5a-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="14a5a-133">Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.</span><span class="sxs-lookup"><span data-stu-id="14a5a-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="14a5a-134">**Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="14a5a-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="14a5a-135">Reguły są przetwarzane w kolejności hello, są one wyświetlane, a ruch zostanie skierowany za pośrednictwem hello pierwszą regułę odpowiadającą niezależnie od szczegółowością.</span><span class="sxs-lookup"><span data-stu-id="14a5a-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="14a5a-136">Na przykład jeśli masz przy użyciu odbiornika podstawowe reguły i zasady przy użyciu odbiornika obejmujący wiele lokacji zarówno na powitania sam port hello reguły z hello obejmujący wiele lokacji odbiornika musi być wymienione przed reguły hello przy hello odbiornika podstawowych, aby hello toofunction reguły obejmujący wiele lokacji jako Oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="14a5a-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="14a5a-137">**Certyfikaty:** każdego odbiornika wymaga unikatowego certyfikatu, w tym przykładzie 2 odbiorników są tworzone dla wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="14a5a-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="14a5a-138">Dwa certyfikaty PFX i hello hasła dla nich muszą toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="14a5a-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="14a5a-139">Tworzenie pul zaplecza dla każdej lokacji</span><span class="sxs-lookup"><span data-stu-id="14a5a-139">Create back-end pools for each site</span></span>

<span data-ttu-id="14a5a-140">Dla każdej lokacji puli zaplecza, że aplikacja obsługuje bramy jest potrzebne, w tym przypadku 2 są można utworzyć, jeden dla contoso11.com i jeden dla fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="14a5a-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="14a5a-141">Krok 1</span><span class="sxs-lookup"><span data-stu-id="14a5a-141">Step 1</span></span>

<span data-ttu-id="14a5a-142">Przejdź tooan istniejącą bramę aplikacji w portalu Azure (https://portal.azure.com) hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="14a5a-143">Wybierz **pul zaplecza** i kliknij przycisk **Dodaj**</span><span class="sxs-lookup"><span data-stu-id="14a5a-143">Select **Backend pools** and click **Add**</span></span>

![Dodawanie pul zaplecza][7]

### <a name="step-2"></a><span data-ttu-id="14a5a-145">Krok 2</span><span class="sxs-lookup"><span data-stu-id="14a5a-145">Step 2</span></span>

<span data-ttu-id="14a5a-146">Wprowadź informacje hello puli zaplecza hello **pool1**, dodawanie hello adresy ip lub nazwy FQDN dla serwerów zaplecza hello i kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="14a5a-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![Ustawienia pool1 puli wewnętrznej bazy danych][8]

### <a name="step-3"></a><span data-ttu-id="14a5a-148">Krok 3</span><span class="sxs-lookup"><span data-stu-id="14a5a-148">Step 3</span></span>

<span data-ttu-id="14a5a-149">W bloku pul zaplecza powitania kliknij **Dodaj** tooadd dodatkowe puli zaplecza **pool2**, dodawanie hello adresy ip lub nazwy FQDN dla serwerów zaplecza hello i kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="14a5a-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![Ustawienia pool2 puli wewnętrznej bazy danych][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="14a5a-151">Tworzenie odbiorników dla każdego zaplecza</span><span class="sxs-lookup"><span data-stu-id="14a5a-151">Create listeners for each back-end</span></span>

<span data-ttu-id="14a5a-152">Brama aplikacji w korzysta z protokołu HTTP 1.1 toohost nagłówków hosta więcej niż jednej witryny sieci Web na hello sam publiczny adres IP i portu.</span><span class="sxs-lookup"><span data-stu-id="14a5a-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="14a5a-153">odbiornik podstawowe Hello utworzone w portalu hello nie zawiera tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="14a5a-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="14a5a-154">Krok 1</span><span class="sxs-lookup"><span data-stu-id="14a5a-154">Step 1</span></span>

<span data-ttu-id="14a5a-155">Kliknij przycisk **odbiorników** hello istniejącą bramę aplikacji i kliknij przycisk **obejmujący wiele lokacji** tooadd hello pierwszy odbiornika.</span><span class="sxs-lookup"><span data-stu-id="14a5a-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![obiekty nasłuchujące bloku — omówienie][1]

### <a name="step-2"></a><span data-ttu-id="14a5a-157">Krok 2</span><span class="sxs-lookup"><span data-stu-id="14a5a-157">Step 2</span></span>

<span data-ttu-id="14a5a-158">Wprowadź informacje powitania dla odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="14a5a-159">W tym przykładzie protokół SSL jest skonfigurowany zakończenia, Utwórz nowy port serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="14a5a-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="14a5a-160">Przekaż toobe certyfikatu PFX hello używane do kończenia żądań SSL.</span><span class="sxs-lookup"><span data-stu-id="14a5a-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="14a5a-161">Jedyną różnicą Hello tego bloku standardowe odbiornika podstawowe toohello porównywana blok jest hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="14a5a-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![odbiornik bloku właściwości][2]

### <a name="step-3"></a><span data-ttu-id="14a5a-163">Krok 3</span><span class="sxs-lookup"><span data-stu-id="14a5a-163">Step 3</span></span>

<span data-ttu-id="14a5a-164">Kliknij przycisk **obejmujący wiele lokacji** i utwórz inny odbiornik, zgodnie z opisem w poprzednim kroku hello hello drugiej witryny.</span><span class="sxs-lookup"><span data-stu-id="14a5a-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="14a5a-165">Upewnij się, że toouse innego certyfikatu dla odbiornika drugi hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="14a5a-166">Jedyną różnicą Hello tego bloku standardowe odbiornika podstawowe toohello porównywana blok jest hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="14a5a-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="14a5a-167">Podanie informacji powitania dla odbiornika hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="14a5a-167">Fill out hello information for hello listener and click **OK**.</span></span>

![odbiornik bloku właściwości][3]

> [!NOTE]
> <span data-ttu-id="14a5a-169">Tworzenie odbiorników w portalu Azure bramy aplikacji hello jest długotrwałych zadań, może upłynąć niektórych hello toocreate czasu dwa odbiorniki w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="14a5a-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="14a5a-170">Gdy odbiorników pełną hello wyświetlane w portalu hello w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="14a5a-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![odbiornik — omówienie][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="14a5a-172">Tworzenie reguł toomap odbiorników toobackend pule</span><span class="sxs-lookup"><span data-stu-id="14a5a-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="14a5a-173">Krok 1</span><span class="sxs-lookup"><span data-stu-id="14a5a-173">Step 1</span></span>

<span data-ttu-id="14a5a-174">Przejdź tooan istniejącą bramę aplikacji w portalu Azure (https://portal.azure.com) hello.</span><span class="sxs-lookup"><span data-stu-id="14a5a-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="14a5a-175">Wybierz **reguły** i wybrać istniejącą regułę domyślną hello **rule1** i kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="14a5a-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="14a5a-176">Krok 2</span><span class="sxs-lookup"><span data-stu-id="14a5a-176">Step 2</span></span>

<span data-ttu-id="14a5a-177">Wypełnij bloku zasady hello w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="14a5a-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="14a5a-178">Wybieranie odbiornika pierwszy hello i pierwszej puli, a następnie klikając polecenie **zapisać** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="14a5a-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![Edytuj istniejącą regułę][6]

### <a name="step-3"></a><span data-ttu-id="14a5a-180">Krok 3</span><span class="sxs-lookup"><span data-stu-id="14a5a-180">Step 3</span></span>

<span data-ttu-id="14a5a-181">Kliknij przycisk **podstawowe reguły** toocreate hello drugą regułę.</span><span class="sxs-lookup"><span data-stu-id="14a5a-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="14a5a-182">Wypełnij formularz hello z hello drugi odbiornika, a drugie puli zaplecza, a następnie kliknij przycisk **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="14a5a-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![Dodawanie bloku podstawowe reguły][10]

<span data-ttu-id="14a5a-184">W tym scenariuszu kończy się konfigurowanie istniejącą bramę aplikacji z obsługą wielu lokacji za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="14a5a-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14a5a-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14a5a-185">Next steps</span></span>

<span data-ttu-id="14a5a-186">Dowiedz się, jak tooprotect witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="14a5a-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
