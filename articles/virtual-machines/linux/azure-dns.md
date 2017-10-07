---
title: aaaDNS opcje rozpoznawania nazw dla maszyn wirtualnych systemu Linux na platformie Azure
description: "Nazwa usługi DNS dla maszyn wirtualnych systemu Linux IaaS platformy Azure, w tym scenariuszy, pod warunkiem rozpoznawania, hybrydowego zewnętrznego serwera DNS i Przenieś swój własny DNS."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opcje rozpoznawania nazw DNS dla maszyn wirtualnych systemu Linux na platformie Azure
Platforma Azure udostępnia rozpoznawanie nazw DNS domyślnie dla wszystkich maszyn wirtualnych, które znajdują się w jednej sieci wirtualnej. Można zaimplementować własne rozwiązania rozpoznawania nazw DNS przez skonfigurowanie usługi DNS na maszynach wirtualnych obsługującego platformy Azure. Witaj następujące scenariusze powinien pomagają w określeniu Witaj, który działa w danej sytuacji.

* [Rozpoznawanie nazw, która udostępnia usługi Azure](#azure-provided-name-resolution)
* [Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server)

Typ Hello rozpoznawania nazw, którego używasz, zależy od tego, jak sieci maszyn wirtualnych i wystąpień roli należy toocommunicate ze sobą.

Witaj poniższej tabeli przedstawiono scenariusze i odpowiedniego rozwiązania rozpoznawania nazwy:

| **Scenariusz** | **Rozwiązania** | **Sufiks** |
| --- | --- | --- |
| Rozpoznawanie między wystąpień roli lub maszyn wirtualnych w hello nazw tej samej sieci wirtualnej |[Rozpoznawanie nazw, która udostępnia usługi Azure](#azure-provided-name-resolution) |Nazwa hosta lub w pełni kwalifikowaną nazwę domeny (FQDN) |
| Rozpoznawanie nazw między wystąpień roli lub maszyn wirtualnych w różnych sieciach wirtualnych |Zarządzany przez klienta serwerów DNS, które przekazywania kwerend między sieciami wirtualnymi rozpoznanie przez platformę Azure (serwer proxy DNS). Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server). |Tylko nazwa FQDN |
| Rozpoznawanie nazwy usługi z wystąpień roli lub maszynach wirtualnych platformy Azure i komputerów lokalnych |Zarządzany przez klienta z serwerów DNS (na przykład lokalnego kontrolera domeny, kontrolera domeny tylko do odczytu lokalnej lub zsynchronizowane za pomocą transferów stref DNS dodatkowej). Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server). |Tylko nazwa FQDN |
| Rozpoznawanie nazwy Azure hostów z komputerów lokalnych |Przesyła zapytania tooa zarządzany przez klienta DNS serwera proxy w hello odpowiedniej sieci wirtualnej. Serwer proxy Hello przekazuje tooAzure zapytania do rozpoznania. Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server). |Tylko nazwa FQDN |
| Reverse DNS wewnętrznych adresów IP |[Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Nie dotyczy |

## <a name="name-resolution-that-azure-provides"></a>Rozpoznawanie nazw, która udostępnia usługi Azure
Wraz z rozpoznawanie publicznej nazwy DNS platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień ról, które znajdują się w hello tej samej sieci wirtualnej. W sieciach wirtualnych opartych na usłudze Azure Resource Manager hello sufiks DNS jest spójne w ramach sieci wirtualnej hello; Witaj FQDN nie jest wymagana. Karty sieciowe tooboth (NIC) i maszyny wirtualne można przypisać nazwy DNS. Mimo że hello rozpoznawania nazw, które platforma Azure udostępnia nie wymaga żadnej konfiguracji, nie jest hello wybór odpowiedniego dla wszystkich scenariuszy wdrożenia w hello powyższej tabeli.

### <a name="features-and-considerations"></a>Funkcje i zagadnienia
**Funkcje:**

* Konfiguracja nie jest wymagane toouse rozpoznawania nazw, które platforma Azure udostępnia.
* Usługa rozpoznawania nazw Hello Azure udostępnia ma wysoką dostępność. Nie należy toocreate i zarządzania klastrami serwerów DNS.
* Usługa rozpoznawania nazw Hello Azure udostępnia może służyć wraz z własnych tooresolve serwerów DNS zarówno lokalnie, jak i nazwy hostów Azure.
* Rozpoznawanie nazw są udostępniane między maszynami wirtualnymi w sieci wirtualnych bez potrzeby hello nazwy FQDN.
* Można użyć nazwy hostów, które najlepiej opisują wdrożeń zamiast Praca z nazwami wygenerowany automatycznie.

**Kwestie do rozważenia:**

* Nie można zmodyfikować Hello sufiks DNS, który tworzy Azure.
* Nie można ręcznie zarejestrować własnych.
* Usługa WINS i NetBIOS są nieobsługiwane.
* Nazwy hostów musi być zgodny z DNS.
    Nazwy musi zawierać tylko 0-9, a-z, i "-", i ich nie może zaczynać się ani kończyć "-". Zobacz dokument RFC 3696 sekcji 2.
* Ruch zapytanie DNS jest ograniczenie dla każdej maszyny wirtualnej. Ograniczanie nie powinny mieć wpływ na większości aplikacji.  Ograniczanie żądań zaobserwowano, upewnij się, że włączone jest buforowanie po stronie klienta.  Aby uzyskać więcej informacji, zobacz [pobierania hello większości rozpoznawania nazw, które platforma Azure udostępnia z](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Pobieranie hello większości rozpoznawania nazw, które platforma Azure udostępnia z
**Buforowanie po stronie klienta:**

Niektóre zapytania DNS nie są wysyłane przez sieć hello. Buforowanie po stronie klienta pomaga zmniejszenia opóźnienia i zwiększyć odporność toonetwork niespójności rozwiązując cyklicznego zapytania DNS z lokalnej pamięci podręcznej. Rekordy DNS zawierają Time To Live (TTL), dzięki czemu hello pamięci podręcznej toostore hello rekordu tak długo, jak to możliwe bez wywierania wpływu na świeżości rekordów. W związku z tym buforowanie po stronie klienta jest odpowiednia dla większości sytuacji.

Niektóre dystrybucje systemu Linux nie dołączaj buforowanie domyślnie. Firma Microsoft zaleca, Dodaj maszynę wirtualną systemu Linux tooeach pamięci podręcznej, po sprawdzeniu, że nie lokalnej pamięci podręcznej.

Dostępnych jest kilka różnych buforowanie pakiety, takie jak dnsmasq, DNS. Poniżej przedstawiono hello kroki tooinstall dnsmasq na najczęściej używane dystrybucje hello:

**Ubuntu (używa resolvconf)**
  * Zainstaluj pakiet dnsmasq hello ("get stanie instalacji dnsmasq sudo").

**SUSE (używa netconf)**:
1. Zainstaluj pakiet dnsmasq hello ("sudo zypper instalacji dnsmasq").
2. Włącz usługę dnsmasq hello ("Włącz dnsmasq.service systemctl").
3. Uruchom usługę dnsmasq hello ("systemctl start dnsmasq.service").
4. Edytuj "/ etc/sysconfig/sieci/konfiguracji" i zmień NETCONFIG_DNS_FORWARDER = "" za "dnsmasq".
5. Zaktualizowanie resolv.conf ("netconfig update") tooset hello pamięci podręcznej jako hello lokalnego rozpoznawania nazw DNS.

**CentOS przez oprogramowanie Wave nieautoryzowanego (dawniej OpenLogic; używa NetworkManager)**
1. Zainstaluj pakiet dnsmasq hello ("sudo yum instalacji dnsmasq").
2. Włącz usługę dnsmasq hello ("Włącz dnsmasq.service systemctl").
3. Uruchom usługę dnsmasq hello ("systemctl start dnsmasq.service").
4. Dodaj "dołączy domeny nazwy serwerów 127.0.0.1;" too"/etc/dhclient-eth0.conf".
5. Uruchom ponownie pamięci podręcznej hello sieci usługi ("usługi sieciowej restart") tooset hello jako hello lokalnego rozpoznawania nazw DNS

> [!NOTE]
> : pakiet "dnsmasq" hello jest tylko jeden hello buforuje wiele DNS, które są dostępne dla systemu Linux. Przed użyciem go, sprawdź jego przydatności do potrzeb i zainstalowanym nie pamięci podręcznej.
>
>

**Ponownych prób po stronie klienta**

Usługa DNS jest głównie protokołu UDP. Ponieważ hello protokołu UDP nie gwarantuje dostarczanie komunikatów, hello samego protokołu DNS obsługuje logiki ponawiania próby. Każdy klient DNS (systemu operacyjnego) może pokazać Logika ponawiania różne w zależności od preferencji hello twórcy:

* Systemy operacyjne Windows ponów próbę po jednej drugi, a następnie ponownie po drugim dwa, cztery i innego cztery sekundy.
* Hello domyślne Linux Instalatora ponownych prób po 5 sekund.  Należy zmienić ten tooretry pięć razy na sekundę.  

toocheck hello bieżące ustawienia na maszynie wirtualnej systemu Linux "kot /etc/resolv.conf" i poszukaj w wierszu "Opcje" hello, na przykład:

    options timeout:1 attempts:5

Witaj resolv.conf plik został wygenerowany automatycznie i nie można edytować. Witaj określonych czynności, które dodać hello "Opcje" wiersza różnią się dystrybucji:

**Ubuntu** (używa resolvconf)
1. Dodaj too'/etc/resolveconf/resolv.conf.d/head wiersza opcje hello ".
2. Uruchom tooupdate "resolvconf -u".

**SUSE** (używa netconf)
1. Dodaj toohello "timeout:1 prób: 5" NETCONFIG_DNS_RESOLVER_OPTIONS = "" parametru w "/ etc/sysconfig/sieci/konfiguracji".
2. Uruchom tooupdate "netconfig update".

**CentOS przez nieautoryzowanego oprogramowania Wave (dawniej OpenLogic)** (używa NetworkManager)
1. Dodaj too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo zł "Opcje timeout:1 prób: 5" ' ".
2. Uruchom tooupdate "sieci usługi po ponownym uruchomieniu".

## <a name="name-resolution-using-your-own-dns-server"></a>Rozpoznawanie nazw przy użyciu serwera DNS
Twoje potrzeby rozpoznawania nazw może wykracza poza hello funkcji platformy Azure. Na przykład może wymagać rozpoznawania nazw DNS między sieciami wirtualnymi. toocover tego scenariusza można używać serwerów DNS.  

Serwery DNS w sieci wirtualnej może do przodu DNS wysyła zapytanie do rozpoznawania nazw toorecursive Azure tooresolve nazwy hostów, w której znajdują się hello tej samej sieci wirtualnej. Na przykład serwer DNS, który działa na platformie Azure mogą odpowiadać tooDNS zapytania dotyczące własnej DNS strefy plików i przesyła innych tooAzure zapytania. Ta funkcja umożliwia toosee maszyn wirtualnych zarówno wpisy w plikach strefy i nazwy hostów, które platforma Azure udostępnia (za pośrednictwem usługi przesyłania dalej hello). Rozwiązujący cykliczne toohello dostępu platformy Azure jest dostarczany za pomocą wirtualnego adresu IP hello 168.63.129.16.

Przesyłanie dalej DNS również umożliwia rozpoznawanie nazw DNS między sieciami wirtualnymi i umożliwia z lokalnej maszyny tooresolve nazwy hostów, które platforma Azure udostępnia. tooresolve nazwa hosta maszyny wirtualnej, maszyna wirtualna serwera DNS hello musi znajdować się w hello tej samej sieci wirtualnej i być tooAzure zapytania hostname tooforward skonfigurowany. Sufiks DNS hello różni się w każdej sieci wirtualnej, można użyć Przesyłanie warunkowe zasady toosend DNS wysyła zapytanie toohello Popraw sieci wirtualnej do rozpoznania. Witaj poniższej ilustracji przedstawiono dwie sieci wirtualne i sieć lokalną podczas rozpoznawania nazw DNS między sieciami wirtualnymi za pomocą tej metody:

![Rozpoznawanie nazw DNS między sieciami wirtualnymi](./media/azure-dns/inter-vnet-dns.png)

Gdy używasz rozpoznawania nazw, które platforma Azure udostępnia hello wewnętrzny sufiks DNS podano tooeach maszyny wirtualnej przy użyciu protokołu DHCP. Korzystając z własnych rozwiązania rozpoznawania nazw, ten sufiks nie jest podany toovirtual maszyny ponieważ sufiks hello koliduje z innych architektur DNS. toomachines toorefer przez nazwę FQDN lub tooconfigure sufiks hello na maszynach wirtualnych, można użyć programu PowerShell lub hello sufiks hello toodetermine interfejsu API:

* Sieci wirtualne, które są zarządzane przez Menedżera zasobów Azure, sufiks hello jest dostępna za pośrednictwem hello [karty interfejsu sieciowego](https://msdn.microsoft.com/library/azure/mt163668.aspx) zasobów. Można również uruchomić hello `azure network public-ip show <resource group> <pip name>` polecenie Szczegóły hello toodisplay Twojego publicznego adresu IP, który zawiera hello FQDN hello karty sieciowej.

Przekazywanie zapytań tooAzure nie własnych potrzeb, należy najpierw tooprovide rozwiązania DNS.  Rozwiązania DNS musi:

* Podaj rozpoznawania odpowiedniej nazwy hosta, na przykład za pomocą [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Jeśli używasz DDNS, może być konieczne, usuwanie starych rekordów DNS toodisable. Dzierżawy DHCP platformy Azure są bardzo długie i oczyszczania może usunąć rekordy DNS przedwcześnie.
* Podaj odpowiednie rekursywnego rozpoznawania tooallow rozpoznawania nazw domen zewnętrznych.
* Być dostępny (TCP i UDP na porcie 53) z klientów hello, który i być może tooaccess hello Internet.
* Być zabezpieczony przed dostępu przed zagrożeniami toomitigate Internet hello powodowanego przez czynników zewnętrznych.

> [!NOTE]
> Aby uzyskać najlepszą wydajność, korzystając z maszyn wirtualnych na serwerach DNS platformy Azure, wyłącz protokół IPv6 i przypisz [publiczny adres IP na poziomie wystąpienia](../../virtual-network/virtual-networks-instance-level-public-ip.md) maszyny wirtualnej serwera DNS tooeach.  
>
>
