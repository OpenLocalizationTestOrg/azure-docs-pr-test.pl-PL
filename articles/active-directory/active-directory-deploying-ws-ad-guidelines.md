---
title: "aaaGuidelines dla wdrażania systemu Windows Server Active Directory na maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Jeśli wiesz, jak usługi domenowe toodeploy AD i usługi federacyjnej AD lokalnie, Dowiedz się, jak działają na maszynach wirtualnych Azure."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Wskazówki dotyczące wdrażania usługi Active Directory systemu Windows Server na maszynach wirtualnych Azure
W tym artykule opisano hello istotnych różnic między wdrażanie systemu Windows serwera usług domenowych Active Directory (AD DS) i Active Directory Federation Services (AD FS) lokalnie i wdrażania ich na maszynach wirtualnych Microsoft Azure.

## <a name="scope-and-audience"></a>Zakres i odbiorców
Artykuł Hello jest przeznaczony dla tych już z wdrożeniem lokalne usługi Active Directory. Obejmuje ona hello różnice między wdrożeniem usługi Active Directory na Microsoft Azure maszyny wirtualne/sieciach wirtualnych platformy Azure i wdrożeniach usługi Active Directory tradycyjnych, lokalnie. Maszyny wirtualne platformy Azure i sieci wirtualnych platformy Azure są częścią infrastruktury jako — usługa (IaaS) oferty dla tooleverage organizacji zasobów w chmurze hello obliczeniowych.

Dla tych, które nie są jeszcze znane z wdrażanie usługi Active Directory, zobacz hello [przewodniku wdrażania usług AD DS](https://technet.microsoft.com/library/cc753963) lub [Planowanie wdrożenia usług AD FS](https://technet.microsoft.com/library/dn151324.aspx) odpowiednio.

W tym artykule zakłada, że czytnik hello zapoznać się z hello następujące pojęcia:

* Windows Server AD DS wdrażania i zarządzania
* Wdrażanie i konfigurowanie infrastruktury DNS toosupport DS AD systemu Windows Server
* Windows Server AD FS wdrażania i zarządzania
* Wdrażanie, konfigurowanie i zarządzanie aplikacjami danej firmy (usługi sieci web i witryn sieci Web) mogą używających tokenów systemu Windows Server AD FS
* Pojęcia ogólne maszyny wirtualnej, takie jak jak tooconfigure a wirtualnej maszyny, wirtualne dyski i sieci wirtualnych

W tym artykule omówiono wymagania hello scenariusza hybrydowego wdrożenia w których systemu Windows Server AD DS lub AD FS częściowo wdrożonej lokalnymi i częściowo wdrożonych na maszynach wirtualnych Azure. dokument Hello obejmuje najpierw hello krytyczne różnice między systemem Windows Server AD DS i AD FS na maszynach wirtualnych Azure i lokalnego, a punkty ważnych decyzji, które mają wpływ na projektowanie i wdrażanie. rest Hello papieru hello opisano wskazówki dla każdego punkty decyzyjne hello w bardziej szczegółowo i jak tooapply hello wytyczne toovarious wdrożeń.

W tym artykule omówiono konfiguracji hello [usługi Azure Active Directory](http://azure.microsoft.com/services/active-directory/), czyli opartego na interfejsie REST usługi, która udostępnia możliwości kontroli dostępu i zarządzania tożsamościami dla aplikacji w chmurze. Azure Active Directory (Azure AD) i Windows Server usług AD DS są, jednak zaprojektowane toowork razem tooprovide tożsamościami i dostępem rozwiązania do zarządzania dla współczesnych hybrydowego IT środowisk i nowoczesnych aplikacji. toohelp poznać różnice hello i relacje między systemu Windows Server AD DS i Azure AD, należy wziąć pod uwagę następujące hello:

1. Możesz napotkać systemu Windows Server AD DS w chmurze hello na maszynach wirtualnych Azure podczas korzystania z usługi Azure tooextend lokalnego centrum danych chmury hello.
2. Można użyć usługi Azure AD toogive użytkowników aplikacji pojedynczego logowania jednokrotnego tooSoftware jako — usługa (SaaS). Microsoft Office 365 używa tej technologii, na przykład i aplikacje działające na platformie Azure lub innych platform chmury można jej również użyć.
3. Można użyć usługi Azure AD (jej usługi kontroli dostępu) toolet użytkownikom zalogować się przy użyciu tożsamości z usługi Facebook, Google, Microsoft i innych tooapplications dostawców tożsamości, które znajdują się w chmurze hello lub lokalnie.

Aby uzyskać więcej informacji na temat tych różnic, zobacz [tożsamości Azure](fundamentals-identity.md).

## <a name="related-resources"></a>Powiązane zasoby
Może pobierać i uruchamiać hello [oceny gotowości maszyny wirtualnej Azure](https://www.microsoft.com/download/details.aspx?id=40898). Hello oceny zostanie automatycznie sprawdzać w lokalnym środowisku i generować raportu niestandardowego oparte na powitania wskazówki znaleziono toohelp w tym temacie migracja hello tooAzure środowiska.

Zalecamy również najpierw zapoznanie się hello samouczki, prowadnice i klipów wideo, które obejmują hello następujące tematy:

* [Konfigurowanie sieci wirtualnej Cloud-Only w hello portalu Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Konfigurowanie sieci VPN lokacja-lokacja w hello portalu Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalowanie nowego lasu usługi Active Directory w sieci wirtualnej platformy Azure](active-directory-new-forest-virtual-machine.md)
* [Instalowanie repliki kontrolera domeny usługi Active Directory na platformie Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS specjalista IT: (01) maszyny wirtualnej podstawy](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS specjalista IT: (05) tworzenie sieci wirtualnych i łączności między lokalizacjami](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Wprowadzenie
Witaj podstawowe wymagania dotyczące wdrażania usługi Active Directory systemu Windows Server na maszynach wirtualnych Azure różnią się bardzo mało z wdrożeniem go w lokalnych maszyn wirtualnych (i, toosome stopniu maszyn fizycznych). Na przykład w hello wielkość liter w systemie Windows Server AD DS, jeśli kontrolery domeny hello (DC) wdrażanych na maszynach wirtualnych Azure są replik w istniejącym lokalnym firmowej domenie lub lesie, a następnie hello wdrożenia usługi Azure może być traktowana przede wszystkim w hello tak samo jak mogą traktować innych dodatkowych lokacji usługi Active Directory systemu Windows Server. Oznacza to podsieci muszą być zdefiniowane w systemu Windows Server AD DS, utworzyć lokacji, podsieci hello połączone toothat lokacji i podłączone Lokacje tooother przy użyciu odpowiednich linków lokacji. Istnieją, jednak pewne różnice, które są typowe tooall Azure wdrożeń i niektóre, które różnią się zgodnie z toohello wdrażania scenariusza. Poniżej opisano dwa podstawowe różnice:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Maszyny wirtualne platformy Azure może być konieczne firmowej sieci lokalnej toohello łączności.
Łączenie maszyn wirtualnych platformy Azure wstecz tooan lokalnej sieci firmowej wymaga sieci wirtualnej platformy Azure, w tym lokacja do lokacji lub punktu lokacji wirtualnej sieci prywatnej (VPN) składnika tooseamlessly mogli połączyć maszyn wirtualnych platformy Azure i komputerach lokalnych. Ten składnik sieci VPN można również włączyć lokalnej domeny Członkowskie komputerów tooaccess domeny usługi Active Directory systemu Windows Server, w których kontrolery domeny są obsługiwane wyłącznie na maszynach wirtualnych Azure. Jest ważne toonote, jednak, że jeśli hello VPN kończy się niepowodzeniem, uwierzytelniania i innych operacji, które są zależne od usługi Active Directory systemu Windows Server również zakończy się niepowodzeniem. Gdy użytkownicy będą mogli toosign przy użyciu istniejących poświadczeń pamięci podręcznej, wszystkie peer-to-peer lub próby uwierzytelniania klient serwer dla bilety ma jeszcze toobe wystawiony ani starych stały się zakończy się niepowodzeniem.

Zobacz [sieci wirtualnej](http://azure.microsoft.com/documentation/services/virtual-network/) pokaz wideo i listę samouczki krok po kroku, w tym [skonfigurowania sieci VPN lokacja-lokacja w portalu Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Windows Server Active Directory można także wdrożyć w sieci wirtualnej platformy Azure, która nie ma łączności z siecią lokalną. wytyczne Hello w tym temacie założono jednak użytą sieci wirtualnej platformy Azure, ponieważ zapewnia możliwości, które są niezbędne tooWindows serwera adresów IP.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Statyczne adresy IP musi być skonfigurowany przy użyciu programu Azure PowerShell.
Dynamiczne adresy są przydzielane domyślnie, ale zamiast tego użyj tooassign polecenia cmdlet Set-AzureStaticVNetIP hello statycznego adresu IP. Które ustawia statyczny adres IP, który będzie aktualny za pośrednictwem naprawą usługi i zamykania maszyny Wirtualnej ponownego uruchomienia komputera. Aby uzyskać więcej informacji, zobacz [statyczny adres IP wewnętrznego dla maszyn wirtualnych](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>— Warunki
Witaj poniżej przedstawiono listę niepełna warunków dla różnych technologii platformy Azure, które zostanie dodane odwołanie w tym artykule.

* **Maszyny wirtualne platformy Azure**: hello oferty IaaS na platformie Azure, który umożliwia klientom toodeploy uruchomionych maszyn wirtualnych niemal wszystkie tradycyjnie lokalnej obciążenie serwera.
* **Sieć wirtualna platformy Azure**: hello sieci usługi na platformie Azure, który umożliwia klientom tworzenie i zarządzanie sieciami wirtualnymi na platformie Azure oraz ich bezpiecznego połączenia tootheir własnych lokalną infrastrukturę sieci przy użyciu wirtualnej sieci prywatnej (VPN).
* **Wirtualny adres IP**: to znaczy adresów IP internetowy niepowiązana tooa określonego komputera lub sieci karty interfejsu. Usługi w chmurze są przypisywane wirtualnego adresu IP do odbierania ruchu sieciowego, czyli przekierowanego tooan maszyny Wirtualnej platformy Azure. Wirtualny adres IP jest właściwością usługi w chmurze, która może zawierać jeden lub więcej maszyn wirtualnych platformy Azure. Należy również zauważyć, że sieć wirtualną platformy Azure może zawierać co najmniej jedną usługę chmury. Wirtualne adresy IP zapewniają natywnej funkcji równoważenia obciążenia.
* **Dynamicznego adresu IP**: jest to adres IP hello jest tylko wewnętrzna. Go powinna być skonfigurowana jako statyczny adres IP (przy użyciu polecenia cmdlet hello zestaw AzureStaticVNetIP) dla maszyn wirtualnych obsługujących role serwera hello DNS kontrolera domeny.
* **Naprawianie usługi**: hello proces, w którym Azure automatycznie zwraca tooa usługi stanu uruchomiona ponownie po wykryciu hello usługi nie powiodło się. Naprawianie usługi jest jednym z hello aspektów platformy Azure, która obsługuje dostępność i odporność. Gdy jest to mało prawdopodobne, wyniku hello usługi naprawianie zdarzenia dla kontrolera domeny uruchomiony na maszynie Wirtualnej jest podobne tooan nieplanowane ponowne uruchomienie komputera, ale ma kilka efekty uboczne:
  
  * zmieni Hello wirtualnej karty sieciowej w hello maszyny Wirtualnej
  * adres MAC karty sieci wirtualnej hello Hello ulegnie zmianie.
  * zmieni Hello identyfikator procesora/Procesora hello maszyny Wirtualnej
  * Witaj konfiguracji IP hello wirtualnej karty sieciowej nie zmieni się tak długo, jak hello maszyna wirtualna jest dołączona tooa sieci wirtualnej i hello adres IP maszyny Wirtualnej jest statyczny.
  
  Żadna z tych zachowań wpływ na usługi Active Directory systemu Windows Server ponieważ ma ona zależność hello adres MAC lub identyfikator procesora/Procesora, a wszystkie wdrożenia usługi Active Directory systemu Windows Server na platformie Azure są zalecane toobe Uruchom na sieć wirtualną platformy Azure zgodnie z powyższym .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Jest to kontrolerów domeny usługi Active Directory systemu Windows Server toovirtualize awaryjnym?
Wdrażanie kontrolerów domeny katalogu Active systemu Windows Server na maszynach wirtualnych Azure jest toohello podmiotu tych samych wskazówek jako uruchomione kontrolery domeny lokalnych na maszynie wirtualnej. Uruchomienie zwirtualizowanych kontrolerów domeny jest bezpieczne rozwiązanie, tak długo, jak wytyczne dotyczące tworzenia kopii zapasowej i przywracanie kontrolery domeny zostaną wykonane. Aby uzyskać więcej informacji dotyczących ograniczenia i wytyczne dotyczące uruchamiania zwirtualizowanych kontrolerów domeny, zobacz [uruchamianie kontrolerów domeny w funkcji Hyper-V](https://technet.microsoft.com/library/dd363553).

Funkcji hypervisor Podaj lub trivialize technologie, które mogą spowodować problemy w przypadku wielu systemów rozproszonych, w tym Windows Server Active Directory. Na przykład na serwerze fizycznym, można sklonować dysku lub przy użyciu nieobsługiwanej metody tooroll wstecz hello stanu serwera, w tym za pomocą sieci SAN i tak dalej, ale operacją na serwerze fizycznym jest trudniejsze niż przywracania migawki maszyny wirtualnej w ramach funkcji hypervisor. Platforma Azure oferuje funkcje, które mogą skutkować hello takie same niepożądanych warunku. Na przykład nie należy kopiować pliki VHD kontrolerów domeny zamiast regularnego wykonywania kopii zapasowych przywracanie ich może powodować podobne funkcje przywracania migawki toousing sytuacji.

Takie wycofań wprowadzenie rozbieżnościach numerów USN, które mogą prowadzić toopermanently stanów rozbieżności między kontrolerów domeny. Które mogą spowodować problemy takie jak:

* Obiektach pokutujących
* Niespójne hasła
* Wartości atrybutów niespójna
* Niezgodność schematu, jeśli wzorzec schematu hello zostanie wycofana

Aby uzyskać więcej informacji na temat wpływ kontrolerów domeny, zobacz [numerów USN i wycofanie numerów USN](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

Począwszy od systemu Windows Server 2012, [dodatkowe zabezpieczenia są wbudowane w tooAD DS](https://technet.microsoft.com/library/hh831734.aspx). Te zabezpieczenia chronić zwirtualizowanych kontrolerów domeny przed problemami z wyżej wymienionych hello hello podstawowej platformy funkcji hypervisor obsługuje identyfikator generacji maszyny Wirtualnej. Azure obsługuje identyfikator VM-GenerationID, co oznacza, że kontrolery domeny z systemem Windows Server 2012 lub nowszego Azure maszyny wirtualne mają hello dodatkowe zabezpieczenia.

> [!NOTE]
> Należy zamknąć i ponownie uruchomić maszynę Wirtualną, która jest uruchamiany roli kontrolera domeny hello na platformie Azure w ramach systemu operacyjnego gościa hello zamiast hello **Shut Down** opcję hello Azure porta. Obecnie za pomocą portalu tooshut hello wyłączenia maszyny Wirtualnej powoduje, że toobe wirtualna hello alokację. Deallocated maszyna wirtualna ma zaletą hello nie są naliczane opłaty, ale również resetuje ono hello generacji maszyny Wirtualnej, który jest niepożądanych dla kontrolera domeny. Gdy hello generacji maszyny Wirtualnej zostanie zresetowana, invocationID hello hello AD DS z bazy danych również jest resetowany, hello puli identyfikatorów RID jest odrzucany i folderu SYSVOL jest oznaczony jako nieautorytatywny. Aby uzyskać więcej informacji, zobacz [tooActive wprowadzenie wirtualizacja usług domenowych Directory (AD DS)](https://technet.microsoft.com/library/hh831734.aspx) i [bezpieczna wirtualizacja usługi DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Dlaczego wdrażania systemu Windows Server AD DS na maszynach wirtualnych platformy Azure?
Wiele scenariuszy wdrażania systemu Windows Server AD DS dobrze nadają się do wdrażania maszyn wirtualnych na platformie Azure. Na przykład załóżmy, że masz firmy w Europie, który wymaga tooauthenticate użytkowników w lokalizacji zdalnej w Azji. Witaj firmy nie wcześniej wdrożony serwer Active Directory kontrolerów domeny systemu Windows w Azji powodu toodeploy toohello koszt doświadczenia z nich i ograniczone toomanage hello serwerów po wdrożeniu. W związku z tym żądania uwierzytelniania od Azja są obsługiwane przez kontrolery domeny w Europie nieoptymalne wyniki. W takim przypadku można wdrożyć kontrolera domeny na maszynie Wirtualnej, określony muszą być uruchamiane w hello centrum danych Azure w Azji. Dołączanie tooan tego kontrolera domeny sieci wirtualnej platformy Azure, połączoną bezpośrednio z lokalizacji zdalnej toohello poprawi wydajność uwierzytelniania.

Azure jest również nadają się jako substitute toootherwise kosztowne awaryjnego odzyskiwania (DR). Witaj stosunkowo niskich kosztach obsługi niewielkiej liczby kontrolerów domeny i jednej sieci wirtualnych na platformie Azure reprezentuje atrakcyjną alternatywą.

Na koniec można toodeploy aplikację sieciową na platformie Azure, takich jak SharePoint, która wymaga usługi Active Directory systemu Windows Server, lecz ma nie zależności na powitania lokalnej sieci lub hello firmy Windows Server Active Directory. W takim przypadku wdrożeniem izolowanego lasu na hello Azure toomeet SharePoint wymagania serwera jest optymalna. Ponownie wdrażanie aplikacji sieciowych, które wymagają łączności toohello lokalnej sieci i hello firmowej usługi Active Directory jest również obsługiwany.

> [!NOTE]
> Ponieważ zapewnia połączenie warstwy 3 hello składnika sieci VPN, który zapewnia łączność w sieci wirtualnej platformy Azure i siecią lokalną można również włączyć serwery członkowskie z systemem kontrolery domeny tooleverage lokalnych działających jako maszyny wirtualne platformy Azure na platformie Azure sieć wirtualna. Jednak jeśli hello sieci VPN jest niedostępny, komunikację między komputerami lokalnymi i kontrolery domeny z systemem Azure nie będzie działać, co zapewnia uwierzytelnianie i różnych innych błędów.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Różni się między wdrażania kontrolerów domeny usługi Active Directory systemu Windows Server na maszynach wirtualnych platformy Azure i lokalnymi
* W żadnym scenariuszu wdrożenia usługi Active Directory systemu Windows Server, który zawiera więcej niż jednej maszyny Wirtualnej jest konieczne toouse sieci wirtualnej platformy Azure, spójności adresów IP. Należy pamiętać, że w tym przewodniku założono, że kontrolery domeny są uruchomione na sieć wirtualną platformy Azure.
* Podobnie jak w przypadku lokalnego kontrolerów domeny, zaleca się statycznych adresów IP. Statyczny adres IP można skonfigurować tylko za pomocą programu Azure PowerShell. Zobacz [statyczny adres IP wewnętrznego dla maszyn wirtualnych](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) więcej szczegółów. Jeśli monitorowanie systemów lub innych rozwiązań sprawdzających konfiguracji statycznego adresu IP w systemie operacyjnym gościa hello, można przypisać hello tego samego statycznego adresu IP adres toohello właściwości karty sieciowej z hello maszyny Wirtualnej. Należy jednak pamiętać, że karta sieciowa hello zostaną usunięte, jeśli hello wirtualna ulega naprawą usługi lub jest wyłączony w portalu hello i jego adres cofnięciu przydziału. W takim przypadku statyczny adres IP hello gościu hello należy toobe resetowania.
* Wdrażanie maszyn wirtualnych w sieci wirtualnej nie pociąga za sobą (lub wymagają) łączność sieci lokalnej wstecz tooan; sieć wirtualna Hello umożliwia jedynie tej możliwości. Należy utworzyć wirtualnej sieci prywatnej komunikacji między Azure i siecią lokalną. Należy toodeploy punktu końcowego sieci VPN w sieci lokalnej hello. Witaj sieci VPN jest otwierany z sieci lokalnej toohello platformy Azure. Aby uzyskać więcej informacji, zobacz [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md) i [skonfigurowania sieci VPN lokacja-lokacja w portalu Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Opcja zbyt[utworzyć VPN punkt lokacja](../vpn-gateway/vpn-gateway-point-to-site-create.md) jest dostępne tooconnect poszczególnych komputerów z systemem Windows bezpośrednio tooan sieci wirtualnej platformy Azure.
> 
> 

* Niezależnie od tego, czy tworzenia wirtualnej sieci lub nie, Azure opłaty za wyjście ruch, ale nie wejściowych. Różne opcje projektowania usługi Active Directory systemu Windows Server może mieć wpływ na ilość ruchu wyjście jest generowany przez wdrożenie. Na przykład wdrożenia kontrolera domeny tylko do odczytu (RODC) ogranicza ruch wychodzący ruch nie jest replikowany ruchu wychodzącego. Ale decyzji hello toodeploy kontrolera RODC należy toobe porównywany tooperform potrzeby hello zapisu względem hello kontrolera domeny i hello [zgodności](https://technet.microsoft.com/library/cc755190) aplikacji i usług w witrynie hello że z kontrolera RODC. Aby uzyskać więcej informacji o opłatach ruchu sieciowego, zobacz [Azure, w skrócie cennik](http://azure.microsoft.com/pricing/).
* Gdy masz pełną kontrolę nad jakiego serwera toouse zasobów dla maszyn wirtualnych na obszarze firmy, takich jak ilość pamięci RAM, rozmiar dysku i tak dalej na platformie Azure musisz wybrać z listy wstępnie skonfigurowanego serwera rozmiary. Kontroler domeny dysk z danymi na potrzeby dodawania toohello system operacyjny dysku w kolejności toostore hello usługi Active Directory systemu Windows Server w bazie danych.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Można wdrażać systemu Windows Server AD FS na maszynach wirtualnych Azure?
Tak, można wdrożyć system Windows Server AD FS na maszynach wirtualnych Azure i hello [najlepszych rozwiązań dotyczących wdrażania usług AD FS](https://technet.microsoft.com/library/dn151324.aspx) lokalnymi zastosowanie tooAD FS wdrożenia na platformie Azure. Ale niektóre hello najlepszych rozwiązań, takich jak Równoważenie obciążenia i wysokiej dostępności wymagane technologie poza co usługi AD FS oferuje, samej siebie. Musi być one udostępniane przez hello podstawowej infrastruktury. Załóżmy przejrzenia niektórych z tych najlepszych rozwiązań i zobacz, jak może zostać osiągnięty przy użyciu maszyn wirtualnych platformy Azure i sieci wirtualnej platformy Azure.

1. **Nigdy nie uwidacznia serwerów usługi tokenów (STS) zabezpieczeń bezpośrednio toohello Internet.**
   
    Jest to ważne, ponieważ hello STS wystawia tokeny zabezpieczające. W związku z tym STS serwerów, takich jak serwery usług AD FS powinny być traktowane z hello sam poziom ochrony jako kontroler domeny. W przypadku naruszenia zabezpieczeń tokenu Zabezpieczającego złośliwi użytkownicy mają hello możliwości tooissue tokenów dostępu potencjalnie zawierające oświadczenia ich po wybraniu aplikacji firm toorelying oraz innych serwerów usługi STS w organizacjach ufających.
2. **Wdrożenie kontrolerów domeny usługi Active Directory dla wszystkich domen użytkownika w hello sam sieci jako serwery hello usług AD FS.**
   
    Serwery usług AD FS, użyj użytkowników tooauthenticate usług domenowych w usłudze Active Directory. Zalecane jest toodeploy kontrolerów domeny na powitania sam sieci jako hello AD FS serwery. Zapewnia ciągłość działania, w przypadku hello powiązanie hello sieć platformy Azure i sieci lokalnej jest uszkodzona i umożliwia mniejsze opóźnienia i zwiększa wydajność dla nazwy logowania.
3. **Wdrażanie wielu węzłów usług AD FS wysokiej dostępności i równoważenia obciążenia hello.**
   
    W większości przypadków hello awarii aplikacji, która umożliwia usług AD FS jest nie do przyjęcia, ponieważ krytyczne aplikacji hello, które wymagają tokeny zabezpieczające są często. W związku z tym i ponieważ usług AD FS znajduje się teraz w hello ścieżkę krytyczną tooaccessing misji krytyczne aplikacje, hello AD FS usługi musi być wysokiej dostępności przy użyciu wielu serwerów proxy usług AD FS i serwery usług AD FS. tooachieve dystrybucji żądań, usługi równoważenia obciążenia są zwykle wdrażane przed zarówno hello AD FS proxy, jak i serwery hello usług AD FS.
4. **Wdrażanie co najmniej jeden węzeł serwera Proxy aplikacji sieci Web, aby uzyskać dostęp do Internetu.**
   
    Jeśli użytkownicy muszą tooaccess aplikacji chronionej przez usługę FS hello AD, hello AD FS usługi potrzeb toobe dostępnej w sklepie hello internet. Jest to osiągane przez wdrożenie hello usługi Serwer Proxy aplikacji sieci Web. Zdecydowanie zaleca się toodeploy więcej niż jeden węzeł na potrzeby hello wysokiej dostępności i równoważenia obciążenia.
5. **Ograniczanie dostępu z zasobów sieciowych toointernal powitania serwera Proxy aplikacji sieci Web węzłów.**
   
    tooallow użytkowników zewnętrznych tooaccess usług AD FS z hello internet, należy toodeploy węzłów serwera Proxy aplikacji sieci Web (lub Proxy usług AD FS w starszych wersjach systemu Windows Server). powitania serwera proxy aplikacji sieci Web, którego węzły są bezpośrednio widoczne toohello Internet. Nie są one wymagane toobe przyłączonych do domeny i ich tylko muszą serwerów dostępu do toohello AD FS za pośrednictwem portów TCP 443 i 80. Zdecydowanie zaleca się tooall tej komunikacji jest zablokowany przez inne komputery (zwłaszcza w kontrolerach domeny).
   
    Jest to zazwyczaj osiągnięte lokalnej za pomocą strefą DMZ. Zapory w trybie dozwolonych operacji toorestrict ruchu w sieci lokalnej toohello hello DMZ (to znaczy tylko adresy IP określone przez ruch z hello i przez określone porty są dozwolone, a wszystkie inne ruch jest blokowany).

Witaj Poniższy diagram przedstawia tradycyjną lokalnego wdrożenia usług AD FS.

![Diagram wdrażania usług federacyjnych Active Directory tradycyjnych, lokalnie](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Jednak ponieważ Azure nie zapewnia natywnego, kompletne zapory funkcji, inne opcje potrzebne toobe używane toorestrict ruchu. Witaj poniższej tabeli przedstawiono poszczególne opcje, a jego zalety i wady.

| Opcja | Zalety | Wadą |
| --- | --- | --- |
| [Listy ACL sieć platformy Azure](../virtual-network/virtual-networks-acl.md) |Mniej kosztowne i łatwiejsze konfiguracji początkowej |Konfiguracja ACL dodatkowe sieci wymagane, jeśli wszelkie nowe maszyny wirtualne są dodawane toohello wdrożenia |
| [Barracuda NG zapory](https://www.barracuda.com/products/ngfirewall) |Tryb listy dozwolonych operacji i nie wymaga sieci ACL konfiguracji |Zwiększenie kosztów i wprowadzania złożoności początkowej instalacji |

Witaj ogólne kroki toodeploy usług AD FS w tym przypadku są następujące:

1. Tworzenie sieci wirtualnej z łączności między lokalizacjami, za pomocą sieci VPN lub [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Wdrożenie kontrolerów domeny w sieci wirtualnej hello. Ten krok jest opcjonalny, ale zalecane.
3. Wdrażanie domeny serwerów usług AD FS na powitania sieci wirtualnej.
4. Utwórz [zestaw o zrównoważonym obciążeniu wewnętrzny](http://azure.microsoft.com/blog/internal-load-balancing/) zawiera serwery hello usług AD FS i używa nowego prywatnego adresu IP w sieci wirtualnej hello (dynamicznego adresu IP).
   
   1. Zaktualizuj DNS toocreate hello FQDN toopoint toohello prywatne (dynamiczny) adres IP zestawu o zrównoważonym obciążeniu wewnętrzny hello.
5. Utworzenie usługi w chmurze (lub oddzielne sieci wirtualnej) dla hello węzłów serwera Proxy aplikacji sieci Web.
6. Wdrożyć hello węzły serwera Proxy aplikacji sieci Web w usłudze chmury hello lub sieci wirtualnej
   
   1. Utwórz zestaw o zrównoważonym obciążeniu zewnętrznych zawierającą hello węzłów serwera Proxy aplikacji sieci Web.
   2. Zaktualizuj hello zewnętrznych DNS nazwę (FQDN) toopoint toohello chmury usługi publiczny adres IP (hello wirtualnego adresu IP).
   3. Skonfiguruj hello toouse serwerów proxy usług AD FS nazwy FQDN, która odpowiada hello AD FS serwerów, zestawu o zrównoważonym obciążeniu wewnętrzny toohello.
   4. Zaktualizuj toouse witryn sieci web opartej na oświadczeniach hello zewnętrznej nazwy FQDN dla dostawcy oświadczeń.
7. Ograniczanie dostępu między maszyny tooany serwera Proxy aplikacji sieci Web w sieci wirtualnej hello AD FS.

ruch toorestrict hello zestawu równoważeniem obciążenia dla hello Azure wewnętrznego modułu równoważenia obciążenia wymaga toobe skonfigurowana do obsługi ruchu tylko tooTCP portów 80 i 443, a wszystkie inne ruchu toohello wewnętrznego dynamicznego adresu IP zestawu o zrównoważonym obciążeniu hello jest porzucany.

![Diagram sieci usług AD FS list kontroli dostępu przy TCP 443 i 80 dozwolone.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Ruch toohello AD FS serwery mogą być dozwolone tylko przez hello następujące źródła:

* Hello Azure wewnętrznego modułu równoważenia obciążenia.
* adres IP Hello administrator sieci lokalne powitania.

> [!WARNING]
> Hello projektu należy uniemożliwić osiągnięcia innych maszyn wirtualnych w hello sieci wirtualnej platformy Azure lub żadnych lokalizacji w sieci lokalnej hello węzłów serwera Proxy aplikacji sieci Web. Który jest możliwe przez skonfigurowanie reguł zapory w urządzenia lokalne powitania dla połączeń Expressroute lub hello urządzenia sieci VPN w połączeniach sieci VPN typu lokacja lokacja.
> 
> 

Opcja toothis wadą jest hello potrzeby tooconfigure hello sieciowej listy ACL dla wielu urządzeń, w tym wewnętrznego modułu równoważenia obciążenia, serwery hello usług AD FS i innych serwerów, które zostaną dodane toohello sieci wirtualnej. Jeśli dowolne urządzenie zostanie dodany toohello wdrożenia bez konfigurowania sieci listy ACL toorestrict ruchu tooit, hello całego wdrożenia może być zagrożone. Jeśli kiedykolwiek zmian adresów IP hello hello węzłów serwera Proxy aplikacji sieci Web, należy zresetować sieci hello listy kontroli dostępu (co oznacza, że serwery proxy hello powinien być skonfigurowany toouse [dynamicznych adresów IP](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![Usługi AD FS na platformie Azure za pomocą sieci listy kontroli dostępu.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Innym rozwiązaniem jest toouse hello [Barracuda NG zapory](https://www.barracuda.com/products/ngfirewall) urządzenia toocontrol ruchu między serwerami proxy usług AD FS i serwerami hello usług AD FS. Ta opcja jest zgodny z najlepsze rozwiązania dotyczące zabezpieczeń i wysokiej dostępności i wymaga mniej administracji po instalacji początkowej hello, ponieważ urządzenia zapory NG Barracuda hello zapewnia tryb dozwolonych administracji zapory i może być zainstalowana bezpośrednio w sieci wirtualnej platformy Azure. Która eliminuje hello potrzeby tooconfigure sieci listy ACL kiedykolwiek toohello wdrożenia jest dodawany nowy serwer. Jednak ta opcja dodaje początkowe wdrożenie złożoność oraz koszt projektu.

W takim przypadku dwie sieci wirtualne są wdrażane zamiast jednego. Zadzwonimy ich VNet1 i VNet2. VNet1 zawiera serwery proxy hello a VNet2 hello STSs i sieci firmowej wstecz toohello hello sieci połączenia. VNet1 w związku z tym jest fizycznie (chociaż praktycznie) izolowane od VNet2 i z kolei z sieci firmowej hello. VNet1 jest następnie tooVNet2 połączonych za pomocą specjalnych tunelowania technologii, znane jako transportu niezależne sieci architektura (TINA). Witaj TINA tunel jest dołączona tooeach hello sieci wirtualnych za pomocą zapory Barracuda NG — jeden Barracuda w każdej sieci wirtualnej hello.  Dla wysokiej dostępności zaleca się wdrożenie dwóch Szympansy w każdej sieci wirtualnej; jeden aktywny hello innych pasywne. Oferują one bardzo zaawansowane możliwości zapory umożliwiających nam toomimic hello działania DMZ tradycyjnych, lokalnie na platformie Azure.

![Usługi AD FS na platformie Azure za pomocą zapory.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Aby uzyskać więcej informacji, zobacz [usług AD FS: rozszerzenie toohello frontonu aplikacji obsługujących oświadczenia lokalnymi Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Alternatywne tooAD FS wdrożenie niepowodzeniem, jeśli celem hello jest Office 365 logowania jednokrotnego samodzielnie
Istnieje inny alternatywny toodeploying AD FS całkowicie, jeśli celem jest tylko tooenable logowania dla usługi Office 365. Można w takim przypadku po prostu wdrożyć narzędzia DirSync przy użyciu hasła synchronizacji lokalnie i osiągnięcia hello takiego samego wyniku zakończenia z złożoności minimalnego wdrożenia, ponieważ to rozwiązanie nie wymaga usług AD FS lub Microsoft Azure.

Witaj poniższej tabeli porównano działanie hello logowania procesy z włączonymi i wyłączonymi wdrażanie usług AD FS.

| Usługi Office 365 pojedynczego logowania za pomocą usług AD FS oraz narzędzia DirSync | Office 365 sam logowania jednokrotnego przy użyciu narzędzia DirSync i synchronizacji haseł |
| --- | --- |
| 1. hello użytkownika rejestruje tooa w sieci firmowej i jest uwierzytelniony tooWindows serwera usługi Active Directory. |1. hello użytkownika rejestruje tooa w sieci firmowej i jest uwierzytelniony tooWindows serwera usługi Active Directory. |
| 2. hello użytkownik spróbuje tooaccess usługi Office 365 (Jestem @contoso.com). |2. hello użytkownik spróbuje tooaccess usługi Office 365 (Jestem @contoso.com). |
| 3. Usługi Office 365 przekierowuje hello tooAzure użytkownika AD. |3. Usługi Office 365 przekierowuje hello tooAzure użytkownika AD. |
| 4. Ponieważ usługa Azure AD nie można uwierzytelnić użytkownika hello i rozumie, że istnieje relacja zaufania usług AD FS w lokalnym, przekierowuje tooAD użytkownika hello FS. |4. Usługi Azure AD nie może zaakceptować biletów Kerberos bezpośrednio i żadna relacja zaufania nie istnieje, więc żądania użytkownika hello wprowadź poświadczenia. |
| 5. hello użytkownik wysyła Kerberos biletu toohello AD FS STS. |5. hello użytkownik wprowadza hello takie same lokalne hasło i usługi Azure AD sprawdza poprawność je przed hello nazwy użytkownika i hasła, która była synchronizowana przez narzędzie DirSync. |
| 6. Usługi AD FS przekształca powitalne toohello biletu Kerberos wymagany format/oświadczeń i przekierowuje hello tooAzure użytkownika AD token. |6. Usługi Azure AD przekierowuje tooOffice użytkownika hello 365. |
| 7. Witaj użytkownik jest uwierzytelniany tooAzure AD (przekształcania innego występuje). |7. hello użytkownik może zalogować się w tooOffice 365 i za pomocą tokenu usługi Azure AD hello OWA. |
| 8. Usługi Azure AD przekierowuje tooOffice użytkownika hello 365. | |
| 9. użytkownik hello dyskretnie jest zalogowany na tooOffice 365. | |

W hello usługi Office 365 z narzędzia DirSync z scenariusz synchronizacji haseł (nie usług AD FS) logowanie jednokrotne zastępuje "tego samego logowania jednokrotnego" gdzie "sam" po prostu oznacza, że użytkownicy musi ponownie wprowadzić swoje tych samych poświadczeń lokalnego, podczas uzyskiwania dostępu do usługi Office 365. Należy pamiętać, że te dane mogą zapamiętanych przez użytkownika hello przeglądarki toohelp zmniejszyć kolejnych monitów.

### <a name="additional-food-for-thought"></a>Dodatkowe myśl for żywności
* W przypadku wdrożenia serwera proxy usług AD FS na maszynie wirtualnej platformy Azure, jest potrzebne połączenie toohello AD FS serwerów. Jeśli są one lokalnymi, zaleca się korzystać z połączenie sieci VPN typu lokacja lokacja hello dostarczanych przez hello sieci wirtualnej tooallow powitania serwera Proxy aplikacji sieci Web węzłów toocommunicate z ich serwerów usług AD FS.
* W przypadku wdrożenia serwera usług AD FS na platformie Azure wirtualnej maszyny, kontrolerów domeny usługi Active Directory Server tooWindows łączności, magazynów atrybutów i baz danych konfiguracji jest to konieczne, a także wymagać ExpressRoute lub połączeń VPN lokacja lokacja między hello Azure wirtualnych sieci i hello lokalnej sieci.
* Opłaty są stosowane tooall ruch z maszyn wirtualnych platformy Azure (ruch wychodzący). Jeśli koszt jest współczynnik pobudzenie hello, jest wskazane toodeploy powitania serwera Proxy aplikacji sieci Web węzłów na platformie Azure, pozostawiając hello usług AD FS serwerów lokalnych. Jeśli hello AD FS serwery są wdrażane na również maszyn wirtualnych platformy Azure, dodatkowych kosztów zostanie pobrany tooauthenticate lokalnych użytkowników. Ruch wychodzący generuje koszt niezależnie od tego, czy przechodzenie hello ExpressRoute lub hello połączenia sieci VPN lokacja lokacja.
* Jeśli zdecydujesz się obciążenie serwera natywnego toouse Azure równoważenia możliwości wysokiej dostępności serwerów usług AD FS, należy pamiętać, że Równoważenie obciążenia sieciowego zapewnia sond, które są używane toodetermine hello kondycji hello maszyn wirtualnych w ramach usługi w chmurze hello. W przypadku hello maszyn wirtualnych platformy Azure (w przeciwieństwie ról tooweb lub procesu roboczego) należy użyć niestandardowych sondowania ponieważ hello agenta, który odpowiada toohello domyślnej sondy nie znajduje się na maszynach wirtualnych platformy Azure. Dla uproszczenia, można użyć niestandardowej sondowaniem TCP — to wymaga tylko połączenia TCP (segmentów TCP SYN wysyłane i odpowiedzi toowith segmentów TCP SYN ACK) pomyślnie nawiązane toodetermine kondycja maszyny wirtualnej. Można skonfigurować toouse niestandardowych sondowania hello żadnych toowhich portu TCP, które maszyny wirtualne są aktywnie nasłuchujących.

> [!NOTE]
> Maszyny wymagające powitalne tooexpose sam zestaw portów bezpośrednio toohello Internet (np. port 80 i 443) nie mogą współużytkować hello tej samej usługi w chmurze. W związku z tym zaleca się utworzenie usługi w chmurze dedykowane dla serwerów systemu Windows Server AD FS w kolejności tooavoid potencjalnych pokrywa się między wymagania dotyczące portów dla aplikacji i usług systemu Windows Server AD FS.
> 
> 

## <a name="deployment-scenarios"></a>Scenariusze wdrażania
Hello następujące części przedstawiono popularne scenariusze toodraw uwagi tooimportant zagadnienia dotyczące wdrażania należy wziąć pod uwagę. Każdy scenariusz zawiera łącza toomore szczegóły hello decyzje i tooconsider czynników.

1. [Usługi AD DS: Wdrażanie aplikacji obsługujących usługi AD DS z nie jest wymagany dla łączności z siecią firmową](#BKMK_CloudOnly)
   
    Na przykład usługi internetowy programu SharePoint jest wdrożony na maszynie wirtualnej platformy Azure. Aplikacja Hello nie ma zależności zasobów sieci firmowej. Witaj aplikacja wymaga systemu Windows Server AD DS, ale nie wymaga hello firmowych systemu Windows Server AD DS.
2. [Usług AD FS: Toohello frontonu aplikacji obsługujących oświadczenia lokalnymi Internet rozszerzenia](#BKMK_CloudOnlyFed)
   
    Na przykład aplikacji obsługującej oświadczenia, który został pomyślnie wdrożony lokalnymi i używane przez użytkowników firmowej musi toobecome dostępny z Internetu hello. Aplikacja Hello musi toobe dostępne bezpośrednio przez hello Internet zarówno przez partnerów biznesowych za pomocą firmowej tożsamości i istniejący użytkownicy firmowej.
3. [Usług AD DS: Windows Server AD DS obsługujący aplikację, która wymaga sieci firmowej toohello łączności wdrażania](#BKMK_HybridExt)
   
    Na przykład aplikacji obsługujących LDAP obsługuje uwierzytelnianie zintegrowane systemu Windows, który używa systemu Windows Server AD DS jako repozytorium dla danych konfiguracji i profil użytkownika jest wdrażana na maszynie wirtualnej platformy Azure. Jest pożądane hello tooleverage aplikacji hello istniejących firmowych systemu Windows Server AD DS i zapewnienia logowania jednokrotnego. Aplikacja Hello nie jest obsługujący oświadczenia.

### <a name="BKMK_CloudOnly"></a>1. Usługi AD DS: Wdrażanie aplikacji obsługujących usługi AD DS z nie jest wymagany dla łączności z siecią firmową
![Tylko w chmurze wdrożenia usług AD DS](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**rysunek 1**

#### <a name="description"></a>Opis
Program SharePoint jest wdrożony na maszynie wirtualnej platformy Azure i aplikacji hello nie ma żadnych zależności zasobów sieci firmowej. Witaj aplikacja wymaga systemu Windows Server AD DS, ale nie *nie* wymagają hello firmowych systemu Windows Server AD DS. Brak protokołu Kerberos lub federacyjnych relacji zaufania są wymagane, ponieważ użytkownicy są własnym udostępnianych za pośrednictwem aplikacji hello do domeny hello systemu Windows Server AD DS, który również jest hostowana w chmurze hello na maszynach wirtualnych Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Zagadnienia dotyczące scenariusza i jak obszarów technologii stosowane toohello scenariusza
* [Topologia sieci](#BKMK_NetworkTopology): tworzenie sieci wirtualnej platformy Azure, bez łączności między lokalizacjami (znanej także jako połączenie lokacja lokacja).
* [Konfiguracja wdrażania kontrolera domeny](#BKMK_DeploymentConfig): Wdrażanie nowego kontrolera domeny w lesie usługi Active Directory systemu Windows Server nowy, jednej domenie. To powinny być wdrażane wraz z serwera DNS systemu Windows hello.
* [Topologia lokacji usługi Active Directory systemu Windows Server](#BKMK_ADSiteTopology): Użyj hello domyślnej witryny Windows Server Active Directory (wszystkim komputerom będzie w nazwa-pierwszej-lokacji).
* [Adresowanie IP i DNS](#BKMK_IPAddressDNS):
  
  * Ustawianie statycznego adresu IP dla hello kontrolera domeny za pomocą polecenia cmdlet Set-AzureStaticVNetIP Azure PowerShell hello.
  * Instalowanie i konfigurowanie serwera DNS z systemem Windows na kontrolerach domeny hello na platformie Azure.
  * Skonfiguruj właściwości sieci wirtualnej hello o nazwie hello i adres IP hello maszynę Wirtualną, która obsługuje hello role serwera DNS i kontrolera domeny.
* [Wykaz globalny](#BKMK_GC): hello pierwszego kontrolera domeny w lesie hello musi być serwerem wykazu globalnego. Dodatkowe kontrolery domeny powinien również być skonfigurowany jako wykazów globalnych, ponieważ w lesie pojedynczej domeny wykazu globalnego hello nie wymaga żadnych dodatkowych działań z hello kontrolera domeny.
* [Rozmieszczenie hello systemu Windows Server AD DS, bazy danych i folderu SYSVOL](#BKMK_PlaceDB): Dodaj tooDCs dysku danych, uruchomione jako maszyny wirtualne platformy Azure w kolejności toostore hello usługi Active Directory systemu Windows Server w bazie danych, dzienników i folderu SYSVOL.
* [Kopia zapasowa i przywracanie](#BKMK_BUR): Określ, gdzie toostore kopii zapasowych stanu systemu. W razie potrzeby dodaj inny dysk toohello maszyny Wirtualnej kontrolera domeny toostore kopie zapasowe danych.

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS: rozszerzenie toohello frontonu aplikacji obsługujących oświadczenia lokalnymi Internet
![Federacja z łączności między lokalizacjami](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**na rysunku 2**

#### <a name="description"></a>Opis
Aplikacji obsługującej oświadczenia, który został pomyślnie wdrożony lokalnymi i używane przez toobecome potrzeb użytkowników firmowej dostępne bezpośrednio z Internetu hello. Aplikacja Hello służy jako sieci web frontonu tooa bazy danych SQL w którym są przechowywane dane. serwery SQL Hello używane przez aplikacji hello znajdują się również hello w sieci firmowej. Dwa systemu Windows Server AD FS STSs i równoważenia obciążenia, zostały wdrożone lokalnymi tooprovide dostępu toohello użytkownikom. Aplikacja Hello teraz musi toobe ponadto dostępne bezpośrednio przez hello Internet zarówno przez partnerów biznesowych za pomocą firmowej tożsamości i istniejący użytkownicy firmowej.

Toosimplify nakładu pracy i potrzeb wdrażania i konfigurowania hello spełniają to wymaganie nowe, zostanie podjęta decyzja dwa dodatkowe web frontends i dwa serwery proxy w systemie Windows Server AD FS można zainstalować na maszynach wirtualnych platformy Azure. Wszystkie cztery maszyny wirtualne będą widoczne bezpośrednio toohello Internet i będzie świadczona w sieci lokalnej toohello połączenie przy użyciu sieci VPN lokacja lokacja sieci wirtualnej platformy Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Zagadnienia dotyczące scenariusza i jak obszarów technologii stosowane toohello scenariusza
* [Topologia sieci](#BKMK_NetworkTopology): tworzenie sieci wirtualnej platformy Azure i [skonfigurowania łączności między lokalizacjami](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Dla każdego hello certyfikatów systemu Windows Server AD FS Sprawdź, czy hello adres URL zdefiniowany w szablonie certyfikatu hello i certyfikatów wynikowych hello jest osiągalna wystąpień hello systemu Windows Server AD FS działających na platformie Azure. Może to wymagać tooparts łączności między lokalizacjami infrastruktury PKI. Na przykład, jeśli punkt końcowy hello listy CRL jest oparte na protokole LDAP i hostowanej wyłącznie lokalnej, a następnie łączności między lokalizacjami będzie wymagane. Jeśli nie jest to pożądane, może być konieczne toouse certyfikatów wystawianych przez urząd certyfikacji, którego listy CRL jest dostępny za pośrednictwem Internetu hello.
  > 
  > 
* [Konfiguracji usługi w chmurze](#BKMK_CloudSvcConfig): Upewnij się, masz dwie usługi w chmurze w kolejności dwie wirtualne adresy IP z równoważeniem obciążenia. wirtualny adres IP usługi chmury pierwszy Hello będzie ukierunkowanej toohello dwóch proxy systemu Windows Server AD FS maszyn wirtualnych na porty 80 i 443. Hello systemu Windows Server AD FS serwer proxy maszyn wirtualnych zostanie skonfigurowany adres IP toohello toopoint hello lokalnymi równoważenia obciążenia, czy Zeskanowano hello systemu Windows Server AD FS STSs. wirtualny adres IP usługi chmury drugi Hello będzie ukierunkowanej toohello dwa uruchomionych maszyn wirtualnych frontonu sieci web hello ponownie na porty 80 i 443. Konfigurowanie niestandardowych sondowania tooensure hello równoważenia obciążenia, tylko kieruje ruch toofunctioning systemu Windows Server AD FS serwera proxy i sieci web frontonu maszyn wirtualnych.
* [Konfiguracja serwera federacyjnego](#BKMK_FedSrvConfig): Konfigurowanie systemu Windows Server AD FS bezpieczeństwa toogenerate (STS) serwera federacyjnego tokeny dla lasu usługi Active Directory systemu Windows Server hello utworzone w chmurze hello. Relacje zaufania dostawcy oświadczeń federacji z różnych partnerów hello, które mają tooaccept tożsamości z i konfigurowanie relacji zaufania jednostek jednostki uzależnionej z hello różne aplikacje, które mają toogenerate tokenów.
  
    W większości przypadków systemu Windows Server AD FS, serwery proxy są wdrażane w charakterze internetowy ze względów bezpieczeństwa podczas ich odpowiedniki systemu Windows Server AD FS federation pozostać odizolowane od bezpośrednie połączenie z Internetem. Niezależnie od scenariusza wdrożenia należy skonfigurować usługi w chmurze z wirtualnym adresem IP, które będzie dostarczać publicznie dostępnego adresu IP i port, który jest możliwe saldo tooload między z dwóch wystąpień systemu Windows Server AD FS STS albo wystąpień serwera proxy.
* [Konfiguracja wysokiej dostępności systemu Windows Server AD FS](#BKMK_ADFSHighAvail): jest wskazane toodeploy farmy programu Windows Server AD FS przy użyciu co najmniej dwóch serwerów w tryb failover i równoważenia obciążenia. Może być tooconsider przy użyciu hello wewnętrznej bazy danych systemu Windows (WID) dla danych konfiguracji systemu Windows Server AD FS, a użyć hello wewnętrzne Równoważenie obciążenia możliwości Azure toodistribute przychodzących żądań w hello serwerów w farmie hello.

Aby uzyskać więcej informacji, zobacz hello [przewodniku wdrażania usług AD DS](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. Usług AD DS: Windows Server AD DS obsługujący aplikację, która wymaga sieci firmowej toohello łączności wdrażania
![Wdrażanie usług AD DS między lokalizacjami](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**rysunek 3**

#### <a name="description"></a>Opis
Aplikacja obsługująca LDAP jest wdrożony na maszynie wirtualnej platformy Azure. Obsługuje uwierzytelnianie zintegrowane systemu Windows, a używa systemu Windows Server AD DS jako repozytorium dla danych profilu konfiguracji i użytkownika. Celem Hello hello tooleverage aplikacji hello istniejących firmowych systemu Windows Server AD DS i udostępniać rejestracji jednokrotnej. Aplikacja Hello nie jest obsługujący oświadczenia. Użytkownicy muszą również aplikacji hello tooaccess bezpośrednio z hello Internet. toooptimize wydajności i kosztów zdecydowano, że dwa kontrolery domeny dodatkowe, które są częścią domeny firmowej hello można wdrożyć obok aplikacji hello na platformie Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Zagadnienia dotyczące scenariusza i jak obszarów technologii stosowane toohello scenariusza
* [Topologia sieci](#BKMK_NetworkTopology): tworzenie sieci wirtualnej platformy Azure z [łączności między lokalizacjami](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Metoda instalacji](#BKMK_InstallMethod): wdrażania replik kontrolerów domeny, z hello firmowej domeny usługi Active Directory systemu Windows Server. Dla repliki kontrolera domeny systemu Windows Server AD DS można zainstalować na powitania maszyny Wirtualnej, i opcjonalnie Użyj hello instalacji z nośnika (IFM) funkcja tooreduce hello ilość danych wymaga toobe zreplikowane toohello nowego kontrolera domeny podczas instalacji. Samouczek, zobacz [Instalowanie repliki kontrolera domeny usługi Active Directory na platformie Azure](active-directory-install-replica-active-directory-domain-controller.md). Nawet jeśli używasz IFM może być bardziej efektywne hello toobuild lokalnego wirtualnego kontrolera domeny i Przenieś hello cały wirtualny dysk twardy (VHD) toohello chmurze zamiast replikować podczas instalacji systemu Windows Server AD DS. Dla bezpieczeństwa zalecane jest, Usuń hello wirtualnego dysku twardego z sieci lokalne powitania po został skopiowany tooAzure.
* [Topologia lokacji usługi Active Directory systemu Windows Server](#BKMK_ADSiteTopology): Utwórz nową witrynę Azure Lokacje usługi Active Directory i usług. Utwórz Windows Server Active Directory podsieci obiektu toorepresent hello sieci wirtualnej platformy Azure i Dodaj hello podsieci toohello lokacji. Utwórz nowy link lokacji, zawierający nową witrynę Azure hello i hello lokacji, w których hello sieci wirtualnej platformy Azure punktu końcowego sieci VPN znajduje się w kolejności toocontrol oraz zoptymalizować tooand ruchu usługi Active Directory systemu Windows Server z platformy Azure.
* [Adresowanie IP i DNS](#BKMK_IPAddressDNS):
  
  * Ustawianie statycznego adresu IP dla hello kontrolera domeny za pomocą polecenia cmdlet Set-AzureStaticVNetIP Azure PowerShell hello.
  * Instalowanie i konfigurowanie serwera DNS z systemem Windows na kontrolerach domeny hello na platformie Azure.
  * Skonfiguruj właściwości sieci wirtualnej hello o nazwie hello i adres IP hello maszynę Wirtualną, która obsługuje hello role serwera DNS i kontrolera domeny.
* [Rozproszona geograficznie kontrolery domeny](#BKMK_DistributedDCs): odpowiednio skonfigurować dodatkowe sieci wirtualnych. Jeśli topologii lokacji usługi Active Directory wymaga kontrolerów domeny w lokalizacji geograficznych, które odpowiadają toodifferent Azure regionach, niż mają odpowiednio toocreate lokacji usługi Active Directory.
* [Kontrolery domeny tylko do odczytu](#BKMK_RODC): demonstrujący wdrażanie kontrolera RODC w hello Azure lokacji, w zależności od wymagań do wykonywania operacji przed hello kontrolera domeny i hello zgodność aplikacji i usług zapisu w witrynie hello z kontrolera RODC. Aby uzyskać więcej informacji na temat zgodności aplikacji, zobacz hello [Podręcznik zgodności aplikacji kontrolerów domeny tylko do odczytu](https://technet.microsoft.com/library/cc755190).
* [Wykaz globalny](#BKMK_GC): wykazów globalnych są potrzebne tooservice żądań logowania w wielu domenach lasach. Jeśli wykaz Globalny w hello Azure lokacji nie są wdrażane, będą naliczane koszty ruch wychodzący, ponieważ żądania uwierzytelniania spowodować GC zapytań w innych lokacjach. toominimize, że ruch, można włączyć członkostwa grup uniwersalnych buforowanie hello Azure lokacji w usługach i lokacje usługi Active Directory.
  
    W przypadku wdrożenia wykazu Globalnego, Konfigurowanie łączy lokacji i kosztów linków lokacji, dzięki czemu nie jest preferowany jako źródłowego kontrolera domeny przez inne wykazów globalnych, które wymagają tooreplicate GC hello w hello usługi Azure site hello tej samej partycji domeny częściowej.
* [Rozmieszczenie hello systemu Windows Server AD DS, bazy danych i folderu SYSVOL](#BKMK_PlaceDB): Dodaj tooDCs dysku danych, działające na maszynach wirtualnych Azure w kolejności toostore hello usługi Active Directory systemu Windows Server w bazie danych, dzienników i folderu SYSVOL.
* [Kopia zapasowa i przywracanie](#BKMK_BUR): Określ, gdzie toostore kopii zapasowych stanu systemu. W razie potrzeby dodaj inny dysk toohello maszyny Wirtualnej kontrolera domeny toostore kopie zapasowe danych.

## <a name="deployment-decisions-and-factors"></a>Decyzji dotyczących wdrożenia i czynniki
Ta tabela zawiera podsumowanie hello obszarów technologii usługi Active Directory systemu Windows Server, które są w pełni funkcjonalne w hello poprzedzających scenariuszy i hello odpowiedniego tooconsider decyzji, o szczegółach toomore łącza poniżej. Niektóre obszary technologii mogą nie być odpowiednie tooevery scenariusz wdrażania, a niektóre obszarów technologii może być ważniejsze scenariusz wdrażania tooa niż innych obszarów technologii.

Na przykład jeśli wdrożysz repliki kontrolera domeny w sieci wirtualnej, a las zawiera pojedynczą domenę, wybierając toodeploy serwera wykazu globalnego w takim przypadku nie będą krytyczne toohello scenariusz wdrażania ponieważ dodatkowe replikacja nie zostanie utworzony wymagania. Na hello drugiej strony, jeśli las hello ma wiele domen, a następnie toodeploy decyzji hello wykazu globalnego w sieci wirtualnej mogą mieć wpływ na przepustowość, wydajność, uwierzytelnianie, wyszukiwanie w katalogu macierzystym i tak dalej.

| Obszar technologii usługi Active Directory systemu Windows Server | Decyzje | Czynniki |
| --- | --- | --- |
| [Topologia sieci](#BKMK_NetworkTopology) |Czy można utworzyć sieć wirtualną? |<li>Wymagania dotyczące tooaccess Corp zasobów</li> <li>Authentication</li> <li>Zarządzanie kontami</li> |
| [Konfiguracja wdrażania kontrolera domeny](#BKMK_DeploymentConfig) |<li>Wdrażanie oddzielnego lasu bez żadnych relacji zaufania?</li> <li>Wdrażanie nowego lasu z Federacją?</li> <li>Wdrażanie nowego lasu z zaufaniem lasu usługi Active Directory systemu Windows Server lub Kerberos?</li> <li>Rozszerz las Corp, wdrażając repliki kontrolera domeny?</li> <li>Rozszerz las Corp przez wdrożenie nowej domeny podrzędnej lub drzewa domen?</li> |<li>Bezpieczeństwo</li> <li>Zgodność</li> <li>Koszty</li> <li>Odporność i odporność na uszkodzenia</li> <li>Zgodność aplikacji</li> |
| [Topologia lokacji usługi Active Directory systemu Windows Server](#BKMK_ADSiteTopology) |Jak skonfigurować podsieci, lokacji i łączy lokacji z ruchem toooptimize sieci wirtualnej platformy Azure i minimalizuje koszt |<li>Definicje podsieci i lokacji</li> <li>Witryny sieci Web łącza i powiadomienie o zmianie</li> <li>Kompresja replikacji</li> |
| [Adresowanie IP i DNS](#BKMK_IPAddressDNS) |Jak adresy tooconfigure IP i rozpoznawanie nazw? |<li>Użyj hello Użyj hello AzureStaticVNetIP zestaw polecenia cmdlet tooassign statycznego adresu IP</li> <li>Instalowanie serwera DNS systemu Windows Server i skonfigurować właściwości sieci wirtualnej hello o nazwie hello i adres IP maszyny Wirtualnej, który jest hostem ról serwera DNS i kontrolera domeny hello hello</li> |
| [Rozproszona geograficznie kontrolerów domeny](#BKMK_DistributedDCs) |Jak tooDCs tooreplicate na osobne sieci wirtualnej? |Jeśli topologii lokacji usługi Active Directory wymaga kontrolerów domeny w lokalizacji geograficznych, które odpowiadają toodifferent Azure regionach, niż mają odpowiednio toocreate lokacji usługi Active Directory. [Skonfiguruj sieć wirtualną sieć toovirtual łączności](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate między kontrolerami domeny w różnych sieciach wirtualnych. |
| [Kontrolery domeny tylko do odczytu](#BKMK_RODC) |Użyj kontrolerów domeny tylko do odczytu lub zapisu? |<li>Filtrowanie atrybutów o dużym znaczeniu Biznesowym/dane osobowe</li> <li>Klucze tajne filtru</li> <li>Limit ruchu wychodzącego</li> |
| [Wykaz globalny](#BKMK_GC) |Zainstaluj wykazu globalnego? |<li>Dla jednej domeny lasu należy wszystkie kontrolery domeny wykazów globalnych</li> <li>Dla lasu o wielu domenach wykazów globalnych są wymagane do uwierzytelniania</li> |
| [Metody instalacji](#BKMK_InstallMethod) |Jak tooinstall kontrolera domeny na platformie Azure? |Albo: <li>Instalacja usług AD DS za pomocą środowiska Windows PowerShell lub narzędzia Dcpromo</li> <li>Przenieś wirtualny dysk twardy wirtualnego kontrolera domeny lokalnej</li> |
| [Rozmieszczenie hello systemu Windows Server AD DS, bazy danych i folderu SYSVOL](#BKMK_PlaceDB) |W przypadku, gdy toostore systemu Windows Server AD DS, bazy danych, dzienników i folderu SYSVOL? |Zmień wartości domyślne Dcpromo.exe. Te krytycznych plików usługi Active Directory *musi* można umieścić na dyskach danych Azure zamiast dysków systemu operacyjnego, które implementuje buforowanie zapisu. |
| [Tworzenie kopii zapasowej i przywracanie](#BKMK_BUR) |Jak toosafeguard i odzyskiwanie danych? |Utwórz kopie zapasowe stanu systemu |
| [Konfiguracja serwera federacyjnego](#BKMK_FedSrvConfig) |<li>Wdrażanie nowego lasu z Federacją w chmurze hello?</li> <li>Wdrażanie usług AD FS lokalnej i ujawnia serwera proxy w chmurze hello?</li> |<li>Bezpieczeństwo</li> <li>Zgodność</li> <li>Koszty</li> <li>Tooapplications dostępu przez partnerów biznesowych</li> |
| [Konfiguracji usługi w chmurze](#BKMK_CloudSvcConfig) |Usługi w chmurze jest niejawnie wdrożone hello Utwórz maszynę wirtualną po raz pierwszy. Potrzebujesz usługi w chmurze dodatkowe toodeploy? |<li>Maszyna wirtualna lub maszyn wirtualnych wymaga bezpośredniego ujawnienia toohello Internet?</li> <li> Usługa hello wymaga równoważenia obciążenia?</li> |
| [Wymagania dotyczące serwera federacyjnego publicznego i prywatnego adresu IP, adresów (dynamicznego adresu IP i wirtualnego adresu IP)](#BKMK_FedReqVIPDIP) |<li>Wystąpienie hello systemu Windows Server AD FS jest konieczne toobe bezpośrednio z Internetu hello dostępu?</li> <li>Aplikacja hello wdrażane w chmurze hello wymaga własnego internetowy adres i port?</li> |Utwórz jedną usługę chmury dla każdego wirtualnego adresu IP, który jest wymagany przez wdrożenie |
| [Konfiguracja wysokiej dostępności systemu Windows Server AD FS](#BKMK_ADFSHighAvail) |<li>Liczbę węzłów w mojej farmie serwerów systemu Windows Server AD FS?</li> <li>Ile toodeploy węzłów w farmie serwerów proxy Moje systemu Windows Server AD FS?</li> |Odporność i odporność na uszkodzenia |

### <a name="BKMK_NetworkTopology"></a>Topologia sieci
Spójności adresów IP hello toomeet kolejności i wymagania systemu DNS dla systemu Windows Server AD DS, należy utworzyć toofirst [sieci wirtualnej platformy Azure](../virtual-network/virtual-networks-overview.md) i Dołącz tooit sieci maszyn wirtualnych. Podczas jego tworzenia, należy zdecydować, czy toooptionally rozszerzyć łączności tooyour lokalnymi firmowej sieci, co niewidocznie łączy wirtualnej platformy Azure maszyny lokalne tooon maszyny — jest to osiągane przy użyciu tradycyjnych technologii sieci VPN i wymaga się, że punkt końcowy sieci VPN można narażony na krawędzi sieci firmowej hello hello. Oznacza to hello sieci VPN jest inicjowane z sieci firmowej Azure toohello, nie odwrotnie.

Należy pamiętać, że dodatkowe opłaty podczas rozszerzania sieci wirtualnej sieci lokalnej tooyour poza hello standardowe opłaty, które są stosowane tooeach maszyny Wirtualnej. W szczególności są opłaty za czas procesora CPU hello bramy sieci wirtualnej platformy Azure i hello ruch wychodzący ruch generowany przez każdego maszynę Wirtualną, która komunikuje się z lokalnymi maszynami w hello sieci VPN. Aby uzyskać więcej informacji na temat opłat ruchu sieciowego, zobacz [Azure, w skrócie cennik](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Konfiguracja wdrażania kontrolera domeny
sposób Hello, skonfiguruj powitalne kontrolera domeny zależy od wymagań hello hello usługi można mają toorun na platformie Azure. Na przykład można wdrożyć nowy las, odizolowanych od firmy lasu, do testowania, weryfikacja koncepcji, jest nowa aplikacja lub innych projektów w krótkim czasie, który wymaga usług katalogowych, ale zasobów firmowych toointernal nie określonym dostępu.

Jako korzyści izolowanego lasu, który kontroler domeny nie jest replikowany z lokalnymi kontrolerów domeny, co powoduje mniej wychodzącego ruchu sieciowego generowany przez system hello, bezpośrednio zmniejszenie kosztów. Aby uzyskać więcej informacji na temat opłat ruchu sieciowego, zobacz [Azure, w skrócie cennik](http://azure.microsoft.com/pricing/).

Inny przykład załóżmy, że masz wymagania ochrony prywatności dla usługi, ale usługa hello jest zależna od tooyour dostępu wewnętrznego systemu Windows Server Active Directory. Jeśli dane toohost hello usługi w chmurze hello są dozwolone, można wdrożyć nową domenę podrzędną lasu wewnętrznego, na platformie Azure. W takim przypadku można wdrożyć kontrolera domeny dla hello nowej domeny podrzędnej (bez hello wykazu globalnego w kolejności toohelp adres prywatności). Ten scenariusz, wraz z wdrożenia kontrolera domeny repliki wymaga sieci wirtualnej dla łączności z kontrolerów domeny z lokalnymi.

Jeśli tworzysz nowy las, wybierz czy toouse [relacje zaufania usługi Active Directory](https://technet.microsoft.com/library/cc771397) lub [relacje zaufania federacji](https://technet.microsoft.com/library/dd807036). Wymagania hello saldo ustawieniem zgodności, zabezpieczeń, zgodności, koszt i elastyczność. Na przykład tootake zaletą [uwierzytelnianie selektywne](https://technet.microsoft.com/library/cc755844) może wybrać toodeploy nowy las na platformie Azure i utworzyć relację zaufania usługi Active Directory systemu Windows Server między hello lokalnego lasu i hello chmury lasu. Jeśli aplikacja hello jest obsługujący oświadczenia, jednak można wdrożyć relacje zaufania federacji, zamiast relacji zaufania lasów usługi Active Directory. Innym czynnikiem będą się, że hello koszt replikowania tooeither większej ilości danych dzięki rozszerzeniu lokalnej usługi Active Directory systemu Windows Server toohello chmury lub generować bardziej wychodzący ruch wyniku uwierzytelniania i obciążenia zapytania.

Wymagania dotyczące dostępności i odporności na uszkodzenia wpłynąć na wybór. Na przykład jeśli zostanie przerwany hello link, aplikacje wykorzystaniu zaufania Kerberos lub relacji zaufania federacji wszystkie prawdopodobnie całkowicie nie działają, chyba że wdrożono wystarczające infrastruktury na platformie Azure. Konfiguracje wdrożenia alternatywne, takie jak replik kontrolerów domeny (zapisywalny lub kontrolery RODC) zwiększa prawdopodobieństwo hello jest możliwe tootolerate awarii łącza.

### <a name="BKMK_ADSiteTopology"></a>Topologia lokacji usługi Active Directory systemu Windows Server
Użytkownik musi toocorrectly zdefiniuj Lokacje i łączy lokacji w kolejności toooptimize ruchu i ograniczania kosztów. Lokacje, linki lokacji i podsieci wpływa na powitania topologii replikacji między kontrolerów domeny i hello przepływu ruchu uwierzytelniania. Należy wziąć pod uwagę powitania po opłat ruchu, a następnie wdrożyć i skonfigurować kontrolery domeny, zgodnie z wymaganiami toohello danego scenariusza wdrażania:

* Brak nominalnego opłaty za godzinę dla bramy hello:
  
  * Można uruchomić i zatrzymać zgodnie z własnymi potrzebami
  * Jeśli zatrzymana, maszynach wirtualnych platformy Azure są odizolowane od sieci firmowej hello
* Ruch przychodzący jest bezpłatna
* Ruch wychodzący jest rozliczana zgodnie z zbyt[Azure, w skrócie cennik](http://azure.microsoft.com/pricing/). Aby zoptymalizować właściwości link lokacji między lokacjami lokalnymi i hello chmury witryn w następujący sposób:
  
  * Jeśli używasz wielu sieci wirtualnych, Konfigurowanie łączy lokacji hello i kosztów odpowiednio tooprevent systemu Windows Server AD DS z priorytetyzowanie hello Azure lokacji do jednego, która może zapewnić hello te same poziomy usług bez dodatkowych opłat. Można także rozważyć wyłączenie Mostek hello wszystkie lokacji (BASL) link — opcja (która jest domyślnie włączona). Daje to pewność, że tylko bezpośrednio połączone lokacje replikują między sobą. Kontrolery domeny w sposób przechodni podłączonej lokacji nie będą mogli tooreplicate bezpośrednio ze sobą, ale musi zostać zreplikowana za pośrednictwem wspólnego lokacji lub lokacji. Jeśli hello pośredniczące witryn stać się niedostępne z jakiegoś powodu nie odbywa się replikacja między kontrolerów domeny w sposób przechodni podłączonej lokacji nawet jeśli dostępny jest łączność między lokacjami hello. Na koniec w przypadku, gdy sekcje zachowania w ramach replikacji przechodniej pozostają pożądane, Utwórz witrynę mostków, zawierających hello odpowiednich linków i witryn, takich jak lokalnie, witryn sieci firmowej.
  * [Konfigurowanie kosztów linków lokacji](https://technet.microsoft.com/library/cc794882) odpowiednio tooavoid niezamierzone ruchu. Na przykład jeśli **spróbuj dalej najbliższej lokacji** jest włączona, upewnij się, że sieć wirtualna hello Lokacje nie są następnie hello najbliższego przez odpowiednie zwiększenie kosztów hello skojarzonego obiektu łącza lokacji hello, który łączy toohello wstecz hello usługi Azure site Sieć firmowa.
  * Skonfiguruj lokacja [interwałów](https://technet.microsoft.com/library/cc794878) i [harmonogramy](https://technet.microsoft.com/library/cc816906) zgodnie z tooconsistency wymagania i szybkość zmian obiektu. Wyrównuje harmonogram replikacji z tolerancja opóźnienia. Kontrolery domeny są replikowane tylko hello ostatni stan wartości, tak malejącej interwał replikacji hello zmniejszyć koszty, jeśli brak wystarczającej ilości zmiany obiektu.
* W przypadku minimalizowania kosztów priorytet, upewnij się, replikacja jest zaplanowana i powiadomienia o zmianie nie jest włączona. Podczas replikacji między lokacjami jest hello domyślna konfiguracja. Nie jest to istotne, jeśli są wdrażania kontrolera RODC w sieci wirtualnej, ponieważ hello kontrolera RODC nie będą replikowane na wszystkie zmiany ruchu wychodzącego. Jednak w przypadku wdrożenia zapisywalnego kontrolera domeny, należy upewnij się, że hello lokacja nie jest skonfigurowany tooreplicate aktualizacje z częstotliwością niepotrzebne. W przypadku wdrożenia serwera wykazu globalnego (GC), upewnij się, że każdej lokacji, który zawiera wykaz Globalny replikuje partycji domeny ze źródłowego kontrolera domeny w lokacji, która jest połączona z łącza lokacji lub łącza lokacji, które mają niższe koszty niż hello GC w hello usługi Azure site.
* Możliwe jest toofurther nadal zmniejszenie ruchu w sieci generowane przez funkcję replikacji między lokacjami, zmieniając algorytmu kompresji hello replikacji. algorytm kompresji Hello jest kontrolowana przez algorytm kompresji HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator wpis rejestru REG_DWORD hello. Wartość domyślna Hello to 3, które są powiązane z toohello Kompresuj Xpress algorytmu. Możesz zmienić too2 wartość hello, jakie zmiany hello tooMSZip algorytmu. W większości przypadków spowoduje to zwiększenie kompresji hello, ale pod wydatków hello użycia procesora CPU. Aby uzyskać więcej informacji, zobacz [działa topologia replikacji jak Active Directory](https://technet.microsoft.com/library/cc755994).

### <a name="BKMK_IPAddressDNS"></a>Adresowanie IP i DNS
Maszyny wirtualne platformy Azure są przydzielane "dzierżawy DHCP adresy" domyślnie. Ponieważ dynamicznych adresów sieci wirtualnej platformy Azure będą się powtarzać z maszyną wirtualną dla okresu istnienia hello hello maszyny wirtualnej, są spełnione wymagania hello systemu Windows Server AD DS.

W związku z tym użycie adresu dynamicznego na platformie Azure, możesz obowiązują za pomocą statycznego adresu IP, ponieważ podlega routingowi hello okres dzierżawy hello i hello okres dzierżawy hello jest równy toohello istnienia hello usługi w chmurze.

Jednak hello dynamicznego adresu cofnięciu przydziału Jeśli hello maszyna wirtualna jest zamknięta. tooprevent hello adresu IP z cofana, możesz [tooassign AzureStaticVNetIP zestawu statycznego adresu IP użyj](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Rozpoznawanie nazw, wdrażać własne (lub Wykorzystaj istniejące) infrastrukturze serwera DNS; DNS platformy Azure nie spełnia hello zaawansowanych potrzeb rozpoznawania nazwy systemu Windows Server AD DS. Na przykład go nie obsługuje dynamicznych rekordów SRV i tak dalej. Rozpoznawanie nazw jest element konfiguracji krytyczne dla kontrolerów domeny oraz klientów przyłączonych do domeny. Kontrolery domeny musi istnieć możliwość rejestrowania rekordów zasobów i rozwiązywania rekordów zasobów innego kontrolera domeny.
Ze względów odporność na uszkodzenia i wydajności jest usługa DNS systemu Windows Server hello optymalne tooinstall na powitania kontrolerów domeny działających na platformie Azure. Następnie skonfiguruj hello właściwości sieci wirtualnej platformy Azure o nazwie hello i adres IP serwera DNS hello. Po uruchomieniu innych maszyn wirtualnych w sieci wirtualnej hello, ustawień programu rozpoznawania nazw DNS klienta zostaną skonfigurowane serwer DNS jako część hello dynamiczne przydzielanie adresów IP.

> [!NOTE]
> Nie można przyłączyć domeny usługi Active Directory systemu Windows Server AD DS tooa komputerów lokalnych, hostowanej na platformie Azure bezpośrednio przez hello Internet. Witaj wymagania dotyczące portów usługi Active Directory i operacji przyłączania do domeny hello renderować ją niepraktyczne toodirectly Uwidacznianie hello niezbędne porty i w rezultacie cały toohello DC Internet.
> 
> 

Maszyny wirtualne zarejestrować nazwy DNS automatycznie podczas uruchamiania lub zmiany nazwy.

Aby uzyskać więcej informacji na temat w tym przykładzie i inny przykład pokazujący sposób tooprovision hello pierwsza maszyna wirtualna i zainstalowania usług AD DS na nim, zobacz [zainstalować nowy las usługi Active Directory w systemie Microsoft Azure](active-directory-new-forest-virtual-machine.md). Aby uzyskać więcej informacji o korzystaniu z programu Windows PowerShell, zobacz [instalacji programu Azure PowerShell](/powershell/azureps-cmdlets-docs) i [poleceń cmdlet do zarządzania Azure](/powershell/module/azurerm.compute/#virtual_machines).

### <a name="BKMK_DistributedDCs"></a>Rozproszona geograficznie kontrolerów domeny
Azure zalety odnośnie do hostowania wielu kontrolerów domeny w różnych sieciach wirtualnych:

* Obejmujący wiele lokacji odporności na uszkodzenia
* Oddziałów toobranch fizycznej bliskości (mniejsze opóźnienia)

Aby uzyskać informacje o konfigurowaniu bezpośrednia komunikacja między sieciami wirtualnymi, zobacz [skonfigurować łączność sieciową toovirtual sieci wirtualnej](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Kontrolery domeny tylko do odczytu
Należy toochoose czy toodeploy odczytu — tylko lub zapisywalne kontrolery domeny. Może być odchylona toodeploy kontrolerów RODC, ponieważ nie ma fizyczną kontrolę nad nimi, ale kontrolery RODC są zaprojektowane toobe wdrażane w lokalizacjach, gdzie ich zabezpieczeń fizycznych jest zagrożone, takich jak biur oddziałów.

Azure nie stanowią hello fizycznych zagrożenie dla bezpieczeństwa oddziału firmy, ale kontrolery RODC może nadal potwierdzenia toobe bardziej ekonomiczne ponieważ hello funkcje, które zapewniają są odpowiednie toothese środowisk, choć bardzo różnych powodów. Na przykład kontrolery RODC nie ma żadnych replikację wychodzącą i są w stanie tooselectively wypełnić klucze tajne (hasła). Na powitania wadą interfejsu, brak hello tych kluczy tajnych może wymagać toovalidate ruch wychodzący na żądanie ich jako uwierzytelnia użytkownika lub komputera. Ale kluczy tajnych można selektywnie wstępnie i pamięci podręcznej.

Kontrolery RODC zapewniają dodatkowe korzyści i w jego pobliżu problemów o dużym znaczeniu Biznesowym, a dane osobowe, ponieważ można dodać zestawu atrybutów (FAS) filtrowane atrybutów, które zawierają dane poufne toohello kontrolera RODC. Hello FAS to dostosowywalne zestaw atrybutów, które nie są replikowane tooRODCs. W przypadku, gdy nie są dozwolone lub nie ma toostore dane osobowe lub o dużym znaczeniu Biznesowym na platformie Azure, można użyć hello FAS ze względów bezpieczeństwa. Aby uzyskać więcej informacji zobacz [kontrolera RODC filtrowane atrybutu [(https://technet.microsoft.com/library/cc753459)].

Upewnij się, że aplikacje będą zgodne z kontrolera RODC ma toouse. Wiele aplikacji z obsługą usługi Active Directory systemu Windows Server działają prawidłowo w przypadku kontrolera RODC, ale niektóre aplikacje można wykonać Niewydajne lub się nie powieść, jeśli nie mają dostępu tooa zapisywalnego kontrolera domeny. Aby uzyskać więcej informacji, zobacz [Podręcznik zgodności aplikacji kontrolerów domeny tylko do odczytu](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Wykaz globalny
Określa, czy należy toochoose tooinstall wykazu globalnego (GC). W lesie pojedynczej domeny wszystkie kontrolery domeny należy skonfigurować jako serwerów wykazu globalnego. Nie zwiększa kosztów ponieważ nie będzie żadnych dodatkowych replikacją.

W przypadku lasu o wielu domenach wykazów globalnych są członkostwa grup uniwersalnych tooexpand niezbędne podczas procesu uwierzytelniania hello. Jeśli wykaz Globalny nie należy wdrażać, obciążenia w sieci wirtualnej hello, które uwierzytelniania kontrolera domeny na platformie Azure pośrednio wygeneruje tooquery ruchu wychodzącego uwierzytelniania GC lokalnymi podczas każdej próby uwierzytelnienia.

Hello kosztów związanych z wykazów globalnych są mniej przewidywalne, ponieważ one hostów w każdej domenie (w ramach). Jeśli obciążenie hello obsługuje usługę internetowy i uwierzytelnia użytkowników w systemie Windows Server AD DS, kosztów hello można całkowicie nieprzewidywalne. toohelp zmniejszyć zapytania GC poza hello chmury lokacji podczas uwierzytelniania, możesz [Włącz buforowanie członkostwa grup uniwersalnych](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Metody instalacji
Jak należy toochoose tooinstall hello kontrolerów domeny w sieci wirtualnej hello:

* Podwyższ poziom nowych kontrolerów domeny. Aby uzyskać więcej informacji, zobacz [zainstalować nowy las usługi Active Directory w sieci wirtualnej platformy Azure](active-directory-new-forest-virtual-machine.md).
* Przenieś hello wirtualnego dysku twardego lokalnego wirtualnego kontrolera domeny toohello chmury. W takim przypadku musi zapewnić tym hello lokalnego wirtualnego kontrolera domeny "przeniesienia" nie "skopiowanych" lub "Sklonowany".

Użyj tylko Azure maszyn wirtualnych kontrolerów domeny (jako min. tooAzure "web" lub "pracownik" Rola maszyn wirtualnych). Są trwałe i trwałość stanu na Kontrolerze domeny jest wymagany. Maszyny wirtualne platformy Azure są przeznaczone dla obciążeń, takich jak kontrolerów domeny.

Użyj narzędzia SYSPREP toodeploy lub nie klonowania kontrolerów domeny. tooclone możliwości Hello kontrolerów domeny jest dostępna tylko w systemach w systemie Windows Server 2012. Witaj w klonowania funkcji wymaga obsługi VMGenerationID w hello podstawowych funkcji hypervisor. Funkcji Hyper-V w systemie Windows Server 2012 i Azure sieciach wirtualnych zarówno VMGenerationID, podobnie jak obsługują dostawców oprogramowania wirtualizacji innej firmy.

### <a name="BKMK_PlaceDB"></a>Rozmieszczenie hello systemu Windows Server AD DS, bazy danych i folderu SYSVOL
Wybierz, w którym toolocate hello bazy danych systemu Windows Server AD DS, dzienników i folderu SYSVOL. Muszą one wdrożone na dyskach danych Azure.

> [!NOTE]
> Azure dyski danych są ograniczone too1 TB.
> 
> 

Domyślnie stacji dysków danych wykonać nie pamięci podręcznej zapisu. Stacjach dysków, które są dołączone tooa maszyny Wirtualnej użyj zapisu do buforowania. Zapisem sprawia, że buforowanie się, że zapisu hello jest toodurable zatwierdzić magazynu platformy Azure przed zakończeniem z punktu widzenia hello systemu operacyjnego hello wirtualna hello transakcji. Zapewnia trwałość na powitania koszt wolniejsze zapisów.

Jest to ważne w przypadku systemu Windows Server AD DS, ponieważ dysk buforowanie zapisu unieważnia założeń przyjmowanych hello kontrolera domeny. Systemu Windows Server AD DS próbuje toodisable buforowanie zapisu, ale jest toohonor systemu We/Wy dysku toohello go. Buforowanie zapisu toodisable awarii w pewnych okolicznościach, wprowadzenie wycofania numeru USN, co powoduje pokutujące obiekty i inne problemy.

Najlepszym rozwiązaniem dla wirtualnych kontrolerów domeny hello następujące:

* W ustawieniu hello hosta preferencji pamięci podręcznej na dysku danych Azure hello = Brak. Zapobiega to problemy z buforowania zapisu dla operacji usług AD DS.
* Przechowywanie hello bazy danych, dzienników i folderu SYSVOL na powitania obu tych samych danych na dysku lub oddzielnych dysków z danymi. Zazwyczaj jest to innym dysku niż hello dysku używanym przez sam system operacyjny hello. takeaway klucza Hello jest hello bazy danych usług AD DS w systemie Windows Server i folderu SYSVOL nie mogą być przechowywane na typ dysku systemu operacyjnego Azure. Domyślnie hello proces instalacji usług AD DS instaluje te składniki w folderze % systemroot %, co nie jest zalecane dla platformy Azure.

### <a name="BKMK_BUR"></a>Kopia zapasowa i przywracanie
Należy pamiętać o co to jest i nie jest obsługiwana dla kopii zapasowej i przywracania kontrolera domeny na ogólnie rzecz biorąc, a w szczególności, systemami na maszynie wirtualnej. Zobacz [kopia zapasowa i przywracanie zagadnienia dotyczące zwirtualizowanych kontrolerów domeny](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Utwórz kopie zapasowe stanu systemu, używając tylko oprogramowania kopii zapasowej, w szczególności rozpoznający kopii zapasowej wymagania dotyczące systemu Windows Server AD DS, takie jak Kopia zapasowa systemu Windows Server.

Nie Kopiuj i klonowanie zamiast regularnego wykonywania kopii zapasowych plików VHD kontrolerów domeny. Przywracanie kiedykolwiek należy wymagać, grozi to przy użyciu sklonowane lub skopiowane wirtualne dyski twarde bez systemu Windows Server 2012 i obsługiwanej funkcji hypervisor wprowadzi rozbieżnościach numerów USN.

### <a name="BKMK_FedSrvConfig"></a>Konfiguracja serwera federacyjnego
w części Hello konfiguracji serwerów federacyjnych usług AD FS w systemie Windows Server (STSs) zależy czy hello aplikacje, które mają toodeploy na platformie Azure muszą tooaccess zasobów w sieci lokalnej.

Jeśli aplikacji hello spełniają następujące kryteria hello, można wdrożyć aplikacji hello w izolacji od sieci lokalnej.

* Akceptacji tokenów SAML
* Są one exposable toohello Internet
* Nie uzyskiwania dostępu do zasobów lokalnych

W takim przypadku należy skonfigurować systemu Windows Server AD FS STSs następująco:

1. Konfigurowanie izolowanych lesie na platformie Azure.
2. Zapewnianie dostępu federacyjnego toohello lasu przez skonfigurowanie farmy serwerów federacyjnych systemu Windows Server AD FS.
3. Konfigurowanie systemu Windows Server AD FS (farmy serwerów federacyjnych i federacyjnego serwera proxy farmy) w lesie lokalnym hello.
4. Należy ustanowić relację zaufania federacji między lokalne powitania i Azure wystąpień usług AD FS w systemie Windows Server.

Na hello drugiej strony, jeśli hello aplikacje wymagają dostęp do zasobów lokalnych tooon, użytkownik może skonfigurować systemu Windows Server AD FS z aplikacji hello na platformie Azure w następujący sposób:

1. Skonfiguruj połączenie między lokalnymi sieciami i platformą Azure.
2. Konfigurowanie farmy serwerów federacyjnych systemu Windows Server AD FS w lesie lokalnym hello.
3. Skonfiguruj serwer proxy farmy serwerów federacyjnych usług AD FS w systemie Windows Server na platformie Azure.

Ta konfiguracja ma zaletą hello ograniczenia narażenia hello zasobów lokalnych tooconfiguring podobne systemu Windows Server AD FS z aplikacji w sieci obwodowej.

Należy pamiętać, że w każdym z tych scenariuszy można ustanowić relacji zaufania z więcej dostawców tożsamości, jeśli jest potrzebny współpracy business-to-business.

### <a name="BKMK_CloudSvcConfig"></a>Konfiguracji usługi w chmurze
Usługi w chmurze są niezbędne, jeśli chcesz tooexpose maszyny Wirtualnej bezpośrednio toohello Internet lub tooexpose internetowy równoważeniem obciążenia aplikacji. Jest to możliwe, ponieważ każda usługa w chmurze oferuje pojedynczy można skonfigurować wirtualny adres IP.

### <a name="BKMK_FedReqVIPDIP"></a>Wymagania dotyczące serwera federacyjnego publicznego i prywatnego adresu IP, adresów (dynamicznego adresu IP i wirtualnego adresu IP)
Każda maszyna wirtualna platformy Azure odbiera dynamicznego adresu IP. Dynamiczny adres IP jest prywatny adres dostępny tylko w obrębie platformy Azure. W większości przypadków, będzie konieczne tooconfigure wirtualnego adresu IP dla wdrożeń usług AD FS w systemie Windows Server. Witaj wirtualnego adresu IP jest konieczne tooexpose toohello punktów końcowych usługi AD FS w systemie Windows Server Internet i będzie używany przez federacyjne partnerów i klientów uwierzytelniania i bieżące zarządzanie. Wirtualny adres IP jest właściwością elementu usługi w chmurze, który zawiera co najmniej jednej maszyny wirtualnej Azure. Jeśli hello aplikacji obsługującej oświadczenia wdrożony na platformie Azure i Windows Server AD FS są skierowane do Internetu jak również udziału typowe porty, każda będzie wymagać wirtualnego adresu IP własnych i dlatego będzie konieczne toocreate jednej chmury usługi dla aplikacji hello i drugi dla systemu Windows Server AD FS.

Definicje warunków hello wirtualnego adresu IP i dynamicznego adresu IP, zobacz [terminów i definicje](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Konfiguracja wysokiej dostępności systemu Windows Server AD FS
Mimo że jest usług federacyjnych możliwe toodeploy autonomicznej usługi Windows Server AD FS, jest zalecane toodeploy farmy z co najmniej dwa węzły Zabezpieczającego usług AD FS i serwera proxy dla środowisk produkcyjnych.

Zobacz [zagadnienia dotyczące topologii wdrożenia 2.0 usług AD FS](https://technet.microsoft.com/library/gg982489) w hello [AD FS 2.0 projektowania przewodnik](https://technet.microsoft.com/library/dd807036) toodecide najlepsze opcje konfiguracji wdrożenia własnych potrzeb.

> [!NOTE]
> W programie Równoważenie obciążenia tooget kolejności dla systemu Windows Server AD FS z punktów końcowych na platformie Azure, skonfiguruj wszystkie elementy członkowskie farmy hello systemu Windows Server AD FS w hello sama usługa w chmurze i użyj hello Równoważenie obciążenia możliwości platformy Azure dla protokołu HTTP (domyślnie: 80) i porty HTTPS (domyślnie: 443). Aby uzyskać więcej informacji, zobacz [sondę modułu równoważenia obciążenia Azure](https://msdn.microsoft.com/library/azure/jj151530).
> Windows Server (Równoważenia sieciowego) nie jest obsługiwana na platformie Azure.
> 
> 

