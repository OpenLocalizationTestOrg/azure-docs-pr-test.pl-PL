---
title: "aaaInfrastructure i łączności tooSAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Skonfiguruj wymaga połączenia infrastruktury toouse SAP HANA na platformie Azure (wystąpienia duże)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infrastruktura SAP HANA (duże wystąpień) i łączność na platformie Azure 

Definicje wyprzedzeniem przed przeczytaniem tego przewodnika. W [omówienie SAP HANA (duże wystąpień) i architektury na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) wprowadzono dwóch różnych klas jednostek HANA dużych wystąpienie:

- S72, S72m S144, S144m, S192 i S192m, które firma Microsoft można znaleźć hello tooas I klasy typu jednostek magazynowych.
- S384, S384m S384xm, S576, S768 i S960, które firma Microsoft można znaleźć tooas Witaj "class typu II' SKU.

Specyfikatory klas Hello są toobe będzie używane w całym hello HANA wystąpienia dużych tooeventually dokumentację można znaleźć możliwości toodifferent i wymagania odpowiednio jednostki SKU HANA dużych wystąpienia.

Inne definicje, często używanych są:
- **Sygnatura wystąpienia dużych:** stos infrastruktury sprzętu SAP HANA TDI certyfikowane i wystąpień SAP HANA toorun w obrębie platformy Azure w wersji dedykowanej.
- **SAP HANA na platformie Azure (duże wystąpienia):** oficjalną nazwą języka dla oferty hello Azure toorun HANA wystąpień w na SAP HANA TDI certyfikowanego sprzętu, które zostało wdrożone w dużych wystąpienia sygnatury w różnych regionach platformy Azure. Witaj powiązane termin **wystąpienia dużych HANA** jest skrót SAP HANA na platformie Azure (wystąpienia duże) i jest powszechnie używany ten przewodnik wdrożenia technicznego.
 

Po hello zakupu SAP HANA na platformie Azure (wystąpienia duże) jest zakończona między użytkownikiem a hello zespół kont Microsoft enterprise, hello następujące informacje jest wymagana przez Microsoft toodeploy HANA dużych jednostek wystąpienie:

- Nazwa klienta
- (W tym adres e-mail i numer telefonu) informacje dotyczące kontaktów biznesowych
- Skontaktuj się z pomocą informacje techniczne (w tym wiadomości e-mail adres i numer telefonu)
- Techniczne informacje kontaktowe sieci (w tym wiadomości e-mail adres i numer telefonu)
- Region wdrożenia usługi Azure (zachodnie stany USA, wschodnie stany USA, Australia Wschodnia, Australia Południowo-Wschodnia, Europa Zachodnia i Europa Północna, począwszy od lipca 
- 2017)
- Potwierdź SAP HANA na Azure (wystąpienia duże) jednostki SKU (Konfiguracja)
- Jak już szczegółowo w hello omówienie i architektura dokumentu dla wystąpień dużych HANA, dla każdego regionu Azure wdrażane na:
    - /29 zakres adresów IP dla połączeń ER P2P, podłączoną do sieci wirtualnych Azure tooHANA dużych wystąpień
    - Prefiksie/24 blok CIDR używany dla hello HANA puli adresów IP w dużych serwera wystąpień
- Witaj wartości adresów IP zakres używany w atrybucie przestrzeni adresowej sieci wirtualnej hello każdej sieci wirtualnej Azure, łączącego toohello HANA dużych wystąpień
- Dane dla każdego wystąpienia dużych HANA systemu:
  - Żądany hostname - najlepiej z pełną nazwę domeny.
  - Żądany adres IP jednostkę wystąpienia dużych HANA hello poza hello zakres adresów puli adresów IP serwera — należy pamiętać, że hello pierwsze 30 adresy IP na powitania serwera puli adresów IP, zakresu adresów są zarezerwowane do użytku wewnętrznego w dużych wystąpień HANA
  - Nazwy SAP HANA SID hello SAP HANA wystąpienia (woluminy toocreate wymagane hello potrzeby związane z SAP HANA dysku). Hello HANA identyfikator SID jest wymagany dla hello uprawnień do tworzenia <sidadm> w woluminach systemu plików NFS hello, które pierwsze dołączonych toohello HANA dużych wystąpienia jednostki. Ponadto jest używany jako jeden ze składników nazwa hello hello woluminów dysków, które uzyskać zainstalowane. Jeśli chcesz toorun więcej niż jedno wystąpienie HANA w jednostce hello, należy toolist wielu HANA identyfikatorów SID. Każda z nich pobiera osobny zestaw woluminów przypisane.
  - Witaj groupid hello hana sidadm użytkownik ma w hello systemu operacyjnego Linux jest wymagany toocreate hello niezbędne SAP HANA związane z woluminami. Witaj instalacji SAP HANA zazwyczaj tworzy grupę sapsys hello z identyfikatorem grupy 1001. Użytkownik hana sidadm Hello jest częścią tej grupy
  - Witaj userid hello hana sidadm użytkownik ma w hello systemu operacyjnego Linux jest wymagany toocreate hello niezbędne SAP HANA związane z woluminami. Jeśli używasz wielu wystąpień HANA w jednostce hello, należy toolist wszystkie hello <sid>adm użytkowników 
- Identyfikator subskrypcji platformy Azure dla toowhich subskrypcji platformy Azure hello SAP HANA w wystąpieniach dużych HANA Azure będą połączone bezpośrednio toobe. Ten identyfikator subskrypcji odwołuje się do hello subskrypcji platformy Azure, który będzie się, że toobe obciążana hello HANA dużych wystąpienia jednostki.

Po podaniu hello informacji postanowienia Microsoft SAP HANA na platformie Azure (wystąpienia duże) i zwróci toolink niezbędne informacje hello sieci wirtualnych Azure tooHANA dużych wystąpień i tooaccess hello HANA wystąpienia dużych jednostek.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Łączenie wystąpień dużych tooHANA maszynach wirtualnych platformy Azure

Jak już wspomniano w [omówienie SAP HANA (duże wystąpień) i architektury na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) hello minimalnego wdrożenia HANA dużych wystąpień z warstwy aplikacji SAP hello w Azure wygląda, takich jak:

![Sieć wirtualna Azure połączone tooSAP HANA Azure (wystąpienia duże) i lokalnej](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Wyszukiwanie bliżej na powitania po stronie sieci wirtualnej Azure, Zdajemy sobie sprawę potrzebę hello:

- Definicja Hello sieć wirtualną platformy Azure jest toodeploy toobe używany będzie hello maszynach wirtualnych hello warstwy aplikacji SAP do.
- Który automatycznie oznacza, że podsieci domyślne hello sieci wirtualnej platformy Azure jest definiowana będący naprawdę hello jeden używane toodeploy maszyn wirtualnych hello do.
- toohave musi Hello sieci wirtualnej Azure, która jest tworzona co najmniej jedną podsieć maszyny Wirtualnej i jedną podsieć bramy ExpressRoute. Te podsieci powinien być przypisany hello zakresów adresów IP jak określono i opisanych w hello następujące sekcje.

Tak Oto nieco zbliżonej do tworzenia sieci wirtualnej platformy Azure dla wystąpień dużych HANA hello

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Tworzenie hello sieci wirtualnej platformy Azure dla wystąpień dużych HANA

>[!Note]
>Witaj sieci wirtualnej platformy Azure dla wystąpienia dużych HANA musi zostać utworzony przy użyciu modelu wdrażania usługi Azure Resource Manager hello. Hello starsze Azure model wdrażania, powszechnie znane jako klasycznego modelu wdrażania, nie jest obsługiwana z hello wystąpienia dużych HANA rozwiązania.

Witaj sieci wirtualnej można utworzyć przy użyciu hello portalu Azure, programu PowerShell, szablon Azure lub interfejsu wiersza polecenia Azure (zobacz [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). W hello poniższy przykład szukamy do sieci wirtualnej została utworzona za pośrednictwem hello portalu Azure.

Jeśli szukamy do definicji hello sieć wirtualną platformy Azure za pośrednictwem portalu Azure hello Zobaczmy na niektóre hello definicji oraz jak te dotyczą toowhat możemy listę różnych zakresów adresów IP. Jak możemy omówieniu hello **przestrzeni adresowej**, możemy oznacza przestrzeń adresowa hello hello sieci wirtualnej platformy Azure jest dozwolone toouse. Ta przestrzeń adresowa jest również zakres adresów hello hello sieci wirtualnej używa dla propagacji trasy protokołu BGP. To **przestrzeni adresowej** są widoczne w tym miejscu:

![Adres miejsca Azure z sieci wirtualnej wyświetlane w hello portalu Azure](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

W przypadku hello poprzedzających z 10.16.0.0/16 hello sieci wirtualnej Azure podano zamiast dużej i dwubajtowe toouse zakres adresów IP. Oznacza, że wszystkie zakresy adresów IP hello kolejne podsieci w tej sieci wirtualnej może mieć ich zakresów w ramach tej przestrzeni adresowej. Zwykle nie zalecamy zakres adresów dużych jednej sieci wirtualnej na platformie Azure. Ale pobieranie kolejny krok, Oto na powitania podsieci zdefiniowanej w hello sieci wirtualnej platformy Azure:

![Podsieci sieci wirtualnej platformy Azure i ich zakresy adresów IP](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Jak widać, przyjrzymy się sieci wirtualnej z pierwszej podsieci maszyny Wirtualnej (w tym miejscu o nazwie "default") i podsieć o nazwie "GatewaySubnet".
W następującej sekcji hello, możemy odwoływać się zakres adresów IP toohello hello podsieć, w której wywołano "default" hello grafiki jako **zakres adresów IP podsieci maszyny Wirtualnej Azure**. W następujące sekcje hello, możemy odnosi się zakres adresów IP toohello hello podsieci bramy jako **zakres adresów IP podsieci bramy sieci wirtualnej**. 

W przypadku hello dowodzą grafiki hello dwa powyżej, zobacz ten hello **przestrzeni adresowej sieci wirtualnej** obejmuje zarówno hello **zakres adresów IP podsieci maszyny Wirtualnej Azure** i hello **adresów IP podsieci bramy sieci wirtualnej zakres**. 

W innych przypadkach, gdy konieczne tooconserve lub być określone zakresy adresów IP, można ograniczyć hello **przestrzeni adresowej sieci wirtualnej** sieci wirtualnej toohello zakresów określonych, używany przez każdej podsieci. W takim przypadku można zdefiniować hello **przestrzeni adresowej sieci wirtualnej** z sieci wirtualnej określonych jako wiele zakresów, jak pokazano poniżej:

![Azure przestrzeni adresowej sieci wirtualnej z dwoma obszarami](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

W takim przypadku hello **przestrzeni adresowej sieci wirtualnej** ma dwa pola zdefiniowane. Te dwie spacje zakresów adresów IP identyczne toohello zdefiniowanych dla **zakres adresów IP podsieci maszyny Wirtualnej Azure** i hello **zakres adresów IP podsieci bramy sieci wirtualnej.**

Można użyć dowolnego standard nazewnictwa, który chcesz dla tych podsieci dzierżawy (podsieci maszyny Wirtualnej). Jednak **musi zawsze występować jeden i tylko jeden podsieci bramy dla każdej sieci wirtualnej** łączące toohello SAP HANA obwodu usługi ExpressRoute Azure (wystąpienia duże). I **tej podsieci bramy muszą zawsze być o nazwie "GatewaySubnet"** tooensure prawidłowego umieszczania hello bramę usługi ExpressRoute.

> [!WARNING] 
> Kluczowe znaczenie tej podsieci bramy hello zawsze jest o nazwie "GatewaySubnet".

Wiele podsieci maszyny Wirtualnej mogą być używane, nawet przy użyciu zakresów adresów nieciągłych. Ale jak już wspomniano, tych zakresów adresów muszą być objęte hello **przestrzeni adresowej sieci wirtualnej** hello sieci wirtualnej w formie zagregowanej lub na liście hello dokładnie zakresy hello podsieci maszyny Wirtualnej i hello podsieci bramy.

Podsumowanie hello ważne informacja dotycząca sieć wirtualną platformy Azure łączy tooHANA dużych wystąpień:

- Należy toosubmit tooMicrosoft hello **przestrzeni adresowej sieci wirtualnej** podczas wykonywania początkowe wdrożenie HANA dużych wystąpień. 
- Witaj **przestrzeni adresowej sieci wirtualnej** może być jeden zakres większy, które obejmuje zakres hello zakresów adresów IP podsieci maszyny Wirtualnej platformy Azure i zakres adresów IP podsieci bramy sieci wirtualnej hello.
- Lub można przesłać jako **przestrzeni adresowej sieci wirtualnej** wiele zakresów, które obejmują powitania od różnych zakresów zakresów adresów IP podsieci maszyny Wirtualnej i zakres adresów IP podsieci bramy sieci wirtualnej hello adresów.
- Witaj zdefiniowane **przestrzeni adresowej sieci wirtualnej** jest używane propagacji routingu BGP.
- Nazwa Hello hello podsieć bramy musi być: **"GatewaySubnet".**
- Witaj **przestrzeni adresowej sieci wirtualnej** służy jako filtru w tooallow po stronie wystąpienia dużych HANA hello lub nie zezwalaj na ruch toohello HANA dużych wystąpienia jednostki z platformy Azure. Jeśli hello informacje routingu BGP hello sieci wirtualnej platformy Azure i zakresy adresów IP hello skonfigurowana do filtrowania na powitania po stronie wystąpienia dużych HANA nie są zgodne, mogą wystąpić problemy z łącznością.
- Dostępne są niektóre szczegółowe informacje o hello podsieć bramy, które są omawiane dalsze w dół w sekcji "Łączenie tooHANA sieci wirtualnej, duże wystąpienia usługi ExpressRoute"



### <a name="different-ip-address-ranges-toobe-defined"></a>Toobe zakresów adresów IP w różnych zdefiniowany 

Już wprowadzone niektóre hello IP adres zakresy niezbędne toodeploy HANA wystąpień dużych we wcześniejszych sekcjach. Istnieją pewne więcej zakresów adresów IP, które są ważne. Przejdź przez niektóre dodatkowe szczegóły. Witaj następujących adresów IP, których nie wszystkie wymagają toobe przesłać tooMicrosoft muszą toobe zdefiniowane przed wysłaniem żądania początkowego rozmieszczania:

- **Przestrzeń adresowa sieci wirtualnej:** jak już wprowadzone wcześniej, jest lub adres IP hello range(s) możesz przypisano (lub planujesz tooassign) są tooyour adres miejsca parametru w hello sieci wirtualnych Azure (VNet) łączenie toohello SAP HANA dużych wystąpienia środowisko. Zaleca się, że ten parametr przestrzeń adresowa jest wartość wielowierszowego obejmuje hello zakresów podsieci maszyny Wirtualnej platformy Azure i hello zakresu podsieci bramy Azure, jak pokazano wcześniej hello grafiki. Ten zakres nie mogą się pokrywać z lokalnymi lub zakres adresów puli adresów IP serwera lub ER P2P. Jak tooget to lub tych zakresów adresów IP? Dostawca zespołu lub usługi sieci firmowej powinna zapewniać jednego lub wielu liczbą zakresów adresów IP, która jest lub nie są używane w sieci. Przykład: Jeśli podsieć maszyny Wirtualnej Azure (zobacz wcześniej) 10.0.1.0/24 i podsieć bramy Azure (patrz niżej) jest 10.0.2.0/28, następnie przestrzeń adresowa sieci wirtualnej platformy Azure jest zalecane toobe dwóch wierszach. 10.0.1.0/24 i 10.0.2.0/28. Mimo że można agregowane wartości przestrzeni adresowej hello, zalecane jest dopasowywanie ich zakresy podsieci toohello tooavoid przypadkowego ponownego użycia nieużywane IP zakresów adresów w większych przestrzeni adresów w przyszłości hello w innym miejscu w sieci. **zakres adresów IP, które toobe musi przesłać tooMicrosoft podczas pytania o początkowe wdrożenie jest Hello przestrzeni adresowej sieci Wirtualnej**

- **Azure zakres adresów IP podsieci maszyny Wirtualnej:** hello jedną przypisano (lub planujesz tooassign) jest zakres adresów IP to, jak wspomniano wcześniej już parametr podsieci sieci wirtualnej Azure toohello w sieci wirtualnej platformy Azure łączenie toohello SAP HANA dużych wystąpienia środowiska . Ten zakres adresów IP jest tooyour adresy IP używane tooassign maszynach wirtualnych platformy Azure. adresy IP Hello poza tym zakresem mogą tooyour tooconnect serwery wystąpienia dużych SAP HANA. W razie potrzeby wiele podsieci maszyny Wirtualnej platformy Azure mogą być używane. A/24 blok CIDR jest zalecana przez firmę Microsoft dla każdej podsieci maszyny Wirtualnej Azure. Ten zakres adresów musi być częścią hello wartości używana podczas hello przestrzeni adresowej sieci wirtualnej platformy Azure. Jak tooget ten zakres adresów IP? Dostawca zespołu lub usługi sieci firmowej powinien zapewnić zakres adresów IP, który nie jest obecnie używany w sieci.

- **Zakres adresów IP podsieci bramy sieci wirtualnej:** w zależności od hello funkcje planujesz toouse, hello zalecane jest rozmiar:
   - Bramy z największą wydajnością ExpressRoute: / 26 blok adresów — wymagany dla typu II klasy jednostki SKU
   - Współistnienie z sieci VPN i ExpressRoute przy użyciu bramy ExpressRoute wysokiej wydajności (lub mniejsze): / 27 blok adresów
   - Innych sytuacjach: / 28 blok adresów. Ten zakres adresów musi być częścią wartości hello używane w wartości "Sieci wirtualnej przestrzeni adresowej" hello. Ten zakres adresów musi być częścią hello wartości używana podczas hello przestrzeni adresowej sieci wirtualnej Azure wartości potrzebnych toosubmit tooMicrosoft. Jak tooget ten zakres adresów IP? Dostawca zespołu lub usługi sieci firmowej powinien zapewnić zakres adresów IP, który nie jest obecnie używany w sieci. 

- **Zakres łączności ER P2P adresów:** ten zakres jest zakres adresów IP hello połączenie P2P SAP HANA dużych wystąpienia usługi ExpressRoute (ER). Ten zakres adresów IP musi być /29 zakres adresów CIDR IP. Ten zakres nie musi nakłada się z lokalnymi lub innymi IP platformy Azure, zakresy adresów. Ten zakres adresów IP jest używane tooset się hello ER łączności z serwerów bramy ExpressRoute sieci wirtualnej Azure toohello wystąpienia dużych SAP HANA. Jak tooget ten zakres adresów IP? Dostawca zespołu lub usługi sieci firmowej powinien zapewnić zakres adresów IP, który nie jest obecnie używany w sieci. **Ten zakres jest zakres adresów IP, które toobe musi przesłać tooMicrosoft podczas pytania o początkowe wdrożenie**
  
- **Zakres puli adresów IP serwera:** ten zakres adresów IP jest używany tooassign hello poszczególne serwery adresów IP tooHANA dużych wystąpienia. Witaj zalecany rozmiar podsieci jest prefiksie/24 CIDR zablokować — ale jeśli potrzebne może być mniejszy minimum tooa dostarczać 64 adresy IP. Z tego zakresu hello pierwsze 30 adresy IP są zarezerwowane do użytku przez firmę Microsoft. Upewnij się, że ten fakt przypada na wybierając rozmiar hello hello zakresu. Ten zakres musi nie nakłada się z lokalnymi lub innymi IP platformy Azure adresów. Jak tooget ten zakres adresów IP? Dostawca zespołu lub usługi sieci firmowej powinien zapewnić zakres adresów IP, który nie jest obecnie używany w sieci. Prefiksie/24 (zalecane) CIDR unikatowy bloku toobe można przypisywać hello określonych adresów IP wymaganych dla SAP HANA na platformie Azure (wystąpienia duże). **Ten zakres jest zakres adresów IP, które toobe musi przesłać tooMicrosoft podczas pytania o początkowe wdrożenie**
 
Chociaż należy toodefine i Planowanie zakresów adresów IP hello powyżej, nie wszystkie ich muszą tooMicrosoft toobe przesyłane. toosummarize hello powyżej, zakresów adresów IP hello są tooMicrosoft tooname wymagane są następujące:

- Space(s) adresów sieci wirtualnej platformy Azure
- Zakres adresów dla łączności ER P2P
- Zakresu adresów puli adresów IP serwera

Dodawanie dodatkowe sieci wirtualnych, wymagającym tooHANA tooconnect dużych wystąpienia wymaga toosubmit hello przestrzeni adresowej sieci wirtualnej platformy Azure w nowych dodajesz tooMicrosoft. 

Poniżej przedstawiono przykład hello inne zakresy i niektóre zakresy przykład tooconfigure i ostatecznie Podaj tooMicrosoft. Jak widać, wartość hello hello przestrzeni adresowej sieci wirtualnej platformy Azure nie jest przedstawiona w pierwszym przykładzie hello, ale zdefiniowano z zakresów hello hello pierwszej maszyny Wirtualnej Azure podsieci zakresu adresów IP i zakres adresów IP podsieci bramy sieci wirtualnej hello. Przy użyciu wielu podsieci maszyny Wirtualnej w ramach sieci wirtualnej Azure hello czy pracy odpowiednio konfigurując i przesyłanie hello IP dodatkowe zakresy adresów hello dodatkowe adresy podsieci maszyny Wirtualnej używane jako część hello przestrzeni adresowej sieci wirtualnej platformy Azure.

![Zakresy adresów IP w SAP HANA wymagane we wdrożeniu minimalnego Azure (wystąpienia duże)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

Istnieje również możliwość hello agregowanie danych hello przesłać tooMicrosoft. W takim przypadku hello przestrzeni adresowej sieci wirtualnej Azure hello tylko obejmuje jedną spację. Za pomocą zakresów adresów IP hello używanych w przykładzie hello wcześniej. Ta zagregowane przestrzeń adresowa sieci wirtualnej może wyglądać jak:

![Druga możliwość zakresów adresów IP w SAP HANA wymagane we wdrożeniu minimalnego Azure (wystąpienia duże)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Jak pokazano powyżej, zamiast dwa zakresy mniejszych, zdefiniowane hello przestrzeni adresowej sieci wirtualnej Azure, hello mamy jeden zakres większy, który obejmuje 4096 adresów IP. Duże definicji hello przestrzeni adresowej pozostawia niektórych raczej duże zakresy nieużywane. Od wartości sieci wirtualnej przestrzeni adresowej hello są używane do propagacji trasy protokołu BGP, użycie hello Nieużywane zakresy lokalnie lub w innym miejscu w sieci może spowodować problemy routingu. Dlatego jest powitalne zalecane tookeep przestrzeni adresowej ściśle dostosowany przestrzeni adresowej podsieci rzeczywiste hello używane. W razie potrzeby bez przestoju na powitania sieci wirtualnej, można dodać nowe wartości przestrzeni adresowej później.
 
> [!IMPORTANT] 
> Każdy adres IP przestrzeni adresowej sieci wirtualnej Azure zakresu ER-P2P, pula IP serwera, należy **nie** nakładają się ze sobą lub inny zakres używany w innym miejscu w sieci; każdego musi być kolumną dyskretną i jako hello dwa grafiki nie może być wcześniej Pokaż podsieć inny zakres. Ewentualnych nakładania się między zakresy hello Azure w sieci wirtualnej nie może połączyć toohello obwodu ExpressRoute.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Następne kroki po zdefiniowaniu zakresów adresów
Po zdefiniowaniu zakresów adresów IP hello hello następujących działań należy toohappen:

1. Przedstawia zakresy adresów IP hello przestrzeni adresowej sieci wirtualnej Azure, hello ER P2P łączności i zakres puli adresów IP serwera, oraz inne dane, które zostały wymienione na początku hello hello dokumentu. W tym momencie możesz również można uruchomić hello toocreate sieci wirtualnej i hello podsieci maszyny Wirtualnej. 
2. Obwodzie usługi Express Route jest tworzony przez firmę Microsoft, między subskrypcją platformy Azure i sygnatura wystąpienia dużych HANA hello.
3. Na powitania dużych wystąpienia sygnatury sieci dzierżawcy jest tworzony przez firmę Microsoft.
4. Microsoft konfiguruje sieć w hello SAP HANA na tooaccept infrastruktury platformy Azure (wystąpienia duże) adres IP z Azure sieć wirtualna przestrzeń adresowa komunikującym się z wystąpieniami dużych HANA.
5. W zależności od hello zakupionymi określonych SAP HANA na Azure SKU (duże wystąpienia) firma Microsoft przypisuje Jednostka obliczeniowa w sieci dzierżawcy, Przydziel zainstalować Magazyn i zainstaluj system operacyjny hello (SUSE lub Red Hat Linux). Adresy IP dla tych jednostek są wyjmowane z hello adresów puli adresów IP serwera przesłane tooMicrosoft zakresu.

Na końcu hello hello procesu wdrażania firma Microsoft dostarcza powitania po tooyou danych:
- Informacje potrzebne tooconnect Twojego obwodu ExpressRoute toohello Azure VNet(s) łączy wystąpień dużych tooHANA sieci wirtualnych platformy Azure:
     - Klucze autoryzacji
     - ExpressRoute PeerID
- Dane tooaccess wystąpień dużych HANA po ustanowić obwodu ExpressRoute i sieci wirtualnej platformy Azure.

Możesz również znaleźć sekwencji hello łączący HANA dużych wystąpień w dokumencie hello [kończyć tooEnd Instalatora programu SAP HANA dużych wystąpień](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Wiele hello następujące kroki przedstawiono przykład wdrożenia w tym dokumencie. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>Łączenie tooHANA sieci wirtualnej, duże wystąpienia usługi ExpressRoute

Zdefiniowane wszystkie zakresy adresów IP hello i teraz otrzymano hello danych firmy Microsoft, można rozpocząć łączenia hello utworzone przed tooHANA wystąpień dużych sieci wirtualnej. Raz hello utworzenia sieci wirtualnej Azure, bramę usługi ExpressRoute należy utworzyć na powitania sieci wirtualnej toolink hello sieci wirtualnej toohello obwodu usługi expressroute, łączącego toohello dzierżawy klienta na powitania dużych wystąpienia sygnatury.

> [!NOTE] 
> Ten krok może potrwać too30 toocomplete minut, hello nowej bramy jest tworzony w Witaj wyznaczone subskrypcji platformy Azure, a następnie połączonych toohello określona sieć wirtualna Azure.

Jeśli brama już istnieje, sprawdź, czy należy bramę usługi ExpressRoute. W przeciwnym razie hello bramy należy usunąć i utworzyć ponownie jako bramę usługi ExpressRoute. Jeśli brama usługi ExpressRoute już zostanie nawiązane, ponieważ hello sieci wirtualnej platformy Azure jest już połączony obwodu ExpressRoute toohello łączność z lokalnymi, kontynuować toohello poniższej sekcji Łączenie z sieciami wirtualnymi.

- Użyj (nowy) albo hello [portalu Azure](https://portal.azure.com/), lub środowiska PowerShell toocreate bramy sieci VPN ExpressRoute podłączone tooyour sieci wirtualnej.
  - Jeśli używasz hello portalu Azure, Dodaj nową **Brama sieci wirtualnej** , a następnie wybierz **ExpressRoute** jako hello typu bramy.
  - Jeśli zamiast tego wybrano programu PowerShell, należy najpierw pobrać i użyć hello najnowsza wersja [zestawu SDK usługi Azure PowerShell](https://azure.microsoft.com/downloads/) tooensure zapewnienia optymalnego działania. Witaj następującego polecenia Utwórz bramę usługi ExpressRoute. Teksty Hello poprzedzony  _$_  są tego toobe należy zaktualizować określone informacje o zmiennych zdefiniowanych przez użytkownika.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

W tym przykładzie użyto hello jednostka SKU bramy wysokowydajnej. Opcje są wysokowydajnej lub UltraPerformance jako hello tylko SKU bramy obsługiwanych przez SAP HANA na platformie Azure (wystąpienia duże).

> [!IMPORTANT]
> Dla dużych wystąpień hello SKU HANA typy S384, S384m S384xm, S576, S768 i S960 (typ klasy II jednostki SKU), hello użycia hello UltraPerformance jednostka SKU bramy jest obowiązkowy.

### <a name="linking-vnets"></a>Łączenie sieci wirtualnych

Teraz hello sieci wirtualnej Azure ma bramę usługi ExpressRoute, użycie informacji o autoryzacji hello udostępniane przez Microsoft tooconnect hello ExpressRoute bramy toohello SAP HANA obwodu ExpressRoute Azure (wystąpienia duże) utworzone dla tego połączenia. Ten krok można wykonać przy użyciu hello portalu Azure lub programu PowerShell. Zaleca się Hello portalu, jednak instrukcje programu PowerShell są następujące. 

- Można wykonywać hello następujące polecenia dla każdej bramy sieci wirtualnej przy użyciu różnych AuthGUID dla każdego połączenia. pierwsze dwie pozycje Hello pokazano poniżej skryptu hello pochodzą z hello informacje dostarczane przez firmę Microsoft. Ponadto hello AuthGUID jest specyficzne dla każdej sieci wirtualnej i bramy. Oznacza, że jeśli chcesz tooadd innej sieci wirtualnej Azure, należy tooget innego AuthID dla Twojego obwodu usługi expressroute łączy HANA dużych wystąpień na platformie Azure. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Jeśli chcesz tooconnect hello bramy toomultiple obwody usługi ExpressRoute, które są skojarzone z subskrypcją, może być konieczne tooexecute ten krok więcej niż raz. Na przykład, prawdopodobnie będą tooconnect hello tej samej bramy sieci wirtualnej toohello obwodu ExpressRoute łączącego hello sieci wirtualnej tooyour lokalną sieć.

## <a name="adding-more-ip-addresses-or-subnets"></a>Dodawanie więcej adresów IP lub podsieci

Użyj albo hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia, dodając więcej adresów IP lub podsieci.

W takim przypadku zalecane hello jest tooadd hello nowego zakresu adresów IP jako nowy zakres toohello przestrzeni adresowej sieci wirtualnej zamiast generowania nowego zagregowanych zakresu. W obu przypadkach należy toosubmit tej zmiany tooMicrosoft tooallow łączności z tego nowego IP adres zakresu toohello HANA dużych wystąpienia jednostki na kliencie. Można także otworzyć pomocy technicznej platformy Azure żądania tooget hello nowej sieci wirtualnej przestrzeni adresowej dodane. Po otrzymaniu potwierdzenia, wykonaj kolejne kroki hello.

toocreate dodatkowe podsieci z hello portalu Azure, zobacz artykuł hello [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), i toocreate z programu PowerShell, zobacz [utworzyć sieć wirtualną przy użyciu programu PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Dodawanie sieci wirtualnych

Po początkowym nawiązaniu połączenia sieci wirtualnych platformy Azure, możesz tooadd te dodatkowe, które dostępu SAP HANA na platformie Azure (wystąpienia duże). Najpierw należy przesłać żądanie pomocy technicznej platformy Azure, w tym żądaniu obejmują hello określone informacje identyfikacyjne hello konkretnego wdrożenia usługi Azure i hello IP adres miejsca zakresów z hello przestrzeni adresowej sieci wirtualnej platformy Azure. SAP HANA na zarządzania usługą Azure udostępnia następnie hello niezbędne informacje należy tooconnect hello dodatkowe sieci wirtualne i usługi ExpressRoute. Dla każdej sieci wirtualnej należy Unikatowy klucz autoryzacji tooconnect toohello wystąpień dużych tooHANA obwodu usługi Expressroute.

Kroki tooadd nowej sieci wirtualnej platformy Azure:

1. Zakończenie hello pierwszym etapem procesu dołączania hello, zobacz hello _tworzenie sieci wirtualnej Azure_ sekcji.
2. Ukończyć powitalnych drugim etapem procesu dołączania hello, zobacz hello _tworzenia podsieci bramy_ sekcji.
3. tooconnect dodatkowe toohello sieci wirtualnych obwodu ExpressRoute wystąpienia z dużych HANA, otwórz żądanie pomocy technicznej platformy Azure z informacjami na hello nowej sieci wirtualnej i zażądaj nowego klucza autoryzacji.
4. Po powiadomienie, że autoryzacja hello jest zakończenie, należy użyć informacji dostarczonych przez firmę Microsoft autoryzacji hello toocomplete hello trzeci krok w procesie dołączania hello, zapoznaj się z hello _łączenia sieci wirtualnych_ sekcji.

## <a name="increasing-expressroute-circuit-bandwidth"></a>Zwiększenie przepustowości obwodu ExpressRoute

Zapoznaj się z SAP HANA na zarządzanie usługami Azure. Jeśli przepustowość hello zaleca tooincrease hello SAP HANA obwodu usługi ExpressRoute Azure (wystąpienia duże), należy utworzyć żądanie pomocy technicznej platformy Azure. (Można zażądać zwiększenia przepustowości obwodu pojedynczego się tooa maksymalnie 10 GB/s). Następnie możesz otrzymać powiadomienie po zakończeniu operacji hello; żadne dodatkowe akcje niezbędne tooenable wyższe szybkość na platformie Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Dodawanie dodatkowych obwodu usługi ExpressRoute

Zapoznaj się z SAP HANA na zarządzanie usługami Azure, jeśli zaleca się, że potrzebne są dodatkowe obwodu ExpressRoute, powoduje toocreate żądania pomocy technicznej platformy Azure, nowe obwodu ExpressRoute (i tooget autoryzacji informacji tooconnect tooit). przestrzeń adresowa Hello będzie można użyć powitalne sieci wirtualnych muszą być zdefiniowane przed wprowadzeniem hello żądania, aby SAP HANA na autoryzacji tooprovide zarządzania usługą Azure.

Gdy jest tworzony nowy obwód hello i zakończeniu hello SAP HANA w konfiguracji zarządzania usługą Azure ma tooreceive powiadomienia o hello informacje, które należy tooproceed. Wykonaj kroki hello podanego powyżej do tworzenia i łączenia hello nowej sieci wirtualnej toothis dodatkowe obwodu. Nie jesteś obwodu dodatkowe toothis sieci wirtualnych platformy Azure można tooconnect Jeśli już połączony tooanother SAP HANA obwodu ExpressRoute Azure (wystąpienia duże) w hello tym samym regionie Azure.

## <a name="deleting-a-subnet"></a>Usuwanie podsieci

można tooremove podsieci sieci wirtualnej, albo hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia. W przypadku, gdy IP sieci wirtualnej platformy Azure adres zakresu/Azure przestrzeni adresowej sieci wirtualnej została zagregowanych zakresu, nie ma żadnych wykonaj dla możesz z firmą Microsoft. Oprócz tego hello sieć wirtualna jest nadal propagowanie przestrzeni adresowej trasy protokołu BGP, która obejmuje hello usunąć podsieci. Jeśli hello IP sieci wirtualnej platformy Azure adres zakresu/Azure przestrzeni adresowej sieci wirtualnej jest zdefiniowany jako wiele zakresów adresów IP z których jeden podsieci przypisane tooyour usunięte, należy usunąć który poza przestrzeń adresowa sieci wirtualnej i następnie informuje SAP HANA na zarządzania usługą Azure tooremove z hello zakresy tego SAP HANA na platformie Azure (wystąpienia duże) jest dozwolone toocommunicate z.

Gdy nie ma jeszcze są określone, dedykowane wskazówki witryny Azure.com na usuwanie podsieci, hello proces usuwania podsieci hello odwrócenie procesu hello dodanie ich. Zobacz artykuł hello [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji na temat tworzenia podsieci.

## <a name="deleting-a-vnet"></a>Usunięcie sieci wirtualnej

Podczas usuwania sieci wirtualnej za pomocą obu hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia. SAP HANA na zarządzania usługą Azure usuwa hello istniejącego zezwolenia na powitania SAP HANA obwodu usługi Azure ExpressRoute (duże wystąpień) i Usuń hello IP sieci wirtualnej platformy Azure adres zakresu/Azure przestrzeni adresowej sieci wirtualnej komunikacji hello wystąpieniami dużych HANA.

Po usunięciu hello sieci wirtualnej Otwórz pomocy technicznej platformy Azure żądania tooprovide hello przestrzeń adresów IP range(s) toobe usunięte.

Gdy nie ma jeszcze są określone, dedykowane wskazówki witryny Azure.com na usuwanie sieci wirtualnych, hello proces usuwania sieci wirtualnych hello odwrócenie procesu hello dodawania obrazu, który opisano powyżej. Zobacz artykuły hello [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [utworzyć sieć wirtualną przy użyciu programu PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji na temat tworzenia sieci wirtualnych.

tooensure wszystko, co jest usunięte, Usuń hello następujące elementy:

- Witaj połączenia ExpressRoute, Brama sieci wirtualnej publiczny adres IP bramy sieci wirtualnej i sieci wirtualnej

## <a name="deleting-an-expressroute-circuit"></a>Usuwanie obwodu usługi ExpressRoute

tooremove dodatkowe SAP HANA obwodu usługi ExpressRoute Azure (wystąpienia duże), otwórz żądanie pomocy technicznej platformy Azure z SAP HANA na zarządzania usługą Azure i żądania obwodu hello powinien zostać usunięty. W ramach hello subskrypcji platformy Azure można usunąć lub zachować hello sieci wirtualnej odpowiednio do potrzeb. Jednak należy usunąć hello połączenie między hello obwodu ExpressRoute wystąpień z dużych HANA i hello połączone bramy sieci wirtualnej.

Również tooremove sieci wirtualnej, należy wykonać hello wskazówki na temat usuwania hello powyżej w sekcji sieci wirtualnej.


