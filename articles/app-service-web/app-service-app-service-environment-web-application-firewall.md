---
title: "aaaConfiguring sieci Web aplikacji zapory (WAF) dla środowiska usługi aplikacji"
description: "Dowiedz się, jak zapory tooconfigure aplikacji sieci web przed środowiska usługi aplikacji."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="9e839-103">Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="9e839-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="9e839-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9e839-104">Overview</span></span>
<span data-ttu-id="9e839-105">Sieci Web zapór aplikacji, takich jak hello [Barracuda zapory aplikacji sieci Web dla platformy Azure](https://www.barracuda.com/programs/azure) dostępnych na powitania [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ułatwia zabezpieczenie aplikacji sieci web, sprawdzając tooblock ruch przychodzący sieci web SQL iniekcji, skryptów krzyżowych, przekazywanie złośliwego oprogramowania i aplikacji przed atakami DDoS i inne ataki.</span><span class="sxs-lookup"><span data-stu-id="9e839-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="9e839-106">Sprawdza również hello odpowiedzi z serwerów sieci web zaplecza powitania dla zapobiegania utracie danych (DLP).</span><span class="sxs-lookup"><span data-stu-id="9e839-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="9e839-107">W połączeniu z hello izolacji i dodatkowe skalowanie podał środowiska usługi App Service, zapewnia to idealne rozwiązanie w środowisku toohost biznesowe krytyczne aplikacje sieci web muszą toowithstand złośliwymi żądaniami i dużych obciążeń ruchem.</span><span class="sxs-lookup"><span data-stu-id="9e839-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="9e839-108">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9e839-108">Setup</span></span>
<span data-ttu-id="9e839-109">Dla tego dokumentu, który będzie skonfigurowanie naszych środowiska usługi aplikacji za wiele obciążenia zrównoważonym wystąpień Barracuda zapory aplikacji sieci Web tak, aby tylko na ruch z hello zapory aplikacji sieci Web można osiągnąć hello środowiska usługi aplikacji i nie będzie dostępny z hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="9e839-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="9e839-110">Firma Microsoft będzie miał usługi Azure Traffic Manager przed naszych saldo tooload wystąpień Barracuda zapory aplikacji sieci Web w centrach danych platformy Azure i regionów.</span><span class="sxs-lookup"><span data-stu-id="9e839-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="9e839-111">Diagramu wysokiego poziomu hello instalacji będzie wyglądała co przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="9e839-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Architektura][Architecture] 

> <span data-ttu-id="9e839-113">Uwaga: Z wprowadzeniem hello [ILB obsługę środowiska usługi aplikacji](app-service-environment-with-internal-load-balancer.md), można skonfigurować toobe hello ASE niedostępne z hello DMZ i być dostępne toohello sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="9e839-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="9e839-114">Konfigurowanie środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="9e839-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="9e839-115">tooconfigure środowiska usługi aplikacji można znaleźć zbyt[naszej dokumentacji](app-service-web-how-to-create-an-app-service-environment.md) na powitania podmiotu.</span><span class="sxs-lookup"><span data-stu-id="9e839-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="9e839-116">Po utworzeniu środowiska usługi aplikacji utworzony, można utworzyć [aplikacje sieci Web](app-service-web-overview.md), [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md) i [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) w tym środowisku, które będą wszystkie chronione za hello zapory aplikacji sieci Web firma Microsoft Skonfiguruj w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="9e839-117">Konfigurowanie usługi w chmurze zapory aplikacji sieci Web Barracuda</span><span class="sxs-lookup"><span data-stu-id="9e839-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="9e839-118">Ma barracuda [szczegółowe artykułu](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) na temat wdrażania jego zapory aplikacji sieci Web na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9e839-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="9e839-119">Jednak ponieważ firma Microsoft ma nadmiarowości i nie wprowadzenie pojedynczego punktu awarii, ma co najmniej 2 toodeploy zapory aplikacji sieci Web wystąpienia maszyn wirtualnych na powitania tej samej usługi chmury, gdy następujące instrukcje.</span><span class="sxs-lookup"><span data-stu-id="9e839-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="9e839-120">Dodawanie tooCloud punktów końcowych usługi</span><span class="sxs-lookup"><span data-stu-id="9e839-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="9e839-121">Gdy masz 2 lub wirtualna zapory aplikacji sieci Web więcej wystąpień w usłudze w chmurze można użyć hello [portalu Azure](https://portal.azure.com/) tooadd HTTP i HTTPS punkty końcowe, które są używane przez aplikację, jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Konfigurowanie punktu końcowego][ConfigureEndpoint]

<span data-ttu-id="9e839-123">Aplikacje korzystanie z innych punktów końcowych, aby tooadd się, że te listy toothis również.</span><span class="sxs-lookup"><span data-stu-id="9e839-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="9e839-124">Konfigurowanie Barracuda zapory aplikacji sieci Web za pomocą portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="9e839-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="9e839-125">Barracuda zapory aplikacji sieci Web używa TCP Port 8000 dla konfiguracji za pomocą portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9e839-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="9e839-126">Ponieważ istnieje wiele wystąpień maszyn wirtualnych zapory aplikacji sieci Web hello należy toorepeat hello tutaj kroki dla każdego wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e839-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="9e839-127">Uwaga: Po wykonaniu konfiguracji zapory aplikacji sieci Web, Usuń punkt końcowy protokołu TCP/8000 hello z tookeep maszyny wirtualne zapory aplikacji sieci Web z zapory aplikacji sieci Web bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="9e839-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="9e839-128">Dodaj punkt końcowy zarządzania hello jak pokazano w obrazie hello poniżej tooconfigure Twojego Barracuda zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9e839-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Dodaj punkt końcowy zarządzania][AddManagementEndpoint]

<span data-ttu-id="9e839-130">Punkt końcowy zarządzania toohello toobrowse przeglądarki w systemie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9e839-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="9e839-131">Usługi w chmurze jest nazywany test.cloudapp.net, czy dostęp do tego punktu końcowego przechodząc toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="9e839-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="9e839-132">Powinna zostać wyświetlona strona logowania, takich jak poniżej że możesz zalogować się przy użyciu poświadczeń określonych w fazie instalacji maszyny Wirtualnej hello zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9e839-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Zarządzanie strony logowania][ManagementLoginPage]

<span data-ttu-id="9e839-134">Raz logowania jako hello powinien zostać wyświetlony pulpit nawigacyjny w hello obraz poniżej przedstawia podstawowe dane statystyczne dotyczące hello ochrony zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9e839-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Pulpit nawigacyjny zarządzania][ManagementDashboard]

<span data-ttu-id="9e839-136">Kliknięcie karty usługi hello umożliwi Ci w skonfigurowaniu Twojej zapory aplikacji sieci Web dla usług, które ochrony.</span><span class="sxs-lookup"><span data-stu-id="9e839-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="9e839-137">Aby uzyskać więcej informacji na temat konfigurowania sieci Barracuda zapory aplikacji sieci Web można znaleźć [dokumentacji](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="9e839-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="9e839-138">W przykładzie hello poniżej aplikacji sieci Web platformy Azure obsługujące ruch HTTP i HTTPS została skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="9e839-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Dodaj zarządzania usługi][ManagementAddServices]

> <span data-ttu-id="9e839-140">Uwaga: W zależności od sposobu konfiguracji aplikacji i jakie funkcje są używane w środowisku usługi aplikacji, będzie potrzebny tooforward ruch TCP porty inne niż 80 i 443, np. Jeśli masz ustawienia protokołu SSL z adresu IP dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9e839-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="9e839-141">Lista portów sieci używanych w środowisku usługi aplikacji można znaleźć za[ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) sekcji porty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="9e839-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="9e839-142">Konfigurowanie Menedżera ruchu Microsoft Azure (OPCJONALNIE)</span><span class="sxs-lookup"><span data-stu-id="9e839-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="9e839-143">Jeśli aplikacja jest dostępna w wielu regionach, a następnie konieczne będzie saldo tooload ich za [usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e839-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="9e839-144">toodo, dzięki czemu można dodać punktu końcowego w hello [klasycznego portalu Azure](https://manage.azure.com) za pomocą nazwy usługi w chmurze hello z zapory aplikacji sieci Web w w profilu usługi Traffic Manager hello, jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Punkt końcowy Menedżera ruchu][TrafficManagerEndpoint]

<span data-ttu-id="9e839-146">Jeśli aplikacja wymaga uwierzytelniania, upewnij się, że jakiś zasób, który nie wymaga uwierzytelniania dla Menedżera ruchu tooping hello dostępność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9e839-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="9e839-147">Adres URL hello pod hello sekcji konfiguracji można skonfigurować na powitania [klasycznego portalu Azure](https://manage.azure.com) jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="9e839-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Konfigurowanie usługi Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="9e839-149">tooforward hello polecenia ping Menedżera ruchu z aplikacji tooyour zapory aplikacji sieci Web, należy tłumaczeń toosetup witryny sieci Web na Barracuda WAF tooforward ruchu tooyour aplikacji jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Tłumaczenie witryny sieci Web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="9e839-151">Zabezpieczanie tooApp ruchu usługi środowisko przy użyciu sieci zabezpieczeń grupy (NSG)</span><span class="sxs-lookup"><span data-stu-id="9e839-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="9e839-152">Wykonaj hello [ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) dla szczegóły dotyczące ograniczania ruchu tooyour środowiska usługi aplikacji z hello zapory aplikacji sieci Web tylko przy użyciu adresu hello VIP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9e839-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="9e839-153">Oto przykład polecenia programu Powershell do wykonywania tego zadania TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="9e839-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="9e839-154">Zastąp hello SourceAddressPrefix hello wirtualny adres IP (VIP) usługi w chmurze Twoje WAF.</span><span class="sxs-lookup"><span data-stu-id="9e839-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="9e839-155">Uwaga: hello VIP usługi w chmurze ulegnie zmianie po usunięcie i ponowne utworzenie hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9e839-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="9e839-156">Upewnij się, że tooupdate hello adresu IP w grupie zasobów sieciowych powitania po przeprowadzeniu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9e839-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
