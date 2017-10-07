---
title: "aaaResolution dla maszyn wirtualnych i wystąpień roli"
description: "Nazwy scenariuszy rozwiązania IaaS platformy Azure, rozwiązania hybrydowe między inną chmurę usługi Active Directory i przy użyciu serwera DNS "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Rozpoznawanie nazw dla maszyn wirtualnych i wystąpień roli
W zależności od tego, jak używasz Azure toohost IaaS i PaaS, hybrydowych rozwiązań może być konieczne hello tooallow maszyn wirtualnych i wystąpień roli, utworzyć toocommunicate ze sobą. Tej komunikacji może odbywać się przy użyciu adresów IP, ale jest znacznie prostsza nazwy toouse, które można łatwo zapamiętać i nie należy zmieniać. 

Jeśli wystąpień roli i maszyn wirtualnych hostowanych na platformie Azure wymagane adresów IP toointernal nazwy domeny tooresolve, można użyć jednej z dwóch metod:

* [Rozpoznawanie nazw platformy Azure](#azure-provided-name-resolution)
* [Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) (co może powodować przekazywanie zapytań toohello serwerach DNS platformy Azure) 

Typ Hello rozpoznawania nazw, których używasz, zależy od tego, jak maszyn wirtualnych i wystąpień roli należy toocommunicate ze sobą.

**Witaj poniższej tabeli przedstawiono scenariusze i odpowiedniego rozwiązania rozpoznawania nazwy:**

| **Scenariusz** | **Rozwiązania** | **Sufiks** |
| --- | --- | --- |
| Rozpoznawanie nazw między wystąpień roli lub maszyn wirtualnych znajdujących się w hello sama usługa lub sieci wirtualnej w chmurze |[Rozpoznawanie nazw platformy Azure](#azure-provided-name-resolution) |Nazwa hosta lub nazwa FQDN |
| Rozpoznawanie nazw między wystąpień roli lub maszyn wirtualnych znajdujących się w różnych sieciach wirtualnych |Zarządzany przez klienta DNS serwerów przekazujących zapytań między sieciami wirtualnymi rozpoznanie przez platformę Azure (serwer proxy DNS).  Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Rozpoznawanie nazwy komputerów i usług lokalnych z wystąpień roli lub maszyn wirtualnych na platformie Azure |Zarządzany przez klienta z serwerów DNS (np. lokalnego kontrolera domeny, kontrolera domeny tylko do odczytu lokalnej lub zsynchronizowany przy użyciu transferów stref DNS dodatkowej).  Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Rozpoznawanie nazwy Azure hostów z komputerów lokalnych |Zapytania do przodu tooa zarządzany przez klienta DNS serwera proxy w sieci wirtualnej odpowiedniego hello, serwera proxy hello przekazuje tooAzure zapytania do rozpoznawania. Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Reverse DNS wewnętrznych adresów IP |[Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Nie dotyczy |
| Rozpoznawanie nazw między maszynami wirtualnymi lub wystąpień roli znajduje się w różnych usług w chmurze, nie znajduje się w sieci wirtualnej |Nie dotyczy. Łączność między maszyn wirtualnych i wystąpień roli w innej chmurze usługi nie jest obsługiwana poza siecią wirtualną. |Nie dotyczy |

## <a name="azure-provided-name-resolution"></a>Rozpoznawanie nazw platformy Azure
Wraz z rozpoznawanie publicznej nazwy DNS platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień ról, które znajdują się w obrębie hello wirtualnego tej samej sieci lub w chmurze usługi.  Maszyny wirtualne/wystąpienia w usłudze w chmurze korzystają hello DNS tego samego sufiks (Aby samodzielnie hostname hello jest wystarczająca), ale klasycznych sieci wirtualnych różnych usług w chmurze ma inne sufiksy DNS, więc hello nazwy FQDN jest wymagane tooresolve nazw między usługami inną chmurę.  W sieci wirtualne w modelu wdrażania usługi Resource Manager hello hello sufiks DNS jest spójne w ramach sieci wirtualnej hello (więc hello FQDN nie jest potrzebny) i tooboth karty sieciowe i maszyn wirtualnych można przypisać nazwy DNS. Mimo że rozpoznawanie nazw platformy Azure nie wymaga żadnej konfiguracji, nie jest hello wybór odpowiedniego dla wszystkich scenariuszy wdrożenia w powyższej tabeli hello.

> [!NOTE]
> W przypadku hello role sieci web i proces roboczy można także przejść hello adresów IP wystąpień roli oparte na powitania roli nazwę i numer wystąpienia przy użyciu hello interfejs API REST zarządzania usługami Azure. Aby uzyskać więcej informacji, zobacz [dokumentacja interfejsu API REST zarządzania usługi](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Funkcje i zagadnienia
**Funkcje:**

* Łatwość użycia: w kolejności toouse rozpoznawania nazw platformy Azure jest wymagana żadna konfiguracja.
* Witaj platformy Azure usługa rozpoznawania nazw zapewnia wysoką dostępność, zapisywanie hello możesz muszą toocreate i zarządzania klastrami serwerów DNS.
* Można używać w połączeniu z własnych tooresolve serwerów DNS zarówno lokalnie, jak i nazwy hostów Azure.
* Rozpoznawanie nazw jest udostępniane między wystąpieniami/maszyn wirtualnych roli w ramach hello sama usługa w chmurze bez konieczności nazwę FQDN.
* Rozpoznawanie nazw są udostępniane między maszynami wirtualnymi w sieciach wirtualnych, które używają hello modelu wdrażania usługi Resource Manager, bez potrzeby hello nazwy FQDN. Sieci wirtualne w hello klasycznego modelu wdrażania wymagają hello FQDN podczas rozpoznawania nazw w innej chmurze usługi. 
* Można użyć nazwy hostów, które najlepiej opisują wdrożeń, a nie Praca z nazwami wygenerowany automatycznie.

**Kwestie do rozważenia:**

* Nie można zmodyfikować sufiks DNS utworzony Azure Hello.
* Nie można ręcznie zarejestrować własnych.
* Usługa WINS i NetBIOS są nieobsługiwane. (Użytkownik nie widzi maszyn wirtualnych w Eksploratorze Windows).
* Nazwy hostów musi być zgodny z DNS (muszą oni korzystać tylko 0-9, a-z i "-" i nie może zaczynać się ani kończyć "-". Zobacz dokument RFC 3696 sekcja 2).
* Ruch zapytanie DNS jest ograniczenie dla każdej maszyny Wirtualnej. Nie powinno to mieć wpływ na większości aplikacji.  Ograniczanie żądań zaobserwowano, upewnij się, że włączone jest buforowanie po stronie klienta.  Aby uzyskać więcej informacji, zobacz [pobierania hello większości rozpoznawania nazw platformy Azure z](#Getting-the-most-from-Azure-provided-name-resolution).
* Tylko maszyny wirtualne hello pierwszy 180 usług w chmurze są zarejestrowane dla każdej sieci wirtualnej w klasycznym modelu wdrażania. Nie dotyczy sieci toovirtual w modelach wdrażania Menedżera zasobów.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Pobieranie hello większości z rozpoznawania nazw platformy Azure
**Buforowanie po stronie klienta:**

Nie wszystkie zapytania DNS musi toobe wysyłane przez sieć hello.  Buforowanie po stronie klienta pomaga zmniejszenia opóźnienia i zwiększyć odporność toonetwork blips rozwiązując cyklicznego zapytania DNS z lokalnej pamięci podręcznej.  Rekordy DNS zawierają Time To Live (TTL) umożliwiający hello pamięci podręcznej toostore hello rekordu tak długo, jak to możliwe bez wywierania wpływu na świeżości rekordów, tak po stronie klienta jest odpowiedni dla większości sytuacji.

domyślne powitania klienta DNS systemu Windows ma wbudowane pamięci podręcznej DNS.  Niektóre buforowanie domyślnie nie zawierają dystrybucjach systemu Linux, zaleca się jeden dodania tooeach maszyny Wirtualnej systemu Linux (po sprawdzeniu, że nie ma lokalnej pamięci podręcznej już).

Istnieje wiele różnych DNS buforowania dostępnych pakietów, np. dnsmasq, Oto hello kroki tooinstall dnsmasq na dystrybucjach najbardziej typowych hello:

* **Ubuntu (używa resolvconf)**:
  * po prostu zainstaluj pakiet dnsmasq hello ("get stanie instalacji dnsmasq sudo").
* **SUSE (używa netconf)**:
  * Zainstaluj pakiet dnsmasq hello ("sudo zypper instalacji dnsmasq") 
  * Włącz usługę dnsmasq hello ("Włącz dnsmasq.service systemctl") 
  * Uruchom usługę dnsmasq hello ("systemctl start dnsmasq.service") 
  * Edytuj "/ etc/sysconfig/sieci/konfiguracji" i zmień NETCONFIG_DNS_FORWARDER = "" za "dnsmasq"
  * zaktualizowanie resolv.conf ("netconfig update") tooset hello pamięci podręcznej jako hello lokalnego rozpoznawania nazw DNS
* **OpenLogic (używa NetworkManager)**:
  * Zainstaluj pakiet dnsmasq hello ("sudo yum instalacji dnsmasq")
  * Włącz usługę dnsmasq hello ("Włącz dnsmasq.service systemctl")
  * Uruchom usługę dnsmasq hello ("systemctl start dnsmasq.service")
  * Dodaj "dołączy domeny nazwy serwerów 127.0.0.1;" too"/etc/dhclient-eth0.conf"
  * Uruchom ponownie pamięci podręcznej hello sieci usługi ("usługi sieciowej restart") tooset hello jako hello lokalnego rozpoznawania nazw DNS

> [!NOTE]
> Pakiet "dnsmasq" Hello jest tylko jeden hello wiele pamięci podręcznej DNS dostępne dla systemu Linux.  Przed użyciem go, sprawdź, czy jego przydatności do określonych potrzeb, a nie pamięci podręcznej jest zainstalowany.
> 
> 

**Ponownych prób po stronie klienta:**

Usługa DNS jest głównie protokołu UDP.  Jak hello protokołu UDP nie gwarantuje dostarczanie komunikatów, obsługi logiki ponawiania próby w samego protokołu DNS hello.  Każdy klient DNS (systemu operacyjnego) może pokazać Logika ponawiania różne w zależności od preferencji twórców hello:

* Systemów operacyjnych Windows ponów próbę po 1 sekundę, a następnie ponownie po innym 2, 4 i inny 4 sekundy. 
* Witaj domyślne Linux Instalatora ponownych prób po 5 sekund.  Jest zalecana toochange tego tooretry 5 razy w drugim 1 w odstępach czasu.  

toocheck hello bieżące ustawienia na Maszynę wirtualną systemu Linux, "/etc/resolv.conf cat" i sprawdź w wierszu "Opcje" hello, np.:

    options timeout:1 attempts:5

Plik resolv.conf Hello jest zwykle generowanych automatycznie i nie można edytować.  Hello określone kroki, aby dodać wiersz hello "Opcje" różnią się distro:

* **Ubuntu** (używa resolvconf):
  * Dodaj hello opcje wiersza too'/etc/resolveconf/resolv.conf.d/head " 
  * Uruchom tooupdate "resolvconf -u"
* **SUSE** (używa netconf):
  * Dodaj toohello "timeout:1 prób: 5" NETCONFIG_DNS_RESOLVER_OPTIONS = "" parametru w "/ etc/sysconfig / / konfigurację sieci" 
  * Uruchom tooupdate "netconfig aktualizacji"
* **OpenLogic** (używa NetworkManager):
  * Dodaj too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo zł "Opcje timeout:1 prób: 5" ' " 
  * Uruchom tooupdate "ponowne uruchomienie usługi sieciowej"

## <a name="name-resolution-using-your-own-dns-server"></a>Rozpoznawanie nazw przy użyciu serwera DNS
Istnieją różne sytuacje, w przypadku, gdy Twoje potrzeby rozpoznawania nazw może go poza hello funkcje udostępniane przez platformę Azure, na przykład gdy przy użyciu domen usługi Active Directory lub gdy wymagają rozpoznawania nazw DNS między sieciami wirtualnymi (sieci wirtualne).  toocover tych scenariuszy Azure zapewnia możliwość hello toouse możesz serwery DNS.  

Serwery DNS w sieci wirtualnej może przekazywać programy rozpoznawania nazw DNS zapytania tooAzure cykliczne tooresolve jako nazw hostów w tej sieci wirtualnej.  Na przykład domeny kontrolera (DC) działają na platformie Azure mogą odpowiadać tooDNS zapytania dotyczące jego domeny i przesyła innych tooAzure zapytania.  Dzięki temu toosee maszyn wirtualnych zarówno lokalnych zasobów (za pośrednictwem hello kontrolera domeny), jak i nazwy hostów platformy Azure (za pośrednictwem usługi przesyłania dalej hello).  Rozwiązujący cykliczne tooAzure dostępu zostaną przekazane za pośrednictwem wirtualnego adresu IP hello 168.63.129.16.

Przesyłanie dalej DNS również umożliwia rozpoznawania nazw DNS między sieciami wirtualnymi oraz pozwala na tooresolve maszyny z lokalnymi nazwy hostów platformy Azure.  W celu tooresolve nazwa hosta maszyny Wirtualnej, serwer DNS hello maszyna wirtualna musi znajdować się w hello sam wirtualnych sieci i można tooAzure zapytania hostname tooforward skonfigurowany.  Sufiks DNS hello jest różna w każdej sieci wirtualnej, można użyć Przesyłanie warunkowe zasady toosend DNS wysyła zapytanie toohello Popraw sieci wirtualnej do rozpoznania.  powitania po obraz zawiera dwie sieci wirtualnych i sieci lokalnej podczas rozpoznawania nazw DNS między sieciami wirtualnymi przy użyciu tej metody.  Usługi przesyłania dalej DNS na przykład jest dostępny w hello [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) i [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS między sieciami wirtualnymi](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Podczas rozpoznawania nazwy platformy Azure, sufiks DNS wewnętrzny (*. internal.cloudapp.net) jest podana tooeach maszyny Wirtualnej za pomocą protokołu DHCP.  Dzięki temu rozpoznawania nazwy hosta jako nazwę hosta hello, są rekordy w strefie internal.cloudapp.net hello.  Korzystając z własnych rozwiązania rozpoznawania nazw, powitalne sufiks międzynarodowych nazw DOMEN nie jest podany tooVMs, ponieważ zakłócać innych architektur DNS (na przykład scenariusze przyłączonych do domeny).  Zamiast tego udostępniamy symbol zastępczy niedziałającej (reddog.microsoft.com).  

W razie potrzeby sufiks DNS wewnętrzny hello może zostać określony przy użyciu programu PowerShell lub hello interfejsu API:

* Sieci wirtualne w modelach wdrażania Menedżera zasobów sufiks hello jest dostępna za pośrednictwem hello [karty interfejsu sieciowego](https://msdn.microsoft.com/library/azure/mt163668.aspx) zasobów lub za pośrednictwem hello [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) polecenia cmdlet.    
* W klasycznych modeli wdrażania, sufiks hello jest dostępna za pośrednictwem hello [uzyskać interfejsu API wdrożenia](https://msdn.microsoft.com/library/azure/ee460804.aspx) wywołania lub za pośrednictwem hello [Get AzureVM-debugowania](https://msdn.microsoft.com/library/azure/dn495236.aspx) polecenia cmdlet.

Jeśli przekazywanie zapytań tooAzure nie własnych potrzeb, konieczne będzie tooprovide rozwiązania DNS.  Konieczne będzie rozwiązania DNS:

* Podaj rozpoznawania nazwy hosta odpowiednie, np. za pomocą [DDNS](virtual-networks-name-resolution-ddns.md).  Uwaga: Jeśli przy użyciu DDNS może być konieczne oczyszczanie rekordów DNS toodisable, jak dzierżaw DHCP platformy Azure są bardzo długie i oczyszczania może usunąć DNS przedwcześnie rekordy. 
* Podaj odpowiednie rekursywnego rozpoznawania tooallow rozpoznawania nazw domen zewnętrznych.
* Jest dostępny (TCP i UDP na porcie 53) z klientów hello służy i być może tooaccess hello internet.
* Można zabezpieczyć przed dostępem z hello internet, toomitigate zagrożenia powodowanego przez czynników zewnętrznych.

> [!NOTE]
> Aby uzyskać najlepszą wydajność, korzystając z maszyn wirtualnych platformy Azure jako serwery DNS, należy wyłączyć IPv6 i [publiczny adres IP na poziomie wystąpienia](virtual-networks-instance-level-public-ip.md) powinien być przypisany do serwera DNS tooeach maszyny Wirtualnej.  Jeśli wybierzesz toouse systemu Windows Server jako serwer DNS, [w tym artykule](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) zapewnia analizy wydajności i optymalizacji.
> 
> 

### <a name="specifying-dns-servers"></a>Określanie serwerów DNS
Przy użyciu serwerów DNS, Azure udostępnia hello możliwości toospecify wiele serwerów DNS dla sieci wirtualnej lub na sieć interfejsu (Resource Manager) / (klasyczne) usługa w chmurze.  Serwerów DNS określonych dla interfejsu sieci usługi chmury Pobierz pierwszeństwo nad określone dla sieci wirtualnej hello.

> [!NOTE]
> Właściwości połączenia sieci, takich jak serwer DNS adresów IP, nie należy edytować bezpośrednio z poziomu maszyn wirtualnych systemu Windows, jak mogą uzyskać wymazane podczas usługi poprawianego po wymianie pobiera hello karty sieci wirtualnej. 
> 
> 

Podczas korzystania z modelu wdrażania usługi Resource Manager hello, serwery DNS można określić w hello portalu, interfejsu API/szablonów ([sieci wirtualnej](https://msdn.microsoft.com/library/azure/mt163661.aspx), [kart](https://msdn.microsoft.com/library/azure/mt163668.aspx)) lub programu PowerShell ([sieci wirtualnej](https://msdn.microsoft.com/library/mt603657.aspx), [kart](https://msdn.microsoft.com/library/mt619370.aspx)).

Korzystając z hello klasycznego modelu wdrażania, serwery DNS dla sieci wirtualnej hello może zostać określony w hello portalu lub [hello *konfiguracji sieci* pliku](https://msdn.microsoft.com/library/azure/jj157100).  Dla usług w chmurze, serwery DNS hello są określone za pomocą [hello *konfiguracji usługi* pliku](https://msdn.microsoft.com/library/azure/ee758710) lub w programie PowerShell ([AzureVM nowy](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> W przypadku zmiany ustawień DNS hello maszyn wirtualnych sieci/wirtualnego została już wdrożona, należy toorestart każdej maszyny Wirtualnej w odpowiednich dla efektu tootake zmiany hello.
> 
> 

## <a name="next-steps"></a>Następne kroki
Model wdrażania Menedżera zasobów:

* [Utwórz lub zaktualizuj sieć wirtualną](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Utwórz lub zaktualizuj karty interfejsu sieciowego](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [Nowy AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [Nowe AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Klasycznego modelu wdrażania:

* [Schemat konfiguracji usługi Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Schemat konfiguracji sieci wirtualnej](https://msdn.microsoft.com/library/azure/jj157100)
* [Skonfiguruj sieć wirtualną przy użyciu pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md) 

