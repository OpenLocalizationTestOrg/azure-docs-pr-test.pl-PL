---
title: "środowiska usługi aplikacji tooAzure aaaIntroduction"
description: "Krótki przegląd środowiska usługi aplikacji Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Środowiska usługi tooApp wprowadzenie #
 
## <a name="overview"></a>Omówienie ##

Środowiska usługi aplikacji Azure to funkcja usługi Azure App Service, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować aplikacji usługi App Service na dużą skalę. Ta funkcja może obsługiwać Twoje [sieci web apps][webapps], [aplikacji mobilnych][mobileapps], [aplikacje interfejsu API][APIapps], i [funkcje][Functions].

Środowiska usługi aplikacji (ASEs) są odpowiednie dla obciążeń aplikacji, które wymagają:

- Bardzo dużej skali.
- Izolacja i bezpiecznego dostępu do sieci.
- Użycie pamięci wysokiej.

Klienci mogą tworzyć wiele ASEs w pojedynczym regionie Azure lub w wielu regionach platformy Azure. Tego rodzaju elastyczności sprawia, że ASEs nadaje się doskonale dla warstwy aplikacji bezstanowych, w związku z wysoką obciążeniami RPS skalowanie w poziomie.

ASEs są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej. Klienci mają precyzyjną kontrolę nad aplikacji dla ruchu przychodzącego i wychodzącego ruchu sieciowego. Aplikacje mogą nawiązywać bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci VPN.

Wszystkie artykuły i jak tooinstructions o ASEs są dostępne w hello [Plik README dla środowiska usługi aplikacji][ASEReadme]:

* ASEs włączyć hosting aplikacji wysokiej skali z bezpiecznego dostępu do sieci. Aby uzyskać więcej informacji, zobacz hello [nowości AzureCon](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) na ASEs.
* Wiele ASEs mogą być używane tooscale poziomo. Aby uzyskać więcej informacji, zobacz [jak tooset się wpływ aplikacja rozproszona geograficznie](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs może być używane tooconfigure Architektura zabezpieczeń, jak pokazano w hello AzureCon nowości. toosee, jak pokazano hello nowości AzureCon Architektura zabezpieczeń hello został skonfigurowany, zobacz hello [artykuł na temat tooimplement architektury zabezpieczeń warstwowych](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) ze środowiska usługi aplikacji.
* Aplikacje działające na ASEs może mieć ich dostęp uzyskiwany za nadrzędnego urządzeń, takich jak zapory aplikacji sieci web (WAFs). Aby uzyskać więcej informacji, zobacz [Konfigurowanie zapory aplikacji sieci Web dla środowiska usługi aplikacji](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Dedykowanym środowisku ##

Jest ASE dedykowane wyłącznie tooa jedną subskrypcją i może zawierać 100 wystąpień. zakres Hello mogą znajdować się na 100 wystąpień w jednym planów usługi App Service planu too100 jednego wystąpienia usługi aplikacji, a wszystko w pomiędzy.

ASE składa się z interfejsy i pracowników. Interfejsy są zobowiązani do zakończenia połączenia HTTP/HTTPS i automatyczne równoważenie obciążenia żądań aplikacji w elemencie ASE. Interfejsy są automatycznie dodawane jako hello planów usługi App Service w hello ASE jest skalowana w poziomie.

Pracownicy są role, które hostowanie aplikacji klienta. Pracownicy są dostępne w trzech rozmiarach stałe:

* Jeden rdzeń/3.5 GB pamięci RAM
* Dwa podstawowe/7 GB pamięci RAM
* Cztery podstawowe/14 GB pamięci RAM

Klienci nie muszą toomanage front kończy się i pracowników. Wszystkie infrastruktury jest automatycznie dodawane jako klienci skalowania planów usługi aplikacji. Usługi aplikacji planów są tworzone lub skalowany w elemencie ASE hello wymaga infrastruktury dodaniu lub usunięciu zależnie od potrzeb.

Brak płaskim miesięczne szybkości dla ASE, który pokrywa hello infrastruktury i nie zmienia się rozmiar hello hello ASE. Ponadto jest koszt core planu usługi aplikacji. Wszystkie aplikacje obsługiwane w elemencie ASE znajdują się w hello izolowane cennik jednostki SKU. Aby uzyskać informacje o cenach dla ASE, zobacz hello [cennik usługi aplikacji] [ Pricing] strony i przejrzyj dostępne opcje ASEs hello.

## <a name="virtual-network-support"></a>Obsługa sieci wirtualnej ##

ASE można tworzyć tylko w sieci wirtualnej platformy Azure Resource Manager. toolearn więcej informacji na temat sieci wirtualnych platformy Azure, zobacz hello [często zadawane pytania dotyczące sieci wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). ASE zawsze istnieje w sieci wirtualnej, a dokładnie w podsieci sieci wirtualnej. Można użyć funkcji zabezpieczeń hello toocontrol sieci wirtualne dla ruchu przychodzącego i wychodzącego sieci komunikacji dla aplikacji.

ASE może być skierowane do Internetu za pomocą publicznego adresu IP lub wewnętrzny uwzględniającym tylko adres (ILB) usługi równoważenia obciążenia wewnętrznego platformy Azure.

[Sieciowe grupy zabezpieczeń] [ NSGs] Ograniczanie ruchu przychodzącego komunikacji toohello podsieci, z którym znajduje się ASE. Można użyć grupy NSG toorun aplikacje za nadrzędnego urządzeń i usług, takich jak WAFs i dostawców SaaS sieci.

Aplikacje muszą również często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web. Jeśli wdrożono ASE hello w sieci wirtualnej z sieci lokalnej toohello połączenia sieci VPN, aplikacji hello w hello ASE dostęp do zasobów lokalnych hello. Ta funkcja ma wartość true, niezależnie od tego, czy hello VPN [lokacja lokacja](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) lub [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) sieci VPN.

Aby uzyskać więcej informacji na temat działania ASEs z sieciami wirtualnymi i sieciach lokalnych, zobacz [zagadnienia dotyczące sieci środowiska usługi aplikacji][ASENetwork].

## <a name="app-service-environment-v1"></a>Środowisko usługi App Service — wersja 1 ##

Środowiska usługi aplikacji ma dwie wersje: ASEv1 i ASEv2. Witaj poprzedzających informacji oparto na ASEv2. Ten przedstawia sekcji hello różnice między ASEv1 i ASEv2. 

W ASEv1, potrzebujesz toomanage wszystkie zasoby hello ręcznie. Zawierającej front kończy się hello, pracowników i adresy IP używane dla opartych na protokole SSL. Aby można skalować w poziomie planu usługi aplikacji, musisz toofirst skalowania puli procesów roboczych hello miejscu toohost go.

ASEv1 używa innego modelu cenowego z ASEv2. W ASEv1 płacisz za każdego rdzenia przydzielone. Zawierającej rdzeni interfejsy lub pracowników, którzy nie są hosting dowolnych zadań. W ASEv1 hello domyślny rozmiar maksymalny skali ASE jest 55 hosty łącznie. Zawierającej pracowników i interfejsy. Jeden tooASEv1 korzyści jest, czy może on zostać wdrożony w klasycznej sieci wirtualnej i sieci wirtualnych Menedżera zasobów. toolearn więcej informacji na temat ASEv1, zobacz [wprowadzenie v1 środowiska usługi aplikacji][ASEv1Intro].

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
