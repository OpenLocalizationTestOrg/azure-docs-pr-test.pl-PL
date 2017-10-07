---
title: "aaaGetting wprowadzenie do zabezpieczeń Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie funkcji zabezpieczeń Microsoft Azure oraz Ogólne zagadnienia dotyczące organizacji, które jest przeprowadzana migracja dostawcy chmury tooa zasoby."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Wprowadzenie do zabezpieczeń platformy Microsoft Azure
Podczas tworzenia lub migracji dostawcy chmury tooa zasoby IT są zależne tooprotect możliwości organizacji w aplikacji i danych za pomocą usługi hello i formanty hello zapewniają bezpieczeństwo hello toomanage zasobów opartych na chmurze.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą ich potrzeb zabezpieczeń. Ponadto Azure zapewnia szereg zabezpieczeń można skonfigurować opcje i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożeń.

Ten poglądowy artykuł dotyczący zabezpieczeń platformy Azure koncentruje się na następujących zagadnieniach:

* Azure usługi i funkcje, można użyć toohelp zabezpieczanie usług i danych w systemie Azure.
* W jaki sposób firma Microsoft zabezpiecza hello toohelp infrastruktury platformy Azure chronić Twoje dane i aplikacje.

## <a name="identity-and-access-management"></a>Zarządzanie tożsamościami i dostępem
Bardzo ważne jest kontrolowanie dostępu tooIT infrastruktury, danych i aplikacji. Microsoft Azure zapewnia te możliwości przez usługi Azure Active Directory (Azure AD), usługi Azure Storage i pomocy technicznej dla wielu standardów i interfejsów API.

[Usługi Azure AD](../active-directory/active-directory-whatis.md) jest aparatem, który udostępnia uwierzytelniania, autoryzacji i kontroli dostępu dla użytkowników w organizacji, grup i obiekty i repozytorium tożsamości. Usługi Azure AD jest również oferuje deweloperom efektywny sposób toointegrate identity management w swoich aplikacjach. Standardowych protokołów, takich jak [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx), i [OpenID Connect](http://openid.net/connect/) odpowiednie możliwości logowania na platformach, takich jak .NET, Java, Node.js i PHP.

Witaj interfejsu API programu Graph opartego na interfejsie REST umożliwia deweloperom tooread i zapisywania katalogu toohello z dowolnej platformie. Dzięki obsłudze [OAuth 2.0](http://oauth.net/2/), deweloperzy mogą tworzyć przenośnych i aplikacji sieci web, które integrują się z firmy Microsoft i innych firm interfejsów API sieci web oraz tworzenie własnych bezpiecznego interfejsów API w sieci web. Biblioteki klienckie typu „open source” są dostępne dla platformy .Net, Sklepu Windows oraz systemów iOS i Android. Ponadto trwają prace nad dodatkowymi bibliotekami.

### <a name="how-azure-enables-identity-and-access-management"></a>W jaki sposób platforma Azure umożliwia zarządzanie tożsamościami i dostępem
Usługa Azure AD może służyć jako autonomiczny katalog chmury dla organizacji lub jako rozwiązanie zintegrowane z istniejącą lokalną usługą Active Directory. Funkcje integracji obejmują synchronizację katalogów i logowanie jednokrotne (SSO). Te rozszerzają zasięg hello istniejącej tożsamości lokalnych do chmury hello i udoskonalanie hello administratora i użytkownika.

Dostępne są również następujące funkcje zarządzania tożsamościami i dostępem:

* Azure AD umożliwia [logowania jednokrotnego](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS aplikacji, niezależnie od tego, gdzie są obsługiwane. Niektóre aplikacje są sfederowane z usługą Azure AD, a inne korzystają z logowania jednokrotnego z użyciem hasła. Aplikacje federacyjne mogą także obsługiwać inicjowanie obsługi administracyjnej użytkowników i przechowywanie haseł.
* Toodata dostępu w [usługi Azure Storage](https://azure.microsoft.com/services/storage/) jest kontrolowany przez uwierzytelniania. Każde konto magazynu ma klucza podstawowego ([klucz konta magazynu](https://msdn.microsoft.com/library/azure/ee460785.aspx), lub SAK) i klucz tajny pomocniczy (sygnatury dostępu współdzielonego hello lub SAS).
* Usługa Azure AD zapewnia jako usługi przy użyciu federacji tożsamości za pomocą [Active Directory Federation Services](../active-directory/fundamentals-identity.md), synchronizacji i replikacji z lokalnymi katalogami.
* [Usługa Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) jest hello usługi Multi-Factor authentication, który wymaga logowania tooverify użytkowników przy użyciu aplikacji mobilnej, połączenia telefonicznego lub wiadomości SMS. Można go przy użyciu usługi Azure AD toohelp bezpieczną lokalną zasobów z serwera usługi Azure Multi-Factor Authentication hello, a także z niestandardowych aplikacji i katalogów przy użyciu hello zestawu SDK.
* [Usługi domenowe Azure AD](https://azure.microsoft.com/services/active-directory-ds/) umożliwia dołączenie bez wdrażania kontrolerów domeny w domenie tooa maszyn wirtualnych platformy Azure. Można zalogować toothese maszyn wirtualnych za pomocą firmowych poświadczeń usługi Active Directory i administrować przyłączonych do domeny maszyn wirtualnych przy użyciu plany bazowe zabezpieczeń tooenforce zasad grupy na wszystkich maszyn wirtualnych platformy Azure.
* [Usługa Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) zapewnia usługę wysokiej dostępności zarządzania globalne tożsamości dla aplikacji dla użytkowników, która może obsłużyć toohundreds milionów tożsamości. Można ją łatwo integrować z platformami mobilnymi i platformami sieci Web. Użytkownicy mogą rejestrować w tooall aplikacji za pomocą środowiska można dostosować przy użyciu istniejących kont społecznościowych lub tworząc nowe poświadczenia.

## <a name="data-access-control-and-encryption"></a>Kontrola dostępu do danych i szyfrowanie
Firma Microsoft wprowadza zasady hello rozdzielenie obowiązków i [najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) w całym operacje platformy Azure. Toodata dostępu przez personel pomocy technicznej platformy Azure wymaga Twojej zgody jawnej i jest przyznawane na podstawie "just-in-time", która jest rejestrowana i sprawdzona, następnie odwołane po zakończeniu hello zaangażowania.

Platforma Azure udostępnia również wiele możliwości ochrony przesyłanych i przechowywanych danych. Dotyczy to również szyfrowania danych, plików, aplikacji, usług, komunikację i dysków. Szyfrowanie informacji przed wprowadzeniem go na platformie Azure i przechowywać kluczy w centrach danych z lokalnego.

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Technologie szyfrowania na platformie Azure
Szczegółowe informacje o środowisku subskrypcji tooyour dostępu administracyjnego można zebrać za pomocą [raportów usługi Azure AD](../active-directory/active-directory-reporting-audit-events.md). Można skonfigurować [szyfrowania dysków funkcją BitLocker](https://technet.microsoft.com/library/cc732774.aspx) na wirtualne dyski twarde zawierające informacje poufne na platformie Azure.

Inne funkcje na platformie Azure, która pomoże tookeep, którego bezpieczeństwo danych obejmują:

* Deweloperzy aplikacji mogą tworzyć szyfrowania do aplikacji hello ich wdrażanie na platformie Azure przy użyciu systemu Windows hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) i .NET Framework.
* Całkowicie kontrolować hello klucze szyfrowania po stronie klienta dla magazynu obiektów Blob platformy Azure. Usługa Magazyn Hello nigdy nie widzi hello kluczy i jest zdolny do odszyfrowywania danych hello.
* [Usługa Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (z hello [zestawu RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) zawiera plik i szyfrowania i wycieku danych zapobiegania poziom danych za pośrednictwem zarządzania na podstawie zasad dostępu.
* Azure obsługuje [szyfrowania na poziomie kolumny i na poziomie tabeli (funkcji TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) w maszyn wirtualnych programu SQL Server który obsługuje innych firm lokalnych serwerów zarządzania kluczami w centrach danych.
* Klucze konta magazynu, sygnatur dostępu współdzielonego, certyfikaty zarządzania i innych kluczy są unikatowe tooeach dzierżawą platformy Azure.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) hybrydowym magazynie szyfruje dane za pomocą 128-bitowego pary kluczy publiczny/prywatny przed przekazaniem go tooAzure magazynu.
* Azure obsługuje i używa wielu mechanizmów szyfrowania, w tym SSL/TLS, IPsec i AES, w zależności od typów danych hello, kontenery i transportów.

## <a name="virtualization"></a>Wirtualizacja
Witaj platformy Azure używa środowisku wirtualnym. Wystąpienia użytkownika działać jako autonomiczne maszyny wirtualne, które nie mają dostępu tooa serwera fizycznego hosta i Izolacja jest wymuszana za pomocą fizycznych [poziomy uprawnień procesora (pierścień-0/pierścień-3)](https://en.wikipedia.org/wiki/Protection_ring).

Pierścień 0 jest hello najbardziej uprzywilejowanych i 3 jest najmniej hello. system operacyjny gościa Hello działa w 1 pierścień mniejszym uprzywilejowanego, i aplikacje są uruchamiane w hello najniższych uprawnieniach 3 pierścień. Ta wirtualizacji zasoby fizyczne prowadzi tooa wyraźnej separacji między funkcji hypervisor, co spowoduje rozdzielenie dodatkowe zabezpieczenia hello dwa i system operacyjny gościa.

Hello Azure funkcji hypervisor działa jak jądra i przekazuje wszystkie żądania dostępu do sprzętu z hosta toohello maszyn wirtualnych gościa dla przetwarzania przy użyciu interfejsu pamięci współużytkowanej, nazywany magistralę maszyny wirtualnej. Uniemożliwia użytkownikom uzyskiwanie dostępu odczytu/zapisu/wykonania surowego toohello systemu i zmniejsza ryzyko hello udostępnianie zasobów systemowych.

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Implementowanie wirtualizacji na platformie Azure
Platforma Azure korzysta zaporą funkcji hypervisor (filtr pakietów), która jest zaimplementowana w funkcji hypervisor hello i skonfigurowany przez agenta kontrolera sieci szkieletowej. Pozwala to chronić dzierżawców przed nieautoryzowanym dostępem. Domyślnie cały ruch jest zablokowany, po utworzeniu maszyny wirtualnej, a następnie agent kontrolera sieci szkieletowej hello konfiguruje tooadd filtru pakietów hello *regułami i wyjątkami* tooallow autoryzowany ruchu.

Istnieją dwie kategorie reguł, które są w tym miejscu programowane:

* **Reguły konfiguracji lub infrastruktury maszyny**: Domyślnie cała komunikacja jest zablokowany. Są wyjątki tooallow toosend maszyny wirtualnej i odbierać dane DHCP i DNS. Maszyny wirtualne można również wysyłać ruch toohello "public" internet i wysyłania ruchu tooother maszyn wirtualnych w ramach klastra hello i Serwer aktywacji hello systemu operacyjnego. maszyny wirtualne Hello listy dozwolonych wychodzących miejsc docelowych nie ma podsieci Azure routera, zarządzania platformy Azure, Utwórz kopię zakończenia i inne właściwości firmy Microsoft.
* **Plik konfiguracji roli**: definiuje hello przychodzących dostępu kontroli zawiera listę (kontroli dostępu ACL) oparte na modelu usługi hello dzierżawy. Na przykład, jeśli dzierżawcy frontonu sieci Web na porcie 80 na maszynie wirtualnej, następnie Azure otwiera TCP port 80 tooall adresów IP w przypadku konfigurowania punktu końcowego w hello [Azure klasycznego modelu wdrażania](../azure-resource-manager/resource-manager-deployment-model.md). Jeśli hello maszyny wirtualnej ma wstecz roli zakończenia lub procesu roboczego uruchomiona, spowoduje to otwarcie hello procesu roboczego roli tylko toohello maszyny wirtualnej w ramach hello sam dzierżawy.

## <a name="isolation"></a>Izolacja
Wymaganie dotyczące zabezpieczeń innej chmurze ważne jest tooprevent separacji nieautoryzowanych i niezamierzone przesyłanie informacji między wdrożeń w udostępnionym przypadku architektury wielodostępnej.

Implementuje Azure [kontroli dostępu do sieci](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) i podział poprzez izolowanie od sieci VLAN, listy ACL, obciążenia równoważenia i filtry IP. Ogranicza ona zakres zewnętrznego ruchu przychodzącego tooports i protokoły na maszynach wirtualnych w zdefiniowanych przez użytkownika. Implementuje Azure filtrowania tooprevent sfałszowane ruch sieciowy i ograniczanie składniki platformy tootrusted ruchu przychodzącego i wychodzącego. Zasady przepływu ruchu są implementowane na urządzeniach ochrony brzegowej, które domyślnie nie zezwalają na ruch.

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Translatora adresów sieciowych (NAT) jest używany tooseparate ruchu w sieci wewnętrznej od zewnętrznego ruchu. Ruch wewnętrzny nie podlega routingowi zewnętrznemu. [Wirtualne adresy IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx), które podlegają routingowi zewnętrznemu, są przekształcane na [wewnętrzne dynamiczne adresy IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx), które podlegają routingowi tylko w obrębie platformy Azure.

Maszyny wirtualne tooAzure zewnętrznego ruchu jest zaporą za pomocą listy kontroli dostępu na routerach, usługi równoważenia obciążenia i przełączniki warstwy 3. Dozwolone są tylko określone znane protokoły. Listy ACL są w miejscu toolimit ruchu pochodzącego z maszyn wirtualnych gościa tooother sieci VLAN, używany do zarządzania. Ponadto ruch filtrowane za pomocą filtrów IP hello systemu operacyjnego hosta dalsze limity hello ruchu w obu warstwach łącza i sieci danych.

### <a name="how-azure-implements-isolation"></a>Implementowanie izolacji na platformie Azure
Hello Kontroler sieci szkieletowej Azure jest odpowiedzialny za przydzielanie zasobów infrastruktury tootenant obciążeń i zarządza jednokierunkowe komunikacji z hello hosta toovirtual maszyn. Hello Azure funkcji hypervisor wymusza pamięci i oddzielenie procesu maszyny wirtualnej, a bezpiecznie kieruje dzierżaw tooguest OS ruchu sieciowego. Azure implementuje również izolacji dzierżawców, magazynu i sieci wirtualnych.

* Każda dzierżawa usługi Azure AD jest logicznie samodzielnie przy użyciu granic zabezpieczeń.
* Konta magazynu Azure są unikatowe tooeach subskrypcji, i musi zostać uwierzytelniony dostęp przy użyciu klucza konta magazynu.
* Sieci wirtualne są logicznie odizolowane przy użyciu kombinacji unikatowy prywatnych adresów IP, zapory i listy ACL adresu IP. Moduły równoważenia obciążenia trasy dzierżaw odpowiednie toohello ruchu na podstawie definicji punktu końcowego.

## <a name="virtual-networks-and-firewalls"></a>Sieci wirtualne i zapór
Witaj [rozproszone i wirtualnych sieciach](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) w Pomocy usługi Azure upewnij się, że ruchu sieci prywatnej jest logicznie odizolowane od ruchu na innych sieci wirtualnych platformy Azure.

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Subskrypcji może zawierać wiele izolowane sieci prywatnych (i obejmują zapory, równoważenia obciążenia i translatora adresów sieciowych).

Platforma Azure udostępnia trzy poziomy podstawowej sieci podziału w każdym Azure klastra toologically segregate ruchu. [Wirtualne sieci lokalne](https://azure.microsoft.com/services/virtual-network/) (VLAN) są używane tooseparate ruchu klientów z resztą hello hello sieć platformy Azure. Toohello dostępu do sieci platformy Azure z poza klastra hello jest ograniczony przy użyciu usługi równoważenia obciążenia.

Tooand ruchu sieciowego z maszyny wirtualnej musi przejść przez przełącznik wirtualny hello funkcji hypervisor. składnik filtru IP Hello w katalogu głównym hello systemu operacyjnego izoluje hello głównego maszyny wirtualnej na podstawie maszyn wirtualnych gościa hello i maszyn wirtualnych gościa powitania od siebie nawzajem. Wykonuje, filtrowania ruchu toorestrict komunikacji między węzłami dzierżawcy i hello publicznej sieci Internet (na podstawie powitania klienta usługi konfiguracji), ich oddzielenie od pozostałych dzierżawców.

Filtr IP Hello zapobiega maszyn wirtualnych-gości z:

* Generowanie fałszywych ruchu.
* Nie odbiera ruch skierowany toothem.
* Kierowanie ruchu tooprotected infrastruktury punktów końcowych.
* Wysyłanie i odbieranie nieodpowiednie emisji ruchu.

Można umieścić maszyny wirtualne na [sieci wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-network/). Te sieci wirtualne są podobne sieci toohello skonfigurować w lokalnych środowiskach, na którym są zwykle skojarzone z przełącznikiem wirtualnym. Maszyny wirtualne podłączone toohello, który tej samej sieci wirtualnej mogą komunikować się ze sobą bez dodatkowej konfiguracji. Można również skonfigurować różne podsieci w sieci wirtualnej.

Program hello następujące technologie sieci wirtualnych Azure toohelp bezpiecznej komunikacji w sieci wirtualnej:

* [**Sieciowe grupy zabezpieczeń (NSG)**](../virtual-network/virtual-networks-nsg.md). W Twojej sieci wirtualnej można użyć grupy NSG toocontrol ruchu tooone lub więcej wystąpień maszyny wirtualnej. Sieciowa grupa zabezpieczeń zawiera reguły kontroli dostępu, które zezwalają na ruch lub go blokują w oparciu o kierunek ruchu, protokół, adres źródłowy i docelowy oraz port.
* [**Zdefiniowane przez użytkownika routingu**](../virtual-network/virtual-networks-udr-overview.md). Można kontrolować hello routingiem pakietów przez urządzenie wirtualne, tworząc trasy zdefiniowane przez użytkownika, określające hello następnego skoku dla pakietów przepływających tooa określonej podsieci toogo tooa sieci wirtualnej zabezpieczeń urządzenia.
* [**Przekazywanie IP**](../virtual-network/virtual-networks-udr-overview.md). Urządzenia zabezpieczeń sieci wirtualnej musi być możliwe tooreceive ruchu przychodzącego, który nie jest tooitself zaadresowane. miejsca docelowe tooother skierowana tooallow ruchu tooreceive maszyn wirtualnych, Włącz przesyłanie dalej IP dla maszyny wirtualnej hello.
* [**Wymuszane tunelowanie**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). Wymuszanie tunelowania umożliwia przekierowanie lub "force" wszystkie ruch do Internetu generowany przez maszyny wirtualne w lokalizacji lokalnej wstecz tooyour sieci wirtualnej za pośrednictwem tunelu VPN lokacja lokacja dla inspekcji i inspekcji
* [**Listy ACL punktu końcowego**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Można kontrolować, komputery, które są dozwolone połączenia przychodzące z maszyny wirtualnej tooa Internet hello w sieci wirtualnej, definiując listy ACL punktu końcowego.
* [**Rozwiązania zabezpieczeń sieciowych oferowane przez partnerów**](https://azure.microsoft.com/marketplace/). Istnieje szereg partnerskich rozwiązań zabezpieczeń sieci, które są dostępne hello Azure Marketplace.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Jak Azure implementuje sieci wirtualnych i zapór
Azure implementuje filtrowanie pakietów zapór na wszystkich maszynach wirtualnych hosta i gościa domyślnie. Obrazy systemu operacyjnego Windows hello Azure Marketplace ma także włączona domyślnie Zapora systemu Windows. Moduły równoważenia obciążenia w obwodzie hello Azure sieci publicznych kontroli komunikacji na podstawie list ACL adresu IP, zarządzane przez administratorów klienta.

Jeśli dane klienta na platformie Azure są przenoszone w ramach zwykłych operacji lub podczas awarii, odbywa się to za pośrednictwem prywatnych, szyfrowanych kanałów komunikacyjnych. Inne funkcje zatrudnieni przez Azure toouse w sieci wirtualnych i zapory są:

* **Zapora hosta natywnego**: sieć szkieletowa usług Azure i usługi Azure Storage, uruchom na natywnej systemu operacyjnego z nie funkcji hypervisor. Dlatego zapory systemu windows hello jest skonfigurowany z hello poprzednich dwóch zestawów reguł. Magazyn uruchamia natywnego toooptimize wydajności.
* **Zapory hostów**: Zapora hosta hello jest system operacyjny hosta hello tooprotect, uruchomioną hello funkcji hypervisor. reguły Hello jest jedynym kontrolerem sieci szkieletowej usług hello zaprogramowanych tooallow i przejść systemu operacyjnego hosta toohello tootalk pól na określonym porcie. Witaj pozostałe wyjątki są tooallow DHCP odpowiedzi i odpowiedzi DNS. Azure korzysta z pliku konfiguracji komputera, który ma hello szablonu reguł zapory dla systemu operacyjnego hosta hello. sam host Hello jest chroniony na ataki zewnętrzne komunikatu toopermit skonfigurowano zaporę systemu Windows tylko ze znanych, uwierzytelnionym źródeł.
* **Gość zapory**: replikuje reguły hello w filtr pakietów przełącznika maszyny wirtualnej hello ale zaprogramowanych w różnych oprogramowania (na przykład fragment zapory systemu Windows hello system operacyjny gościa hello). Hello gościa maszyny wirtualnej zapory może być skonfigurowany toorestrict tooor komunikacji z maszyny wirtualnej gościa hello, nawet jeśli komunikacja hello jest dozwolone przez konfiguracje na hoście hello filtru IP. Na przykład można wybrać toouse hello gościa maszyny wirtualnej zapory toorestrict komunikacji między dwiema Twojej sieci wirtualnych, które zostały skonfigurowane tooconnect tooone innego.
* **Zapory magazynu (PD)**: hello zapory na powitania magazynu frontonu filtry ruchu toobe tylko z portów 80/443 i inne narzędzia niezbędne porty. Zapora Hello na powitania magazynu zaplecza ogranicza toocome komunikację tylko z serwerów frontonu magazynu.
* **Brama sieci wirtualnej**: hello [Brama sieci wirtualnej Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) służy jako brama między lokalizacjami hello łączenie obciążeń w sieci wirtualnej Azure tooyour lokacjami lokalnymi. Jest wymagane tooconnect do lokacji lokalnej tooon [tuneli VPN lokacja lokacja IPsec](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), lub za pomocą [ExpressRoute](../expressroute/expressroute-introduction.md) obwodów. Dla tuneli IPsec i IKE sieci VPN bramy hello przeprowadzić Uzgodnienia IKE i ustanowienia hello tunel VPN S2S protokołu IPsec między sieciami wirtualnymi hello i lokacjami lokalnymi. Bramy sieci wirtualnej również przerwanie [sieci VPN typu punkt lokacja](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Bezpieczny dostęp zdalny
Dane przechowywane w chmurze hello musi mieć wystarczające zabezpieczenia włączone tooprevent luki w zabezpieczeniach i zachowania poufności i integralności podczas podczas przesyłania danych. Obejmują one kontrolki sieci powiązane z mechanizmami zarządzania dostępem i tożsamościami podlegającymi inspekcji w oparciu o zasady.

Wbudowanej technologii kryptograficznych pozwala tooencrypt komunikacji w ramach i między wdrożeniami, między regiony platformy Azure oraz z Azure tooon lokalnych centrów danych. Toovirtual dostępu administratora maszyny za pośrednictwem [sesji pulpitu zdalnego](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [zdalnej programu Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), i hello portalu Azure są zawsze szyfrowane.

toosecurely rozszerzanie lokalnego centrum danych chmury toohello, platforma Azure udostępnia zarówno [sieci VPN typu lokacja lokacja](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) i [sieci VPN typu punkt lokacja](../vpn-gateway/vpn-gateway-point-to-site-create.md), oraz dedykowane łącza o [ExpressRoute](../expressroute/expressroute-introduction.md)(tooAzure połączeń sieci wirtualnych za pośrednictwem połączenia VPN są szyfrowane).

### <a name="how-azure-implements-secure-remote-access"></a>Implementowanie bezpiecznego dostępu zdalnego na platformie Azure
Zawsze musi zostać uwierzytelniony toohello połączeń portalu Azure, a potrzebują SSL/TLS. Można skonfigurować zarządzanie bezpiecznego tooenable certyfikaty zarządzania. Standardowe protokoły, takie jak [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) i [IPsec](https://en.wikipedia.org/wiki/IPsec) są w pełni obsługiwane.

Usługa [Azure ExpressRoute](../expressroute/expressroute-introduction.md) umożliwia tworzenie prywatnych połączeń między centrami danych platformy Azure oraz infrastrukturą znajdującą się w lokalizacji lokalnej lub wspólnej. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Oferują więcej niezawodności, szybkości szybsze niższe opóźnienia i lepsze zabezpieczenia niż typowe łącza internetowego. W niektórych przypadkach transferu danych między lokalnymi lokalizacji i Azure przy użyciu połączeń ExpressRoute również może spowodować znaczne oszczędności.

## <a name="logging-and-monitoring"></a>Rejestrowanie i monitorowanie
Platforma Azure udostępnia uwierzytelnionego rejestrowania zdarzeń związanych z zabezpieczeniami, które generują dziennik inspekcji i jest odtworzone tootampering toobe odporność. W tym informacje o systemie, takie jak dzienniki zdarzeń zabezpieczeń infrastruktury platformy Azure, maszyny wirtualne i usługi Azure AD. Monitorowanie zdarzeń zabezpieczeń obejmuje zbierania zdarzeń, takie jak zmiany adresów IP serwera DHCP lub DNS; tooports prób uzyskania dostępu, protokoły lub adresy IP, które są blokowane przez projekt; zmiany w ustawieniach zasad lub zapora zabezpieczeń; Tworzenie konta lub grupy; i nieoczekiwane procesy lub instalacja sterownika.

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

Dzienniki inspekcji rejestrujące dostęp i działania uprawnionych użytkowników, próby uzyskania autoryzowanego i nieautoryzowanego dostępu, wyjątki systemowe i zdarzenia zabezpieczeń danych są przechowywane przez określony okres. Witaj przechowywania dzienników jest według uznania, ponieważ Konfigurowanie zbierania dzienników i przechowywania tooyour własnych wymagań.

### <a name="how-azure-implements-logging-and-monitoring"></a>Implementowanie rejestrowania i monitorowania na platformie Azure
Azure wdraża obliczeń tooeach agentów agentów zarządzania (MA) i monitorowania zabezpieczeń Azure (ASM), magazynu lub węzeł sieci szkieletowej w obszarze Zarządzanie native lub wirtualnych. Każdy Agent zarządzania jest skonfigurowany tooauthenticate tooa usługi team konta magazynu przy użyciu certyfikatu uzyskanego z magazynu certyfikatów Azure hello i do przodu wstępnie skonfigurowane diagnostycznych i konto magazynu toohello danych zdarzenia. Agenci nie są toocustomers wdrożonych maszyn wirtualnych.

Azure Administratorzy dostępu do dzienników za pośrednictwem portalu sieci web, uwierzytelnionym i kontrolą dostępu toohello dzienników. Administrator może filtrować, korelować i analizować dzienniki. kont magazynu zespół usługi Azure Hello dla dzienniki są chronione przed toohelp dostępu bezpośredniego administratora zapobiec naruszeniu dziennika.

Firma Microsoft zbiera dzienniki urządzeń sieciowych przy użyciu protokołu Syslog hello oraz serwery hosta przy użyciu usługi Microsoft Audit Collection Services (ACS). Te dzienniki są umieszczane w dziennika bazy danych, z której zostaną wygenerowane alerty dla zdarzeń podejrzane. Hello administrator można uzyskać dostęp i analizować te dzienniki.

[Diagnostyka Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) jest funkcją Azure umożliwiającą toocollect danych diagnostycznych z aplikacji działających na platformie Azure. To są dane diagnostyczne dla debugowania i rozwiązywania problemów, pomiaru wydajności monitorowania użycia zasobów, analizy ruchu, planowanie pojemności i inspekcji. Po zebraniu danych diagnostycznych hello może być przeniesione tooan kontem magazynu platformy Azure trwałości. Transfery albo mogą być planowane lub na żądanie.

## <a name="threat-mitigation"></a>Ograniczenie zagrożeń
Dodanie tooisolation, szyfrowania i filtrowanie Azure wykorzystuje wiele zagrożeń środki zaradcze mechanizmy i procesy tooprotect infrastrukturą i usługami. Te obejmują kontrole wewnętrzne oraz toodetect technologie używane i eliminowanie zagrożeń zaawansowanych, takich jak DDoS, podwyższenie poziomu uprawnień i hello [10 pierwszych OWASP](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

Opcje zabezpieczeń Hello i procesów zarządzania ryzykiem firmy Microsoft ma w miejscu toosecure zmniejszyć jego infrastruktury chmury hello ryzyko naruszenia zabezpieczeń. W hello zdarzenie wystąpi zdarzenie, hello zespołu zarządzania zdarzeniami zabezpieczeń (SIM) w obrębie zespołu Microsoft Online Services zabezpieczeń i zgodności (OSSC) hello jest gotowy toorespond w dowolnym momencie.

### <a name="how-azure-implements-threat-mitigation"></a>Implementowanie ograniczania zagrożeń na platformie Azure
Azure ma kontroli bezpieczeństwa w miejscu tooimplement zagrożeń ograniczenie i również klientów toohelp ograniczyć potencjalne zagrożenia w swoich środowiskach. Witaj Poniższa lista zawiera podsumowanie możliwości ograniczenie zagrożeń hello oferowanych na platformie Azure:

* [Azure ochrony przed złośliwym kodem](azure-security-antimalware.md) jest domyślnie włączone na wszystkich serwerach infrastruktury. Możesz opcjonalnie można udostępnić go w maszynach wirtualnych.
* Firma Microsoft prowadzi ciągłe monitorowanie z przekraczaniem zagrożenia toodetect serwerów, sieci i aplikacji i zapobiec luki w zabezpieczeniach. Automatyczne alerty powiadamiają Administratorzy nietypowych zachowań, pozwalając im działania naprawcze tootake na zagrożeń wewnętrznych i zewnętrznych.
* W ramach subskrypcji, takie jak zapory aplikacji sieci web z wdrożeniem rozwiązania innych firm zabezpieczeń [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Firmy Microsoft podejście toopenetration testy obejmują "[zespołu kart interfejsu sieciowego czerwony](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," który obejmuje specjalistom ds. zabezpieczeń firmy Microsoft do zaatakowania systemów produkcyjnych na żywo (z systemem innym niż klienta) w Azure tootest ochronę przed rzeczywistych, zaawansowane , zagrożenia.
* Wdrażanie zintegrowanych systemów zarządzania hello dystrybucji oraz instalacji poprawki zabezpieczeń na hello platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/)

[Blog zespołu ds. zabezpieczeń platformy Azure](http://blogs.msdn.com/b/azuresecurity/)

[Centrum zabezpieczeń firmy Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

[Blog usługi Active Directory](http://blogs.technet.com/b/ad/)
