---
title: aaaRun Cassandra z systemem Linux na platformie Azure | Dokumentacja firmy Microsoft
description: Jak toorun Cassandra klastra w systemie Linux w maszynach wirtualnych platformy Azure z poziomu aplikacji Node.js
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Uruchamianie rozwiązania Cassandra w systemie Linux na platformie Azure i uzyskiwanie do niej dostępu na platformie Node.js
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Zobacz szablony Menedżera zasobów dla [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) i [Spark klastra i Cassandra na CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Omówienie
Microsoft Azure to platforma chmury Otwórz uruchamianego zarówno do firmy Microsoft jako oprogramowania również w innych niż Microsoft, w tym systemów operacyjnych, serwerów aplikacji, oprogramowanie pośredniczące obsługi wiadomości, a także baz danych SQL i NoSQL z obu modeli handlowych i otwórz źródła. Tworzenie usług odporne na chmur publicznych, w tym na platformie Azure wymaga staranne planowanie i architektura zamierzonego dla obu serwerów aplikacji jako warstwy dobrze magazynu. Naturalnie Cassandra w magazynie rozproszonym architektura ułatwia tworzenie wysokiej dostępności systemów, które są odporne na uszkodzenia w przypadku awarii klastra. Cassandra jest skali chmury bazy danych NoSQL utrzymywana przez Foundation oprogramowania Apache cassandra.apache.org; Cassandra jest napisany w języku Java i dlatego działa zarówno na system Windows, jak i Linux platformy.

Witaj w tym artykule koncentruje się tooshow Cassandra wdrożenia na Ubuntu jako klaster pojedynczych i wielu danych Centrum wykorzystaniu maszyny wirtualne Microsoft Azure i sieci wirtualnych. Hello wdrożenia klastra w przypadku obciążeń produkcyjnych zoptymalizowanych pod kątem wykracza poza zakres tego artykułu ponieważ wymaga konfiguracji węzła wielu dysków, potrzebne projektowania topologia pierścienia odpowiednie i modelowania toosupport hello danych replikacji, spójność danych, przepływności i wymagania dotyczące wysokiej dostępności.

Ten ma artykułu tooshow podstawowych podejście, na czym polega w budynku hello Cassandra klastra porównaniu Docker, Chef lub Puppet, co może uniemożliwić hello wdrożenia infrastruktury dużo prostsze.  

## <a name="hello-deployment-models"></a>Witaj modele wdrażania
Sieci Microsoft Azure umożliwia wdrożenie hello izolowanego prywatnej klastrów, hello dostępu, które może być ograniczone tooattain zabezpieczenia poprawnie sieci szczegółowych.  Ponieważ ten artykuł dotyczy przedstawiający hello Cassandra wdrożenia na poziomie podstawowym, firma Microsoft nie koncentruje się na powitania poziomu spójności i hello projekt magazynu optymalnej przepustowości. Poniżej znajduje się lista hello wymagania sieciowe związane z naszych hipotetyczny klastra:

* Systemy zewnętrzne nie może uzyskać dostępu Cassandra bazy danych z lub poza Azure
* Cassandra klaster ma toobe za modułem równoważenia obciążenia dla ruchu thrift
* Wdrażanie węzłów Cassandra na dwie grupy w każdej centrum danych dostępności klastra rozszerzone
* Zablokowanie klastra hello tak że tylko bezpośrednio toohello dostępu do bazy danych ma farmy serwerów aplikacji
* Brak publicznego punktów końcowych sieci innych niż SSH
* Każdy węzeł Cassandra musi stałym wewnętrznego adresu IP

Cassandra może być wdrożony tooa pojedynczy region platformy Azure lub regiony toomultiple oparte na powitania rozproszonych rodzaj obciążenia hello. W przypadku wdrażania modelu może być wykorzystywana tooserve użytkownicy końcowi bliżej tooa określonego obiektu geograficznego za pośrednictwem hello Cassandra w tej samej infrastrukturze. Cassandra dla wbudowanego węzła replikacji ma opieki synchronizacji hello wielu wzorca zapisuje pochodzących z wielu centrów danych i przedstawia widok spójne hello tooapplications danych. W przypadku wdrożenia może również pomóc z hello umożliwiają ograniczenie ryzyka związanego z hello szerszych awarie usługi Azure. Topologii replikacji i spójności dostosowywalne w Cassandra pomoże spełnia zróżnicowane potrzeby RPO aplikacji.

### <a name="single-region-deployment"></a>Wdrażanie jednego regionu
Firma Microsoft rozpoczyna się od wdrożenia jednego regionu i zbiorów hello learnings modelu w przypadku tworzenia. Sieci wirtualne platformy Azure będzie podsieci używane toocreate izolowane spełnienia wymagań zabezpieczeń sieci hello wymienionych powyżej.  proces Hello opisano w temacie Tworzenie wdrożenia jednego regionu hello używa Ubuntu 14.04 LTS i Cassandra 2.08; Jednak proces hello można łatwo można przyjąć toohello innych wersji systemu Linux. Witaj poniżej przedstawiono niektóre właściwości systemowych hello hello pojedynczy region wdrożenia.  

**Wysoka dostępność:** hello węzłów Cassandra pokazano hello rysunek 1 są wdrażane dostępności tootwo ustawia tak, aby węzły hello są rozkładane między wiele domen błędów w celu zapewnienia wysokiej dostępności. Maszyny wirtualne adnotowany przy każdym zestawie dostępności jest mapowane too2 domen błędów.  Microsoft Azure używa hello koncepcji toomanage domeny błędów nieplanowane przestoje (np. awarii sprzętu lub oprogramowania) podczas hello koncepcji uaktualniania domeny (np. hosta lub gościa systemu operacyjnego stosowanie poprawek/uaktualnień, uaktualnień aplikacji) służy do zarządzania zaplanowany czas przestoju. Zobacz [odzyskiwania po awarii i wysoką dostępność aplikacji Azure](http://msdn.microsoft.com/library/dn251004.aspx) dla roli hello awarii i uaktualniania domen w celu osiągnięcia wysokiej dostępności.

![Wdrażanie jednego regionu](./media/cassandra-nodejs/cassandra-linux1.png)

Rysunek 1: Wdrożenie pojedynczy region

Zauważ, że w czasie hello pisania tego dokumentu, Azure nie zezwalają hello jawne mapowanie grupy domeny określonych błędów tooa maszyn wirtualnych. w związku z tym nawet w przypadku modelu wdrażania hello pokazany na rysunku 1, jest statystycznie prawdopodobne, że wszystkie maszyny wirtualne hello mogą być mapowane tootwo domen błędów zamiast cztery.

**Ruch Thrift równoważenia obciążenia:** bibliotek klienckich Thrift wewnątrz powitania serwera sieci web Połącz toohello klastra za pośrednictwem wewnętrznego modułu równoważenia obciążenia. Wymaga to proces dodawania podsieci toohello usługi równoważenia obciążenia wewnętrznego hello "dane" hello (zobacz rysunek 1) w kontekście hello hello hosting hello Cassandra klastra usługi w chmurze. Po zdefiniowaniu hello wewnętrznego modułu równoważenia obciążenia każdy węzeł wymaga toobe punkt końcowy ze zrównoważonym obciążeniem hello dodane w adnotacji hello zestawu o zrównoważonym obciążeniu wcześniej nazwę modułu równoważenia obciążenia zdefiniowane. Zobacz [wewnętrzny równoważenia obciążenia Azure ](../../../load-balancer/load-balancer-internal-overview.md)więcej szczegółów.

**Ziarna klastra:** koniecznie tooselect hello większości węzłów wysokiej dostępności dla ziarna jako hello nowe węzły będą komunikować się z inicjatora węzłów toodiscover hello topologii hello klastra. Jeden węzeł z każdym zestawie dostępności jest wyznaczony jako inicjatora węzłów tooavoid pojedynczy punkt awarii.

**Współczynnik replikacji i poziomu spójności:** Cassandra w kompilacji w wysokiej dostępności i danych trwałości charakteryzuje się hello współczynnik replikacji (RF - liczby kopii każdego wiersza przechowywane na powitania klastra) i poziomu spójności (liczba repliki toobe odczytana/zapisana przed zwróceniem hello wynik toohello wywołującego). Współczynnik replikacji jest określana podczas hello tworzenie przestrzeni KLUCZY (podobne tooa relacyjnej bazy danych), określić poziom spójności hello podczas wystawiania hello CRUD zapytania. W dokumentacji Cassandra [Konfigurowanie spójności](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegóły spójności i wzór hello na obliczenia kworum.

Cassandra obsługuje dwa typy modeli integralności danych — spójność i spójność ostateczna; Hello współczynnik replikacji i poziomu spójności ze sobą określi, jeśli hello dane są spójne natychmiast po zakończeniu operacji zapisu lub będą zgodne po pewnym czasie. Na przykład określenie KWORUM jako powitalne poziomu spójności będzie zawsze gwarantuje spójności danych dowolnego poziomu spójności poniżej hello liczby replik toobe zapisywane jako wymagane tooattain powoduje danych po pewnym czasie zgodnych KWORUM (np. jeden).

powyższy współczynnik replikacji 3 i KWORUM klastra 8 węzłów Hello (2 węzły są odczytywane lub zapisywane spójności) poziomu spójności odczytu/zapisu, przełączniki hello teoretycznego utraty na powitania większości 1 węzła dla replikacji grupy przed uruchomieniem aplikacji hello Błąd powitania po raz pierwszy. Przy założeniu, że wszystkie spacje klucza hello również mieć zrównoważonym żądań odczytu/zapisu.  Oto Hello hello parametrów, które będą używane dla klastra hello wdrożone:

Konfiguracja klastra Cassandra jednego regionu:

| Parametr klastra | Wartość | Uwagi |
| --- | --- | --- |
| Liczba węzłów (N) |8 |Całkowita liczba węzłów w klastrze hello |
| Współczynnik replikacji (RF) |3 |Liczba replik danego wiersza |
| Poziom zgodności (Zapisz) |QUORUM[(RF/2) +1) = 2] hello wyników z hello jest zaokrąglana formułę |Zapisuje na powitania większości 2 replik przed wysłaniem odpowiedzi hello toohello wywołującego 3 repliki są zapisywane w sposób spójny po pewnym czasie. |
| Poziom zgodności (odczyt) |KWORUM [(RF/2) + 1 = 2] jest zaokrąglana hello wynik formuły hello |Odczytuje 2 replik przed wysłaniem odpowiedzi toohello wywołującego. |
| Strategii replikacji |Zobacz NetworkTopologyStrategy [replikacji danych](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) w Cassandra dokumentacji, aby uzyskać więcej informacji |Rozumie hello topologii wdrożenia i umieszcza replik w węzłach, tak, aby wszystkie repliki hello nie trafiają do hello sam stojak |
| Snitch |Zobacz GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) w Cassandra dokumentacji, aby uzyskać więcej informacji |NetworkTopologyStrategy korzysta z koncepcji snitch toounderstand hello topologii. GossipingPropertyFileSnitch zapewnia lepszą kontrolę w mapowaniu każdego węzła toodata Centrum i stojaku. Witaj klastra używa następnie toopropagate plotki tych informacji. To jest znacznie prostsza w dynamicznej tooPropertyFileSnitch względną ustawienie adresu IP |

**Azure zagadnienia dotyczące klastra Cassandra:** możliwości maszyny wirtualne Microsoft Azure korzysta z magazynu obiektów Blob platformy Azure dysku trwałości; Usługa Azure Storage zapisuje 3 replik każdego dysku, aby uzyskać wysoką trwałością. Oznacza to, każdy wiersz danych wstawione do tabeli Cassandra jest już zapisana w 3 repliki i dlatego spójność danych jest już wykonane obsługę nawet jeśli hello współczynnik replikacji (RF) jest 1. Witaj główny problem z współczynnik replikacji jest 1 jest aplikacji hello wystąpi przestój nawet w przypadku awarii jednego węzła Cassandra. Jednak jeśli węzeł nie działa dla problemów hello (np. sprzętu, błędów oprogramowania systemu) rozpoznawany przez kontroler sieci szkieletowej Azure, jego obsługa będzie inicjowana nowy węzeł w jego miejscu przy użyciu hello tego samego dysków. Inicjowanie obsługi administracyjnej nowych węzła tooreplace hello starego jedną może potrwać kilka minut.  Podobnie czynności zaplanowanej konserwacji, jak zmiany system operacyjny gościa, uaktualnia Cassandra, a wprowadzanie uaktualnień hello węzłów w klastrze hello wykonuje Kontroler sieci szkieletowej Azure zmian w aplikacji.  Również uaktualnień stopniowych może potrwać kilka węzłów w dół w czasie i dlatego hello klastra może wystąpić krótki przestój w przypadku kilku partycji. Jednak hello dane nie zostaną utracone powodu toohello wbudowane funkcje nadmiarowości usługi Azure Storage.  

Dla systemów wdrożone tooAzure, która nie wymaga wysokiej dostępności (np. około 99,9 czyli równoważne too8.76 godzin na rok; zobacz [wysokiej dostępności](http://en.wikipedia.org/wiki/High_availability) szczegółowe informacje) może być możliwe toorun z RF = 1 i poziom spójności równej ONE.  W przypadku aplikacji o wysokiej dostępności wymagania, RF = 3 i poziomu spójności = KWORUM będą tolerować hello czasu jednego z węzłów hello jeden hello replik. RF = 1 w przypadku tradycyjnych wdrożeń (np. lokalnego) nie można użyć powodu toohello możliwa utrata danych wynikające z problemów, takich jak awarii dysku.   

## <a name="multi-region-deployment"></a>W przypadku wdrożenia
Dla dowolnego narzędzia zewnętrznego, należy replikacji danych Centrum rozpoznają i modelu spójności opisane powyżej pomaga przy użyciu hello w przypadku wdrażania fabrycznej hello bez hello Cassandra firmy. Jest to całkowicie różnią się od tradycyjnych relacyjnych baz danych hello, gdzie hello instalację na potrzeby dublowania bazy danych dla wielu wzorców operacji zapisu może być dość złożone. Cassandra w regionie wielu konfigurowanie może pomóc w tym hello następujące scenariusze użycia hello:

**Wdrożenia na podstawie bliskości:** aplikacje wielodostępne, wyczyść mapowania użytkowników dzierżawy-do-region, można korzystali przez małe opóźnienia hello w przypadku klastra. Na przykład zarządzanie learning systemów dla instytucji edukacyjnych można wdrożyć klaster rozproszonych w wschodnie stany USA i zachodnie stany USA regionów tooserve hello odpowiednich szkoły wyższe dla transakcyjnego, a także analizy. dane Hello można lokalnie spójne o hello czasu odczyty i zapisy i może być ostatecznie spójne w obu regionach hello. Istnieją inne przykłady takich jak dystrybucji nośnika, handlu elektronicznego i niczego i wszystko, co służy geograficznie skoncentrowanego użytkownika podstawowego jest przypadek użycia dobrej dla tego modelu wdrażania.

**Wysoka dostępność:** nadmiarowość jest kluczowym czynnikiem w celu osiągnięcia wysokiej dostępności sprzętu i oprogramowania; więcej szczegółów, zobacz Tworzenie niezawodnej systemy chmur w systemie Microsoft Azure. W systemie Microsoft Azure hello tylko niezawodny sposób realizacji nadmiarowość wartość true, jest wdrażanie klastra w przypadku. Aplikacje można wdrożyć w trybie aktywny aktywny lub aktywny / pasywny i jeśli regionów hello jest wyłączony, usługi Azure Traffic Manager można przekierować ruch toohello aktywnego regionu.  Z wdrożeniem pojedynczego obszaru hello, jeśli hello dostępności 99,9, region dwa wdrożenia może osiągnąć dostępności 99.9999 obliczone przez formułę hello: (1-(1-0.999) * (1-0.999)) * 100); Zobacz hello powyżej papieru, aby uzyskać szczegółowe informacje.

**Odzyskiwanie po awarii:** Cassandra w przypadku klastra, jeśli przeznaczony prawidłowo, może wytrzymać przestojami centrum danych w wyniku katastrofy. Jeśli działa jeden region, regiony tooother wdrożonych aplikacji hello można uruchomić obsługująca hello użytkowników końcowych. Jak żadnych innych firm ciągłości implementacji aplikacja hello ma toobe na uszkodzenia na utratę danych, na podstawie hello danych w potoku asynchroniczne hello. Jednak Cassandra sprawia, że odzyskiwania hello znacznie usprawnić niż czas hello procesów odzyskiwania tradycyjne bazy danych. Rysunek 2 przedstawia hello typowe wdrożenie w przypadku modelu w ośmiu węzłów w każdym regionie. Zarówno regiony są dublowane obrazy wzajemnie dla hello tego samego elementu symetrycznego; projekty rzeczywistych są zależne od hello typ obciążenia (np. transakcyjnej lub analitycznych), RPO, RTO, spójności danych i wymagań dotyczących dostępności.

![Obsługa wielu region wdrożenia](./media/cassandra-nodejs/cassandra-linux2.png)

Rysunek 2: W przypadku Cassandra wdrożenia

### <a name="network-integration"></a>Integracja sieci
Ustawia maszyn wirtualnych wdrożonych tooprivate sieci znajdujących się na dwóch regionach komunikuje się ze sobą przy użyciu tunelu VPN. tunel VPN Hello łączy dwie bramy oprogramowanie udostępniane w trakcie procesu wdrażania sieci hello. Zarówno regiony mają podobną architekturę sieci pod względem podsieci "web" i "dane"; Sieć platformy Azure umożliwia tworzenie hello tyle podsieci zgodnie z potrzebami i stosować listy ACL, odpowiednio do potrzeb zabezpieczeń sieci. Podczas projektowania topologii klastra hello między danych Centrum komunikacji opóźnienia i hello ekonomicznego wpływu hello sieci ruchu potrzeby toobe traktowane jako.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Spójność danych wdrożenia Centrum usługi danych
Rozproszone toobe potrzeba wdrożenia świadome hello klastra topologii wpływu na przepustowość i wysokiej dostępności. Hello RF i poziomu spójności toobe potrzeby wybrane w taki sposób, który hello kworum nie zależy od dostępności hello wszystkich centrów danych hello.
Dla systemu, który wymaga wysokiej spójności, LOCAL_QUORUM dla spójności poziom (odczyty i zapisy) będzie upewnij się, że hello lokalnego odczytuje i zapisuje są spełnione z lokalne powitania węzły, podczas gdy dane są replikowane asynchronicznie toohello centrów danych zdalnych.  Tabela 2 zawiera podsumowanie konfiguracji hello szczegóły hello w przypadku klastra opisane w dalszej części hello zwiększenia.

**Konfiguracja klastra Cassandra dwa regionu**

| Parametr klastra | Wartość | Uwagi |
| --- | --- | --- |
| Liczba węzłów (N) |8 + 8 |Całkowita liczba węzłów w klastrze hello |
| Współczynnik replikacji (RF) |3 |Liczba replik danego wiersza |
| Poziom zgodności (Zapisz) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] hello wynik formuły hello jest zaokrąglana |węzły 2 zostanie zapisany w centrum danych z pierwszego toohello synchronicznie; Hello dodatkowych węzłów 2 wymaganych dla kworum zostanie zapisany asynchronicznie toohello 2 centrum danych. |
| Poziom zgodności (odczyt) |LOCAL_QUORUM ((RF/2) + 1) = 2 hello wynik formuły hello jest zaokrąglana |Żądań odczytu są spełnione przy tylko jeden region; 2 węzły są odczytywane przed wysłaniem odpowiedzi powitania klienta toohello Wstecz. |
| Strategii replikacji |Zobacz NetworkTopologyStrategy [replikacji danych](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) w Cassandra dokumentacji, aby uzyskać więcej informacji |Rozumie hello topologii wdrożenia i umieszcza replik w węzłach, tak, aby wszystkie repliki hello nie trafiają do hello sam stojak |
| Snitch |Zobacz GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) w Cassandra dokumentacji, aby uzyskać więcej informacji |NetworkTopologyStrategy korzysta z koncepcji snitch toounderstand hello topologii. GossipingPropertyFileSnitch zapewnia lepszą kontrolę w mapowaniu każdego węzła toodata Centrum i stojaku. Witaj klastra używa następnie toopropagate plotki tych informacji. To jest znacznie prostsza w dynamicznej tooPropertyFileSnitch względną ustawienie adresu IP |

## <a name="hello-software-configuration"></a>Witaj konfiguracji oprogramowania
następujące wersje oprogramowania Hello są używane podczas wdrażania hello:

<table>
<tr><th>Oprogramowanie</th><th>Element źródłowy</th><th>Wersja</th></tr>
<tr><td>ŚRODOWISKA JRE    </td><td>[ŚRODOWISKA JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Ponieważ pobieranie środowiska JRE wymaga ręcznego akceptacji licencji Oracle, toosimplify hello wdrożenia, pobierania wszystkich hello później przekazywanie do obrazu szablonu Ubuntu hello, firma Microsoft będzie tworzony jako klaster toohello macierzystych pulpitu toohello wymaganego oprogramowania wdrożenia.

Pobierz hello powyżej oprogramowania w katalogu pobierania dobrze znanego (np. %TEMP%/downloads w systemie Windows lub ~/Downloads na większości dystrybucje systemu Linux lub Mac.) na komputerze lokalnym hello.

### <a name="create-ubuntu-vm"></a>TWORZENIE MASZYNY WIRTUALNEJ SYSTEMU UBUNTU
W tym kroku procesu hello utworzymy Ubuntu obrazu z hello wstępnie wymagane oprogramowanie, aby hello obrazu mogą być ponownie używane do inicjowania obsługi kilka węzłów Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>Krok 1: Generuje parę kluczy SSH
Platforma Azure wymaga X509 klucza publicznego, który jest PEM lub DER zakodowane w hello inicjowania obsługi administracyjnej czasu. Generowanie pary kluczy publiczny/prywatny przy użyciu instrukcji hello znajdujący się w sposób tooUse SSH z systemem Linux na platformie Azure. Jeśli planujesz toouse putty.exe jako klient SSH w systemie Windows lub Linux, masz tooconvert hello PEM kodowany w formacie tooPPK klucza prywatnego RSA przy użyciu puttygen.exe; Witaj odpowiednie instrukcje znajdują się w hello powyżej strony sieci web.

#### <a name="step-2-create-ubuntu-template-vm"></a>Krok 2: Tworzenie Ubuntu szablonu maszyny Wirtualnej
toocreate hello szablonu maszyny Wirtualnej, zaloguj się do hello Azure classic hello portalu i użycie następującej sekwencji: kliknij przycisk Nowy, obliczeń, maszyny WIRTUALNEJ, z GALERII, UBUNTU, Ubuntu Server 14.04 LTS, a następnie kliknij strzałkę w prawo hello. Samouczek opisujący toocreate Maszynę wirtualną systemu Linux, zobacz temat Tworzenie maszyny wirtualnej systemem Linux.

Wprowadź następujące informacje na ekranie powitania "konfiguracja maszyny wirtualnej" #1 hello:

<table>
<tr><th>NAZWA POLA              </td><td>       WARTOŚĆ POLA               </td><td>         UWAGI                </td><tr>
<tr><td>DATA WYDANIA WERSJI    </td><td> Wybierz datę z hello listy rozwijanej</td><td></td><tr>
<tr><td>NAZWA MASZYNY WIRTUALNEJ    </td><td> Szablon przypadku                   </td><td> Jest to nazwa hosta hello hello maszyny Wirtualnej </td><tr>
<tr><td>WARSTWY                     </td><td> STANDARDOWA                           </td><td> Pozostaw domyślną hello              </td><tr>
<tr><td>ROZMIAR                     </td><td> A1                              </td><td>Wybierz hello, maszyna wirtualna jest oparta na powitania we/wy potrzeb. w tym celu należy pozostawić domyślne hello </td><tr>
<tr><td> NOWĄ NAZWĘ UŻYTKOWNIKA             </td><td> localadmin                       </td><td> "Administrator" jest zastrzeżoną nazwą użytkownika w xx 12 Ubuntu i po</td><tr>
<tr><td> UWIERZYTELNIANIE         </td><td> Kliknij pole wyboru                 </td><td>Sprawdź, czy ma toosecure przy użyciu klucza SSH </td><tr>
<tr><td> CERTYFIKAT             </td><td> Nazwa pliku certyfikatu klucza publicznego hello </td><td> Użyj klucza publicznego hello wcześniej wygenerowany</td><tr>
<tr><td> Nowe hasło    </td><td> Silne hasło </td><td> </td><tr>
<tr><td> Potwierdź hasło    </td><td> Silne hasło </td><td></td><tr>
</table>

Wprowadź następujące informacje na ekranie powitania "konfiguracja maszyny wirtualnej" #2 hello:

<table>
<tr><th>NAZWA POLA             </th><th> WARTOŚĆ POLA                       </th><th> UWAGI                                 </th></tr>
<tr><td> USŁUGI W CHMURZE    </td><td> Utwórz nową usługę w chmurze    </td><td>Usługa w chmurze jest zasoby obliczeniowe kontenera, takich jak maszyny wirtualne</td></tr>
<tr><td> NAZWA DNS USŁUGI W CHMURZE    </td><td>ubuntu template.cloudapp.net    </td><td>Nadaj nazwę modułu równoważenia obciążenia o niesprecyzowanym maszyny</td></tr>
<tr><td> REGION/GRUPY KOLIGACJI/SIECI WIRTUALNEJ </td><td>    Zachodnie stany USA    </td><td> Wybierz region, z którego dostęp do aplikacji sieci web hello Cassandra klastra</td></tr>
<tr><td>KONTO MAGAZYNU </td><td>    Użyj domyślnej    </td><td>Użyj domyślnego konta magazynu hello lub wstępnie utworzone konto magazynu w określonym regionie</td></tr>
<tr><td>ZESTAW DOSTĘPNOŚCI </td><td>    Brak </td><td>    Pozostaw to pole puste</td></tr>
<tr><td>PUNKTY KOŃCOWE    </td><td>Użyj domyślnej </td><td>    Użyj hello domyślnej konfiguracji SSH </td></tr>
</table>

Kliknij strzałkę w prawo, pozostaw wartości domyślne hello na ekranie powitania #3, a następnie kliknij przycisk hello "wyboru" przycisk toocomplete hello wirtualna procesu inicjowania obsługi administracyjnej. Po kilku minutach hello maszyny Wirtualnej z hello nazwy "ubuntu-template" powinna być w stanie "uruchomiona".

### <a name="install-hello-necessary-software"></a>Zainstaluj hello niezbędne oprogramowanie
#### <a name="step-1-upload-tarballs"></a>Krok 1: Przekazywanie tarballs
Przy użyciu protokołu scp lub pscp, hello kopiowania pobrane wcześniej oprogramowanie zbyt ~ / directory pliki do pobrania przy użyciu hello zgodny z formatem polecenia:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-środowiska jre-8u5-linux-x64.tar.gzlocaladmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Powtórz hello powyżej polecenia dla środowiska JRE również podobnie jak w przypadku hello Cassandra bitów.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>Krok 2: Przygotowanie hello strukturę katalogów i wyodrębniać hello archiwa
Zaloguj się do hello maszyny Wirtualnej i Utwórz strukturę katalogów hello i Wyodrębnij oprogramowania jako superużytkownika przy użyciu skryptu bash hello poniżej:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Po wklejeniu tego skryptu do okna vim upewnij się, że tooremove hello karetki zwracany ("\r") przy użyciu hello następujące polecenie:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Krok 3: Edytowanie profilu itp.
Dołącz następujące hello na końcu hello:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Krok 4: Instalacja JNA dla systemów produkcyjnych.
Użyj hello następujące polecenie sekwencji: hello następujące polecenie, zainstaluj jna-3.2.7.jar i too/usr/share.java jna-platform — 3.2.7.jar katalogu sudo stanie get zainstaluje libjna java

Utwórz łącza symbolicznego w katalogu CASS_HOME/lib $ tak, aby Cassandra uruchamiania skryptu można znaleźć te słoików:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Krok 5: Konfigurowanie cassandra.yaml
Edytuj cassandra.yaml na każdej maszyny Wirtualnej konfiguracji tooreflect wymagane przez wszystkie maszyny wirtualne hello [firma Microsoft będzie dostosować to podczas inicjowania obsługi rzeczywistych hello]:

<table>
<tr><th>Nazwa pola   </th><th> Wartość  </th><th>    Uwagi </th></tr>
<tr><td>nazwa_klastra </td><td>    "CustomerService"    </td><td> Użyj nazwy hello, które odzwierciedla wdrożenia</td></tr>
<tr><td>listen_address    </td><td>[pozostaw to pole puste]    </td><td> Usuń "localhost" </td></tr>
<tr><td>rpc_addres   </td><td>[pozostaw to pole puste]    </td><td> Usuń "localhost" </td></tr>
<tr><td>ziarna    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Lista wszystkich adresów IP hello, które są oznaczone jako dane.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> To jest używany przez hello NetworkTopologyStrateg wnioskowanie hello centrum danych i hello stojak hello maszyny Wirtualnej</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Krok 6: Przechwytywanie obrazu maszyny Wirtualnej hello
Zaloguj się do maszyny wirtualnej hello przy użyciu nazwy hosta hello (hk-urzędów certyfikacji template.cloudapp.net) i klucz prywatny SSH hello wcześniej utworzony. Zobacz temat jak tooUse SSH z systemem Linux na platformie Azure, aby uzyskać szczegółowe informacje w sposób toolog za pomocą hello polecenia ssh lub putty.exe.

Wykonaj powitania po sekwencji obraz powitania toocapture akcje:

##### <a name="1-deprovision"></a>1. Deprovision
Użyj polecenia hello "sudo agenta waagent — deprovision + użytkownika" tooremove określone informacje o wystąpieniu maszyny wirtualnej. Zobacz dla [jak tooCapture maszyny wirtualnej systemu Linux](capture-image.md) szczegółowe na proces przechwytywania obrazu hello tooUse jako szablon.

##### <a name="2-shutdown-hello-vm"></a>2: hello zamykania maszyny Wirtualnej
Upewnij się, że zostanie wyróżniona hello maszyny wirtualnej, a następnie kliknij łącze zamknięcia hello z hello dolnym pasku poleceń.

##### <a name="3-capture-hello-image"></a>3: obraz powitania przechwytywania
Upewnij się, że zostanie wyróżniona hello maszyny wirtualnej, a następnie kliknij łącze PRZECHWYTYWANIA hello z hello dolnym pasku poleceń. W następnym ekranie powitania nadaj nazwę obrazu (np. hk-cas-2-08-ub-14-04-2014071), odpowiednich opis obrazu, a następnie kliknij przycisk proces PRZECHWYTYWANIA hello toofinish znaku "wyboru" hello.

To może zająć kilka sekund i obraz powitania powinny być dostępne w sekcji Moje obrazy hello Galeria obrazów. pomyślnie przechwycony obraz powitania Hello źródłowej maszyny Wirtualnej zostaną automatycznie usunięte. 

## <a name="single-region-deployment-process"></a>Proces wdrażania pojedynczy Region
**Krok 1: Tworzenie sieci wirtualnej hello** Zaloguj się do hello portalu Azure i utworzyć sieć wirtualną (klasyczne) z atrybutami hello pokazano hello w poniższej tabeli. Zobacz [Utwórz sieć wirtualną (klasyczne) przy użyciu portalu Azure hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) szczegółowy opis kroków procesu hello.      

<table>
<tr><th>Nazwa atrybutu maszyny Wirtualnej</th><th>Wartość</th><th>Uwagi</th></tr>
<tr><td>Nazwa</td><td>sieć wirtualna — przypadku zachód nam</td><td></td></tr>
<tr><td>Region</td><td>Zachodnie stany USA</td><td></td></tr>
<tr><td>Serwery DNS</td><td>Brak</td><td>Zignoruj ten komunikat, ponieważ nie używamy serwera DNS</td></tr>
<tr><td>Przestrzeń adresów</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>Uruchamianie adresu IP</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Dodaj następujące podsieci hello:

<table>
<tr><th>Nazwa</th><th>Uruchamianie adresu IP</th><th>CIDR</th><th>Uwagi</th></tr>
<tr><td>sieci Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Podsieć hello kolektywu serwerów sieci web</td></tr>
<tr><td>Dane</td><td>10.1.2.0</td><td>/24 (251)</td><td>Podsieć hello węzłów bazy danych</td></tr>
</table>

Dane i podsieci w sieci Web mogą być chronione przy użyciu grup zabezpieczeń sieci, pokrycie hello wykracza poza zakres tego artykułu.  

**Krok 2: Maszyny wirtualne należy** przy użyciu obrazu hello utworzone wcześniej, utworzymy hello następujące maszyny wirtualne w chmurze powitania serwera "hk-c-svc Zachód" ją i powiązać je toohello odpowiednich podsieci, jak pokazano poniżej:

<table>
<tr><th>Nazwa komputera    </th><th>Podsieć    </th><th>Adres IP    </th><th>Zestaw dostępności</th><th>DC/Rack</th><th>Inicjatora?</th></tr>
<tr><td>HK-c1-zachód us    </td><td>Dane    </td><td>10.1.2.4    </td><td>HK-c-aset-1    </td><td>DC = stojak WESTUS = szafa1 </td><td>Tak</td></tr>
<tr><td>HK-c2-zachód us    </td><td>Dane    </td><td>10.1.2.5    </td><td>HK-c-aset-1    </td><td>DC = stojak WESTUS = szafa1    </td><td>Nie </td></tr>
<tr><td>HK-c3-zachód us    </td><td>Dane    </td><td>10.1.2.6    </td><td>HK-c-aset-1    </td><td>DC = stojak WESTUS = szafa2    </td><td>Tak</td></tr>
<tr><td>HK-c4-zachód us    </td><td>Dane    </td><td>10.1.2.7    </td><td>HK-c-aset-1    </td><td>DC = stojak WESTUS = szafa2    </td><td>Nie </td></tr>
<tr><td>HK-c5-zachód us    </td><td>Dane    </td><td>10.1.2.8    </td><td>HK-c-aset-2    </td><td>DC = stojak WESTUS = szafa3    </td><td>Tak</td></tr>
<tr><td>HK-c6-zachód us    </td><td>Dane    </td><td>10.1.2.9    </td><td>HK-c-aset-2    </td><td>DC = stojak WESTUS = szafa3    </td><td>Nie </td></tr>
<tr><td>HK-c7-zachód us    </td><td>Dane    </td><td>10.1.2.10    </td><td>HK-c-aset-2    </td><td>DC = stojak WESTUS = rack4    </td><td>Tak</td></tr>
<tr><td>HK-c8-zachód us    </td><td>Dane    </td><td>10.1.2.11    </td><td>HK-c-aset-2    </td><td>DC = stojak WESTUS = rack4    </td><td>Nie </td></tr>
<tr><td>HK-w1 — zachód us    </td><td>sieci Web    </td><td>10.1.1.4    </td><td>HK p-aset-1    </td><td>                       </td><td>Nie dotyczy</td></tr>
<tr><td>HK-w2 — zachód us    </td><td>sieci Web    </td><td>10.1.1.5    </td><td>HK p-aset-1    </td><td>                       </td><td>Nie dotyczy</td></tr>
</table>

Tworzenie hello powyżej listy maszyn wirtualnych wymaga hello następującego procesu:

1. Tworzenie usługi w chmurze pusta w określonym regionie
2. Utwórz maszynę Wirtualną z wcześniej przechwycony obraz powitania i dołącz je toohello sieci wirtualnej utworzonej wcześniej; Powtórz tę czynność dla wszystkich hello maszyn wirtualnych.
3. Dodawanie usługi w chmurze toohello usługi równoważenia obciążenia wewnętrznego i dołącz je podsieci toohello "dane"
4. Dla każdej maszyny Wirtualnej utworzone wcześniej Dodaj punkt końcowy równoważenia obciążenia dla ruchu thrift za pośrednictwem ze zrównoważonym obciążeniem połączony zestaw toohello wcześniej utworzony wewnętrznego modułu równoważenia obciążenia

Witaj powyżej procesu mogą być wykonywane przy użyciu klasycznego portalu Azure; Użyj komputera z systemem Windows (Użyj maszyny Wirtualnej na platformie Azure, jeśli nie masz komputera z systemem Windows tooa dostępu), użyj wszystkich maszyn wirtualnych 8 powitania po tooprovision skrypt programu PowerShell automatycznie.

**Lista 1: Skrypt programu PowerShell do obsługi maszyn wirtualnych**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Krok 3: Konfigurowanie Cassandra na każdej maszynie Wirtualnej**

Zaloguj się do hello maszyny Wirtualnej i wykonaj następujące hello:

* Edytuj $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello Centrum i stojak właściwości danych:
  
       dc =EASTUS, rack =rack1
* Edytuj węzły inicjatora tooconfigure cassandra.yaml, jak pokazano poniżej:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Krok 4: Uruchom hello maszyn wirtualnych i przetestować hello klastra**

Zaloguj się do jednego z węzłów hello, (np. hk-c1-zachód us) i hello uruchom następujące polecenie toosee hello stan klastra hello:

       nodetool –h 10.1.2.4 –p 7199 status

Powinny pojawić się hello wyświetlania podobne toohello jeden poniżej 8 węzłów klastra:

<table>
<tr><th>Stan</th><th>Adres    </th><th>Ładowanie    </th><th>Tokeny    </th><th>Właścicielem </th><th>Identyfikator hosta    </th><th>Stojak</th></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa1</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa1</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa2</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa2</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa3</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>szafa3</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>rack4</td></tr>
<tr><th>WYREJESTRUJ    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Identyfikator GUID (usunięte)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Test hello pojedynczy klaster regionu
Użyj hello następujące kroki tootest hello klastra:

1. Za pomocą polecenia programu Powershell hello apletu polecenia Get-AzureInternalLoadbalancer, uzyskać adres IP hello hello wewnętrznego modułu równoważenia obciążenia (np.  10.1.2.101). Poniżej przedstawiono Hello Składnia polecenia hello: Get-AzureLoadbalancer — ServiceName "hk — c-svc zachód us" [Wyświetla szczegóły hello hello wewnętrznego modułu równoważenia obciążenia oraz adres IP]
2. Zaloguj się do kolektywu serwerów sieci web hello maszyny Wirtualnej (np. hk-w1 — zachód us) przy użyciu programu Putty lub ssh
3. Wykonanie $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Użyj powitania po tooverify polecenia CQL działa hello klastra:
   
     TWORZENIE przestrzeni KLUCZY customers_ks z REPLIKACJĄ = {"class": "SimpleStrategy", "replication_factor": 3};   UŻYJ customers_ks;   Tworzenie tabeli Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Wstaw do Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Wstaw do Customers(customer_id, firstname, lastname) wartości 2, 'Magdalena', 'Nowak';
   
     Wybierz * od klientów.

Powinny pojawić się wyświetlanej takie jak hello jedną poniżej:

<table>
  <tr><th> customer_id </th><th> Imię </th><th> nazwisko </th></tr>
  <tr><td> 1 </td><td> Jan </td><td> Nowak </td></tr>
  <tr><td> 2 </td><td> Magdalena </td><td> Nowak </td></tr>
</table>

Należy pamiętać, że używa tego hello przestrzeni kluczy, utworzony w kroku 4 SimpleStrategy replication_factor 3. SimpleStrategy jest zalecane dla pojedynczego wdrożenia Centrum natomiast NetworkTopologyStrategy danych z wielu centrów. Replication_factor 3 zapewni tolerancji na wypadek awarii węzła.

## <a id="tworegion"></a>Proces w przypadku wdrażania
Zostanie korzystaj z wdrożenia jednego regionu hello ukończone i powtórz hello tego samego procesu instalowania hello drugi regionu. Różnica klucza Hello hello jednego i wielu wdrożenia region jest Instalator tunelu VPN hello do komunikacji między regionu; Firma Microsoft będzie rozpoczynać się od instalacji sieciowej hello, udostępnić hello maszyn wirtualnych i skonfiguruj Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Krok 1: Tworzenie sieci wirtualnej hello na powitania Region 2
Zaloguj się do hello klasycznego portalu Azure i utworzyć sieć wirtualną z programem atrybuty hello hello tabeli. Zobacz [skonfigurować sieć wirtualną Cloud-Only w hello klasycznego portalu Azure](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) szczegółowy opis kroków procesu hello.      

<table>
<tr><th>Nazwa atrybutu    </th><th>Wartość    </th><th>Uwagi</th></tr>
<tr><td>Nazwa    </td><td>sieci wirtualnej przypadku wschód us</td><td></td></tr>
<tr><td>Region    </td><td>Wschodnie stany USA</td><td></td></tr>
<tr><td>Serwery DNS        </td><td></td><td>Zignoruj ten komunikat, ponieważ nie używamy serwera DNS</td></tr>
<tr><td>Konfigurowanie sieci VPN punkt lokacja</td><td></td><td>        Zignoruj ten komunikat</td></tr>
<tr><td>Konfiguracja tunelu sieci VPN łączącego lokacje</td><td></td><td>        Zignoruj ten komunikat</td></tr>
<tr><td>Przestrzeń adresów    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>Uruchamianie adresu IP    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Dodaj następujące podsieci hello:

<table>
<tr><th>Nazwa    </th><th>Uruchamianie adresu IP    </th><th>CIDR    </th><th>Uwagi</th></tr>
<tr><td>sieci Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Podsieć hello kolektywu serwerów sieci web</td></tr>
<tr><td>Dane    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Podsieć hello węzłów bazy danych</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Krok 2: Tworzenie sieci lokalne
Sieci lokalnej w sieci wirtualnej platformy Azure jest przestrzeń adresów serwera proxy, która mapuje tooa witryny zdalnej w tym chmurę prywatną lub inny region platformy Azure. Ta przestrzeń adresowa serwera proxy jest powiązane tooa bramy zdalnego dla routingu toohello sieci prawo sieci miejsc docelowych. Zobacz [Konfigurowanie sieci wirtualnej tooVNet połączenia](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) hello instrukcje dotyczące nawiązywania połączenia do Wirtualnymi.

Utwórz dwie sieci lokalne na powitania poniższe informacje:

| Nazwa sieci | Adres bramy sieci VPN | Przestrzeń adresów | Uwagi |
| --- | --- | --- | --- |
| HK-lnet-map-to-East-US |23.1.1.1 |10.2.0.0/16 |Podczas tworzenia hello sieci lokalnej nadaj symbol zastępczy adres bramy. Adres bramy rzeczywistych Hello jest wypełniony, po utworzeniu bramy hello. Upewnij się, że przestrzeń adresowa hello dokładnie zgodny hello odpowiednich zdalna sieć wirtualna; w takim przypadku hello sieci Wirtualnej utworzone w hello regionu wschodnie stany USA. |
| HK-lnet-map-to-West-US |23.2.2.2 |10.1.0.0/16 |Podczas tworzenia hello sieci lokalnej nadaj symbol zastępczy adres bramy. Adres bramy rzeczywistych Hello jest wypełniony, po utworzeniu bramy hello. Upewnij się, że przestrzeń adresowa hello dokładnie zgodny hello odpowiednich zdalna sieć wirtualna; w takim przypadku hello sieci Wirtualnej utworzone w hello regionu zachodnie stany USA. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Krok 3: Mapy sieci "Lokalnie" toohello odpowiednich sieci wirtualnych
Z hello klasycznego portalu Azure wybierz każdej sieci wirtualnej, kliknij przycisk "Konfiguruj" Sprawdź "Connect toohello sieci lokalnej" i wybierz sieci lokalne powitania na powitania poniższe informacje:

| Virtual Network | Sieci lokalnej |
| --- | --- |
| HK — sieci wirtualnej zachód us |HK-lnet-map-to-East-US |
| HK — sieci wirtualnej wschód us |HK-lnet-map-to-West-US |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Krok 4: Tworzenie bramy na VNET1 i VNET2
Z pulpitu nawigacyjnego hello sieci wirtualnych obu hello kliknij przycisk Utwórz bramy, które wyzwoli bramy sieci VPN hello w procesie inicjowania obsługi. Adres bramy rzeczywiste hello powinien być wyświetlany po kilku minut hello pulpitu nawigacyjnego w każdej sieci wirtualnej.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Krok 5: Aktualizacja "Lokalnie" sieci z adresami odpowiednich "bramy" hello
Edytować zarówno hello sieci lokalne tooreplace hello symbolu zastępczego brama IP adresu hello rzeczywistego adresu IP hello tylko elastycznie bramy. Użyj następującego mapowania hello:

<table>
<tr><th>Sieci lokalnej    </th><th>Brama sieci wirtualnej</th></tr>
<tr><td>HK-lnet-map-to-East-US </td><td>Brama hk — sieci wirtualnej zachód us</td></tr>
<tr><td>HK-lnet-map-to-West-US </td><td>Brama hk — sieci wirtualnej wschód us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Krok 6: Klucz udostępniony hello aktualizacji
Użyj powitania po klucz tooupdate skrypt programu Powershell IPSec hello każdej bramy sieci VPN [Użyj hello sake klucza dla obu bram hello]: Set AzureVNetGatewayKey - VNetName hk — sieci wirtualnej wschód us - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Zestaw AzureVNetGatewayKey - VNetName hk — sieci wirtualnej zachód us - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Krok 7: Nawiązania połączenia hello do Wirtualnymi
Hello klasycznego portalu Azure użyj menu "Pulpitu NAWIGACYJNEGO" hello zarówno hello sieci wirtualnych tooestablish brama brama połączenia. Użyj elementów menu "POŁĄCZ" hello w hello dolnym pasku narzędzi. Po kilku minutach pulpitu nawigacyjnego hello powinien być wyświetlany szczegóły połączenia hello graficznie.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Krok 8: Tworzenie maszyn wirtualnych hello w regionie #2
Utwórz obraz Ubuntu hello zgodnie z opisem w regionie #1 wdrożenia przez następujące hello same kroki lub skopiuj hello obrazu wirtualnego dysku twardego pliku toohello Azure konta magazynu znajdującego się w regionie #2 a hello obrazu. Skorzystaj z tego obrazu, a następnie utwórz powitania po listę maszyn wirtualnych do nowej usługi w chmurze, hk-c-svc wschód nam:

| Nazwa komputera | Podsieć | Adres IP | Zestaw dostępności | DC/Rack | Inicjatora? |
| --- | --- | --- | --- | --- | --- |
| HK-c1-wschód us |Dane |10.2.2.4 |HK-c-aset-1 |DC = stojak EASTUS = szafa1 |Tak |
| HK-c2-wschód us |Dane |10.2.2.5 |HK-c-aset-1 |DC = stojak EASTUS = szafa1 |Nie |
| HK-c3-wschód us |Dane |10.2.2.6 |HK-c-aset-1 |DC = stojak EASTUS = szafa2 |Tak |
| HK-c5-wschód us |Dane |10.2.2.8 |HK-c-aset-2 |DC = stojak EASTUS = szafa3 |Tak |
| HK-c6-wschód us |Dane |10.2.2.9 |HK-c-aset-2 |DC = stojak EASTUS = szafa3 |Nie |
| HK-c7-wschód us |Dane |10.2.2.10 |HK-c-aset-2 |DC = stojak EASTUS = rack4 |Tak |
| HK-c8-wschód us |Dane |10.2.2.11 |HK-c-aset-2 |DC = stojak EASTUS = rack4 |Nie |
| HK-w1 — wschód us |sieci Web |10.2.1.4 |HK p-aset-1 |Nie dotyczy |Nie dotyczy |
| HK-w2 — wschód us |sieci Web |10.2.1.5 |HK p-aset-1 |Nie dotyczy |Nie dotyczy |

Wykonaj hello same instrukcje jako region #1, ale użyj przestrzeni adresowej 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Krok 9: Konfigurowanie Cassandra na każdej maszynie Wirtualnej
Zaloguj się do hello maszyny Wirtualnej i wykonaj następujące hello:

1. Edytuj $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello Centrum i stojak właściwości danych w formacie hello: dc = stojak EASTUS = szafa1
2. Edytuj węzły inicjatora tooconfigure cassandra.yaml: ziarna: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>Krok 10: Uruchom Cassandra
Zaloguj się do każdej maszyny Wirtualnej i uruchomić Cassandra w tle hello, uruchamiając następujące polecenie hello: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Witaj testu w przypadku klastra
Już Cassandra zostało wdrożone too16 węzłów z 8 węzłów w każdym regionie Azure. Te węzły znajdują się w hello sam klastra ze względu na powitania wspólnej nazwy klastra i konfiguracja węzła hello inicjatora. Użyj następującego procesu tootest hello klastra hello:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Krok 1: Uzyskiwanie adresu IP usługi równoważenia obciążenia wewnętrznego powitania dla obu regionów hello przy użyciu programu PowerShell
* Get-AzureInternalLoadbalancer - ServiceName "hk — c-svc zachód us"
* Get-AzureInternalLoadbalancer - ServiceName "hk — c-svc wschód us"  
  
    Należy zwrócić uwagę hello adresów IP (np. - 10.1.2.101, wschód - zachód 10.2.2.101) wyświetlane.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Krok 2: Wykonaj następujące hello w regionu zachodnie powitania po zalogowaniu w hk-w1 — zachód us
1. Wykonanie $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Wykonaj następujące polecenia CQL hello:
   
     TWORZENIE przestrzeni KLUCZY customers_ks z REPLIKACJĄ = {"class": "NetworkToplogyStrategy", "WESTUS": 3, EASTUS: 3};   UŻYJ customers_ks;   Tworzenie tabeli Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Wstaw do Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Wstaw do Customers(customer_id, firstname, lastname) wartości 2, 'Magdalena', 'Nowak';   Wybierz * od klientów.

Powinny pojawić się wyświetlanej takie jak hello jedną poniżej:

| customer_id | Imię | nazwisko |
| --- | --- | --- |
| 1 |Jan |Nowak |
| 2 |Magdalena |Nowak |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Krok 3: Wykonanie następujących hello w regionie wschodnie hello po zalogowaniu w hk-w1 — wschód us:
1. Wykonanie $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Wykonaj następujące polecenia CQL hello:
   
     UŻYJ customers_ks;   Tworzenie tabeli Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Wstaw do Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Wstaw do Customers(customer_id, firstname, lastname) wartości 2, 'Magdalena', 'Nowak';   Wybierz * od klientów.

Powinny pojawić się sam wyświetlić widziany dla regionu zachodnie hello hello:

| customer_id | Imię | nazwisko |
| --- | --- | --- |
| 1 |Jan |Nowak |
| 2 |Magdalena |Nowak |

Wykonaj kilka więcej operacji wstawienia i zobacz, czy pobrać tych zreplikowanych toowest-us, które są częścią klastra hello.

## <a name="test-cassandra-cluster-from-nodejs"></a>Testowanie Cassandra klastra w oprogramowaniu Node.js
Przy użyciu jednej z maszyn wirtualnych systemu Linux hello utworzone wcześniej w warstwie "web" hello, firma Microsoft będzie wykonywać proste danych hello wcześniej wstawiony tooread skryptu środowiska Node.js

**Krok 1: Instalacja klienta Cassandra i Node.js**

1. Instalowanie środowiska Node.js i npm
2. Instalowanie pakietu "cassandra klienta w węźle" za pomocą programu npm
3. Wykonanie następującego skryptu w wierszu polecenia powłoki hello wyświetlającego hello json ciąg hello pobrać danych hello:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Podsumowanie
Microsoft Azure to elastyczna platforma, która umożliwia uruchamianie hello zarówno firmy Microsoft, jak i oprogramowanie typu open source, jak zostało to pokazane w tym ćwiczeniu. Klastry Cassandra wysokiej dostępności można wdrożyć na jednego centrum danych przez rozłożenie hello węzłów klastra hello wielu domen błędów. Klastry Cassandra można także wdrożyć w różnych regionach platformy Azure odległymi geograficznie systemów potwierdzającego po awarii. Azure i umożliwia razem Cassandra hello konstrukcja wysoce skalowalną, wysokiej dostępności i usługi w chmurze możliwych do odzyskania po awarii wymagane przez internet współczesnych skalowania usług.  

## <a name="references"></a>Dokumentacja
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

