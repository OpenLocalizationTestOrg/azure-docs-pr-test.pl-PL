---
title: "aaaOverview i architektura SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Omówienie architektury tooDeploy SAP HANA na platformie Azure (wystąpienia duże)."
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
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Architektura na platformie Azure i SAP HANA (duże wystąpień) — omówienie

## <a name="what-is-sap-hana-on-azure-large-instances"></a>Co to jest SAP HANA na platformie Azure (wystąpienia duże)?

SAP HANA na platformie Azure (wystąpienia duże) jest tooAzure unikatowe rozwiązanie. Ponadto tooproviding, które maszyny wirtualne Azure w celu hello wdrażanie i uruchamianie SAP HANA Azure oferuje hello toorun możliwości i wdrożenie SAP HANA na serwerach bez systemu operacyjnego, które są dedykowane tooyou jako klient. Hello SAP HANA dla rozwiązania Azure (wystąpienia duże) tworzy na sprzęcie bez systemu operacyjnego nieudostępnione/serwera hosta, który jest przypisany tooyou jako klient. sprzęt serwera Hello jest osadzony w większych sygnatury, które zawiera compute/serwer, sieci i infrastruktury magazynu. Które jako połączenie jest certyfikowany TDI HANA. Hello ofertę usługi SAP HANA na platformie Azure (wystąpienia duże) oferuje różne jednostki SKU inny serwer lub rozmiary, począwszy od jednostek, które mają 72 procesorów i toounits 768 GB pamięci, który mają 960 procesory i pamięć 20 TB.

powitania klienta izolacji w ramach sygnatury infrastruktury hello jest wykonywane w dzierżawcami, które szczegółowo wygląda następująco:

- Sieci: Izolacja klientów w ramach infrastruktury stosu za pośrednictwem sieci wirtualnych dla poszczególnych dzierżawców odbiorcy przypisany. Dzierżawa jest przypisany tooa jednego odbiorcy. Klient może mieć wielu dzierżawców. Hello izolacji sieci dzierżawców uniemożliwia komunikację sieciową między dzierżawcami hello infrastruktury sygnatury poziomu. Nawet jeśli dzierżawcy należy toohello tego samego klienta.
- Składniki magazynu: tooit przypisane izolacji za pomocą magazynu maszyn wirtualnych, które mają woluminów magazynu. Woluminy magazynu można przypisać tylko maszyny wirtualnej magazynu tooone. Magazyn maszyny wirtualnej jest przypisane pojedynczej dzierżawy w stosie certyfikowanych infrastruktury SAP HANA TDI hello wyłącznie jest tooone. W związku z tym woluminów magazynu maszyny wirtualnej magazynu tooa przypisane są dostępne w jednym określonym i pokrewnych dzierżawy tylko. I nie są widoczne między hello różnym dzierżawcom wdrożone.
- Serwera lub hosta: jednostka serwera lub host nie jest udostępniana między klientów lub dzierżawców. Serwera lub hosta wdrożone tooa klienta, to jednostka atomic obliczeniowe bez systemu operacyjnego, przypisany tooone pojedynczej dzierżawy. **Nie** jest używane partycjonowanie sprzętowe lub partycjonowanie elastyczne można skutkiem, odbiorcy, udostępnianie hosta lub serwer z innego klienta. Woluminów magazynu, które są przypisane toohello magazynu maszyny wirtualnej dzierżawcy określonych hello są toosuch zainstalowanego serwera. Dzierżawcy mogą mieć różne jednostki magazynowe przypisana wyłącznie jednej jednostki serwera toomany.
- W ramach SAP HANA w sygnaturze infrastruktury platformy Azure (wystąpienia duże) wiele różnych dzierżaw są wdrożone i odizolowane od siebie wzajemnie za pośrednictwem hello pojęcia dzierżawy na poziomie sieci, magazynu i zasobów obliczeniowych. 


Te jednostki bez systemu operacyjnego serwera są obsługiwane toorun SAP HANA w tylko. warstwy aplikacji SAP Hello lub pośredniczącym obciążenie działa w maszynach wirtualnych platformy Azure firmy Microsoft. sygnatury infrastruktury Hello działających hello SAP HANA na platformie Azure (wystąpienia duże) jednostki są toohello połączonych sieci Azure szkieletowymi, tak, zapewniającą łączność małe opóźnienia między maszynami wirtualnymi Azure i SAP HANA w jednostkach Azure (wystąpienia duże).

Ten dokument jest jednym z pięciu dokumentów, które obejmują hello tematem SAP HANA na platformie Azure (wystąpienia duże). W tym dokumencie rozszerzana za pomocą podstawowej architektury hello, obowiązki, usług i ogólne za pośrednictwem funkcji hello rozwiązań. Dla większości hello obszarów, takich jak sieć i łączność hello inne cztery dokumenty są obejmującego szczegółowe informacje i przejść do szczegółów szczegółu. dokumentację Hello SAP HANA na platformie Azure (wystąpienia duże) nie obejmuje aspektów instalacji SAP NetWeaver lub wdrożenia SAP NetWeaver w maszynach wirtualnych platformy Azure. W tym temacie omówiono oddzielna dokumentacja znalezione w hello sam kontener dokumentacji. 


Witaj pięciu części tego przewodnika opisano hello następujące tematy:

- [Architektura na platformie Azure i SAP HANA (duże wystąpienia) — omówienie](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infrastruktura SAP HANA (duże wystąpień) i łączność na platformie Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Jak tooinstall i skonfigurować SAP HANA (duże wystąpień) w systemie Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Rozwiązywanie problemów SAP HANA (duże wystąpień) i monitorowania na platformie Azure](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definicje

Kilka wspólnych definicji są powszechnie używane w hello architektury i technicznej Deployment Guide. Uwaga hello następujące warunki i ich znaczenie:

- **IaaS:** infrastruktura jako usługa
- **PaaS:** platforma jako usługa
- **SaaS:** oprogramowanie jako usługa
- **Składnik programu SAP:** poszczególnych aplikacji SAP, takie jak ECC, BW, Menedżer rozwiązania lub EP. Składniki programu SAP może bazować na tradycyjnych technologii ABAP lub Java lub aplikacji z systemem innym niż NetWeaver na podstawie takich jak obiektów biznesowych.
- **Środowisko SAP:** jeden lub więcej składników programu SAP pogrupowane logicznie tooperform funkcji biznesowych, takich jak projektowanie, QAS, szkolenia, odzyskiwania po awarii lub produkcji.
- **Poziomo SAP:** odwołuje się toohello cały SAP zasoby w orientacji poziomej Twojej IT. Witaj pozioma SAP obejmuje wszystkie produkcyjnych i środowiskach nieprodukcyjnych.
- **Systemu SAP:** hello kombinację DBMS i warstwy aplikacji programistycznej SAP ERP, system testowy programu SAP BW SAP CRM produkcji systemu, itp. Azure wdrożenia nie obsługują dzielenia te dwie warstwy między lokalną i platformą Azure. Oznacza, że systemu SAP jest wdrożonych lokalnie lub jest wdrożony na platformie Azure. Jednak można wdrożyć hello systemów pozioma SAP do platformy Azure lub lokalnie. Na przykład można wdrożyć hello systemów programowania i testowania SAP CRM na platformie Azure, podczas wdrażania hello SAP CRM produkcji systemu lokalnego. SAP HANA na platformie Azure (wystąpienia duże) jest on przeznaczony hostowania warstwy aplikacji SAP hello systemów SAP w maszynach wirtualnych platformy Azure, a następnie hello powiązanym wystąpieniu SAP HANA jednostkę hello HANA dużych wystąpienia sygnatury.
- **Sygnatura wystąpienia dużych:** stos infrastruktury sprzętu SAP HANA TDI certyfikowane i wystąpień SAP HANA toorun w obrębie platformy Azure w wersji dedykowanej.
- **SAP HANA na platformie Azure (duże wystąpienia):** oficjalną nazwą języka dla oferty hello Azure toorun HANA wystąpień w na SAP HANA TDI certyfikowanego sprzętu, które zostało wdrożone w dużych wystąpienia sygnatury w różnych regionach platformy Azure. Witaj powiązane termin **wystąpienia dużych HANA** jest skrót SAP HANA na platformie Azure (wystąpienia duże) i jest powszechnie używany ten przewodnik wdrożenia technicznego.
- **Między lokalizacjami:** opisano scenariusz, w którym maszyny wirtualne są wdrożone tooan subskrypcji Azure, która lokacja lokacja, obejmujący wiele lokacji lub połączenia ExpressRoute między datacenter(s) lokalne powitania i Azure. Dokumentacja wspólnych Azure rodzaju wdrożenia również są opisane jako scenariusze między lokalizacjami. Powodem Hello połączenia hello jest tooextend lokalnej domeny Active Directory/OpenLDAP lokalnymi i lokalnymi DNS na platformie Azure. Hello pozioma lokalnymi jest rozszerzona toohello zasobów Azure hello subskrypcji platformy Azure. Występuje to rozszerzenie, hello maszyn wirtualnych może być częścią domeny lokalne powitania. Użytkownicy domeny hello lokalnej domeny można uzyskać dostępu do serwerów hello i usługi można uruchamiać na tych maszynach wirtualnych (takie jak usługi systemu DBMS). Możliwe jest komunikacji i rozpoznawania nazw między maszyn wirtualnych wdrożonych lokalnie i wdrożone maszyny wirtualne platformy Azure. Takie jest hello typowy scenariusz, w których większość SAP są wdrażane zasoby. Zobacz prowadnice hello [planowania i projektowania dla bramy sieci VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [tworzenie sieci wirtualnej za pomocą połączenia lokacja-lokacja za pomocą portalu Azure hello](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) więcej szczegółowych informacji.
- **Dzierżawy:** klienta wdrożony w dużych wystąpień HANA sygnatury pobiera izolowane do "dzierżawa". Dzierżawa jest izolowana hello sieci, magazynu i warstwy obliczeniowej od pozostałych dzierżawców. Tak tej jednostki magazynu i zasobów obliczeniowych, przypisane toohello różnym dzierżawcom nie widać siebie lub komunikują się ze sobą na powitania HANA dużych wystąpienia sygnatury poziom. Klienta można wybrać toohave wdrożenia w różnych dzierżawców. Nawet wówczas nie występuje komunikacja między dzierżawcami na hello poziomie sygnatury HANA dużych wystąpienia.

Istnieje szereg dodatkowych zasobów, które zostały opublikowane w temacie hello wdrożenia SAP obciążenia w chmurze publicznej Microsoft Azure. Zdecydowanie zaleca się, każdy planowania i wykonywania wdrożenia SAP HANA na platformie Azure jest doświadczony i korzystają z zasad hello Azure IaaS i hello wdrożenia SAP obciążeń na platformie Azure IaaS. Witaj następujące zasoby zawierają dodatkowe informacje i ma być utworzone odwołanie, przed kontynuowaniem:


- [Za pomocą rozwiązania SAP na maszyny wirtualne Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certyfikat

Oprócz hello certyfikacji NetWeaver, SAP wymaga specjalnych certyfikacji SAP HANA toosupport SAP HANA na niektórych infrastruktury, takich jak Azure IaaS.

podstawowe Hello Uwaga SAP NetWeaver i stopień tooa certyfikacji SAP HANA jest [&#1928533; Uwaga SAP — aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure](https://launchpad.support.sap.com/#/notes/1928533).

To [SAP Uwaga #2316233 - SAP HANA w systemie Microsoft Azure (wystąpienia duże)](https://launchpad.support.sap.com/#/notes/2316233/E) również jest znacząca. Obejmuje ona hello rozwiązania opisane w tym przewodniku. Ponadto możesz są obsługiwane toorun SAP HANA hello typu GS5 maszyny Wirtualnej Azure. [Informacje dla tego przypadku są publikowane w witrynie sieci Web hello SAP](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hello SAP HANA dla rozwiązania Azure (wystąpienia duże) określonego tooin SAP Uwaga #2316233 zapewnia firmy Microsoft i SAP klientom Witaj toodeploy możliwości duży pakiet Business SAP, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA lub innych obciążeń SAP HANA na platformie Azure. rozwiązanie Hello jest oparta na powitania HANA SAP, certyfikowane sygnatury dedykowanego sprzętu ([SAP HANA dostosowane Datacenter integracja — TDI](https://scn.sap.com/docs/DOC-63140)). Uruchamianie jako SAP HANA TDI skonfigurowane rozwiązanie zapewnia zaufania hello wiedząc, że wszystkie aplikacje oparte na SAP HANA (w tym SAP Business Suite na SAP HANA, SAP Business magazynu (BW) SAP HANA, S4/HANA i BW4/HANA) będą toowork na powitania Infrastruktura sprzętu.

W porównaniu toorunning SAP HANA w maszynach wirtualnych platformy Azure to rozwiązanie ma korzyści — zapewnia znacznie większych woluminów pamięci. Jeśli chcesz tooenable tego rozwiązania, istnieją toounderstand niektóre kluczowe aspekty:

- Warstwa aplikacji Hello SAP i aplikacji z systemem innym niż SAP Uruchom w maszynach wirtualnych platformy Azure (maszyny wirtualne) hostowanych w hello zwykle sprzętu Azure sygnatury.
- Odbiorcy lokalnej infrastruktury, centra danych oraz wdrożenia aplikacji platformy w chmurze Microsoft Azure toohello połączonych za pośrednictwem usługi Azure ExpressRoute (zalecane) lub wirtualnej sieci prywatnej (VPN). Active Directory (AD) i DNS są również rozszerzać na platformie Azure.
- wystąpienie bazy danych SAP HANA Hello HANA obciążenia działa na SAP HANA na platformie Azure (wystąpienia duże). Sygnatura wystąpienia dużych Hello jest połączony w sieci Azure, więc oprogramowanie na maszynach wirtualnych Azure zakłócają działania w wystąpieniach dużych HANA wystąpienia HANA hello.
- Sprzętu SAP HANA na platformie Azure (wystąpienia duże) jest dedykowany sprzęt podać w przypadku infrastruktury jako usługi (IaaS) za pomocą systemu SUSE Linux Enterprise Server lub Red Hat Enterprise Linux, wstępnie zainstalowane. Zgodnie z maszyn wirtualnych Azure dalszego aktualizacji i systemu operacyjnego toohello konserwacji odpowiada użytkownik.
- Instalacja HANA lub wszelkie dodatkowe składniki niezbędne toorun SAP HANA w jednostkach HANA dużych wystąpień odpowiada, jest odpowiednie wszystkie trwające operacje i administracji SAP HANA na platformie Azure.
- Ponadto toohello rozwiązania opisane w tym miejscu, można zainstalować inne składniki w Twojej subskrypcji platformy Azure, łączącego tooSAP HANA na platformie Azure (wystąpienia duże).  Na przykład te składniki, które umożliwiają komunikację z i/lub bezpośrednio bazy danych SAP HANA toohello (skok, serwery protokołu RDP SAP HANA Studio usług danych SAP dla scenariuszy analizy Biznesowej programu SAP lub rozwiązań w zakresie monitorowania sieci).
- Jak Azure wystąpień dużych HANA oferują obsługi funkcji wysokiej dostępności i odzyskiwania po awarii.

## <a name="architecture"></a>Architektura

Na ogólne hello SAP HANA dla rozwiązania Azure (wystąpienia duże) ma hello SAP warstwy aplikacji znajdujących się w maszynach wirtualnych platformy Azure i hello warstwy bazy danych znajdującej się na sprzęcie TDI SAP skonfigurowane znajduje się w dużych wystąpienia sygnatury w hello na tym samym regionie Azure, która jest połączona tooAzure IaaS.

> [!NOTE]
> Należy warstwy aplikacji toodeploy hello SAP w hello tego samego regionu Azure hello SAP DBMS warstwy. Ta reguła jest dobrze udokumentowane w opublikowanych informacji o SAP obciążenia na platformie Azure. 

Witaj ogólna architektura SAP HANA na platformie Azure (wystąpienia duże) udostępnia SAP TDI certyfikowanym sprzętem konfiguracji (niezwirtualizowanych, systemu operacyjnego, wysokiej wydajności serwera bazy danych SAP HANA hello) i hello możliwości i elastyczność Azure tooscale zasoby dla hello SAP toomeet warstwy aplikacji potrzeb.

![Omówienie architektury SAP HANA na platformie Azure (wystąpienia duże)](./media/hana-overview-architecture/image1-architecture.png)

Architektura Hello wyświetlany jest podzielony na trzy części:

- **Prawo:** infrastruktury lokalnej z różnych aplikacji w centrach danych użytkownikom końcowym dostęp do aplikacji FIRMOWYCH (np. SAP). W idealnym przypadku to lokalnej infrastruktury jest następnie połączony tooAzure z platformy Azure, [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Centrum:** pokazuje Azure IaaS oraz, w tym przypadku korzystanie z maszyn wirtualnych platformy Azure toohost SAP lub inne aplikacje, które używają SAP HANA jako DBMS system. Mniejsze wystąpień HANA zapewniające funkcji z pamięci hello maszynach wirtualnych platformy Azure są wdrażane w maszynach wirtualnych platformy Azure, wraz z ich warstwy aplikacji. Dowiedz się więcej o [maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machines/).
<br />Sieć platformy Azure jest systemów SAP toogroup używane razem z innych aplikacji w sieciach wirtualnych platformy Azure (sieci wirtualne). Te sieci wirtualne połączyć systemów tooon lokalnych, jak również tooSAP HANA na platformie Azure (wystąpienia duże).
<br />SAP NetWeaver aplikacji i baz danych, które są obsługiwane toorun platformie Microsoft Azure, zobacz [&#1928533; SAP Obsługa Uwaga — aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure](https://launchpad.support.sap.com/#/notes/1928533). Dokumentacja na temat wdrażania rozwiązania SAP na platformie Azure należy przejrzeć:

  -  [Za pomocą programu SAP na maszynach wirtualnych systemu Windows (VM)](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Za pomocą rozwiązania SAP na maszyny wirtualne Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Po lewej:** pokazuje hello SAP HANA TDI certyfikowanego sprzętu w hello Azure dużych wystąpienia sygnatury. jednostki wystąpienia dużych HANA Hello są toohello połączonych sieci wirtualnych platformy Azure z subskrypcji przy użyciu hello tej samej technologii co hello łączność z lokalnymi na platformie Azure.

Sygnatura wystąpienia dużych Azure Hello, sama łączy hello następujące składniki:

- **Obliczanie:** serwerów, które są oparte na Intel Xeon E7-8890v3 lub Intel Xeon E7-8890v4 procesorów, które hello niezbędne możliwości obliczeniowych i SAP HANA certyfikowane.
- **Sieć:** A unified szybkich sieci szkieletowej, łączącego hello przetwarzania danych, magazynu i składników sieci LAN.
- **Magazyn:** infrastruktury magazynu, który jest dostępny za pośrednictwem ujednoliconego sieci szkieletowej. Określonej pojemności została podana w zależności od hello wdrażany określonych SAP HANA konfiguracji platformy Azure (wystąpienia duże) (większej pojemności magazynu jest dostępna w dodatkowych miesięczny koszt).

W ramach hello wielodostępnej infrastrukturze sygnatura wystąpienia dużych hello klienci są wdrażane jako izolowanego dzierżaw. Na wdrożenie hello dzierżawy należy tooname subskrypcji platformy Azure w ramach Twojej rejestracji platformy Azure. Ten będzie toobe hello subskrypcji platformy Azure, hello HANA dużych wystąpienia będzie rozliczane przed toobe. Te dzierżawy mają relację 1:1 toohello subskrypcji platformy Azure. Sieci rozsądnego jest możliwe tooaccess HANA dużych wystąpienia jednostki wdrożyć w jednej dzierżawy w jednym regionie Azure z różnych sieci wirtualnych platformy Azure, których należy toodifferent subskrypcji platformy Azure. Chociaż te subskrypcje platformy Azure muszą toobelong toohello tego samego rejestracji platformy Azure. 

Podobnie jak w przypadku maszyn wirtualnych platformy Azure, SAP HANA na platformie Azure (wystąpienia duże) jest oferowana w wielu regionach platformy Azure. W funkcji odzyskiwania po awarii toooffer kolejności można wybrać tooopt w. Różne sygnatury dużych wystąpienie w ramach jednego regionu politycznej geograficznie są połączone tooeach innych. Na przykład HANA dużych wystąpienia sygnatury nam zachód i nam wschodnie są połączone za pośrednictwem dedykowanej sieci łącza hello w celu replikacji odzyskiwania po awarii. 

Tak samo, jak można wybrać różne typy maszyny Wirtualnej z maszyn wirtualnych platformy Azure, są dostępne różne jednostki SKU z HANA dużych wystąpień dostosowanych dla obciążenia różnych rodzajów SAP HANA. SAP stosuje stosunek gniazda tooprocessor pamięci dla różnych obciążeń oparte na generacje procesorów Intel hello — istnieją cztery różne typy jednostki SKU oferowane:

Począwszy od 2017 lipca SAP HANA na platformie Azure (wystąpienia duże) jest dostępny w kilka konfiguracji w programie hello Azure regionów z NAMI zachód i nam wschodnie, Australia Wschodnia, Australia Południowo-Wschodnia, Europa Zachodnia i Europa Północna:

| Rozwiązanie SAP | Procesor CPU | Memory (Pamięć) | Magazyn | Dostępność |
| --- | --- | --- | --- | --- |
| Zoptymalizowana pod kątem OLAP: programu SAP BW BW/4HANA<br /> lub SAP HANA dla ogólnych obciążeń OLAP | SAP HANA na Azure S72<br /> — 2 procesor Intel Xeon® x E7 8890 v3<br /> 36 rdzeni Procesora i 72 wątków CPU |  768 GB |  3 TB | Dostępna |
| --- | SAP HANA na Azure S144<br /> – 4 procesor Intel Xeon® x E7 8890 v3<br /> 72 rdzeni Procesora i 144 wątków CPU |  1,5 TB |  6 TB | Nieoferowane już |
| --- | SAP HANA na Azure S192<br /> – 4 procesor Intel Xeon® x E7 8890 v4<br /> 96 rdzeni Procesora i 192 wątków CPU |  2.0 TB |  8 TB | Dostępna |
| --- | SAP HANA na Azure S384<br /> – 8 procesor Intel Xeon® x E7 8890 v4<br /> 192 rdzeni Procesora i 384 wątków CPU |  4.0 TB |  16 TB | Gotowe tooOrder |
| Zoptymalizowana pod kątem OLTP: SAP Business Suite<br /> SAP HANA lub S/4HANA (OLTP)<br /> ogólny OLTP | SAP HANA na Azure S72m<br /> — 2 procesor Intel Xeon® x E7 8890 v3<br /> 36 rdzeni Procesora i 72 wątków CPU |  1,5 TB |  6 TB | Dostępna |
|---| SAP HANA na Azure S144m<br /> – 4 procesor Intel Xeon® x E7 8890 v3<br /> 72 rdzeni Procesora i 144 wątków CPU |  3.0 TB |  12 TB | Nieoferowane już |
|---| SAP HANA na Azure S192m<br /> – 4 procesor Intel Xeon® x E7 8890 v4<br /> 96 rdzeni Procesora i 192 wątków CPU  |  4.0 TB |  16 TB | Dostępna |
|---| SAP HANA na Azure S384m<br /> – 8 procesor Intel Xeon® x E7 8890 v4<br /> 192 rdzeni Procesora i 384 wątków CPU |  6.0 TB |  18 TB | Gotowe tooOrder |
|---| SAP HANA na Azure S384xm<br /> – 8 procesor Intel Xeon® x E7 8890 v4<br /> 192 rdzeni Procesora i 384 wątków CPU |  8.0 TB |  22 TB |  Gotowe tooOrder |
|---| SAP HANA na Azure S576<br /> – 12 procesor Intel Xeon® x E7 8890 v4<br /> 288 rdzeni Procesora i 576 wątków CPU |  12.0 TB |  28 TB | Gotowe tooOrder |
|---| SAP HANA na Azure S768<br /> – 16 procesor Intel Xeon® x E7 8890 v4<br /> 384 rdzeni Procesora i 768 wątków CPU |  16.0 TB |  36 TB | Gotowe tooOrder |
|---| SAP HANA na Azure S960<br /> – 20 procesor Intel Xeon® x E7 8890 v4<br /> 480 rdzeni Procesora i 960 wątków CPU |  20.0 TB |  46 TB | Gotowe tooOrder |

- Rdzenie procesora CPU = suma nie-Procesora rdzeni hiperwątkowych sum hello procesorów hello powitania serwera jednostki.
- Wątków procesora CPU = Suma wątków obliczeniowe udostępniane przez hiperwątkowych rdzeni Procesora, sum hello procesorów hello powitania serwera jednostki. Wszystkie jednostki są konfigurowane przez domyślny toouse funkcji Hyper-Threading.


Witaj różne konfiguracje powyżej, które są dostępne lub "nie są oferowane już" odwołuje się [&#2316233; SAP Obsługa Uwaga — SAP HANA w systemie Microsoft Azure (wystąpienia duże)](https://launchpad.support.sap.com/#/notes/2316233/E). Hello konfiguracje, które są oznaczone jako "Gotowy tooOrder" szybko znaleźć ich wejściem w hello Uwaga SAP. Jednak te wystąpienia jednostki SKU może zostać określona już dla hello sześciu różnych regionach platformy Azure hello HANA dużych wystąpienie usługi jest dostępna.

Konkretne konfiguracje Hello wybrany są zależne od obciążenia, zasobów procesora CPU i pamięci żądany. Istnieje możliwość hello tooleverage obciążenia OLTP jednostki magazynowe, które są zoptymalizowane pod kątem obciążeń OLAP. 

podstawowa dla wszystkich ofert hello sprzętu Hello są SAP HANA TDI certyfikowane. Jednak wyróżnia się między dwoma różnymi klasami sprzętu, która dzieli jednostki SKU hello do:

- S72, S72m S144, S144m, S192 i S192m, które firma Microsoft można znaleźć hello tooas I klasy typu jednostek magazynowych.
- S384, S384m S384xm, S576, S768 i S960, które firma Microsoft można znaleźć tooas Witaj "class typu II' SKU.

Jest ważne toonote, które pełnej sygnatury HANA dużych wystąpienia nie jest wyłącznie przydzielone dla jednego odbiorcy &#39; Użyj s. Ten fakt stosuje toohello stojakami zasoby obliczeniowe i magazynujące, które są połączone za pośrednictwem sieci szkieletowej również wdrożona na platformie Azure. Duże wystąpień HANA infrastruktury, takich jak Azure, wdraża różnych klientów &quot;dzierżawców&quot; które są odizolowane od siebie w hello następujące trzy poziomy:

- Sieci: Izolacja za pośrednictwem sieci wirtualnych w ramach hello HANA dużych wystąpienia sygnatury.
- Magazyn: Izolacji za pomocą magazynu maszyn wirtualnych, które mają woluminów magazynu przypisane i izolowanie woluminów magazynu między dzierżawcami.
- Obliczeniowe: Przypisanie dedykowanego serwera jednostki tooa pojedynczej dzierżawy. Nie trudne lub partycjonowanie elastyczne jednostek serwera. Bez udostępniania jednego serwera lub hosta jednostki między dzierżawcami. 

W związku wdrożeń hello HANA wystąpień dużych jednostek od różnych dzierżawców nie są widoczne w innych tooeach. Nie może HANA dużych jednostek wystąpienia wdrożone w różnych dzierżawców komunikować się bezpośrednio ze sobą na poziomie sygnatury wystąpienia dużych HANA hello. Tylko HANA dużych wystąpienia jednostek w ramach jednego dzierżawcy mogą komunikować się tooeach innych na hello poziomie sygnatury HANA dużych wystąpienia.
Dzierżawcy wdrożonej w sygnatura wystąpienia dużych hello jest przypisany rozliczeń tooone rozsądnego subskrypcji platformy Azure. Jednak wise sieci, które są dostępne z sieciami wirtualnymi platformy Azure z innych subskrypcji platformy Azure w ramach hello tego samego rejestracji platformy Azure. W przypadku wdrożenia z innej subskrypcji platformy Azure w hello sam region platformy Azure, możesz również wybrać tooask rozdzielonych dzierżawcy HANA dużych wystąpienia.

Brak istotnych różnic między systemem SAP HANA HANA dużych wystąpień i SAP HANA działające na maszynach wirtualnych Azure wdrożona na platformie Azure:

- Nie ma żadnych warstwa wirtualizacji dla SAP HANA na platformie Azure (wystąpienia duże). Otrzymasz wydajność hello sprzętu bez systemu operacyjnego dla źródłowego hello.
- W przeciwieństwie do usługi Azure hello SAP HANA na serwerze Azure (wystąpienia duże) jest dedykowany tooa określonego klienta. Nie było możliwości czy jednostki serwera lub hosta jest trudne lub elastyczne podzielona na partycje. W związku z tym jednostki HANA dużych wystąpienia jest używany jako przypisany jako dzierżawca całego tooa i z tego tooyou jako klient. Ponowne uruchomienie lub zamknięcie powitania serwera nie prowadzi automatycznie toohello systemu operacyjnego i SAP HANA wdrażany na innym serwerze. (Dla typu klasy I jednostki SKU, hello jedynym wyjątkiem jest Jeśli serwer mogą wystąpić problemy i ponowne wdrożenie musi toobe wykonywane na innym serwerze.)
- W przeciwieństwie do usługi Azure, których typy procesora hosta w przypadku wybrania dla hello najlepsze stosunek ceny do wydajności typy procesora hello wybrany dla SAP HANA na platformie Azure (wystąpienia duże) są hello najwyższy wykonywanie wierszu procesor Intel E7v3 i E7v4 hello.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Uruchamianie wielu wystąpień SAP HANA na jedną jednostkę HANA dużych wystąpienia
Jest możliwe toohost, więcej niż jednego aktywnego wystąpienia SAP HANA na powitania HANA dużych wystąpienia jednostki. W kolejności toostill zapewniają możliwości hello migawek przechowywania i odzyskiwania po awarii, taka konfiguracja wymaga woluminu, ustaw dla każdego wystąpienia. Od tej chwili hello HANA dużych wystąpienia jednostki można podzielić w następujący sposób:

- S72, S72m S144, S192: W przyrostach 256 GB z najmniejszą hello 256 GB uruchamianie jednostki. Wielokrotności jak 256 GB, 512 GB i tak dalej, może być maksymalna łączna toohello pamięci hello hello jednostki.
- S144m i S192m: W przyrostach 256 GB z 512 GB hello najmniejsza jednostka. Wielokrotności jak 512 GB, 768 GB i tak dalej, może być maksymalna łączna toohello pamięci hello hello jednostki.
- Typ klasy II: wielokrotnością 512 GB z hello najmniejszą początkowa jednostki 2 TB. Wielokrotności jak 512 GB, 1 TB, 1,5 TB i tak dalej, może być maksymalna łączna toohello pamięci hello hello jednostki.

Przykłady uruchamianie wielu wystąpień SAP HANA może wyglądać jak:

| SKU | Rozmiar pamięci | Rozmiar magazynu | Rozmiary z wieloma bazami danych |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | Wystąpienie HANA 1 x 768 GB<br /> lub wystąpienie 1 x 512 GB + 1 x 256 GB wystąpienia<br /> lub wystąpień 3 x 256 GB | 
| S72m | 768 GB | 3 TB | 3x512GB HANA wystąpień<br />lub wystąpienie 1 x 512 GB + 1 x 1 TB wystąpienia<br />lub wystąpień 6 x 256 GB<br />lub wystąpienie 1x1.5 TB | 
| S192m | 4 TB | 16 TB | 8 x 512 GB wystąpień<br />lub wystąpień 4 x 1 TB<br />lub wystąpień 4 x 512 GB + 2 x 1 TB wystąpień<br />lub wystąpień 4 x 768 GB + 2 x 512 GB wystąpień<br />lub wystąpienie. 1 x 4 TB |
| S384xm | 8 TB | 22 TB | 4 x 2 TB wystąpień<br />lub wystąpień 2 x 4 TB<br />lub wystąpień 2 x 3 TB + 1 x 2 TB wystąpień<br />lub wystąpień 2x2.5 TB + 1 x 3 TB wystąpień<br />lub wystąpienie. 1 x 8 TB |


Otrzymasz hello pomysłu. Na pewno istnieją także inne różnice. 


## <a name="operations-model-and-responsibilities"></a>Operacje modelu i jego obowiązki

usługi Hello z SAP HANA na platformie Azure (wystąpienia duże) jest wyrównywana z usług Azure IaaS. Możesz pobrać wystąpienia HANA dużych wystąpień z zainstalowanym systemem operacyjnym jest zoptymalizowany pod kątem SAP HANA. Zgodnie z maszyn wirtualnych z IaaS platformy Azure, większość zadań hello wzmocnienia zabezpieczeń hello systemu operacyjnego, instalowania dodatkowego oprogramowania, potrzebne, instalowanie HANA, operacyjnego hello systemu operacyjnego i HANA i aktualizowanie hello systemu operacyjnego i HANA odpowiada użytkownik. Microsoft nie wymusza aktualizacje systemu operacyjnego lub HANA aktualizacje w przypadku.

![Obowiązki SAP HANA na platformie Azure (wystąpienia duże)](./media/hana-overview-architecture/image2-responsibilities.png)

Jak widać w powyższym diagramie hello SAP HANA na platformie Azure (wystąpienia duże) jest wielodostępne infrastruktury jako oferty usługi. I w związku z tym hello podział odpowiedzialności znajduje się na granicy infrastruktury systemu operacyjnego hello, hello większości. Microsoft jest odpowiedzialny za wszystkie aspekty usługi hello poniżej wiersza hello hello systemu operacyjnego i jest odpowiedzialny powyżej hello wiersza, w tym hello systemu operacyjnego. Tak najbardziej aktualne lokalnymi metody mogą być których zastosowano zgodności, zabezpieczeń, zarządzanie aplikacjami, podstawy i systemu operacyjnego zarządzania mogą nadal toobe używane. systemy Hello są wyświetlane tak, jakby znajdują się w sieci w odniesieniu do wszystkich.

Jednak ta usługa jest zoptymalizowana pod kątem SAP HANA, więc obszary, w której Tobą a firmą Microsoft muszą toowork razem toouse hello podstawowej infrastruktury możliwości uzyskania najlepszych wyników.

powitania po liście zapewnia bardziej szczegółowo w każdej warstwy hello i Twoje obowiązki:

**Sieć:** wszystkie hello sieciach wewnętrznych dla sygnatury dużych wystąpienia hello systemem SAP HANA jego dostęp do magazynu toohello łączności między wystąpieniami hello (na potrzeby skalowania w poziomie i inne funkcje), pozioma toohello połączenia i łączność tooAzure, w którym znajduje się w usłudze Azure Virtual Machines warstwy aplikacji hello SAP. Zawiera także połączenia sieci WAN między centrach danych platformy Azure dla replikacji celów odzyskiwania po awarii. Wszystkie sieci są podzielone na partycje przez dzierżawcę hello oraz zastosować QOS.

**Magazyn:** hello wirtualizację partycjonowanej magazynu dla wszystkich woluminów wymagane przez serwery SAP HANA hello, a także migawki. 

**Serwery:** hello dedykowanych serwerów fizycznych toorun hello bazami danych HANA SAP przypisane tootenants. Hello serwerów hello typie I klas jednostek magazynowych są pobieranej sprzętu. Z tych typów serwerów konfiguracji serwera hello są zbierane i przechowywane w profilach, mogą zostać przeniesione z jednego sprzętu fizycznego tooanother sprzętu fizycznego. Takie (ręczna) przenoszenie profilu przez operacje można porównać coś tooAzure usługi naprawianie. serwery Hello hello jednostki SKU klasy II typu nie są oferty takiej możliwości.

**SDDC:** oprogramowania do zarządzania hello, które jest używane toomanage danych Centrum oprogramowania zdefiniowane jednostki. Umożliwia on Microsoft toopool zasobów skali, dostępności i optymalnej wydajności.

**Systemu operacyjnego:** hello wybierz (SUSE Linux lub Red Hat Linux) systemu operacyjnego uruchomionego na powitania serwerów. obrazy Hello systemu operacyjnego, są udostępniane są obrazy hello podał hello poszczególnych Linux dostawcy tooMicrosoft hello w celu uruchamiania SAP HANA. Jesteś toohave wymagana subskrypcja z producentem Linux hello hello określonego obrazu zoptymalizowanych pod kątem SAP HANA. Twoje obowiązki obejmują rejestrowanie obrazów hello hello dostawcy systemu operacyjnego. Z punktu hello przekazanie przez firmę Microsoft możesz są również odpowiedzialne za wszelkie dodatkowe stosowanie poprawek systemu operacyjnego Linux hello. Tej poprawki również obejmuje dodatkowe pakiety, które mogą być wymagane do pomyślnej instalacji SAP HANA (można znaleźć w dokumentacji instalacji HANA i uwagi SAP tooSAP w) i które nie zostały uwzględnione hello określonego dostawcy systemu Linux w ich SAP HANA. Zoptymalizowane obrazy systemu operacyjnego. odpowiedzialność Hello powitania klienta obejmuje również poprawki dla hello systemu operacyjnego jest powiązane toomalfunction/optymalizacji hello systemu operacyjnego i jego sprzętu sterowniki pokrewne toohello określonego serwera. Lub zabezpieczeń ani funkcjonalności stosowania poprawek hello systemu operacyjnego. Odpowiedzialność klienta jest również monitorowania i planowania pojemności programu:

- Zużycie zasobów procesora CPU
- Zużycie pamięci
- Powiązane toofree woluminy miejsca, IOPS i opóźnienia
- Ruch sieciowy woluminu między wystąpieniem dużych HANA i warstwy aplikacji SAP

Hello podstawowej infrastruktury wystąpień dużych HANA udostępnia funkcje tworzenia kopii zapasowych i przywracania hello woluminu systemu operacyjnego. Z tej funkcji jest również obowiązkiem użytkownika.

**Oprogramowanie pośredniczące:** hello SAP HANA wystąpienia, przede wszystkim. Administracji, operacje i monitorowania są Twoje odpowiedzialności. Brak funkcji, pod warunkiem, który pozwala toouse magazynu migawek dla celów odzyskiwania po awarii i wykonywania kopii zapasowej i przywracania. Te możliwości są udostępniane przez hello infrastruktury. Jednak Twoje obowiązki również obejmować projektowanie wysokiej dostępności i odzyskiwania po awarii dzięki takim funkcjom, wykorzystaniu je i monitorowania, czy migawki magazynu zostały wykonane pomyślnie.

**Dane:** danych zarządzanych przez SAP HANA i innych danych, takich jak kopie zapasowe udziałów plików znajdujących się na woluminach lub pliku. Twoje obowiązki obejmują monitorowanie wolnego miejsca na dysku i zarządzanie zawartością hello na woluminach hello i monitorowanie hello pomyślne wykonanie kopii zapasowych woluminów dysków i pamięci masowej migawki. Pomyślne wykonanie witryn tooDR replikacji danych jest jednak hello odpowiedzialność firmy Microsoft.

**Aplikacje:** hello SAP wystąpień aplikacji lub w przypadku aplikacji z systemem innym niż SAP, warstwy aplikacji hello tych aplikacji. Twoje obowiązki obejmują wdrażania, zarządzania, operacje, i monitorowania tych aplikacji powiązanych toocapacity planowania użycia zasobów procesora CPU, zużycie pamięci, użycia magazynu Azure i zużycie przepustowości sieci w ramach Sieci wirtualne platformy Azure i z sieciami wirtualnymi platformy Azure tooSAP HANA na platformie Azure (wystąpienia duże).

**WAN:** hello połączeń ustanowić z lokalnego wdrożenia tooAzure dla obciążeń. Naszych klientów z wystąpieniami dużych HANA Użyj Azure ExpressRoute dla łączności. To połączenie nie jest częścią hello SAP HANA na rozwiązanie Azure (wystąpienia duże), dlatego jest odpowiedzialny za hello instalacji tego połączenia.

**Archiwum:** łączyli tooarchive kopii danych przy użyciu własnych metod na kontach magazynu. Archiwizowanie wymaga zarządzania, zgodności kosztów i operacji. Jest odpowiedzialny za Generowanie kopie archiwum i kopii zapasowych na platformie Azure i przechowywania ich w sposób zgodny.

Zobacz hello [umowy SLA dla SAP HANA na platformie Azure (wystąpienia duże)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Zmiana rozmiaru

Zmiany rozmiaru dla wystąpień dużych HANA nie różni się od rozmiaru dla HANA ogólnie. Dla istniejących i wdrażane systemy, ma toomove z innych tooHANA RDBMS, SAP udostępnia wiele raportów, które Uruchom istniejących systemach SAP. Jeśli baza danych hello jest tooHANA przeniesiony, te raporty sprawdzenie, czy dane hello i obliczyć wymagania dotyczące pamięci dla wystąpienia HANA hello. Przeczytaj powitania po tooget uwagi SAP więcej informacji na temat sposobu toorun te raporty i w jaki sposób tooobtain ich najnowszych poprawek/wersji:

- [Uwaga SAP #1793345 - zmiany rozmiaru pakietu SAP na HANA](https://launchpad.support.sap.com/#/notes/1793345)
- [Uwaga &#1872170; - pakiet w raporcie zmiany rozmiaru HANA i S/4 HANA SAP](https://launchpad.support.sap.com/#/notes/1872170)
- [Uwaga SAP #2121330 — często zadawane pytania: Programu SAP BW na HANA zmiany rozmiaru raportu](https://launchpad.support.sap.com/#/notes/2121330)
- [Uwaga &#1736976; - raport rozmiaru dla BW na HANA SAP](https://launchpad.support.sap.com/#/notes/1736976)
- [SAP Uwaga #2296290 — nowy raport rozmiaru dla BW na HANA](https://launchpad.support.sap.com/#/notes/2296290)

Implementacje zielony pola SAP szybkie Rozmiar symboli jest wymagania dotyczące pamięci dostępne toocalculate hello implementacji oprogramowania SAP na górze HANA.

Wymagania dotyczące pamięci dla HANA rosną wraz z rozwojem ilość danych, tak toobe uwagę hello zużycie pamięci i zawierać stanie toopredict co to jest toobe będzie w hello przyszłych. Oparte na powitania wymagania dotyczące pamięci, można wówczas zmapować Twoje żądanie do jednego z hello jednostki SKU HANA dużych wystąpienia.

## <a name="requirements"></a>Wymagania

Ta lista składana wymagania dotyczące systemu SAP HANA na platformie Azure (wystąpienia większy).

**Microsoft Azure:**

- Subskrypcja platformy Azure, które mogą być połączone tooSAP HANA na platformie Azure (wystąpienia duże).
- Microsoft Premier umowę dotyczącą pomocy technicznej. Zobacz [&#2015553; SAP Obsługa Uwaga — SAP w systemie Microsoft Azure: wymagania wstępne dotyczące pomocy technicznej](https://launchpad.support.sap.com/#/notes/2015553) Aby uzyskać szczegółowe informacje dotyczące toorunning SAP na platformie Azure. Używanie HANA dużych wystąpienia jednostki z 384 i większej liczby procesorów CPU, należy również hello tooextend tooinclude umowy pomocy technicznej Premium Azure szybkie odpowiedzi (ARR).
- Rozpoznawanie hello HANA dużych wystąpienia jednostki SKU użytkownik musi po wykonaniu zmiany rozmiaru korzystają z programu SAP.

**Połączenie sieciowe:**

- Usługa Azure ExpressRoute między lokalnymi tooAzure: tooconnect lokalnymi tooAzure centrum danych, upewnij się, że tooorder co najmniej 1 GB/s połączenia od usługodawcy internetowego. 

**System operacyjny:**

- Licencji w systemie SUSE Linux Enterprise Server 12 SAP aplikacji.

> [!NOTE] 
> Witaj systemu operacyjnego dostarczane przez firmę Microsoft nie jest zarejestrowany w systemie SUSE ani nie jest połączony z wystąpieniem SMT.

- SUSE Linux subskrypcji zarządzania narzędzia (SMT) wdrożona na platformie Azure na maszynie Wirtualnej platformy Azure. Zapewnia możliwość hello SAP HANA na toobe Azure (wystąpienia duże) rejestrowane i odpowiednio aktualizowane przez SUSE (ponieważ nie ma żadnych dostęp do Internetu w obrębie centrum danych wystąpienia dużych HANA). 
- Licencje Red Hat Enterprise Linux 6.7 lub 7.2 dla SAP HANA.

> [!NOTE]
> Hello systemu operacyjnego dostarczane przez firmę Microsoft nie jest zarejestrowany w Red Hat nie jest połączony it tooa Red Hat subskrypcji Menedżera wystąpienia.

- Red Hat subskrypcji Menedżera wdrożona na platformie Azure na maszynie Wirtualnej platformy Azure. Hello Red Hat subskrypcji Menedżera zapewnia możliwość hello SAP HANA na toobe Azure (wystąpienia duże) rejestrowane i odpowiednio aktualizowane przez Red Hat (ponieważ nie ma żadnych bezpośredni dostęp do Internetu z w ramach dzierżawy hello wdrożone na powitania sygnatura wystąpienia dużych Azure).
- SAP wymaga toohave obsługi kontraktu u swojego dostawcy systemu Linux. To wymaganie jest zachowywana przez rozwiązanie hello faktu HANA wystąpień dużych lub hello który Twojej uruchamiania systemu Linux na platformie Azure. W przeciwieństwie do niektórych hello Linux Azure galerii obrazów, opłaty za usługę hello nie wchodzi w oferta rozwiązania hello HANA dużych wystąpień. Jest on możesz jako toofulfill hello wymagań klientów SAP dotyczących umów pomocy technicznej z dystrybutorem Linux hello.   
   - W systemie SUSE Linux, wyszukiwanie hello wymagania dotyczące obsługi kontraktu w [SAP Uwaga #1984787 - SUSE LINUX Enterprise Server 12: informacje o instalacji](https://launchpad.support.sap.com/#/notes/1984787) i [&#1056161; Uwaga SAP - SUSE priorytet obsługę aplikacje SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Red Hat Linux należy toohave hello poprawną subskrypcję poziomy, które obejmują pomocy technicznej i usługi (systemy operacyjne toohello HANA wystąpień dużych aktualizacji. Red Hat zaleca się wprowadzenie subskrypcję "RHEL dla SAP aplikacji biznesowych". Dotyczących usług i pomocy technicznej, sprawdź [SAP Uwaga #2002167 - Red Hat Enterprise Linux 7.x: instalacji i uaktualniania](https://launchpad.support.sap.com/#/notes/2002167) i [SAP Uwaga #1496410 - Red Hat Enterprise Linux 6.x: instalacji i uaktualniania](https://launchpad.support.sap.com/#/notes/1496410) szczegółowe informacje.

**Baza danych:**

- Licencje i składników instalacji oprogramowania SAP HANA (platforma lub enterprise edition).

**Aplikacje:**

- Licencje i składniki instalacji oprogramowania aplikacje SAP, łączenia tooSAP HANA i powiązanych umów pomocy technicznej SAP.
- Licencje i składniki instalacji oprogramowania dla aplikacji z systemem innym niż SAP używana w relacji tooSAP HANA w środowisku Azure (wystąpienia duże) i powiązanych umów pomocy technicznej.

**Umiejętności:**

- Środowisko i wiedzy na IaaS platformy Azure i jej składniki.
- Środowisko i wiedzy na temat wdrażania SAP obciążenia na platformie Azure.
- SAP HANA instalacji certyfikowane osobistych.
- SAP, architektów umiejętności toodesign wysokiej dostępności i odzyskiwania po awarii wokół SAP HANA.

**SAP:**

- Oczekuje się, klienci SAP i obsługuje kontraktu o SAP
- Szczególnie w przypadku wdrożeń na powitania II typu klasy jednostki SKU HANA dużych wystąpienia zdecydowanie zaleca tooconsult z SAP w wersjach programu SAP HANA i konfiguracje ostatecznego na dużych rozmiarze sprzętu skalowanie w pionie.


## <a name="storage"></a>Magazyn

Witaj układu magazynu dla SAP HANA na platformie Azure (wystąpienia duże) jest konfigurowana przy SAP HANA na zarządzania usługą Azure za pośrednictwem SAP zalecane wytyczne udokumentowane w hello [SAP HANA przestrzeni dyskowej jest potrzebne](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) oficjalny dokument.

Hello HANA dużych wystąpień hello typ klasy I są dostarczane z cztery razy hello pamięci wolumin jako wolumin magazynu. Dla typu klasy II HANA wystąpienia dużych jednostek hello hello magazynu nie będzie toobe cztery razy więcej. Witaj pochodzi z woluminem, który jest przeznaczony do przechowywania kopii zapasowej dziennika transakcji HANA. Znajdź więcej szczegółów w [jak tooinstall i skonfigurować SAP HANA (duże wystąpień) w systemie Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Zobacz hello w poniższej tabeli pod względem Alokacja magazynu. Witaj tabela zawiera listę około hello pojemności dla różnych woluminach hello wyposażone w różnych jednostkach wystąpienia dużych HANA hello.

| HANA dużych wystąpienia jednostki SKU | Hana/danych | Hana/dziennika | Hana/udostępnionych | Hana / / kopii zapasowej dziennika |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12 000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16 000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20 000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | UŻYWANE 28 000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36,000 GB | 4100 GB | 2050 GB | 4100 GB |


Rzeczywiste woluminów wdrożonej zależą nieco wdrożenia i narzędzie, które jest używane tooshow hello rozmiarów.

Jeśli podzielić SKU wystąpienia z dużych HANA, kilka przykładów części dzielenia możliwe będzie wyglądała:

| Pamięć partycji w GB | Hana/danych | Hana/dziennika | Hana/udostępnionych | Hana / / kopii zapasowej dziennika |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Rozmiary są liczbami nierównej woluminów, które może różnić się nieznacznie oparte na wdrożenia i narzędzia używane toolook na powitania woluminów. Są także innych rozmiarów partycji thinkable, takich jak 2,5 TB. Rozmiary magazynu będzie obliczana formułą podobnie jak używane dla partycji hello powyżej. Hello termin "partycji" nie wskazuje, czy system operacyjny hello, pamięć lub zasoby procesora CPU są w żadnym podzielone na partycje. Wskazuje on, po prostu partycji magazynu dla różnych wystąpień HANA hello, może być toodeploy na jednym z jednym HANA dużych wystąpienia jednostki. 

Ponieważ klient może być wymagane dla miejsca do magazynowania, należy hello możliwości tooadd magazynu toopurchase dodatkowego magazynu w jednostkach 1 TB. Ten dodatkowy magazyn może być dodany jako dodatkowe woluminu lub mogą być używane tooextend co najmniej jeden z istniejących woluminów hello. Nie jest możliwe toodecrease hello rozmiarów woluminów hello pierwotnie wdrożone, a przede wszystkim udokumentowane przez tabel hello powyżej. Ponadto nie jest możliwe toochange hello nazwy woluminów hello lub instalacji. woluminy magazynu Hello opisane powyżej są dołączone toohello HANA dużych wystąpienia jednostki jako woluminy NFS4.

Klientów można toouse magazynu migawek dla wykonywania kopii zapasowej i przywracania i odzyskiwaniem po awarii do celów odzyskiwania. Więcej informacji na ten temat wyszczególnione w [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Szyfrowanie nieużywanych danych
Magazyn Hello używany dla wystąpień dużych HANA umożliwia przezroczystego szyfrowania danych hello są przechowywane na dyskach hello. Podczas wdrażania dużych jednostki HANA wystąpienia mają toohave opcji hello tego rodzaju włączone szyfrowanie. Możesz również wybrać toochange woluminów tooencrypted po wdrożeniu hello już. Przenieś Hello z woluminów niezaszyfrowane tooencrypted jest niewidoczny i nie wymaga przestojów. 

Z hello typie I klas jednostek SKU, hello woluminu hello rozruchu, jednostka LUN jest przechowywana na, są szyfrowane. W przypadku typu hello klasy II jednostki SKU z HANA dużych wystąpień należy tooencrypt hello rozruch jednostki LUN z metody systemu operacyjnego. 


## <a name="networking"></a>Sieć

Architektura Hello Azure Networking to wdrożenie toosuccessful kluczowym składnikiem aplikacji SAP w wystąpieniach dużych HANA. Zazwyczaj SAP HANA we wdrożeniach Azure (wystąpienia duże) mają większy pozioma SAP z kilku różnych rozwiązań SAP o różnych rozmiarach baz danych, użycie zasobów procesora CPU i użycie pamięci. Prawdopodobnie nie wszystkie tych systemów SAP są oparte na SAP HANA, więc prawdopodobnie hybrydowych, który używa programu SAP orientacji poziomej:

- Wdrażane SAP systemów lokalnych. Powodu rozmiary tootheir tych systemów aktualnie nie może być umieszczona w środowisku Azure. Klasycznym przykładem może być uruchomiona na serwerze SQL firmy Microsoft (jako hello bazy danych), co wymaga więcej systemu SAP ERP produkcji lub zapewniają zasobów pamięci maszyn wirtualnych platformy Azure.
- Wdrożona na podstawie SAP HANA SAP systemów lokalnych.
- Wdrożonych systemów SAP w maszynach wirtualnych platformy Azure. Te systemy można programowanie i testowanie piaskownicy, lub produkcji wystąpień dla każdego hello aplikacji SAP NetWeaver można pomyślnie wdrożyć na platformie Azure (na maszynach wirtualnych), na podstawie zapotrzebowania zasobów konsumenckich i pamięci. Te systemy również mogą być oparte na baz danych, takich jak SQL Server (zobacz [&#1928533; SAP Obsługa Uwaga — aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure](https://launchpad.support.sap.com/#/notes/1928533/E)) lub SAP HANA (zobacz [SAP HANA certyfikowane IaaS platformy](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- Wdrożenia serwerów aplikacji SAP na platformie Azure (na maszynach wirtualnych), korzystających z SAP HANA na platformie Azure (wystąpienia duże) w sygnatury dużych wystąpienia platformy Azure.

Hybrydowego SAP w orientacji poziomej (co najmniej cztery różne scenariusze wdrażania) jest typowa, istnieje wiele przypadków klienta pełną pozioma SAP działające na platformie Azure. Jak maszyny wirtualne Microsoft Azure stają się coraz bardziej zaawansowanych, zwiększa się hello liczbę klientów, przeniesienie ich rozwiązania SAP na platformie Azure.

Azure networking w kontekście hello systemów SAP wdrożona na platformie Azure nie jest skomplikowane. Jest on oparty na powitania następujące zasady:

- Sieci wirtualnych platformy Azure (sieci wirtualne) muszą obwodu Azure ExpressRoute toohello toobe połączone, łączącego tooon lokalnej sieci.
- Obwód usługi expressroute, zwykle połączenie tooAzure lokalnymi powinien mieć przepustowości 1 GB/s lub wyższy. Ta minimalnej przepustowości umożliwia odpowiedniej przepustowości do przesyłania danych między lokalnymi i systemami uruchomionych na maszynach wirtualnych platformy Azure (a także systemów tooAzure połączenia z lokalnym użytkownicy końcowi).
- Wszystkie systemy SAP w toobe Azure należy skonfigurować w sieci wirtualnych Azure toocommunicate ze sobą.
- Usługi Active Directory i DNS obsługiwanego lokalnie zostały rozszerzone na platformie Azure za pośrednictwem usługi ExpressRoute z lokalnymi.


> [!NOTE] 
> Z rozliczeń punktu widzenia tylko jedna subskrypcja platformy Azure może odnosić się tylko tooone dzierżawy pojedynczego w dużych wystąpienia sygnatury w określonym regionie Azure, a z drugiej strony pojedynczej dzierżawy sygnatury dużych wystąpienia może odnosić się tylko tooone subskrypcji platformy Azure. Ten fakt jest tooany nie różnych innych obiektów rozliczeniowy na platformie Azure

Wdrażanie SAP HANA na platformie Azure (duże wystąpień) w wielu różnych regionach platformy Azure, powoduje toobe oddzielne dzierżawy wdrożenie hello sygnatura dużych wystąpienia. Jednak można uruchamiać jednocześnie w obszarze hello poziomą tego samego SAP tak długo, jak te wystąpienia są częścią hello tej samej subskrypcji platformy Azure. 

> [!IMPORTANT] 
> Tylko wdrożenie zarządzania zasobami Azure jest obsługiwana z SAP HANA na platformie Azure (wystąpienia duże).

 

### <a name="additional-azure-vnet-information"></a>Dodatkowe informacje o sieci wirtualnej Azure

W kolejności tooconnect tooExpressRoute sieci wirtualnej Azure, należy utworzyć bramę Azure (zobacz [temat bram sieci wirtualnej dla usługi ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Brama usługi Azure może służyć za pomocą infrastruktury tooan ExpressRoute poza Azure (lub sygnatura wystąpienia Azure dużych tooan) lub tooconnect między sieciami wirtualnymi platformy Azure (zobacz [skonfigurować połączenia do wirtualnymi dla Menedżera zasobów przy użyciu programu PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Możesz połączyć hello Azure bramy tooa maksymalnie cztery różne połączenia ExpressRoute, tak długo, jak te połączenia pochodzą z różnych routerów krawędzi przedsiębiorstwa MS (MSEE).  Aby uzyskać więcej informacji, zobacz [SAP HANA (duże wystąpień) infrastruktury i łączności na platformie Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Witaj przepływności brama Azure zapewnia jest inna oba przypadki użycia (zobacz [o bramy sieci VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Maksymalna przepustowość Hello, które możemy się z bramą sieci wirtualnej jest 10 GB/s, przy użyciu połączenia ExpressRoute. Należy pamiętać, że kopiowania plików między maszyny Wirtualnej platformy Azure, znajdującej się w sieci wirtualnej platformy Azure oraz systemu lokalnego (jako strumień o pojedynczej kopii) nie będzie hello pełnej przepływności hello bramy innej jednostki SKU. tooleverage hello pełną przepustowości hello bramy sieci wirtualnej, muszą używać wielu strumieni lub różnych plików kopii w strumieniach równoległych pojedynczego pliku.


### <a name="networking-architecture-for-hana-large-instances"></a>Architektura sieci dla wystąpień dużych HANA
Hello sieci dla wystąpień dużych HANA architektura jak pokazano poniżej, można podzielić na cztery różne części:

- Sieci lokalnej i tooAzure połączenia ExpressRoute. Ta część jest domeny klientom Witaj i tooAzure połączonych za pośrednictwem usługi ExpressRoute. Jest to część hello w prawym dolnym hello grafiki hello poniżej.
- Jak krótko opisanych wyżej z sieciami wirtualnymi platformy Azure, która ponownie ma bram sieci platformy Azure. Jest to obszar, w których należy toofind hello odpowiednie projekty do wymagań aplikacji, zabezpieczeń i zgodności z przepisami. Za pomocą wystąpień dużych HANA jest inny punkt brany pod uwagę pod względem liczby sieci wirtualnych i Azure toochoose jednostki SKU bramy z. Jest to część hello w prawym górnym rogu hello hello grafiki.
- Łączność wystąpień dużych HANA za pomocą technologii ExpressRoute na platformie Azure. Ta część jest wdrożony i obsługiwane przez firmę Microsoft. Wszystko, czego potrzebujesz toodo klienta tooprovide niektórych zakresów adresów IP i po wdrożeniu hello elementów zawartości z połączeniem HANA dużych wystąpień hello ExpressRoute obwodu toohello Azure VNet(s) (zobacz [infrastruktury SAP HANA (duże wystąpień) i połączenie na platformie Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Sieć w dużych wystąpień HANA, który jest przeważnie przezroczysty dla Ciebie jako klient.

![Sieć wirtualna Azure połączone tooSAP HANA Azure (wystąpienia duże) i lokalnej](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

fakt Hello używanie dużych HANA wystąpień nie zmienia tooget wymaganie hello zasobów lokalnych połączone za pośrednictwem ExpressRoute tooAzure. Ponadto nie zmienia wymaganie hello występowania jednego lub wielu sieci wirtualnych uruchomionymi hello maszynach wirtualnych platformy Azure, które warstwy aplikacji hello hosta łączy toohello HANA wystąpień hostowanych w HANA dużych wystąpienia jednostki. 

Hello różnica tooSAP wdrożeń w czystym Azure, jest dostarczany z faktów hello który:

- jednostki wystąpienia dużych HANA Hello dzierżawy klienta są połączone za pośrednictwem innego obwodu usługi expressroute w VNet(s) Twojego Azure. W warunkach obciążenia tooseparate kolejności, tooAzure lokalnymi hello łącza ExpressRoute sieci wirtualnych i połączeń między sieciami wirtualnymi platformy Azure i wystąpień HANA dużych nie współużytkują hello sam routery.
- Hello profilu obciążenia między warstwy aplikacji hello SAP i hello HANA wystąpienia jest inny rodzaj wiele żądań małe i serii, takich jak dane przesyła (zestawy wyników) z SAP HANA do warstwy aplikacji hello.
- Hello SAP architektura jest bardziej podatna opóźnienia toonetwork niż typowy scenariusz, w którym dane pobiera wymieniane między lokalną i platformą Azure.
- Brama sieci wirtualnej Hello ma co najmniej dwa połączenia ExpressRoute, a oba połączenia udziału hello maksymalną przepustowość dla danych przychodzących hello bramy sieci wirtualnej.

Opóźnienie sieci Hello doświadczonym między maszynami wirtualnymi Azure i HANA dużych jednostek wystąpienie może być większa niż typowe opóźnienia obustronne sieci maszyn wirtualnych do maszyny Wirtualnej. Zależne od hello region platformy Azure, mierzone wartości hello może przekroczyć hello 0,7 ms obustronne opóźnienia sklasyfikowane jako poniżej średniej w [SAP Uwaga #1100926 — często zadawane pytania: wydajność sieci](https://launchpad.support.sap.com/#/notes/1100926/E). Niemniej jednak klienci wdrożone aplikacje SAP na podstawie SAP HANA produkcji bardzo pomyślnie na wystąpień dużych SAP HANA. Hello klientów, którzy wdrożone zgłosił dużą ulepszenia uruchamiając swoje aplikacje SAP na SAP HANA przy użyciu HANA dużych wystąpienia jednostki. Niemniej jednak należy przetestować procesy biznesowe dokładnie w dużych wystąpień HANA Azure.
 
W kolejności tooprovide deterministyczne opóźnienie między maszynami wirtualnymi Azure i wystąpienia dużych HANA ważne jest wybór hello hello jednostka SKU bramy sieci wirtualnej platformy Azure. W odróżnieniu od hello wzorce ruchu między lokalnymi i maszyn wirtualnych platformy Azure hello wzorzec ruchu między maszynami wirtualnymi Azure i wystąpień dużych HANA można programować małych jednak dużych seria żądań i przesyłane toobe woluminów danych. W kolejności toohave takie seria obsłużony, zdecydowanie zaleca się użycie hello hello UltraPerformance jednostka SKU bramy. Dla hello jednostki SKU HANA dużych wystąpienia klasy typu II użycia hello bramy UltraPerformance hello SKU jako brama sieci wirtualnej platformy Azure jest wymagane.  

> [!IMPORTANT] 
> Podany hello ogólną ruchu sieciowego między hello SAP aplikacji i warstwy bazy danych tylko hello wysokowydajnej lub bramy UltraPerformance jednostki SKU dla sieci wirtualnych jest obsługiwana w przypadku łączenia tooSAP HANA na platformie Azure (wystąpienia duże). Dla dużych HANA wystąpienia jednostki SKU II typu hello UltraPerformance jednostka SKU bramy jest obsługiwany jako brama sieci wirtualnej platformy Azure.



### <a name="single-sap-system"></a>Pojedynczego systemu SAP

pokazanym powyżej infrastruktury lokalnej Hello jest połączony za pośrednictwem usługi na platformie Azure i hello obwodu ExpressRoute łączy do firmy Microsoft Enterprise krawędzi routera (MSEE) (zobacz [opis techniczny ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Po ustanowione, tej trasy łączy do hello Microsoft Azure w sieci szkieletowej, a wszystkie regiony platformy Azure są dostępne.

> [!NOTE] 
> Łączyć MSEE toohello — toohello najbliższy region platformy Azure w orientacji poziomej SAP hello krajobrazów SAP działające na platformie Azure. Sygnatury dużych wystąpienia platformy Azure są połączone za pośrednictwem dedykowanych MSEE urządzeń toominimize opóźnienie sieci między maszynami wirtualnymi Azure w Azure IaaS oraz wystąpienia dużych sygnatury.

Hello bramy sieci wirtualnej dla hello maszynach wirtualnych platformy Azure, hosting wystąpień aplikacji SAP, jest połączone toothat obwodu ExpressRoute i hello tej samej sieci wirtualnej jest połączonych tooa oddzielne Router MSEE dedykowanego tooconnecting tooLarge wystąpienia sygnatury.

To jest przykład prostego pojedynczego systemu SAP, gdzie hello SAP warstwy aplikacji jest hostowana na platformie Azure i bazy danych SAP HANA hello odbywa się na SAP HANA na platformie Azure (wystąpienia duże). Witaj zakłada się, że przepustowość bramy sieci wirtualnej hello 2 GB/s lub 10 GB/s przepustowości nie stanowi wąskiego gardła.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Wiele systemów SAP lub dużych systemów SAP

W przypadku wielu systemów SAP lub dużych systemach SAP wdrożenia łączenie tooSAP HANA na Azure (wystąpienia duże) &#39; s tooassume uzasadnione hello przepływności hello bramy sieci wirtualnej mogą stać się wąskiego gardła. W takim przypadku należy warstwy aplikacji hello toosplit do wielu sieci wirtualnych platformy Azure. Przyczyną może być również recommendable toocreate specjalne sieci wirtualnych podłączoną tooHANA dużych wystąpień dla przypadkach, takich jak:

- Wykonywanie kopii zapasowych bezpośrednio z hello HANA wystąpień w tooa HANA dużych wystąpień maszyny Wirtualnej na platformie Azure obsługującego udziałów NFS
- Kopiowanie dużych kopii zapasowych lub innych plików z HANA dużych jednostek toodisk miejsce zajmowane przez wystąpienia zarządzanych na platformie Azure.

Używa oddzielnych sieci wirtualnych, że wpływ dużych plików pozwala uniknąć hosta maszyn wirtualnych, które zarządzania magazynem hello lub transfer danych z dużych wystąpień HANA tooAzure na powitania bramy sieci wirtualnej, który służy hello czy uruchomiono maszyny wirtualne warstwy aplikacji hello SAP. 

Aby uzyskać większą skalowalność architektury sieci:

- Korzystaj z wielu sieci wirtualnych platformy Azure pojedynczego, większy warstwy aplikacji SAP.
- Wdrażanie jednego oddzielne sieć wirtualną Azure systemu każdego SAP wdrożeniu toocombining w porównaniu tych systemów SAP w różnych podsieciach w obszarze hello tej samej sieci wirtualnej.

 Skalowalność architektury sieci SAP HANA na platformie Azure (wystąpienia duże):

![Wdrażanie programu SAP warstwy aplikacji przez wiele sieci wirtualnych platformy Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Wdrażanie warstwy aplikacji hello SAP lub składniki, przez wiele sieci wirtualnych platformy Azure zgodnie z powyższym, wprowadzono koszty nieuniknione opóźnienia, który wystąpił podczas komunikacji między aplikacji hello znajdującej się w tych sieci wirtualnych platformy Azure. Domyślnie program hello ruch sieciowy między maszynami wirtualnymi Azure znajduje się w różnych trasy sieci wirtualnych za pośrednictwem hello MSEE routery w tej konfiguracji. Jednak od września 2016 marszruty mogą być optymalizowane. Witaj toooptimize sposób i zmniejszyć opóźnienia hello w ramach komunikacji między dwiema sieciami wirtualnymi polega na komunikacji równorzędnej sieci wirtualnych platformy Azure w ramach hello tego samego regionu. Nawet jeśli te sieci wirtualne są w różnych subskrypcji. Za pomocą usługi Azure wirtualne sieci równorzędne —, hello komunikacji między maszynami wirtualnymi w dwóch różnych sieci wirtualnych platformy Azure można Użyj hello sieć platformy Azure szkieletu toodirectly komunikują się ze sobą. Dzięki temu przedstawiający podobne opóźnienie tak, jakby hello maszyny wirtualne będą w hello tej samej sieci wirtualnej. Natomiast ruch adresowania zakresów adresów IP, które są połączone za pośrednictwem bramy sieci wirtualnej Azure hello, jest kierowany przez hello oddzielną bramę sieci wirtualnej z hello sieci wirtualnej. Komunikacja równorzędna w artykule hello można uzyskać szczegółowe informacje o sieci wirtualnej Azure [sieci wirtualnej komunikacji równorzędnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Routing na platformie Azure

Istnieją dwie ważne routingu zagadnienia dotyczące sieci dla SAP HANA na platformie Azure (wystąpienia duże):

1. SAP HANA na platformie Azure (wystąpienia duże) można uzyskać tylko w maszynach wirtualnych platformy Azure w hello dedykowanego połączenia ExpressRoute; nie bezpośrednio z lokalnego. Niektórzy klienci administracji i wszystkich aplikacji wymagających bezpośredniego dostępu, takie jak Menedżer rozwiązania SAP uruchomione w siedzibie firmy, nie można połączyć z bazy danych SAP HANA toohello.

2. SAP HANA Azure (duże wystąpień) w jednostkach mieć przypisanego adresu IP z adresów puli adresów IP serwera hello zakresu można jako powitania klienta przesłane (zobacz [SAP HANA (duże wystąpień) infrastruktury i łączności na platformie Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje).  Ten adres IP jest dostępna za pośrednictwem hello Azure subskrypcji i ExpressRoute łączącego tooHANA sieci wirtualnych platformy Azure na platformie Azure (wystąpienia duże). Witaj adresu IP przypisanego poza tego zakresu adresów puli adresów IP serwera przypisanej bezpośrednio jednostki sprzętu toohello i nie jest NAT'ed już to hello przypadku hello pierwszego wdrożenia tego rozwiązania. 

> [!NOTE] 
> Jeśli należy tooSAP tooconnect HANA na platformie Azure (duże wystąpień) w _hurtowni danych_ scenariusz, w której aplikacje i/lub użytkownicy końcowi muszą tooconnect: toohello bazy danych SAP HANA (uruchomiony bezpośrednio), musi być inny składnik sieci używane: dane tooroute wstecznego serwera proxy, tooand z. Na przykład F5 BIG-IP, NGINX Menedżera ruchu wdrożona na platformie Azure jako rozwiązanie routingu wirtualne zapory/ruchu.

### <a name="internet-connectivity-of-hana-large-instances"></a>Połączenie z Internetem HANA dużych wystąpień
Wystąpienia dużych HANA nie mieć bezpośrednie połączenie z Internetem. Jest to ograniczenie z możliwości, na przykład zarejestrować hello obrazu systemu operacyjnego bezpośrednio z hello dostawcy systemu operacyjnego. Dlatego może być konieczne toowork z lokalnego serwera SLES SMT lub RHEL subskrypcji Menedżera

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Szyfrowanie danych między maszynami wirtualnymi Azure i wystąpień dużych HANA
Danych przesyłanych między wystąpieniami dużych HANA i maszyn wirtualnych platformy Azure nie jest zaszyfrowany. Jednak wyłącznie w celu wymiany hello między powitania po stronie HANA DBMS i aplikacji na podstawie JDBC/ODBC można włączyć szyfrowanie ruchu. Odwołanie [tej dokumentacji przez SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Przy użyciu HANA dużych wystąpienia jednostek w wielu regionach

Konieczne może być inne przyczyny toodeploy SAP HANA na platformie Azure (duże wystąpień) w wielu regionach platformy Azure, oprócz odzyskiwania po awarii. Możesz określić ma tooaccess HANA dużych wystąpień każdej hello maszyn wirtualnych wdrożonych w hello różnych sieci wirtualnych w regionach hello. Ponieważ hello adresy IP przypisane toohello różne jednostki HANA dużych wystąpień nie są propagowane poza hello sieci wirtualnych platformy Azure (które są połączone bezpośrednio za pomocą ich wystąpienia toohello bramy), jest niewielkie zmiany toohello projekt sieci wirtualnej z wprowadzonych powyżej: Bramy sieci wirtualnej platformy Azure może obsłużyć czterech różnych obwody usługi ExpressRoute z różnych MSEEs i każdego sieć wirtualną, która jest połączonych tooone hello sygnatur dużych wystąpienia może być sygnatura wystąpienia dużych toohello połączonych w innym regionie Azure.

![Sygnatury dużych wystąpienia tooAzure połączone sieci wirtualnych Azure w różnych regionach platformy Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Hello powyżej rysunek przedstawia sposób hello różnych sieci wirtualnych platformy Azure w obu regiony są tootwo połączonych różnych ExpressRoute obwodów, które są używane tooconnect tooSAP HANA na platformie Azure (duże wystąpień) w obu regionach platformy Azure. Witaj nowo wdrożonych połączenia są hello prostokątne czerwonych linii. Te połączenia poza hello sieci wirtualnych platformy Azure, hello maszyn wirtualnych uruchomionych w jednej z tych sieci wirtualnych umożliwia dostęp do poszczególnych jednostek hello różnych wystąpień dużych HANA wdrożone w dwóch regionach hello. Jak widać w grafiki hello powyżej, zakłada się, ma dwa połączenia ExpressRoute z lokalnymi toohello dwóch regionach platformy Azure; zalecana ze względów odzyskiwania po awarii.

> [!IMPORTANT] 
> Użycie wielu obwody usługi ExpressRoute dołączanie ścieżki AS i ustawienia lokalnego BGP preferencji powinny być używane tooensure właściwego routingu ruchu.


