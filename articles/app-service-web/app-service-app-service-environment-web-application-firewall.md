---
title: "Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji"
description: "Informacje o sposobie konfigurowania zapory aplikacji sieci web przed środowiska usługi aplikacji."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="fdfa4-103">Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="fdfa4-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="fdfa4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fdfa4-104">Overview</span></span>
<span data-ttu-id="fdfa4-105">Zapory aplikacji sieci Web, takich jak [Barracuda zapory aplikacji sieci Web dla platformy Azure](https://www.barracuda.com/programs/azure) dostępnych na [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ułatwia zabezpieczenie aplikacji sieci web, sprawdzając ruch przychodzący sieci web do blokowania przekazywania złośliwego oprogramowania iniekcji skryptów krzyżowych, SQL i aplikacji przed atakami DDoS i inne ataki.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="fdfa4-106">Sprawdza również odpowiedzi z serwerów sieci web zaplecza dla zapobiegania utracie danych (DLP).</span><span class="sxs-lookup"><span data-stu-id="fdfa4-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="fdfa4-107">W połączeniu z izolacji i dodatkowe skalowanie podał środowiska usługi App Service, zapewnia to idealne środowiska do hosta biznesowe krytyczne aplikacje sieci web muszą wytrzymać złośliwymi żądaniami i dużych obciążeń ruchem.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="fdfa4-108">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="fdfa4-108">Setup</span></span>
<span data-ttu-id="fdfa4-109">Dla tego dokumentu, który będzie skonfigurowanie naszych środowiska usługi aplikacji za wiele obciążenia zrównoważonym wystąpień Barracuda zapory aplikacji sieci Web tak, aby tylko na ruch z zapory aplikacji sieci Web można osiągnąć środowiska usługi aplikacji i nie będzie dostępny od strefy DMZ.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="fdfa4-110">Firma Microsoft będzie miał usługi Azure Traffic Manager przed naszych wystąpień Barracuda zapory aplikacji sieci Web w celu zrównoważenia obciążenia w centrach danych platformy Azure i regionów.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="fdfa4-111">Diagramu wysokiego poziomu ustawień będzie wyglądała co przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architektura][Architecture] 

> <span data-ttu-id="fdfa4-113">Uwaga: wraz z wprowadzeniem [ILB obsługę środowiska usługi aplikacji](app-service-environment-with-internal-load-balancer.md), można skonfigurować ASE niedostępny od strefy DMZ i udostępniane wyłącznie do sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="fdfa4-114">Konfigurowanie środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="fdfa4-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="fdfa4-115">Aby skonfigurować środowisko usługi aplikacji, zajrzyj do [naszej dokumentacji](app-service-web-how-to-create-an-app-service-environment.md) na ten temat.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="fdfa4-116">Po utworzeniu środowiska usługi aplikacji utworzony, można utworzyć [aplikacje sieci Web](app-service-web-overview.md), [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md) i [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) w tym środowisku, które będą wszystkie chronione za skonfigurowanie w następnej sekcji zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="fdfa4-117">Konfigurowanie usługi w chmurze zapory aplikacji sieci Web Barracuda</span><span class="sxs-lookup"><span data-stu-id="fdfa4-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="fdfa4-118">Ma barracuda [szczegółowe artykułu](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) na temat wdrażania jego zapory aplikacji sieci Web na maszynie wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="fdfa4-119">Jednak ponieważ firma Microsoft ma nadmiarowości i nie wprowadzenie pojedynczego punktu awarii, którą chcesz wdrożyć co najmniej 2 VMs wystąpienie zapory aplikacji sieci Web do tej samej usługi w chmurze, gdy następujące instrukcje.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="fdfa4-120">Dodawanie punktów końcowych do usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="fdfa4-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="fdfa4-121">Gdy masz 2 lub wirtualna zapory aplikacji sieci Web więcej wystąpień w usłudze w chmurze można użyć [portalu Azure](https://portal.azure.com/) można dodać punktów końcowych HTTP i HTTPS, które są używane przez aplikację, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Konfigurowanie punktu końcowego][ConfigureEndpoint]

<span data-ttu-id="fdfa4-123">Jeśli aplikacje korzystanie z innych punktów końcowych, upewnij się, że te do tej listy, a także dodać.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="fdfa4-124">Konfigurowanie Barracuda zapory aplikacji sieci Web za pomocą portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="fdfa4-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="fdfa4-125">Barracuda zapory aplikacji sieci Web używa TCP Port 8000 dla konfiguracji za pomocą portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="fdfa4-126">Ponieważ istnieje wiele wystąpień maszyn wirtualnych zapory aplikacji sieci Web należy powtórzyć kroki opisane w tym miejscu dla każdego wystąpienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="fdfa4-127">Uwaga: Po wykonaniu konfiguracji zapory aplikacji sieci Web, usuwanie punktu końcowego TCP/8000 Twojej VMs zapory aplikacji sieci Web w celu poprawy bezpieczeństwa Twojej zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="fdfa4-128">Dodaj punkt końcowy zarządzania, jak pokazano na poniższej ilustracji skonfigurować Twoje Barracuda zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Dodaj punkt końcowy zarządzania][AddManagementEndpoint]

<span data-ttu-id="fdfa4-130">Korzystanie z przeglądarki, aby przejść do zarządzania punktem końcowym usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="fdfa4-131">Usługi w chmurze jest nazywany test.cloudapp.net, czy dostęp do tego punktu końcowego przechodząc do http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="fdfa4-132">Powinna zostać wyświetlona strona logowania, takich jak poniżej że możesz zalogować się przy użyciu poświadczeń określonych w fazie konfiguracji maszyny Wirtualnej zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Zarządzanie strony logowania][ManagementLoginPage]

<span data-ttu-id="fdfa4-134">Raz logowania powinien zostać wyświetlony pulpit nawigacyjny, na poniższej ilustracji, która przedstawia podstawowe dane statystyczne dotyczące ochrony zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Pulpit nawigacyjny zarządzania][ManagementDashboard]

<span data-ttu-id="fdfa4-136">Klikając na karcie usługi będzie można skonfigurować zapory Twojej aplikacji sieci Web dla usług, które ochrony.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="fdfa4-137">Aby uzyskać więcej informacji na temat konfigurowania sieci Barracuda zapory aplikacji sieci Web można znaleźć [dokumentacji](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="fdfa4-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="fdfa4-138">W przykładzie poniżej aplikacji sieci Web platformy Azure obsługujące ruch HTTP i HTTPS została skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Dodaj zarządzania usługi][ManagementAddServices]

> <span data-ttu-id="fdfa4-140">Uwaga: W zależności od sposobu konfiguracji aplikacji i jakie funkcje są używane w środowisku usługi aplikacji, konieczne będzie przesyłał dalej ruch dla protokołu TCP porty inne niż 80 i 443, np. Jeśli masz ustawienia protokołu SSL z adresu IP dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="fdfa4-141">Listę porty używane w środowisku usługi aplikacji, zapoznaj się [ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) sekcji porty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="fdfa4-142">Konfigurowanie Menedżera ruchu Microsoft Azure (OPCJONALNIE)</span><span class="sxs-lookup"><span data-stu-id="fdfa4-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="fdfa4-143">Jeśli aplikacja jest dostępna w wielu regionach, a następnie chcesz załadować saldo je za [usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fdfa4-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="fdfa4-144">Aby to zrobić, można dodać punktu końcowego w [klasycznego portalu Azure](https://manage.azure.com) przy użyciu nazwy usługi w chmurze dla Twojej zapory aplikacji sieci Web w profilu Menedżera ruchu, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Punkt końcowy Menedżera ruchu][TrafficManagerEndpoint]

<span data-ttu-id="fdfa4-146">Jeśli aplikacja wymaga uwierzytelniania, upewnij się, że jakiś zasób, który nie wymaga uwierzytelniania dla Menedżera ruchu sieciowego na polecenie ping dostępność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="fdfa4-147">Adres URL w sekcji konfiguracji można skonfigurować na [klasycznego portalu Azure](https://manage.azure.com) jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Konfigurowanie usługi Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="fdfa4-149">Do przekazywania pakietów Menedżera ruchu z Twojej zapory aplikacji sieci Web do aplikacji, należy konfiguracji witryny sieci Web tłumaczenia na Twojej Barracuda zapory aplikacji sieci Web do przesyłania ruchu do aplikacji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Tłumaczenie witryny sieci Web][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="fdfa4-151">Zabezpieczanie ruchu do środowiska usługi aplikacji przy użyciu grup zabezpieczeń sieci (NSG)</span><span class="sxs-lookup"><span data-stu-id="fdfa4-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="fdfa4-152">Postępuj zgodnie z [ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) szczegółowe informacje na temat ograniczania ruchu do środowiska usługi aplikacji z zapory aplikacji sieci Web tylko przy użyciu adresu VIP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="fdfa4-153">Oto przykład polecenia programu Powershell do wykonywania tego zadania TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="fdfa4-154">Zamień wirtualny adres IP (VIP) usługi w chmurze Twoje WAF SourceAddressPrefix.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="fdfa4-155">Uwaga: Adres VIP usługi w chmurze ulegnie zmianie po usunięcie i ponowne utworzenie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="fdfa4-156">Upewnij się zaktualizować adres IP w tej grupie zasobów sieciowych, wówczas.</span><span class="sxs-lookup"><span data-stu-id="fdfa4-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
