---
title: "aaaDesigning infrastrukturę sieci, odzyskiwania po awarii | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono zagadnienia dotyczące projektowania sieci dla usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Projektowanie sieci w celu odzyskiwania po awarii

W tym artykule jest specjalistów ukierunkowanej tooIT który są odpowiedzialne za projektowania, wdrażania i obsługi ciągłość prowadzenia działalności biznesowej i infrastruktury (BCDR) odzyskiwania po awarii i którzy potrzebują tooleverage toosupport Microsoft Azure lokacji Recovery (ASR) i rozszerzenie usług ich BCDR. W tym artykule omówiono kwestie praktyczne w struktury sieci w lokacji odzyskiwania po awarii, należy go Azure lub innej lokalnej lokacji. 

## <a name="overview"></a>Omówienie
[Odzyskiwanie lokacji Azure (ASR)](https://azure.microsoft.com/services/site-recovery/) jest usługą Microsoft Azure, która organizuje hello ochrony i odzyskiwania zwirtualizowanych aplikacji na potrzeby odzyskiwania (BCDR) po awarii ciągłości biznesowej. Ten dokument jest zamierzone tooguide hello czytnika hello proces projektowania sieci hello koncentrujących się na zaprojektowanie zakresów adresów IP i podsieci w lokacji odzyskiwania po awarii hello, podczas replikowania maszyn wirtualnych (VM) przy użyciu usługi Site Recovery.

Ponadto w tym artykule przedstawiono, jak Usługa Site Recovery umożliwia zaprojektowanie i Implementowanie usług BCDR toosupport wielooddziałowości wirtualnego centrum danych w czasie testu lub po awarii.

W świecie, w której wszyscy oczekuje łączności 24/7, ma większe znaczenie niż kiedykolwiek tookeep infrastruktury i aplikacji do pracy. Witaj ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii (BCDR) służy składniki toorestore nie powiodło się więc hello organizacji można szybko przywrócić normalne działanie. Tworzenie toodeal strategii odzyskiwania po awarii, ze zdarzeniami mało prawdopodobne, niszczące jest bardzo trudne. To powodu toohello trudności związanego z używaniem przewidywania przyszłych hello, szczególnie ze zdarzeń tooimprobable i hello wysokiego kosztu tooprovide odpowiednie środki ochrony przed dalekosiężną catastrophes.

Kluczowe znaczenie podczas planowania BCDR, cel czas odzyskiwania (RTO) i cel punktu odzyskiwania (RPO) muszą być zdefiniowane jako część planu odzyskiwania po awarii. W przypadku awarii uderzenia powitania klienta centrum danych, za pomocą usługi Azure Site Recovery, klienci mogą szybko (RTO niski) Przełącz do trybu online ich replikowanych maszyn wirtualnych znajdujących się w centrum danych dodatkowej hello lub Microsoft Azure z utraty minimalną ilość danych (RPO niski).

Tryb failover jest możliwe dzięki ASR początkowo kopiuje wyznaczonych maszyn wirtualnych z hello danych podstawowych center toohello pomocniczego Centrum lub tooAzure (w zależności od scenariusza hello), a następnie okresowo odświeża hello replik. Podczas planowania infrastruktury projektu sieci należy traktować jako potencjalne "wąskie gardło", które mogą uniemożliwić z firmy spotkania RTO i cele odzyskiwania.  

Gdy administratorzy planują toodeploy rozwiązanie odzyskiwania po awarii, jest jedno z pytań klucza hello w ich umysły, jak hello maszyny wirtualnej będzie dostępny po zakończeniu pracy awaryjnej hello. Funkcja automatycznego odzyskiwania systemu umożliwia hello administratora toochoose hello sieci toowhich maszyny wirtualnej będzie połączonych tooafter trybu failover. Jeśli lokacja główna hello jest Azure lub jest ona lokalna lokacja zarządzana przez serwer programu VMM, a następnie jest to osiągane przez przy użyciu mapowania sieci. Dowiedz się więcej o [mapowanie sieci w Azure tooAzure DR](site-recovery-network-mapping-azure-to-azure.md) i [mapowanie sieci z programu VMM](site-recovery-network-mapping.md)


Podczas projektowania sieci hello hello odzyskiwania lokacji, hello administrator ma dwie opcje:

* Użyj różnych zakresów adresów IP dla sieci hello w lokacji odzyskiwania. W tym scenariuszu hello maszynę wirtualną po pracy awaryjnej pobierze nowy adres IP i administratora hello byłyby toodo aktualizacji DNS. 
* Użyj tego samego zakresu adresów IP dla sieci hello hello odzyskiwania lokacji. W niektórych scenariuszach Administratorzy preferować adresy IP hello tooretain, które mogą się w lokacji głównej hello nawet po hello w tryb failover. W przypadku normalnych administrator musi tooupdate hello tras tooindicate hello nowej lokalizacji hello adresów IP. Jednak w scenariuszu hello wdrożonym rozciągnięty podsieci między hello głównej i lokacji odzyskiwania hello, zachowując hello adresów IP dla maszyn wirtualnych hello staje się atrakcyjną opcję. Rozciąganie podsieci z tooan sieci lokalnej sieci platformy Azure lub między dwiema sieciami Azure nie jest możliwe.  

Gdy administratorzy planują toodeploy rozwiązanie odzyskiwania po awarii, jedno z pytań klucza hello ich pamiętać jest sposób hello aplikacje będą dostępne po zakończeniu pracy awaryjnej hello. Nowoczesne aplikacje prawie zawsze są zależne od sieci toosome stopień, więc fizycznie przeniesienie usługi z jednej lokacji tooanother reprezentuje żądanie sieciowe. Istnieją dwa sposoby główne, które ten problem wynika z rozwiązania w zakresie odzyskiwania po awarii. Pierwszym sposobem Hello jest toomaintain stałe adresy IP. Pomimo usług hello przenoszenia i hello znajdujące się w różnych lokalizacjach fizycznych serwerów hosta aplikacji zająć hello konfiguracji adresu IP z nimi toohello nowej lokalizacji. drugi podejście Hello obejmuje całkowicie zmiana adresu IP hello podczas przejścia hello na powitania odzyskanej lokacji. Każde podejście jest kilka zmian implementacji, które zestawiono poniżej.

Podczas projektowania sieci hello hello odzyskiwania lokacji, hello administrator ma dwie opcje:

## <a name="option-1-retain-ip-addresses"></a>Opcja 1: Zachowaj adresów IP
Z punktu widzenia procesu odzyskiwania po awarii przy użyciu stałe adresy IP jest wyświetlany toobe hello najprostszą metodą tooimplement, ale składa się z liczbą potencjalne problemy, które w praktyce hello najmniej popularnych podejście. Usługa Azure Site Recovery zapewnia możliwość hello adresy IP hello tooretain we wszystkich scenariuszach. Przed tooretain IP jedną decyduje, odpowiedni należy zwrócić uwagę ograniczenia toohello, który nakłada się na powitania możliwości trybu failover. Daj nam przyjrzeć się hello czynników, które mogą pomóc Ci toomake adresy IP tooretain decyzji, czy nie. Można to osiągnąć na dwa sposoby, za pomocą rozciągnięty podsieci lub wykonując awarię pełne podsieci.

### <a name="stretched-subnet"></a>Rozciągnięty podsieci
W tym miejscu podsieci hello jest udostępniana jednocześnie w serwerze podstawowym i lokalizacje odzyskiwania po awarii. Proste oznacza to, można przenieść serwer i jego drugiej witryny toohello konfiguracji adresu IP (warstwy 3) i sieci hello będzie przekierowywać hello ruchu toohello nową lokalizację automatycznie. Jest to prosta toodeal z z perspektywy serwera, ale ma wiele wyzwań:

* Z punktu widzenia warstwy 2 (warstwę łącza danych) będzie wymagać sprzęt sieciowy, którym może zarządzać rozciągnięty sieci VLAN, ale to stała mniejszy problem teraz jest powszechnie dostępna. problem drugi i trudniejsze Hello jest rozciągnięty hello domeny potencjalnych błędów hello sieci VLAN jest rozszerzony witryn tooboth zasadniczo staje się pojedynczym punktem awarii. Jest to mało prawdopodobnego zdarzenia, miało to miejsce, że emisji storm uruchomiony, ale nie może być izolowane. Możemy znaleźć mieszanych opinie o tym problemie ostatniego i umieścić wiele implementacji pomyślne również "nigdy nie wprowadzimy tej technologii tutaj".
* Rozciągnięty podsieci nie jest możliwe, jeśli używasz Microsoft Azure jako lokacja DR hello.

### <a name="subnet-failover"></a>Tryb failover podsieci
Jest możliwe tooimplement podsieci trybu failover tooobtain hello korzyści hello rozciągnięty podsieci rozwiązania opisane powyżej bez rozciąganie hello podsieci w wielu lokacjach. W tym miejscu wszelkie danej podsieci będą obecne w lokacji 1 lub 2 lokacji, ale nigdy nie w obu lokacjach jednocześnie. W kolejności toomaintain hello przestrzeń adresów IP w przypadku hello pracy awaryjnej, możliwe jest tooprogrammatically Rozmieść dla podsieci infrastruktury router hello hello toomove z tooanother jednej lokacji. W hello scenariusza trybu failover, czy podsieci przenoszenia z hello skojarzone chronionych maszyn wirtualnych. podejście toothis główną wadą Hello jest w przypadku hello awarii, ma toomove hello całej podsieci, które mogą być OK, ale może wpływać na powitania trybu failover szczegółowości zagadnienia.

Przeanalizujmy jak fikcyjnej organizacji o nazwie Contoso jest możliwe tooreplicate lokalizacji odzyskiwania maszyn wirtualnych tooa podczas awarii hello całej podsieci. Najpierw przedstawiono, jak firma Contoso jest możliwe toomanage swoje podsieci podczas replikowania maszyn wirtualnych między dwiema lokalnymi lokalizacji, a następnie omówimy, jak podsieć trybu failover działa, kiedy [Azure jest używana jako lokacja odzyskiwania po awarii hello](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Tryb failover z lokalnymi tooAzure 
Odzyskiwanie lokacji Azure (ASR) umożliwia Azure toobe używany jako lokacja odzyskiwania po awarii dla maszyn wirtualnych.  

Przeanalizujmy scenariusz, w którym fikcyjnej firmy o nazwie Woodgrove Bank ma infrastruktury lokalnej hosting ich linii aplikacji biznesowych i obsługujące ich aplikacji dla urządzeń przenośnych na platformie Azure. Łączność między maszynami wirtualnymi banku Woodgrove na serwerach Azure i lokalnymi są udostępniane przez lokacja lokacja (S2S) wirtualnej sieci prywatnej (VPN) lub usługi ExpressRoute. Połączenia VPN S2S umożliwia banku Woodgrove sieci wirtualnej Azure toobe widoczne jako rozszerzenie banku Woodgrove lokalnej sieci. Tej komunikacji jest włączana przez sieci VPN S2S między krawędzi banku Woodgrove i sieć wirtualna platformy Azure. Teraz Woodgrove chce toouse ASR tooreplicate jego obciążeń uruchomionych tooanother regionu Azure podstawowego region platformy Azure. Ta opcja spełnia potrzeby hello Woodgrove, co chce ekonomiczny opcji odzyskiwania po awarii i może toostore dane w środowiskach chmury publicznej. Woodgrove ma toodeal z aplikacje i konfiguracje, które są zależne od stałe adresy IP, dlatego mają adresy IP tooretain wymagania dotyczące aplikacji po przełączeniu za pośrednictwem tooanother regionu w systemie Azure.

Woodgrove zdecydował tooassign adresów IP z adres IP zakresu (172.16.1.0/24, 172.16.2.0/24) tooits zasobów działające na platformie Azure.

Dla tooreplicate stanie toobe Woodgrove jego tooAzure maszyn wirtualnych przy zachowaniu hello adresy IP, sieci wirtualnej platformy Azure musi toobe utworzony. Należy go rozszerzenie sieci lokalnej hello, dzięki czemu aplikacje mogą w tryb failover z tooAzure lokacji lokalne powitania bezproblemowo Azure umożliwia tooadd lokacja lokacja, a także punkt lokacja sieci VPN łączności toohello sieci wirtualne utworzone na platformie Azure. Podczas konfigurowania połączenia lokacja lokacja, sieć platformy Azure pozwala tooroute ruchu toohello lokalnej lokalizacji (Azure wywołuje ona sieci lokalnej) tylko wtedy, gdy zakres adresów IP hello różni się od zakresu adresów IP lokalne powitania, ponieważ nie Azure Obsługa rozciąganie podsieci.  Oznacza to, że jeśli 192.168.1.0/24 podsieci lokalnej, nie można dodać 192.168.1.0/24 sieci lokalnej w hello sieć platformy Azure. Oczekiwany jest Azure nie może ustalić, czy brak aktywnych maszyn wirtualnych w podsieci hello i podsieci hello jest tworzony tylko do celów odzyskiwania po awarii. Program toobe toocorrectly może kierować ruchem sieciowym poza podsieci hello sieć platformy Azure w sieci hello i sieci lokalnej hello nie może powodować konfliktu.

![Przed podsieci trybu Failover](./media/site-recovery-network-design/network-design7.png)

Przed trybu failover

toohelp Woodgrove spełnić ich wymagań biznesowych, potrzebujemy hello tooimplement przepływów pracy po:

* Tworzenie dodatkowych sieci, Daj nam go wywoływać sieci odzyskiwania, w którym maszyny wirtualne przełączona w tryb failover hello zostałyby utworzone.
* tooensure czy hello IP dla maszyny Wirtualnej jest zachowywane po przejściu w tryb failover, przejdź na kartę Konfiguracja toohello we właściwościach maszyny Wirtualnej, określ hello tego samego adresu IP, który hello maszyny Wirtualnej ma lokalnego i kliknij przycisk Zapisz. Gdy hello wirtualna przeszła w tryb failover, usługi Azure Site Recovery przypisze hello udostępnionej maszyny wirtualnej toohello IP.

![Właściwości sieci](./media/site-recovery-network-design/network-design8.png)

Po wyzwoleniu hello trybu failover i hello maszyny wirtualne są tworzone w hello sieci odzyskiwania hello żądanego protokołu IP, łączności sieciowej toothis można ustanowić za pomocą [tooVnet sieci wirtualnej połączenia](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Jeśli jest to wymagane, ta akcja umożliwia pisanie skryptów.  Jak wspomniano w poprzedniej sekcji hello o pracy awaryjnej podsieci, nawet w przypadku hello tooAzure pracy awaryjnej tras czy toobe odpowiednio zmodyfikowano tooreflect tooAzure teraz został przeniesiony w tym 192.168.1.0/24.

![Po podsieci w tryb Failover](./media/site-recovery-network-design/network-design9.png)

Po pracy awaryjnej

Jeśli nie ma sieci Azure, jak pokazano na rysunku hello powyżej. Po hello w tryb failover, można utworzyć połączenia sieci vpn toosite lokacji między "Lokacji głównej" i "Sieć odzyskiwania".  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Tryb failover tooa dodatkowej lokalnej lokacji
Daj nam Spójrz na scenariusz gdy chcemy, aby zachować hello IP każdego hello maszyn wirtualnych i hello awaryjnej ukończyć ze sobą podsieci. lokacja główna Hello ma aplikacji uruchomionych w podsieci 192.168.1.0/24. W przypadku pracy awaryjnej hello wszystkich hello maszyn wirtualnych, które są częścią tej podsieci będzie można przełączyć toohello odzyskiwania lokacji i zachować swoje adresy IP. Trasy będą miały toobe zmodyfikować odpowiednio fakt hello tooreflect wszystkich maszyn wirtualnych hello należących toosubnet 192.168.1.0/24 teraz przeniósł toohello odzyskiwania lokacji.

W hello następujące hello ilustracji tras między lokacji głównej i lokacji odzyskiwania, trzeci lokacji i lokacji głównej i trzeci lokacji i lokacji odzyskiwania będzie mieć toobe odpowiednio zmodyfikowane.

następujące obrazy Hello zawiera podsieci hello przed hello trybu failover. 192.168.0.1/24 podsieci jest aktywna na powitania lokacji głównej przed hello trybu failover i staje się aktywny, hello lokacja odzyskiwania po hello w tryb failover

![Przed trybu Failover](./media/site-recovery-network-design/network-design2.png)

Przed trybu failover

Obraz powitania poniżej przedstawiono sieci i podsieci po pracy awaryjnej.

![Po pracy awaryjnej](./media/site-recovery-network-design/network-design3.png)

Po pracy awaryjnej

W lokacji dodatkowej jest lokalnym i używasz toomanage serwera VMM następnie podczas włączania ochrony określonej maszyny wirtualnej, funkcja automatycznego odzyskiwania systemu przyzna zasobów sieciowych, zgodnie z toohello następującego przepływu pracy:

* Funkcja automatycznego odzyskiwania systemu przydziela adres IP dla każdego interfejsu sieciowego na maszynie wirtualnej hello z hello puli statycznych adresów IP zdefiniowanych na powitania odpowiednich sieci dla każdego wystąpienia programu System Center VMM.
* Jeśli hello administrator definiuje hello tego samego adresu IP a pulę adresów dla sieci hello w lokacji odzyskiwania hello jako że hello puli adresów IP z hello sieci w lokacji głównej hello, podczas przydzielania hello IP address toohello repliki maszyny wirtualnej funkcja automatycznego odzyskiwania systemu może przydzielić hello takie same Adres IP co hello podstawowej maszyny wirtualnej.  adres IP Hello jest zarezerwowany w programie VMM, ale nie ustawiona jako adresu IP trybu failover na hoście funkcji Hyper-v hello. IP trybu failover na hoście funkcji Hyper-v jest ustawiony przed hello trybu failover.


W przypadku hello tego samego adresu IP nie jest dostępny, funkcja automatycznego odzyskiwania systemu może przydzielić niektóre inne dostępny adres IP z puli adresów IP hello zdefiniowane.

Po powitalne maszyny Wirtualnej jest włączona w celu ochrony można użyć następujących przykładowy skrypt tooverify hello IP, która została przydzielona toohello maszyny wirtualnej. Witaj tego samego adresu IP może ustawić jako adresu IP trybu Failover i przypisane toohello maszyny Wirtualnej na powitania przejścia w tryb failover:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> W scenariuszu hello których na maszynach wirtualnych jest używany protokół DHCP zarządzania hello adresów IP jest całkowicie poza kontrolą hello automatycznego. Administrator może tooensure zaspokajającego hello obsługujących hello adresów IP serwera DHCP na powitania odzyskiwania lokacji z hello tego samego zakresu, jak hello lokacji głównej.
>
>



## <a name="option-2-changing-ip-addresses"></a>Opcja 2: Zmiana adresów IP
Takie podejście jest prawdopodobnie hello toobe najbardziej rozpowszechnionych oparte na co zaobserwowano. Trwa zmiana adresu IP hello każdej maszyny wirtualnej, który jest używany w tryb failover hello formy hello. Wadą tego podejścia wymaga hello przychodzących sieci too'learn "tej aplikacji hello, który był w IPx wynosi teraz IPy. Nawet jeśli IPx i IPy nazwy logiczne, wpisy DNS ma zwykle toobe zmienione lub opróżnionych w całej sieci hello i wpisów pamięci podręcznej w tabelach sieci ma toobe zaktualizowane lub opróżnione, w związku z tym przestoju może być widoczny w zależności od sposobu infrastruktura DNS hello ma została zainstalowana. Te problemy można zminimalizować przy użyciu niskich wartości TTL w przypadku hello aplikacji intranetowych i [Menedżer ruchu Azure przy użyciu usługi ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) Internetu aplikacje oparte na systemie

### <a name="changing-hello-ip-addresses---illustration"></a>Zmiana adresów IP hello - ilustracji
Daj nam przyjrzeć się scenariusz hello planowanego toouse różnych adresów IP między hello głównej i lokacji odzyskiwania hello. W hello poniższy przykład mamy są również trzeci witrynie, gdzie można uzyskać dostępu do aplikacji hello znajdującej się w lokacji podstawowej lub odzyskiwania.

![Różne IP — przed trybu Failover](./media/site-recovery-network-design/network-design10.png)


W powyższym obraz powitania są niektóre aplikacje hostowane w podsieci 192.168.1.0/24 podsieci w lokacji głównej hello i zostały one skonfigurowane toocome się w lokacji odzyskiwania hello w podsieci 172.16.1.0/24 po przejściu w tryb failover. Trasy połączeń i sieci VPN zostały skonfigurowane odpowiednio tak, aby wszystkie trzy witryny mają dostęp do siebie.

Jako obraz powitania poniżej przedstawia po awarii jednego lub więcej aplikacji zostaną przywrócone w hello odzyskiwania podsieci. W takim przypadku nie jesteśmy w całej podsieci ograniczonego toofailover hello na powitania tym samym czasie. Zmiany nie są wymagane tooreconfigure trasy sieci VPN lub sieci. Tryb failover i niektóre aktualizacje DNS będzie upewnij się, czy aplikacje będą nadal dostępne. Jeśli hello DNS jest skonfigurowany tooallow aktualizacje dynamiczne maszyn wirtualnych hello czy rejestrują się za pomocą nowego adresu IP powitania po rozpoczęciu po przejściu w tryb failover.

![IP różne — od trybu Failover](./media/site-recovery-network-design/network-design11.png)


Po maszyny wirtualnej repliki hello przez niepowodzenie może mieć adres IP, który nie jest hello takie same jak adres IP hello hello podstawowej maszyny wirtualnej. Maszyny wirtualne zaktualizuje hello serwera DNS, które używają po rozpoczęciu. Wpisy DNS zazwyczaj mają toobe zmienione lub opróżnionych w całej sieci hello i wpisów pamięci podręcznej w tabelach sieci toobe zaktualizowane lub opróżnione, więc nie jest rzadko toobe, które muszą ponieść przestojów podczas zmiany stanu została wykonana. Ten problem można zminimalizować przez:

* Przy użyciu niskich wartości TTL dla aplikacji sieci intranet.
* Za pomocą Menedżera ruchu Azure przy użyciu usługi ASR Internetu na podstawie aplikacji.
* Przy użyciu następujących hello skryptu w ramach odzyskiwania planowanie tooupdate powitania serwera DNS tooensure czas aktualizacji (hello skryptu nie jest wymagana przy hello rejestracji dynamicznych DNS jest skonfigurowane)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Zmiana adresów IP hello — DR tooAzure
Witaj [sieci infrastruktury Instalatora platformy Microsoft Azure jako lokacja odzyskiwania po awarii](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wpis w blogu wyjaśniono, jak toosetup hello wymagane infrastruktury platformy Azure networking zachowując adresów IP nie jest wymagana. Zaczyna się od opisu aplikacji hello i następnie wyglądu w sposób toosetup sieci lokalnej i na platformie Azure i następnie kończąc jak toodo test trybu failover i planowanego trybu failover.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sposób Site Recovery mapowania sieci źródłowe i docelowe, gdy serwer VMM jest używany toomanage hello podstawowej lokacji.
