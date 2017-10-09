---
title: "grupy zabezpieczeń aaaNetwork na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przepływ tooisolate i kontrolę ruchu w sieci wirtualne za pomocą zapory hello rozproszone na platformie Azure przy użyciu grup zabezpieczeń sieci."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Filtrowanie ruchu sieciowego przy użyciu sieciowych grup zabezpieczeń

Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które Zezwalaj lub Odmów tooresources ruchu sieciowego połączone sieci wirtualne tooAzure (VNet). Grupy NSG mogą być skojarzone toosubnets, poszczególnych maszyn wirtualnych (klasyczne) lub interfejsów sieciowych poszczególnych (NIC) dołączony tooVMs (Resource Manager). Gdy grupa NSG jest skojarzona tooa podsieci, mają zastosowanie reguły hello tooall zasobów połączonych toohello podsieci. Dodatkowo można ograniczyć ruch również skojarzyć tooa NSG maszyny Wirtualnej lub karty sieciowej.

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu oba modele, ale firma Microsoft zaleca się, że większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="nsg-resource"></a>Zasób sieciowej grupy zabezpieczeń
Grupy NSG zawierają hello następujące właściwości:

| Właściwość | Opis | Ograniczenia | Zagadnienia do rozważenia |
| --- | --- | --- | --- |
| Nazwa |Nazwa hello NSG |Musi być unikatowa w obrębie regionu hello.<br/>Może zawierać litery, cyfry, podkreślenia, kropki i łączniki.<br/>Musi zaczynać się literą lub cyfrą.<br/>Musi kończyć się literą, cyfrą lub podkreśleniem.<br/>Nie może przekraczać 80 znaków. |Ponieważ toocreate może być konieczne kilku grup NSG, upewnij się, że masz konwencji nazewnictwa, która ułatwia funkcję hello tooidentify łatwe. |
| Region |Azure [region](https://azure.microsoft.com/regions) gdzie hello grupa NSG jest tworzona. |Grupy NSG mogą być tylko skojarzona tooresources w hello tego samego regionu hello NSG. |toolearn, o ile grupy NSG mogą mieć na region, odczytać hello [Azure ogranicza](../azure-subscription-service-limits.md#virtual-networking-limits-classic) artykułu.|
| Grupa zasobów |Witaj [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) hello w istnieje grupa NSG. |Mimo że grupy NSG istnieje w grupie zasobów, może być skojarzony tooresources w dowolnej grupie zasobów, tak długo, jak hello zasób jest częścią hello tego samego regionu Azure hello NSG. |Grupy zasobów są używane toomanage razem w ramach jednostki wdrożenia wielu zasobów.<br/>Można rozważyć zgrupowanie hello grupy NSG z zasobami, które jest ona skojarzona. |
| Reguły |Reguły ruchu przychodzącego i wychodzącego określające, jaki ruch jest dozwolony lub zablokowany. | |Zobacz hello [reguły NSG](#Nsg-rules) sekcji tego artykułu. |

> [!NOTE]
> Listy kontroli dostępu oparte na punktach końcowych i zabezpieczeń sieciowych grup nie są obsługiwane na hello wystąpienia tej samej maszyny Wirtualnej. Toouse grupy NSG i już listę ACL punktów końcowych w miejscu, najpierw usuń listę ACL punktów końcowych hello. toolearn sposób odczytać tooremove ACL hello [Zarządzanie listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu PowerShell](virtual-networks-acl-powershell.md) artykułu.
> 

### <a name="nsg-rules"></a>Reguły sieciowej grupy zabezpieczeń
Reguły NSG obejmują następujące właściwości hello:

| Właściwość | Opis | Ograniczenia | Zagadnienia do rozważenia |
| --- | --- | --- | --- |
| **Nazwa** |Nazwa reguły hello. |Musi być unikatowa w obrębie regionu hello.<br/>Może zawierać litery, cyfry, podkreślenia, kropki i łączniki.<br/>Musi zaczynać się literą lub cyfrą.<br/>Musi kończyć się literą, cyfrą lub podkreśleniem.<br/>Nie może przekraczać 80 znaków. |Może zawierać kilka reguł NSG, upewnij się, że postępuj zgodnie z konwencją nazewnictwa, która pozwala tooidentify hello funkcji reguły. |
| **Protokół** |Protokół toomatch hello reguły. |TCP, UDP lub * |Przy użyciu * tylko protokół zawiera ICMP (tylko ruch wschód-zachód), tak jak także protokołów UDP i TCP i może zmniejszyć hello liczbę potrzebnych reguł.<br/>At hello sam czas, przy użyciu * może być rozwiązaniem zbyt ogólnym, dlatego zalecane jest, że używasz * tylko wtedy, gdy jest to konieczne. |
| **Zakres portów źródłowych** |Toomatch zakres portu źródłowego hello reguły. |Numer pojedynczego portu od 1 too65535, zakres portu (przykład: 1-65535), lub * (dla wszystkich portów). |Porty źródłowe mogą być efemeryczne. Jeśli program kliencki nie korzysta z określonego portu, należy w większości przypadków użyć znaku *.<br/>Spróbuj toouse zakresy portów, jak hello możliwe tooavoid wymagają wielu reguł.<br/>Wielu portów lub zakresów portów nie można oddzielać przecinkiem. |
| **Zakres portów docelowych** |Port docelowy zakres toomatch hello reguły. |Numer pojedynczego portu od 1 too65535, zakres portu (przykład: 1-65535), lub \* (dla wszystkich portów). |Spróbuj toouse zakresy portów, jak hello możliwe tooavoid wymagają wielu reguł.<br/>Wielu portów lub zakresów portów nie można oddzielać przecinkiem. |
| **Prefiks adresu źródłowego** |Źródłowy adres prefiks lub znacznik toomatch hello reguły. |Pojedynczy adres IP (np. 10.10.10.10), podsieć IP (np. 192.168.1.0/24), [znacznik domyślny](#default-tags) lub * (dla wszystkich adresów). |Należy rozważyć użycie zakresów, znaczników domyślnych i * tooreduce hello liczbę reguł. |
| **Prefiks adresu docelowego** |Docelowy adres prefiks lub znacznik toomatch hello reguły. | Pojedynczy adres IP (np. 10.10.10.10), podsieć IP (np. 192.168.1.0/24), [znacznik domyślny](#default-tags) lub * (dla wszystkich adresów). |Należy rozważyć użycie zakresów, znaczników domyślnych i * tooreduce hello liczbę reguł. |
| **Kierunek** |Kierunek ruchu toomatch hello reguły. |Ruch przychodzący lub wychodzący. |Reguły ruchu przychodzącego i wychodzącego są przetwarzane oddzielnie w zależności od kierunku. |
| **Priorytet** |Reguły są sprawdzane hello według priorytetu. Gdy reguła ma zastosowanie, żadne inne reguły nie są sprawdzane pod kątem dopasowania. | Liczba z zakresu od 100 do 4096. | Należy rozważyć utworzenie reguł przez przeskoczenie priorytetów o 100 dla każdej reguły miejsca tooleave dla nowych zasad, które można utworzyć w hello przyszłych. |
| **Dostęp** |Typ tooapply dostępu, jeśli reguła hello. | Zezwolenie lub zablokowanie. | Należy pamiętać, że nie znaleziono reguły Zezwalaj pakietu, hello jest porzucany. |

Sieciowe grupy zabezpieczeń zawierają dwa zestawy reguł: zestaw reguł przychodzących i wychodzących. Witaj priorytety reguł muszą być unikatowe w każdym z nich. 

![Przetwarzanie reguł sieciowej grupy zabezpieczeń](./media/virtual-network-nsg-overview/figure3.png) 

Poprzedni obraz powitania pokazuje, jak są przetwarzane reguły NSG.

### <a name="default-tags"></a>Znaczniki domyślne
Znaczniki domyślne są dostarczanymi przez system identyfikatorami tooaddress kategorii adresów IP. Można użyć znaczników domyślnych w hello **prefiks adresu źródłowego** i **prefiks adresu docelowego** właściwości reguły. Istnieją trzy znaczniki domyślne, których można użyć:

* **VirtualNetwork** (Resource Manager) (**VIRTUAL_NETWORK** klasycznego): ten tag obejmuje przestrzeń adresową sieci wirtualnej hello (zakresy CIDR określone na platformie Azure), wszystkie połączone lokalne przestrzenie adresowe, a Azure sieci wirtualnych (sieci lokalne).
* **AzureLoadBalancer** (model usługi Resource Manager) (**AZURE_LOADBALANCER** — model klasyczny): ten znacznik określa moduł równoważenia obciążenia infrastruktury platformy Azure. Hello tag tłumaczy tooan pochodzą IP centrum danych Azure, w którym sondy kondycji Azure.
* **Internet** (Resource Manager) (**INTERNET** klasycznego): ten tag oznacza hello przestrzeń adresów IP, który znajduje się poza hello sieci wirtualnej i jest dostępny w publicznym Internecie. Witaj zakres obejmuje hello [publiczną przestrzeń adresów IP należącą do Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Reguły domyślne
Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych. Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany najniższy priorytet hello, mogą być zastąpione przez hello utworzonych reguł. 

reguły domyślne Hello Zezwalaj i nie zezwalaj na ruch:
- **Sieć wirtualna:** ruch pochodzący z sieci wirtualnej i kończący się w niej jest dozwolony zarówno w kierunku przychodzącym, jak i wychodzącym.
- **Internet:** ruch wychodzący jest dozwolony, ale ruch przychodzący jest blokowany.
- **Moduł równoważenia obciążenia:** Zezwalaj Azure kondycji hello tooprobe usługi równoważenia obciążenia maszyn wirtualnych i wystąpień ról. Jeśli nie używa się zestawu z równoważeniem obciążenia, tę zasadę można zastąpić.

**Reguły domyślne ruchu przychodzącego**

| Nazwa | Priorytet | Źródłowy adres IP | Port źródłowy | Docelowy adres IP | Port docelowy | Protokół | Dostęp |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | Zezwalaj |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | Zezwalaj |
| DenyAllInBound |65500 | * | * | * | * | * | Zablokuj |

**Domyślne reguły ruchu wychodzącego**

| Nazwa | Priorytet | Źródłowy adres IP | Port źródłowy | Docelowy adres IP | Port docelowy | Protokół | Dostęp |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | Zezwalaj |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | Zezwalaj |
| DenyAllOutBound | 65500 | * | * | * | * | * | Zablokuj |

## <a name="associating-nsgs"></a>Kojarzenie sieciowych grup zabezpieczeń
Możesz skojarzyć tooVMs NSG, karty sieciowe i podsieci, w zależności od modelu wdrażania hello, którego używasz, w następujący sposób:

* **Maszyna wirtualna (klasyczna tylko):** reguły zabezpieczeń są stosowane tooall ruchu do/z hello maszyny Wirtualnej. 
* **Karta sieciowa (tylko Resource Manager):** reguły zabezpieczeń są stosowane tooall ruchu do/z hello kart hello grupa NSG jest skojarzona z. Na maszynie Wirtualnej z wieloma kartami Sieciowymi, można zastosować różne (lub hello sam) tooeach NSG kart pojedynczo. 
* **Podsieć (Resource Manager i model klasyczny):** reguły zabezpieczeń są stosowane tooany ruchu do/z wszystkie zasoby podłączone toohello sieci wirtualnej.

Można skojarzyć różne grupy NSG tooa maszyny Wirtualnej (lub karty Sieciowej, w zależności od modelu wdrażania hello) i hello podsieci, która karta sieciowa lub maszyna wirtualna jest połączony. Reguły zabezpieczeń ruchu zastosowane toohello według priorytetu w poszczególnych grupach NSG w powitania po kolejności:

- **Ruch przychodzący**

  1. **Grupa NSG stosowana toosubnet:** NSG podsieci ma pasującego ruchu toodeny reguły, hello jest porzucany.

  2. **Grupa NSG stosowana tooNIC** (Resource Manager) lub maszyna wirtualna (klasyczna): Jeśli NSG VM\NIC ma zgodną regułę, która nie zezwala na ruch, porzucenia pakietów na powitania VM\NIC, nawet jeśli NSG podsieci ma zgodną regułę, która zezwala na ruch.

- **Ruch wychodzący**

  1. **Grupa NSG stosowana tooNIC** (Resource Manager) lub maszyna wirtualna (klasyczna): Jeśli VM\NIC NSG zgodną regułę, która nie zezwala na ruch, porzucenia pakietów.

  2. **Grupa NSG stosowana toosubnet:** Jeśli NSG podsieci ma zgodną regułę, która nie zezwala na ruch, porzucenia pakietów, nawet jeśli VM\NIC NSG ma zgodną regułę, która zezwala na ruch.

> [!NOTE]
> Mimo że można skojarzyć tylko jednej grupy NSG tooa podsieć maszyny Wirtualnej i/lub kart; możesz skojarzyć hello tej samej grupy NSG tooas wiele zasobów ma.
>

## <a name="implementation"></a>Wdrażanie
Grupy NSG można wdrożyć w hello Resource Manager i klasycznych modeli wdrażania przy użyciu hello następujące narzędzia:

| Narzędzie wdrażania | Wdrożenie klasyczne | Resource Manager |
| --- | --- | --- |
| Portal Azure   | Tak | [Tak](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Tak](virtual-networks-create-nsg-classic-ps.md) | [Tak](virtual-networks-create-nsg-arm-ps.md) |
| Interfejs wiersza polecenia platformy Azure **V1**   | [Tak](virtual-networks-create-nsg-classic-cli.md) | [Tak](virtual-networks-create-nsg-cli-nodejs.md) |
| Interfejs wiersza polecenia platformy Azure **V2**   | Nie | [Tak](virtual-networks-create-nsg-arm-cli.md) |
| Szablon usługi Azure Resource Manager   | Nie  | [Tak](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planowanie
Przed wdrożeniem grup NSG należy hello tooanswer następujące pytania:

1. Jakich typów zasobów chcesz toofilter tooor ruchu z? Możesz podłączyć zasoby, takie jak karty sieciowe, (model usługi Resource Manager), maszyny wirtualne (model klasyczny), usługi Cloud Services, środowiska usług aplikacji i zestawy skalowania maszyn wirtualnych. 
2. Czy zasoby hello ma toofilter ruch do i z połączonych toosubnets w istniejących sieciach wirtualnych?

Aby uzyskać więcej informacji na temat planowania zabezpieczeń sieciowych na platformie Azure, przeczytaj hello [usługi w chmurze i zabezpieczeń sieciowych](../best-practices-network-security.md) artykułu. 

## <a name="design-considerations"></a>Zagadnienia dotyczące projektowania
Jeśli znasz już odpowiedzi hello pytania toohello w hello [Planowanie](#Planning) Przejrzyj następujące sekcje przed zdefiniowaniem grup NSG hello:

### <a name="limits"></a>Limity
Istnieją ograniczenia toohello liczbę grup NSG mogą mieć w ramach subskrypcji i liczbę reguł na grupę NSG. więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.

### <a name="vnet-and-subnet-design"></a>Projekt sieci wirtualnej i podsieci
Ponieważ grupy NSG mogą zostać zastosowane toosubnets, można zminimalizować hello liczbę grup NSG przez grupowanie zasobów według podsieci i zastosowanie grup NSG toosubnets.  Jeśli zdecydujesz się tooapply toosubnets grup NSG, może się okazać, że istniejące sieci wirtualne i podsieci nie zostały zdefiniowane z grupy NSG na uwadze. Może muszą nowych sieci wirtualnych i podsieci toosupport toodefine projektu NSG i wdrażanie nowych zasobów tooyour nowych podsieci. Następnie można zdefiniować toomove strategii migracji istniejących zasobów toohello nowych podsieci. 

### <a name="special-rules"></a>Reguły specjalne
Jeśli zablokujesz ruchu dozwolonego przez reguły hello infrastruktury nie może komunikować się z podstawowymi usługami Azure:

* **Wirtualny adres IP węzła hosta hello:** podstawowe usługi infrastruktury, takie jak DHCP, DNS i monitorowanie kondycji są realizowane za pośrednictwem hello hosta wirtualnego adresu IP 168.63.129.16. Ten publiczny adres IP należy tooMicrosoft i jest hello jedynym zwirtualizowanym adresem IP w tym celu używany we wszystkich regionach. Ten adres IP mapuje toohello fizycznego adresu IP hello maszyny serwera (węzła hosta) obsługującego hello maszyny Wirtualnej. węzeł hosta Hello działa jako hello przekazywania DHCP, hello DNS cyklicznego programu rozpoznawania nazw i źródła sondy hello hello obciążenia sondy kondycji modułu równoważenia i sondy kondycji komputera hello. Adres IP toothis komunikacji nie jest atak.
* **Licencjonowanie (usługa zarządzania kluczami):** obrazy systemu Windows uruchomione na maszynach wirtualnych muszą być licencjonowane. tooensure licencjonowania, żądanie zostanie wysłana toohello serwerów hosta usługi zarządzania kluczami, które obsługi tych kwerend. Witaj żądań wychodzące przez port 1688.

### <a name="icmp-traffic"></a>Ruch protokołu ICMP
Witaj bieżące reguły NSG uwzględniają tylko protokoły *TCP* lub *UDP*. Nie ma określonego znacznika dla protokołu *ICMP*. Jednak ruch protokołu ICMP jest dozwolone w ramach sieci wirtualnej przez regułę domyślną AllowVNetInBound hello, umożliwiający tooand ruchu z dowolnego portu i protokołu w ramach hello sieci wirtualnej.

### <a name="subnets"></a>Podsieci
* Należy wziąć pod uwagę hello liczba warstw, której wymaga obciążenie. Każdy warstwę można wyizolować przy użyciu podsieci, z podsiecią toohello grupa NSG stosowana. 
* Jeśli potrzebujesz tooimplement podsieć dla bramy sieci VPN lub obwodu ExpressRoute, czy **nie** zastosować grupy NSG toothat podsieci. Jeśli tak zrobisz, może nie działać łączność pomiędzy różnymi sieciami wirtualnymi lub między różnymi lokalizacjami. 
* Tooimplement urządzenie wirtualne sieci (NVA), należy połączyć hello NVA tooits własnej podsieci i utworzyć tooand trasy zdefiniowane przez użytkownika (przez) z hello NVA. Można wdrożyć na poziomie podsieci NSG toofilter ruch do i z tej podsieci. więcej informacji na temat Udr odczytu hello toolearn [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) artykułu.

### <a name="load-balancers"></a>Moduły równoważenia obciążenia
* Należy rozważyć hello obciążenia równoważenia i adres sieciowy reguły translation (NAT) dla każdego modułu równoważenia obciążenia używane przez każdego z obciążeń. Reguły NAT są tooa powiązane puli zaplecza, która zawiera karty sieciowe (Resource Manager) lub wystąpień roli usługi w chmurze/VMs (klasyczne). Należy rozważyć utworzenie grupy NSG dla każdej puli zaplecza, co pozwala tylko na ruch mapowany za pomocą reguł hello zaimplementowana w hello usługi równoważenia obciążenia. Utworzenie grupy NSG dla każdej puli zaplecza gwarantuje ruchu przychodzącego puli zaplecza toohello bezpośrednio (a nie za pośrednictwem usługi równoważenia obciążenia hello), jest również filtrowany.
* W przypadku wdrożeń klasycznych możesz utworzyć punkty końcowe, które mapują porty w tooports usługi równoważenia obciążenia na maszynach wirtualnych lub wystąpień roli. Można również utworzyć osobisty publiczny moduł równoważenia obciążenia za pomocą usługi Resource Manager. Witaj port docelowy dla ruchu przychodzącego jest rzeczywistym portem hello hello maszyny Wirtualnej lub wystąpienia roli, nie port hello udostępnianych przez usługi równoważenia obciążenia. Witaj, port źródłowy i adres dla hello toohello połączenia, które maszyna wirtualna jest port i adres na hello komputera zdalnego w hello Internet, a nie hello port i adres udostępniane przez usługi równoważenia obciążenia hello.
* Podczas tworzenia grup NSG toofilter ruchu przechodzącego przez wewnętrzny moduł równoważenia obciążenia (ILB) hello źródła portu i zakres adresów dotyczą pochodzą z hello pochodzące z komputera, nie hello modułu równoważenia obciążenia. zakres adres i port docelowy Hello są hello komputera docelowego, nie hello modułu równoważenia obciążenia.

### <a name="other"></a>Inne
* Listy kontroli dostępu oparte na punktach końcowych (ACL) i grupy NSG nie są obsługiwane na powitania wystąpienia tej samej maszyny Wirtualnej. Toouse grupy NSG i już listę ACL punktów końcowych w miejscu, najpierw usuń listę ACL punktów końcowych hello. Aby uzyskać informacje na temat tooremove jako punkt końcowy listy kontroli dostępu, zobacz hello [Zarządzanie listy ACL punktu końcowego](virtual-networks-acl-powershell.md) artykułu.
* W Menedżerze zasobów służy tooa grupy NSG skojarzonej karty Sieciowej dla maszyn wirtualnych z wielu kart sieciowych tooenable Zarządzanie (dostęp zdalny) na podstawie dla karty Sieciowej. Kojarzenie unikatowych grup NSG tooeach kart interfejsu Sieciowego umożliwia rozdzielenie typów ruchu sieciowego między kart sieciowych.
* Podobne toohello stosowania równoważenia obciążenia, podczas filtrowania ruchu z innych sieci wirtualnych, należy użyć zakresu adresów źródłowych hello hello komputera zdalnego nie hello bramy łączącej hello sieci wirtualnych.
* Wiele usług platformy Azure nie może być tooVNets połączonych. Zasobów platformy Azure nie jest połączony tooa sieci wirtualnej, nie można użyć grupy NSG toofilter ruchu toohello zasobów.  Przeczytaj dokumentację hello hello usług możesz użyć toodetermine, czy usługa hello może być tooa połączonych sieci wirtualnej.

## <a name="sample-deployment"></a>Przykładowe wdrożenie
Aplikacja hello tooillustrate hello informacji w tym artykule, należy wziąć pod uwagę typowym scenariuszem stosowania dwie warstwy pokazano na poniższej ilustracji hello:

![Sieciowe grupy zabezpieczeń](./media/virtual-network-nsg-overview/figure1.png)

Jak pokazano na diagramie hello, hello *Web1* i *sieci Web 2* maszyny wirtualne są połączone toohello *frontonu* podsieci i hello *DB1* i *Bazy danych DB2* maszyny wirtualne są połączone toohello *zaplecza* podsieci.  Obie podsieci są częścią hello *TestVNet* sieci wirtualnej. składniki aplikacji Hello każdy uruchomiony w tooa maszyny Wirtualnej Azure połączone sieci wirtualnej. Scenariusz Hello ma hello następujące wymagania:

1. Rozdzielenie ruchu między hello sieci WEB i serwerami bazy danych.
2. Zasady przekazywania ruchu, z hello serwerów sieci web tooall usługi równoważenia obciążenia na porcie 80 równoważenia obciążenia.
3. Załadować równoważenia NAT reguł do przodu ruchu przychodzącego do modułu równoważenia obciążenia hello na porcie 50001 tooport 3389 na powitania serwera WEB1 maszyny Wirtualnej.
4. Nie toohello dostęp do maszyn wirtualnych frontonu lub zaplecza z hello Internetu, z wyjątkiem wymagań 2 i 3.
5. Nie wychodzący dostęp do Internetu z serwerów sieci WEB lub DB hello.
6. Dostęp z podsieci frontonu hello jest dozwolony tooport 3389 dowolny serwer sieci web.
7. Dostęp z podsieci frontonu hello jest dozwolony tooport 3389 dowolnego serwera bazy danych.
8. Dostęp z podsieci frontonu hello jest dozwolony tooport 1433 wszystkie serwery bazy danych.
9. Rozdzielenie ruchu administracyjnego (port 3389) i ruchu bazy danych (1433) na różne karty sieciowe na serwerach DB.

Wymagania 1 – 6 (z wyjątkiem wymagania 3 i 4) są wszystkie spacje toosubnet zamkniętej. Witaj następujące grupy NSG wymagań hello poprzedniej, przy jednoczesnym zmniejszeniu hello liczbę grup NSG wymagane:

### <a name="frontend"></a>FrontEnd
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | Zezwalaj | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | Zezwalaj | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | Zablokuj | 300 | Internet | * | * | * | TCP |

**Reguły ruchu wychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |Zablokuj |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Zablokuj | 100 | Internet | * | * | * | * |

**Reguły ruchu wychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Zablokuj | 100 | * | * | Internet | * | * |

Witaj następujące grupy NSG są tworzone i skojarzone tooNICs w hello następujące maszyny wirtualne:

### <a name="web1"></a>WEB1
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | Zezwalaj | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | Zezwalaj | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> zakres adresów źródła Hello hello poprzednie reguły to **Internet**, nie hello wirtualnego adresu IP dla modułu równoważenia obciążenia hello. port źródłowy Hello jest *, a nie 500001. Reguły NAT dla usługi równoważenia obciążenia nie są hello taki sam jak reguł zabezpieczeń grupy NSG. Reguły zabezpieczeń NSG są zawsze powiązane toohello oryginalnym źródłem i ostatecznym miejscem przeznaczenia ruchu, **nie** hello równoważenia obciążenia między hello dwa. 
> 
> 

### <a name="web2"></a>WEB2
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | Zablokuj | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | Zezwalaj | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>Serwery DB (karta sieciowa zarządzania)
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | Zezwalaj | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>Serwery DB (karta sieciowa ruchu bazy danych)
**Reguły ruchu przychodzącego**

| Reguła | Dostęp | Priorytet | Zakres adresów źródłowych | Port źródłowy | Zakres adresów docelowych | Port docelowy | Protokół |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | Zezwalaj | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Ponieważ niektóre z grup NSG hello są skojarzone tooindividual kart sieciowych, reguły hello są zasoby wdrażane za pomocą Menedżera zasobów. Reguły są łączone dla podsieci i karty sieciowej w zależności od sposobu ich kojarzenia. 

## <a name="next-steps"></a>Następne kroki
* [Wdrażanie sieciowych grup zabezpieczeń (model usługi Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [Wdrażanie sieciowych grup zabezpieczeń (model klasyczny)](virtual-networks-create-nsg-classic-ps.md).
* [Manage NSG logs](virtual-network-nsg-manage-log.md) (Zarządzanie dziennikami sieciowej grupy zabezpieczeń).
* [Rozwiązywanie problemów z sieciowymi grupami zabezpieczeń] (virtual-network-nsg-troubleshoot-portal.md)
