---
title: "często zadawane pytania dotyczące sieci wirtualnych aaaAzure | Dokumentacja firmy Microsoft"
description: "Najczęściej zadawane pytania dotyczące sieci wirtualne Microsoft Azure toohello odpowiedzi."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Sieć wirtualna platformy Azure — często zadawane pytania (FAQ)

## <a name="virtual-network-basics"></a>Podstawy sieci wirtualnej

### <a name="what-is-an-azure-virtual-network-vnet"></a>Co to jest sieci wirtualnej platformy Azure (VNet)?
Sieci wirtualnej platformy Azure (VNet) to reprezentacja sieci w chmurze hello. Jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej. Można użyć tooprovision sieci wirtualnych i zarządzać wirtualnych sieci prywatnych (VPN) w Azure i, opcjonalnie, hello łącze sieci wirtualnych z innych sieci wirtualnych na platformie Azure lub z lokalnej infrastruktury toocreate hybrydowy lub między różnymi lokalizacjami rozwiązaniami IT. Każdej sieci wirtualnej, którą utworzysz ma bloku CIDR i mogą być połączone tooother sieci wirtualnych i lokalnej sieci tak długo, jak bloków CIDR hello nie mogą się pokrywać. Masz również kontroli ustawienia serwera DNS dla sieci wirtualnych i segmentacji hello sieć wirtualną na podsieci.

Użyj sieci wirtualnych do:

* Utwórz dedykowane prywatnej tylko w chmurze sieci wirtualnej czasami konfiguracji między lokalizacjami nie jest wymagany do rozwiązania. Po utworzeniu sieci wirtualnej, usług i maszyn wirtualnych w ramach sieci wirtualnej mogą komunikować się bezpośrednio i bezpiecznie ze sobą w chmurze hello. Śledzi ruch bezpiecznie w obrębie hello sieci wirtualnej, ale nadal możliwe tooconfigure punktu końcowego połączenia hello maszyn wirtualnych i usług, które wymagają komunikacja z Internetem w ramach rozwiązania.
* Bezpiecznie rozszerzanie centrum danych z sieci wirtualnych, można tworzyć tradycyjnych skali toosecurely (S2S), sieci VPN lokacja lokacja wydajność centrum danych. S2S sieci VPN za pomocą protokołu IPSEC tooprovide bezpiecznego połączenia między bramą sieci VPN firmy i Azure.
* Włącz hybrydowe chmury scenariuszy sieci wirtualnych zapewnia hello toosupport elastyczność zakresu scenariuszy hybrydowych chmury. Można bezpiecznie łączyć z typu tooany aplikacji opartych na chmurze systemów Unix i lokalnego systemu, takich jak Komputery mainframe firmy.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Jak sprawdzić, czy potrzeba sieci wirtualnej?
Witaj [omówienie sieci wirtualnej](virtual-networks-overview.md) artykuł zawiera tabelę decyzji, która pomoże Ci zdecydować hello najlepsze sieci projektu dla siebie opcję.

### <a name="how-do-i-get-started"></a>Jak rozpocząć?
Odwiedź hello [dokumentacji sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/) tooget uruchomiona. Ta zawartość zawiera informacje o przegląd i wdrażania dla wszystkich funkcji VNet hello.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Sieci wirtualne można używać bez łączności między lokalizacjami?
Tak. Można użyć sieci wirtualnej bez korzystania z połączeń hybrydowych. Jest to szczególnie przydatne, jeśli chcesz, aby kontrolery domeny usługi Active Directory firmy Microsoft Windows Server toorun i farmy programu SharePoint na platformie Azure.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>Można przeprowadzić optymalizacji sieci WAN między sieciami wirtualnymi lub sieci wirtualnej i Moje lokalnego centrum danych?

Tak. Można wdrożyć [urządzenie wirtualne sieci WAN optymalizacji](https://azure.microsoft.com/marketplace/?term=wan+optimization) z kilku dostawców za pośrednictwem hello Azure Marketplace.

## <a name="configuration"></a>Konfiguracja

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Narzędzia należy używać toocreate sieci wirtualnej?
Możesz użyć hello następujące narzędzia toocreate lub konfigurowanie sieci wirtualnej:

* Portalu Azure (klasycznego i sieci wirtualne usługi Resource Manager).
* Plik konfiguracji sieci (netcfg - tylko klasyczne sieci wirtualne). Zobacz hello [skonfigurować sieć wirtualną przy użyciu pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md) artykułu.
* PowerShell (klasycznego i sieci wirtualne usługi Resource Manager).
* Azure CLI (klasycznego i sieci wirtualne usługi Resource Manager).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Jakie zakresów adresów można używać w mojej sieci wirtualnych?
Wszelkie zakres adresów IP zdefiniowanych w [RFC 1918](http://tools.ietf.org/html/rfc1918). Na przykład 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>Czy można mieć publicznych adresów IP w mojej sieci wirtualnych
Tak. Aby uzyskać więcej informacji na temat zakresy publicznych adresów IP, zobacz hello [przestrzeni adresowej publicznego adresu IP w sieci wirtualnej](virtual-networks-public-ip-within-vnet.md) artykułu. Publiczne adresy IP, nie będzie dostępny bezpośrednio z hello Internet.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Istnieje już Ogranicz liczbę toohello podsieci w mojej sieci wirtualnej?
Tak. Witaj odczytu [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu, aby uzyskać szczegółowe informacje. Przestrzeni adresowej podsieci nie może nakładać się wzajemnie.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Czy istnieją wszystkie ograniczenia dotyczące używania adresów IP w ramach tych podsieci?
Tak. Azure rezerwuje niektórych adresów IP w każdej podsieci. Witaj imię i nazwisko adresów IP podsieci hello są zastrzeżone dla protokołu zgodność, wraz z 3 więcej adresów używanych na potrzeby usług Azure.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Jak małe i jak duży może być sieci wirtualnych i podsieci?
Hello najmniejszą podsieci, które firma Microsoft obsługuje jest /29 i hello największy /8 (przy użyciu definicje podsieci CIDR).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Czy mogę przenieść mój tooAzure sieci VLAN, przy użyciu sieci wirtualnych
Nie. Sieci wirtualne są nakładki warstwy 3. Azure nie obsługuje żadnych semantyki warstwy 2.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Czy mogę określić niestandardowe zasady routingu w mojej sieci wirtualnych i podsieci
Tak. Możesz użyć użytkownika zdefiniowane routingu przez. Aby uzyskać więcej informacji na temat przez, odwiedź stronę [trasy zdefiniowane przez użytkownika i przesyłania dalej protokołu IP](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Sieci wirtualne obsługują multiemisji lub emisji?
Nie. Firma Microsoft nie obsługują multiemisji lub emisji.

### <a name="what-protocols-can-i-use-within-vnets"></a>Jakie protokoły można używać w ramach sieci wirtualnych?
Można używać protokołów TCP, UDP i ICMP TCP/IP w ramach sieci wirtualnych. Multiemisji, emisji hermetyzowany IP-in-IP pakiety i pakiety Generic Routing Encapsulation (GRE) są zablokowane w ramach sieci wirtualnych. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Czy można wywołać Moje domyślne routery w sieci wirtualnej?
Nie.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Można użyć polecenia tracert toodiagnose łączności?
Nie.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Po hello utworzenia sieci wirtualnej można dodać podsieci?
Tak. Podsieci można dodać tooVNets w dowolnym momencie tak długo, jak adres podsieci hello nie jest częścią innej podsieci w hello sieci wirtualnej.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>Rozmiar hello mojej podsieci można modyfikować po jej utworzeniu?
Tak. Można dodać, usunąć, rozszerzenia lub zmniejszyć rozmiar podsieci, jeśli nie ma żadnych maszyn wirtualnych wdrożonych w niej usługi.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Podsieci można zmodyfikować po ich utworzeniu?
Tak. Można dodać, usuwanie i modyfikowanie bloków CIDR hello używane przez sieci wirtualnej.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>Można połączyć toohello internet, czy Moje usług w sieci wirtualnej?
Tak. Wszystkie usługi wdrożyć w ramach sieci wirtualnej można połączyć toohello internet. Co usługa w chmurze wdrożona na platformie Azure ma przypisany tooit publicznie adresowanego adresu VIP. Konieczne będzie toodefine wejściowych punktów końcowych dla ról PaaS i punktów końcowych dla maszyn wirtualnych tooenable tych połączeń tooaccept usług z hello internet.

### <a name="do-vnets-support-ipv6"></a>Sieci wirtualne obsługują IPv6?
Nie. W tej chwili nie można używać protokołu IPv6 sieci wirtualnych.

### <a name="can-a-vnet-span-regions"></a>Sieci wirtualnej może obejmować regionów?
Nie. Sieci wirtualnej jest ograniczona tooa pojedynczym regionie.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>Można połączyć sieć wirtualną tooanother sieci wirtualnej na platformie Azure?
Tak. Możesz połączyć jednej sieci wirtualnej tooanother sieci wirtualnej przy użyciu:
- Brama sieci VPN platformy Azure. Witaj odczytu [skonfigurować połączenia do wirtualnymi](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artykułu, aby uzyskać szczegółowe informacje. 
- Komunikacja równorzędna sieci wirtualnej. Witaj odczytu [sieci wirtualnej komunikacji równorzędnej omówienie](virtual-network-peering-overview.md) artykułu, aby uzyskać szczegółowe informacje.

## <a name="name-resolution-dns"></a>Rozpoznawanie nazw (domen DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>Jakie są moje opcje DNS dla sieci wirtualnych?
Użyj tabeli decyzji hello na powitania [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](virtual-networks-name-resolution-for-vms-and-role-instances.md) dostępne opcje tooguide strony użytkownika przez wszystkie hello DNS.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>Dla sieci wirtualnej można określić serwerów DNS?
Tak. Można określić adresy IP serwerów DNS w ustawieniach sieci wirtualnej hello. To zostaną zastosowane jako serwerów DNS hello domyślnego dla wszystkich maszyn wirtualnych w hello sieci wirtualnej.

### <a name="how-many-dns-servers-can-i-specify"></a>Jak wiele serwerów DNS można określić?
Odwołanie hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu, aby uzyskać szczegółowe informacje.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>Moje serwery DNS można zmodyfikować po utworzono hello sieci?
Tak. Lista serwerów DNS hello sieci wirtualnej można zmienić w dowolnym momencie. Lista serwerów DNS w przypadku zmiany, konieczne będzie toorestart hello maszyn wirtualnych w sieci wirtualnej w kolejności ich toopick hello nowego serwera DNS.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Co to jest DNS platformy Azure i działa z sieci wirtualnych?
DNS platformy Azure to usługa DNS wielodostępne oferowanych przez firmę Microsoft. Azure rejestruje wszystkich maszyn wirtualnych i wystąpień roli usługi chmury w tej usłudze. Ta usługa udostępnia rozpoznawanie nazw przez hosta o nazwie dla maszyn wirtualnych i wystąpień roli zawartych w hello sama usługa w chmurze i przez nazwę FQDN dla maszyn wirtualnych i wystąpień roli w hello tej samej sieci wirtualnej. Witaj odczytu [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](virtual-networks-name-resolution-for-vms-and-role-instances.md) toolearn artykułu więcej informacji na temat DNS.

> [!NOTE]
> Istnieje ograniczenie w tym toohello czasu pierwszych 100 usługi w chmurze w sieci wirtualnej do rozpoznawania nazw między dzierżawcy przy użyciu DNS platformy Azure. Jeśli używasz serwera DNS, to ograniczenie nie ma zastosowania.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Można I zastąpienie ustawień DNS na — maszyny wirtualnej / service podstawy?
Tak. Serwery DNS można ustawiać na chmurze usługa podstawy toooverride hello domyślne ustawienia sieci. Jednak zaleca się, że używasz możliwie DNS sieci.

### <a name="can-i-bring-my-own-dns-suffix"></a>Czy mogę przenieść mój własny sufiks DNS
Nie. Nie można określić niestandardowego sufiksu DNS dla Twojej sieci wirtualnych.

## <a name="connecting-virtual-machines"></a>Łączenie maszyny wirtualne

### <a name="can-i-deploy-vms-tooa-vnet"></a>Można wdrożyć maszyn wirtualnych tooa sieci wirtualnej?
Tak. Wszystkie tooa interfejsów (NIC), podłączonych sieci maszyny Wirtualnej wdrożonej za pośrednictwem modelu wdrażania usługi Resource Manager hello musi być tooa połączonych sieci wirtualnej. Maszyn wirtualnych wdrożonych za pośrednictwem hello klasycznego modelu wdrażania można opcjonalnie tooa połączonych sieci wirtualnej.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Co to są typy hello adresów IP można przypisać tooVMs?
* **Prywatne:** przypisane tooeach kart interfejsu Sieciowego w ramach każdej maszyny Wirtualnej. adres Hello jest przypisany, przy użyciu metody statyczne lub dynamiczne albo hello. Prywatne adresy IP są przypisywane z zakresu hello, który określono w ustawieniach hello podsieci sieci wirtualnej. Wdrożone za pośrednictwem hello klasycznego modelu wdrażania są przypisane zasoby prywatnych adresów IP, nawet jeśli nie są one połączone tooa sieci wirtualnej. Prywatnego adresu IP przypisanego hello metody dynamicznej pozostaje przypisany zasobów tooa aż do usunięcia hello zasobów (maszyn wirtualnych lub usługi w chmurze miejsc wdrożenia). Prywatny adres IP przypisany za pomocą metody dynamicznej hello mogą ulec zmianie po ponownym uruchomieniu maszyny Wirtualnej po o w hello zatrzymane (cofnięciu przydziału) stanu. Prywatnego adresu IP przypisanego hello metody statycznej pozostaje przypisany tooa zasobów do momentu usunięcia hello zasobów. Jeśli potrzebujesz tooensure tego hello prywatnego adresu IP zasobu nigdy nie zmienia się do momentu usunięcia zasobu hello, przypisanie prywatnego adresu IP z metody statycznej hello.
* **Publicznego:** tooNICs opcjonalnie przypisanej dołączony tooVMs wdrożone za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello. przy użyciu metody statyczne lub dynamiczne alokacji hello można przypisać adres Hello. Wszystkie maszyny wirtualne i usługi w chmurze wystąpień roli wdrożone za pośrednictwem hello klasycznego modelu wdrażania istnieje w ramach usługi w chmurze, która jest przypisana *dynamiczne*, publiczny wirtualny adres IP (VIP). Publiczny *statycznych* adres IP, nazywany [zastrzeżony adres IP](virtual-networks-reserved-public-ip.md), opcjonalnie można przypisać jako adresu VIP. Można przypisać publicznego tooindividual adresy IP maszyn wirtualnych lub usługi w chmurze wystąpień roli wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Te adresy są nazywane [wystąpienie poziomu publicznego adresu IP (ILPIP](virtual-networks-instance-level-public-ip.md) adresów i może być przypisywany dynamicznie.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Dla maszyny Wirtualnej, który utworzy w późniejszym czasie można rezerwować prywatnego adresu IP?
Nie. Nie można zarezerwować prywatnego adresu IP. Jeśli dostępny jest prywatny adres IP zostanie do niej przypisany wystąpienie maszyny Wirtualnej lub roli tooa przez serwer DHCP hello. Czy maszyna wirtualna może lub nie mogą być hello ma hello prywatnego adresu IP address toobe przypisane do. Można jednak zmienić hello prywatnego adresu IP już utworzone tooany dostępne prywatny adres IP maszyny Wirtualnej.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Czy prywatnej zmiany adresów IP dla maszyn wirtualnych w sieci wirtualnej?
To zależy. Dynamiczne prywatnych adresów IP pozostają z maszyny Wirtualnej do jej zatrzymania (cofnięciu przydziału) lub usunięty. Prywatnych adresów IP nie są wydawane z maszyny Wirtualnej, dopóki zostanie usunięty.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>Można ręcznie przypisać z tooNICs adresów IP w ramach systemu operacyjnego maszyny Wirtualnej hello?
Tak, ale nie jest zalecane. Ręcznie zmiany hello adres IP dla karty Sieciowej w systemie operacyjnym maszyny Wirtualnej może potencjalnie pozwolić toolosing łączności toohello maszyny Wirtualnej, jeśli toochange zostały hello adresu IP przypisanego tooa kart interfejsu Sieciowego w ramach hello maszyny Wirtualnej platformy Azure.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Co się stanie toomy adresów IP, jeśli zatrzymać miejsce wdrożenia usługi w chmurze lub zamknięcie maszyny Wirtualnej z poziomu systemu operacyjnego hello?
Brak elementów. Hello adresów IP (VIP publiczne, publiczne i prywatne) pozostają miejsce wdrożenia usługi chmury przypisanej toohello lub maszyny Wirtualnej. Dynamiczne adresy są wydawane tylko, jeśli maszyna wirtualna zostanie zatrzymana (cofnięciu przydziału) lub usunięty, lub usunięciu miejsca wdrożenia usługi chmury. Kliknięcie przycisku hello **zatrzymać** przycisk dla maszyny Wirtualnej w portalu Azure hello ustawia jego tooStopped stanu (cofnięciu przydziału). W takim przypadku hello maszyny Wirtualnej spowoduje utratę swoje adresy IP.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>Można przenieść maszyny wirtualne z jednej podsieci tooanother podsieci w sieci wirtualnej bez ponownego wdrażania?
Tak. Więcej informacji można znaleźć w hello [jak toomove maszyny Wirtualnej lub roli wystąpienia tooa innej podsieci](virtual-networks-move-vm-role-to-subnet.md) artykułu.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>Moje maszyny wirtualnej można skonfigurować statyczny adres MAC?
Nie. Adres MAC nie można skonfigurować statycznie.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Pozostanie hello adres MAC hello takie same dla moich maszyny Wirtualnej po jej utworzeniu?
Tak, hello adres MAC pozostaje hello takie same dla maszyny Wirtualnej wdrożone za pośrednictwem hello Resource Manager i klasycznych modeli wdrażania, dopóki zostanie usunięty. Wcześniej hello adres MAC został wydany, jeśli hello maszyna wirtualna została zatrzymana (cofnięciu przydziału), ale teraz adres MAC hello jest zachowywana nawet wtedy, gdy hello maszyna wirtualna jest w hello alokację stanu.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>Można połączyć toohello internet z maszyny Wirtualnej w sieci wirtualnej?
Tak. Wszystkie maszyny wirtualne i usługi w chmurze wystąpień roli wdrożyć w ramach sieci wirtualnej mogą łączyć toohello Internet.

## <a name="azure-services-that-connect-toovnets"></a>Usług Azure, które łączą tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>Z sieci wirtualnej można używać aplikacji sieci Web usługi aplikacji Azure?
Tak. Można wdrażać aplikacje sieci Web w sieci wirtualnej przy użyciu ASE (środowiska usługi aplikacji). Wszystkie aplikacje sieci Web bezpiecznie łączyć i uzyskiwać dostęp do zasobów w sieci wirtualnej platformy Azure, jeśli połączenie punkt lokacja jest skonfigurowana dla sieci wirtualnej. Aby uzyskać więcej informacji zobacz następujące artykuły hello:

* [Tworzenie aplikacji sieci Web w środowisku usługi aplikacji](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Integracja aplikacji z sieci wirtualnej platformy Azure](../app-service-web/web-sites-integrate-with-vnet.md)
* [Przy użyciu integracji sieci wirtualnej i połączeń hybrydowych z aplikacji sieci Web](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Z sieci web i proces roboczy ról (PaaS) w sieci wirtualnej można wdrożyć usługi w chmurze?
Tak. Usługi w chmurze wystąpień roli w ramach sieci wirtualnych (opcjonalnie) można wdrożyć. toodo tak, określ hello nazwa sieci wirtualnej i mapowania roli/podsieci hello w sekcji konfiguracji sieci hello konfiguracji usługi. Nie trzeba tooupdate dowolne z plików binarnych.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>Można połączyć tooa ustawić skali maszyny wirtualnej (VMSS) sieci wirtualnej?
Tak. Należy połączyć tooa VMSS sieci wirtualnej.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Czy mogę przenieść mój usług i sieci wirtualnych
Nie. Nie można przenieść usług i sieci wirtualnych. Będą mieć toodelete i ponownie wdróż toomove usługi hello go tooanother sieci wirtualnej.

## <a name="security"></a>Bezpieczeństwo

### <a name="what-is-hello-security-model-for-vnets"></a>Co to jest model zabezpieczeń hello sieci wirtualnych?
Sieci wirtualne są całkowicie odizolowane od siebie i innych usług hostowanych w hello infrastruktury platformy Azure. Sieci wirtualnej jest granicą zaufania.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>Czy mogę ograniczyć zasoby podłączone tooVNet przepływu ruchu przychodzącego i wychodzącego
Tak. Możesz zastosować [grup zabezpieczeń sieci](virtual-networks-nsg.md) tooindividual podsieci w sieci wirtualnej, kart sieciowych dołączonych tooa sieci wirtualnej, lub obie.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>Czy można zaimplementować zapory między zasobami połączone sieci wirtualnej?
Tak. Można wdrożyć [urządzenie wirtualne zapory sieciowej](https://azure.microsoft.com/en-us/marketplace/?term=firewall) z kilku dostawców za pośrednictwem hello Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>Dostępne Zabezpieczanie sieci wirtualne są informacje?
Tak. Zobacz hello [Przegląd zabezpieczeń sieci Azure](../security/security-network-overview.md) artykułu, aby uzyskać szczegółowe informacje.

## <a name="apis-schemas-and-tools"></a>Interfejsy API, schematy i narzędzia

### <a name="can-i-manage-vnets-from-code"></a>Sieci wirtualne można zarządzać z kodu?
Tak. Można użyć interfejsów API REST dla sieci wirtualnych w hello [usługi Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) i [klasyczny (Zarządzanie usługą)](http://go.microsoft.com/fwlink/?LinkId=296833)) modele wdrażania.

### <a name="is-there-tooling-support-for-vnets"></a>Istnieje już obsługę narzędzi dla sieci wirtualnych?
Tak. Dowiedz się więcej o korzystaniu z:
- Witaj toodeploy portalu Azure sieci wirtualnych za pośrednictwem hello [usługi Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) i [klasycznego](virtual-networks-create-vnet-classic-pportal.md) modele wdrażania.
- Sieci wirtualne wdrożone za pośrednictwem hello toomanage PowerShell [Resource Manager](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) i [klasycznego](/powershell/module/azure/?view=azuresmps-3.7.0) modele wdrażania.
- Witaj [Azure interfejsu wiersza polecenia (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage sieci wirtualne wdrożone za pośrednictwem oba modele wdrażania.  
