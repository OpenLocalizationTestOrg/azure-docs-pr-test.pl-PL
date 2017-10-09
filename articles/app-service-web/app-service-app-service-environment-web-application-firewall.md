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
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji
## <a name="overview"></a>Omówienie
Sieci Web zapór aplikacji, takich jak hello [Barracuda zapory aplikacji sieci Web dla platformy Azure](https://www.barracuda.com/programs/azure) dostępnych na powitania [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ułatwia zabezpieczenie aplikacji sieci web, sprawdzając tooblock ruch przychodzący sieci web SQL iniekcji, skryptów krzyżowych, przekazywanie złośliwego oprogramowania i aplikacji przed atakami DDoS i inne ataki. Sprawdza również hello odpowiedzi z serwerów sieci web zaplecza powitania dla zapobiegania utracie danych (DLP). W połączeniu z hello izolacji i dodatkowe skalowanie podał środowiska usługi App Service, zapewnia to idealne rozwiązanie w środowisku toohost biznesowe krytyczne aplikacje sieci web muszą toowithstand złośliwymi żądaniami i dużych obciążeń ruchem.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Konfiguracja
Dla tego dokumentu, który będzie skonfigurowanie naszych środowiska usługi aplikacji za wiele obciążenia zrównoważonym wystąpień Barracuda zapory aplikacji sieci Web tak, aby tylko na ruch z hello zapory aplikacji sieci Web można osiągnąć hello środowiska usługi aplikacji i nie będzie dostępny z hello DMZ. Firma Microsoft będzie miał usługi Azure Traffic Manager przed naszych saldo tooload wystąpień Barracuda zapory aplikacji sieci Web w centrach danych platformy Azure i regionów. Diagramu wysokiego poziomu hello instalacji będzie wyglądała co przedstawiono poniżej.

![Architektura][Architecture] 

> Uwaga: Z wprowadzeniem hello [ILB obsługę środowiska usługi aplikacji](app-service-environment-with-internal-load-balancer.md), można skonfigurować toobe hello ASE niedostępne z hello DMZ i być dostępne toohello sieci prywatnej. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Konfigurowanie środowiska usługi aplikacji
tooconfigure środowiska usługi aplikacji można znaleźć zbyt[naszej dokumentacji](app-service-web-how-to-create-an-app-service-environment.md) na powitania podmiotu. Po utworzeniu środowiska usługi aplikacji utworzony, można utworzyć [aplikacje sieci Web](app-service-web-overview.md), [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md) i [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) w tym środowisku, które będą wszystkie chronione za hello zapory aplikacji sieci Web firma Microsoft Skonfiguruj w następnej sekcji hello.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Konfigurowanie usługi w chmurze zapory aplikacji sieci Web Barracuda
Ma barracuda [szczegółowe artykułu](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) na temat wdrażania jego zapory aplikacji sieci Web na maszynie wirtualnej na platformie Azure. Jednak ponieważ firma Microsoft ma nadmiarowości i nie wprowadzenie pojedynczego punktu awarii, ma co najmniej 2 toodeploy zapory aplikacji sieci Web wystąpienia maszyn wirtualnych na powitania tej samej usługi chmury, gdy następujące instrukcje.

### <a name="adding-endpoints-toocloud-service"></a>Dodawanie tooCloud punktów końcowych usługi
Gdy masz 2 lub wirtualna zapory aplikacji sieci Web więcej wystąpień w usłudze w chmurze można użyć hello [portalu Azure](https://portal.azure.com/) tooadd HTTP i HTTPS punkty końcowe, które są używane przez aplikację, jak pokazano w poniższym obrazie hello.

![Konfigurowanie punktu końcowego][ConfigureEndpoint]

Aplikacje korzystanie z innych punktów końcowych, aby tooadd się, że te listy toothis również. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Konfigurowanie Barracuda zapory aplikacji sieci Web za pomocą portalu zarządzania
Barracuda zapory aplikacji sieci Web używa TCP Port 8000 dla konfiguracji za pomocą portalu zarządzania. Ponieważ istnieje wiele wystąpień maszyn wirtualnych zapory aplikacji sieci Web hello należy toorepeat hello tutaj kroki dla każdego wystąpienia maszyny Wirtualnej. 

> Uwaga: Po wykonaniu konfiguracji zapory aplikacji sieci Web, Usuń punkt końcowy protokołu TCP/8000 hello z tookeep maszyny wirtualne zapory aplikacji sieci Web z zapory aplikacji sieci Web bezpieczne.
> 
> 

Dodaj punkt końcowy zarządzania hello jak pokazano w obrazie hello poniżej tooconfigure Twojego Barracuda zapory aplikacji sieci Web.

![Dodaj punkt końcowy zarządzania][AddManagementEndpoint]

Punkt końcowy zarządzania toohello toobrowse przeglądarki w systemie usługi w chmurze. Usługi w chmurze jest nazywany test.cloudapp.net, czy dostęp do tego punktu końcowego przechodząc toohttp://test.cloudapp.net:8000. Powinna zostać wyświetlona strona logowania, takich jak poniżej że możesz zalogować się przy użyciu poświadczeń określonych w fazie instalacji maszyny Wirtualnej hello zapory aplikacji sieci Web.

![Zarządzanie strony logowania][ManagementLoginPage]

Raz logowania jako hello powinien zostać wyświetlony pulpit nawigacyjny w hello obraz poniżej przedstawia podstawowe dane statystyczne dotyczące hello ochrony zapory aplikacji sieci Web.

![Pulpit nawigacyjny zarządzania][ManagementDashboard]

Kliknięcie karty usługi hello umożliwi Ci w skonfigurowaniu Twojej zapory aplikacji sieci Web dla usług, które ochrony. Aby uzyskać więcej informacji na temat konfigurowania sieci Barracuda zapory aplikacji sieci Web można znaleźć [dokumentacji](https://techlib.barracuda.com/waf/getstarted1). W przykładzie hello poniżej aplikacji sieci Web platformy Azure obsługujące ruch HTTP i HTTPS została skonfigurowana.

![Dodaj zarządzania usługi][ManagementAddServices]

> Uwaga: W zależności od sposobu konfiguracji aplikacji i jakie funkcje są używane w środowisku usługi aplikacji, będzie potrzebny tooforward ruch TCP porty inne niż 80 i 443, np. Jeśli masz ustawienia protokołu SSL z adresu IP dla aplikacji sieci Web. Lista portów sieci używanych w środowisku usługi aplikacji można znaleźć za[ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) sekcji porty sieciowe.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Konfigurowanie Menedżera ruchu Microsoft Azure (OPCJONALNIE)
Jeśli aplikacja jest dostępna w wielu regionach, a następnie konieczne będzie saldo tooload ich za [usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo, dzięki czemu można dodać punktu końcowego w hello [klasycznego portalu Azure](https://manage.azure.com) za pomocą nazwy usługi w chmurze hello z zapory aplikacji sieci Web w w profilu usługi Traffic Manager hello, jak pokazano w poniższym obrazie hello. 

![Punkt końcowy Menedżera ruchu][TrafficManagerEndpoint]

Jeśli aplikacja wymaga uwierzytelniania, upewnij się, że jakiś zasób, który nie wymaga uwierzytelniania dla Menedżera ruchu tooping hello dostępność aplikacji. Adres URL hello pod hello sekcji konfiguracji można skonfigurować na powitania [klasycznego portalu Azure](https://manage.azure.com) jak pokazano poniżej.

![Konfigurowanie usługi Traffic Manager][ConfigureTrafficManager]

tooforward hello polecenia ping Menedżera ruchu z aplikacji tooyour zapory aplikacji sieci Web, należy tłumaczeń toosetup witryny sieci Web na Barracuda WAF tooforward ruchu tooyour aplikacji jak pokazano w poniższym przykładzie hello.

![Tłumaczenie witryny sieci Web][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Zabezpieczanie tooApp ruchu usługi środowisko przy użyciu sieci zabezpieczeń grupy (NSG)
Wykonaj hello [ruch przychodzący kontroli dokumentacji](app-service-app-service-environment-control-inbound-traffic.md) dla szczegóły dotyczące ograniczania ruchu tooyour środowiska usługi aplikacji z hello zapory aplikacji sieci Web tylko przy użyciu adresu hello VIP usługi w chmurze. Oto przykład polecenia programu Powershell do wykonywania tego zadania TCP port 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Zastąp hello SourceAddressPrefix hello wirtualny adres IP (VIP) usługi w chmurze Twoje WAF.

> Uwaga: hello VIP usługi w chmurze ulegnie zmianie po usunięcie i ponowne utworzenie hello usługi w chmurze. Upewnij się, że tooupdate hello adresu IP w grupie zasobów sieciowych powitania po przeprowadzeniu rejestracji. 
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
