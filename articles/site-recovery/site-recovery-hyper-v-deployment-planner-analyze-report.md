---
title: "Planista wdrażania usługi Azure Site Recovery dla funkcji Hyper-V na platformie Azure | Microsoft Docs"
description: "W tym artykule opisano analizę wygenerowanego raportu planisty wdrożenia usługi Azure Site Recovery w przypadku scenariusza dotyczącego funkcji Hyper-V na platformie Azure."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/02/2017
ms.author: nisoneji
ms.openlocfilehash: 9340fe48c1da874d6c0cf02c026e5dec6ddabbe7
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2017
---
# <a name="analyze-the-azure-site-recovery-deployment-planner-report"></a>Analizowanie raportu planisty wdrożenia usługi Azure Site Recovery
Wygenerowany raport programu Microsoft Excel zawiera następujące arkusze:

## <a name="on-premises-summary"></a>Podsumowanie środowiska lokalnego
Arkusz Podsumowanie środowiska lokalnego zawiera przegląd profilowanego środowiska funkcji Hyper-V ![Podsumowanie środowiska lokalnego](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-summary-h2a.png)

**Data rozpoczęcia** i **Data zakończenia**: daty rozpoczęcia i zakończenia profilowania danych na potrzeby generowania raportu. Domyślnie data rozpoczęcia to data rozpoczęcia profilowania, a data zakończenia to data zatrzymania profilowania. Mogą to być wartości „StartDate” i „EndDate”, jeśli raport jest generowany przy użyciu tych parametrów.

**Łączna liczba dni profilowania**: całkowita liczba dni profilowania od daty rozpoczęcia do daty zakończenia, dla których jest generowany raport.

**Liczba zgodnych maszyn wirtualnych**: całkowita liczba zgodnych maszyn wirtualnych, dla których są obliczane: wymagana przepustowość sieci, wymagana liczba kont magazynu i liczba rdzeni platformy Microsoft Azure.

**Łączna liczba dysków na wszystkich zgodnych maszynach wirtualnych**: całkowita liczba dysków wszystkich zgodnych maszyn wirtualnych.

**Średnia liczba dysków na zgodną maszynę wirtualną**: średnia liczba dysków obliczana dla wszystkich zgodnych maszyn wirtualnych.

**Średni rozmiar dysku (GB)**: średni rozmiar dysku obliczany dla wszystkich zgodnych maszyn wirtualnych.

**Żądany cel punktu odzyskiwania (w minutach)**: domyślny cel punktu odzyskiwania lub przekazana wartość parametru „DesiredRPO” podczas generowania raportu, które umożliwiają oszacowanie wymaganej przepustowości.

**Żądana przepustowość (Mb/s)**: przekazana wartość parametru „Bandwidth” podczas generowania raportu umożliwiająca oszacowanie osiągalnego celu punktu odzyskiwania.

**Zaobserwowany dzienny typowy współczynnik zmian danych (GB)**: średni współczynnik zmian danych zaobserwowany we wszystkie dni profilowania.

## <a name="recommendations"></a>Zalecenia  
Arkusz Zalecenia raportu dotyczącego replikacji z funkcji Hyper-V do platformy Azure zawiera następujące szczegółowe informacje zgodnie z wybranym żądanym celem punktu odzyskiwania:

![Zalecenia z raportu replikacji z funkcji Hyper-V do platformy Azure](media/site-recovery-hyper-v-deployment-planner-analyze-report/Recommendations-h2a.png)

### <a name="profile-data"></a>Profilowanie danych
![Profilowanie danych](media/site-recovery-hyper-v-deployment-planner-analyze-report/profile-data-h2a.png)

**Okres profilowanych danych**: okres, podczas którego działało profilowanie. Domyślnie w obliczeniach narzędzie uwzględnia wszystkie profilowane dane. Jeśli podczas generowania raportu użyto opcji StartDate and EndDate, będzie on obejmować wybrany okres. 

**Liczba profilowanych serwerów funkcji Hyper-V**: liczba serwerów funkcji Hyper-V, które obejmuje generowany raport maszyn wirtualnych. Kliknij liczbę, aby wyświetlić nazwy serwerów funkcji Hyper-V. Spowoduje to otwarcie arkusza wymagań dotyczących magazynu lokalnego, w którym zostaną wyświetlone wszystkie serwery z wymaganiami dotyczącymi magazynu.    

**Żądany cel punktu odzyskiwania**: cel punktu odzyskiwania dla danego wdrożenia. Domyślnie wymagana przepustowość sieci jest obliczana dla wartości celu punktu odzyskiwania równych 15, 30 i 60 minut. Odpowiednie wartości są aktualizowane w arkuszu zgodnie z wybraną wartością. W przypadku użycia parametru DesiredRPOinMin podczas generowania raportu ta wartość jest wyświetlana w obszarze wyniku żądanego celu punktu odzyskiwania.

### <a name="profiling-overview"></a>Omówienie profilowania
![Omówienie profilowania](media/site-recovery-hyper-v-deployment-planner-analyze-report/profiling-overview-h2a.png)

**Łączna liczba profilowanych maszyn wirtualnych**: całkowita liczba maszyn wirtualnych, których profilowane dane są dostępne. Jeśli parametr VMListFile zawiera nazwy nieprofilowanych maszyn wirtualnych, te maszyny wirtualne nie zostaną uwzględnione podczas generowania raportów i zostaną wykluczone z łącznej liczby profilowanych maszyn wirtualnych.

**Zgodne maszyny wirtualne**: liczba maszyn wirtualnych, które mogą być chronione na platformie Azure przy użyciu usługi Azure Site Recovery. Jest to łączna liczba zgodnych maszyn wirtualnych, dla których są obliczane: wymagana przepustowość sieci, liczba kont magazynu i liczba rdzeni platformy Azure. Szczegóły wszystkich maszyn wirtualnych są dostępne w sekcji „Zgodne maszyny wirtualne”.

**Niezgodne maszyny wirtualne**: liczba profilowanych maszyn wirtualnych, które nie są zgodne na potrzeby ochrony za pomocą usługi Azure Site Recovery. Przyczyny niezgodności wymieniono w sekcji „Niezgodne maszyny wirtualne”. Jeśli plik VMListFile zawiera nazwy maszyn wirtualnych, które nie były profilowane, te maszyny wirtualne są wykluczane z liczby niezgodnych maszyn wirtualnych. Dla tych maszyn wirtualnych jest wyświetlany tekst „Nie znaleziono danych” na końcu sekcji „Niezgodne maszyny wirtualne”.

**Żądany cel punktu odzyskiwania**: żądany cel punktu odzyskiwania w minutach. Raport jest generowany dla trzech wartości celu punktu odzyskiwania: 15 (ustawienie domyślne), 30 i 60 minut. Zalecenie dotyczące przepustowości w raporcie zmienia się zgodnie z pozycją wybraną z listy rozwijanej żądanego celu punktu odzyskiwania w prawym górnym rogu arkusza. Jeśli raport został wygenerowany przy użyciu parametru -DesiredRPO z wartością niestandardową, ta wartość jest wyświetlana jako domyślna na liście rozwijanej żądanego celu punktu odzyskiwania.

### <a name="required-network-bandwidth-mbps"></a>Wymagana przepustowość sieci (Mb/s)
![Wymagana przepustowość sieci](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-network-bandwidth-h2a.png)

**Aby osiągnąć cel punktu odzyskiwania przez 100 procent czasu**: zalecana przepustowość (w Mb/s) do przydzielenia, która umożliwia osiąganie żądanego celu punktu odzyskiwania przez 100 procent czasu. Taka przepustowość musi zostać przeznaczona na stałą replikację przyrostową wszystkich zgodnych maszyn wirtualnych, aby uniknąć naruszeń celu punktu odzyskiwania.

**Aby osiągnąć cel punktu odzyskiwania przez 90 procent czasu**: jeśli z powodów związanych z cenami połączeń szerokopasmowych lub innych nie możesz ustawić przepustowości wymaganej do osiągnięcia żądanego celu punktu odzyskiwania przez 100 procent czasu, możesz wybrać mniejszą przepustowość umożliwiającą osiągnięcie żądanego celu punktu odzyskiwania przez 90 procent czasu. Aby umożliwić poznanie skutków ustawienia mniejszej przepustowości, w raporcie przedstawiono analizę warunkową liczby i czasu trwania naruszeń celu punktu odzyskiwania.

**Osiągnięta przepływność**: przepływność między serwerem, na którym uruchomiono polecenie GetThroughput, i regionem platformy Azure, w którym znajduje się konto magazynu. Ta wartość przepływności wskazuje przybliżony poziom, który można osiągnąć podczas ochrony zgodnych maszyn wirtualnych za pomocą usługi Azure Site Recovery, jeśli charakterystyka sieci i magazynu serwera funkcji Hyper-V pozostają takie same jak w przypadku serwera, na którym uruchomiono narzędzie.

W przypadku wszystkich wdrożeń usługi Azure Site Recovery w przedsiębiorstwach zalecamy użycie usługi [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Wymagane konta magazynu
Ten wykres przedstawia łączną liczbę kont magazynu (w warstwach Standardowa i Premium) wymaganych do ochrony wszystkich zgodnych maszyn wirtualnych. Aby dowiedzieć się, którego konta magazynu używać dla poszczególnych maszyn wirtualnych, zobacz sekcję „Rozmieszczenie maszyny wirtualnej względem magazynu”.

![Wymagane konta magazynu](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-storage-accounts-h2a.png)

### <a name="required-number-of-azure-cores"></a>Wymagana liczba rdzeni platformy Azure
Wynik to łączna liczba rdzeni do skonfigurowania przed rozpoczęciem pracy w trybie failover lub testem pracy w trybie failover dla wszystkich zgodnych maszyn wirtualnych. Jeśli liczba rdzeni w ramach subskrypcji jest zbyt mała, usługa Azure Site Recovery nie może utworzyć maszyn wirtualnych w czasie pracy w trybie failover lub testu pracy w trybie failover.
![Wymagana liczba rdzeni platformy Azure](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-number-of-azure-cores-h2a.png)


### <a name="additional-on-premises-storage-requirement"></a>Wymagania dotyczące dodatkowego magazynu lokalnego

Całkowita ilość wolnego miejsca wymagana na serwerach funkcji Hyper-V do pomyślnej replikacji początkowej i replikacji różnicowej, dzięki której będziesz mieć pewność, że replikacja maszyny wirtualnej nie spowoduje niepożądanych przestojów w działaniu aplikacji produkcyjnych. Szczegóły wymagań dotyczących poszczególnych woluminów są dostępne w sekcji [wymagań dotyczących magazynu lokalnego](#on-premises-storage-requirement). 

Aby zrozumieć, dlaczego do replikacji jest wymagane wolne miejsce, zapoznaj się z sekcją [wymagań dotyczących magazynu lokalnego](#why-do-i-need-free-space-on-the-hyper-v-server-for-the-replication).

![wymagania dotyczące magazynu lokalnego i częstotliwość kopiowania](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-storage-and-copy-frequency-h2a.png)

### <a name="maximum-copy-frequency"></a>Maksymalna częstotliwość kopiowania
Maksymalną zalecaną częstotliwość kopiowania należy ustawić, aby osiągać żądany cel punktu odzyskiwania. Wartość domyślna to 5 minut. Aby osiągać lepszy cel punktu odzyskiwania, można ustawić częstotliwość kopiowania na 30 sekund.

### <a name="what-if-analysis"></a>Analiza warunkowa
![Analiza warunkowa](media/site-recovery-hyper-v-deployment-planner-analyze-report/what-if-analysis-h2a.png) Ta analiza przedstawia liczbę naruszeń, które mogą wystąpić podczas profilowania w przypadku ustawienia mniejszej przepustowości umożliwiającej osiąganie żądanego celu punktu odzyskiwania tylko przez 90% czasu. W danym dniu może wystąpić co najmniej jedno naruszenie. Wykres przedstawia szczyt celu punktu odzyskiwania w danym dniu. Na podstawie tej analizy można zdecydować, czy liczba naruszeń celu punktu odzyskiwania we wszystkich dniach i szczytowa wartość celu punktu odzyskiwania na dzień jest dopuszczalna przy określonej mniejszej przepustowości. Jeśli tak, można przydzielić mniejszą przepustowość na potrzeby replikacji. W przeciwnym razie przydziel większą przepustowość zgodnie z propozycją, aby osiągać żądany cel punktu odzyskiwania przez 100 procent czasu. 

### <a name="recommendation-for-successful-initial-replication"></a>Zalecenie dotyczące pomyślnej replikacji początkowej
W tej sekcji przedstawiamy zalecenie dotyczące liczby partii, w których maszyny wirtualne mają być chronione, oraz minimalnej przepustowości wymaganej do pomyślnego ukończenia replikacji początkowej (IR, initial replication). 

![Dzielenie replikacji początkowej na partie](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-h2a.png)

Maszyna wirtualna musi być chroniona z zachowaniem podanej kolejności partii. Każda partia ma określoną listę maszyn wirtualnych. Maszyny wirtualne partii 1 muszą być chronione przed partią 2. Maszyny wirtualne partii 2 muszą być chronione przed partią 3 itd. Po zakończeniu replikacji początkowej maszyn wirtualnych partii 1 można włączyć replikację dla maszyn wirtualnych partii 2. Podobnie po zakończeniu replikacji początkowej maszyn wirtualnych partii 2 można włączyć replikację dla maszyn wirtualnych partii 3 itd. Jeśli kolejność partii nie będzie przestrzegana, wystarczająca przepustowość dla replikacji początkowej może być niedostępna dla maszyn wirtualnych chronionych później. W wyniku maszyny wirtualne nigdy nie będą mogły ukończyć replikacji początkowej lub kilka chronionych maszyn wirtualnych może przejść do trybu ponownej synchronizacji. Arkusz dzielenia replikacji początkowej na partie dla wybranego celu punktu odzyskiwania zawiera szczegółowe informacje na temat maszyn wirtualnych, które powinny zostać uwzględnione w każdej partii.

Na poniższym wykresie przedstawiono rozkład przepustowości dla replikacji początkowej i replikacji różnicowej w partiach w danej kolejności. W przypadku ochrony maszyn wirtualnych z pierwszej partii w replikacji początkowej jest dostępna pełna przepustowość. Po zakończeniu replikacji początkowej pierwszej partii część przepustowości będzie wymagana na potrzeby replikacji różnicowej. Pozostała przepustowość będzie dostępna podczas replikacji początkowej maszyn wirtualnych drugiej partii. Na pasku partii 2 przedstawiono wymaganą przepustowości replikacji różnicowej dla maszyn wirtualnych partii 1 i przepustowość dostępną dla replikacji początkowej maszyn wirtualnych partii 2. Podobnie na pasku partii 3 przedstawiono przepustowość wymaganą dla replikacji różnicowej poprzednich partii (maszyn wirtualnych partii 1 i partii 2) oraz przepustowość dostępną na potrzeby replikacji początkowej dla partii 3 itd.  Po zakończeniu replikacji początkowej wszystkich partii ostatni pasek pokazuje przepustowość wymaganą na potrzeby replikacji różnicowej dla wszystkich chronionych maszyn wirtualnych. 

**Dlaczego należy podzielić replikację początkową na partie?**
Czas ukończenia replikacji początkowej opiera się na rozmiarze dysku maszyny wirtualnej, używanym miejscu na dysku i dostępnej przepływności sieci. Szczegóły są dostępne w arkuszu dzielenia replikacji początkowej na partie na dla wybranego celu punktu odzyskiwania.

### <a name="cost-estimation"></a>Szacowanie kosztów
Na wykresie przedstawiono podsumowanie szacowanych łącznych kosztów odzyskiwania po awarii (DR) na platformie Azure w wybranym regionie docelowym w walucie określonej na potrzeby generowania raportu.
![Podsumowanie szacowania kosztów](media/site-recovery-hyper-v-deployment-planner-analyze-report/cost-estimation-summary-h2a.png) Podsumowanie pomaga zrozumieć ponoszone koszty magazynowania, obliczania, użycia sieci i licencji w przypadku ochrony wszystkich zgodnych maszyn wirtualnych na platformie Azure przy użyciu usługi Azure Site Recovery. Koszt jest obliczany dla zgodnych maszyn wirtualnych, a nie dla wszystkich profilowanych maszyn wirtualnych.  
 
Koszt można wyświetlić w rozliczeniu miesięcznym lub rocznym. Dowiedz się więcej o [obsługiwanych regionach docelowych](./site-recovery-hyper-v-deployment-planner-cost-estimation.md#supported-target-regions) i [obsługiwanych walutach](./site-recovery-hyper-v-deployment-planner-cost-estimation.md#supported-currencies).

**Koszt według składników**: całkowity koszt odzyskiwania po awarii jest dzielony na cztery składniki: obliczenia, magazyn, sieć i koszt licencji usługi Azure Site Recovery. Koszt jest obliczany na podstawie wykorzystania powstałego podczas replikacji oraz w czasie testowania odzyskiwania po awarii dla mocy obliczeniowych, magazynu (warstwa Premium i Standardowa), usługi ExpressRoute/sieci VPN skonfigurowanej między lokacją lokalną i platformą Azure oraz dla licencji usługi Azure Site Recovery.

**Koszt według stanów**: łączny koszt odzyskiwania po awarii (DR) jest dzielony na kategorie na podstawie dwóch różnych stanów — replikacji i testowania odzyskiwania po awarii. 

**Koszt replikacji**: koszt, który zostanie naliczony podczas replikacji. Obejmuje on koszt magazynu, użycia sieci i licencji usługi Azure Site Recovery. 

**Koszt testowania odzyskiwania po awarii**: koszt, który zostanie naliczony podczas testów pracy w trybie failover. Usługa Azure Site Recovery uruchamia maszyny wirtualne podczas testu pracy w trybie failover. Koszt testowania odzyskiwania po awarii obejmuje koszt magazynu i mocy obliczeniowej działających maszyn wirtualnych. 

**Koszt magazynu platformy Azure na miesiąc/rok**: obejmuje łączny koszt magazynu, który zostanie naliczony dla magazynów w warstwie Premium i Standardowa podczas replikacji i testowania odzyskiwania po awarii.
W arkuszu [Szacowanie kosztów](site-recovery-hyper-v-deployment-planner-cost-estimation.md) możesz wyświetlić szczegółową analizę kosztów dla poszczególnych maszyn wirtualnych.

### <a name="growth-factor-and-percentile-values-used"></a>Używane wartości współczynnika wzrostu i percentyla
W tej sekcji w dolnej części arkusza pokazano wartość percentyla używaną przez wszystkie liczniki wydajności profilowanych maszyn wirtualnych (domyślnie jest używany 95. percentyl) i współczynnik wzrostu (wartość domyślna to 30 procent) używany we wszystkich obliczeniach.

![Używane wartości współczynnika wzrostu i percentyla](media/site-recovery-hyper-v-deployment-planner-run/growth-factor-max-percentile-value.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Zalecenia dotyczące danych wejściowych w postaci dostępnej przepustowości
![Omówienie profilowania przy użyciu danych wejściowych przepustowości](media/site-recovery-hyper-v-deployment-planner-analyze-report/profiling-overview-bandwidth-input-h2a.png)

Może wystąpić sytuacja, w której nie można ustawić przepustowości większej niż x Mb/s na potrzeby replikacji usługi Azure Site Recovery. Narzędzie umożliwia wprowadzenie dostępnej przepustowości (za pomocą parametru -Bandwidth podczas generowania raportu) i uzyskać osiągalny cel punktu odzyskiwania w minutach. Osiągalna wartość celu punktu odzyskiwania pozwala zdecydować, czy trzeba aprowizować dodatkową przepustowość, czy rozwiązanie odzyskiwania po awarii może używać tego celu punktu odzyskiwania.

![Osiągalna wartość celu punktu odzyskiwania](media/site-recovery-hyper-v-deployment-planner-analyze-report/achivable-rpo-h2a.PNG)

## <a name="vm-storage-placement-recommendation"></a>Zalecenie dotyczące rozmieszczenia maszyny wirtualnej względem magazynu 

![Rozmieszczenie maszyny wirtualnej względem magazynu](media/site-recovery-hyper-v-deployment-planner-analyze-report/vm-storage-placement-h2a.png)

**Typ magazynu dysków**: konto magazynu w warstwie Standardowa lub Premium używane do replikacji wszystkich odpowiednich maszyn wirtualnych wymienionych w kolumnie **Maszyny wirtualne do rozmieszczenia**.

**Sugerowany prefiks**: proponowany 3-znakowy prefiks, którego można użyć w nazwie konta magazynu. Możesz użyć własnego prefiksu, ale propozycja narzędzia będzie zgodna z [konwencją nazewnictwa partycji dla kont magazynu](https://aka.ms/storage-performance-checklist).

**Sugerowana nazwa konta**: nazwa konta magazynu po uwzględnieniu proponowanego prefiksu. Zastąp nazwę w nawiasach kątowych (< i >) niestandardowymi danymi wejściowymi.

**Konto magazynu dzienników**: wszystkie dzienniki replikacji są przechowywane na standardowym koncie magazynu. W przypadku maszyn wirtualnych replikowanych do konta magazynu w warstwie Premium skonfiguruj dodatkowe konto magazynu w warstwie Standardowa na potrzeby magazynu dzienników. Jedno konto magazynu dzienników w warstwie Standardowa może być używane przez wiele kont magazynu replikacji w warstwie Premium. Maszyny wirtualne replikowane do kont magazynu w warstwie Standardowa używają tego samego konta magazynu dla dzienników.

**Sugerowana nazwa konta dzienników**: nazwa konta dzienników magazynu po uwzględnieniu proponowanego prefiksu. Zastąp nazwę w nawiasach kątowych (< i >) niestandardowymi danymi wejściowymi.

**Podsumowanie rozmieszczania**: podsumowanie łącznego obciążenia maszyn wirtualnych na koncie magazynu podczas replikacji i pracy w trybie failover lub testu pracy w trybie failover. Obejmuje ono łączną liczbę maszyn wirtualnych mapowanych na konto magazynu, łączną liczbę operacji we/wy odczytu i zapisu na sekundę dla wszystkich maszyn wirtualnych umieszczanych na tym koncie magazynu, łączną liczbę operacji we/wy zapisu na sekundę (replikacja), łączny skonfigurowany rozmiar wszystkich dysków oraz łączną liczbę dysków.

**Maszyny wirtualne do rozmieszczenia**: lista wszystkich maszyn wirtualnych, które powinny zostać umieszczone na danym koncie magazynu w celu uzyskania optymalnej wydajności i użycia.

## <a name="compatible-vms"></a>Zgodne maszyny wirtualne
Raport programu Microsoft Excel generowany przez planistę wdrożenia usługi Azure Site Recovery zawiera szczegóły wszystkich zgodnych maszyn wirtualnych w arkuszu „Zgodne maszyny wirtualne”.

![Zgodne maszyny wirtualne](media/site-recovery-hyper-v-deployment-planner-analyze-report/compatible-vms-h2a.png)

**Nazwa maszyny wirtualnej**: nazwa maszyny wirtualnej używana w pliku VMListFile podczas generowania raportu. Ta kolumna obejmuje też dyski (VHD) dołączone do maszyn wirtualnych. Nazwy obejmują nazwy hostów funkcji Hyper-V, na których zostały rozmieszczone maszyny wirtualne po tym, jak narzędzie odnalazło je w trakcie okresu profilowania.

**Zgodność maszyny wirtualnej**: wartości to **Tak** i **Tak**\*. Wartość **Tak**\* jest przeznaczona dla wystąpień, w których maszyna wirtualna odpowiada usłudze [Azure Premium Storage](https://aka.ms/premium-storage-workload). Tutaj profilowany dysk o wysokim współczynniku zmian lub dużej liczbie operacji we/wy na sekundę pasuje do rozmiaru dysku w warstwie Premium większego niż rozmiar mapowany do dysku. Decyzja o tym, do którego typu dysku magazynu Premium będzie mapowany dysk, jest podejmowana na podstawie jego rozmiaru na poziomie konta magazynu. 
* Mniej niż 128 GB — P10.
* 128 GB do 256 GB — P15.
* 256 GB do 512 GB — P20.
* 512 GB do 1024 GB — P30.
* 1025 GB do 2048 GB — P40.
* 2049 GB do 4095 GB — P50.

Na przykład jeśli charakterystyki obciążenia dysku powodują umieszczenie go w kategorii P20 lub P30, ale z powodu rozmiaru jest mapowany w dół do niższego typu magazynu Premium, narzędzie oznacza daną maszynę wirtualną jako **Tak**\*. Narzędzie zaleca również zmianę rozmiaru dysku źródłowego tak, aby mieścił się w zalecanym typie dysku Premium Storage lub zmianę docelowego typu dysku po zakończeniu pracy w trybie failover.

**Typ magazynu**: dostępne typy magazynu to Standardowa i Premium.

**Sugerowany prefiks**: 3-znakowy prefiks konta magazynu.

**Konto magazynu**: nazwa uwzględniająca proponowany prefiks konta magazynu.

**Szczytowa liczba operacji we/wy odczytu i zapisu na sekundę (ze współczynnikiem wzrostu)**: liczba operacji we/wy odczytu i zapisu na sekundę dla szczytowego obciążenia na dysku (domyślnie jest używany 95. percentyl) wraz z przyszłym współczynnikiem wzrostu (wartość domyślna to 30%). Pamiętaj, że łączna liczba operacji we/wy odczytu i zapisu maszyny wirtualnej nie zawsze jest sumą operacji we/wy odczytu i zapisu z poszczególnych dysków maszyny wirtualnej, ponieważ szczytowa liczba operacji we/wy odczytu i zapisu maszyny wirtualnej to wartość szczytowa sumy operacji we/wy odczytu i zapisu poszczególnych dysków z każdej minuty okresu profilowania.

**Szczytowa wartość współczynnika zmian danych w MB/s (ze współczynnikiem wzrostu)**: szczytowy współczynnik zmian danych na dysku (domyślnie jest używany 95. percentyl) wraz z przyszłym współczynnikiem wzrostu (wartość domyślna to 30%). Pamiętaj, że łączny współczynnik zmian danych maszyny wirtualnej nie zawsze jest sumą współczynników zmian danych z poszczególnych dysków maszyny wirtualnej, ponieważ szczytowy współczynnik zmian danych maszyny wirtualnej to wartość szczytowa sumy współczynników zmian poszczególnych dysków z każdej minuty okresu profilowania.

**Rozmiar maszyny wirtualnej platformy Azure**: idealnie zamapowany rozmiar maszyny wirtualnej usług Azure Cloud Services dla tej lokalnej maszyny wirtualnej. Mapowanie jest oparte na wielkości pamięci, liczbie dysków/rdzeni/kart sieciowych oraz liczbie operacji we/wy zapisu i odczytu lokalnej maszyny wirtualnej. Zawsze zalecany jest najmniejszy rozmiar maszyny wirtualnej platformy Azure zgodny ze wszystkimi charakterystykami lokalnej maszyny wirtualnej.

**Liczba dysków**: łączna liczba dysków (VHD) na maszynie wirtualnej.

**Rozmiar dysku (GB)**: łączny rozmiar wszystkich dysków maszyny wirtualnej. W narzędziu jest też wyświetlany rozmiar poszczególnych dysków maszyny wirtualnej.

**Rdzenie**: liczba rdzeni procesora CPU maszyny wirtualnej.

**Pamięć (MB)**: pamięć RAM maszyny wirtualnej.

**Karty sieciowe**: liczba kart sieciowych maszyny wirtualnej.

**Typ rozruchu**: typ rozruchu maszyny wirtualnej. Dozwolone wartości to BIOS i EFI.

## <a name="incompatible-vms"></a>Niezgodne maszyny wirtualne
Raport programu Microsoft Excel generowany przez planistę wdrożenia usługi Azure Site Recovery zawiera szczegóły wszystkich niezgodnych maszyn wirtualnych w arkuszu „Niezgodne maszyny wirtualne”.

![Niezgodne maszyny wirtualne](media/site-recovery-hyper-v-deployment-planner-analyze-report/incompatible-vms-h2a.png)

**Nazwa maszyny wirtualnej**: nazwa maszyny wirtualnej używana w pliku VMListFile podczas generowania raportu. Ta kolumna obejmuje też dyski (VHD) dołączone do maszyn wirtualnych. Nazwy obejmują nazwy hostów funkcji Hyper-V, na których zostały rozmieszczone maszyny wirtualne po tym, jak narzędzie odnalazło je w trakcie okresu profilowania.

**Zgodność maszyny wirtualnej**: wskazuje, dlaczego dana maszyna wirtualna nie jest zgodna na potrzeby użycia z usługą Azure Site Recovery. Niezgodność każdego dysku na podstawie opublikowanych [limitów magazynów](https://aka.ms/azure-storage-scalbility-performance) może wynikać z dowolnej spośród następujących przyczyn:

* Rozmiar dysku jest większy niż 4095 GB. Usługa Azure Storage obecnie nie obsługuje dysków danych większych niż 4095 GB.

* Dysk systemu operacyjnego jest większy niż 2047 GB dla maszyny wirtualnej 1. generacji (typ rozruchu: BIOS).  W przypadku maszyn wirtualnych 1. generacji usługa Azure Site Recovery nie obsługuje rozmiaru dysku systemu operacyjnego większego niż 2047 GB.

* Dysk systemu operacyjnego jest większy niż 300 GB dla maszyny wirtualnej 2. generacji (typ rozruchu: EFI). W przypadku maszyn wirtualnych 2. generacji usługa Azure Site Recovery nie obsługuje rozmiaru dysku systemu operacyjnego większego niż 300 GB.

* Nazwy maszyn wirtualnych zawierające dowolny spośród następujących znaków: “” [] `nie są obsługiwane.  Narzędzie nie może pobrać profilowanych danych maszyn wirtualnych, których nazwy zawierają dowolne spośród tych znaków. 

* Dysk VHD jest udostępniany między co najmniej dwiema maszynami wirtualnymi. Platforma Azure nie obsługuje maszyn wirtualnych z udostępnionym dyskiem VHD.

* Maszyna wirtualna z wirtualnym protokołem Fiber Channel nie jest obsługiwana. Usługa Azure Site Recovery nie obsługuje maszyn wirtualnych z wirtualnym protokołem Fiber Channel.

* Klaster funkcji Hyper-V nie zawiera brokera replikacji. Usługa Azure Site Recovery nie obsługuje maszyny wirtualnej w klastrze funkcji Hyper-V, jeśli nie skonfigurowano brokera repliki funkcji Hyper-V dla klastra.

* Maszyna wirtualna nie jest wysoko dostępna. Usługa Azure Site Recovery nie obsługuje maszyny wirtualnej węzła klastra funkcji Hyper-V, którego dyski VHD są przechowywane na dysku lokalnym, a nie na dysku klastra. 

* Łączny rozmiar maszyny wirtualnej (suma replikacji i testu pracy w trybie failover) przekracza obsługiwany limit rozmiaru konta usługi Storage w wersji Premium (35 TB). Ta niezgodność występuje przeważnie, jeśli wartość charakterystyki wydajności pojedynczego dysku maszyny wirtualnej przekracza maksymalny obsługiwany limit standardowego magazynu platformy Azure lub usługi Azure Site Recovery. Takie wystąpienie powoduje przeniesienie do strefy magazynów Premium Storage. Jednak maksymalny obsługiwany rozmiar konta magazynu Premium Storage jest równy 35 TB i jedna chroniona maszyna wirtualna nie może być chroniona na wielu kontach magazynu. Zauważ również, że przeprowadzenie testu pracy w trybie failover na chronionej maszynie wirtualnej, jeśli na potrzeby testu pracy w trybie failover skonfigurowano dysk niezarządzany, powoduje również uruchomienie go na koncie magazynu z trwającą replikacją. W tym wystąpieniu dodatkowa wymagana ilość miejsca w magazynie jest taka sama jak w przypadku replikacji. Dzięki temu replikacja będzie kontynuowana i równocześnie test pracy w trybie failover zakończy się sukcesem. W przypadku skonfigurowania dysku zarządzanego na potrzeby testu pracy w trybie failover nie trzeba będzie uwzględniać dodatkowego miejsca dla maszyny wirtualnej testu pracy w trybie failover.

* Źródłowe operacje we/wy na sekundę przekraczają obsługiwany limit operacji we/wy na sekundę magazynu wynoszący 7500 operacji na dysk.

* Źródłowe operacje we/wy na sekundę przekraczają obsługiwany limit operacji we/wy na sekundę maszyny wirtualnej wynoszący 80 000 operacji na dysk.

* Średni współczynnik zmian danych źródłowej maszyny wirtualnej przekracza obsługiwany limit współczynnika zmian danych usługi Azure Site Recovery wynoszący 10 MB/s dla średniego rozmiaru operacji we/wy.

* Średnia liczba operacji we/wy zapisu na sekundę maszyny wirtualnej przekracza obsługiwany limit operacji we/wy na sekundę usługi Azure Site Recovery równy 840 operacji.

* Obliczony magazyn migawek przekracza obsługiwany limit magazynu migawek wynoszący 10 TB.

**Szczytowa wartość operacji we/wy odczytu i zapisu na sekundę (ze współczynnikiem wzrostu)**: liczba operacji we/wy na sekundę dla szczytowego obciążenia na dysku (domyślnie jest używany 95. percentyl) wraz z przyszłym współczynnikiem wzrostu (wartość domyślna to 30%). Pamiętaj, że łączna liczba operacji we/wy odczytu i zapisu maszyny wirtualnej nie zawsze jest sumą operacji we/wy odczytu i zapisu z poszczególnych dysków maszyny wirtualnej, ponieważ szczytowa liczba operacji we/wy odczytu i zapisu maszyny wirtualnej to wartość szczytowa sumy operacji we/wy odczytu i zapisu poszczególnych dysków z każdej minuty okresu profilowania.

**Szczytowa wartość współczynnika zmian danych w MB/s (ze współczynnikiem wzrostu)**: szczytowy współczynnik zmian danych na dysku (domyślnie jest używany 95. percentyl) wraz z przyszłym współczynnikiem wzrostu (wartość domyślna to 30%). Pamiętaj, że łączny współczynnik zmian danych maszyny wirtualnej nie zawsze jest sumą współczynników zmian danych z poszczególnych dysków maszyny wirtualnej, ponieważ szczytowy współczynnik zmian danych maszyny wirtualnej to wartość szczytowa sumy współczynników zmian poszczególnych dysków z każdej minuty okresu profilowania.

**Liczba dysków**: łączna liczba dysków VHD maszyny wirtualnej.

**Rozmiar dysku (GB)**: łączny skonfigurowany rozmiar wszystkich dysków maszyny wirtualnej. W narzędziu jest też wyświetlany rozmiar poszczególnych dysków maszyny wirtualnej.

**Rdzenie**: liczba rdzeni procesora CPU maszyny wirtualnej.

**Pamięć (MB)**: wielkość pamięci RAM maszyny wirtualnej.

**Karty sieciowe**: liczba kart sieciowych maszyny wirtualnej.

**Typ rozruchu**: typ rozruchu maszyny wirtualnej. Dozwolone wartości to BIOS i EFI.

## <a name="azure-site-recovery-limits"></a>Limity usługi Azure Site Recovery
W poniższej tabeli przedstawiono limity usługi Azure Site Recovery. Limity te są oparte na naszych testach, ale nie obejmują wszystkich możliwych kombinacji operacji we/wy aplikacji. Rzeczywiste wyniki mogą różnić w zależności od kombinacji operacji we/wy aplikacji. Aby uzyskać najlepsze wyniki nawet po zakończeniu planowania wdrożenia, zawsze zalecamy dokładne przetestowanie aplikacji przy użyciu testu pracy w trybie failover w celu uzyskania prawdziwych informacji o wydajności aplikacji.
 
**Cel magazynu replikacji** | **Średni rozmiar operacji we/wy maszyny wirtualnej** |**Średni współczynnik zmian danych źródłowej maszyny wirtualnej** | **Łączny współczynnik zmian danych źródłowej maszyny wirtualnej dziennie**
---|---|---|---
Standard Storage | 8 KB | 2 MB/s na maszynę wirtualną | 168 GB na maszynę wirtualną
Premium Storage | 8 KB  | 5 MB/s na maszynę wirtualną | 421 GB na maszynę wirtualną
Premium Storage | 16 KB lub więcej| 10 MB/s na maszynę wirtualną | 842 GB na maszynę wirtualną

Limity te są średnimi wartościami przy założeniu 30-procentowego nakładania się operacji we/wy. Usługa Azure Site Recovery może obsługiwać większą przepływność na podstawie zakresu nakładania się na siebie, większego rozmiaru operacji zapisu i rzeczywistego zachowania związanego z obciążeniem operacji we/wy. Poprzednie liczby zakładają typowe zaległości wynoszące około pięć minut. Oznacza to, że przekazane dane są przetwarzane i punkt odzyskiwania jest tworzony w ciągu pięciu minut.

## <a name="on-premises-storage-requirement"></a>Wymagania dotyczące magazynu lokalnego

Arkusz zawiera informacje o łącznym wymaganym wolnym miejscu w magazynie dla każdego woluminu serwerów funkcji Hyper-V (gdzie znajdują się dyski VHD) na potrzeby pomyślnego ukończenia replikacji początkowej i replikacji różnicowej. Przed włączeniem replikacji dodaj wymagane miejsce do magazynowania na woluminach, aby zapewnić, że replikacja nie spowoduje żadnych niepożądanych przestojów aplikacji produkcyjnych. 

Planista wdrożenia usługi Azure Site Recovery identyfikuje optymalne wymagane miejsce do magazynowania w oparciu o rozmiar dysków VHD i przepustowość sieci używaną podczas replikacji.

![wymagania dotyczące magazynu lokalnego](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-storage-requirement-h2a.png)

### <a name="why-do-i-need-free-space-on-the-hyper-v-server-for-the-replication"></a>Dlaczego trzeba mieć wolne miejsca na serwerze funkcji Hyper-V podczas replikacji?
* Po włączeniu replikacji maszyny wirtualnej usługa Azure Site Recovery tworzy migawkę każdego dysku VHD maszyny wirtualnej na potrzeby replikacji początkowej (IR). W czasie replikacji początkowej nowe zmiany są zapisywane na dyskach przez aplikację. Usługa Azure Site Recovery śledzi te zmiany różnicowe w plikach dziennika, które wymagają dodatkowego miejsca do magazynowania.  Do momentu ukończenia replikacji początkowej pliki dziennika są przechowywane lokalnie. Jeśli nie ma wystarczającej ilości miejsca dla plików dziennika i migawki (AVHDX), replikacja przejdzie w tryb ponownej synchronizacji i nigdy nie zostanie ukończona. W najgorszym przypadku potrzeba będzie 100% dodatkowego wolnego miejsca dla rozmiaru dysku VHD na potrzeby replikacji początkowej.
* Po zakończeniu replikacji początkowej rozpoczyna się replikacja różnicowa. Usługa Azure Site Recovery śledzi te zmiany różnicowe w plikach dziennika przechowywanych w woluminie, w którym znajdują się dyski VHD maszyny wirtualnej. Te pliki dziennika są replikowane na platformie Azure ze skonfigurowaną częstotliwością kopiowania. W zależności od dostępnej przepustowości sieci replikowanie plików dziennika na platformie platformy Azure może potrwać pewien czas. Jeśli ilość wolnego miejsca jest niewystarczająca do przechowywania plików dziennika, replikacja zostanie wstrzymana, a stan replikacji maszyny wirtualnej zmieni się na wymaganą ponowną synchronizację.
* Jeśli przepustowość sieci jest niewystarczająca do wypychania plików dziennika do platformy Azure, pliki dziennika gromadzą się na woluminie. W najgorszym przypadku, gdy rozmiar plików dziennika zwiększy się do 50% rozmiaru dysku VHD, replikacja maszyny wirtualnej przejdzie w stan wymaganej ponownej synchronizacji. W najgorszym przypadku potrzeba będzie 50% dodatkowego wolnego miejsca dla rozmiaru dysku VHD na potrzeby replikacji różnicowej.

**Host funkcji Hyper-V**: lista profilowanych serwerów funkcji Hyper-V. Jeśli serwer jest częścią klastra funkcji Hyper-V, wszystkie węzły klastra są grupowane razem.

**Wolumin (ścieżka dysku VHD)**: każdy wolumin hosta funkcji Hyper-V, na którym znajdują się dyski VHD/VHDX. 

**Dostępne wolne miejsce (GB)**: wolne miejsce dostępne na woluminie.

**Łączne wymagane miejsce do magazynowania na woluminie (GB)**: łączna ilość wolnego miejsca do magazynowania wymaganego do pomyślnego zakończenia replikacji początkowej i replikacji różnicowej. 

**Łączne dodatkowe miejsce do magazynowania magazynu do aprowizowania na woluminie na potrzeby pomyślnego zakończenia replikacji**: zalecane łączne dodatkowe miejsce, które należy aprowizować na woluminie, aby zapewnić pomyślne zakończenie replikacji początkowej i replikacji różnicowej.

## <a name="initial-replication-batching"></a>Dzielenie replikacji początkowej na partie 

### <a name="why-do-i-need-initial-replication-ir-batching"></a>Dlaczego należy podzielić replikację początkową na partie?
Jeśli wszystkie maszyny wirtualne są chronione w tym samym czasie, wymagane wolne miejsce może być znacznie większe. Jeśli ilość miejsca do magazynowania jest niewystarczająca, replikacja maszyn wirtualnych przejdzie w tryb ponownej synchronizacji. Ponadto przepustowość sieci wymagana do pomyślnego ukończenia replikacji początkowej wszystkich maszyn wirtualnych jednocześnie może być znacznie większa. 

### <a name="initial-replication-batching-for-a-selected-rpo"></a>Dzielenie replikacji początkowej na partie dla wybranego celu punktu odzyskiwania replikacji początkowej
Ten arkusz zawiera szczegółowy widok każdej partii dla replikacji początkowej (IR). Dla każdego celu puntu odzyskiwania jest tworzony oddzielny arkusz dzielenia replikacji początkowej na partie. 

Jeśli zostanie wykonane zalecenie dotyczące wymaganego magazynu lokalnego dla każdego woluminu, główną informacją wymaganą do replikowania będzie lista maszyn wirtualnych, które mogą być chronione równolegle. Te maszyny wirtualne są grupowane razem w ramach partii. Może istnieć wiele partii. Maszyny wirtualne należy obejmować ochroną w podanej kolejności partii. Najpierw należy włączyć ochronę maszyn wirtualnych w partii 1, po zakończeniu replikacji początkowej ochronę maszyn wirtualnych partii 2 itd. Ten arkusz zawiera listę partii i odpowiadających im maszyn wirtualnych. 

![Szczegóły dzielenia replikacji początkowej na partie 1](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-for-rpo-h2a.png)
![Szczegóły dzielenia replikacji początkowej na partie 2](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-for-rpo2-h2a.png)

### <a name="each-batch-provides-the-following-information"></a>Każda partia udostępnia następujące informacje: 
**Host funkcji Hyper-V**: host funkcji Hyper-V maszyny wirtualnej do objęcia ochroną.
Maszyna wirtualna: maszyna wirtualna do objęcia ochroną. 

**Komentarze**: jeśli w przypadku określonego woluminu maszyny wirtualnej wymagane jest wykonanie akcji, w tym miejscu znajduje się komentarz.  Jeśli na przykład ilość wolnego miejsca dostępnego na woluminie jest niewystarczająca, tekst komentarza jest następujący: Dodaj dodatkowy magazyn, aby chronić tę maszynę wirtualną.

**Wolumin (ścieżka dysku VHD)**: nazwa woluminu, na którym znajdują się dyski VHD maszyny wirtualnej. Wolne miejsce dostępne na woluminie (GB): wolne miejsce dostępne na woluminie dla maszyny wirtualnej. Podczas obliczania wolnego miejsca dostępnego na woluminach jest uwzględniane miejsce na dysku używane do replikacji różnicowej przez maszyny wirtualne z poprzednich partii, których dyski VHD znajdują się na tym samym woluminie.  

Na przykład maszyny VM1, VM2 i VM3 znajdują się na woluminie E:\VHDpath. Przed replikacją wolne miejsce na woluminie wynosi 500 GB. Maszyna VM1 jest częścią partii 1, maszyna VM2 jest częścią partii 2, a maszyna VM3 jest częścią partii 3.  W przypadku maszyny VM1 dostępne wolne miejsce wynosi 500 GB. W przypadku maszyny VM2 dostępne wolne miejsce będzie wynosić 500 — miejsce na dysku wymagane dla replikacji różnicowej maszyny VM1.  Powiedzmy, że maszyna VM1 wymaga 300 GB miejsca dla replikacji różnicowej. Wolne miejsce dostępne dla maszyny VM2 wyniesie 500 GB - 300 GB = 200 GB.  Podobnie maszyna VM2 wymaga 300 GB dla replikacji różnicowej. Wolne miejsce dostępne dla maszyny VM3 wyniesie 200 GB - 300 GB = -100 GB.

**Magazyn na woluminie wymagany dla replikacji początkowej (GB)**: wolne miejsce do magazynowania wymagane na woluminie dla maszyny wirtualnej do pomyślnego zakończenia replikacji początkowej i replikacji różnicowej.

**Magazyn na woluminie wymagany dla replikacji różnicowej (GB)**: wolne miejsce do magazynowania wymagane na woluminie dla maszyny wirtualnej do pomyślnego zakończenia replikacji różnicowej.

**Wymagany dodatkowy magazyn oparty na niedoborze umożliwiający uniknięcie niepowodzenia replikacji (GB)**: dodatkowe wymagane miejsce na woluminie dla maszyny wirtualnej.  Jest to maksymalna wartość wymaganego miejsca do magazynowania na potrzeby replikacji początkowej i replikacji różnicowej — wolne miejsce dostępne na woluminie.

**Minimalna przepustowość wymagana dla replikacji początkowej (Mb/s)**: minimalna przepustowość wymagana na potrzeby replikacji początkowej dla maszyny wirtualnej.

**Minimalna przepustowość wymagana dla replikacji różnicowej (Mb/s)**: minimalna przepustowość wymagana na potrzeby replikacji różnicowej dla maszyny wirtualnej.

### <a name="network-utilization-details-for-each-batch"></a>Szczegóły wykorzystania sieci dla każdej partii 
Każda tabela partii zawiera podsumowanie wykorzystania sieci przez partię.

**Przepustowość dostępna dla partii**: przepustowość dostępna dla partii po uwzględnieniu przepustowości replikacji różnicowej poprzedniej partii.

**Przybliżona przepustowość dostępna dla replikacji początkowej partii**: przepustowość dostępna dla replikacji początkowej maszyn wirtualnych w partii. 

**Przybliżona przepustowość wykorzystana dla replikacji różnicowej partii**: przepustowość potrzebna do replikacji różnicowej maszyn wirtualnych w partii. 

**Szacowany czas replikacji początkowej dla partii (GG:MM)**: szacowany czas replikacji początkowej w formacie godziny:minuty.

## <a name="cost-estimation"></a>Szacowanie kosztów
Dowiedz się więcej na temat [szacowania kosztów](site-recovery-hyper-v-deployment-planner-cost-estimation.md). 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [szacowania kosztów](site-recovery-hyper-v-deployment-planner-cost-estimation.md).