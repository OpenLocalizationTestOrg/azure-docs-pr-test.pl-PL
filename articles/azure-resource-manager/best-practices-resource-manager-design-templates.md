---
title: "aaaDesign Azure szablony złożonych rozwiązań | Dokumentacja firmy Microsoft"
description: "Przedstawiono najlepsze rozwiązania dotyczące projektowania szablonów usługi Azure Resource Manager w złożonych scenariuszach"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>Wzorce projektowe dla szablonów usługi Azure Resource Manager w przypadku wdrażania złożonych rozwiązań
Przy użyciu elastyczne podejście oparte na szablonach usługi Azure Resource Manager, można wdrożyć złożonej topologii szybkie i spójne. Można dostosować te wdrożenia łatwo jako podstawowych ofert rozwijać lub wariantów tooaccommodate dla scenariuszy izolowanej lub klientów.

Ten temat jest częścią większej oficjalny dokument. Pobierz hello tooread pełnej papier [światowej klasy Azure zasobów Menedżer szablonów zagadnienia i sprawdzonych rozwiązań](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

Szablony łączyć hello zalet hello podstawowej usługi Azure Resource Manager z zdolności adaptacyjnych hello i czytelność kodu JavaScript Object Notation (JSON). Za pomocą szablonów, można:

* Spójne wdrażanie topologii i ich obciążeń.
* Zarządzanie wszystkich zasobów w aplikacji ze sobą przy użyciu grup zasobów.
* Zastosuj toousers odpowiedni dostęp toogrant kontroli dostępu opartej na rolach, grup i usług.
* Użyj znakowania skojarzenia toostreamline zadań, takich jak rozliczenia pakietów zbiorczych.

Ten artykuł zawiera szczegółowe informacje na scenariusze użycia, architektura i wzorce implementacji zidentyfikowanego w trakcie naszych sesji projektowania i implementacji rzeczywistych szablonu z klientami Azure zespół doradczy klientów (AzureCAT). Daleko od uczelni, tych sposobów są sprawdzonych rozwiązań poinformowany przez hello tworzenia szablonów dla 12 hello top opartych na systemie Linux OSS technologii, takich jak: Apache Kafka, Apache Spark, Cloudera, Couchbase Hortonworks HDP, Enterprise DataStax obsługiwane przez Apache Cassandra, Elasticsearch Wpięć, bazy danych MongoDB, PostgreSQL, Redis i Nagios. 

W tym artykule współużytkuje te toohelp sprawdzonych rozwiązań projektowania szablonów usługi Azure Resource Manager klas world.  

W naszym Praca z klientami określiliśmy kilka środowisko konsumowania szablon Menedżera zasobów przedsiębiorstwa, s integratory systemu (SI) i udostępnionych woluminów klastra. Witaj poniższe sekcje zawierają ogólne omówienie typowych scenariuszy i wzorce dla różnych typów klientów.

## <a name="enterprises-and-system-integrators"></a>Przedsiębiorstwach i integratorów systemów. platforma
W dużych organizacjach widzimy często konsumentów dwóch szablonów usługi Resource Manager: zespoły rozwoju oprogramowania wewnętrzny i firmowych IT. Wykryto, że scenariusze hello hello SIs mapy toohello scenariuszy dla przedsiębiorstw, tak hello te same kwestie.

### <a name="internal-software-development-teams"></a>Zespoły rozwoju oprogramowania wewnętrznego
Jeśli zespół osiąga toosupport oprogramowania firmy, szablony umożliwiają łatwe tooquickly wdrażać technologie do zastosowania w rozwiązaniach specyficzne dla firm. Można również użyć szablonów toorapidly utworzyć środowiska szkolenia, umożliwiających umiejętności niezbędne toogain członków zespołu.

Za pomocą szablonów jako — jest lub rozszerzyć lub tworzą je tooaccommodate potrzeb. Za pomocą znakowania w szablonach, można udostępnić rozliczeń Podsumowanie różnych widokach, takich jak zespołu, projekt, osoby i education.

Firm chce często, że rozwoju oprogramowania zespoły toocreate szablonu spójne wdrożenia rozwiązania. Szablon Hello ułatwia ograniczenia niektórych elementów w tym środowisku pozostają z ustaloną i nie może zostać zastąpiona. Na przykład bank mogą wymagać tooinclude szablonu RBAC programisty nie można poprawić rozwiązania banku toosend danych tooa magazynu osobistego konta.

### <a name="corporate-it"></a>Firmowej IT
Działy IT firmy zwykle korzystają z szablonów do dostarczania chmury możliwości pojemności i hostowanych w chmurze.

#### <a name="cloud-capacity"></a>Pojemność w chmurze
Jest to często stosowana metoda firmowej IT grup tooprovide chmury pojemności dla zespołów "rozmiary obrazów na koszulki", które są standardowe oferty rozmiary, takich jak małych, średnich i dużych. Hello obrazów na koszulki o rozmiarze oferty można łączyć różnych typów zasobów i ilości, zapewniając poziom normalizacji, dzięki którym możliwe toouse szablony. Szablony Hello dostarczanie pojemności w spójny sposób, który wymusza zasady firmowe i używa znakowanie organizacji tooconsuming obciążenia zwrotnego tooprovide.

Na przykład może wymagać rozwoju tooprovide, testów lub środowisk produkcyjnych, w których hello zespoły rozwoju oprogramowania można wdrożyć ich rozwiązania. środowisko Hello ma topologii sieci wstępnie zdefiniowane i elementy, które hello zespoły rozwoju oprogramowania nie można zmienić, takich jak zasady dostępu toohello publiczny internet i pakietów inspekcji. Ponadto klientowi mogą przysługiwać role w danej organizacji dla tych środowisk z prawami dostępu unikatowych hello środowiska.

#### <a name="cloud-hosted-capabilities"></a>Możliwości hostowanych w chmurze
Można użyć szablonów toosupport hostowanych w chmurze możliwości, takie jak pakiety oprogramowania lub złożone oferty, które są oferowane toointernal rodzajach działalności gospodarczej. Przykładem złożone oferty może być analytics jako usługa — analytics, wizualizacji i innych technologii — dostarczone w konfiguracji zoptymalizowane, połączonych w topologii sieci wstępnie zdefiniowane.

Możliwości hostowanych w chmurze są zagrożone hello zabezpieczeń i zagadnienia dotyczące roli ustala pojemności chmury hello oferty, w którym są wbudowane. Te możliwości są oferowane zmian lub jako zarządzanych usług. Dla hello później, wymagane są role ograniczonego dostępu tooenable dostępu do środowiska hello do celów zarządzania.

## <a name="cloud-service-vendors"></a>Dostawców usługi w chmurze
Po rozmowie toomany woluminów CSV, określiliśmy, że wiele metod może zająć toodeploy usług dla klientów i skojarzone wymagania.

### <a name="csv-hosted-offering"></a>Hostowana CSV oferty
Jeśli w ramach własnej subskrypcji platformy Azure Twojej oferty, typowe są dwa podejścia hostingu: wdrażanie różnych wdrożenia dla każdego klienta lub wdrożeniu jednostek skalowania, które stanowi podstawę współużytkowanej infrastruktury używane dla wszystkich klientów.

* **Różne wdrożenia dla każdego klienta.** Różne wdrożeń na klienta wymaga stałej topologie znanych konfiguracji. Te wdrożenia może mieć rozmiary inną maszynę wirtualną (VM), różną liczbę węzłów i różnych ilości powiązanym magazynie. Znakowanie wdrożeń służy do rozliczeń zbiorczy każdego klienta. RBAC może być włączone tooallow klientów dostępu tooaspects środowiska chmury.
* **Jednostki skalowania w udostępnionych środowiskach wielodostępnych.** Szablon może reprezentować jednostki skalowania dla środowiska z wieloma dzierżawcami. W takim przypadku hello tej samej infrastruktury jest używane toosupport wszystkich klientów. wdrożenia Hello reprezentuje grupę zasobów dostarczających poziom pojemności dla hello hostowanej oferty, takie jak liczba użytkowników oraz liczbę transakcji. Te jednostki skali są zwiększyć lub zmniejszyć, jak długo żądanie.

### <a name="csv-offering-injected-into-customer-subscription"></a>Oferta CSV do subskrypcji klienta
Możesz toodeploy oprogramowanie do subskrypcji własnością klientów końcowych. Można użyć szablonów toodeploy różnych wdrożeń do klienta konto platformy Azure.

Te wdrożenia użycie funkcji RBAC, aby można było zaktualizować i Zarządzanie wdrażaniem hello w ramach konta powitania klienta.

### <a name="azure-marketplace"></a>Azure Marketplace
tooadvertise i sprzedawać Twojej oferty za pośrednictwem portalu marketplace, takich jak Azure Marketplace, można tworzyć szablony toodeliver różne typy wdrożenia, które są uruchamiane z konta Azure klienta. Te wdrożenia distinct można przedstawić zwykle jako rozmiar koszulki (małe, średnie, duża), typ produktu/odbiorców (społeczności, developer i enterprise) lub typu funkcji (podstawowe o wysokiej dostępności).  W niektórych przypadkach te typy pozwalają toospecify niektóre atrybuty hello, takiego jak wdrożenie typu maszyny Wirtualnej lub liczbę dysków.

## <a name="oss-projects"></a>Projekty OSS
W obrębie projektów typu open source szablonów usługi Resource Manager Włącz toodeploy społeczności rozwiązanie szybko przy użyciu sprawdzonych rozwiązań. Szablony można przechowywać w repozytorium GitHub, więc społeczności hello je skorygować w czasie. Użytkownicy wdrażania tych szablonów w ich własnej subskrypcji platformy Azure.

Witaj poniższych sekcjach podano elementów hello potrzebnych tooconsider przed rozpoczęciem projektowania rozwiązania.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>Identyfikowanie, co to jest poza i wewnątrz maszyny Wirtualnej
Podczas projektowania szablonu jest przydatne toolook na powitania wymagań w zakresie co to jest poza i wewnątrz hello maszynach wirtualnych (VM):

* Poza oznacza hello maszyn wirtualnych i innych zasobów wdrożenia, takich jak hello topologii sieci, znakowanie odwołania toohello certyfikaty/klucze tajne i kontroli dostępu opartej na rolach. Te zasoby są częścią szablonu.
* Oznacza wewnątrz hello zainstalowanego oprogramowania i potrzeby ogólnego stanu konfiguracji. Inne mechanizmy, takie jak rozszerzeń maszyny Wirtualnej lub skrypty, są używane w całości lub częściowo. Mechanizmy te mogą być zidentyfikowane i wykonywane przez szablon hello, ale nie są w nim.

Typowe przykłady działań, które należy wykonać "wewnątrz pola hello" —  

* Instalowanie lub usuwanie ról i funkcji serwera
* Instalowanie i konfigurowanie oprogramowania na poziomie hello węzła lub klastra
* Wdrażanie witryn sieci Web na serwerze sieci web
* Wdrażanie schematów bazy danych
* Zarządzanie rejestru lub inne ustawienia konfiguracji
* Zarządzanie plikami i katalogami
* Uruchamianie, zatrzymywanie i zarządzania procesami i usługami
* Zarządzanie grupami lokalnymi i kont użytkowników
* Zainstaluj pakiety i zarządzać nimi (.msi, .exe, yum itp.)
* Zarządzanie zmienne środowiskowe
* Uruchom skrypty natywnego (środowiska Windows PowerShell, bash, itp.)

### <a name="desired-state-configuration-dsc"></a>Konfiguracja żądanego stanu (DSC)
Planowanie hello wewnętrzny stan klasy poza wdrażania maszyn wirtualnych, ma toomake się, że to wdrożenie nie "rozchodzenia" z konfiguracji hello, który został zdefiniowany i zaznaczone do kontroli źródła. To podejście zapewnia deweloperów lub Operatorzy nie upewnij środowisko tooan zmian ad hoc, które nie są sprawdzane, przetestowane lub zarejestrowane w kontroli źródła. Ten formant jest ważne, ponieważ hello ręcznej zmiany nie są w kontroli źródła. Również nie są częścią wdrożenia standardowego hello i będzie miało wpływ na przyszłe zautomatyzowanych wdrożeń oprogramowania hello.

Poza pracownikom wewnętrzny konfiguracji żądanego stanu są też ważne z punktu widzenia zabezpieczeń. Przed hakerami regularnie próbujesz toocompromise i wykorzystać systemów oprogramowania. Zakończone powodzeniem jest wspólne pliki tooinstall, a w przeciwnym razie Zmień stan hello ze złamanymi zabezpieczeniami systemu. Za pomocą konfiguracji żądanego stanu, można zidentyfikować delty między hello potrzeby i rzeczywisty stan i przywrócić znanej konfiguracji.

Brak rozszerzenia zasobu dla hello najpopularniejszych mechanizmy DSC - PowerShell DSC, Chef i Puppet. Każdy z tych rozszerzeń można wdrożyć hello początkowy stan maszyny Wirtualnej i być również używane toomake się, że hello potrzeby się, że stan jest przechowywany.

## <a name="common-template-scopes"></a>Typowe zakresy szablonu
W naszym środowisku możemy przedstawiono trzy zakresy szablony klucza rozwiązania wyłonić. Te trzy zakresy — wydajność, możliwości i end-to-end rozwiązania — są opisane w hello następujące sekcje.

### <a name="capacity-scope"></a>Zakres pojemności
Zakres pojemności oferuje zestaw zasobów w standardowej topologii, który jest wstępnie skonfigurowana toobe zgodność z przepisami i zasady. najbardziej typowym przykładem Hello jest wdrażana przez środowisko deweloperskie standardowe w scenariuszu informatycznego w firmie lub tożsamości usługi.

### <a name="capability-scope"></a>Zakres możliwości
Zakres możliwości koncentruje się na wdrażanie i Konfigurowanie topologii dla danej technologii. Typowe scenariusze, w tym technologii, takich jak SQL Server, Cassandra, Hadoop.

### <a name="end-to-end-solution-scope"></a>Zakres end-to-end rozwiązania
Zakresu rozwiązania End-to-End docelowe poza jednym możliwości, a zamiast tego koncentruje się na dostarczaniu tooend rozwiązanie obejmuje kilka możliwości.  

Zakres zakres rozwiązania szablonu manifesty jako zestaw co najmniej jeden zakres możliwości szablonów zasobów specyficznych dla rozwiązania, logiki i żądanego stanu. Przykładem rozwiązania o zakresie szablonu jest szablon rozwiązania zakończenia tooend danych potoku. Szablon Hello może mieszać topologii określonego rozwiązania i stan z wielu szablonów zakres możliwości rozwiązania, takie jak Kafka, Storm i Hadoop.

## <a name="choosing-free-form-vs-known-configurations"></a>Wybranie dowolnego a znanych konfiguracji
Początkowo uważasz szablon powinien zapewnić konsumentów hello największą elastyczność, ale wiele kwestii wpłynąć na wybór hello, czy konfiguracje dowolnych toouse a znanych konfiguracji. W tej sekcji wymieniono wymagania klienta klucza hello i kwestii technicznych, które w kształcie podejście hello udostępnione w tym dokumencie.

### <a name="free-form-configurations"></a>Konfiguracje dowolnych
Na powierzchni hello konfiguracje dowolnych dźwiękowej idealne. One pozwalają tooselect typu maszyny Wirtualnej i podaj dowolną liczbę węzłów i dołączone dyski dla tych węzłów — i zrobić jako parametry szablonu tooa. Jednak ta metoda nie jest idealnym rozwiązaniem w niektórych scenariuszach.

W [rozmiary maszyn wirtualnych](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)hello różnych typach maszyn wirtualnych i dostępne rozmiary są identyfikowane i dyski każdego hello liczby trwałe (2, 4, 8, 16 i 32), który może zostać dołączony. Każdy dysk dołączony zapewnia 500 IOPS i wielu z tych dysków może puli dla mnożnik tej liczby IOPS. Na przykład 16 dysków może być tooprovide puli 8000 IOPS. Buforowanie wykonuje się za pomocą konfiguracji systemu operacyjnego hello, za pomocą funkcji miejsca do magazynowania systemu Windows firmy Microsoft lub macierzy tanich dysków (RAID) w systemie Linux.

Konfiguracja dowolnych umożliwia wybór hello kilka wystąpień maszyn wirtualnych, wirtualna różnych typów, a rozmiary w tych wystąpieniach różnych dyskach hello typu maszyny Wirtualnej, i co najmniej jeden skrypty tooconfigure hello wirtualna zawartości.

Bardzo często, że wdrożenie może mieć wiele typów węzłów, takich jak wzorzec i węzły danych, tego rodzaju elastyczności jest często podane dla każdego typu węzła.

Po rozpoczęciu toodeploy klastry żadnego znaczenia rozpoczęciem toowork z tych scenariuszy złożonych. Jeśli zostały wdrażanie klastra usługi Hadoop, na przykład z 8 węzłów głównych i węzłów 200 danych oraz puli 4 dołączonych dysków w każdym węźle głównym i puli 16 dysków dołączonych na węzeł danych, trzeba 208 maszyn wirtualnych i toomanage 3,232 dysków.

Konto magazynu będzie ograniczenie przepustowości żądań powyżej jego zidentyfikowanych 20 000 ograniczyć transakcje na sekundę, należy przyjrzeć się partycjonowanie konta magazynu i użyć obliczenia się, że toodetermine hello odpowiedniej liczby magazynu kont tooaccommodate tej topologii. Podane wieloma hello kombinacji obsługiwane przez hello dowolnych podejście, obliczenia dynamiczne są wymagane toodetermine hello odpowiednie partycjonowania. Witaj język szablonu usługi Azure Resource Manager nie zawiera obecnie funkcje matematyczne, należy wykonać te obliczenia w kodzie, generowania unikatowych, ustalony szablonu z hello odpowiednie informacje.

W organizacji IT i scenariusze SI ktoś Obsługa szablonów hello i obsługuje topologie hello wdrożony co najmniej jeden organizacji. To dodatkowe obciążenie — szablony dla każdego klienta i różnych konfiguracjach — równocześnie pożądane.

Możesz użyć tych środowisk toodeploy szablonów w subskrypcji Azure klienta, ale zespoły IT firmy i woluminy CSV zwykle wdrożyć je do ich własnych subskrypcji przy użyciu toobill funkcja obciążenia zwrotnego klientom. W tych scenariuszach celem hello jest toodeploy pojemność dla wielu klientów w puli subskrypcji i Zachowaj wdrożeń gęsto umieszczane w hello subskrypcje toominimize subskrypcji przetwarzania — to znaczy więcej toomanage subskrypcji. O rozmiarze naprawdę dynamiczne wdrożenia osiągnięcie tego typu gęstość wymaga zachować ostrożność podczas planowania i projektowania dodatkowe szkieletów pracy w imieniu organizacji hello.

Ponadto nie można utworzyć subskrypcji za pośrednictwem wywołania interfejsu API, ale należy to zrobić ręcznie za pośrednictwem portalu hello. Zwiększa liczbę hello subskrypcji, wszelkie wynikowy przetwarzania subskrypcji wymaga udziału człowieka — nie mogły zostać zautomatyzowane. Z bardzo dużo zmienności rozmiary hello wdrożeń, należy udostępnić toopre liczbę subskrypcji ręcznie tooensure subskrypcje są dostępne.

Biorąc pod uwagę następujące czynniki Konfiguracja naprawdę dowolnych jest mniej atrakcyjne niż co najpierw blush.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>Znane konfiguracje — Witaj podejście zmiany rozmiaru obrazów na koszulki
Nie oferują szablon, który zapewnia elastyczność całkowitej i niezliczonych zmian, wiemy z doświadczenia wspólnego wzorca jest raczej tooselect możliwości hello tooprovide znane konfiguracje — w efekcie rozmiary obrazów na standardowe koszulki takich jak piaskownicy, małych, średnich i dużych. Inne przykłady rozmiary obrazów na koszulki są ofert produktów, takich jak community edition lub enterprise edition.  W innych przypadkach może być konfiguracje specyficznego dla obciążenia technologii — takie jak ograniczyć mapy lub nie sql.

Wiele organizacji IT organizacji, dostawców OSS i SIs udostępnianie ich ofert dzisiaj w ten sposób w lokalnej, zwirtualizowanych środowiskach (przedsiębiorstwa) lub oprogramowania jako usługa (SaaS) oferty (woluminy CSV i OSVs).

Takie podejście zapewnia dobre, znanej konfiguracji o różnych rozmiarach, które są wstępnie skonfigurowane dla klientów. Bez znanych konfiguracji klientów końcowych musi określić rozmiaru klastra na ich własnych, uwzględnieniu ograniczenia zasobów platformy i czy matematyczne tooidentify hello wynikowa partycjonowanie konta magazynu i innych zasobów (z powodu rozmiaru toocluster i zasobów ograniczenia). Znane konfiguracje włączyć klientów tooeasily hello wybierz prawa Rozmiar koszulki — to znaczy danego wdrożenia. Ponadto toomaking lepsze środowisko dla powitania klienta niewielkiej liczby znanych konfiguracji jest łatwiejsze toosupport i ułatwiają dostarczanie wyższego poziomu gęstości.

To podejście znanej konfiguracji koncentruje się na rozmiary obrazów na koszulki mogą także mieć różną liczbę węzłów w rozmiarze. Na przykład mały rozmiar koszulki może być między węzłami 3 do 10.  Rozmiar koszulki Hello może być zaprojektowana tooaccommodate zapasowych too10 węzłów i podaj hello konsumenta hello możliwości toomake dowolnej postaci opcje toohello rozmiar maksymalny zidentyfikowane.  

Rozmiar koszulki, na podstawie typu obciążenie może być więcej dowolnej postaci charakteru pod względem hello liczba węzłów, które można wdrożyć, ale mają rozmiar węzła różne obciążenia i konfiguracji oprogramowania hello na powitania węzła.

Rozmiary obrazów na koszulki oparte na ofert produktów, takich jak społeczność lub przedsiębiorstwa, może mieć typów różnych zasobów i maksymalną liczbę węzłów, które można wdrożyć, zwykle powiązane zagadnienia toolicensing lub dostępność funkcji w różnych ofert hello.

Można również zapewnić klientom z unikatowy wariantów za pomocą szablonów opartych na formacie JSON hello. Podczas pracy nad wartości odstających, możesz dołączyć do nich hello odpowiednie planowania i zagadnienia dotyczące projektowania, pomocy technicznej i analiza kosztów.

Na podstawie zużycia hello scenariuszy szablonu i wymagania określone na początku hello tego dokumentu, określiliśmy, że wzorzec do rozkładu szablonu.

## <a name="capacity-and-capability-scoped-solution-templates"></a>Pojemność i szablony zakres możliwości rozwiązania
Rozkład zapewnia projektowania tootemplate podejściu, które obsługuje ponowne użycie, rozszerzalności, testowania i narzędzi. Ta sekcja zawiera szczegóły na jak podejście dekompozycji może być zastosowane tootemplates z zakresem możliwości.

W tej metody szablonu głównego odbiera wartości parametrów od konsumenta szablonu, a następnie łączy tooseveral typów szablonów i skryptów poniżej, jak pokazano poniżej. Parametry, zmienne statyczne i wygenerowanego zmienne są używane tooprovide wartości i szablonów hello połączone.

![Parametry szablonu](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**Parametry są przekazywane tooa szablonie głównym, a następnie toolinked szablonów**

następujące sekcje fokus na powitania typów szablonów i skrypty, które jednego szablonu jest rozłożone na powitania. sekcje Hello przedstawia podejścia do przekazywania informacji o stanie między hello szablonów. Opisano każdego szablonu i hello typy skryptu w obrazie hello wraz z przykładami. Na przykład kontekstowe, zobacz "umieścić go razem: Przykładowe zastosowanie" dalszej części tego dokumentu.

### <a name="template-metadata"></a>Metadane szablonu
Metadane szablonu (plik metadata.json hello) zawiera opis szablonu w formacie JSON, który może zostać odczytany przez ludzi i systemów oprogramowania par klucz/wartość.

![Metadane szablonu](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Metadane szablonu jest opisany w pliku metadata.json hello**

Agenci oprogramowanie można pobrać pliku metadata.json hello i publikowania informacji hello i szablon toohello link w katalogu lub strony sieci web. Elementy obejmują *itemDisplayName*, *opis*, *podsumowania*, *githubUsername*, i *dateUpdated*.

Poniżej przedstawiono przykładowy plik w całości.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>Główny szablonu
Szablon głównego Hello odbiera parametrów z użytkownikiem, korzysta z tej informacji toopopulate obiekt złożony zmienne i wykonuje szablony hello połączone.

![Główny szablonu](./media/best-practices-resource-manager-design-templates/main-template.png)

**szablonu głównego Hello odbiera parametrów z użytkownikiem**

Jeden parametr, który został dostarczony jest typem znanej konfiguracji znanej także jako hello parametr rozmiaru obrazów na koszulki ze względu na jego wartości standardowych, takich jak małych, średnich i dużych. W praktyce można użyć tego parametru na wiele sposobów. Aby uzyskać więcej informacji zobacz temat "Znanej konfiguracji zasobów szablonu" w dalszej części tego dokumentu.

Niektóre zasoby są wdrażane niezależnie od tego, znanej konfiguracji hello określonej przez parametr użytkownika. Te zasoby są udostępniane za pomocą szablonu pojedynczego zasobu udostępnionego i są współużytkowane przez innych szablonów, więc hello udostępnianego zasobu szablon jest uruchamiany pierwszy.

Niektóre zasoby są wdrażane opcjonalnie niezależnie od określonej konfiguracji znanych hello.

### <a name="shared-resources-template"></a>Udostępnione zasoby szablonu
Ten szablon udostępnia zasoby, które są wspólne dla wszystkich znanych konfiguracji. Zawiera sieć wirtualną hello, zestawów dostępności i inne zasoby, które są wymagane niezależnie od hello znanej konfiguracji szablonu, które zostało wdrożone.

![Zasobów szablonu](./media/best-practices-resource-manager-design-templates/template-resources.png)

**Udostępnione zasoby szablonu**

Nazwy zasobów, takie jak nazwa sieci wirtualnej hello, na podstawie hello głównym szablonu. Można określić je jako zmienną w obrębie tego szablonu lub ich odbierania jako parametr użytkownika hello, zgodnie z wymaganiami organizacji.

### <a name="optional-resources-template"></a>Opcjonalne zasoby szablonu
Hello szablon opcjonalnych zasobów zawiera zasoby programowe wdrażane na podstawie wartości hello parametr lub zmienna.

![Opcjonalne zasoby](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**Opcjonalne zasoby szablonu**

Na przykład można użyć opcjonalnych zasobów szablonu tooconfigure jumpbox, który umożliwia bezpośredni dostęp tooa wdrożyć środowisko z hello publicznej sieci Internet. Czy powinno być włączone hello jumpbox użyje tooidentify parametr lub zmienna i hello *concat* funkcji takich jak nazwa docelowej hello toobuild dla szablonu hello *jumpbox_enabled.json*. Łączenie szablonu użyje hello wynikowy jumpbox hello tooinstall zmiennej.

Możesz połączyć hello opcjonalnych zasobów szablonu w wielu miejscach:

* Podczas wdrażania odpowiednich tooevery połączyć oparte na parametr szablonu zasobów udostępnionych hello.
* Gdy dotyczy tooselect znane konfiguracje — na przykład zainstalować tylko w dużych wdrożeniach — połączyć oparte na parametr lub zmienna driven hello znanej konfiguracji szablonu.

Określa, czy dany zasób jest opcjonalny mogą nie kierować hello szablon konsumenta tylko przez dostawcę szablonu hello. Na przykład może wymagać toosatisfy wymagania danego produktu lub dodatek produktu (wspólne dla woluminów CSV) lub zasad tooenforce (w przypadku SIs i rozwiązaniami INFORMATYCZNYMI dla firm grupy). W takich przypadkach można użyć zmiennej tooidentify czy hello zasobu powinny zostać wdrożone.

### <a name="known-configuration-resources-template"></a>Szablon zasobów znanej konfiguracji
W szablonie głównym hello parametr może być uwidocznione tooallow hello szablon konsumenta toospecify toodeploy wymaganą konfiguracją znane. Często ta konfiguracja znane korzysta z podejścia rozmiar obrazów na koszulki z zestawem rozmiary stałym konfiguracji, takie jak piaskownicy, małe, średnie i duże.

![Zasoby znanej konfiguracji](./media/best-practices-resource-manager-design-templates/known-config.png)

**Szablon zasobów znanej konfiguracji**

podejście rozmiar obrazów na koszulki Hello jest najczęściej używany, ale parametry hello może reprezentować dowolny zbiór znanych konfiguracji. Na przykład można określić zestaw środowisk dla aplikacji przedsiębiorstwa, takich jak projektowanie, testów i produktu. Można też użyć dla toorepresent usługi chmury różnych skalowania jednostki, wersje produktu lub konfiguracje produktu, takie jak społeczności deweloperów i Enterprise.

Podobnie jak w przypadku hello udostępnianego zasobu szablon, zmiennych są przekazywane toohello znanych konfiguracji szablonu z poziomu:

* Użytkownik końcowy — czyli parametry hello wysyłane toohello głównym szablonu.
* Organizacja — to znaczy hello zmienne w szablonie głównym hello, które reprezentują wymagań wewnętrznych lub zasad.

### <a name="member-resources-template"></a>Szablon elementu członkowskiego zasobów
W znanej konfiguracji co najmniej jednego elementu członkowskiego typu węzła często są dołączone. Na przykład z platformą Hadoop masz węzłów głównych i węzły danych. Jeśli instalujesz bazy danych MongoDB ma węzły danych i kryterium. Jeśli wdrażasz DataStax masz węzły danych i maszyny Wirtualnej z OpsCenter zainstalowane.

![Elementy członkowskie zasobów](./media/best-practices-resource-manager-design-templates/member-resources.png)

**Szablon elementu członkowskiego zasobów**

Poszczególne typy węzłów można mają różne rozmiary maszyn wirtualnych, liczba dołączonych dysków, tooinstall skryptów i skonfiguruj hello węzłów, konfiguracji portów dla hello maszyn wirtualnych, liczba wystąpień i inne szczegóły. Tak każdy typ węzła pobiera własnego szablonu zasobów elementu członkowskiego, który zawiera hello szczegółów wdrażanie i konfigurowanie infrastruktury, a także wykonywanie skryptów toodeploy i konfigurowanie oprogramowania w ramach hello maszyny Wirtualnej.

Dla maszyn wirtualnych zazwyczaj dwa typy skryptów są używane, powszechnie wielokrotnego użytku i niestandardowych skryptów.

### <a name="widely-reusable-scripts"></a>Skrypty powszechnie wielokrotnego użytku
Można używać skryptów powszechnie wielokrotnego użytku przez wiele typów szablonów. Jedna z hello lepsze Przykłady te skrypty powszechnie wielokrotnego użytku konfiguruje RAID na dyskach toopool systemu Linux i uzyskać większą liczbę IOPS. Niezależnie od oprogramowania hello instalowane w hello maszyny Wirtualnej skrypt umożliwia ponowne użycie sprawdzonych rozwiązań dla typowych scenariuszy.

![Skryptów wielokrotnego użytku](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**Szablony zasobów Członkowskich można wywołać skryptów powszechnie wielokrotnego użytku**

### <a name="custom-scripts"></a>Niestandardowych skryptów
Szablony zwykle wywołać co najmniej jeden skrypty, które Instalowanie i konfigurowanie oprogramowania w maszynach wirtualnych. Wspólnego wzorca jest widoczna w dużych topologiach wdrożonym wielu wystąpień co najmniej jeden typ elementu członkowskiego. Skrypt instalacji jest inicjowane dla każdej maszyny Wirtualnej, które mogą być wykonywane równolegle, następuje skrypt instalacji, który jest wywoływana po wdrożeniu wszystkich maszyn wirtualnych (lub wszystkich maszyn wirtualnych typu danego elementu członkowskiego).

![Niestandardowych skryptów](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**Szablony zasobów Członkowskich można wywołać skryptów do określonego celu, takie jak konfiguracja maszyny Wirtualnej**

## <a name="capability-scoped-solution-template-example---redis"></a>Przykład szablonu zakres możliwości rozwiązania — Redis
tooshow jak implementacja może działać, Przyjrzyjmy się praktycznym przykładem tworzenia szablonu, który ułatwia wdrażanie hello i konfigurację pamięci podręcznej Redis w standardowe rozmiary obrazów na koszulki.  

W przypadku wdrożenia hello istnieje zestaw zasobów udostępnionych (sieci wirtualne, konta magazynu, zestawów dostępności) i opcjonalnie zasobów (jumpbox). Istnieją znane konfiguracji z wieloma reprezentowane jako rozmiary obrazów na koszulki (małe, średnie, duża), ale każdego z jednego węzła typu. Istnieją również dwa skrypty specyficzne dla celu (instalacji, konfiguracji).

### <a name="creating-hello-template-files"></a>Tworzenie hello pliki szablonów
Należy utworzyć szablon głównego o nazwie azuredeploy.json.

Utwórz szablon zasobów o nazwie resources.json udostępnionych

Utwórz wdrożenie hello tooenable opcjonalne szablonu zasobów jumpbox, o nazwie jumpbox_enabled.json

Redis używa tylko jednego węzła o typie, utworzyć szablon pojedynczego zasobu elementu członkowskiego o nazwie resources.json węzła.

Z pamięci podręcznej Redis mają tooinstall każdego indywidualnego węzła, a następnie ponowne skonfigurowanie klastra hello.  Skrypty tooaccommodate hello instalacja i konfigurowanie pamięci podręcznej redis klastra install.sh i setup.sh-redis klastra.

### <a name="linking-hello-templates"></a>Łączenie hello szablonów
Przy użyciu szablonu połączeń, hello szablonu głównego łączy się toohello zasobów udostępnionych szablonu, który określa hello sieci wirtualnej.

Logika jest dodawani hello szablonu głównego tooenable konsumentów hello szablonu toospecify czy jumpbox powinny zostać wdrożone. *Włączone* wartość hello *EnableJumpbox* parametr wskazuje toodeploy jumpbox chce powitania klienta. Gdy ta wartość zostanie podana, szablon hello łączy *_enabled* sufiks nazwy szablonu podstawowego tooa hello jumpbox możliwości.

Szablon głównego Hello stosuje hello *dużych* wartość parametru jako nazwę szablonu podstawowego tooa sufiks rozmiary obrazów na koszulki, a następnie używa tej wartości w łączu szablonu wychodzących za*technology_on_os_large.json*.

Topologia Hello będzie wyglądać na tej ilustracji.

![Redis szablonu](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Struktura szablonu dla szablonu Redis**

### <a name="configuring-state"></a>Konfigurowanie stanu
Hello węzłów w klastrze hello istnieją dwa kroki tooconfiguring hello stanu, zarówno reprezentowany przez skrypty określonego celu.  Redis instaluje "redis klastra install.sh" i "redis klastra setup.sh" Ustawia hello klastra.

### <a name="supporting-different-size-deployments"></a>Obsługa wdrożeń inny rozmiar
Wewnątrz zmiennych szablonu rozmiar obrazów na koszulki hello określa hello liczba węzłów każdego typu toodeploy dla hello określony rozmiar (*dużych*). Następnie wdraża tej liczby wystąpień maszyn wirtualnych przy użyciu pętli zasobów, zapewniając tooresources unikatowe nazwy przez dodanie nazwy węzła z liczbą sekwencji liczbową z *copyIndex()*. Robi te kroki dla obu gorącego i ciepłych strefy maszyn wirtualnych, zgodnie z definicją w szablonie nazwy obrazów na koszulki hello

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>Szablony rozwiązania w zakresie dekompozycji i end-to-end
Szablon rozwiązania w zakresie rozwiązania end-to-end koncentruje się na dostarczanie rozwiązania end-to-end.  Ta metoda jest zwykle kompozycji wielu szablonów zakres możliwości dodatkowe zasoby, logiki i stanu.

Jako wyróżniane na poniższym obrazie hello hello tego samego modelu używanego dla szablonów możliwości zakres jest rozszerzony na użytek szablonów w zakresie rozwiązania End-to-End.

Udostępnione zasoby szablonu i opcjonalnie szablony zasobów służą hello tę samą funkcję jak hello pojemności i możliwości zakres podejścia szablonu, ale są w zakresie hello tooend rozwiązanie.

Zakres tooend rozwiązanie szablony również można zwykle mają rozmiary obrazów na koszulki, hello znanych zasobów konfiguracji szablonu odzwierciedla, co jest wymagane dla danej konfiguracji znanych hello rozwiązania.

tooone łącza znane konfiguracji szablonu zasobów Hello lub więcej możliwości zakresu szablonów rozwiązania, które są odpowiednie toohello tooend rozwiązanie, a także hello szablony zasobów elementu członkowskiego, która jest wymagana dla hello tooend rozwiązanie.

Rozmiar koszulki hello hello rozwiązania mogą różnić się od szablonu hello poszczególnych zakres możliwości, zmiennych w hello znane konfiguracji szablonu zasobów są używane tooprovide hello odpowiednie wartości dla rozwiązania możliwości podrzędny zakres Szablony toodeploy hello odpowiedni rozmiar koszulki.

![End-to-end](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**Hello model używany pojemności lub zakres możliwości rozwiązania szablonów można łatwo rozszerzony na użytek zakresy szablon rozwiązania tooend zakończenia**

## <a name="preparing-templates-for-hello-marketplace"></a>Przygotowywanie szablony hello Marketplace
Hello łatwo poprzedzających podejście bierze pod uwagę scenariusze, w których przedsiębiorstwa, SIs i woluminów CSV tooeither chcesz wdrożyć szablony hello lub Włącz ich toodeploy klientów na ich własnych.

Innym scenariuszu żądany jest wdrażanie szablonu za pomocą hello marketplace.  Takie podejście dekompozycji działa w przypadku marketplace hello również z niewielkimi zmianami.

Jak wspomniano wcześniej, szablonów można typy wdrożeń różne toooffer używanych do sprzedaży w witrynie marketplace hello. Typy wdrożeń różne może być rozmiary obrazów na koszulki (małe, średnie, duża), typ produktu/odbiorców (społeczności, developer i enterprise) lub typu funkcji (podstawowe o wysokiej dostępności).

Jak pokazano poniżej, hello istniejących tooend zakończenia rozwiązania lub możliwości zakresie szablonów można łatwo wykorzystana hello toolist różne konfiguracje znane hello rynku.

Hello szablonu głównego toohello parametry są najpierw zmodyfikować tooremove hello przychodzących parametru o nazwie tshirtSize.

Podczas mapowania typów wdrożenia różne hello toohello znane konfiguracji szablonu zasobów, muszą hello wspólnych zasobów i znaleźć konfiguracji w hello szablonu zasobów udostępnionych oraz potencjalnie w opcjonalne szablony zasobów.

Jeśli chcesz toopublish Twojego marketplace toohello szablonu, należy ustanowić różne kopie zastępujący hello wcześniej dostępne dla ruchu przychodzącego parametru zmiennej tooa tshirtSize osadzone w szablonie hello szablonu głównego.

![Portal Marketplace](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Dostosowania rozwiązania o zakresie szablonu dla hello marketplace**

## <a name="next-steps"></a>Następne kroki
* toolearn o udostępnianiu stanu do i z szablonów, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

