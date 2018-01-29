---
title: "Czas rozpoznawania nazw dla maszyn wirtualnych i wystąpień roli"
description: "Nazwy scenariuszy rozwiązania IaaS platformy Azure, rozwiązania hybrydowe między inną chmurę usługi Active Directory i przy użyciu serwera DNS "
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: jdial
ms.openlocfilehash: 5a298f535308cff90ddd249594b7bb5e36909867
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Rozpoznawanie nazw dla maszyn wirtualnych i wystąpień roli
W zależności od tego, jak używasz usługi Azure do hostowania IaaS i PaaS, hybrydowych rozwiązań konieczne może być umożliwiają maszyn wirtualnych i wystąpień ról, które zostało utworzone w celu komunikowania się ze sobą. Mimo że ten komunikat może odbywać się przy użyciu adresów IP, jest znacznie prostsza do użyć nazw, które można łatwo zapamiętać i nie należy zmieniać. 

Jeśli wystąpień roli maszyn wirtualnych hostowanych na platformie Azure wymagane i rozpoznawanie nazw domen do adresów IP, można użyć jednej z dwóch metod:

* [Rozpoznawanie nazw platformy Azure](#azure-provided-name-resolution)
* [Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) (która może przesłać kwerendy do serwerów DNS platformy Azure) 

Rodzaj rozpoznawania nazw, których używasz, zależy od tego, jak maszyn wirtualnych i wystąpień roli muszą komunikować się ze sobą.

**W poniższej tabeli przedstawiono scenariusze i odpowiedniego rozwiązania rozpoznawania nazwy:**

| **Scenariusz** | **Rozwiązania** | **Suffix** |
| --- | --- | --- |
| Rozpoznawanie nazw między wystąpień roli lub maszyn wirtualnych znajdujących się w tej samej usługi w chmurze lub sieci wirtualnej |[Rozpoznawanie nazw platformy Azure](#azure-provided-name-resolution) |Nazwa hosta lub nazwa FQDN |
| Rozpoznawanie nazw w usłudze Azure App Service (aplikacja sieci Web, funkcji, Bot itp.) przy użyciu integracji z sieciami Wirtualnymi wystąpień roli lub maszyn wirtualnych znajdujących się w tej samej sieci wirtualnej |Zarządzany przez klienta DNS serwerów przekazujących zapytań między sieciami wirtualnymi rozpoznanie przez platformę Azure (serwer proxy DNS).  Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Rozpoznawanie nazw między wystąpień roli lub maszyn wirtualnych znajdujących się w różnych sieciach wirtualnych |Zarządzany przez klienta DNS serwerów przekazujących zapytań między sieciami wirtualnymi rozpoznanie przez platformę Azure (serwer proxy DNS).  Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Rozpoznawanie nazwy komputerów i usług lokalnych z wystąpień roli lub maszyn wirtualnych na platformie Azure |Zarządzany przez klienta z serwerów DNS (np. lokalnego kontrolera domeny, kontrolera domeny tylko do odczytu lokalnej lub zsynchronizowany przy użyciu transferów stref DNS dodatkowej).  Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Rozpoznawanie nazwy Azure hostów z komputerów lokalnych |Do przodu zapytań do serwera proxy DNS zarządzany przez klienta w odpowiedniej sieci wirtualnej, serwer proxy przekazuje zapytania na platformie Azure do rozpoznania. Zobacz [rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Tylko nazwa FQDN |
| Reverse DNS wewnętrznych adresów IP |[Rozpoznawanie nazw przy użyciu serwera DNS](#name-resolution-using-your-own-dns-server) |Nie dotyczy |
| Rozpoznawanie nazw między maszynami wirtualnymi lub wystąpień roli znajduje się w różnych usług w chmurze, nie znajduje się w sieci wirtualnej |Nie dotyczy. Łączność między maszyn wirtualnych i wystąpień roli w innej chmurze usługi nie jest obsługiwana poza siecią wirtualną. |Nie dotyczy |

## <a name="azure-provided-name-resolution"></a>Rozpoznawanie nazw platformy Azure
Wraz z rozpoznawanie publicznej nazwy DNS platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i wystąpień ról, które znajdują się w tej samej sieci wirtualnej lub usługi w chmurze.  Maszyny wirtualne/wystąpienia w usłudze w chmurze udostępnić tym samym sufiksem DNS (tylko nazwa hosta jest wystarczająca), ale w innej chmurze klasycznych sieci wirtualnych usługi mają inne sufiksy DNS, więc nazwa FQDN nie jest wymagane do rozpoznawania nazw między usługami inną chmurę.  W sieciach wirtualnych w modelu wdrażania usługi Resource Manager, sufiks DNS jest spójna sieci wirtualnych (tak, aby nazwa FQDN nie jest potrzebny) i nazwy DNS można przypisać do karty sieciowe i maszyn wirtualnych. Mimo że rozpoznawanie nazw platformy Azure nie wymaga żadnej konfiguracji, nie jest odpowiednim wyborem w przypadku wszystkich scenariuszy wdrożenia w poprzedniej tabeli.

> [!NOTE]
> W przypadku ról sieć web i proces roboczy można także przejść wewnętrznych adresów IP na podstawie liczby nazwę i wystąpienie roli przy użyciu interfejsu API REST zarządzania usługi Azure wystąpień roli. Aby uzyskać więcej informacji, zobacz [dokumentacja interfejsu API REST zarządzania usługi](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Funkcje i zagadnienia
**Funkcje:**

* Łatwość użycia: Aby można było używać rozpoznawania nazw platformy Azure jest wymagana żadna konfiguracja.
* Usługa rozpoznawania nazw platformy Azure jest wysokiej dostępności, co pozwala zaoszczędzić konieczność tworzenia i zarządzania klastrami serwerów DNS.
* Można w połączeniu z serwerem DNS do rozpoznawania zarówno lokalnie, jak i nazwy hostów Azure.
* Rozpoznawanie nazw są udostępniane między wystąpieniami/maszyn wirtualnych roli w ramach tej samej usługi w chmurze bez konieczności nazwę FQDN.
* Rozpoznawanie nazw są udostępniane między maszynami wirtualnymi w sieciach wirtualnych, które używają modelu wdrażania usługi Resource Manager, bez potrzeby dla nazwy FQDN. Sieci wirtualne w klasycznym modelu wdrażania wymagają nazwy FQDN podczas rozpoznawania nazw w innej chmurze usługi. 
* Można użyć nazwy hostów, które najlepiej opisują wdrożeń, a nie Praca z nazwami wygenerowany automatycznie.

**Kwestie do rozważenia:**

* Nie można zmodyfikować sufiks DNS utworzony Azure.
* Nie można ręcznie zarejestrować własnych.
* Usługa WINS i NetBIOS są nieobsługiwane. (Użytkownik nie widzi maszyn wirtualnych w Eksploratorze Windows).
* Nazwy hostów musi być zgodny z DNS (muszą oni korzystać tylko 0-9, a-z i "-" i nie może zaczynać się ani kończyć "-". Zobacz dokument RFC 3696 sekcja 2).
* Ruch zapytanie DNS jest ograniczenie dla każdej maszyny Wirtualnej. Nie powinno to mieć wpływ na większości aplikacji.  Ograniczanie żądań zaobserwowano, upewnij się, że włączone jest buforowanie po stronie klienta.  Aby uzyskać więcej informacji, zobacz [wprowadzenie w pełni wykorzystać możliwości rozpoznawania nazw platformy Azure](#Getting-the-most-from-Azure-provided-name-resolution).
* W pierwszej usługi w chmurze 180 tylko maszyny wirtualne są zarejestrowane dla każdej sieci wirtualnej w klasycznym modelu wdrażania. To nie ma zastosowania do sieci wirtualnych w modelach wdrażania Menedżera zasobów.

### <a name="getting-the-most-from-azure-provided-name-resolution"></a>Pobieranie w pełni wykorzystać możliwości rozpoznawania nazw platformy Azure
**Client-side Caching:**

Nie wszystkie zapytania DNS musi być przesyłane przez sieć.  Buforowanie po stronie klienta pomaga zmniejszenia opóźnienia i poprawy odporności na blips sieci rozwiązując cyklicznego zapytania DNS z lokalnej pamięci podręcznej.  Rekordy DNS zawierają Time To Live (TTL) umożliwiający pamięci podręcznej do przechowywania bez wpływania na świeżości rekordów, tak po stronie klienta jest odpowiedni dla większości sytuacji rekordu tak długo, jak to możliwe.

Domyślnie klienta DNS systemu Windows ma wbudowane pamięci podręcznej DNS.  Niektóre buforowanie domyślnie nie zawierają dystrybucjach systemu Linux, zaleca się jeden dodania do każdej maszyny Wirtualnej systemu Linux (po sprawdzeniu, że nie ma lokalnej pamięci podręcznej już).

Istnieje szereg różnych DNS buforowania dostępnych pakietów. Na przykład dnsmasq. Poniższe kroki listy instalowanie dnsmasq na najbardziej typowych dystrybucjach:

* **Ubuntu (używa resolvconf)**:
  * po prostu zainstaluj pakiet dnsmasq ("get stanie instalacji dnsmasq sudo").
* **SUSE (używa netconf)**:
  * Zainstaluj pakiet dnsmasq ("sudo zypper instalacji dnsmasq") 
  * Włącz usługę dnsmasq ("Włącz dnsmasq.service systemctl") 
  * Uruchom usługę dnsmasq ("systemctl start dnsmasq.service") 
  * Edytuj "/ etc/sysconfig/sieci/konfiguracji" i zmień NETCONFIG_DNS_FORWARDER = "" do "dnsmasq"
  * zaktualizowanie resolv.conf ("netconfig update") można ustawić pamięci podręcznej lokalnego rozpoznawania nazw DNS
* **OpenLogic (używa NetworkManager)**:
  * Zainstaluj pakiet dnsmasq ("sudo yum instalacji dnsmasq")
  * Włącz usługę dnsmasq ("Włącz dnsmasq.service systemctl")
  * Uruchom usługę dnsmasq ("systemctl start dnsmasq.service")
  * Dodaj "dołączy domeny nazwy serwerów 127.0.0.1;" do "/etc/dhclient-eth0.conf"
  * Uruchom ponownie usługi sieciowej ("usługi sieciowej restart"), można ustawić pamięci podręcznej jako lokalnego rozpoznawania nazw DNS

> [!NOTE]
> Pakiet "dnsmasq" jest tylko jeden z wielu pamięci podręcznej DNS, dostępne dla systemu Linux.  Przed użyciem go, sprawdź, czy jego przydatności do określonych potrzeb, a nie pamięci podręcznej jest zainstalowany.
> 
> 

**Ponownych prób po stronie klienta:**

Usługa DNS jest głównie protokołu UDP.  Jak protokół UDP nie gwarantuje dostarczanie komunikatów, obsługi logiki ponawiania próby w samego protokołu DNS.  Każdy klient DNS (systemu operacyjnego) może pokazać Logika ponawiania różne w zależności od preferencji twórcy:

* Systemów operacyjnych Windows ponów próbę po 1 sekundę, a następnie ponownie po innym 2, 4 i inny 4 sekundy. 
* Domyślne Linux Instalatora ponownych prób po 5 sekund.  Zaleca się, aby zmienić to, aby ponowić próbę 5 razy w drugim 1 w odstępach czasu.  

Użyj polecenia "kot /etc/resolv.conf", aby sprawdzić bieżące ustawienia na Maszynę wirtualną systemu Linux, a następnie sprawdź w wierszu "Opcje", na przykład:

    options timeout:1 attempts:5

Plik resolv.conf jest zazwyczaj generowanych automatycznie i nie można edytować.  Poszczególne kroki dodaniu pozycji "Opcje" różnią się distro:

* **Ubuntu** (używa resolvconf):
  * Dodaj linię opcji "/ etc/resolveconf/resolv.conf.d/head" 
  * Uruchom 'resolvconf -u' do zaktualizowania
* **SUSE** (używa netconf):
  * Dodaj do NETCONFIG_DNS_RESOLVER_OPTIONS "timeout:1 prób: 5" = "" parametru w "/ etc/sysconfig / / konfigurację sieci" 
  * Uruchom "netconfig update" do zaktualizowania
* **OpenLogic** (używa NetworkManager):
  * Dodaj "echo"Opcje timeout:1 prób: 5"" do "/ etc/NetworkManager/dispatcher.d/11-dhclient" 
  * Uruchom "sieci po ponownym uruchomieniu usługi" do zaktualizowania

## <a name="name-resolution-using-your-own-dns-server"></a>Rozpoznawanie nazw przy użyciu serwera DNS
Istnieją różne sytuacje, w przypadku, gdy potrzeb rozpoznawania nazw może go poza funkcje udostępniane przez platformę Azure, na przykład gdy przy użyciu domen usługi Active Directory lub gdy wymagają rozpoznawania nazw DNS między sieciami wirtualnymi.  Tak, aby pokrywał tych scenariuszy, platforma Azure oferuje możliwości do użycia serwery DNS.  

Serwery DNS w sieci wirtualnej można przekazywać zapytań DNS do rozpoznawania nazw cykliczne platformy Azure do rozpoznania nazwy hostów w tej sieci wirtualnej.  Na przykład domeny kontrolera (DC) działają na platformie Azure można odpowiada na zapytania DNS dla swojej domeny i przesyła inne zapytania na platformie Azure.  Dzięki temu maszyny wirtualne zobaczyć, zarówno lokalnych zasobów (za pośrednictwem kontrolera domeny), jak i nazwy hostów platformy Azure (za pośrednictwem usługi przesyłania dalej).  Dostęp do platformy Azure cykliczne rozwiązujący zostaną przekazane za pośrednictwem wirtualnego adresu IP 168.63.129.16.

Przesyłanie dalej DNS również umożliwia rozpoznawanie nazw DNS w sieci wirtualnej między oraz pozwala na maszynach lokalnych do rozpoznania nazwy hostów platformy Azure.  Aby można było rozpoznać nazwy hosta maszyny Wirtualnej, serwer DNS maszyny Wirtualnej musi znajdować się w tej samej sieci wirtualnej i można skonfigurować do zapytań do przodu nazwy hosta Azure.  Sufiks DNS jest różna w każdej sieci wirtualnej, można użyć zasady warunkowego przesyłania dalej do wysyłania zapytań DNS na poprawną sieci wirtualnej do rozpoznania.  Na poniższej ilustracji przedstawiono dwie sieci wirtualne i sieć lokalną tej sieci wirtualnej między komputerami za pomocą tej metody rozpoznawania nazw DNS.  Usługi przesyłania dalej DNS na przykład jest dostępny w [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) i [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![Sieć wirtualna między DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Podczas rozpoznawania nazwy platformy Azure, sufiks DNS wewnętrzny (*. internal.cloudapp.net) znajduje się na każdej maszynie Wirtualnej za pomocą protokołu DHCP.  Rejestruje nazwę hosta są w strefie internal.cloudapp.net dzięki temu rozpoznawania nazwy hosta.  Korzystając z własnych rozwiązań rozpoznawania nazwy, ponieważ zakłócać innych architektur DNS (na przykład scenariusze przyłączonych do domeny) sufiks międzynarodowych nazw DOMEN nie podano do maszyn wirtualnych.  Zamiast tego udostępniamy symbol zastępczy niedziałającej (reddog.microsoft.com).  

W razie potrzeby sufiks DNS wewnętrzny może zostać określony przy użyciu programu PowerShell lub interfejsu API:

* Dla sieci wirtualnych w modelach wdrażania usługi Resource Manager, jest dostępny za pośrednictwem sufiks [karty interfejsu sieciowego](https://msdn.microsoft.com/library/azure/mt163668.aspx) zasobów lub za pośrednictwem [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) polecenia cmdlet.    
* W klasycznych modeli wdrażania, jest dostępna za pośrednictwem sufiks [uzyskać interfejsu API wdrożenia](https://msdn.microsoft.com/library/azure/ee460804.aspx) wywołania lub za pośrednictwem [Get AzureVM-debugowania](https://msdn.microsoft.com/library/azure/dn495236.aspx) polecenia cmdlet.

Przekazywanie zapytań na platformie Azure nie własnych potrzeb, należy podać rozwiązania DNS.  Konieczne będzie rozwiązania DNS:

* Podaj rozpoznawania nazwy hosta odpowiednie, np. za pomocą [DDNS](virtual-networks-name-resolution-ddns.md).  Uwaga: Jeśli przy użyciu DDNS może być konieczne wyłączenie Oczyszczanie rekord usługi DNS platformy Azure dzierżaw DHCP są bardzo długich i oczyszczania może usunąć rekordy DNS przedwcześnie. 
* Podaj odpowiednie rekursywnego rozpoznawania zezwalająca na rozpoznawanie nazw domen zewnętrznych.
* Być dostępny (TCP i UDP na porcie 53) od klientów, które służy ona i mieć możliwość uzyskania dostępu do Internetu.
* Być zabezpieczony przed dostępu z Internetu, ograniczających zagrożenia powodowanego przez czynników zewnętrznych.

> [!NOTE]
> Aby uzyskać najlepszą wydajność, korzystając z maszyn wirtualnych platformy Azure jako serwery DNS, należy wyłączyć IPv6 i [publiczny adres IP na poziomie wystąpienia](virtual-networks-instance-level-public-ip.md) powinny zostać przypisane do każdego serwera DNS maszyny Wirtualnej.  Jeśli chcesz użyć systemu Windows Server jako serwer DNS, [w tym artykule](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) zapewnia analizy wydajności i optymalizacji.
> 
> 

### <a name="specifying-dns-servers"></a>Określanie serwerów DNS
Korzystając z serwerów DNS, Azure pozwala, aby określić wiele serwerów DNS dla sieci wirtualnej lub dla interfejsu sieciowego (Resource Manager) / (klasyczne) usługa w chmurze.  Serwerów DNS określonych dla interfejsu sieci usługi chmury Pobierz pierwszeństwo nad określone dla sieci wirtualnej.

> [!NOTE]
> Właściwości połączenia sieci, takich jak serwer DNS adresów IP, nie należy edytować bezpośrednio z poziomu maszyn wirtualnych systemu Windows, jak mogą uzyskać wymazane podczas usługi poprawianego po wymianie pobiera karty sieci wirtualnej. 
> 
> 

Podczas korzystania z modelu wdrażania usługi Resource Manager, serwerów DNS można określić w portalu, interfejsu API/szablonów ([sieci wirtualnej](https://msdn.microsoft.com/library/azure/mt163661.aspx), [kart](https://msdn.microsoft.com/library/azure/mt163668.aspx)) lub programu PowerShell ([sieci wirtualnej](https://msdn.microsoft.com/library/mt603657.aspx), [ Karta sieciowa](https://msdn.microsoft.com/library/mt619370.aspx)).

Korzystając z klasycznym modelu wdrażania, serwery DNS dla sieci wirtualnej można określić w portalu lub [ *konfiguracji sieci* pliku](https://msdn.microsoft.com/library/azure/jj157100).  Dla usług w chmurze, serwery DNS są określone za pomocą [ *konfiguracji usługi* pliku](https://msdn.microsoft.com/library/azure/ee758710) lub w programie PowerShell ([AzureVM nowy](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> W przypadku zmiany ustawień DNS dla wirtualnych sieci/wirtualnej maszyny, która została już wdrożona, musisz ponownie uruchomić każdej dotyczy maszyny Wirtualnej, aby zmiany zaczęły obowiązywać.
> 
> 

## <a name="next-steps"></a>Kolejne kroki
Model wdrażania Menedżera zasobów:

* [Utwórz lub zaktualizuj sieć wirtualną](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Utwórz lub zaktualizuj karty interfejsu sieciowego](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Klasycznego modelu wdrażania:

* [Schemat konfiguracji usługi Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Schemat konfiguracji sieci wirtualnej](https://msdn.microsoft.com/library/azure/jj157100)
* [Skonfiguruj sieć wirtualną przy użyciu pliku konfiguracji sieci](virtual-networks-using-network-configuration-file.md) 

