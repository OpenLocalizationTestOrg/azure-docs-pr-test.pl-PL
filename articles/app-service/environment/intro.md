---
title: "Wprowadzenie do środowisk Azure App Service Environment"
description: "Krótkie omówienie środowisk Azure App Service Environment"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 06/13/2017
ms.author: ccompy
ms.custom: mvc
ms.openlocfilehash: 803a1cde5387b549504b42346d1a2e6a5df04746
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2017
---
# <a name="introduction-to-app-service-environments"></a>Wprowadzenie do środowisk App Service Environment #
 
## <a name="overview"></a>Omówienie ##

Azure App Service Environment to funkcja usługi Azure App Service udostępniająca w pełni izolowane, dedykowane środowisko do bezpiecznego uruchamiania aplikacji usługi App Service w dużej skali. Umożliwia ona hostowanie aplikacji internetowych, [aplikacji mobilnych][mobileapps], aplikacji interfejsu API oraz [funkcji][Functions].

Środowiska App Service Environment (ASE) są odpowiednie dla obciążeń aplikacji o następujących wymaganiach:

- Bardzo duża skala.
- Izolacja i bezpieczny dostęp do sieci.
- Wysoki poziom użycia pamięci.

Klienci mogą tworzyć wiele środowisk ASE w pojedynczym regionie platformy Azure lub w wielu regionach platformy Azure. Dzięki tej elastyczności środowiska ASE doskonale nadają się dla warstw aplikacji bezstanowych skalowanych w poziomie na potrzeby obsługi obciążeń o dużej liczbie żądań na sekundę (RPS).

Środowiska ASE są izolowane w celu uruchamiania aplikacji tylko jednego klienta i są zawsze wdrażane w sieci wirtualnej. Klienci mają precyzyjną kontrolę nad przychodzącym i wychodzącym ruchem sieciowym aplikacji. Aplikacje mogą nawiązywać bezpieczne szybkie połączenia za pośrednictwem sieci VPN z zasobami lokalnymi firmy.

* Środowiska ASE umożliwiają hosting aplikacji na dużą skalę z bezpiecznym dostępem do sieci. Aby uzyskać więcej informacji, zobacz film [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) poświęcony środowiskom ASE.
* Za pomocą wielu środowisk ASE można realizować skalowanie w poziomie. Aby uzyskać więcej informacji, dowiedz się, [jak skonfigurować rozproszony geograficznie zasięg aplikacji](app-service-app-service-environment-geo-distributed-scale.md).
* Za pomocą środowisk ASE można skonfigurować architekturę zabezpieczeń, jak zaprezentowano w tym filmie AzureCon Deep Dive. Aby dowiedzieć się, jak skonfigurowano architekturę zabezpieczeń przedstawioną w tym filmie AzureCon Deep Dive, zobacz [artykuł na temat implementowania warstwowej architektury zabezpieczeń](app-service-app-service-environment-layered-security.md) za pomocą środowisk App Service Environment.
* Dostęp aplikacji działających w środowiskach ASE może być kontrolowany za pomocą bram na urządzeniach nadrzędnych, takich jak zapory aplikacji internetowych (WAF). Aby uzyskać więcej informacji, zobacz [Configure a WAF for App Service environments](app-service-app-service-environment-web-application-firewall.md) (Konfigurowanie zapory aplikacji internetowych dla środowiska App Service Environment).

## <a name="dedicated-environment"></a>Dedykowane środowisko ##

Środowisko ASE jest przeznaczone wyłącznie dla jednej subskrypcji i może hostować do 100 wystąpień. Zakres może obejmować 100 wystąpień w jednym planie usługi App Service lub 100 planów usługi App Service z jednym wystąpieniem każdy — możliwe są też wszelkie konfiguracje pośrednie.

Środowisko ASE składa się z frontonów i procesów roboczych. Frontony są odpowiedzialne za zakończenia połączeń HTTP/HTTPS i automatyczne równoważenie obciążenia żądań aplikacji w środowisku ASE. Frontony są automatycznie dodawane w przypadku skalowania w poziomie planów usługi App Service w środowisku ASE.

Procesy robocze to role, które hostują aplikacje klienta. Procesy robocze są dostępne w trzech stałych rozmiarach:

* Jeden procesor vCPU/3,5 GB pamięci RAM
* Dwa procesory vCPU/7 GB pamięci RAM
* Cztery procesory vCPU/14 GB pamięci RAM

Klienci nie muszą zarządzać frontonami ani procesami roboczymi. Wszystkie elementy infrastruktury są automatycznie dodawane, gdy klienci skalują plany usługi App Service. Gdy w środowisku ASE są tworzone lub skalowane plany usługi App Service, wymagane elementy infrastruktury są odpowiednio dodawane lub usuwane.

Obowiązuje zryczałtowana stawka miesięczna za środowisko ASE, która pokrywa koszty infrastruktury i nie zmienia się z rozmiarem tego środowiska. Ponadto obowiązują opłaty za procesory vCPU planów usługi App Service. Wszystkie aplikacje hostowane w środowisku ASE znajdują się w jednostce SKU wyceny „izolowanej” (Isolated). Aby uzyskać informacje o cenach dotyczących środowiska ASE, przejdź na stronę [App Service — cennik][Pricing] i zapoznaj się z dostępnymi opcjami środowisk ASE.

## <a name="virtual-network-support"></a>Obsługa sieci wirtualnej ##

Środowisko ASE można utworzyć tylko w sieci wirtualnej usługi Azure Resource Manager. Aby dowiedzieć się więcej o sieciach wirtualnych platformy Azure, zobacz [często zadawane pytania na ich temat](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Środowisko ASE zawsze istnieje w sieci wirtualnej, a dokładniej — w podsieci sieci wirtualnej. Za pomocą funkcji zabezpieczeń sieci wirtualnych można sterować przychodzącą i wychodzącą komunikacją sieciową używanych aplikacji.

Środowisko ASE może być środowiskiem połączonym z Internetem za pomocą publicznego adresu IP lub wewnętrznym i mającym tylko adres wewnętrznego modułu równoważenia obciążenia (ILB, Internal Load Balancer) platformy Azure.

[Sieciowe grupy zabezpieczeń][NSGs] ograniczają komunikację sieciową przychodzącą do podsieci, w której znajduje się środowisko ASE. Za pomocą tych grup można uruchamiać aplikacje za urządzeniami i usługami nadrzędnymi, takimi jak zapora aplikacji internetowych i sieciowi dostawcy SaaS.

Aplikacje często muszą również uzyskiwać dostęp do zasobów firmy, takich jak wewnętrzne bazy danych i usługi internetowe. Jeśli środowisko ASE wdrożono w sieci wirtualnej mającej połączenie VPN z siecią lokalną, aplikacje w tym środowisku mają dostęp do zasobów lokalnych. Jest tak niezależnie od tego, czy połączenie VPN jest typu [lokacja-lokacja](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/), czy [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/).

Aby uzyskać więcej informacji na temat współdziałania środowisk ASE z sieciami wirtualnymi i sieciami lokalnymi, zobacz [App Service Environment network considerations][ASENetwork] (Zagadnienia dotyczące sieci środowiska App Service Environment).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud/player]

## <a name="app-service-environment-v1"></a>Środowisko usługi App Service — wersja 1 ##

Środowisko App Service Environment występuje w dwóch wersjach: ASEv1 i ASEv2. Podane wcześniej informacje dotyczyły wersji 2 — ASEv2. W tej sekcji przedstawiono różnice między środowiskami ASEv1 i ASEv2. 

W środowisku ASEv1 wszystkimi zasobami trzeba zarządzać ręcznie. Obejmuje to frontony, procesy robocze oraz adresy IP używane do obsługi połączeń SSL opartych na protokole IP. Zanim będzie można skalować w poziomie plan usługi App Service, należy najpierw skalować w poziomie pulę procesów roboczych, w której będzie hostowany.

W przypadku środowiska ASEv1 używany jest inny model cenowy niż w przypadku środowiska ASEv2. W przypadku środowiska ASEv1 płacisz za każdy przydzielony procesor vCPU. Obejmuje to procesory vCPU obsługujące frontony i procesy robocze, które nie hostują żadnych obciążeń. W przypadku środowiska ASEv1 domyślny rozmiar w skali maksymalnej środowiska ASE to 55 hostów łącznie. Obejmuje to frontony i procesy robocze. Jedną z zalet środowiska ASEv1 jest to, że można je wdrożyć w klasycznej sieci wirtualnej oraz w sieci wirtualnej usługi Resource Manager. Aby dowiedzieć się więcej na temat środowiska ASEv1, zobacz [App Service Environment v1 introduction][ASEv1Intro] (Wprowadzenie do środowiska App Service Environment w wersji 1).

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
